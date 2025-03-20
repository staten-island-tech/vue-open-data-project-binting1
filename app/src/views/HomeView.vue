<template>
  <div>
    <TheWelcome 
    v-for="business in businesses" 
    :key="business.vendor_formal_name" 
    :business="business"
    ></TheWelcome>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import TheWelcome from '../components/TheBusiness.vue'

const businesses = ref("");

async function getBusiness () {
  let res = await fetch("https://data.cityofnewyork.us/resource/ci93-uc8s.json?$limit=10");
  let data = await res.json ();
  businesses.value = data;
}

onMounted (() => {
  getBusiness();
});

</script>

<style scoped>
.container {
  width: 80vw;
  margin: 30px auto;
  display: flex;
  color: black;
  flex-wrap: wrap;
  flex-direction: row;
  align-items: center;
  justify-content: space-around;
}
</style>
