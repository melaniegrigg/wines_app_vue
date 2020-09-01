<template>
  <div  class="home">
    <h1>{{ message }}</h1>
    <div class="container">
      {{ selectedTags }}
      <div v-for="tag in tags">
        <input type="checkbox" v-bind:id="tag.id" v-model="selectedTags" v-bind:value="tag.id">
        <label v-bind:for="tag.id"> {{ tag.tag }}</label><br>
      </div>
      <button v-on:click="getWines" type="submit" class="btn btn-primary" id="sendWinesButton">Which Wine? </button>
      <div v-for="wine in wines">
      <h1 v-bind:varietal="wine.varietal" v-bind:color="wine.color">
        <h1> {{wine.varietal}}</h1>
        </h1>
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
      selectedTags: [],
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
    getWines: function () {
      var params = {
        tags: this.selectedTags,
      };
      console.log(this.selectedTags);
      axios
        .get("/api/wines", {
          params: {
            tags: this.selectedTags,
          },
        })
        .then((response) => {
          console.log(response.data);
          this.wines = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
