<template>
  <div>
    <h1 class="hr">Technical Specs</h1>
    <template v-for="(spec, index) in technicalSpecs">
      <div :key="index"><b>{{ spec.label }}: </b>{{ spec.value }}</div>
    </template>
  </div>
</template>

<script>
export default {
  name: 'VideoTechnicalSpecs',
  data: function() {
    return {
    };
  },
  computed: {
    technicalSpecs: function() {
      const { metadata } = this;

      return {
        closedCaptioning: { value: metadata.closed_captioning, label: 'Closed Captioning' },
	collectionId: { value: metadata.collectionid, label: 'Collection ID' },
	color: { value: metadata.color, label: 'Color' },
	identifier: { value: metadata.identifier, label: 'Identifier' },
	numericId: { value: metadata.numeric_id, label: 'Numeric ID' },
	productionDate: { value: metadata.proddate, label: 'Production Date' },
	runTime: { value: metadata.runtime, label: 'Runtime' },
	sound: { value: metadata.sound, label: 'Sound' },
	type: { value: metadata.type, label: 'Type' }
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
.hr {
  margin-bottom: 0;
}
</style>