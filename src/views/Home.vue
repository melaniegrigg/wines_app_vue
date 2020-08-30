<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div class="container">
      {{ selectedTags }}
      <div v-for="tag in tags">
        <input type="checkbox" v-bind:id="tag.id" v-model="selectedTags" v-bind:value="tag.id">
        <label v-bind:for="tag.id"> {{ tag.tag }}</label><br>
      </div>
    </div>
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
      selectedTags: [3],
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
    submit: function () {
      var params = {
        tag: this.tags,
      };
      axios
        .post("/api/wine_tags", params)
        .then((response) => {
          this.$router.push("/wine_tags");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
