<template>
  <div class="reviews">
    <h1 class="header">Reviews</h1>
    <hr>
    <ReviewItem v-for="(review, index) in reviews" :key="index"
      :review="review"/>
  </div>
</template>

<script>
import ReviewItem from './ReviewItem';

export default {
  name: 'ReviewList',
  data: function() {
    return {
    };
  },
  components: {
    ReviewItem
  },
  props: {
    reviews: Array
  }
};
</script>

<style lang="scss" scoped>
.header {
  margin: 0;
}
</style>
