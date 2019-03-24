<template>
  <div class="review">
    <div><b>Review: </b><a :href="reviewer.accountLink">{{ reviewer.name }}</a> - <span class="stars">{{ rating }}</span> - {{ date }}</div>
    <div><b>Subject: </b>{{ review.title }}</div>
    <p>{{ review.body }}</p>
  </div>
</template>

<script>
export default {
  name: 'ReviewItem',
  data: function() {
    return {
    };
  },
  computed: {
    rating: function() {
      const numStars = +this.review.stars;
      const star = "★";
      const rating = star.repeat(numStars);

      return rating;
    },
    date: function() {
      const { review } = this;
      const date = new Date(review.date);
      
      // Converts '2003-09-15 15:54:20' to 'September 9, 2003'
      const locale = 'en-us';
      const dateFormat = {
        month: 'long',
	day: 'numeric',
	year: 'numeric'
      };

      const formattedDate = new Intl.DateTimeFormat(locale, dateFormat).format(date);

      return formattedDate;
    },
    reviewer: function() {
      const { review } = this;
      const name = review.reviewer;

      // Account names can't have whitespaces
      // Converts 'Some One Here' to 'SomeOneHere'
      const encodedName = name.replace(/\s/g, '_');
      const accountLink = `https://archive.org/details/@${encodedName}`;

      return {
        name,
	accountLink
      };
    }
  },
  props: {
    review: {
      type: Object,
      required: true
    }
  }
};
</script>

<style lang="scss" scoped>
.stars {
  color: gold;
}
</style>
