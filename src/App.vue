<template>
  <div id="app">
    <div id="wrapper">

      <!-- Header -->
      <header id="header" class="alt">
      </header>

      <!-- Nav -->
      <nav id="nav">
        <ul>
          <li><a href="/" class="active">Which Wine?</a></li>
          <li><a href="/Ratings">Ratings</a></li>
          <li v-if="!isLoggedIn()"><a href="/LogIn">Login</a></li>
          <li v-if="isLoggedIn()"><a href="/LogOut">Logout</a></li>
          <li><a href="/Signup">Signup</a></li>
        </ul>
      </nav>

       <router-view/>

      <!-- Footer -->
      <footer id="footer">
        <section>
          <ul class="icons">
            <li><a href="https://twitter.com/MelanieGrigger" class="icon brands fa-twitter alt"><span class="label">Twitter</span></a></li>
            <li><a href="#" class="icon brands fa-facebook-f alt"><span class="label">Facebook</span></a></li>
            <li><a href="#" class="icon brands fa-instagram alt"><span class="label">Instagram</span></a></li>
            <li><a href="https://github.com/melaniegrigg" class="icon brands fa-github alt"><span class="label">GitHub</span></a></li>
          </ul>
        </section>
        <p class="copyright">&copy; Melanie Grigger: Design: <a href="https://html5up.net">HTML5 UP</a>.</p>
      </footer>

        <!-- </div>
      <div id="nav">
        <router-link to="/">Home</router-link> |
        <router-link to="/ratings">Ratings</router-link> |
        <span v-if="!isLoggedIn()"><router-link to="/signup">Signup</router-link></span>|
        <span v-if="!isLoggedIn()"><router-link to="/login">Login</router-link></span>|
        <span v-if="isLoggedIn()"><router-link to="/logout">Logout</router-link> </span>
      </div> -->
    </div>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
<script>
import axios from "axios";

export default {
  methods: {
    isLoggedIn: function () {
      if (localStorage.getItem("jwt")) {
        return true;
      } else {
        return false;
      }
    },
    getUserID: function () {
      return localStorage.getItem("user_id");
    },
  },
};
</script>