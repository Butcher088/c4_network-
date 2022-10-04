<template>
  <d2-container>
      <div class="up-body">
        <div class="chart-pie" ref="pieChart"></div>
        <div class="chart-bar" ref="barChart"></div>
      </div>
      <div class="down-body">
        <el-table
        :data="tableData"
        stripe
        ref="table"
        height="100%">
        <el-table-column
          prop="date"
          label="时间"
        align="center">
        </el-table-column>
        <el-table-column
          prop="ip"
          label="IP地址"
        align="center">
        </el-table-column>
        <el-table-column
          prop="port"
          label="端口"
        align="center">
        </el-table-column>
          <el-table-column
          prop="type"
          label="协议"
          align="center">
        </el-table-column>
           <el-table-column
          prop="security"
          label="安全情况"
           align="center">
             <template slot-scope="scope">
              <el-tag
                :type="scope.row.security === '正常' ? 'success' : 'danger'"
                disable-transitions>{{scope.row.security}}
              </el-tag>
            </template>
        </el-table-column>
      </el-table>
      </div>
  </d2-container>
</template>

<script>
export default {
  name: "exception",
  data(){
    return {
      pieData:  [
        { value: 1048, name: '正常'},
        { value: 735, name: '异常'}
      ],
      barDataNor: [],
      barDataExc: [],
      days: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],

      //表格数据
       tableData: [{
          date: '2020-5-3 7:31:20',
          ip: '172.105.113.33',
          port: '50132',
          type: 'TCP',
          security: '正常'
        },{
          date: '2020-5-3 7:31:20',
          ip: '172.105.113.33',
          port: '132',
          type: 'TCP',
          security: '异常'
        },{
          date: '2020-5-4 7:31:20',
          ip: '172.105.113.33',
          port: '50132',
          type: 'TCP',
          security: '正常'
        },{
          date: '2020-12-3 7:31:20',
          ip: '172.105.113.33',
          port: '50132',
          type: 'TCP',
          security: '异常'
        },{
          date: '2020-5-3 7:31:20',
          ip: '172.105.113.33',
          port: '5032',
          type: 'TCP',
          security: '正常'
        },{
          date: '2020-5-3 4:31:20',
          ip: '172.105.113.33',
          port: '50132',
          type: 'TCP',
          security: '正常'
        },{
          date: '2021-5-3 7:31:20',
          ip: '172.105.113.33',
          port: '50132',
          type: 'TCP',
          security: '异常'
        },{
          date: '2020-5-3 7:31:20',
          ip: '172.105.113.33',
          port: '50132',
          type: 'TCP',
          security: '正常'
        },]
    }
  },
  methods: {
    initPieChart(){
        const chart = this.$refs.pieChart
        if(chart){
        const myChart = this.$echarts.init(chart)
        const option = {
                  title: {
                    text: '正常异常比例',
                    left: 'center'
                  },
                  tooltip: {
                    trigger: 'item',
                  },
                  legend: {
                    orient: 'vertical',
                    left: '30'
                  },

                  color: ['#33a9ec','#ef6567',],
                  series: [
                    {
                      type: 'pie',
                      radius: '65%',
                      data: this.pieData,
                      emphasis: {
                        itemStyle: {
                          shadowBlur: 10,
                          shadowOffsetX: 0,
                          shadowColor: 'rgba(0, 0, 0, 0.5)'
                        }
                      },
                      label: {
                        show: true,
                        position: 'outside',
                        formatter: "{b} {d}%"
                      }
                    }
                  ]
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
    initBarChart(){
        this.getBarDate()
        const chart = this.$refs.barChart
        if(chart){
        const myChart = this.$echarts.init(chart)
        const option = {
          title: {
            text: '周日正异常情况',
            left: 'center'
          },
          tooltip: {
            trigger: 'axis',
            axisPointer: {
              type: 'shadow'
            }
          },
          legend: {
            show: true,
            left: 'right',
            orient: 'vertical'
          },
          grid: {
            left: '2%',
            right: '2%',
            bottom: '12%',
            containLabel: true
          },
          xAxis: [
            {
              type: 'category',
              data: this.days,
              axisTick: {
                alignWithLabel: true
              }
            }
          ],
          yAxis: [
            {
              type: 'value'
            }
          ],
          series: [{
              name: '正常',
              type: 'bar',
              barWidth: '30%',
              color: '#33a9ec',
              data: this.barDataNor,
          },
            {
              name: '异常',
              type: 'bar',
              barWidth: '30%',
              color: '#ef6567',
              data: this.barDataExc
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
    //获取柱状图假数据
    getBarDate(){
      let len = 7
      let max = 500
      let min = 0
      //生成正常值和异常
      let normal = Array.from({length:len}, v=> Math.floor(Math.random()*(max-min))+min);
      let except = Array.from({length:len}, v=> Math.floor(Math.random()*(max-min))+min);
      this.barDataNor = normal
      this.barDataExc = except

    },
    //自动滚动
    tableScroll(){
     const table = this.$refs.table;
    // 拿到表格中承载数据的div元素
    const divData = table.bodyWrapper;
    // 拿到元素后，对元素进行定时增加距离顶部距离，实现滚动效果(此配置为每100毫秒移动1像素)
    setInterval(() => {
      // 元素自增距离顶部1像素
      divData.scrollTop += 1;
      // 判断元素是否滚动到底部(可视高度+距离顶部=整个高度)
      if (divData.clientHeight + divData.scrollTop == divData.scrollHeight) {
        // 重置table距离顶部距离
        divData.scrollTop = 0;
      }
    }, 100);  // 滚动速度
    }

  },
  mounted() {
    this.initPieChart()
    this.initBarChart()
    this.tableScroll()
  }
}
</script>

<style scoped>

.up-body{
  width: 100%;
  height: 45%;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
}
.chart-pie{
  width: 40%;
  height: 100%;
}
.chart-bar{
  width: 50%;
  height: 100%;
}
.down-body{
  width: 100%;
  background-color: #2aabd2;
  height: calc(55% - 30px);
}
</style>
