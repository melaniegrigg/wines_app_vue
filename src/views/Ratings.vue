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
        <label>Rating</label>
        <input type="text" class="form-control" v-model="rating">
      </div>
      <div class="form-group">
        <label>Notes</label>
        <input type="text" class="form-control" v-model="notes">
      </div>
      <input type="submit" class="btn btn-primary" value="Submit">
    </form>

    <div class="card text-center">
      <div class="card-header">
        A Rating
      </div>
      <div class="card-body">
        <h5 class="card-title">Ratings</h5>
        <p class="card-text"> Notes </p>
        <a href="#" class="btn btn-primary">Edit Rating</a>
      </div>
      <div class="card-footer text-muted">
          2 days ago
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
      message: "View, rate and edit your saved wines here.",
      ratings: [],
      rating: "",
      notes: "",
      vintner: "",
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
        vintner: this.vintner,
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

