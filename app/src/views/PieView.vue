<template>
  <div style="width: 70vw; height:70vw;"><canvas id="business"></canvas>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import Chart from "chart.js/auto"; 

const chartData = ref("");

async function getData() {
  let res = await fetch("https://data.cityofnewyork.us/resource/ci93-uc8s.json?limit=50");
  let data = await res.json();
  chartData.value = data;
}

onMounted(async () => {
  await getData();
  new Chart(
    document.getElementById('business'),
    {
      type:'bar',
      data: {
        labels:business.value.map(row=>row.ethnicity),
        datasets: [
          {
            label:'Assets',
            data:business.value.map(row => row.largest_value_of_contract),
          }
        ]
      }, 
      options: {
        plugins: {
          title: {
            display:true,
            text:"Business assets"
          }
        }
      }
    }
  )
});
</script>

<style scoped>
</style>
