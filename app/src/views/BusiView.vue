<template>
    <div>
      <h2>{{ business.first_name }}</h2>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute} from 'vue-router';

const route = useRoute();
const business = ref("");

async function getBusiness () {
  let res = await fetch(`https://data.cityofnewyork.us/resource/ci93-uc8s.json?$limit=10?vendor_formal_name=${route.params.account_number}`);
  let data = await res.json ();
  business.value = data;
}

onMounted (() => {
  getBusiness();
});
</script>

<style scoped>

</style>