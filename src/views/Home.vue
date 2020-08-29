<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>{{ message2 }}</h2>
    <button v-on:click="showWine" v-for="tag in tags" > {{tag.tag}}
    </li></button>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message:
        "Welcome to Which Wine! Making wine selection simple by matching your tastes with wine varietals. ",
      message2:
        "Search your current taste preferences and we will select wine varietals for you that match",
      tags: [],
      wines: [],
    };
  },
  created: function () {
    this.indexTags();
  },
  methods: {
    indexTags: function () {
      console.log("indexing Tags");
      axios.get("/api/tags").then((response) => {
        console.log(response.data);
        this.tags = response.data;
      });
    },
    showWine: function () {
      console.log("showing wines");
      axios.get("/api/wines").then((response) => {
        console.log(response.data);
        this.wines = response.data;
      });
    },
  },
};
</script>
