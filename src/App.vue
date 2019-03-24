<template>
  <div id="app">
    <InternetArchiveVideo v-bind:query="query"/>
  </div>
</template>

<script>
import InternetArchiveVideo from './components/InternetArchiveVideo.vue';

export default {
  name: 'app',
  components: {
    InternetArchiveVideo
  },
  data: function() {
    return {
    };
  },
  computed: {
    query: function() {
      const pathname = window.location.pathname.slice(1);
      const defaultQuery = 'InformationM';

      return pathname || defaultQuery;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 60px;
}
</style>
