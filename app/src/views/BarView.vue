<template>
  <div>
    <h1>Average Highest Contract Value by Ethnicity</h1>
    <div style="width: 50vw; height: 50vw;"><canvas id="small"></canvas></div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import Chart from "chart.js/auto"; 

const yum = ref("");

async function getData() {
  let res = await fetch("https://data.cityofnewyork.us/resource/ci93-uc8s.json?$limit=100");
  let data = await res.json();
  yum.value = data;
}

onMounted(async () => {
  await getData();

  const specificEthnicity = yum.value.reduce((acc, row) => {
    if (row.ethnicity && row.largest_value_of_contract){
      const contractValue = Number(row.largest_value_of_contract);

      if(!isNaN(contractValue)) {
        if (!acc[row.ethnicity]) {
      acc[row.ethnicity] =[];
      }
      acc[row.ethnicity].push(contractValue);
    }

    } return acc;
    
  }, {});

  console.log("Grouped by Ethnicity:", specificEthnicity);


  const ethnicityLabels = [];
  const averageAssets = [];

  for(let ethnicity in specificEthnicity) {
    const contracts = specificEthnicity[ethnicity];
    const average = contracts.reduce((sum, value) => sum + value, 0) / contracts.length;
    ethnicityLabels.push(ethnicity);
    averageAssets.push(average);
  }

  new Chart(
    document.getElementById('small'),
    {
      type:'bar',
      data: {
        labels:ethnicityLabels,
        datasets: [
          {
            label:'Average Assets',
            data:averageAssets,
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
h1 {
  color: #88c588;
}
</style>
