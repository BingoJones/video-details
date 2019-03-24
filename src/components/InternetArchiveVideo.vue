<template>
  <div>
    <template v-if="error">
      <p class="error">{{ error }}</p>
    </template>
    <template v-else>
      <Video class="video" :video="video"/>
      <div class="panel-container">
        <ReviewList class="panel" :reviews="reviews"/>
        <VideoSummary class="panel" :metadata="metadata"/>
      </div>
    </template>
  </div>
</template>

<script>
import axios from 'axios';

import Video from './Video.vue';
import VideoSummary from './VideoSummary.vue';
import ReviewList from './ReviewList.vue';

export default {
  name: 'InternetArchiveVideo',
  components: {
    Video,
    VideoSummary,
    ReviewList
  },
  data: function() {
    return {
      video: {},
      reviews: [],
      metadata: {},
      error: false
    };
  },
  props: {
    query: {
      type: String,
      required: true
    }
  },
  created: function() {
    this.fetchData();
  },
  methods: {
    fetchData: function() {
      const vm = this;
      const { query } = vm;
      const url = `https://archive.org/metadata/${query}`;

      axios.get(url)
        .then(function(response) {
          const { data } = response;
          const { metadata } = data;
          const { reviews = [] } = data;

          data.files = data.files || [];
          const video = data.files.find(file => /\.mp4$/.test(file.name));

          if (!video) {
            throw Error(`Could not find any mp4 video for "${query}"`);
          }

          vm.video = {
            title: metadata.title,
            description: metadata.description,
            source: `https://archive.org/download/${vm.query}/${video.name}`,
            thumbnail: `https://archive.org/services/img/${vm.query}`
          };

          vm.metadata = metadata;
          vm.reviews = reviews.map(review => ({
              date: review.reviewdate,
              body: review.reviewbody,
              reviewer: review.reviewer,
              title: review.reviewtitle,
              stars: review.stars
          }));
        })
        .catch(error => {
          this.error = error;
        });
    }
  }
};
</script>

<style lang="scss" scoped>
.panel-container {
  $padding: 10%;
  
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  column-gap: $padding;

  .panel {
    
    &:first-child {
      padding-left: $padding;
    }

    &:last-child {
      padding-right: $padding;
    }
  }      
}

.error {
  text-align: center;
  color: red;
}
</style>
