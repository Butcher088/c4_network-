<template>
<d2-container>
  <div class="text">
  这是介绍文字
  </div>
  <div class="chart" ref="chartYear">
  </div>
  <div class="chart" ref="chartDay">
  </div>
</d2-container>
</template>

<script>
export default {
  name: "predict",
  data(){
    return {
      YdataTure: [],
      YdataPre: [],
      DdataTure: [],
      DdataPre: [],
      days: [],
      hours: [],
    }
  },
  methods:{
    initChartYear(){
      this.getYearData()
      const chart = this.$refs.chartYear
      if(chart){
        const myChart = this.$echarts.init(chart)
        const option = {
              title: {
                text: '预测趋势（长期）',

              },
              tooltip: {
                trigger: 'axis'
              },
              legend: {
                data: ['真实值', '预测值' ]
              },
              grid: {
                left: '3%',
                right: '4%',
                bottom: '3%',
                containLabel: true
              },
              xAxis: {
                type: 'category',
                name: '时间',
                boundaryGap: false,
                data: this.days,
                axisLabel: {
                    interval: 30 //0：表示全部显示不间隔；auto:表示自动根据刻度个数和宽度自动设置间隔个数
                }
              },
              yAxis: {
                type: 'value',
                name: 'Y轴',
              },
              series: [
                {
                  name: '真实值',
                  type: 'line',
                  color: '#12e5ff',
                  data: this.YdataTure
                },
                 {
                  name: '预测值',
                  type: 'line',
                  color: '#ffd428',
                  data: this.YdataPre
                }

              ]
            }
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
    intChartDay(){
      this.getDayData()
      const chart = this.$refs.chartDay
      if(chart){
        const myChart = this.$echarts.init(chart)
        const option = {
              title: {
                text: '预测趋势（每天）',

              },
              tooltip: {
                trigger: 'axis'
              },
              legend: {
                data: ['真实值', '预测值' ]
              },
              grid: {
                left: '3%',
                right: '4%',
                bottom: '3%',
                containLabel: true
              },
              xAxis: {
                name: '时间',
                type: 'category',
                boundaryGap: false,
                data: this.hours,
                axisLabel: {
                    interval: 0 //0：表示全部显示不间隔；auto:表示自动根据刻度个数和宽度自动设置间隔个数
                }
              },
              yAxis: {
                name: 'Y轴',
                type: 'value'
              },
              series: [
                {
                  name: '真实值',
                  type: 'line',
                  color: '#12e5ff',
                  data: this.DdataTure
                },
                 {
                  name: '预测值',
                  type: 'line',
                  color: '#ffd428',
                  data: this.DdataPre
                }

              ]
            }
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
    //获取年的假数据
    getYearData(){
      let len = 365
      let max = 200
      let min = 0
      //生成真实值和预测值
      let value = Array.from({length:len}, v=> Math.floor(Math.random()*(max-min))+min);
      this.YdataTure = value
      value = Array.from({length:len}, v=> Math.floor(Math.random()*(max-min))+min);
      this.YdataPre = value
      //天数列表
      let days = new Array();
      for(let i=1;i<366;i++){
        days.push(i+'天');
      }
      //让x轴显示月份
      for(let i=0, j=1;i<366;i=i+31,j++){
        days[i] = j+'月'
      }
      this.days = days

    },
    //获取日的假数据
    getDayData(){
      let len = 24
      let max = 200
      let min = 0
      //生成真实值和预测值
      let value = Array.from({length:len}, v=> Math.floor(Math.random()*(max-min))+min);
      this.DdataTure = value
      value = Array.from({length:len}, v=> Math.floor(Math.random()*(max-min))+min);
      this.DdataPre = value
      //小时列表
      let hours = new Array();
      for(let i=0;i<24;i++){
        hours.push(i+'时');
      }
      this.hours = hours
    }

  },
  mounted() {
    this.initChartYear()
    this.intChartDay()
  }

}
</script>

<style scoped>
.text{
  width: 100%;
  height: 18%;
  margin: auto;
  background-color: #bdf1ff;
}
.chart{
  width: 98%;
  height: 39%;
  margin: 7px auto;
}
</style>
