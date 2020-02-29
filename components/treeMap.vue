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
                    :id="index+'leaf'"
                    width="20%"
                    height="20%"
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
            type: Object,
            default: function() {
                return {}
            }
        }
    },
    computed:{
        treeMapData: function(){
            let root = this.treeMapFunc(this.users)
            return root
        },
        treeMapLeaves: function(){
            let leaves = this.treeMapData.leaves()
            return leaves
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
                .sum(d => d.value)
                .sort((a, b) => b.value - a.value))
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
<style>
.viewBoxStyle{
    font-size: 10px;
    font: sans-serif 	
}
.rectStyle{
    fill: #000ff0;
    fill-opacity: 0.25;
}
</style>