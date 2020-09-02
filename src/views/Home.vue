<template>
  <div  class="home">
    <h1>{{ message }}</h1>
    <div class="container-fluid">
      <div class="row">
      {{ selectedTags }}
      <div class="col-sm">
      <div v-for="tag in tags">
        <input type="checkbox" v-bind:id="tag.id" v-model="selectedTags" v-bind:value="tag.id">
        <label v-bind:for="tag.id"> {{ tag.tag }}</label><br>
      </div>
      </div>
        </div>
      </div>
      <button v-on:click="getWines" type="submit" class="btn btn-primary" id="sendWinesButton">Which Wine? </button>
      <h1> Wine Selection: </h1>
      <h2 v-for="wine in wines"> {{wine}}</h2>
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
