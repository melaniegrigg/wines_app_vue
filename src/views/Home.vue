<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>{{ message2 }}</h2>
    <tags-input element-id="tags"
    v-model="selectedTags"
    :existing-tags="[
        { key: tags, value: tagsinput}
    ]"
    :typeahead="true"></tags-input>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
import VoerroTagsInput from "@voerro/vue-tagsinput";

export default {
  data: function () {
    return {
      message:
        "Welcome to Which Wine! Making wine selection simple by matching you with wine varietals that suite your current taste preferences. ",
      message2:
        "Search your current taste preferences and we will select wine varietals for you that match",
      tags: [],
    };
  },
  created: function () {
    this.indexTags();
    this.selectedTags();
  },
  methods: {
    indexTags: function () {
      console.log("indexing Tags");
      axios.get("/api/tags").then((response) => {
        console.log(response.data);
        this.tags = response.data;
      });
    },
    selectedTags: function () {
      this.selectedTags = [{ key: "selected", value: "selected:" }];
    },
    submit: function () {
      var params = {
        tags: this.selectTags,
        wines: this.wineTags,
      };
      axios
        .post("/api/wines", params)
        .then((response) => {
          this.$router.push("/wines");
        })
        .cath((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
