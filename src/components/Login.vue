<template>
  <div>
    <div class="container">
      <h1>Login</h1>

      <hr />

      <label for="email"><b>Email</b></label>
      <input
        type="text"
        v-model="email"
        placeholder="Enter Email"
        name="email"
        required
      />

      <label for="psw"><b>Password</b></label>
      <input
        type="password"
        v-model="password"
        placeholder="Enter Password"
        name="psw"
        required
      />

      <button type="submit" @click="userLogin" class="signupbtn">
        Login
      </button>
      <router-link to="/sign-up">Register</router-link>
    </div>
  </div>
</template>

<script>

import axios from "axios";

export default {
  name: "Login",
  data(){
      return {
        email: "",
        password: "",
      };
  },

  methods: {

    async userLogin()
    {
       let result = 
       await axios.get(`http://localhost:3000/users?email=${this.email}&password=${this.password}`);
       console.log(result);
        if(result.status == 200 && result.data.length > 0)
           {
                localStorage.setItem('user-info', JSON.stringify(result.data[0]));
                this.$router.push({name : 'Home'});
           }
        else
            alert("Fields Invalid");
        
    },
    checkLogin() {
        let user = localStorage.getItem("user-info");
        return user ? true : false;
    },


  },
  mounted() {
       let login = this.checkLogin();
        if(login)
        {
            console.log("I am mounted");
            this.$router.push({ name: "Home" });
        }
  },


};
</script>

<style>
</style>