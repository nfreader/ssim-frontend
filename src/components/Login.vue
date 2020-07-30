<template>

  <form @submit.prevent="process">
    <input type="email" name="email" placeholder="Email address" v-model="email" />
    <input type="password" name="password" placeholder="Password" v-model="password" />
    <button type="submit">Submit</button>
  </form>

</template>

<script>
import axios from 'axios'

export default {
  data:()=>{
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    process: function() {
      console.log({email: this.email, password: this.password})
      axios.post('http://localhost:8000/api/user/auth',{
        email: this.email,
        password: this.password
      }).then((res) => {
        console.log(res.data)
      }) 
    }
  }
}

</script>