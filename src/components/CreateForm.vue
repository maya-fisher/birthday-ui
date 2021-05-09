<template>
  <form @submit.prevent="handelSubmit">
      <label>Name</label>
      <input type="text" required v-model="name">
      <label>ID</label>
      <input type="id" required v-model="id">
      <input type="date" required v-model="birthday">
        <div class="submit">
        <button>create birthday</button>
    </div>
  </form>

</template>

<script>
export default {
    data() {
        return {
            name: '',
            id: '',
            birthday: '',
        }
    },
    methods: {
        handelSubmit() {
            console.log({name: this.name, id: this.id, birthday: this.birthday})
            console.log(typeof this.birthday)
            let mydate
        }
    }

}

</script>

<style>
form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
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

button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
    cursor: pointer;
}

.submit {
    text-align: center;
}
</style>