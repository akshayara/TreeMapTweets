<template>
    <div>
        <tree-map :users="users"></tree-map>
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
        }
    },
    components: {
        treeMap
    }
    
}
</script>
<style scoped>
</style>