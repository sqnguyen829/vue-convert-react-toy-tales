<template>
  <div>
    <Header/>
    <div v-if="display">
      <ToyForm v-on:add-toy="addToy"/>
    </div>
    <div class="buttonContainer">
      <button @click="handleClick">Add a Toy</button>
    </div>
    <ToyContainer v-bind:toys="toys" v-on:donate-toy="donateToy" v-on:like-toy="likeToy"/>
  </div>
</template>

<script>
import Header from './components/Header'
import ToyForm from './components/ToyForm'
import ToyContainer from './components/ToyContainer'

export default {
  name: 'App',
  components: {
    Header,
    ToyForm,
    ToyContainer
  },
  data(){
    //data() technically acts like state from react
    return {
      display: false,
      toys: []
    }
  },
  methods: {
    handleClick() {
      this.display = !this.display 
    },
    addToy(newToy) {
      fetch('http://localhost:3000/toys',{
        method:'POST',
        headers:{
        'Content-Type': 'application/json'
        },
        body: JSON.stringify(newToy)
      })
      .then(res => res.json())
      .then(data => this.toys = [...this.toys, data])
      .catch(err => console.log(err))
    },
    donateToy(id) {
      fetch(`http://localhost:3000/toys/${id}`,{
          method:'DELETE',
          headers:{
              'Content-Type': 'application/json'
          }
      })
      .then(()=> this.toys = this.toys.filter(toy => toy.id != id))
      .catch(err => console.log(err))
    },
    likeToy(toy) {
      fetch(`http://localhost:3000/toys/${toy.id}`,{
      method:'PATCH',
      headers:{
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        likes: toy.likes + 1
      })
    })
    .then(res=> res.json())
    .then(data => this.toys = this.toys.map(t => {
      if(t.id === toy.id){
        t.likes = data.likes
        return t
      }else{
        return t
      }
    }))
    }
  },
  created() {//created() acts as a componentDidMount
    //included the method in the second arg of the fetch since it was throwing an error in the console. It didn't affect the fetch though
    fetch('http://localhost:3000/toys',{
      method:'GET'
    })
    .then(res => res.json())
    .then(data => this.toys = data)
    .catch(err => console.log(err))
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }


  body {
  margin: 0;
  font-family: monospace;
}

#toy-header {
  display: flex;
  justify-content: center;
  background: #515DA2;
  opacity: .8;
  height: 7rem;
  padding: 1rem;
}

#toy-header img {
  height: 6rem;
  width: auto;
}

#toy-collection {
  margin: 2rem;
}

.card {
  /* grid-column-start: 1;
  grid-column-end: 3; */
  text-align: center;
  text-align: center;
  border: grey solid 1px;
  padding: 1rem;
  width: 15rem;
  height: 25rem;
  display: inline-grid;
  margin: 1rem 2rem;
  box-shadow: 3px 4px #e04b52
}

.toy-avatar {
  justify-self: center;
  height: 12rem;
  width: auto;
}

button {
  position: relative;
  background-color: #e04b52;
  border: none;
  border-radius: 5px;
  height: 3rem;
  width: max-content;
  color: whitesmoke;
  font-size: 18px;
  justify-self: center;
}

.buttonContainer {
  text-align: center;
  padding: 1rem;
}

button:hover {
  background-color: whitesmoke;
  border: #e04b52 solid 1px;
  color: #e04b52;
}

.container {
  padding: 1rem;
  width: stretch;
  height: auto;
  background: #515DA2;
  opacity: .8;
}

.add-toy-form {
  width: 80%
}

.submit {
  position: relative;
  background-color: #e04b52;
  border-radius: 5px;
  height: 2rem;
  width: max-content;
  color: whitesmoke;
  font-size: 18px;
  justify-self: center;
  font-family: monospace;
  margin: 3px;
}

.submit:hover {
  background-color: whitesmoke;
  border: #e04b52 solid 1px;
  color: #e04b52;
}


.input-text {
  border-radius: 5px;
  height: 2rem;
  width: 60%;
  font-size: 18px;
  font-family: monospace;
  margin: 3px;
}
</style>
