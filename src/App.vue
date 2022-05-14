<template>
  <div id="app">
    <div class="cell cell-map">
      <OlMap />
    </div>
  </div>
</template>

<script lang="ts">
  import OlMap from './components/OlMap.vue';
  export default {
    name: 'App',
    components: {
      OlMap
    },
  }
</script>

<style>

</style>
