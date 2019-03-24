<template>
  <div>
    <h1 class="header">Details</h1>
    <hr>
    <template v-for="(detail, index) in details">
      <div :key="index">
        <b>{{ detail.label }}: </b>
        <template v-if="detail.isUrl">
          <a :href="detail.value">{{ detail.value }}</a>
	</template>
	<template v-else>
          {{ detail.value }}
	</template>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  name: 'VideoDetails',
  data: function() {
    return {
    };
  },
  computed: {
    details: function() {
      const { metadata } = this;

      return {
        publicationDate: { value: metadata.date, label: 'Publication Date' },
	licenseUrl: { value: metadata.licenseurl, label: 'License', isUrl: true },
	topics: { value: metadata.subject, label: 'Topics' },
	publisher: { value: metadata.publisher, label: 'Publisher' },
	sponsor: { value: metadata.sponsor, label: 'Sponsor' }
      };
    }
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
.header {
  margin: 0;
}
</style>