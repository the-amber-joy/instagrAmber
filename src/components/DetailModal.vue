<template>
  <transition name="modal">
    <div class="modal-mask" @click="$emit('modalClose')">
      <div class="modal-wrapper">
        <div class="modal-container">
          <div class="modal-header">
            <slot name="header">
              {{ mediaDate }}
            </slot>
          </div>

          <div class="modal-body">
            <slot name="body">
              <template v-if="mediaFormat === 'photo'">
                <img v-bind:src="mediaPath" />
              </template>
              <template v-else>
                <video v-bind:src="mediaPath" controls autoplay>
                  <source
                    v-bind:src="'/assets/' + mediaPath"
                    type="video/mp4"
                  />
                </video>
              </template>
            </slot>
          </div>

          <div class="modal-footer">
            <slot name="footer">
              {{ mediaCaption }}
            </slot>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "DetailModal",
  props: {
    mediaFormat: String,
    mediaPath: String,
    mediaType: String,
    mediaCaption: String,
    mediaDate: String
  },
  methods: {}
};
</script>

<style scoped>
img,
video {
  max-height: 80vh;
}

.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: flex;
  vertical-align: middle;
}

.modal-container {
  height: 80vh;
  margin: 20px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
  overflow: scroll;
  flex: 0.5;
}

.modal-header h3 {
  margin-top: 0;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
}
</style>
