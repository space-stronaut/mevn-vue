<template>
  <div>
    <ul v-for="user in users" :key="user.id">
      <li>Nama : {{ user.name }}</li>
      <li>umur : {{ user.age }}</li>
    </ul>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    name: 'Home',
    data(){
      return {
        users : []
      }
    },
    mounted(){
      this.getUsers()
    },
    methods : {
      async getUsers(){
        let response = await axios.get('http://127.0.0.1:3000/users')

        this.users = response.data.result
      }
    },
  }
</script>
