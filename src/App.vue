<template>
  <div class="chart" ref="chart"></div>
</template>

<script setup>
import * as echarts from "echarts";
import { ref,onMounted } from "vue";

let chart = ref();

onMounted(() => {
  const myChart = echarts.init(chart.value);
  console.log(myChart)

  let option = {
    xAxis: {
      type: "category",
      data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
    },
    yAxis: {
      type: "value",
    },
    series: [
      {
        data: [120, 200, 150, 80, 70, 110, 130],
        type: "bar",
        showBackground: true,
        backgroundStyle: {
          color: "rgba(180, 180, 180, 0.2)",
        },
      },
    ],
  };

  myChart.setOption(option);
});
</script>

<style>
.chart {
  width: 100%;
  height: 600px;
}
</style>
