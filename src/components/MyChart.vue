<template>
  <div ref="chart" style="width: 600px; height: 400px;"></div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  name: 'MyChart',
  mounted() {
    this.initChart();
  },
  methods: {
    initChart() {
      const chart = echarts.init(this.$refs.chart);
      chart.setOption({
        title: { text: '示例图表' },
        tooltip: {},
        xAxis: {
          data: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子']
        },
        yAxis: {},
        series: [{
          name: '销量',
          type: 'bar',
          data: [5, 20, 36, 10, 10, 20]
        }]
      });
    }
  }
};
</script>