<template>
  <router-link :to="busiPath" card="card">
      <h2>{{  business.first_name }}</h2>
      <h3>{{  account_number }}</h3>
  </router-link>
</template>

<script setup>
import { computed } from 'vue';
const props = defineProps({
  business: Object, 
  account_number: Number,
});

const busiPath = computed (() => {
  return `/business/${props.account_number}`;
})
</script>

<style scoped>

</style>