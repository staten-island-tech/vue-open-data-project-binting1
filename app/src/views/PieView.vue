<template>
    <div>
        <h1>Ethnicity Group Distribution in Brooklyn</h1>
        <div style="width: 50vw; height: 50vw;"><canvas id="small"></canvas></div>
    </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import Chart from "chart.js/auto"; 

const yum = ref([]);

async function getData() {
  let res = await fetch("https://data.cityofnewyork.us/resource/ci93-uc8s.json?$limit=50");
  let data = await res.json();
  yum.value = data;
}

onMounted (async () => {
    await getData(); 

    const bkBusinesses = yum.value.filter(row=>row.city === "Brooklyn");
    const ethnicityCount = bkBusinesses.reduce((acc, row) => {
        if(row.ethnicity) {
            const ethnicity = row.ethnicity.trim();
            acc[ethnicity]=(acc[ethnicity] || 0) +1;
        }
        return acc;
    }, {});

    console.log("Ethnicity Count:", ethnicityCount);

    const ethnicityLabels = Object.keys(ethnicityCount);
    const ethnicityPercentages = Object.values(ethnicityCount).map(count => (count / Object.values(ethnicityCount).reduce((a, b) => a + b, 0)) * 100);

    new Chart (
        document.getElementById('small'),
        {
            type:'pie',
            data: {
                labels: ethnicityLabels,
                datasets: [{
                    data: ethnicityPercentages,
                    backgroundColor:['#FF6384', '#36A2EB', '#FFCE56', '#4BC0C0', '#FF9F40'],
                }]
                
            }, 
            options: {
                plugins: {
                    title: {
                        display: true,
                        text:'Brooklyn SBS Distribution by Ethnicity Groups'
                    }
                }
            }
        }
    )
}) 

</script>

<style scoped>
h1 {
  color: #88c588;
}
</style>