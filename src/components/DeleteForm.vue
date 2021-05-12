<template>
  <form class="delete" @submit.prevent="handelSubmit">

        <div v-if="showError" class="alert">
            <span class="closebtn" onclick="this.parentElement.style.display='none';">&times;</span> 
            <strong>Danger!</strong> Indicates a dangerous or potentially negative action.
        </div>

      <label>ID</label>
      <input type="id" required v-model="id">
        <div class="submit">
        <button>delete birthday</button>
        </div>

        <div v-if="user" class="user">
            <h2>DELETED:</h2>
            <label class="try">NAME: {{newName}}</label><br>
            <label class="try">BIRTHDAY: {{newBirthday}}</label>
        </div>
  </form>

</template>

<script>

const axios = require('axios').default;

export default {
    data() {
        return {
            id: '',
            showError: false,
            newName: '', 
            newBirthday: '', 
            user: false,
        }
    },
    methods: {
        handelSubmit() {
            let response = axios.delete(`http://localhost:6060/birthday/${this.id}`)
            .then(response => {
                this.newBirthday = response.data.person.birthday;
                let d = new Date(parseInt(this.newBirthday));
                this.newBirthday = `${d.getDate()}-${d.getMonth()+1}-${d.getFullYear()}`;
                this.newName = response.data.person.name;
                this.user = true;            
            })
            .catch(err => {
                this.showError = true;
                console.log(`error:${err}`)
            })
        },
     }
}

</script>

<style>




.user {
    background: lightseagreen;
    width: 130;
    margin:50px auto;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
    
}

.user:hover {
    background: rgb(28, 153, 147);
}
.user label {
    color: #2c3e50;
}


</style>