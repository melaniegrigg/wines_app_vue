<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>{{ message2 }}</h2>
    <p>{{ wines }}</p>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Which Wine!",
      message2:
        "Just select your taste preferences and we will select wine varietals that match",
      wines: [],
    };
  },
  created: function () {
    this.indexWines();
  },
  methods: {
    indexWines: function () {
      console.log("indexing wines");
      axios.get("/api/wines").then((response) => {
        console.log(response.data);
        this.wines = response.data;
      });
    },
  },
};
</script>
