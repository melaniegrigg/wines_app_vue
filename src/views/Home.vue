<template>
  <div  class="home">
    <h1>{{ message }}</h1>
    <h2>{{ message2 }}</h2>

    <!-- Dropdown menu-FUNKY -->
    <h2>Funky</h2>
      <div class="dropdown">
      <select v-model="funkyId">
        <option v-for='funky in funkys' :value='funky.id'>{{ funky.tag }}</option>
      </select>
      </div>
      <!-- Dropdown menu-FRUITY -->
    <h2>Fruity</h2>
      <div class="dropdown">
      <select v-model="fruityId">
        <option v-for='fruity in fruitys' :value='fruity.id'>{{ fruity.tag }}</option>
      </select>
      </div>
      <!-- Dropdown menu-EARTHY -->
    <h2>Earthy</h2>
      <div class="dropdown">
      <select v-model="earthyId">
        <option v-for='earthy in earthys' :value='earthy.id'>{{ earthy.tag }}</option>
      </select>
      </div>
      <!-- Dropdown menu-SWEET -->
    <h2>Sweet</h2>
      <div class="dropdown">
      <select v-model='sweetId'>
        <option v-for='sweet in sweets' :value='sweet.id'>{{ sweet.tag }}</option>
      </select>
    </div>
    <!-- Wine select button-returns varietals -->
      <button v-on:click="getWines" type="submit" class="btn btn-primary" id="sendWinesButton">Which Wine? </button>
      <h1> Here are your suggested varietals! <br>Choose one to rate: </h1>
      <h2 v-for="wine in wines"><a href="/ratings"> {{wine.varietal}} </a></h2>
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
        "Select your smell or taste preferences from the menus below and get matched with your personalized wine varietals instantly!",
      tags: [],
      funkyId: "",
      fruityId: "",
      earthyId: "",
      sweetId: "",
      funkys: [],
      fruitys: [],
      earthys: [],
      sweets: [],
      selectedTags: [],
      wines: [],
    };
  },
  created: function () {
    this.indexTags();
  },
  methods: {
    indexTags: function () {
      console.log("indexing sweetTags");
      axios.get("/api/tags").then((response) => {
        console.log(response.data);
        this.funkys = response.data[0];
        this.fruitys = response.data[1];
        this.earthys = response.data[2];
        this.sweets = response.data[3];
      });
    },
    getWines: function () {
      var params = {
        tags: [this.funkyId, this.fruityId, this.earthyId, this.sweetId],
      };
      console.log(this.funkyId);
      axios
        .get("/api/wines", {
          params: {
            tags: [this.funkyId, this.fruityId, this.earthyId, this.sweetId],
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
