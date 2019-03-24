<template>
  <div class="container">
    <video v-bind:src="video.source"
           type="videoType"
           v-bind:poster="video.thumbnail"
           controls>
    </video>
    <h1>{{ video.title }}</h1>
    <p>{{ video.description }}</p>
  </div>
</template>

<script>
export default {
  name: 'Video',
  data: function() {
    return {
    };
  },
  computed: {
    videoType: function() {
      const { video } = this;
      const extension = video.source.match(/\w+$/)[0];

      return `video/${extension}`;
    }
  },
  props: {
    video: {
      type: Object,
      required: true
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  text-align: center;
}
</style>
