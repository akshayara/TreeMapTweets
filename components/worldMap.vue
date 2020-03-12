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
                    :d="sampleGeoPath()(country)"
                    :id="country.properties.name"
                    :fill="country.properties.name == selectedCountryName ? '#3B5998' : '#ccc'"
                    @mouseover="mouseOver(country.properties.name)"
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
            default: 950
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
        selectedCountryName: {
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
        },
    },
    methods: {
        sampleGeoPath: function() {
            return d3Geo.geoPath(this.projection)
        },
        mouseOver: function(countryName) {
            this.showToolTip(countryName)
            this.$emit('highlightChange', countryName)
        },
        mouseOut: function(id) {
            this.$emit('highlightChange', '')
        },
        showToolTip: function(countryName){
            console.log(countryName)
            return d3.select('#'+ countryName)
                    .style('position','absolute')
                    .style('opacity',0.9)
                    .style('visibility','visible')
                    .text(countryName)

        }
    }
}
</script>
<style>

</style>