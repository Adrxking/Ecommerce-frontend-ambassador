<template>
  <form @submit.prevent="submit" class="form-signin">
    
    <h1 class="h3 mb-3 font-weight-normal">Please register</h1>
      
    <label class="sr-only">First Name</label>
    <input v-model="first_name" class="form-control" placeholder="First Name">
    
    <label class="sr-only">Last Name</label>
    <input v-model="last_name" class="form-control" placeholder="Last Name">

    <label class="sr-only">Email address</label>
    <input v-model="email" type="email" class="form-control" placeholder="Email address">
      
    <label class="sr-only">Password</label>
    <input v-model="password" type="password" class="form-control" placeholder="Password">

    <label class="sr-only">Password confirm</label>
    <input v-model="password_confirm" type="password" class="form-control" placeholder="Password confirm">
      
    <button class="btn btn-lg btn-primary btn-block" type="submit">Submit</button>
    
  </form>
</template>

<script>
import axios from "axios";

export default {
  name: "Register",
  data(){
    return {
      first_name: '',
      last_name: '',
      email: '',
      password: '',
      password_confirm: '',
    }
  },
  methods: {
    async submit() {
      await axios.post('register', {
        first_name: this.first_name,
        last_name: this.last_name,
        email: this.email,
        password: this.password,
        password_confirm: this.password_confirm,
      });

      await this.$router.push('/login');
    }
  }
}
</script>

<style>

</style>