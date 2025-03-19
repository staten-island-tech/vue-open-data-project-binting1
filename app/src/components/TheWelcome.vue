<template>
  <router-link :to="busiPath">
      <h2 class="card">{{  business.vendor_formal_name }}</h2>
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
.card {
  width: 50%;
  margin: 10px auto;
  padding: 10px;
  display: flex;
  background-color: #f7bcbc;
}

</style>