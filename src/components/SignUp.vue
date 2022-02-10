<template>
  <div>
    <div class="container">
      <h1>Register</h1>

      <hr />

      <label for="email"><b>Name</b></label>
      <input
        type="text"
        v-model="name"
        placeholder="Enter Name"
        name="name"
        required
      />

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
      <!-- 
      <label>
        <input
          type="checkbox"
          checked="checked"
          name="remember"
          style="margin-bottom: 15px"
        />
        Remember me
      </label> -->

      <button type="submit" @click.prevent="userSignUp" class="signupbtn">
        Sign Up
      </button>
        <router-link to="/login">Login</router-link>

    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      email: "",
      password: "",
      name: "",
    };
  },
  methods: {
    async userSignUp() {
      let result = await axios.post("http://localhost:3000/users", {
        name: this.name,
        email: this.email,
        password: this.password,
      });

      if (result.status == 201) {
        localStorage.setItem("user-info", JSON.stringify(result.data));
        this.$router.push({ name: "Home" });
      }
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

<style >
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

* {
  box-sizing: border-box;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 60%;
  margin-left: 20%;
}

/* Full-width input fields */
input[type="text"],
input[type="password"] {
  width: 100%;
  padding: 15px;
  margin: 5px 0 22px 0;
  display: inline-block;
  border: none;
  background: #f1f1f1;
}

input[type="text"]:focus,
input[type="password"]:focus {
  background-color: #ddd;
  outline: none;
}

hr {
  border: 1px solid #f1f1f1;
  margin-bottom: 25px;
}

/* Set a style for all buttons */
button {
  background-color: #04aa6d;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  cursor: pointer;
  width: 100%;
  opacity: 0.9;
}

button:hover {
  opacity: 1;
}

/* Extra styles for the cancel button */
.cancelbtn {
  padding: 14px 20px;
  background-color: #f44336;
}

/* Float cancel and signup buttons and add an equal width */
.cancelbtn,
.signupbtn {
  float: left;
  width: 100%;
}

/* Add padding to container elements */
.container {
  padding: 16px;
}

/* Clear floats */
.clearfix::after {
  content: "";
  clear: both;
  display: table;
}

/* Change styles for cancel button and signup button on extra small screens */
@media screen and (max-width: 300px) {
  .cancelbtn,
  .signupbtn {
    width: 100%;
  }
}
</style>
