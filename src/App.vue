<template>
<html>
	<head>
		<title>Which Wine? : Melanie Grigger</title>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no" />
		<link rel="stylesheet" href="assets/css/main.css" />
		<noscript><link rel="stylesheet" href="assets/css/noscript.css" /></noscript>
	</head>
	<body class="is-preload">

		<!-- Wrapper -->
  <div id="wrapper">

    <!-- Header -->
      <header id="header" class="alt">
        <span class="logo"><img src="https://i0.wp.com/www.eatthis.com/wp-content/uploads/2019/08/wine-and-cheese-board.jpg?fit=1200%2C879&ssl=1" alt="Wine and cheese board" width="500"/></span>
        <h1>Which Wine?</h1>
        <h2 class="logo">Simpifying wine selection</h2>
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

    <!-- Main -->
      <div id="main">

        <!-- Introduction -->
          <section id="intro" class="main">
            <div class="spotlight">
              <div class="content">
                <header class="major">
                  <h2>Select your taste or smell preferences and get your personalized wine varietal</h2>
                </header>
                <ul class="actions">
                  <li><a href="/signup">Create an account</a> or<a href="/login"> log in</a> to save or rate particular wines by Vintner.</li>
                </ul>
              </div>
              <span class="image"><img src="https://i.pinimg.com/originals/b2/c3/76/b2c376a572acc4d1e81dffe555b7b635.jpg" alt="" /></span>
            </div>
          </section>

          <!-- <section id="first" class="main special">
            <div class
          </section>

          <section id="second" class="main special">
          </section> -->

      </div>
      <router-view/>

    <!-- Footer -->
      <footer id="footer">
        <section>
          <h2>About Which Wine</h2>
          <p>"Which Wine?" is a web app made by Melanie Grigger for a portfolio project. It utilizes Ruby, Rails, VueJS, ActiveRecord, Restful Routes, HTML, CSS and Javascript to create a full stack, user friendly application for wine selection.</p>
          <ul class="actions">
            <li><a href="http://melaniegrigger.com/" class="button">Contact Me</a></li>
          </ul>
        </section>
        <section>
          <h2>Like what you see? Check out my other work.</h2>
          <ul class="icons">
            <li><a href="#" class="icon brands fa-twitter alt"><span class="label">Twitter</span></a></li>
            <li><a href="#" class="icon brands fa-facebook-f alt"><span class="label">Facebook</span></a></li>
            <li><a href="#" class="icon brands fa-instagram alt"><span class="label">Instagram</span></a></li>
            <li><a href="#" class="icon brands fa-github alt"><span class="label">GitHub</span></a></li>
          </ul>
        </section>
        <p class="copyright">&copy; Melanie Grigger. Design: <a href="https://html5up.net">HTML5 UP</a>.</p>
      </footer>

  </div>
	</body>
</html>
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
