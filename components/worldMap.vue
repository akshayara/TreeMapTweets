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
            <g>
                <path
                    v-for="(country, index) in this.countries.features"
                    :key="index"
                    fill="#ccc"
                    :d="geoPath"
                    :id="country.properties.name">
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
        }
    },
    data: function () {
        return {
            countries: countryList
        }
    },
    computed: {
        widthScat: function(){
            return this.width - this.margin.left - this.margin.right
        },
        heightScat: function(){
            return this.height - this.margin.top - this.margin.bottom
        },
        projection: function(){
            d3Projection.geoCylindricalStereographic()
        },
        geoPath: function(){
            d3Geo.geoPath(this.projection)
        }
    },
    methods: {
    }
}
</script>
<style scoped>

</style>