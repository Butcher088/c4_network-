<template>
  <d2-container>
    <div class="card" v-for="item in cards" >
        <el-card class="box-card" shadow="hover">
        <div slot="header">
          <span class="title">{{item.title}}</span>
          <el-switch  v-model="item.active" active-color="#409EFF" @change="operate(item)"
                      inactive-color="#C0CCDA" style="float: right; padding: 3px 0" ></el-switch>
        </div>
        <div class="name">{{item.name}}</div>
        <div class="description">{{item.description}}</div>
        </el-card>
    </div>
  </d2-container>
</template>

<script>
//组件通信
import bus from '../bus'
export default {
  name: 'trafficScheduling',
  data(){
    return{
      cards: [
        {
          title: '方案一',
          name: '基于LSTM智能流量调度策略',
          description: '开启之后系统将自动适配当前园区网络状态，并是供最优的流量转发策略',
          active: true
        },
        {
          title: '方案二',
          name: '基于带宽的最优路径转发',
          description: '适用于视频直播业务场景',
          active: true
        },
        {
          title: '方案三',
          name: '基于链路质量实现的最短路径转发',
          description: '基于链铭质量实现的最短路径转发',
          active: true
        }
      ],

      //传递给日志页面的数据
      operation: []
    }
  },
  methods: {
    getTime(){
  　　let yy = new Date().getFullYear();
  　　let mm = new Date().getMonth()+1;
  　　let dd = new Date().getDate();
  　　let hh = new Date().getHours();
  　　let mf = new Date().getMinutes()<10 ? '0'+new Date().getMinutes() : new Date().getMinutes();
  　　let ss = new Date().getSeconds()<10 ? '0'+new Date().getSeconds() : new Date().getSeconds();
  　　let time = yy+'-'+mm+'-'+dd+' '+hh+':'+mf+':'+ss;
  　　return time
    },
    operate(item){
      let time  = this.getTime()
      if(item.active){
          //弹出提示
         this.$message({
          message: item.name+' 已启用',
          type: 'success'
        });
         //记录操作
         this.operation.unshift({
           title: '流量调度方案',
           name: item.name,
           operation: '启用成功！',
           time: time,
           type: 'success'

         })
      }else{
        //弹出提示
         this.$message({
          message: item.name+' 已停用',
        });
          //记录操作
         this.operation.unshift({
           title: '流量调度方案',
           name: item.name,
           operation: '停用成功！',
           time: time,
           type: 'primary'
         })
      }
    }
  },
  destroyed() {
     bus.$emit('operation', this.operation);
     console.log('传送')
  }
}

</script>

<style scoped>
.card{
  margin: 0 2rem 1rem ;
  height: 30%;
}
.box-card{
  height: 100%;
}
.title{
  font-weight: bolder;
  font-size: larger;
}
.name{
  font-weight: bold;
  font-size: large;
}
.description{
  margin-top: 1rem;
  color: #33a9ec;
}
</style>
