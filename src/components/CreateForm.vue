<template>

  <form id="createForm" @submit.prevent="handelSubmit">

        <div v-if="showError" class="alert">
            <span class="closebtn" onclick="this.parentElement.style.display='none';">&times;</span> 
            <strong>NOTE!</strong> This ID already exists in the system. try again.
        </div>

        <label>Name</label>
        <input type="text" required v-model="name">
        <label>ID</label>
        <input type="id" required v-model="id">
        <label>Birthday</label>
        <input type="date" required v-model="birthday">
        <div class="submit">
        <button id="createButton">create birthday</button>
        </div>

  </form>

    <div v-if="user" class="user">
        <h2>CREATED NEW BIRTHDAY</h2>
        <label class="try">NAME: {{newName}}</label><br>
        <label class="try">BIRTHDAY: {{newBirthday}}</label>
    </div>



</template>

<script>

import { BASE_URL } from '../App'

const axios = require('axios').default;
import { baseURL } from "@/config";

export default {
    data() {
        return {
            name: '',
            id: '',
            birthday: '',
            showError: false,
            newName: '', 
            newBirthday: '', 
            user: false,
        }
    },
    methods: {
        handelSubmit() {
            let dateArray = this.birthday.split("-");
            let newDate = new Date( dateArray[0], dateArray[1] - 1, dateArray[2]);
            let timestamp = Math.floor(newDate.getTime()/1000);
            let user = {name: this.name, userId: this.id, birthday: timestamp};
            console.log(`${baseURL}/birthday`);
            let response = axios.post(`${BASE_URL}/birthday`, user)
            .then(response => {
                this.newBirthday = response.data.person.birthday;
                let d = new Date(parseInt(this.newBirthday));
                this.newBirthday = `${d.getDate()}-${d.getMonth()+1}-${d.getFullYear()}`;
                this.newName = response.data.person.name;
                this.user = true;
                this.showError = false;
            })
            .catch(err => {
                this.showError = true;
                this.user = false;
                console.log(`error:${err}`)
            })

        },
     }
}

</script>

<style>

.user {
    background: lightblue;
    width: 230px;
    margin:50px auto;
    text-align: left;
    padding: 40px;
    margin-top: 17%;
    border-radius: 10px;
    
}


.user label {
    color: #2c3e50;
}

form {    
    width: 270px;
    margin:-290px auto;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
    background-color:whitesmoke;
}


label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.9em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}

input {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}

.submit {
    text-align: center;
}

.submit button {
    background: #ff7f50;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
    cursor: pointer;
}

.error {
    width: 100px;
    height: 100px;
    background: cornflowerblue;

}

.alert {
  padding: 20px;
  background-color: #f44336;
  color: white;
  opacity: 1;
  transition: opacity 0.6s;
  margin-bottom: 15px;
}

.alert {
  opacity: 1;
  transition: opacity 0.6s; /* 600ms to fade out */
}


/* The close button */
.closebtn {
  margin-left: 15px;
  color: white;
  font-weight: bold;
  float: right;
  font-size: 22px;
  line-height: 20px;
  cursor: pointer;
  transition: 0.3s;
}

.closebtn:hover {
  color: black;
}
</style>