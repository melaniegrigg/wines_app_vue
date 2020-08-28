<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>{{ message2 }}</h2>
    <voerro-tags-input element-id="tags"
    v-model="selectedTags"
    :index="[
        { key: tags, value: selectedTags}
    ]"
    :typeahead="true"></voerro-tags-input>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
import VoerroTagsInput from "@voerro/vue-tagsinput";

export default {
  components: {
    VoerroTagsInput,
  },
  props: {
    typehead: { type: Boolean, default: false },
  },
  data: function () {
    return {
      message:
        "Welcome to Which Wine! Making wine selection simple by matching your tastes with wine varietals. ",
      message2:
        "Search your current taste preferences and we will select wine varietals for you that match",
      tags: [],
      selectedTags: [],
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
      this.selectedTags = [{ key: "tags", value: this.selectedTags }];
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
