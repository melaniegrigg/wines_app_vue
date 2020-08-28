<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>{{ message2 }}</h2>
    <h2> {{ tags }}</h2>
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
  },
};
</script>
