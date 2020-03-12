<template>
    <div class="geoDiv">
        <tree-map :users="usersSet" :selectedCountryName="selectedCountryName" @highlightChange="getCountryHovered"></tree-map>
        <world-map :selectedCountryName="selectedCountryName" @highlightChange="getCountryHovered"></world-map>
    </div>
</template>
<script>
import treeMap from '~/components/treeMap.vue'
import worldMap from '~/components/worldMap.vue'
import * as d3 from 'd3'
export default {
    data(){
        return {
            usersSet: [
                { 
                    screen_name: 'a', 
                    tweets: [{}, {}, {}], 
                    profile_image_url_https: "https://i2.wp.com/www.sardiniauniqueproperties.com/wp-content/uploads/2015/10/Square-Profile-Pic-1-1.jpg",
                    location: { 
                        country: 'United States of America', 
                        state: 'WA' 
                    }
                },
                { 
                    screen_name: 'b', 
                    tweets: [{}, {}, {}], 
                    profile_image_url_https: "https://i2.wp.com/www.sardiniauniqueproperties.com/wp-content/uploads/2015/10/Square-Profile-Pic-1-1.jpg",
                    location: { 
                        country: 'United States of America', 
                        state: 'CA' 
                    } 
                },
                { 
                    screen_name: 'c', 
                    tweets: [{}, {}, {}], 
                    profile_image_url_https: "https://i2.wp.com/www.sardiniauniqueproperties.com/wp-content/uploads/2015/10/Square-Profile-Pic-1-1.jpg",
                    location: { 
                        country: 'United States of America', 
                        state: 'CA' 
                    } 
                },
                { 
                    screen_name: 'd', 
                    tweets: [{}, {}, {}], 
                    profile_image_url_https: "https://i2.wp.com/www.sardiniauniqueproperties.com/wp-content/uploads/2015/10/Square-Profile-Pic-1-1.jpg",
                    location: { 
                        country: 'United States of America', 
                        state: 'FL' 
                    } 
                },
                { 
                    screen_name: 'd', 
                    tweets: [{}, {}, {}], 
                    profile_image_url_https: "https://i2.wp.com/www.sardiniauniqueproperties.com/wp-content/uploads/2015/10/Square-Profile-Pic-1-1.jpg",
                    location: { 
                        country: 'United States of America', 
                        state: 'FL' 
                    } 
                },
                { 
                    screen_name: 'd', 
                    tweets: [{}, {}, {}], 
                    profile_image_url_https: "https://i2.wp.com/www.sardiniauniqueproperties.com/wp-content/uploads/2015/10/Square-Profile-Pic-1-1.jpg",
                    location: { 
                        country: 'United States of America', 
                        state: 'FL' 
                    } 
                },
                { 
                    screen_name: 'aa', 
                    tweets: [{}, {}, {}], 
                    profile_image_url_https: "https://i2.wp.com/www.sardiniauniqueproperties.com/wp-content/uploads/2015/10/Square-Profile-Pic-1-1.jpg",
                    location: { 
                        country: 'United States of America', 
                        state: 'FL' 
                    } 
                },
                { 
                    screen_name: 'e', 
                    tweets: [{}, {}, {}], 
                    profile_image_url_https: "https://i2.wp.com/www.sardiniauniqueproperties.com/wp-content/uploads/2015/10/Square-Profile-Pic-1-1.jpg",
                    location: { 
                        country: 'Canada', 
                        state: 'AB' 
                    } 
                },
                { 
                    screen_name: 'f', 
                    tweets: [{}, {}, {}], 
                    profile_image_url_https: "https://i2.wp.com/www.sardiniauniqueproperties.com/wp-content/uploads/2015/10/Square-Profile-Pic-1-1.jpg",
                    location: { 
                        country: 'Canada', 
                        state: 'ON' 
                    }
                },
                { 
                    screen_name: 'g', 
                    tweets: [{}, {}, {}], 
                    profile_image_url_https: "https://i2.wp.com/www.sardiniauniqueproperties.com/wp-content/uploads/2015/10/Square-Profile-Pic-1-1.jpg",
                    location: { 
                        country: 'India',
                        state: 'Delhi'
                    }
                }
            ],
            selectedCountryName:''
        }
    },
    components: {
        treeMap,
        worldMap
    },
    methods: {
        getCountryHovered(countryName){
            this.selectedCountryName=countryName
        }
    }
    
}
</script>
<style scoped>
.geoDiv div {
      width:500px;
      display:inline-block;
      padding:5px;
      text-align:center;
      color:#000000;
      font-family: arial, sans-serif;
}
</style>