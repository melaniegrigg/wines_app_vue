<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>{{ message2 }}</h2>
    <p v-for="tag in tags" > {{tag.tag}}</p>
    </button>
    <button v-on:click="selectTag">Which Wine?
    </button>
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
    selectTag: function () {
      console.log("sending tags to wine_tags");

      var params = {
        tag: "this tag is selected",
      };
      axios.get("/api/wine_tags", params).then((response) => {
        console.log(response.data);
        this.wine_tags.push(response.data);
      });
    },
  },
};
</script>
