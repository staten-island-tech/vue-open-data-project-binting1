<template>
  <div>
    <canvas ref="pieChartCanvas"></canvas>
  </div>
</template>

<script setup>
import { ref, onMounted, defineProps } from "vue";
import Chart from "chart.js/auto";

const props = defineProps({
  chartData: Object,
});

const pieChartCanvas = ref(null);

onMounted(() => {
  if (pieChartCanvas.value) {
    new Chart(pieChartCanvas.value, {
      type: "pie",
      data: {
        labels: props.chartData.labels,
        datasets: [
          {
            label: "Avg Contract Value",
            data: props.chartData.dataValues,
            backgroundColor: ["red", "blue", "green", "yellow"],
          },
        ],
      },
    });
  }
});
</script>

<style scoped>
</style>
