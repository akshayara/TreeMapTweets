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
            users: [
                {
                    name: 'Amir',
                    location: {
                        country: 'USA',
                        state: 'CA'
                    }
                },
                {
                    name: 'Akshaya',
                    location: {
                        country: 'Canada',
                        state: 'ON'
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
.viewBoxStyle{
    font-size: 10px;
    font: sans-serif 	
}
</style>