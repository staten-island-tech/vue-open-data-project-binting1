<template>
  <div>
    <TheWelcome v-for="bus in business" :key="bus.first_name"></TheWelcome>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import TheWelcome from '../components/TheWelcome.vue'

const business = ref('');
async function getBusiness () {
  let res = await fetch("https://data.cityofnewyork.us/resource/ci93-uc8s.json");
  let data = await res.json ();
  business.value = data;
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
  flex-wrap: wrap;
  flex-direction: row;
  align-items: center;
  justify-content: space-around;
}
</style>
