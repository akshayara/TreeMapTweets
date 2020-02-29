<template>
  <div class="container">
    <div>
      <logo :givenText="this.sample" />
      <h1 class="title">
        scatterplotusertweets
      </h1>
      <h2 class="subtitle">
        {{this.sample}}
      </h2>
      <div class="links">
        <a
          target="_blank"
          class="button--green"
          @click="generateRandomNumber"
        >
          Again!
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          class="button--grey"
        >
          GitHub
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import * as d3 from 'd3'
export default {
  name: 'ScatterPlot',

  props: {},
  data() {
    return {
      sample: null
    }
  },
  components: {
    Logo
  },
  mounted: function () {
    this.generateRandomNumber()
  },
  methods: {
    generateRandomNumber: function() {
      this.sample = Math.random() * 1000
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
