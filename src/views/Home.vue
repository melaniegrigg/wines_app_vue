<template>
  <div  class="home">
    <h1>{{ message }}</h1>
    <h2>{{ message2}}</h2>
    <h2>Funky</h2>
    <div class="dropdown">
    <select v-model='funkys'>
      <option v-for='funky in funkys' :value='funky.id'>{{ funky.tag }}</option>
    </select>
    </div>
    <h2>Fruity</h2>
    <div class="dropdown">
    <select v-model='fruitys'>
      <option v-for='fruity in fruitys' :value='fruity.id'>{{ fruity.tag }}</option>
    </select>
    </div>
    <h2>Earthy</h2>
    <div class="dropdown">
    <select v-model='earthys'>
      <option v-for='earthy in earthys' :value='earthy.id'>{{ earthy.tag }}</option>
    </select>
    </div>
    <h2>Sweet</h2>
    <div class="dropdown">
    <select v-model='sweets'>
      <option v-for='sweet in sweets' :value='sweet.id'>{{ sweet.tag }}</option>
    </select>
    </div>
    <!-- <section id="first" class="main special">
      <div v-for="funky in funkys">
        <input type="checkbox" v-bind:id="funky.id" v-model="selectedTags" v-bind:value="funky.id">
        <label v-bind:for="funky.id"> {{ funky.tag }}</label><br>
      </div> -->
      <button v-on:click="getWines" type="submit" class="btn btn-primary" id="sendWinesButton">Which Wine? </button>
      <h1> Here are your suggested varietals! <br>Choose one to rate: </h1>
      <h2 v-for="wine in wines"><a href="/ratings"> {{wine.varietal}} </a></h2>
    </section>
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
        "Select one tase or smell preference from each menu below and get matched with your personalized wine varietals instantly!",
      tags: [],
      funkys: [],
      fruitys: [],
      earthys: [],
      sweets: [],
      selectedTags: [],
      wines: [],
    };
  },
  // created: function () {
  //   this.indexTags1();
  // },
  created: function () {
    this.indexTags();
  },
  methods: {
    indexTags: function () {
      console.log("indexing funkyTags");
      axios.get("/api/tags").then((response) => {
        console.log(response.data);
        this.tags = response.data;
      });
    },
    indexFunkys: function () {
      console.log("indexing funkyTags");
      axios.get("/api/tags").then((response) => {
        console.log(response.data);
        this.funkys = response.data;
      });
    },
    indexFruitys: function () {
      console.log("indexing fruityTags");
      axios.get("/api/tags").then((response) => {
        console.log(response.data);
        this.fruitys = response.data;
      });
    },
    indexEarthys: function () {
      console.log("indexing earthyTags");
      axios.get("/api/tags").then((response) => {
        console.log(response.data);
        this.earthys = response.data;
      });
    },
    indexSweets: function () {
      console.log("indexing sweetTags");
      axios.get("/api/tags").then((response) => {
        console.log(response.data);
        this.sweets = response.data;
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
