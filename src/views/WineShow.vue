<template>
  <div class="ratings">
    <h1>{{ message }}</h1>
    <h1 v-bind-model="showWines()">{{ wines }}</h1>

    <!-- <p><button v-on:click="saveWine()">Save Post</button></p> -->
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Here are your wines",
      wines: [],
    };
  },
  created: function () {
    this.showWines();
  },
  methods: {
    showWines: function () {
      console.log("showing");
      console.log(this.$route);

      axios.get(`/api/wines`).then((response) => {
        console.log(response.data);
        this.wines = response.data;
      });
    },
    // ratePost: function () {
    //   console.log("deleting the recipe");
    // },
  },
};
</script>