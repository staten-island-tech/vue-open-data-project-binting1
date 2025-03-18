<template>
  <router-link :to="busiPath">
      <h2 class="card">{{  business.vendor_formal_name }}</h2>
  </router-link>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  business: Object, 
  vendor_formal_name: String,
});

const busiPath = computed (() => {
  return `/business/${props.vendor_formal_name}`;
})
</script>

<style scoped>
.card {
  width: 50%;
  margin: 10px auto;
  padding: 10px;
  display: flex;
  background-color: #f7bcbc;
}

</style>