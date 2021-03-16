<template>
    <div class="container">
        <form class="add-toy-form" @submit="addToy">
          <h3>Create a toy!</h3>
          <input type="text" v-model="name" name="name" placeholder="Enter a toy's name..." class="input-text"/>
          <br/>
          <input type="text" v-model="image" name="image" placeholder="Enter a toy's image URL..." class="input-text"/>
          <br/>
          <input type="submit" name="submit" value="Create New Toy" class="submit"/>
        </form>
      </div>
</template>

<script>
export default {
  name:'ToyForm',
  data() {
    return {
      name:'',
      image:''
    }
  },
  methods: {
    addToy(e) {
      e.preventDefault();
      const newToy = {
        name:this.name,
        image:this.image,
        likes:0
      }
      this.$emit('add-toy', newToy)
      this.title = ''
      this.image = ''
    }
  }
}
</script>