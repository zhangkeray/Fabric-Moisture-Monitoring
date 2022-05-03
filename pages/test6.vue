<template>
  <div class="fluid mt-5">
    <!-- <ul id="controls">
      <li class="to-end">已選項目</li>
      <li class="to-middle">比較</li>
      <li class="to-start">比對項目</li>
    </ul>

    <div id="before-after">
      <div class="view view-after">
        <img src="mockImg/0-200x100.png" />
      </div>
      <div class="view view-before">
        <img src="mockImg/5-200x100.png" />
      </div>
      <div id="dragme"></div>
    </div> -->

    <!-- <h1>沾濕面積</h1> -->
    <v-row>
      <v-col cols="3">
        <v-row>
          <v-col cols="6">
            <div class="container">
              <div>
                <div>0分鐘沾濕面積: 100%</div>
                <div class="img-left"></div>
              </div>

              <div>
                <div style="position: absolute; right: 541px; top: 0px">
                  10分鐘沾濕面積: 46%
                </div>
                <div style="position: absolute; right: 300px; top: 250px">
                  <h1>面積差值: 54%</h1>
                </div>

                <div class="img-right"></div>
              </div>
            </div>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </div>
</template>

<script>
// echarts引入
import DonutChart1 from "../components/index/DonutChart/DonutChart1.vue";
import RealTimeLineChart from "../components/index/RealTimeChart/RealTimeLineChart.vue";

export default {
  // echarts引入
  components: {
    DonutChart1,
    RealTimeLineChart,
  },
  name: "test3",
  head: {
    title: "即時監控",
    link: [
      // { rel: "icon", type: "image/x-icon", href: "/favicon.ico" },
      { rel: "stylesheet", href: "css/jquery-ui.css" },
      { rel: "stylesheet", href: "css/object.css" },
      { rel: "stylesheet", href: "css/card3.css" },
      { rel: "stylesheet", href: "css/details.css" },
    ],
    script: [
      {
        src: "/js/jquery.js",
        type: "text/javascript",
      },
      {
        src: "/js/jquery-ui.js",
        type: "text/javascript",
      },
      {
        src: "/js/jquery-collision.js",
        type: "text/javascript",
      },
      {
        src: "https://cdnjs.cloudflare.com/ajax/libs/gsap/latest/TweenMax.min.js",
        type: "text/javascript",
      },
      {
        src: "https://cdnjs.cloudflare.com/ajax/libs/gsap/latest/utils/Draggable.min.js",
        type: "text/javascript",
      },
      // {
      //   src: '/js/object.js',
      //   type: 'text/javascript',
      // },
    ],
  },
  data() {
    return {
      //left btn
      // 切換按鈕
      isActive: false,
      // 左側隱藏按鈕動作設定
      direction_imageMode: "right",
      fab_imageMode: false,
      transition_imageMode: "scale-transition",

      direction_palette: "right",
      fab_palette: false,
      transition_palette: "scale-transition",

      direction_calibration: "right",
      fab_calibration: false,
      transition_calibration: "scale-transition",

      direction_light: "right",
      fab_light: false,
      transition_light: "scale-transition",

      direction_autofocus: "right",
      fab_autofocus: false,
      transition_autofocus: "scale-transition",

      // 右1點線面_宣告變數陣列
      spots: [],
      scopes: [],
      lines: [],

      // realtime btn
      isTransform: false,
      //
      right: null,
      slickOptions: {
        arrows: false,
        slidesToShow: 3,
        slidesToScroll: 3,
        // centerMode: true,
        // dots: true,
        vertical: true,
        verticalSwiping: true,
        focusOnSelect: true,
      },
      temperature: [
        {
          mins: "0",
          temp: 21.9,
        },
        {
          mins: "1",
          temp: 23.6,
        },
        {
          mins: "2",
          temp: 25.1,
        },
        {
          mins: "3",
          temp: 26.5,
        },
        {
          mins: "4",
          temp: "28.0",
        },
        {
          mins: "5",
          temp: "29.0",
        },
        {
          mins: "6",
          temp: 29.7,
        },
        {
          mins: "7",
          temp: 30.1,
        },
        {
          mins: "8",
          temp: 30.3,
        },
        {
          mins: "9",
          temp: 30.5,
        },
        {
          mins: "10",
          temp: 21.7,
        },
        {
          mins: "11",
          temp: 30.9,
        },
        {
          mins: "12",
          temp: 31.1,
        },
        {
          mins: "13",
          temp: 31.3,
        },
        {
          mins: "14",
          temp: 31.4,
        },
        {
          mins: "15",
          temp: 31.4,
        },
        {
          mins: "16",
          temp: 31.5,
        },
        {
          mins: "17",
          temp: 31.5,
        },
        {
          mins: "18",
          temp: 31.6,
        },
        {
          mins: "19",
          temp: 31.6,
        },
        {
          mins: "20",
          temp: 31.7,
        },
      ],
    };
  },
  mounted() {
    $(function () {
      /*
    Dependencies : TweenMax and Draggable
    Images by Ivaylo Yovchev ( http://www.ivayloyovchev.com/ )
    
    Test on touch device @ http://cloud.bassta.bg/before-after.html
  */

      var $dragMe = $("#dragme");
      var $beforeAfter = $("#before-after");
      var $viewAfter = $(".view-after");

      Draggable.create($dragMe, {
        type: "left",
        bounds: $beforeAfter,
        onDrag: updateImages,
      });

      function updateImages() {
        TweenLite.set($viewAfter, { width: $dragMe.css("left") }); //or this.x if only dragging
      }

      //Intro Animation
      animateTo(350);

      //Externall nav
      $(".to-start").on("click", function () {
        animateTo(0);
      });

      $(".to-middle").on("click", function () {
        animateTo(298);
      });

      $(".to-end").on("click", function () {
        animateTo(598);
      });

      function animateTo(_left) {
        TweenLite.to($dragMe, 1, { left: _left, onUpdate: updateImages });
      }

      //V2 Click added
      $beforeAfter.on("click", function (event) {
        var eventLeft = event.clientX - $beforeAfter.offset().left;
        animateTo(eventLeft);
      });
    }); //end jQuery wrapper
  },
};
</script>
<style scoped>
body,
div,
p {
  margin: 0;
  padding: 0;
  font-family: Helvetica, sans-serif;
}

#before-after {
  position: relative;
  width: 600px;
  height: 500px;
  border: 2px solid grey;
  margin: 50px auto 0px;
}

.view {
  position: absolute;
  top: 0px;
  left: 0px;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.view-before {
  z-index: 100;
}

.view-after {
  z-index: 200;
}

#dragme {
  position: absolute;
  width: 5px;
  height: 100%;
  top: 0px;
  left: 0px;
  background-color: black;
  cursor: pointer;
  z-index: 300;
}

/*
				Controls
			*/

ul {
  text-align: center;
  margin-top: 50px;
}

ul li {
  list-style: none;
  display: inline-block;
  font-size: 17px;
  cursor: pointer;
  margin: 0px 20px 0px 20px;
}
</style>
<style lang="scss" scoped>
@import url(https://fonts.googleapis.com/css?family=Open+Sans);

body {
  text-align: center;
  font-family: "Open Sans";

  p {
    max-width: 36em;
    margin: 1em auto;
  }
}

// $img-width: 340px;
$img-width: 300px;

%image {
  // background-image: url("http://nick.mtvnimages.com/nick/flipbooks/breadwinners/spot-the-difference/breadwinners-spot-the-difference-image02Q.jpg?quality=0.75");
  background-image: url("/mockImg/5-200x100.png");

  transition-duration: 0.5s;
  background-size: 300px;
  width: $img-width;
  height: 300px;
  display: block;
  float: left;
}

.container {
  position: relative;
  width: $img-width * 2;
  margin: 0 auto;

  &:hover {
    .img-right {
      left: 0;
      mix-blend-mode: difference;
    }
  }
}

.img-left {
  background-image: url("/mockImg/1-200x100.png");
  transition-duration: 0.5s;

  background-size: 300px;
  width: $img-width;
  height: 300px;
  display: block;
  float: left;
}
.img-right {
  @extend %image;
}

.img-right {
  // background-position: 100% 0;
  position: absolute;
  left: $img-width + 5px;
}
</style>
