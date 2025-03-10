<template>
    <div>

    </div>
</template>

<script setup>
async function getBusiness () {
  try {
  let res = await fetch("https://data.cityofnewyork.us/resource/ci93-uc8s.json");
  let data = await res.json ();
  businesses.value = data;
  console.log("Fetched data:", data);
  } catch (error) {
  console.error("Error fetching data:", error);
  }
}

</script>

<style scoped>

</style>