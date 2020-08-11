<template>
  <div class="home">
    <h1>{{ message }}</h1>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      wines: [],
    };
  },
  created: function () {},
  methods: {
    indexWines: function () {
      axios;
    },
  },
};
</script>
