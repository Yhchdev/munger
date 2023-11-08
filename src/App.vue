<template>
  <div>
    <button @click="fetchData">点击获取数据</button>
    <div class="chart" id="chart"></div>
  </div>
</template>

<script>
import * as echarts from "echarts";
import axios from "axios";

export default {
  data() {
    return {
      chartData: null, // 用于存储获取到的数据
    };
  },
  methods: {
    fetchData() {
      axios
        .get("https://service-69d57xe6-1256238121.gz.apigw.tencentcs.com/release/data") // 替换为您的API端点
        .then((response) => {
          this.chartData = response.data; // 将获取到的数据存储到chartData中
          this.renderChart(); // 数据获取成功后调用渲染图表的方法
        })
        .catch((error) => {
          console.error("Error:", error);
        });
    },
    renderChart() {
      // 使用Echarts渲染图表
      const chart = echarts.init(document.getElementById("chart")); // 替换为您的图表容器ID

      console.log(this.chartData.charts[0])
      // 使用this.chartData填充图表数据
      let option = {
        xAxis: {
          type: "category",
          data: this.chartData.charts[0][0].x,
        },
        yAxis: {
          type: "value",
        },
        series: [
          {
            data: this.chartData.charts[0][0].y,
            type: "bar",
            showBackground: true,
            backgroundStyle: {
              color: "rgba(180, 180, 180, 0.2)",
            },
          },
          {
            data: this.chartData.charts[0][1].y,
            type: "line",
          },
        ],
      };
      chart.setOption(option);
    },
  },
};
</script>

<style>
.chart {
  width: 60%;
  height: 600px;
}
</style>
