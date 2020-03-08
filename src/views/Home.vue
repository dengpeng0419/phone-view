<template>
  <div class="invest-target">
    <div class="foot">国网新疆电力有限公司</div>
    <div class="page-title">
      新疆维吾尔自治区企业复工复产分析看板
    </div>
    <div class="page-time">2020年2月13日</div>
    <div class="page-banner">
      <div class="banner-detail">
         <div class="banner-rect">
           <div class="unit">（万千瓦）</div>
           <div class="title">同期最大负荷</div>
           <div class="value">1399.5</div>
         </div>
         <div class="banner-rect">
           <div class="unit">（万千瓦）</div>
           <div class="title">当日最大负荷</div>
           <div class="value">1426.81<span style="color:#E0E957">11.23% &uarr;</span></div>
         </div>
      </div>
      <div class="banner-detail">
         <div class="banner-rect small">
           <div class="title">企业复工率</div>
           <div class="value" style="color:#38D7AC">65%</div>
         </div>
      </div>
    </div>
    <div class="page-banner">
      <div class="banner-detail">
         <div class="banner-rect">
           <div class="unit">（万千瓦时）</div>
           <div class="title">同期电量</div>
           <div class="value">27710.45</div>
         </div>
         <div class="banner-rect">
           <div class="unit">（万千瓦时）</div>
           <div class="title">当日电量</div>
           <div class="value">25726.3<span style="color:#85F6C8">7.71% &darr;</span></div>
         </div>
      </div>
      <div class="banner-detail">
         <!-- <div class="banner-rect small">
           <div class="title">企业复工率</div>
           <div class="value" style="color:#38D7AC">65%</div>
         </div> -->
         <div class="banner-rect small">
           <div class="title">企业复产率</div>
           <div class="value" style="color:#E43B08">60.1%</div>
         </div>
      </div>
    </div>
    <div class="page-content">
      <div class="content-middle">
        <div class="content-title">各地州复工复产情况</div>
        <!-- <div class="map-chart" :options="option"></div> -->
        <div class="map-chart-frame">
          <v-chart class="map-chart" :options="option"></v-chart>
          <div class="map-label">
            <div>复工率:</div>
            <div class="map-radio" style="background:#E5E72D"></div>
            <div>60%~100%</div>
            <div class="map-radio" style="background:#37D3C2"></div>
            <div>30%~60%</div>
          </div>
        </div>
        <div class="content-title">各行业企业复产率</div>
        <v-chart class="bar-chart" :options="trendOption"></v-chart>
        <div class="content-title">大工业用户</div>
        <div class="banner-detail">
          <div class="banner-rect medium" style="margin-right: 10px;">
            <div class="title">当日电量</div>
            <div class="value">436609.6<span style="color:#85F6C8">9.80% &darr;</span></div>
          </div>
          <div class="banner-rect mini">
            <div class="title">复工率</div>
            <div class="value">40.30%</div>
          </div>
        </div>
        <v-chart class="chart-top" :options="topOption"></v-chart>
        <v-chart class="chart-top" :options="bottomOption"></v-chart>

        <div class="content-title">10KV及以下一般工商业</div>
        <div class="banner-detail">
          <div class="banner-rect medium" style="margin-right: 10px;">
            <div class="title">当日电量</div>
            <div class="value">436609.6<span style="color:#DEED81">9.80% &uarr;</span></div>
          </div>
          <div class="banner-rect mini">
            <div class="title">复工率</div>
            <div class="value">67.40%</div>
          </div>
        </div>
        <v-chart class="chart-top" :options="topOption2"></v-chart>
        <v-chart class="chart-top" :options="bottomOption2"></v-chart>
      </div>
    </div>

    <!-- <div class="content">
      <div class="left">
        <div class='banner'>
          <div class="banner-title">{{fixedAssetInvest.label}}</div>
          <div class="banner-content">
            <div class="banner-rect" v-for="(item, index) in fixedAssetInvest.banner" :key=index>
              <div class="top">
                <div class="title">{{item.label}} {{item.unit}}</div>
                <div class="time" :style="{color:item.progress ==='进度滞后'?'#cb0000':'#00ff3c'}">{{item.progress}}</div>
              </div>
              <div class="value">{{item.data.fulfillRate}}</div>
              <div class="bottom">
                <div>
                  <div class="num">{{item.data.year}}</div>
                  <div class="desc">累计完成值</div>
                </div>
                <div>
                  <div class="num">{{item.data.plan}}</div>
                  <div class="desc">年度计划值</div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="chart-frame">
          <div class="title">{{capitalConst.label}}</div>
          <v-chart class="rank-chart" :options="trendOption"></v-chart>
        </div>
      </div>
      <div class="right">
        <div class="title">{{otherSpecialPlan.label}}</div>
        <v-chart class="rank-chart2" :options="trendOption2"></v-chart>
      </div>
    </div> -->
  </div>
</template>

<script>
import { bigCompany, normalCompany, percent } from './data/bigCompany'
import { mapValue1, mapValue2, geoCoordMap } from './data/mapData'
//require('./data/china.js')
export default {
  name: 'home',
  data() {
    return {
      options: [],
      timeOptions: [],
      timeValue: '2019-12',
      year: 2019,
      month: 12,
      value: '',
      yearLabel: '2019年',
      monthLabel: '12月',
      topOption: {},
      bottomOption: {},
      topOption2: {},
      bottomOption2: {},
      trendOption: {},
      companyOptions: [],
      companyValue: 0,
      fixedAssetInvest: {},
      capitalConst: {},
      otherSpecialPlan: {},
      option: {}
    }
  },
  mounted() {
    this.option = {
        //backgroundColor: '#022036',
        // title: {
        //     text: '全国主要城市空气质量',
        //     subtext: 'data from PM25.in',
        //     sublink: 'http://www.pm25.in',
        //     left: 'center',
        //     textStyle: {
        //         color: '#fff'
        //     }
        // },
        tooltip : {
            trigger: 'item',
            formatter: function (params,ticket,callback) {
              const data = params.data
              return data.name + ': ' + data.percent + '%'
            }
        },
        // legend: {
        //     orient: 'vertical',
        //     y: 'bottom',
        //     x:'right',
        //     data:['pm2.5'],
        //     textStyle: {
        //         color: '#fff'
        //     }
        // },
        geo: {
              map: 'china',
              zoom: 3,
              center: [85, 42],
              scaleLimit: {
                min: 3,
                max: 15
              },
              label: {
                // show: true,
                color: '#717F8B',
                  emphasis: {
                      show: true,
                      color: '#ddd',
                  }
              },
              roam: true,
              itemStyle: {
                  normal: {
                  areaColor: '#022036',
                  borderColor: '#111',
                  borderWidth: 1
              },
              emphasis: {
                  areaColor: '#717F8B'
              }
          }
          },
          series : [
              {
                  name: '复工率',
                  type: 'scatter',
                  coordinateSystem: 'geo',
                  data: this.convertData(mapValue1),
                  symbolSize: function (val) {
                      return val[2] / 5;
                  },
                  label: {
                      normal: {
                          formatter: '{b}',
                          position: 'right',
                          show: true
                      },
                      emphasis: {
                          show: false
                      }
                  },
                  itemStyle: {
                      normal: {
                          color: '#E5E72D'
                      }
                  }
              },
              {
                  name: '复工率',
                  type: 'scatter',
                  coordinateSystem: 'geo',
                  data: this.convertData(mapValue2),
                  symbolSize: function (val) {
                      return val[2] / 5;
                  },
                  label: {
                      normal: {
                          formatter: '{b}',
                          position: 'right',
                          show: false
                      },
                      emphasis: {
                          show: false
                      }
                  },
                  itemStyle: {
                      normal: {
                          color: '#37D3C2'
                      }
                  }
              },
              {
                  name: 'Top 5',
                  type: 'effectScatter',
                  coordinateSystem: 'geo',
                  data: this.convertData(mapValue1),
                  symbolSize: function (val) {
                      return val[2] / 5;
                  },
                  showEffectOn: 'render',
                  rippleEffect: {
                      brushType: 'stroke'
                  },
                  hoverAnimation: true,
                  label: {
                      normal: {
                          formatter: '{b}',
                          position: 'right',
                          show: true
                      }
                  },
                  itemStyle: {
                      normal: {
                          color: '#f4e925',
                          shadowBlur: 10,
                          shadowColor: '#333'
                      }
                  },
                  zlevel: 1
              }
          ]
        }
      const curRouter = this.$router.history.current.name;
      this.getPageData();
    },
    methods: {
      convertData(data) {
          var res = [];
          for (var i = 0; i < data.length; i++) {
              var geoCoord = geoCoordMap[data[i].name];
              if (geoCoord) {
                  res.push({
                      name: data[i].name,
                      percent: data[i].value,
                      value: geoCoord.concat(data[i].value)
                  });
              }
          }
          return res;
      },
    getPageData() {
      let bigCompany_x = []
      let bigCompany_y1 = []
      let bigCompany_y2 = []
      let bigCompany_y3 = []
      bigCompany.map((item) => {
        bigCompany_x.push(item['日期'])
        bigCompany_y1.push(item['当日电量'])
        bigCompany_y2.push(item['同期电量'])
        bigCompany_y3.push(item['复工率'].replace('%',''))
      })
      this.topOption = this.showLine('用电趋势', bigCompany_x, bigCompany_y1,bigCompany_y2,5000)
      this.bottomOption = this.showLine('复工率趋势', bigCompany_x, bigCompany_y3,30)

      let normalCompany_x = []
      let normalCompany_y1 = []
      let normalCompany_y2 = []
      let normalCompany_y3 = []
      normalCompany.map((item) => {
        normalCompany_x.push(item['日期'])
        normalCompany_y1.push(item['当日电量'])
        normalCompany_y2.push(item['同期电量'])
        normalCompany_y3.push(item['复工率'].replace('%',''))
      })
      this.topOption2 = this.showLine('用电趋势', normalCompany_x, normalCompany_y1,normalCompany_y2,5000)
      this.bottomOption2 = this.showLine('复工率趋势', normalCompany_x, normalCompany_y3,30)

      let percent_x = []
      let percent_y1 = []
      percent.map((item) => {
        percent_x.push(item['类别'])
        percent_y1.push(item['复产率'].replace('%',''))
      })
      this.trendOption = {
          // title: {
          //   text: '基本建设',
          //   textStyle: {
          //     color: '#77bde1',
          //     fontSize: 22
          //   },
          //   padding: 10
          // },
          tooltip: {
            trigger: 'axis',
            formatter: "{a}<br/>{b} : {c}%",
          },
          calculable : true,
          // legend: {
          //   data: ['累计完成值','年度完成值'],
          //   x: 'right',
          //   y: 'top',
          //   padding: [0,10,0,0],
          //   textStyle: {
          //     color: '#77bde1'
          //   }
          // },
          xAxis: [{
            type : 'category',
            data : percent_x,
            // boundaryGap : [0, 0.01],
            axisLine: {
              show: true,
              lineStyle: {
                color: '#50586c'
              }
            },
            axisTick: {
              show: false
            },
            axisLabel:{
              interval:0,
              rotate: 65,//倾斜度 -90 至 90 默认为0
              textStyle:{
                color: '#77bde1',
                fontSize: 9
              }
            },
            splitLine: {
              show: false,
              lineStyle: {
                color: '#50586c'
              }
            }
          }],
          yAxis: [{
            type : 'value',
            axisLine: {
              show: false,
              lineStyle: {
                color: '#50586c'
              }
            },
            axisTick: {
              show: false
            },
            splitLine: {
              show: false,
              lineStyle: {
                color: '#50586c'
              }
            },
            axisLabel: {
              textStyle: {
                color: '#77bde1',
                fontSize: 8
              }
            }
          }],
          grid: {
            //x: '2%',
            // width: '45%'
            left: '10%',
            top: '5%',
            right: '5%',
            bottom: '60%'
          },
          series: [{
            name:'各行业企业复产率',
            type:'bar',
            data: percent_y1,
            barMaxWidth: 5,
            itemStyle: {
              normal: {
                color: '#63B5DE'
              }
            },
            // label: {
            //   normal: {
            //     show: true,
            //     position: 'top',
            //     color: '#fff',
            //     fontSize: 14
            //   }
            // },
          }]
        };
    },
    showLine(title, x,line1,line2,line3,minData){
      return {
          title: {
            text: title,
            textStyle: {
              color: '#C5EDF8',
              fontSize: 14
            }
          },
          tooltip: {
            trigger: 'axis',
            textStyle: {
              align: 'left'
            }
          },
          grid: {
            top: '18%',
            left: '5%',
            right: '5%',
            bottom: '5%',
            containLabel: true
          },
          // legend: {
          //   data: ['2020','2019'],
          //   x: 'right',
          //   y: 'top',
          //   padding: 10,
          //   textStyle: {
          //     color: '#77bde1'
          //   }
          // },
          calculable : true,
          xAxis: [{
            type: 'category',
            boundaryGap: false,
            data: x,
            axisLine: {
              show: false,
              lineStyle: {
                color: '#8d8d8d'
              }
            },
            axisTick: {
              show: false
            },
            axisLabel: {
              textStyle: {
                color: '#C5EDF8',
                fontSize: 10
              }
            }
          }],
          yAxis: [{
            type: 'value',
            function (value) {
                return value.min - minData;
            },
            axisLine: {
              show: false,
              lineStyle: {
                color: '#8d8d8d'
              }
            },
            axisTick: {
              show: false
            },
            splitLine: {
              show: false,
              lineStyle: {
                color: '#50586c'
              }
            },
            axisLabel: {
              textStyle: {
                color: '#C5EDF8',
                fontSize: 10
              }
            }
          }],
          series: [
            {
              name:'2020',
              type:'line',
              data: line1,
              smooth: true,
              symbol: "none",
              itemStyle: {
                color: '#2EB792',
                borderColor: '#2EB792'
              },
            },
            {
              name:'2019',
              type:'line',
              data: line2,
              smooth: true,
              symbol: "none",
              itemStyle: {
                color: '#468DB2',
                borderColor: '#468DB2'
              },
            },
            {
              name:'2018',
              type:'line',
              data: line3,
              smooth: true,
              symbol: "none",
              itemStyle: {
                color: '#efea3d',
                borderColor: '#efea3d'
              },
            }
          ]
        }
    },
  }
}
</script>

<style lang="scss">
  #app {
    padding: 0 20px;
    box-sizing: border-box;
  }

  .invest-target {
    // font-size: 49px;
    width: 100%;
    min-height: 100vh;
    position: relative;
    display: flex;
    align-items: center;
    box-sizing: border-box;
    flex-direction: column;
    padding-bottom: 76px;
    .foot {
      position: absolute;
      left: 0;
      right: 0;
      text-align: center;
      // right: 45px;
      bottom: 10px;
      font-size:12px;
      font-family: "Microsoft YaHei", sans-serif;
      font-weight:400;
      color:rgba(223,235,255,1);
    }
    .page-title {
      margin-top: 28px;
      font-size:28px;
      font-family: "Microsoft YaHei", sans-serif;
      font-weight:bold;
      color:rgba(223,235,255,1);
      line-height:58px;
    }
    .page-time {
      width: 100%;
      margin-top: 24px;
      text-align: right;
      // padding-right: 100px;
      font-size:14px;
      font-family: "Microsoft YaHei", sans-serif;
      font-weight:400;
      color:rgba(119,189,225,1);
    }
    .page-banner {
      // width:1350px;
      width: 100%;
      height:100px;
      background:rgba(54,102,161,0.15);
      display: flex;
      align-items: center;
      justify-content: space-between;
      //opacity:0.15;
      .small {
        width: 180px !important;
      }

    }
    .banner-detail {
      display: flex;
      margin: 20px 0;
      .banner-rect {
        position: relative;
        width:200px;
        height:80px;
        background:rgba(54,102,161,0.15);
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        border:2px solid rgba(22,83,148,0.8);
        .unit {
          position: absolute;
          top: 5px;
          right: 0;
          font-size:10px;
          font-family: "Microsoft YaHei", sans-serif;
          font-weight:400;
          color:rgba(218,234,254,1);
        }
        .title {
          font-size:20px;
          font-family: "Microsoft YaHei", sans-serif;
          font-weight:400;
          color:rgba(218,234,254,1);
          text-align: left;
          margin-left: 4px;
        }
        .value {
          font-size:22px;
          font-family: "Microsoft YaHei", sans-serif;
          font-weight:400;
          color:rgba(152,208,255,1);
          span {
            font-size:14px;
            margin-left: 40px;
          }
        }
      }
    }
    .page-content {
      width:1350px;
      width: 100%;
      display: flex;
      justify-content: space-between;
      .content-middle {
        width:100%;
        // height:65vh;
        background:rgba(54,102,161,0.15);
        .content-title {
          width: 100%;
          font-size:28px;
          font-family: "Microsoft YaHei", sans-serif;
          font-weight:bold;
          color:rgba(197,237,248,1);
          height:44px;
          line-height: 44px;
          background:linear-gradient(90deg,rgba(41,98,138,1) 0%,rgba(21,56,94,1) 100%);
          box-shadow:0px 3px 8px 0px rgba(2,25,50,0.27);
          text-align: left;
          padding-left: 10px;
          box-sizing: border-box;
        }
      }
      .medium {
        width: 204px !important;
        height: 70px !important;
        .value {
          font-size: 22px;
        }
      }
      .mini {
        width: 136px !important;
        height: 70px !important;
        .value {
          font-size: 22px;
        }
      }
    }

    .chart-top {
      width: 350px;
      width: 100%;
      height: 25vh;
    }

    .bar-chart {
      width: 600px;
      width: 100%;
      height: 28vh;
    }

    .map-chart-frame {
      width: 600px;
      height: 28vh;
      overflow: hidden;
      position: relative;
      .map-label {
        position: absolute;
        bottom: 0;
        left: 0;
        color: #B9E1EE;
        height: 40px;
        line-height: 40px;
        width: 100%;
        background:rgba(38,54,66,1);
        font-size:20px;
        font-family: "Microsoft YaHei", sans-serif;
        font-weight:400;
        text-align: left;
        padding-left: 10px;
        display: flex;
        align-items: center;
      }
      .map-radio {
        margin: 0 10px;
        width:10px;
        height:10px;
        border-radius: 50%;
      }
    }

    .map-chart {
      width: 600px;
      width: 100%;
      height: 28vh;
    }

    .el-input__inner {
      background-color: #2b516c;
          border: 1px solid #2b516c;
    }
    .el-select .el-input.is-focus .el-input__inner {
      border-color: #2b516c;
    }
    .el-select .el-input__inner:focus {
      border-color: #2b516c;
    }
    .el-input__inner {
      color: #77bde1;
    }
  }

</style>

