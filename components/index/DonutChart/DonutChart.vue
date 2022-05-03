<template>
  <div ref="donutChart1" style="height: 341px; width: 230px"></div>
</template>

<script>
import * as echarts from 'echarts'
export default {
  data() {
    return {}
  },
  mounted() {
    this.drawBar()
  },
  methods: {
    drawBar() {
      const chartDom = this.$refs.donutChart1
      const myChart = echarts.init(chartDom) // echarts初始化
      const colorPalette = ['#37484C', '#9aa2a4', '#d8dddd', '#E6E8E9']
      var option

      // 選擇圖表樣式------------------------------------------

      option = {
        tooltip: {
          trigger: 'item',
        },
        legend: {
          top: '10px',
          width: '100px',
          right: '0px',
          itemWidth: 10, // 图例的宽度
          itemHeight: 10, // 图例的高度
          textStyle: {
            // 图例文字的样式
            color: 'white',
            fontSize: 12,
          },
        },

        series: [
          {
            name: '',
            top: '0px',
            // bottom: '0px',
            right: "0px",
            avoidLabelOverlap: false,
            type: 'pie',
            radius: ['60%', '90%'],
            itemStyle: {
              borderRadius: 5,
              borderColor: ' #1d1d1d',
              borderWidth: 5,
            },

            color: colorPalette,

            label: {
              show: true,
              position: 'center',
              // formatter(d) {
              // return d.value;
              formatter: '{d}%',
              fontSize: '30',
              backgroundColor: ' #1d1d1d',
              color: 'white'

            },

            emphasis: {
              label: {
                show: true,
                fontSize: '30',
                // fontWeight: 'bold',
                backgroundColor: ' #1d1d1d',
                 borderColor: ' #1d1d1d',
                 borderWidth: 5,
                 color: 'white',
              },
            },
            labelLine: {
              show: true,
            },
            data: [
              { name: '濕面積', value: 2 },
              { name: '乾面積', value: 3 },
              // { name: '良好總筆數', value: 10 },
            ],
          },
        ],
      }

      // -------------------------------------------------------------

      option && myChart.setOption(option)
    },
  },
}
// let myChart = echarts.init(document.getElementById('charts'));
</script>

<style>
</style>
