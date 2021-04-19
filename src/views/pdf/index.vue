<template>
  <div id="print" ref="mainRef">
    <el-button @click="print">PDF</el-button>
    <div id="mainprint">
      <line-chart :chart-data="lineChartData" />
      <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; wwwwww</p>
      <line-chart :chart-data="lineChartData" />
      <PieChart :chart-data="lineChartData" />
      <PieChart :chart-data="lineChartData" />
      <line-chart :chart-data="lineChartData" />
      <line-chart :chart-data="lineChartData" />
      <line-chart :chart-data="lineChartData" />
      <line-chart :chart-data="lineChartData" />
      <line-chart :chart-data="lineChartData" />
    </div>
  </div>
</template>

<script>
import LineChart from "@/views/dashboard/admin/components/LineChart";
import PieChart from "@/views/dashboard/admin/components/PieChart";
import $ from "jquery";

const lineChartData = {
  newVisitis: {
    expectedData: [100, 120, 161, 134, 105, 160, 165],
    actualData: [120, 82, 91, 154, 162, 140, 145],
  },
  aa: [],
};
export default {
  components: { LineChart, PieChart },
  data() {
    return {
      lineChartData: lineChartData.newVisitis,
    };
  },
  methods: {
    print() {
      const mainCanvas = document.getElementsByTagName("canvas");
      const list = document.getElementsByClassName("chart");
      const cc = document.getElementById("mainprint");
      const arr = [];
      // 将 canvas 转为图片
      for (let i = 0; i < mainCanvas.length; i++) {
        let img = document.createElement("img");
        img.src = mainCanvas[i].toDataURL("image/png");
        arr.push(img);
      }
      for (let i = 0; i < arr.length; i++) {
        $(".chart")[0].replaceWith(arr[i]);
      }
      document.body.innerHTML = document.getElementById("print").innerHTML;    //自定义截图区域
      setTimeout(() => {
        window.print();
      }, 1000);
   // window.location.reload() // 或者刷新页面
    },
  },
};
</script>

