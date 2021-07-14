<template>
  <div>
    <ul v-for="user in users" :key="user.id">
      <li>Nama : {{ user.name }}</li>
      <li>umur : {{ user.age }}</li>
      <li>
        <v-btn  
        color="danger"
        @click="handleDelete(user.name)"
        >
          Delete
        </v-btn>
      </li>
    </ul>

    <v-form
      @submit.prevent="handleSubmit"
    >
      <v-col>
        <v-text-field
          v-model="forms.name"
        >
        </v-text-field>
      </v-col>
      <v-col>
        <v-text-field
          type="number"
          v-model="forms.age"
        >
        </v-text-field>
      </v-col>
      <v-col>
        <v-btn
          type="submit"
          color="primary"
          block
        >Submit
        </v-btn>
      </v-col>
    </v-form>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    name: 'Home',
    data(){
      return {
        users : [],
        forms : {
          name : null,
          age : null
        }
      }
    },
    mounted(){
      this.getUsers()
    },
    methods : {
      async getUsers(){
        let response = await axios.get('http://127.0.0.1:3000/users')

        this.users = response.data.result
      },
      async handleSubmit(){
        try{
          let response = await axios.post('http://127.0.0.1:3000/users', this.forms)

          if (response.status === 200) {
            console.log(response)
            this.getUsers()
            this.forms.name = null
            this.forms.age = null
          }
        }catch(err){
          alert(err)
        }
      },
      async handleDelete(e){
        try{
          let response = await axios.get('http://127.0.0.1:3000/delete/' + e)

          if (response.status === 200) {
            console.log(response)
            this.getUsers()
          }
        }catch(err){
          alert(err)
        }
      }
    },
  }
</script>
