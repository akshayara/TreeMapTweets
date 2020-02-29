<template>
    <div>
        <svg
        id="my_dataTime"
        :width="this.width"
        :height="this.height" >
            <g id="clock-face"
                :transform="overallTransform">
                <line
                v-for="(line, index) in this.rangeFirst"
                    :key="index + line + '-line'"
                    :x1="0"
                    :x2="0"
                    :y1="secondTickStart"
                    :y2="secondTickStart + secondTickLength"
                    :transform="'rotate(' +secondScale(line) + ')'"
                    class=".second-tick"
                >
                </line>
                <text
                    v-for="(secTxt, index) in this.rangeSecond"
                    :key="index + secTxt + '-text'"
                    :x="xValSec(secTxt)"
                    :y="yValSec(secTxt)"
                    class=".second-label"
                >
                    {{ secTxt }}
                </text>
                <line
                v-for="(hour, index) in this.rangeThird"
                    :key="index + hour + '-hour'"
                    :x1="0"
                    :x2="0"
                    :y1="hourTickStart"
                    :y2="hourTickStart + hourTickLength"
                    :transform="'rotate(' + hourScale(hour) + ')'"
                    class=".hour-tick"
                >
                </line>
                <text
                    v-for="(hoursTxt, index) in this.rangeFourth"
                    :key="index + hoursTxt + '-hours'"
                    :x="xValHours(hoursTxt)"
                    :y="yValHours(hoursTxt)"
                    class=".hour-label"
                >
                    {{ hoursTxt }}
                </text>
            </g>
            <g id="clock-hands" :transform="overallTransform">
                <line
                    v-for="(data, index) in this.handData"
                    :key="index + data + '-data'"
                    :class="data.type + '-hand'"
                    :x1="0"
                    :y1="data.balance ? data.balance : 0"
                    :x2="0"
                    :y2="data.length"
                    :transform="'rotate(' + handTransform(data) + ')'"
                    >
                </line>
            </g>
            <g id="face-overlay" :transform="overallTransform">
                <circle
                    :x="0"
                    :y="0"
                    :r="(this.clockRadius/20)">
                </circle>
            </g>
            <g class="hourScale-draw">
            </g>
            <g class="minuteScale-draw">
            </g>
        </svg>
    </div>
</template>
<script>    
import * as d3 from 'd3'
export default {
    props: {
    },
    data() {
        return{
            radians: 0.0174532925,
            clockRadius: 200,
            margin: 50,
            secondHandBalance: 30,
            secondTickLength: -10,
            hourTickLength: -18,
            secondLabelYOffset: 5,
            hourLabelYOffset: 7,
            seconds: 0,
            minutes: 0,
            hours: 0
        }
    },
    mounted(){
        setInterval(()=>{
            this.updateData()
        }, 1000);
    },    
    computed: {
        handData: function() {
            return [
                {
                    type: 'hour',
                    value: this.hours,
                    length: -this.hourHandLength,
                    scale: this.hourScale
                },
                {
                    type: 'minute',
                    value: this.minutes,
                    length: -this.minuteHandLength,
                    scale: this.minuteScale
                },
                {
                    type: 'second',
                    value: this.seconds,
                    length: -this.secondHandLength,
                    scale: this.secondScale,
                    balance: this.secondHandBalance
                }
            ] 
        },
        width: function(){
            return (this.clockRadius + this.margin)*2
        },
        height: function(){
            return (this.clockRadius + this.margin)*2
        },
        hourHandLength: function()
        {
            return 2*this.clockRadius/3
        },
        minuteHandLength: function()
        {
            return this.clockRadius
        },
        secondHandLength: function()
        {
            return this.clockRadius-12
        },
        secondTickStart: function()
        {
            return this.clockRadius
        },
        hourTickStart: function()
        {
            return this.clockRadius
        },
        secondLabelRadius: function()
        {
            return this.clockRadius + 16
        },
        hourLabelRadius: function()
        {
            return this.clockRadius - 40
        },
        xValSec: function(){
            return function (d) {
                return this.secondLabelRadius * Math.sin(this.secondScale(d) * this.radians)
            }
        },
        yValSec: function(){
            return function (d) {
                return -this.secondLabelRadius*Math.cos(this.secondScale(d) * this.radians) + this.secondLabelYOffset
            }
        },
        xValHours: function(){
            return function (d) {
                return this.hourLabelRadius*Math.sin(this.hourScale(d) * this.radians)
            }
        },
        yValHours: function(){
            return function (d) {
                return -this.hourLabelRadius*Math.cos(this.hourScale(d) * this.radians) + this.hourLabelYOffset
            }
        },
        rangeFirst: function(){
            return d3.range(0,60);
        },
        rangeSecond: function(){
            return d3.range(5,61,5)
        },
        rangeThird: function(){
            return d3.range(0,12)
        },
        rangeFourth: function(){
            return d3.range(3,13,3)
        },
        secondScale: function(){
            return d3.scaleLinear()
            .range([0,354])
            .domain([0,59])
        },
        minuteScale: function(){
            return d3.scaleLinear()
            .range([0,354])
            .domain([0,59])
        },
        hourScale: function(){
            return d3.scaleLinear()
            .range([0,330])
            .domain([0,11]);
        },
        handTransform: function() {
            return function (hand) {
                return hand.scale.apply(null, [hand.value])
            }
        },
        overallTransform: function() {
            return 'translate(' + (this.clockRadius + this.margin) + ','
                + (this.clockRadius + this.margin) + ')'
        }

    },
    methods: {
        drawHourScale: function(){
            d3.select(".hourScale-draw").call(this.hourScale)

        },
        drawMinuteScale: function(){
            d3.select(".minuteScale-draw").call(this.minuteScale)

        },
        updateData: function(){
            let t = new Date();
            this.hours = (t.getHours() % 12) + t.getMinutes()/60 
            this.minutes = t.getMinutes()
            this.seconds = t.getSeconds()
            
        }
    }
    
}
</script>
<style>
body {
  background: #fff;
}

svg{
	stroke: #000;
	font-family: "HelveticaNeue-Light", "Helvetica Neue Light", "Helvetica Neue", Helvetica, Arial, "Lucida Grande", sans-serif; 
}

#rim {
  fill: none;
  stroke: #999;
  stroke-width: 3px;
}

.second-hand{
	stroke-width:3;

}

.minute-hand{
	stroke-width:8;
	stroke-linecap:round;
}

.hour-hand{
	stroke-width:12;
	stroke-linecap:round;
}

.hands-cover{
	stroke-width:3;
	fill:#fff;
}

.second-tick{
	stroke-width:3;
	fill:#000;	
}

.hour-tick{
	stroke-width:8; 
}

.second-label{
	font-size: 12px;
}

.hour-label{
	font-size: 24px;
}



</style>
