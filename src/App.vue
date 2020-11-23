<template>
  <div id="app">
    <InstaModo msg="Insta-Quasi-Clone-Modo" :photos="photos" />
  </div>
</template>

<script>
import Vue from "vue";
import VueFilterDateFormat from "@vuejs-community/vue-filter-date-format";
import sortBy from "lodash/sortBy";
import * as metadata from "@/assets/media.json";
import InstaModo from "./components/InstaModo.vue";

Vue.use(VueFilterDateFormat);

export default {
  name: "App",
  components: {
    InstaModo,
  },
  data: () => ({
    photos: sortBy(metadata.photos, "taken_at"),
    videos: metadata.videos,
    dateFormatConfig: {
      dayOfWeekNames: [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
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
        "December",
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
        "Dec",
      ],
      // Timezone offset, in minutes (0 - UTC, 180 - Russia, undefined - current)
      timezone: -360,
    },
  }),
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
