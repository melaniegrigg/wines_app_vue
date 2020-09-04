<template>
  <div  class="home">
    <h1>{{ message }}</h1>
    <div class="container-fluid">
      <div class="row">
        <div class="col-md-10">
          <div v-for="tag in tags">
            <input type="checkbox" v-bind:id="tags1" v-model="selectedTags" v-bind:value="tags1">
            <label v-bind:for="tags1"> {{ tag.tag }}</label>
          </div>
          <div v-for="tags2 in tags">
            <input type="checkbox" v-bind:id="tags2" v-model="selectedTags" v-bind:value="tags2">
            <label v-bind:for="tags2"> {{ tags2.tag }}</label>
          </div>
      </div>
      <div class="row">
        <div class="col-md-6">
          <div v-for="tags3 in tags">
            <input type="checkbox" v-bind:id="tags3" v-model="selectedTags" v-bind:value="tags3">
            <label v-bind:for="tags3"> {{ tags3.tag }}</label>
          </div>
            <div v-for="tags4 in tags">
              <input type="checkbox" v-bind:id="tags4" v-model="selectedTags" v-bind:value="tags4">
              <label v-bind:for="tags4"> {{ tags2.tag }}</label>
          </div>
      </div>
      <button v-on:click="getWines" type="submit" class="btn btn-primary" id="sendWinesButton">Which Wine? </button>
      <h1> Wine Selection: </h1>
      <h2 v-for="wine in wines"><a href="/ratings"> {{wine.varietal}} </a></h2>
    </div>
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
      tags1: [],
      tags2: [],
      tags3: [],
      tags4: [],
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
    types: function (tags) {
      return tags.filter(function (tag) {
        return tag.type === "sweet";
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
