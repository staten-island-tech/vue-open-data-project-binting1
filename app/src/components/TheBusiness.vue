<template>
<div class="container">
  <router-link :to="busiPath">
      <h2 class="text">{{  business.vendor_formal_name }}</h2>
  </router-link>
</div>
  
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  business: Object, 
  account_number: Number,
});

const busiPath = computed (() => {
  return `/business/${props.business.account_number}`;
})
</script>

<style scoped>
.text {
  display: flex;
  text-align: center;
}

.container {
  align-items: center;
  height: 100px;
  max-width: 300px;
  margin: 5px auto;
  padding: 10px;
  background-color: #4c554c;

}

</style>