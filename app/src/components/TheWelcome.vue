<template>
  <router-link :to="busiPath" card="card">
      <h2>{{  business.vendor_formal_name }}</h2>
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
.card {
  width: 300px;
  margin: 20px auto;
  padding: 15px;
  background-color: #ffffff;
  border: 1px solid #ddd;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

</style>