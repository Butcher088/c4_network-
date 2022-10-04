<template>
   <d2-container>
    <div class="zd-header">
      <el-row>
        <el-col span="6">
          <div class="header-part">
            <img src="./image/setting.png" class="icon"/>
            <div class="text">
              <div class="info">系统已运行</div>
              <div class="value">22天3小时20分1秒203毫秒</div>
            </div>
          </div>
        </el-col>
        <el-col span="6">
          <div class="header-part">
            <img src="./image/jiaohuanji.png" class="icon"/>
            <div class="text">
              <div class="info">已上线交换机</div>
              <div class="value">9台</div>
            </div>
          </div>
        </el-col>
        <el-col span="6">
          <div class="header-part">
            <img src="./image/luyouqi.png" class="icon"/>
            <div class="text">
              <div class="info">已上线路由器</div>
              <div class="value">0台</div>
            </div>
          </div>
        </el-col>
        <el-col span="6">
          <div class="header-part">
            <img src="./image/zhuji.png" class="icon"/>
            <div class="text">
              <div class="info">已上线主机</div>
              <div class="value">8台</div>
            </div>
          </div>
        </el-col>
      </el-row>
    </div>
     <div class="zd-body">
        <iframe class="iframe" src="/static/topology.html" name="iframe_a" frameborder="0" scrolling="no"></iframe>
        <div class="table">
          <el-table
          :data="tableData" height="100%" border stripe>
          <el-table-column
            prop="name"
            label="设备名称">
          </el-table-column>
          <el-table-column
            prop="address"
            label="MAC地址">
          </el-table-column>
        </el-table>
        </div>
     </div>
  </d2-container>
</template>

<script>

  export default {
    name: 'barChart',
    data(){
      return {
        topo: '../../../../public/static/topology.html',
        tableData: [
          {
            name: '测试',
            address: '未知'
          },
          {
            name: '测试',
            address: '未知'
          },
          {
            name: '测试',
            address: '未知'
          },{
            name: '测试',
            address: '未知'
          },{
            name: '测试',
            address: '未知'
          },{
            name: '测试',
            address: '未知'
          },{
            name: '测试',
            address: '未知'
          },{
            name: '测试',
            address: '未知'
          },{
            name: '测试',
            address: '未知'
          },{
            name: '测试',
            address: '未知'
          },
          {
            name: '测试',
            address: '未知'
          },
          {
            name: '测试',
            address: '未知'
          },
          {
            name: '测试',
            address: '未知'
          },{
            name: '测试',
            address: '未知'
          },{
            name: '测试',
            address: '未知'
          },{
            name: '测试',
            address: '未知'
          },{
            name: '测试',
            address: '未知'
          },{
            name: '测试',
            address: '未知'
          },{
            name: '测试',
            address: '未知'
          },{
            name: '测试',
            address: '未知'
          },
        ]
      }
    },
    methods: {

    },
    mounted() {
    }
  }
</script>

<style lang="scss" scoped>
.header-part{
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-self: center;
}
.header-part .text{
  align-self: center;
  margin-left: 15px;
}
.icon{
  height: 2.5rem;
  width: 2.5rem;
}
.zd-body{
  height: 80%;
  width: 100%;
  margin: 30px auto;
  display: flex;
  justify-content: space-around;
}
.iframe{
  width: 45%;
  height: calc(100% - 30px);
  border: 1px solid lightgray;
}
.table{
  width: 45%;
  height: calc(100% - 30px);
}
</style>
