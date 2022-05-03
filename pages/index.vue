<template>
  <div class="fluid mt-5">
    <div class="box">
      <v-card class="mt-6 drawer" elevation="10" color="#59595b">
        <v-sheet class="arrow" elevation="5" color="#59595b"></v-sheet>
        <!-- 監測工具monitoring tools-------------------------------------------------------------------------------- -->
        <p class="subtitle text-center"><br />監測<br />項目</p>
        <!-- 點spot -->
        <v-tooltip right class="tips">
          <template #activator="{ on, attrs }">
            <v-btn
              class="left-btn mx-3"
              elevation="6"
              icon
              v-bind="attrs"
              v-on="on"
              @click="spot()"
            >
              <img alt="spot" src="/left-icons/spot.png" width="20em" />
            </v-btn>
            <!-- <v-btn x-small icon class="btn reset" color="#9BA3A5">
                  <v-icon x-small class="icon">mdi-restore</v-icon>
                </v-btn> -->
          </template>
          <span>點</span>
        </v-tooltip>
        <!-- 線line -->
        <v-tooltip right class="tips">
          <template #activator="{ on, attrs }">
            <v-btn
              class="left-btn mx-3 mt-3"
              elevation="6"
              icon
              v-bind="attrs"
              v-on="on"
              @click="line()"
            >
              <img alt="line" src="/left-icons/line.png" width="15em" />
            </v-btn>
          </template>
          <span>直線</span>
        </v-tooltip>
        <!-- 矩形rectangle -->
        <v-tooltip right class="tips">
          <template #activator="{ on, attrs }">
            <v-btn
              class="left-btn mx-3 my-3"
              elevation="6"
              icon
              v-bind="attrs"
              v-on="on"
              @click="scope()"
            >
              <img
                alt="rectangle"
                src="/left-icons/rectangle.png"
                width="18em"
              />
            </v-btn>
          </template>
          <span>矩形</span>
        </v-tooltip>
        <v-divider></v-divider>
        <!-- 影像呈現image presentation------------------------------------------------------------------------------ -->
        <p class="subtitle text-center"><br />影像<br />呈現</p>
        <!-- 影像模式image mode -->
        <v-speed-dial
          :direction="direction_imageMode"
          :transition="transition_imageMode"
        >
          <template #activator>
            <v-tooltip right class="tips">
              <template #activator="{ on, attrs }">
                <v-btn
                  v-model="fab_imageMode"
                  elevation="6"
                  class="left-btn mx-3"
                  icon
                  v-bind="attrs"
                  v-on="on"
                >
                  <v-icon v-if="fab_imageMode"> mdi-close </v-icon>
                  <img
                    v-else
                    alt="palette"
                    src="/left-icons/image-mode/image-mode.png"
                    width="21em"
                  />
                </v-btn>
              </template>
              <span>影像模式</span>
            </v-tooltip>
          </template>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class="mt-2"
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt="image-mode-thermal"
                  src="/left-icons/image-mode/image-mode-thermal.png"
                  width="22em"
                />
              </v-btn>
            </template>
            <span>Thermal</span>
          </v-tooltip>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class="mt-2"
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt="image-mode-thermal-msx"
                  src="/left-icons/image-mode/image-mode-thermal-msx.png"
                  width="22em"
                />
              </v-btn>
            </template>
            <span>Thermal MSX</span>
          </v-tooltip>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class="mt-2"
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt="image-mode-digital-camera"
                  src="/left-icons/image-mode/image-mode-digital-camera.png"
                  width="22em"
                />
              </v-btn>
            </template>
            <span>Digital Camera</span>
          </v-tooltip>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class="mt-2"
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt="image-mode-marco"
                  src="/left-icons/image-mode/image-mode-marco.png"
                  width="22em"
                />
              </v-btn>
            </template>
            <span>Marco</span>
          </v-tooltip>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class="mt-2"
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt="image-mode-thermal-fsx"
                  src="/left-icons/image-mode/image-mode-thermal-fsx.png"
                  width="22em"
                />
              </v-btn>
            </template>
            <span>Thermal FSX</span>
          </v-tooltip>
        </v-speed-dial>
        <!-- 色譜模式palette -->
        <v-speed-dial
          :direction="direction_palette"
          :transition="transition_palette"
        >
          <template #activator>
            <v-tooltip right class="tips">
              <template #activator="{ on, attrs }">
                <v-btn
                  v-model="fab_palette"
                  class="left-btn mx-3 my-3"
                  elevation="6"
                  icon
                  v-bind="attrs"
                  v-on="on"
                >
                  <v-icon v-if="fab_palette"> mdi-close </v-icon>
                  <img
                    v-else
                    alt="palette"
                    src="/left-icons/palette/palette.png"
                    width="18em"
                  />
                </v-btn>
              </template>
              <span>色譜模式</span>
            </v-tooltip>
          </template>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class=""
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt="palette-iron"
                  src="/left-icons/palette/palette-iron.png"
                  width="24em"
                />
              </v-btn>
            </template>
            <span>Iron</span>
          </v-tooltip>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class=""
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt="palette-lava"
                  src="/left-icons/palette/palette-lava.png"
                  width="24em"
                />
              </v-btn>
            </template>
            <span>Lava</span>
          </v-tooltip>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class=""
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt="palette-gray"
                  src="/left-icons/palette/palette-gray.png"
                  width="24em"
                />
              </v-btn>
            </template>
            <span>Gray</span>
          </v-tooltip>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class=""
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt="palette-rainbow"
                  src="/left-icons/palette/palette-rainbow.png"
                  width="24em"
                />
              </v-btn>
            </template>
            <span>Rainbow</span>
          </v-tooltip>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class=""
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt="palette-rainbow-hc"
                  src="/left-icons/palette/palette-rainbow-hc.png"
                  width="24em"
                />
              </v-btn>
            </template>
            <span>Rainbow HC</span>
          </v-tooltip>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class=""
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt="palette-arctic"
                  src="/left-icons/palette/palette-arctic.png"
                  width="20em"
                />
              </v-btn>
            </template>
            <span>Arctic</span>
          </v-tooltip>
        </v-speed-dial>
        <v-divider></v-divider>

        <!-- 計算工具calibration tools------------------------------------------------------------------------------ -->
        <p class="subtitle text-center"><br />校正<br />工具</p>

        <!-- 計算calibration -->
        <v-speed-dial
          :direction="direction_calibration"
          :transition="transition_calibration"
        >
          <template #activator>
            <v-tooltip right class="tips">
              <template #activator="{ on, attrs }">
                <v-btn
                  v-model="fab_calibration"
                  class="left-btn mx-3"
                  elevation="6"
                  icon
                  v-bind="attrs"
                  v-on="on"
                >
                  <v-icon v-if="fab_calibration"> mdi-close </v-icon>
                  <img
                    v-else
                    alt="palette"
                    src="/left-icons/calibration/calibration.png"
                    width="16em"
                  />
                </v-btn>
              </template>
              <span>校正</span>
            </v-tooltip>
          </template>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class="mt-2"
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt=""
                  src="/left-icons/calibration/calibration-now.png"
                  width="23em"
                />
              </v-btn>
            </template>
            <span>立即校正</span>
          </v-tooltip>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class="mt-2"
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt=""
                  src="/left-icons/calibration/calibration-auto.png"
                  width="20em"
                />
              </v-btn>
            </template>
            <span>自動校正</span>
          </v-tooltip>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class="mt-2"
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt=""
                  src="/left-icons/calibration/calibration-10min.png"
                  width="20em"
                />
              </v-btn>
            </template>
            <span>每10分鐘</span>
          </v-tooltip>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class="mt-2"
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt=""
                  src="/left-icons/calibration/calibration-30min.png"
                  width="20em"
                />
              </v-btn>
            </template>
            <span>每30分鐘</span>
          </v-tooltip>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class="mt-2"
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt=""
                  src="/left-icons/calibration/calibration-60min.png"
                  width="20em"
                />
              </v-btn>
            </template>
            <span>每60分鐘</span>
          </v-tooltip>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class="mt-2"
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt=""
                  src="/left-icons/calibration/calibration-manual.png"
                  width="20em"
                />
              </v-btn>
            </template>
            <span>手動校正</span>
          </v-tooltip>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class="mt-2"
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt=""
                  src="/left-icons/calibration/calibration-stop.png"
                  width="20em"
                />
              </v-btn>
            </template>
            <span>停止校正</span>
          </v-tooltip>
        </v-speed-dial>
        <!-- 照明light -->
        <v-speed-dial
          :direction="direction_light"
          :transition="transition_light"
        >
          <template #activator>
            <v-tooltip right class="tips">
              <template #activator="{ on, attrs }">
                <v-btn
                  v-model="fab_light"
                  class="left-btn mx-3 mt-3"
                  elevation="6"
                  icon
                  v-bind="attrs"
                  v-on="on"
                  @click="light"
                >
                  <v-icon v-if="fab_light"> mdi-close </v-icon>
                  <img
                    v-else
                    id="light_img"
                    alt="palette"
                    src="/left-icons/light/light-off.png"
                    width="14em"
                  />
                </v-btn>
              </template>
              <span>照明</span>
            </v-tooltip>
          </template>
        </v-speed-dial>
        <!-- 自動對焦autoFocus -->
        <v-speed-dial
          :direction="direction_autofocus"
          :transition="transition_autofocus"
        >
          <template #activator>
            <v-tooltip right class="tips">
              <template #activator="{ on, attrs }">
                <v-btn
                  v-model="fab_autofocus"
                  class="left-btn mx-3 my-3"
                  elevation="6"
                  icon
                  v-bind="attrs"
                  v-on="on"
                >
                  <v-icon v-if="fab_autofocus"> mdi-close </v-icon>
                  <img
                    v-else
                    alt="palette"
                    src="/left-icons/autofocus/autofocus.png"
                    width="16em"
                  />
                </v-btn>
              </template>
              <span>自動對焦</span>
            </v-tooltip>
          </template>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class=""
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt="palette-iron"
                  src="/left-icons/autofocus/autofocus-focus-further.png"
                  width="18em"
                />
              </v-btn>
            </template>
            <span>遠景</span>
          </v-tooltip>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class=""
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt="palette-lava"
                  src="/left-icons/autofocus/autofocus-focus-closer.png"
                  width="18em"
                />
              </v-btn>
            </template>
            <span>近景</span>
          </v-tooltip>
          <v-tooltip top class="tips">
            <template #activator="{ on, attrs }">
              <v-btn
                class=""
                elevation="6"
                x-small
                dark
                fab
                v-bind="attrs"
                v-on="on"
              >
                <img
                  alt="palette-gray"
                  src="/left-icons/autofocus/autofocus-autofocus.png"
                  width="18em"
                />
              </v-btn>
            </template>
            <span>自動對焦</span>
          </v-tooltip>
        </v-speed-dial>
        <v-divider></v-divider>
        <!-- 影像調整image adjustment ------------------------------------------------------------------------------ -->
        <p class="subtitle text-center"><br />影像<br />調整</p>
        <!-- 全螢幕fullscreen -->
        <v-tooltip right class="tips">
          <template #activator="{ on, attrs }">
            <v-btn
              class="left-btn mx-3"
              elevation="6"
              icon
              v-bind="attrs"
              v-on="on"
            >
              <img
                class=""
                alt="spot"
                src="/left-icons/fullscreen.png"
                width="19em"
              />
            </v-btn>
          </template>
          <span>全螢幕</span>
        </v-tooltip>
        <!-- 影像快照snapshot -->
        <v-tooltip right class="tips">
          <template #activator="{ on, attrs }">
            <v-btn
              class="left-btn mx-3 mt-3"
              elevation="6"
              icon
              v-bind="attrs"
              v-on="on"
            >
              <img
                class=""
                alt="line"
                src="/left-icons/snapshot.png"
                width="19em"
              />
            </v-btn>
          </template>
          <span>影像快照</span>
        </v-tooltip>
        <!-- 串流暫停freeze/持續unfreeze -->
        <v-tooltip right class="tips">
          <template #activator="{ on, attrs }">
            <v-btn
              class="left-btn mx-3 mt-3"
              icon
              v-bind="attrs"
              elevation="6"
              v-on="on"
              @click="freeze"
            >
              <img
                id="unfreeze"
                alt="rectangle"
                src="/left-icons/freeze/unfreeze.png"
                width="9em"
              />
            </v-btn>
          </template>
          <span>串流暫停/持續</span>
        </v-tooltip>

        <!-- 隱藏/顯示監測項目hide/show overlay -->
        <v-tooltip right class="tips">
          <template #activator="{ on, attrs }">
            <v-btn
              class="left-btn mx-3 my-3"
              elevation="6"
              icon
              v-bind="attrs"
              v-on="on"
            >
              <img
                class=""
                alt="rectangle"
                src="/left-icons/hide-overlay.png"
                width="18em"
              />
            </v-btn>
          </template>
          <span>隱藏/顯示監測項目</span>
        </v-tooltip>
      </v-card>
    </div>

    <v-row justify="center" align="center">
      <!-- <v-col cols="1">

      </v-col> -->

      <v-col cols="5">
        <v-row>
          <v-col cols="12">
            <v-card>
              <v-card-title class="py-0"> <h6>顯示</h6> </v-card-title>
              <v-responsive :aspect-ratio="4 / 3">
                <div class="frame">
                  <img id="image" src="mockImg/1-200x100.png" />
                </div>
              </v-responsive>
            </v-card>
          </v-col>

          <v-col cols="12">
            <v-card>
              <v-card-title class="py-0">
                <h6>歷經時間</h6>

                <v-btn
                  v-on:click="isTransform = !isTransform"
                  x-small
                  class="realtimebtn ml-3"
                  >開始</v-btn
                >
                <v-btn
                  v-on:click="isTransform = !isTransform"
                  x-small
                  class="stop ml-3"
                  >暫停</v-btn
                >
              </v-card-title>

              <real-time-line-chart-2 />
            </v-card>
          </v-col>
        </v-row>
      </v-col>

      <v-col cols="4">
        <v-row>
          <v-col cols="5">
            <v-card justify="center" align="center">
              <v-card-title class="py-0"> <h6>濕度變化比對</h6> </v-card-title>
              <div class="carousel-wrapper px-0">
                <client-only>
                  <slick :options="slickOptions">
                    <!-- <div v-for="item in temperature" :key="item.mins"> -->
                    <div
                      v-for="item in temperature"
                      :key="item.mins"
                      class="img-wrapper"
                    >
                      <img :src="`mockImg/./${item.mins}-200x100.png`" />
                      <div class="subtitle">
                        TIME (MIN):&nbsp;&nbsp;{{
                          item.mins
                        }}&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TEMP (℃):&nbsp;&nbsp;{{
                          item.temp
                        }}
                      </div>
                    </div>
                    <!-- </div> -->
                  </slick>
                </client-only>
              </div>
            </v-card>
          </v-col>

          <v-col cols="5">
            <v-card justify="center" align="center">
              <v-card-title class="py-0"> <h6>濕度變化比對</h6> </v-card-title>
              <div class="carousel-wrapper px-0">
                <client-only>
                  <slick :options="slickOptions">
                    <!-- <div v-for="item in temperature" :key="item.mins"> -->
                    <div
                      v-for="item in temperature"
                      :key="item.mins"
                      class="img-wrapper"
                    >
                      <img :src="`mockImg/./${item.mins}-200x100.png`" />
                      <div class="subtitle">
                        TIME (MIN):&nbsp;&nbsp;{{
                          item.mins
                        }}&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TEMP (℃):&nbsp;&nbsp;{{
                          item.temp
                        }}
                      </div>
                    </div>
                    <!-- </div> -->
                  </slick>
                </client-only>
              </div>
            </v-card>
          </v-col>

          <v-col cols="2">
            <v-card justify="center" align="center" height="34.3em">
              <v-card-title class="py-0"> <h6>紀錄</h6> </v-card-title>
              <div class="subtitle">原沾濕面積: 100%</div>
              <br />
              <div class="subtitle">目前沾濕面積: 0%</div>
              <br />
              <div class="subtitle">比較面積差值:<br />17%</div>
              <br />
              <div class="subtitle">最大面積差值:<br />20%</div>
              <br />
              <div class="subtitle">最小面積差值:<br />8%</div>
              <br />
              <div class="subtitle">平均面積差值:<br />15%</div>
            </v-card>
          </v-col>

          <v-col cols="6">
            <v-card justify="center" align="center">
              <v-card-title class="py-0"> <h6>統計</h6> </v-card-title>
              <donut-chart-2 />
            </v-card> 
          </v-col>

                    <v-col cols="6">
            <v-card justify="center" align="center">
              <v-card-title class="py-0"> <h6>統計</h6> </v-card-title>
              <donut-chart-2 />
            </v-card> 
          </v-col>
          
        </v-row>
      </v-col>

      <v-col cols="2">
        <v-card>
          <v-card-title class="py-0">
            <h6 class="ngg">表面溫度</h6>
          </v-card-title>
          <v-card-text class="pb-0">
            100T
            <br />
            ROOM TEMP: 21±1℃ RH65±5% DISTANCE: 50±1CM
          </v-card-text>
          <v-simple-table fixed-header height="44.5em" class="mx-3 pb-3">
            <template v-slot:default>
              <thead>
                <tr>
                  <th class="text-center">TIME (MIN)</th>
                  <th class="text-center" style="padding-right: 40px">
                    TEMP (℃)
                  </th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="item in temperature" :key="item.mins">
                  <td class="text-center">{{ item.mins }}</td>
                  <td class="text-center" style="padding-right: 40px">
                    {{ item.temp }}
                  </td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
// echarts引入
import DonutChart2 from "../components/index/DonutChart/DonutChart2.vue";
import RealTimeLineChart2 from '../components/index/RealTimeChart/RealTimeLineChart2.vue';

export default {
  // echarts引入
  components: {
    DonutChart2,
    RealTimeLineChart2,
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
};
</script>
<style>
/* .carousel-wrapper {
  padding-left: 80px;
  padding-right: 80px;
} */

.img-wrapper img {
  /* margin: auto; */
  width: 200px;
  height: 150px;
  background-image: linear-gradient(gray 100%, transparent 0);
}

/* 影像串流 */

#image {
  width: 100%;
  pointer-events: none;
  isolation: isolate;
}
</style>

<style scoped>
/* 左側浮動按鈕 */
.drawer {
  position: fixed;
  width: 3.6em;
  left: -3.599em;
  height: 51.8em;
  transition: all 0.5s;
  border-radius: 0px 10px 10px 0px;
  z-index: 99999;
  /* background-color: #031316; */
  color: rgba(89, 89, 91, 1);
}
.box {
  background-color: #fff;
}
.box:hover .drawer {
  left: 0;
}

/* 影像串流 */

.arrow {
  height: 23px;
  width: 100px;
  position: absolute;
  margin-left: 1.16em;
  margin-top: 25.5em;
  transform: rotate(270deg);
  border-radius: 0 0 100px 100px;
}
/* 按鈕提示 */
.tips {
  z-index: 100000;
}
/* 區塊標題文字 */
.subtitle {
  font-size: 12px;
  color: #d9dddd;
  text-align: center;
}
.subtitle-right {
  font-size: 12px;
  color: #9ba3a5;
  text-align: left;
  font-family: "Noto Sans TC", sans-serif;
}
/* h4 {
  line-height: 2em;
  padding-left: 1em;
  color: #031418;
  font-family: 'Noto Sans TC', sans-serif;
  font-weight: bold;
} */
.gg {
  float: left;
  text-align: center;
}
.font-display {
  font-family: "Noto Sans TC", sans-serif;
}
.chartTitle {
  color: #545454;
}

.date-picker {
  float: right;
}

.card5 {
  display: flex;
  /* 水平置中 */
  justify-content: center;
  /* 垂直置中 */
  align-content: center;
  flex-wrap: wrap;
}
.card5content {
  width: 6em;
  float: left;
  margin: auto;
}
.btn {
  background-color: #f2f4f4;
}
.reset {
  float: right;
  margin-top: 0.5em;
  margin-right: 0.5em;
}
.cardtitle {
  line-height: 2.5em;
  font-weight: 900;
  color: #505f62;
}

.text-color >>> .v-text-field__slot input {
  color: #9ba3a5;
}

.left-btn {
  background-color: #2d2d2d;
  width: 2.25em;
  height: 2.25em;
}

.right-btn {
  background-color: #f2f4f4;
  width: 2.25em;
  height: 2.25em;
}

/* .ngg{
  color: #1d1d1d;
} */
</style>
