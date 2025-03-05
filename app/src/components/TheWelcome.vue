<template>
  <router-link :to="busiPath" card="card">
      <h2>{{  business.account_number }}</h2>
  </router-link>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  business: Object, 
});

const busiPath = computed (() => {
  return "https://data.cityofnewyork.us/resource/ci93-uc8s.json";
})
</script>

<style scoped>

</style>