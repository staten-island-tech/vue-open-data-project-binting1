<template>
    <div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute} from 'vue-router';

const route = useRoute();
const small = ref('');

async function getSmall () {
  try {
  let res = await fetch(`https://data.cityofnewyork.us/resource/ci93-uc8s.json?vendor_formal_name=${route.params.vendor_formal_name}`);
  let data = await res.json ();
  small.value = data;
  console.log("Fetched data:", data);
  } catch (error) {
  console.error("Error fetching data:", error);
  }
}

onMounted (() => {
  getSmall();
});
</script>

<style scoped>

</style>