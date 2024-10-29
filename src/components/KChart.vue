<template>
  <div ref="chartRef" class="chart-container"></div>
</template>

<script setup>
import * as echarts from 'echarts';
import {onBeforeUnmount, onMounted, ref} from "vue";

// 内部样例数据
const kLineData = [
  { date: '2021-01-01', open: 100, close: 105, high: 110, low: 95 },
  { date: '2021-01-02', open: 105, close: 102, high: 108, low: 100 },
  { date: '2021-01-03', open: 102, close: 108, high: 112, low: 98 },
  { date: '2021-01-04', open: 108, close: 106, high: 110, low: 100 },
  { date: '2021-01-05', open: 106, close: 110, high: 115, low: 102 },
  { date: '2021-01-06', open: 110, close: 109, high: 112, low: 105 },
  { date: '2021-01-07', open: 109, close: 115, high: 120, low: 105 },
  { date: '2021-01-08', open: 115, close: 113, high: 120, low: 110 },
  { date: '2021-01-09', open: 113, close: 118, high: 122, low: 110 },
  { date: '2021-01-10', open: 118, close: 120, high: 125, low: 115 },
];

const chartRef = ref(null);
let chartInstance = null;

const initChart = () => {
  chartInstance = echarts.init(chartRef.value);

  const option = {
    title: {
      text: 'K线图'
    },
    tooltip: {
      trigger: 'axis',
      axisPointer: {
        type: 'cross'
      }
    },
    xAxis: {
      type: 'category',
      data: kLineData.map(item => item.date),
      boundaryGap: false
    },
    yAxis: {
      type: 'value',
      scale: true,
      splitArea: {
        show: true
      }
    },
    series: [
      {
        name: 'K线图',
        type: 'candlestick',
        data: kLineData.map(item => [item.date, item.open, item.close, item.low, item.high]),
        itemStyle: {
          color: '#ec0000', // 上涨颜色
          color0: '#00da3c', // 下跌颜色
          borderColor: '#ec0000',
          borderColor0: '#00da3c'
        }
      }
    ]
  };

  chartInstance.setOption(option);
};

onMounted(() => {
  initChart();
});

onBeforeUnmount(() => {
  if (chartInstance) {
    chartInstance.dispose();
  }
});
</script>

<style scoped>
.chart-container {
  width: 100%;
  height: 400px;
}
</style>