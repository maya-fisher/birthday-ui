<template>
  <h1> {{title}} </h1>

  <div id="main">

    <div id="buttonsDiv">
      <button class="button" @click.left="toggleCreate"><span>create page </span></button>
      <button class="button" @click.left="toggleDelete"><span>delete page </span></button>
      <button class="button" @click.left="toggleGet"><span>get page </span></button>
      <button class="button" @click.left="toggleUpdate"><span>update page </span></button>

    </div>

    <div class="createDiv" v-if="showCreatePage">
      <Create>
      </Create>
    </div>
    
    <div v-if="showDeletePage">
      <DeleteForm>
      </DeleteForm>
    </div>

    <div v-if="showGetPage">
      <GetForm>
      </GetForm>
    </div>

    <div v-if="showUpdatePage">
      <UpdateForm>
      </UpdateForm>
    </div>

  </div>

</template>

<script>

import Create from './components/CreateForm.vue'
import GetForm from './components/GetForm.vue'
import DeleteForm from './components/DeleteForm.vue'
import UpdateForm from './components/UpdateForm.vue'
const axios = require('axios').default;

export default {
  name: 'App',
  components: { Create, GetForm, DeleteForm, UpdateForm}, 
  data() {
    return {
      title: 'BIRTHDAY SERVICE',
      showModel: false,
      showCreatePage: false,
      showGetPage: false,
      showDeletePage: false,
      showUpdatePage: false,
    }
  },
  methods: {

    toggleCreate() {
      this.showCreatePage = !this.showCreatePage
    },

    toggleGet() {
      this.showGetPage = !this.showGetPage
    },

    toggleDelete() {
      this.showDeletePage = !this.showDeletePage
    },

    toggleUpdate() {
      this.showUpdatePage = !this.showUpdatePage
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

#main {
  display: flex;
  flex-direction: row;
}

#buttonsDiv {
  display: flex;
  flex-direction: column;
}

#buttonsDiv button {
  border-radius: 4px;
  background-color: #0b6dff;
  border: none;
  color: #FFFFFF;
  text-align: center;
  font-size: 20px;
  padding: 18px;
  width: 200px;
  transition: all 0.5s;
  cursor: pointer;
  margin: 5px;
}

#buttonsDiv button span {
    cursor: pointer;
  display: inline-block;
  position: relative;
  transition: 0.5s;
}

#buttonsDiv button span:after {
  content: '\00bb';
  position: absolute;
  opacity: 0;
  top: 0;
  right: -20px;
  transition: 0.5s;
}

#buttonsDiv button:hover span {
    padding-right: 25px;
}

.button span:after {
  content: '\00bb';
  position: absolute;
  opacity: 0;
  top: 0;
  right: -20px;
  transition: 0.5s;
}

#buttonsDiv button:hover span:after {
  opacity: 1;
  right: 0;
}


</style>

