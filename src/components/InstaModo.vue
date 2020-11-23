<template>
  <div class="all">
    <h1>{{ title }}</h1>
    <vue-masonry-wall :items="items" :ssr="{columns: 2}" :options="{ width: 100, padding: 6 }">
      <template v-slot:default="{ item }">
        <div v-if="item.format === 'photo'">
          <hr />
          <figure>
            <figcaption>
              {{ item.taken_at }}
              {{ item.caption }}
            </figcaption>
            <img v-bind:src="'/assets/' + item.path" width="200px">
          </figure>
        </div>
        <div v-else>
          <hr />
          <figure>
            <figcaption>
              {{ item.taken_at }}
              {{ item.caption }}
            </figcaption>
            <video id="video" controls preload="metadata">
              <source v-bind:src="'/assets/' + item.path" type="video/mp4" />
            </video>
          </figure>
        </div>
      </template>
    </vue-masonry-wall>
  </div>
</template>

<script>
export default {
  name: "InstaModo",
  props: {
    title: String,
    items: Array,
    dateFormatConfig: Object
  }
};
</script>
