<template>
  <div class="card" v-for="bus in business" :key="bus.first_name">
    <h2>{{  bus.name }}</h2>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
const business = ref("");
async function getBusiness() {
  let res = await fetch("https://data.cityofnewyork.us/resource/ci93-uc8s.json");
  let data  = await res.json(); 
  business.value = data.resource;
}

onMounted(() => {
  getBusiness();
});

</script>

<style scoped>

</style>