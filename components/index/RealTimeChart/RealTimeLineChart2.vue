<template>
  <div ref="donutChart1" style="height: 145px; width: 830px"></div>
</template>

<script>
import * as echarts from "echarts";
export default {
  data() {
    return {};
  },
  mounted() {
    this.drawBar();
  },

  methods: {
    drawBar() {
      const chartDom = this.$refs.donutChart1;
      const myChart = echarts.init(chartDom); // echarts初始化
      const colorPalette = ["#37484C", "#9aa2a4", "#d8dddd", "#E6E8E9"];
      var option;

      // 選擇圖表樣式------------------------------------------

      var data = [];
      var time = [];
      // var starTime = 30 * 60 * 1000; // 这个是当前时间向前取值，我在这里设置的是半个小时
      var starTime = 0; // 这个是当前时间向前取值，我在这里设置的是0

      var times = new Date(); //X轴开始的时间，可以自行设置

      function initDate(value) {
        //时间格式化
        if (value < 9) {
          return "0" + value;
        } else {
          return value;
        }
      }




      option = {
        // title: {
        //     text: ''
        // },
        grid: {
          //   show: false,
          // top: '25',
          bottom: "30",
          left: "45",
          height: "70%",
        },
        tooltip: {
          trigger: "axis",
          formatter: function (params) {
            params = params[0];
            return params.name + ":" + params.value;
          },
          axisPointer: {
            animation: false,
          },
        },
        xAxis: {
          type: "category",
          splitLine: {
            show: false,
          },
          data: time,
        },
        yAxis: {
          type: "value",
          boundaryGap: [0, "100%"],
          splitLine: {
            show: false,
          },
        },
        series: [
          {
            name: "模拟数据",
            type: "line",
            showSymbol: false,
            hoverAnimation: false,
            data: data,
          },
        ],
      };
      var sum = 0;
      var Now = [];
      // 设置定时器
      setInterval(function () {
        // var now = new Date();
        //这里就是先删除第一个，然后把当前时间放上去，可以根据需求进行改变
        // time.shift()
        // time.push(initDate(now.getMonth() + 1) + '/' + initDate(now.getDate()) + ' ' + initDate(now.getHours()) + ':' + initDate( now.getMinutes() )  )
        // time.push(initDate(now.getMinutes()));
        var test = getDuration(sum)
        Now.push(test);
        // data.shift()
        data.push(Math.round(Math.random() * 30 + 10));
        //最后就是重新绘制echarts
        myChart.setOption({
          series: {
            data: data,
          },
          xAxis: { data: Now },
        });
        sum++;
      }, 1000);

      // -------------------------------------------------------------
      // 秒 轉 分、時、天，並且隱藏時間未到的單位

      option && myChart.setOption(option);
      
      function getDuration(second) {
        var days = Math.floor(second / 86400);
        var hours = Math.floor((second % 86400) / 3600);
        var minutes = Math.floor(((second % 86400) % 3600) / 60);
        var seconds = Math.floor(((second % 86400) % 3600) % 60);
        if (second < 60) {
          var duration = seconds + "秒";
        } else if (second >= 60 && second < 3600) {
          var duration = minutes + "分" + seconds + "秒";
        } else if (second >= 3600 && second < 86400) {
          var duration = hours + "時<br />" + minutes + "分" + seconds + "秒";
        } else if (second >= 86400) {
          var duration =
            days + "天" + hours + "時<br />" + minutes + "分" + seconds + "秒";
        }
        return duration;
      }
      // 秒 轉 分、時、天，並且隱藏時間未到的單位
    },
  },
};
// let myChart = echarts.init(document.getElementById('charts'));
</script>

<style>
#specialLook {
  pointer-events: all;

  border: 0;
  background-color: #37484c;
  color: #fff;
  border-radius: 10px;
  cursor: pointer;
}

#specialLook:hover {
  color: #37484c;
  background-color: #fff;
  border: 2px #37484c solid;
}
</style>
