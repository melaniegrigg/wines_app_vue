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
      <input type="submit" class="btn btn-primary" value="Submit">
    </form>

     <h1>Wines You've Rated</h1>
      <div v-for="rating in ratings" class="ratings">
        <h2>Vintner: {{rating.vintner}}</h2>
        <h3>Rating: {{rating.rating}}</h3>
        <h3>Notes: {{rating.notes}}</h3>
        <button v-on:click="showRating(rating)">Edit/Delete</button>
      </div>
    <dialog style="color:pink" id="rating-details">
      <form method="dialog">
        <h1 style="color:pink">Rating Info</h1>
        <p>Vintner: <input style="color:purple" v-model="currentRating.vintner"></p>
        <p>Rating: <input style="color:purple" v-model="currentRating.rating"></p>
        <p>Notes: <input style="color:purple" v-model="currentRating.notes"></p>
        <button v-on:click="updateRating(currentRating)"><h3 style="color:purple">Save</h3></button>
        <button><h3 style="color:purple">Close</h3></button>
        <button v-on:click="destroyRating(currentRating)"><h3 style="color:purple">Delete</h3></button>
      </form>
    </dialog>

    <!-- <div class="ratings">
      <h1>Wines You've Rated</h1>
      <div v-for="rating in ratings" class="ratings">
        <h2>Vintner: {{rating.vintner}}</h2>
        <h3>Rating: {{rating.rating}}</h3>
        <h3>Notes: {{rating.notes}}</h3>
        <button v-on:click="updateRating(currentRating)">Edit this rating</button>
        <button v-on:click="deleteRating(currentRating)">Delete Rating</button>
      </div>
    </div> -->
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
      console.log("current user's ratings");
      axios.get("/api/ratings").then((response) => {
        console.log(response.data);
        this.ratings = response.data;
      });
    },
    submit: function () {
      var params = {
        vintner: this.newVintner,
        rating: this.newRating,
        notes: this.newNotes,
      };

      console.log(params);

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
      console.log(rating);
      this.currentRating = rating;
      document.querySelector("#rating-details").showModal();
    },
    updateRating: function (rating) {
      console.log(rating);

      var params = {
        vintner: rating.vintner,
        rating: rating.rating,
        notes: rating.notes,
      };
      axios.patch("/api/ratings/" + rating.id, params).then((response) => {
        console.log(response.data);
        this.currentRating = response.data;
      });
    },
    destroyRating: function (rating) {
      console.log(rating);
      axios.delete("/api/ratings/" + rating.id).then((response) => {
        console.log(response.data);
        var index = this.ratings.indexOf(rating);

        this.ratings.splice(index, 1);
        console.log(index);
      });
    },
  },
};
</script>

