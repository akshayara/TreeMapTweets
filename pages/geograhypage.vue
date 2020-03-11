<template>
    <div>
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
                    profile_imgae_url_https: "https://www.google.com/url?sa=i&source=images&cd=&ved=2ahUKEwimt6zdk5PoAhVmxYUKHcPeAiEQjRx6BAgBEAQ&url=https%3A%2F%2Fwww.rd.com%2Fadvice%2Frelationships%2Fonline-dating-profile-photos%2F&psig=AOvVaw1vGMfr0TMqx0X4K3E6a6S3&ust=1584041272239104",
                    location: { 
                        country: 'United States of America', 
                        state: 'WA' 
                    }
                },
                { 
                    screen_name: 'b', 
                    tweets: [{}, {}, {}], 
                    profile_imgae_url_https: "https://www.google.com/url?sa=i&source=images&cd=&ved=2ahUKEwimt6zdk5PoAhVmxYUKHcPeAiEQjRx6BAgBEAQ&url=https%3A%2F%2Fwww.rd.com%2Fadvice%2Frelationships%2Fonline-dating-profile-photos%2F&psig=AOvVaw1vGMfr0TMqx0X4K3E6a6S3&ust=1584041272239104",
                    location: { 
                        country: 'United States of America', 
                        state: 'CA' 
                    } 
                },
                { 
                    screen_name: 'c', 
                    tweets: [{}, {}, {}], 
                    profile_imgae_url_https: "https://www.google.com/url?sa=i&source=images&cd=&ved=2ahUKEwimt6zdk5PoAhVmxYUKHcPeAiEQjRx6BAgBEAQ&url=https%3A%2F%2Fwww.rd.com%2Fadvice%2Frelationships%2Fonline-dating-profile-photos%2F&psig=AOvVaw1vGMfr0TMqx0X4K3E6a6S3&ust=1584041272239104",
                    location: { 
                        country: 'United States of America', 
                        state: 'CA' 
                    } 
                },
                { 
                    screen_name: 'd', 
                    tweets: [{}, {}, {}], 
                    profile_imgae_url_https: "https://www.google.com/url?sa=i&source=images&cd=&ved=2ahUKEwimt6zdk5PoAhVmxYUKHcPeAiEQjRx6BAgBEAQ&url=https%3A%2F%2Fwww.rd.com%2Fadvice%2Frelationships%2Fonline-dating-profile-photos%2F&psig=AOvVaw1vGMfr0TMqx0X4K3E6a6S3&ust=1584041272239104",
                    location: { 
                        country: 'United States of America', 
                        state: 'FL' 
                    } 
                },
                { 
                    screen_name: 'd', 
                    tweets: [{}, {}, {}], 
                    profile_imgae_url_https: "https://www.google.com/url?sa=i&source=images&cd=&ved=2ahUKEwimt6zdk5PoAhVmxYUKHcPeAiEQjRx6BAgBEAQ&url=https%3A%2F%2Fwww.rd.com%2Fadvice%2Frelationships%2Fonline-dating-profile-photos%2F&psig=AOvVaw1vGMfr0TMqx0X4K3E6a6S3&ust=1584041272239104",
                    location: { 
                        country: 'United States of America', 
                        state: 'FL' 
                    } 
                },
                { 
                    screen_name: 'd', 
                    tweets: [{}, {}, {}], 
                    profile_imgae_url_https: "https://www.google.com/url?sa=i&source=images&cd=&ved=2ahUKEwimt6zdk5PoAhVmxYUKHcPeAiEQjRx6BAgBEAQ&url=https%3A%2F%2Fwww.rd.com%2Fadvice%2Frelationships%2Fonline-dating-profile-photos%2F&psig=AOvVaw1vGMfr0TMqx0X4K3E6a6S3&ust=1584041272239104",
                    location: { 
                        country: 'United States of America', 
                        state: 'FL' 
                    } 
                },
                { 
                    screen_name: 'e', 
                    tweets: [{}, {}, {}], 
                    profile_imgae_url_https: "https://www.google.com/url?sa=i&source=images&cd=&ved=2ahUKEwimt6zdk5PoAhVmxYUKHcPeAiEQjRx6BAgBEAQ&url=https%3A%2F%2Fwww.rd.com%2Fadvice%2Frelationships%2Fonline-dating-profile-photos%2F&psig=AOvVaw1vGMfr0TMqx0X4K3E6a6S3&ust=1584041272239104",
                    location: { 
                        country: 'Canada', 
                        state: 'AB' 
                    } 
                },
                { 
                    screen_name: 'f', 
                    tweets: [{}, {}, {}], 
                    profile_imgae_url_https: "https://www.google.com/url?sa=i&source=images&cd=&ved=2ahUKEwimt6zdk5PoAhVmxYUKHcPeAiEQjRx6BAgBEAQ&url=https%3A%2F%2Fwww.rd.com%2Fadvice%2Frelationships%2Fonline-dating-profile-photos%2F&psig=AOvVaw1vGMfr0TMqx0X4K3E6a6S3&ust=1584041272239104",
                    location: { 
                        country: 'Canada', 
                        state: 'ON' 
                    }
                },
                { 
                    screen_name: 'g', 
                    tweets: [{}, {}, {}], 
                    profile_imgae_url_https: "https://www.google.com/url?sa=i&source=images&cd=&ved=2ahUKEwimt6zdk5PoAhVmxYUKHcPeAiEQjRx6BAgBEAQ&url=https%3A%2F%2Fwww.rd.com%2Fadvice%2Frelationships%2Fonline-dating-profile-photos%2F&psig=AOvVaw1vGMfr0TMqx0X4K3E6a6S3&ust=1584041272239104",
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
</style>