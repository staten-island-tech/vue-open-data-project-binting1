<template>
  <div>
    <h1>NYC Contracts Data (Pie Chart)</h1>
    <PieChart v-if="chartData" :chartData="chartData" />
    <p v-else>Loading data...</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import PieChart from "@/components/PieChart.vue"; 

const chartData = ref(null);

async function fetchData() {
  try {
    const response = await fetch("https://data.cityofnewyork.us/resource/ci93-uc8s.json");
    const data = await response.json();

    const categories = ["ASIAN", "HISPANIC", "BLACK", "NON-MINORITY"];
    const groupedData = categories.map((ethnicity) => {
      const filtered = data.filter((item) => item.ethnicity === ethnicity);
      const avgValue =
        filtered.reduce((sum, item) => sum + parseFloat(item.contract_value), 0) /
        (filtered.length || 1);
      return avgValue.toFixed(2);
    });

    chartData.value = {
      labels: categories,
      dataValues: groupedData,
    };
  } catch (error) {
    console.error("Error fetching data:", error);
  }
}

onMounted(fetchData);
</script>

<style scoped>
</style>
