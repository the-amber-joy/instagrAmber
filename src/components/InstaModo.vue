<template>
  <div class="all">
    <h1>{{ msg }}</h1>
    <div v-for="photo in photos" v-bind:key="photo.path" width="20%">
      <figure>
        <img v-bind:src="'/assets/' + photo.path" />
        <figcaption>
          {{
            new Date(photo.taken_at)
              | dateFormat("dddd, MMMM DD, YYYY h:mm a", dateFormatConfig)
          }}
          {{ photo.caption }}<br />
        </figcaption>
      </figure>
    </div>
  </div>
</template>

<script>
export default {
  name: "InstaModo",
  props: {
    msg: String,
    photos: Array,
    dateFormatConfig: Object
  }
};
</script>
