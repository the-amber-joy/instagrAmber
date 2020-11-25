<template>
  <div id="app">
    <Gallery :title="title" :allMedia="allMedia" />
  </div>
</template>

<script>
import Vue from "vue";
import VueFilterDateFormat from "@vuejs-community/vue-filter-date-format";
import map from "lodash/map";
import sortBy from "lodash/sortBy";
import concat from "lodash/concat";
import * as metadata from "@/assets/media.json";
import dateFormatConfig from "@/assets/dateFormatConfig.json";
import Gallery from "./components/Gallery.vue";

Vue.use(VueFilterDateFormat);

const photos = map(metadata.photos, photo => {
  return {
    format: "photo",
    ...photo
  };
});
const videos = map(metadata.videos, video => {
  return {
    format: "video",
    ...video
  };
});
const allMedia = sortBy(concat(photos, videos), "taken_at");

export default {
  name: "App",
  components: {
    Gallery
  },
  data: () => ({
    title: "instagrAmber",
    allMedia,
    dateFormatConfig
  })
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
