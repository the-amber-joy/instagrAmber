<template>
  <div class="all">
    <h1>{{ title }}</h1>
    <div class="media">
      <div
        v-for="(item, index) in allMedia"
        v-bind:key="index"
        class="container"
      >
        <figure>
          <template v-if="item.format === 'photo'">
            <img v-on:click="openItem(item)" v-bind:src="item.path" />
          </template>
          <template v-else>
            <video v-on:click="openItem(item)" v-bind:src="item.path">
              <source v-bind:src="'/assets/' + item.path" type="video/mp4" />
            </video>
          </template>
          <figcaption v-on:click="toggleCaption($event, item)">
            <span v-html="item.icon"></span>
            {{
              new Date(item.taken_at)
                | dateFormat("dddd, MMMM DD,", dateFormatConfig)
            }}<br />
            {{
              new Date(item.taken_at)
                | dateFormat("YYYY h:mma", dateFormatConfig)
            }}<br />
            <span class="caption" :class="{ expandCaption: item.isActive }">{{
              item.caption
            }}</span>
          </figcaption>
        </figure>
        <hr />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "InstaModo",
  props: {
    title: String,
    allMedia: Array,
    dateFormatConfig: Object
  },
  methods: {
    openItem: function(item) {
      window.open(item.path);
    },
    toggleCaption: function(event, item) {
      item.isActive = !item.isActive;
    }
  }
};
</script>

<style scoped>
.media {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  grid-template-rows: repeat(auto, minmax(300px, 1fr));
  grid-gap: 1rem;
  grid-auto-flow: dense;
}
img,
video {
  max-width: 200px;
}
hr {
  position: absolute;
  bottom: 0;
  width: 100%
}
figcaption {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3;
  overflow: hidden;
  cursor: pointer;
}
.container {
  position: relative;
}
.expandCaption {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: none;
  overflow: show;
}
</style>
