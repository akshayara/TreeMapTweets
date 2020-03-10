<template>
    <div>
        <svg
            :width="width"
            :height="height">
            <g 
                :tranform="'translate(' + this.margin.left + ',' + this.margin.top + ')'"
                :width="this.widthScat"
                :height="this.heightScat">

            </g>
            <g id="myG">
                <path
                    v-for="(country, index) in this.countries.features"
                    :key="index"
                    fill="#ccc"
                    :d="sampleGeoPath()(country)"
                    :id="country.properties.name"
                    @mouseover="mouseOver(countryName)"
                    @mouseout="mouseOut(country.properties.name)">
                </path>
            </g>
        </svg>
    </div>
</template>
<script>
import * as d3 from 'd3'
import * as d3Geo from 'd3-geo'
import * as d3Projection from 'd3-geo-projection'
import * as d3Array from 'd3-array'

import countryList from '../static/countries.json'
export default {
    props: {
        width: {
            type: Number,
            default: 960
        },
        height: {
            type: Number,
            default: 550
        },
        margin: {
            type: Object,
            default: function() {
                return {
                    top: 5,
                    right: 5,
                    left: 5,
                    bottom: 5
                }
            }
        },
        countryName: {
            type:String,
            default: ''
        }
    },
    data: function () {
        return {
            countries: countryList,
            projection:  d3Projection.geoCylindricalStereographic(),
            svgGroup: null
        }
    },
    mounted: function(){
        this.svgGroup = d3.select('#myG')
    },
    computed: {
        widthScat: function(){
            return this.width - this.margin.left - this.margin.right
        },
        heightScat: function(){
            return this.height - this.margin.top - this.margin.bottom
        }
    },
    methods: {
        sampleGeoPath: function() {
            return d3Geo.geoPath(this.projection)
        },
        mouseOver: function(id) {
            console.log(id)
            this.svgGroup.select('#' + id).style('fill', '#3B5998')
        },
        mouseOut: function(id) {
            this.svgGroup.select('#' + id).style('fill', '#ccc')
        }
    }
}
</script>
<style scoped>

</style>