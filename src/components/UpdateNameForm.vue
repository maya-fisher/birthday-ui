<template>
  <form class="get" @submit.prevent="handelSubmit">

        <div v-if="showError" class="alert">
            <span class="closebtn" onclick="this.parentElement.style.display='none';">&times;</span> 
            <strong>NOTE!!</strong> There is no user with this ID.
        </div>

      <label>ID</label>
      <input type="id" required v-model="id">
      <label>Name</label>
      <input type="text" required v-model="name">        
        <div class="submit">
        <button>update birthday</button>

        
        </div>
            <div v-if="user" class="user">
            <h2></h2>
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
            name: '',
            showError: false,
            newName: '', 
            newBirthday: '', 
            user: false,
        }
    },
    methods: {
        handelSubmit() {
            console.log(this.id, this.name)

            axios.put(`http://localhost:6060/birthday/${this.id}`, {"name": this.name}).then(response => {
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


</style>