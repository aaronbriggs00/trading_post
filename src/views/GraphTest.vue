<template>
  <div class="graph-test">
    <doughnut-chart
      :chartData="doughnutChartData"
      :options="doughnutChartOptions"
    ></doughnut-chart>
  </div>
</template>

<script>
import DoughnutChart from "./../components/DoughnutChart.js";

export default {
  components: {
    DoughnutChart,
  },
  data() {
    return {
      doughnutChartData: {
        datasets: [
          {
            data: [10, 20, 30],
            backgroundColor: [
              "rgb(255, 102, 102)",
              "rgb(255, 102, 102)",
              "rgb(255, 102, 102)",
            ],
            borderColor: [
              "rgb(255, 102, 102)",
              "rgb(255, 102, 102)",
              "rgb(255, 102, 102)",
            ],
          },
        ],
        labels: ["red", "yellow", "blue"],
      },
      doughnutChartOptions: {},
    };
  },
  methods: {},
};
</script>

<style>
.small {
  max-width: 600px;
  margin: 150px auto;
}
</style>
