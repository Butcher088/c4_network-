<template>
  <d2-container>
   <div class="block">
      <el-timeline>
          <el-timeline-item  v-for="item in data" :timestamp="item.time" placement="top" :type="item.type" size="large">
          <el-card class="card">
            <div class="title">{{item.title}}</div>
            <div class="name">{{item.name}}</div>
            <div class="operation">{{item.operation}}</div>
          </el-card>
        </el-timeline-item>
      </el-timeline>
    </div>
  </d2-container>
</template>

<script>
import bus from '../bus'

export default {
  name: "logmanage",
  data(){
    return {
      data: []
    }
  },
  methods: {
    init(){
        var that = this
         bus.$on('operation', (data) => {
           that.data = data
           console.log(data)
          })
      console.log(this.data)
    }
  },
  created() {
    this.init()
  }
}
</script>

<style scoped>
.block{
  margin: 0 2rem;
}
.card{
  box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
}
.title{
  font-weight: bolder;
  font-size: large;
}
.name{
  font-weight: bold;
  font-size: larger;
  margin: 1rem 0 0.5rem;
}
.operation{
  color: #33a9ec;
  margin-bottom: 0.5rem;
}
</style>
