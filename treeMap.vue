<template>
    <div>
        <svg
            id="treeMapViz"
            :viewBox='[0, 0, 100, 100]'
            class=".viewBoxStyle" >
            <g 
                v-for="(leaf, index) in this.treeMapLeaves"
                    :key="index"
                    :transform="'translate(' + leaf.x0 + ',' + leaf.y0 +')'"
                    >
                <rect
                    :id="index +'leaf'"
                    :width="rectWidth(leaf)"
                    :height="rectHeight(leaf)"
                    class=".rectStyle"
                >
                </rect>
            </g>
        </svg>
    </div>    
</template>
<script >
import * as d3 from 'd3'
export default {
    data(){
        return {
            width: {
                type: Number,
                default: 954
            },
            height: {
                type: Number,
                default: 954
            }
        }
    },
    props:{
        users: {
            type: Array,
            default: function() {
                return []
            }
        }
    },
    computed:{
        treeMapData: function(){
            let root = this.treeMapFunc(this.users)
            return root
        },
        treeMapLeaves: function(){
            let leaves = this.treeMapFunc(this.users).leaves()
            return leaves
        },
        countries: function(){
            const countryArr = [] 
            for(const i of this.users){
                console.log(i)
                    countryArr.push(i.location.country)
                }
            return countryArr
        },
        states: function(){
            const stateArr = [] 
            for(const i of this.users){
                    stateArr.push(i.location.state)
                }
            return stateArr
        },
        countriesLength: function(){
            return this.countries.length
        },
        statesLength: function(){
            return this.states.length
        }
    },
    methods: {
        treeMapFunc: function(da){
            const temp = d3.treemap()
                .tile(d3.treemapSquarify)
                .size([this.width,this.height])
                .padding(1)
                .round(true)
            return temp(d3.hierarchy(da)
                .sum(d => d.country)
                .sort((a, b) => b.country - a.country))
        },
        rectWidth: function(d){
            return d.x1-d.x0
        },
        rectHeight: function(d){
            return d.y1-d.y0
        }   
    }
}
</script>
<style scoped>
.viewBoxStyle{
    font-size: 10px;
    font: sans-serif 	
}
.rectStyle{
    fill: #000ff0;
}
</style>