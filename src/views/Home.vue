<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>{{ message2 }}</h2>
    <div class="form-check form-check-inline">
      <input class="form-check-input" type="checkbox" id="inlineCheckbox1" value="option1">
      <label class="form-check-label" for="inlineCheckbox1">
        <div v-for="tag in tags" class="tag-name">
            <a v-bind:href="`/tags/${tag.tag}`">
              <h2 class="tag-tag">
                {{ tag.tag }}
              </h2>
            </a>
        </div>
      </label>
    </div>
    <div class="form-check form-check-inline">
      <input class="form-check-input" type="checkbox" id="inlineCheckbox2" value="option2">
      <label class="form-check-label" for="inlineCheckbox2">2</label>
    </div>
    <div class="form-check form-check-inline">
      <input class="form-check-input" type="checkbox" id="inlineCheckbox3" value="option3" disabled>
      <label class="form-check-label" for="inlineCheckbox3">3 (disabled)</label>
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
      message:
        "Welcome to Which Wine! Making wine selection simple by matching your tastes with wine varietals. ",
      message2:
        "Search your current taste preferences and we will select wine varietals for you that match",
      tags: [],
      wines: [],
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
    showWine: function () {
      console.log("showing wines");
      axios.get("/api/wines").then((response) => {
        console.log(response.data);
        this.wines = response.data;
      });
    },
  },
};
</script>
