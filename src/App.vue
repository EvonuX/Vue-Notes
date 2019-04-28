<template>
  <div id="app">
    <!-- <nav>
      <router-link to="/">Home</router-link>
      <router-link to="/about">About</router-link>
    </nav>-->
    <router-view/>
  </div>
</template>

<script>
import Skills from "./components/Skills";

export default {
  name: "app",
  components: {
    Skills
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Montserrat:400,700");

body {
  background-color: #eeeeee;
  font-family: "Montserrat", sans-serif;
  display: grid;
  grid-template-rows: auto;
  justify-items: center;
  padding-top: 50px;
}
body,
html {
  margin: 0;
  height: 100%;
}
#app {
  width: 50%;
}

nav {
  padding: 20px 20px 20px 0px;
}

nav a {
  padding: 10px;
  text-decoration: none;
  background: #ffffff;
  border-radius: 3px;
  color: rgb(0, 110, 255);
  font-weight: bold;
  margin-right: 15px;
}
</style>
