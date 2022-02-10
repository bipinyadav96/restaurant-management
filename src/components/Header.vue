<template>
  <div class="topnav">
    <a class="active" href="/">Home</a>
    <a href="/add">Add</a>
  
    <a @click.prevent="logOut">Logout</a>
  </div>
</template>

<script>
export default {
  name: "Header",
  methods: {
      logOut()
      {
          console.log("Logout is called");
         localStorage.clear();
         this.$router.push({name : 'Login'});   
      }
  },
};
</script>

<style>
.topnav {
  background-color: #333;
  overflow: hidden;
   margin-top: -60px;
}

/* Style the links inside the navigation bar */
.topnav a {
  float: left;
  color: #f2f2f2;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
  font-size: 17px;
 
}

/* Change the color of links on hover */
.topnav a:hover {
  background-color: #ddd;
  color: black;
}

/* Add a color to the active/current link */
.topnav a.active {
  background-color: #04aa6d;
  color: white;
}
body{
    padding: 0px;
    margin: 0px;

}

</style>