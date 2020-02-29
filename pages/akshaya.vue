<template>
  <div class="container">
    <div>
      <input type="button" id="addBtn" @click="add" value="+"/>
      <input type="button" id="subBtn" @click="sub" value = "-"/>
      <input type="Number" id="widthText" v-model="userWidth"/>
      <scatter-plot :dots="circles" :width="parseInt(userWidth)"/>
    </div>
  </div>
</template>

<script>
import scatterPlot from '~/components/scatterPlot.vue'
export default {
  name: 'index-page',
  data() {
    return {
       circles: [
        {x: 1, y: 'A'},
        {x: 2, y: 'B'},
        {x: 3, y: 'C'},
        {x: 4, y: 'D'},
        {x: 5, y: 'E'}
      ],
      userWidth: 300
      
    }
  },
  components: {
    scatterPlot
  },
  methods: {
    add: function() {
      let letters = ['A','B','C','D','E']
      let randX = Math.random()*100
      let randY = letters[Math.ceil(Math.random() * letters.length)-1]
      this.circles.push({
        x: randX,
        y: randY
      })
    },
    sub: function(){
      this.circles.splice(0,1)
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
