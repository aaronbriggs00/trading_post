<template>
  <div class="home">
    <bar-chart :chartData="barChartData" :options="barChartOptions"></bar-chart>
  </div>
</template>

<script>
import BarChart from "./../components/BarChart.js";

export default {
  components: {
    BarChart,
  },
  data() {
    return {
      barChartData: {
        datasets: [
          {
            label: "test data",
            backgroundColor: "#0000FF",
            barPercentage: 0.5,
            barThickness: 6,
            maxBarThickness: 8,
            minBarLength: 2,
            data: [10, 20, 30, 40, 50, 60],
          },
        ],
      },
      barChartOptions: {
        responsive: true,
        maintainAspectRatio: false,
      },
    };
  },
  mounted() {},
  methods: {},
};
</script>

<style>
.small {
  max-width: 600px;
  margin: 150px auto;
}
</style>
