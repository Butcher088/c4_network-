<template>
<d2-container>
    <div class="calendar" ref="calendarChart">
    </div>
    <div class="barChart" ref="barChart"></div>
    <div class="steps">
      <el-steps>
    <el-step  v-bind:title="index+'月'" :status="month===index?'finish':'process'"
              v-for="index of 12" :key="index" @click.native="changeMonth(index)" ></el-step>
  </el-steps>
    </div>
</d2-container>
</template>

<script>
import * as echarts from 'echarts';
export default {
  name: "calendar",
  data(){
    return {
      //日历数据
      calendarData: '',
      //当前选择月份
      month: 5,
      //柱状图用的数据
      data: [],
      days: []
    }
  },
  methods: {
    //初始化日历
    initCalendar(){
      this.calendarData = this.getVirtulData('2018')
       const chart = this.$refs.calendarChart
       if (chart) {
        const myChart = this.$echarts.init(chart)
        const option = {
              title: {
                top: 'top',
                left: 'center',
                text: '带宽日历'
              },
              tooltip: {
              trigger: 'item'
              },
            //图例
              visualMap: {
                min: 0,
                max: 10000,
                type: 'piecewise',
                orient: 'vertical',
                top: '55',
                inRange: {
                  color: ['#71d1ff','#0033ff']
                }

              },
              calendar: {
                top: 80,
                left: 150,
                right: 50,
                cellSize: ['auto', 13],
                range: '2018',
                itemStyle: {
                  borderWidth: 2
                },
                yearLabel: { show: false }
              },
              series: {
                type: 'heatmap',
                coordinateSystem: 'calendar',
                data: this.calendarData
              }
            };
        myChart.setOption(option)
        window.addEventListener("resize", function() {
          myChart.resize()
        })
      }
      this.$on('hook:destroyed',()=>{
        window.removeEventListener("resize", function() {
          myChart.resize();
        });
      })
    },
    //初始化柱状图
    initBarChart(){
      this.getMonthData()
      const chart = this.$refs.barChart
       if (chart) {
        const myChart = this.$echarts.init(chart)

          const option = {
               title: {
                top: 'top',
                left: 'center',
                text: '每日带宽情况'
              },
            //dataZoom-inside 内置型数据区域缩放组件 所谓内置 1平移：在坐标系中滑动拖拽进行数据区域平移。2缩放：PC端：鼠标在坐标系范围内滚轮滚动（MAC触控板类同;移动端：在移动端触屏上，支持两指滑动缩放。
            dataZoom: [{
              type: 'inside', //1平移 缩放
              throttle: '50', //设置触发视图刷新的频率。单位为毫秒（ms）。
              minValueSpan: 10, //用于限制窗口大小的最小值,在类目轴上可以设置为 5 表示 5 个类目
              start: 1, //数据窗口范围的起始百分比 范围是：0 ~ 100。表示 0% ~ 100%。
              end: 50, //数据窗口范围的结束百分比。范围是：0 ~ 100。
              zoomLock: true, //如果设置为 true 则锁定选择区域的大小，也就是说，只能平移，不能缩放。
            }],
            // 主要用来控制图表四周留白
            grid: {
            },
            // 提示框组件
            tooltip: {
              trigger: 'axis', //坐标轴触发，主要在柱状图，折线图等会使用类目轴的图表中使用。
              axisPointer: { //去掉移动的指示线
              },
              // 自定义提示框内容
              formatter: function (params, ticket, callback) {
                var text = params[0].data.date + ': ' + params[0].data.value
                return text;
              }
            },
            //直角坐标系 grid 中的 x 轴，
            xAxis: {
              name: '时间',
              type: 'category', //'category' 类目轴，适用于离散的类目数据，为该类型时必须通过 data 设置类目数据。
              // 坐标轴刻度标签(类目,简单说就是x轴上的内容)的相关设置
              axisLabel: {
                //  是否显示坐标刻度标签(这了指是否显示x轴上的月份)
                show: true,
              },
              //x轴刻度线设置
              axisTick: {
                "show": false
              },
              // 类目数据，在类目轴（type: 'category'）中有效。
              data: this.days
            },
            //直角坐标系 grid 中的 y 轴，
            yAxis: {
              name: '带宽利用率',
              type: 'value', //'value' 数值轴，适用于连续数据。
              // 坐标轴轴线相关设置
              axisLine: {
                show: false //y轴线消失
              },
              // 坐标轴刻度标签(类目,简单说就是x轴上的内容)的相关设置
              axisLabel: {
                show: true,
              },
              //y轴刻度线设置
              axisTick: {
                "show": false
              },
              splitNumber: 5, //坐标轴的分割段数，需要注意的是这个分割段数只是个预估值，最后实际显示的段数会在这个基础上根据分割后坐标轴刻度显示的易读程度作调整.在类目轴中无效。
            },
            series: [{
              type: 'bar',
              // 系列中的数据内容数组。数组项通常为具体的数据项。
              data: this.data,
              // 折线条的样式
              lineStyle: {
                color: '#377CFF',
                width: 1
              },
              // 折线拐点的样式
               itemStyle: {
                  color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                    { offset: 0, color: '#83bff6' },
                    { offset: 0.5, color: '#188df0' },
                    { offset: 1, color: '#188df0' }
                  ])
                }
            }]
          };
        myChart.setOption(option)
        window.addEventListener("resize", function() {
          myChart.resize()
        })
      }
      this.$on('hook:destroyed',()=>{
        window.removeEventListener("resize", function() {
          myChart.resize();
        });
      })
    },
    //改变月份
    changeMonth(index){
      console.log('index:'+index)
      this.month = index
      //重新获取数据
      this.initBarChart()
    },
     //日历假数据
    getVirtulData(year) {
          year = year || '2017';
          var date = +echarts.number.parseDate(year + '-01-01');
          var end = +echarts.number.parseDate(+year + 1 + '-01-01');
          var dayTime = 3600 * 24 * 1000;
          var data = [];
          for (var time = date; time < end; time += dayTime) {
            data.push([
              echarts.format.formatTime('yyyy-MM-dd', time),
              Math.floor(Math.random() * 10000)
            ]);
          }
        return data;
      },
      //月份假数据
    getMonthData(){
      //数据
      let len = 30
      let max = 1500
      let min = 100
      let value = Array.from({length:len}, v=> Math.floor(Math.random()*(max-min))+min);
      //天数
      let date = new Array();
      for(let i=1;i<31;i++){
        date.push('第'+i+'天');
      }
      //合并成对象数组
      let data = []
      for(let i=0;i<30;i++){
        data.push({
          date: date[i],
          value: value[i]
        })
      }
      this.data = data
      this.days = date
    }

  },
  mounted() {
    this.initCalendar()
    this.initBarChart()
  }
}
</script>

<style scoped>
.calendar{
  height: 40%;
  width: 100%;
}
.barChart{
  height: 50%;
  width: 100%;
}
.steps{
  width: 90%;
  margin: auto;
}
</style>
