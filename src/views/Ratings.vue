<template>
  <div class="ratings">
    <h1>{{ message }}</h1>
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

    <div class="ratings">
      <h1>Wines You've Rated</h1>
      <div v-for="rating in ratings" class="ratings">
        <h1>Vintner: {{rating.vintner}}</h1>
        <h1>Rating: {{rating.rating}}</h1>
        <h1>Notes: {{rating.notes}}</h1>
        <a v-bind:href="`/ratings/edit${rating.id}/edit`">Edit this rating</a>
        <button v-on:click="deleteRating()">Delete Rating</button>
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
    deleteRating: function () {
      console.log("deleting the rating");
      axios.get(`/api/ratings/${this.$route.params.id}`).then((response) => {
        console.log(response.data);
        this.$router.push("/ratings");
      });
    },
  },
};
</script>

