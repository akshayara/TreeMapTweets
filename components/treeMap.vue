<template>
    <div>
        <svg
            id="treeMapViz"
            :viewBox='[0, 0, width, height]'
            class="viewBoxStyle" 
            >
            <g 
                v-for="(leaf, index) in this.treeMapLeaves"
                    :key="index"
                    :transform="'translate(' + leaf.x0 + ',' + leaf.y0 +')'"
                    >
                <text class="viewBoxStyle"> 
                    {{ titleText(leaf) }}
                </text>
                <rect
                    :id="index+'leaf'"
                    :width="leaf.x1 - leaf.x0"
                    :height="leaf.y1 - leaf.y0"
                    class="rectStyle">
                </rect>
                <circle
                    v-for="(user, index) in leaf.data.value"
                    :key="index"
                    :cx="circleXPos(leaf)"
                    :cy="circleYPos(leaf)"
                    :r=10>
                </circle>  
            </g>
        </svg>
    </div>    
</template>
<script >
import * as d3 from 'd3'
export default {
    data(){
        return {}
    },
    props:{
        width: {
            type: Number,
            default: 1000
        },
        height: {
            type: Number,
            default: 1000
        },
        users: {
            type: Object,
            default: function() {
                return {}
            }
        },
        temp: {
            type: Array,
            default: () => []
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
        },
        locationObj: function(){
            const endResult = []

            //Iterate the array of location objects to get the array of countries
            for(const loc of this.temp.map(a => a.location)){
                const filteredArray = endResult.filter(o => o.country === loc.country)
                if(filteredArray.length === 0)
                    endResult.push({
                        country: loc.country,
                        children: [{name: loc.state, value:0}]
                    })
                const foundCountry = endResult.filter(o => o.country === loc.country)[0]
                const foundIndex = foundCountry.children.findIndex(c => c.name === loc.state)
                if (foundCountry.children[foundIndex])
                    foundCountry.children[foundIndex].value++
            }    
            
            return {
                name: 'All',
                children: endResult
            }
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
        },
        rectColor: function(d){
            while(d.depth >1)
                d=d.parent;
                return d3.color(d.data.name)
        },
        titleText: function(d){
            let txt = d.ancestors().reverse().map(d => d.data.name)
            let formatTxt = d3.format(d.value)
            return txt + formatTxt
        },
        circleXPos: function(d){
            return (d.x1-d.x0)/2
        },
        circleYPos: function(d){
            return (d.y1-d.y0)/2
        }
    }
}
</script>
<style>
.viewBoxStyle {
    font-size: 10px;
    font: sans-serif    
}
.rectStyle {
    fill: #000ff0;
    fill-opacity: 0.25;
    stroke: #0000;
    stroke-width: 3px;
}
</style>