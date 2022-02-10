<template>
  <div >
    <Header />
    <h1>Add Restaurant </h1>
    <div class="container">
          <hr />

    <label for="name"><b>Name </b></label>
    <input
    type="text"
    v-model="name"
    placeholder="Enter Restaurant Name"
    name="name"
    required
    />

    
    <label for="psw"><b>Contact</b></label>
    <input
    type="text"
    v-model="contact"
    placeholder="Enter Contact"
    name="contact"
    required
    />

    <label for="psw"><b>Address</b></label>
    <input
    type="text"
    v-model="address"
    placeholder="Enter Address"
    name="address"
    required
    />

    <button type="submit" @click.prevent="addRestaurant" class="signupbtn">
    Add Restaurant
    </button>
    </div>

  </div>
</template>

<script>
import Header from './Header.vue';
import axios  from 'axios';


export default {
    name: 'Add',
    components: {Header},
    data(){
       return{
          name:'',
          contact: '',
          address: '',
       };
    },
    methods: {
        
        async addRestaurant()
        {
            let response  = await axios.post('http://localhost:3000/restaurants',{
              name: this.name,
              address: this.address,
              contact: this.contact
            });
               console.log(response.data);
            if(response.status == 201 )
            {
              this.$router.push({name: 'Home'});
            }
           
        },

        checkLogin() {
        let user = localStorage.getItem("user-info");
        return user ? true : false;
        },


    },
    mounted() {
       let login = this.checkLogin();
       console.log("Add ", login)
       // login ?  this.$router.push({ name: "Home" }) :  this.$router.push({ name: "Login" });


        if(!login)
        {

            console.log("I am mounted");
            this.$router.push({ name: "Login" });
        }
    },
}
</script>

<style >
* {
  box-sizing: border-box;
}
h1{
  text-align: center;
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