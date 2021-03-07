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

const assetPath = process.env.VUE_APP_ASSET_PATH;

const photos = map(metadata.photos, photo => {
  return {
    ...photo,
    format: "photo",
    icon: "&#x1F4F7;",
    path: `${assetPath}/${photo.path}`,
    isActive: false
  };
});
const videos = map(metadata.videos, video => {
  return {
    ...video,
    format: "video",
    icon: "&#9654;&#65039;",
    path: `${assetPath}/${video.path}`,
    isActive: false
  };
});
const allMedia = sortBy(concat(photos, videos), "taken_at").reverse();

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
