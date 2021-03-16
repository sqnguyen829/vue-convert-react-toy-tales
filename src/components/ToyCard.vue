<template>
    <div class="card">
        <h2>{{toy.name}}</h2>
        <img v-bind:src="toy.image" @error="$event.target.src='https://images-na.ssl-images-amazon.com/images/I/41mhEuepeaL._AC_.jpg'" class="toy-avatar" />
        <p>{{toy.likes}} Likes </p>
        <button @click="$emit('like-toy', toy)" class="like-btn">Like ♥</button>
        <button @click="$emit('donate-toy', toy.id)" class="del-btn" >Donate to GoodWill</button>
      </div>
</template>

<script>
export default {
    name:"ToyCard",
    props:["toy"]
}
</script>

<style scoped>

</style>