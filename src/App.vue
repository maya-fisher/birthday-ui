<template>

  <h1> {{title}} </h1>

    <div id="main">

    <div id="buttonsDiv">
      <button class="button" @click.left="toggleCreate"><span>create new birthday </span></button>
      <button class="button" @click.left="toggleDelete"><span>delete birthday </span></button>
      <button class="button" @click.left="toggleGet"><span>find birthday </span></button>
      <button class="button" @click.left="toggleUpdate"><span>update birthday </span></button>
      <button class="button" @click.left="toggleUpdateName"><span>update name </span></button>
    </div>


    <div class="createDiv" v-if="showCreatePage">
      <Create>
      </Create>
    </div>

    <div class="createDiv" v-if="showDeletePage">
      <DeleteForm>
      </DeleteForm>
    </div>

    <div class="createDiv" v-if="showGetPage">
      <GetForm>
      </GetForm>
    </div>

    <div class="createDiv" v-if="showUpdatePage">
      <UpdateForm>
      </UpdateForm>
    </div>

    <div class="createDiv" v-if="showUpdateNamePage">
      <UpdateNameForm>
      </UpdateNameForm>
    </div>

  </div>


</template>


<script>

export const BASE_URL = "http://localhost:8081"


import Create from './components/CreateForm.vue'
import GetForm from './components/GetForm.vue'
import DeleteForm from './components/DeleteForm.vue'
import UpdateForm from './components/UpdateForm.vue'
import UpdateNameForm from './components/UpdateNameForm'
const axios = require('axios').default;

export default {
  name: 'App',
  components: { Create, GetForm, DeleteForm, UpdateForm, UpdateNameForm }, 
  data() {
    return {
      title: 'BIRTHDAY SERVICE',
      showModel: false,
      showCreatePage: false,
      showGetPage: false,
      showDeletePage: false,
      showUpdatePage: false,
      showUpdateNamePage: false,
    }
  },
  methods: {

    toggleCreate() {
      this.showGetPage = false;
      this.showDeletePage = false;
      this.showUpdatePage = false;
      this.showUpdateNamePage = false;
      this.showCreatePage = !this.showCreatePage
    },

    toggleGet() {
      this.showCreatePage = false;
      this.showDeletePage = false;
      this.showUpdatePage = false;
      this.showUpdateNamePage = false;
      this.showGetPage = !this.showGetPage
    },

    toggleDelete() {
      this.showUpdatePage = false;
      this.showCreatePage = false;
      this.showGetPage = false;
      this.showUpdateNamePage = false;
      this.showDeletePage = !this.showDeletePage
    },

    toggleUpdate() {
      this.showCreatePage = false;
      this.showGetPage = false;
      this.showDeletePage = false;
      this.showUpdateNamePage = false;
      this.showUpdatePage = !this.showUpdatePage
    },

    toggleUpdateName() {
      this.showCreatePage = false;
      this.showGetPage = false;
      this.showDeletePage = false;
      this.showUpdatePage = false;
      this.showUpdateNamePage = !this.showUpdateNamePage
    }

  }
}
</script>

<style>


body {
  background-image: url("./assets/confetti-3.gif");
}
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


.createDiv {
  height: 430px;
}

#buttonsDiv {
  display: flex;
  flex-direction: column;
}

#buttonsDiv button {
  border-radius: 4px;
  background-color: #ffb3de;
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

