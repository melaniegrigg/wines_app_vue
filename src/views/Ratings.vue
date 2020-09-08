<template>
  <div class="ratings">
    <h1>{{ message }}</h1>

      <!-- New rating-form -->
    <form v-on:submit.prevent="submit()">
      <h1>Create a new rating</h1>
      <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>Vintner</label> 
        <input type="text" class="form-control" v-model="newVintner">
      </div>
      <div class="form-group">
        <label>Rating</label>
        <input type="text" class="form-control" v-model="newRating">
      </div>
      <div class="form-group">
        <label>Notes</label>
        <input type="text" class="form-control" v-model="newNotes">
      </div>
      <!-- submit button -->
      <input type="submit" class="btn btn-primary" value="Submit">
    </form>

    <!-- Index current users ratings-must be logged in -->
     <h1>Your Cellar Ratings...</h1>
      <div v-for="rating in ratings" class="ratings">
        <hr>
        <h2>Vintner: {{rating.vintner}}</h2>
        <h4>Rating: {{rating.rating}}</h4>
        <h4>Notes: {{rating.notes}}</h4>
        <button v-on:click="showRating(rating)">Edit This Rating</button>
      </div>

      <!-- Modal For Delete/edit actions -->
    <dialog style="color:#ff66cc" id="rating-details">
      <form method="dialog">
        <h1 style="color:#ff66cc">Rating Info</h1>
        <p>Vintner: <input style="color:#660033" v-model="currentRating.vintner"></p>
        <p>Rating: <input style="color:#660033" v-model="currentRating.rating"></p>
        <p>Notes: <input style="color:#660033" v-model="currentRating.notes"></p>
        <button v-on:click="updateRating(currentRating)"><h3 style="color:#660033">Save</h3></button>
        <button><h3 style="color:#660033">Close</h3></button>
        <button v-on:click="destroyRating(currentRating)"><h3 style="color:#660033">Delete</h3></button>
      </form>
    </dialog>
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
      newRating: "",
      newNotes: "",
      newVintner: "",
      currentRating: {},
      errors: [],
    };
  },
  created: function (rating) {
    this.indexRatings(rating);
  },
  methods: {
    indexRatings: function () {
      axios.get("/api/ratings").then((response) => {
        this.ratings = response.data;
      });
    },
    submit: function () {
      var params = {
        vintner: this.newVintner,
        rating: this.newRating,
        notes: this.newNotes,
      };

      axios
        .post("/api/ratings", params)
        .then((response) => {
          this.$router.push("/");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    showRating: function (rating) {
      this.currentRating = rating;
      document.querySelector("#rating-details").showModal();
    },
    updateRating: function (rating) {
      var params = {
        vintner: rating.vintner,
        rating: rating.rating,
        notes: rating.notes,
      };
      axios.patch("/api/ratings/" + rating.id, params).then((response) => {
        this.currentRating = response.data;
      });
    },
    destroyRating: function (rating) {
      axios.delete("/api/ratings/" + rating.id).then((response) => {
        var index = this.ratings.indexOf(rating);

        this.ratings.splice(index, 1);
      });
    },
  },
};
</script>

