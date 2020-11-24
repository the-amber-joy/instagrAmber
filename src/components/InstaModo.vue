<template>
  <div class="all">
    <h1>{{ title }}</h1>
    <div class="media">
      <div v-for="(item, index) in allMedia" v-bind:key="index">
        <template v-if="item.format === 'photo'">
          <figure>
            <img v-bind:src="'/assets/' + item.path" />
            <figcaption>
              {{
                new Date(item.taken_at)
                  | dateFormat("dddd, MMMM DD,", dateFormatConfig)
              }}<br />
              {{
                new Date(item.taken_at)
                  | dateFormat("YYYY h:mma", dateFormatConfig)
              }}<br />
              <span class="caption">{{ item.caption }}</span>
            </figcaption>
          </figure>
          <hr />
        </template>
        <template v-else>
          <figure>
            <video id="video" controls preload="metadata">
              <source v-bind:src="'/assets/' + item.path" type="video/mp4" />
            </video>
            <figcaption>
              {{
                new Date(item.taken_at)
                  | dateFormat("dddd, MMMM DD,", dateFormatConfig)
              }}<br />
              {{
                new Date(item.taken_at)
                  | dateFormat("YYYY h:mma", dateFormatConfig)
              }}<br />
              <span class="caption">{{ item.caption }}</span>
            </figcaption>
          </figure>
          <hr />
        </template>
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
figcaption {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3;
  overflow: hidden;
}
</style>
