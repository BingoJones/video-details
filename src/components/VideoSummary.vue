<template>
  <div>
    <VideoDetails :metadata="metadata"/>
    <hr class="hr">
    <VideoTechnicalSpecs :metadata="metadata"/>
  </div>
</template>

<script>
import VideoDetails from './VideoDetails';
import VideoTechnicalSpecs from './VideoTechnicalSpecs';

export default {
  name: 'VideoSummary',
  components: {
    VideoDetails,
    VideoTechnicalSpecs
  },
  data: function() {
    return {
    };
  },
  props: {
    metadata: {
      type: Object,
      default: function() {
        return {};
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.hr {
  $gray: #E8E8E8;
  
  height: 1px;
  border: 0;
  border-top: 1px solid $gray;
}
</style>