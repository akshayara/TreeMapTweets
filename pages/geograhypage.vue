<template>
    <div>
        <tree-map :users="users" :temp="usersSet"></tree-map>
    </div>
</template>
<script>
import treeMap from '~/components/treeMap.vue'
import * as d3 from 'd3'
export default {
    data(){
        return {
            users: {
                name: "countries",
                children: [
                    {
                        name: 'USA',
                        children: [
                            { name: 'CA', value: 1},
                            { name: 'GA', value: 3},
                        ]
                    },
                    {
                        name: 'Canada',
                        children: [
                            { name: 'ON', value: 5},
                            { name: 'BC', value: 7},
                            { name: 'AL', value: 7}
                        ]
                    },
                    {
                        name: 'UK',
                        children: [
                            { name: 'England', value: 5},
                        ]
                    }
                ]
            },
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