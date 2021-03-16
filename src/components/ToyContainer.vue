<template>
    <div>
        <div v-bind:key="toy.id" v-for="toy in toys">
            <ToyCard v-bind:toy="toy" v-on:donate-toy="$emit('donate-toy', toy)" v-on:like-toy="$emit('like-toy', toy)"/>
        </div>
    </div>
</template>

<script>
import ToyCard from './ToyCard'

export default {
    name:"ToyContainer",
    components:{
        ToyCard
    },
    props:["toys"],
}
</script>