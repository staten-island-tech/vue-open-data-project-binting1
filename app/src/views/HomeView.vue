<template>
  <div class="container">
    <TheBusiness 
    v-for="business in businesses" 
    :key="business.vendor_formal_name" 
    :business="business"
    ></TheBusiness>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import TheBusiness from '../components/TheBusiness.vue'

const businesses = ref("");

async function getBusiness () {
  let res = await fetch("https://data.cityofnewyork.us/resource/ci93-uc8s.json?$limit=50");
  let data = await res.json ();
  businesses.value = data;
}

onMounted (() => {
  getBusiness();
});

</script>

<style scoped>
.container {
  width: 700px;
  margin: 20px auto;
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  align-items: center;
  justify-content: space-around;
}
</style>
