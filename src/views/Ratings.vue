<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p>{{ ratings }}</p>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "View, rate and edit your saved wines here.",
      ratings: [],
    };
  },
  created: function () {
    this.indexRatings();
  },
  methods: {
    indexRatings: function () {
      console.log("current user's ratings");
      axios.get("/api/ratings").then((response) => {
        console.log(response.data);
        this.current_user.ratings = response.data;
      });
    },
  },
};
</script>
