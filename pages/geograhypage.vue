<template>
    <div>
        <tree-map :users="usersSet"></tree-map>
    </div>
</template>
<script>
import treeMap from '~/components/treeMap.vue'
import * as d3 from 'd3'
export default {
    data(){
        return {
            usersSet: [
                { 
                    name: 'a', 
                    tweets: [{}, {}, {}], 
                    location: { 
                        country: 'USA', 
                        state: 'WA' 
                    }
                },
                { 
                    name: 'b', 
                    tweets: [{}, {}, {}], 
                    location: { 
                        country: 'USA', 
                        state: 'CA' 
                    } 
                },
                { 
                    name: 'c', 
                    tweets: [{}, {}, {}], 
                    location: { 
                        country: 'USA', 
                        state: 'CA' 
                    } 
                },
                { 
                    name: 'd', 
                    tweets: [{}, {}, {}], 
                    location: { 
                        country: 'USA', 
                        state: 'FL' 
                    } 
                },
                { 
                    name: 'd', 
                    tweets: [{}, {}, {}], 
                    location: { 
                        country: 'USA', 
                        state: 'FL' 
                    } 
                },
                { 
                    name: 'd', 
                    tweets: [{}, {}, {}], 
                    location: { 
                        country: 'USA', 
                        state: 'FL' 
                    } 
                },
                { 
                    name: 'e', 
                    tweets: [{}, {}, {}], 
                    location: { 
                        country: 'Canada', 
                        state: 'AB' 
                    } 
                },
                { 
                    name: 'f', 
                    tweets: [{}, {}, {}], 
                    location: { 
                        country: 'Canada', 
                        state: 'ON' 
                    }
                },
                { 
                    name: 'g', 
                    tweets: [{}, {}, {}], 
                    location: { 
                        country: 'India',
                        state: 'Delhi'
                    }
                }
            ]
        }
    },
    components: {
        treeMap
    }
    
}
</script>
<style scoped>
</style>