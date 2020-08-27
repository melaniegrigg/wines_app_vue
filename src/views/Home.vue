<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>{{ message2 }}</h2>
    <p>{{ tags }}</p>
    <tags-input element-id="tags"
    v-model="selectedTags"
    :existing-tags="[
        { key: 'web-development', value: 'Web Development' },
        { key: 'php', value: 'PHP' },
        { key: 'javascript', value: 'JavaScript' },
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
        "Just select your taste preferences and we will select wine varietals that match",
      tags: [],
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
  },
};
</script>
