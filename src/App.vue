<template>
  <div id="app">
    <InstaModo :title="title" :items="items" />
  </div>
</template>

<script>
import Vue from "vue";
import VueFilterDateFormat from "@vuejs-community/vue-filter-date-format";
import VueMasonryWall from "vue-masonry-wall";
import map from "lodash/map";
import sortBy from "lodash/sortBy";
import concat from "lodash/concat";
import * as metadata from "@/assets/media.json";
import InstaModo from "./components/InstaModo.vue";

Vue.use(VueMasonryWall);
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
    InstaModo
  },
  data: () => ({
    title: "instagrAmber",
    items: allMedia,
    dateFormatConfig: {
      dayOfWeekNames: [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday"
      ],
      dayOfWeekNamesShort: ["Su", "Mo", "Tu", "We", "Tr", "Fr", "Sa"],
      monthNames: [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December"
      ],
      monthNamesShort: [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May",
        "Jun",
        "Jul",
        "Aug",
        "Sep",
        "Oct",
        "Nov",
        "Dec"
      ],
      timezone: -360
    }
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
