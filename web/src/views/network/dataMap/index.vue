<template>
  <d2-container>
    <div class="main-body">
      <div ref="chart" class="chart"></div>
      <div class="table"><el-table
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
      </el-table></div>
    </div>
  </d2-container>
</template>

<script>
import data from 'echarts/map/json/world'
import a from 'echarts/'
import * as echarts from "echarts";

echarts.registerMap('world', data);

export default {
  name: 'dataMap',
  data() {
    return {
      //地图数据
      nodes: [[116.3972, 39.9075],
        [-97.822, 37.751],
        [113.72200000000001, 34.7732],
        [120.3024, 36.1155],
        [114.1842, 22.3163],
        [103.8554, 1.3036],
        [139.6899, 35.6893],
        [121.5513, 29.8797],
        [-118.244, 34.0544],
        [118.0633, 36.7906],
        [143.2104, -33.494],
        [120.1612, 30.2994],
        [129.0394, 35.1025],
        [126.9754, 37.5794],
        [117.1762, 39.1488],
        [-119.7257, 45.8234],
        [6.1847, 52.6959],
        [120.602, 31.3093],
        [121.5324, 25.0504],
        [122.1225, 37.5074],
        [117.0211, 36.6756],
        [-122.4121, 37.7506],
        [144.9669, -37.8159],
        [114.5916, 36.1351],
        [121.4581, 31.2222],
        [-6.2591, 53.3379],
        [-93.6124, 41.6021],
        [4.8995, 52.3824]],
      lines: [{coords: [[116.3972, 39.9075], [-97.822, 37.751]]},
        {coords: [[116.3972, 39.9075], [113.72200000000001, 34.7732]]},
        {coords: [[116.3972, 39.9075], [120.3024, 36.1155]]},
        {coords: [[116.3972, 39.9075], [114.1842, 22.3163]]},
        {coords: [[116.3972, 39.9075], [103.8554, 1.3036]]},
        {coords: [[116.3972, 39.9075], [139.6899, 35.6893]]},
        {coords: [[116.3972, 39.9075], [121.5513, 29.8797]]},
        {coords: [[116.3972, 39.9075], [-118.244, 34.0544]]},
        {coords: [[116.3972, 39.9075], [118.0633, 36.7906]]},
        {coords: [[116.3972, 39.9075], [143.2104, -33.494]]},
        {coords: [[116.3972, 39.9075], [120.1612, 30.2994]]},
        {coords: [[116.3972, 39.9075], [129.0394, 35.1025]]},
        {coords: [[116.3972, 39.9075], [126.9754, 37.5794]]},
        {coords: [[116.3972, 39.9075], [117.1762, 39.1488]]},
        {coords: [[116.3972, 39.9075], [-119.7257, 45.8234]]},
        {coords: [[116.3972, 39.9075], [6.1847, 52.6959]]},
        {coords: [[116.3972, 39.9075], [120.602, 31.3093]]},
        {coords: [[116.3972, 39.9075], [121.5324, 25.0504]]},
        {coords: [[116.3972, 39.9075], [122.1225, 37.5074]]},
        {coords: [[116.3972, 39.9075], [117.0211, 36.6756]]},
        {coords: [[116.3972, 39.9075], [-122.4121, 37.7506]]},
        {coords: [[116.3972, 39.9075], [144.9669, -37.8159]]},
        {coords: [[116.3972, 39.9075], [114.5916, 36.1351]]},
        {coords: [[116.3972, 39.9075], [121.4581, 31.2222]]},
        {coords: [[116.3972, 39.9075], [-6.2591, 53.3379]]},
        {coords: [[116.3972, 39.9075], [-93.6124, 41.6021]]},
        {coords: [[116.3972, 39.9075], [4.8995, 52.3824]]}],

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
        },{
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
        },{
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
    initChart() {
      const chart = this.$refs.chart
      if (chart) {
        const myChart = this.$echarts.init(chart)
        const option = {
          geo: {
            map: 'world',
            zlevel: 10,
            show: true,
            layoutCenter: ['50%', '50%'],
            roam: true,
            layoutSize: "90%",
            zoom: 1,
            itemStyle: {
              normal: {
                color: '#383838',
                borderWidth: 1.1,
                borderColor: '#43D0D6'
              }
            },
            emphasis: {
              itemStyle: {
                color: '#2eafff'
              },
              label: {
                show: true,
                color: '#ececec'
              }
            }
          },
          series: [
            {
              type: 'effectScatter',
              coordinateSystem: 'geo',
              zlevel: 15,
              symbolSize: 8,
              rippleEffect: {
                period: 4,
                brushType: 'stroke',
                scale: 6
              },
              itemStyle: {
                color: '#FFB800',
                opacity: 1
              },
              data: this.nodes.slice(0, 10)
            },
            {
              type: 'effectScatter',
              coordinateSystem: 'geo',
              zlevel: 15,
              symbolSize: 8,
              rippleEffect: {
                period: 6,
                brushType: 'stroke',
                scale: 6
              },
              itemStyle: {
                color: '#44ea52',
                opacity: 1
              },
              symbol: 'circle',
              data: this.nodes.slice(10, 19)
            },
            {
              type: 'effectScatter',
              coordinateSystem: 'geo',
              zlevel: 15,
              symbolSize: 6,
              rippleEffect: {
                period: 6,
                brushType: 'fill',
                scale: 6
              },
              itemStyle: {
                color: '#22ffff',
                opacity: 1
              },
              symbol: 'circle',
              data: this.nodes.slice(19, 29)
            },

            {
              type: 'lines',
              coordinateSystem: 'geo',
              zlevel: 15,
              silent: true,
              lineStyle: {
                // color: '#c23531',
                //color: 'rgb(200, 35, 45)',
                opacity: 0.3,
                width: 1.4,
                curveness: 0.3
              },
              data: this.lines.slice(0, 9)
            },
            {
              type: 'lines',
              coordinateSystem: 'geo',
              lineStyle: {
                color: '#ffee39',
                opcity: 1,
                width: 0,
                curveness: 0.3
              },
              effect: {
                constantSpeed: 60,
                show: true,
                trailLength: 0.1,
                symbolSize: 2.5
              },
              zlevel: 15,
              data: this.lines.slice(0, 9)
            },
            {
              type: 'lines',
              coordinateSystem: 'geo',
              zlevel: 15,
              silent: true,
              lineStyle: {
                // color: '#c23531',
                //color: 'rgb(200, 35, 45)',
                opacity: 0.6,
                width: 1.4,
                curveness: 0.6
              },
              data: this.lines.slice(9, 18)
            },
            {
              type: 'lines',
              coordinateSystem: 'geo',
              lineStyle: {
                color: '#1fb1ff',
                opcity: 1,
                width: 0,
                curveness: 0.3
              },
              effect: {
                constantSpeed: 60,
                show: true,
                trailLength: 0.1,
                symbolSize: 2.5
              },
              zlevel: 15,
              data: this.lines.slice(9, 18)
            },
            {
              type: 'lines',
              coordinateSystem: 'geo',
              zlevel: 15,
              silent: true,
              lineStyle: {
                // color: '#c23531',
                //color: 'rgb(200, 35, 45)',
                opacity: 0.3,
                width: 1.4,
                curveness: -0.3
              },
              data: this.lines.slice(18, 28)
            },
            {
              type: 'lines',
              coordinateSystem: 'geo',
              lineStyle: {
                color: '#31ff83',
                opcity: 1,
                width: 0,
                curveness: -0.3
              },
              effect: {
                constantSpeed: 60,
                show: true,
                trailLength: 0.1,
                symbolSize: 2.5
              },
              zlevel: 15,
              data: this.lines.slice(18, 28)
            }
          ]
        }
        myChart.setOption(option)
        window.addEventListener("resize", function () {
          myChart.resize()
        })
        myChart.setOption(option)
      }
      this.$on('hook:destroyed', () => {
        window.removeEventListener("resize", function () {
          myChart.resize();
        });
      })
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
    this.initChart()
    this.tableScroll()
  }
}


</script>

<style scoped>
.main-body{
  height: 100%;
  width: 100%;
  display: flex;
  justify-content: space-around;
}
.chart {
  width: 45%;
  height: calc(100% - 30px);
  background-color: #1b1c21;
}
.table {
  width: 45%;
  height: calc(100% - 30px);
}
</style>
