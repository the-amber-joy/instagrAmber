<template>
  <div class="all">
    <h1>{{ title }}</h1>
    <div v-for="(item, index) in allMedia" v-bind:key="index">
      <template v-if="item.format === 'photo'">
      <hr>
        <figure>
          <figcaption>
            {{
              new Date(item.taken_at)
                | dateFormat("dddd, MMMM DD, YYYY h:mma", dateFormatConfig)
            }} <br />
            {{ item.caption }}
          </figcaption>
          <img v-bind:src="'/assets/' + item.path" />
        </figure>
      </template>
      <template v-else>
        <hr>
        <figure>
          <figcaption>
            {{
              new Date(item.taken_at)
                | dateFormat("dddd, MMMM DD, YYYY h:mma", dateFormatConfig)
            }}<br />
            {{ item.caption }}
          </figcaption>
          <video id="video" controls preload="metadata">
            <source v-bind:src="'/assets/' + item.path" type="video/mp4" />
          </video>
        </figure>
      </template>
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
