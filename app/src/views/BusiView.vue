<template>
    <div class="container">
      <div v-for="business in business" :key="business.account_number" :business="business">
        <h2>{{ business.vendor_formal_name }}</h2>
        <h3>Owner: {{ business.first_name  }} {{ business.last_name }}</h3>
        <h3>Telephone: {{ business.telephone }}</h3>
        <h3>Address: {{business.address1}}, {{ business.city }}, {{ business.zip }}</h3>
        <br>
        <h3><I>{{ business.business_description}}</I></h3>
      </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute} from 'vue-router';

const route = useRoute();
const business = ref("");

async function getBusiness () {
  let res = await fetch(`https://data.cityofnewyork.us/resource/ci93-uc8s.json?$limit=50&account_number=${route.params.account_number}`);
  let data = await res.json ();
  business.value = data;
}

onMounted (() => {
  getBusiness();
});
</script>

<style scoped>
.container {
  background-color: #88c588;
  height: auto;
  padding: 20px;
}
</style>