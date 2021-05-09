<template>
  <h1> {{title}} </h1>

  <div v-if="showModel">
    <Model @close="toggleModel">
        <h1>Modal 1</h1>
        <p> model content</p>
    </Model>
    
  </div>

    <div>
      <Create/>
    </div>


  <div v-if="showModelTwo">
    <Model @close="toggleModelTwo">
        <h1>Modal 2</h1>
        <p> model content</p>
    </Model>
  </div>

  <!-- <button @click.left="toggleModel">open model ONE</button> -->
  <!-- <button @click.left="toggleModelTwo">open model TWO</button> -->
  <br>
  <button @click.left="createBirthday">create birthday</button>
  <button @click.left="deleteBirthday">delete birthday</button>
  <button @click.left="updateBirthday">update birthday</button>
  <button @click.left="getBirthday">get birthday</button>

  <!-- <input type="text" ref="name"> -->
  <!-- <button @click="handleClick">open</button> -->
</template>

<script>

import Create from './components/CreateForm.vue'
import Model from './components/Modal.vue'
const axios = require('axios').default;
var cors = require('cors')


export default {
  name: 'App',
  components: { Model , Create}, 
  data() {
    return {
      title: 'birthday',
      showModel: false,
      showModelTwo: false,
    }
  },
  methods: {
    toggleModel() {
      this.showModel = !this.showModel
    },

    toggleModelTwo() {
      console.log("second model")
      this.showModelTwo = !this.showModelTwo
    }, 


    deleteBirthday() {
        let id = "123"
        axios.delete(`http://localhost:6060/birthday/${id}`).then(response => {console.log(response.data)})

    },

    updateBirthday() {
        let id = 15
        axios.put(`http://localhost:6060/birthday/${id}`, {"birthday": 1392420007}).then(response => {console.log(response.data)})

    },

    getBirthday() {
        let number = 123
        axios.get(`http://localhost:6060/birthday/${number}`, cors()).then(response => {console.log(response.data)})

    },

    createBirthday() {
        const person = {name: 'maya fisher', birthday: 1214428057, userId: "123"};
        axios.post(`http://localhost:6060/birthday`, person).then(response => {console.log(response.data)})
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 50px;
}
h1 {
  border-bottom: 1px solid #ddd;
  display: inline-block;
  padding-bottom: 10px;
}
</style>
