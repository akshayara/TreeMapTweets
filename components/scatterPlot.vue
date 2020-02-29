<template>
    <svg
          id="my_dataviz"
          :width= '(this.width + this.margin.left + this.margin.right)'
          :height= '(this.height +this.margin.top + this.margin.bottom)'>
        <g class="axis-x"
          :transform="'translate(' + this.margin.left + ',' + this.height + ')'"
        >
        </g>
        <g class="axis-y"
          :transform="'translate(' + this.margin.left + ',' + this.margin.top + ')'"
        >
        </g>
        <g
          :transform="'translate(' + this.margin.left + ', '+ this.margin.top +')'"
          class="circleGrp">
          <circle
            v-for="(point, index) in dots"
            :key="index"
            :cx="xScale(point.x)"
            :cy="yScale(point.y)"
            :r=10
          ></circle>
        </g>
      </svg>    
</template>

<script>
import * as d3 from 'd3'
export default {
    props: {
        width: {
            type: Number,
            default: 370
        },
        height: {
            type: Number,
            default: 370
        },
        margin: {
            type: Object,
            default: function() {
                return {
                    top: 30,
                    right: 30,
                    left: 50,
                    bottom: 60
                }
            }
        },
        dots: {
            type: Array,
            default: function() {
                return []
            }
        }
    },
    computed: {
        plotLeft: function() {
        return this.margin.left
        },
        plotRight: function() {
        return this.width - this.margin.right
        },
        plotBottom: function() {
        return this.height - this.margin.bottom
        },
        plotTop: function() {
        return this.margin.top
        },
        plotHeight: function() {
        return this.height - this.margin.top - this.margin.bottom
        },
        plotWidth: function() {
        return this.width - this.margin.left - this.margin.right
        },
        xMin: function () {
        return d3.min(this.dots, function(d) {
            return d.x
            })
        }, 
        xMax: function () {
        return d3.max(this.dots, function(d) {
            return d.x
            })
        },
        yLabels: function () {
        return [...new Set(this.dots.map(a => a.y))]
        },
        xScale: function(){
        return d3.scaleLinear()
            .domain([this.xMin, this.xMax])
            .range([0, 370])
        },
        yScale: function(){
        return d3.scaleBand()
            .domain(this.yLabels)
            .range([0, 370])
        },
        xAxisFunc: function(){
        return d3.axisBottom(this.xScale)

        },
        yAxisFunc: function(){
        return d3.axisLeft(this.yScale)
        }
    },
    beforeUpdate() {
        this.drawAxes()
    },
    mounted: function () {
        this.drawAxes()
    },
    methods: {
        drawAxes: function(){
        d3.select(".axis-x").call(this.xAxisFunc)
        d3.select(".axis-y").call(this.yAxisFunc)
    },
    removeGroups: function(){
      let groups = ['circleGrp', 'axis-x', 'axis-y']
      for(item of groups)
        d3.select(item).remove()
    },
  }
    
}
</script>

<style scoped>

</style>