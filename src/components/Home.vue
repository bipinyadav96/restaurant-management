<template>
  <div>
    <Header />
    <h1>Welcome {{ username }}</h1>
    <table id="customers">
      <tr>
        <th>Name</th>
        <th>Address</th>
        <th>Contact</th>
        <th>Actions</th>
      </tr>
      <tr v-for="(res,index) in restaurants" :key="index">
        <td>{{ res.name }}</td>
        <td>{{ res.address }}</td>
        <td>{{ res.contact }}</td>
        <td><router-link :to="`/update/${res.id}`">Update</router-link>
            <button @click.prevent="removeRestaurant(res.id)">Delete</button>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
import Header from "./Header.vue";
import axios from "axios";

export default {
  name: "Home",
  data() {
    return {
      username: null,
      restaurants: [],
    };
  },
  components: { Header },
  methods: {

    async removeRestaurant(id)
    {
      let response = await axios.delete(`http://localhost:3000/restaurants/${id}`);
      if(response.status == 200)
      {
        this.fetchRestaurants("http://localhost:3000/restaurants");
      }else{
        alert("Delete Error! ");
      }
      
    },

    checkLogin() {
      let user = localStorage.getItem("user-info");
      user = JSON.parse(user);
      if (user) {
        this.username = user.name;
        console.log(this.username);
      }

      return user ? true : false;
    },

    async fetchRestaurants(url) {
      let response = await axios.get(url);
      let restaurants = await response.data;
      this.restaurants = restaurants;
      console.log(restaurants);
    },
  },
  mounted() {
    let login = this.checkLogin();
    if (!login) {
      this.$router.push({ name: "SignUp" });
    }
  


    this.fetchRestaurants("http://localhost:3000/restaurants");
  },
  watcher:{

  }
};
</script>


<style >
h1{
  text-align: center;
}

div {
  padding: 0px;
  margin: 0px;
}

#customers {
  font-family: Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 80%;
  margin-left: 10%;
}

#customers td,
#customers th {
  border: 1px solid #ddd;
  padding: 8px;
}

#customers tr:nth-child(even) {
  background-color: #f2f2f2;
}

#customers tr:hover {
  background-color: #ddd;
}

#customers th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: left;
  background-color: #04aa6d;
  color: white;
}
</style>