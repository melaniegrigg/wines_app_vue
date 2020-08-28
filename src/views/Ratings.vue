<template>
  <div class="ratings">
    <h1>{{ message }}</h1>
    <p>{{ ratings }}</p>
    <form v-on:submit.prevent="submit()">
      <h1>Create a new rating</h1>
      <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>Vintner</label> 
        <input type="text" class="form-control" v-model="vintner">
      </div>
      <div class="form-group">
        <label>Varietal</label>
        <input type="text" class="form-control" v-model="varietal">
      </div>
      <div class="form-group">
        <label>Rating</label>
        <input type="text" class="form-control" v-model="rating">
      </div>
      <div class="form-group">
        <label>Notes</label>
        <input type="text" class="form-control" v-model="notes">
      </div>
      <input type="submit" class="btn btn-primary" value="Submit">
    </form>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "View, rate and edit your saved wines here.",
      ratings: [],
      vintner: "",
      varietal: "",
      rating: "",
      notes: "",
      errors: [],
    };
  },
  created: function () {
    this.indexRatings();
  },
  methods: {
    indexRatings: function () {
      console.log("current user's ratings");
      axios.get("/api/ratings").then((response) => {
        console.log(response.data);
        this.ratings = response.data;
      });
    },
    submit: function () {
      var params = {
        vinter: this.vinter,
        varietal: this.varietal,
        rating: this.rating,
        notes: this.notes,
      };
      axios
        .post("/api/ratings", params)
        .then((response) => {
          console.log(response.data);
          this.ratings = response.data;
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

