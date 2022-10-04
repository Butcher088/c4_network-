<template>
 <d2-container>
   <div class="zd-container">
      <div class="button">
        <el-button @click="dialogFormVisible = true" type="primary" size="small">查询</el-button>
        <el-button @click="toggleSelection()" type="primary" size="small">取消选择</el-button>
      </div>
      <div class="table">
        <el-table
           ref="multipleTable"
          :data="tableData.slice((currentPage-1)*pageSize,currentPage*pageSize)"
          tooltip-effect="dark"
           @selection-change="handleSelectionChange">
          <el-table-column
            type="selection"
            width="55">
          </el-table-column>
          <el-table-column
            prop="date"
            label="数据包到达时间">
          </el-table-column>
          <el-table-column
            prop="ipFrom"
            label="源IP">
          </el-table-column>
          <el-table-column
            prop="ipTo"
            label="目的IP"
            show-overflow-tooltip>
          </el-table-column>
          <el-table-column
            prop="portFrom"
            label="源端口"
            show-overflow-tooltip>
          </el-table-column>
          <el-table-column
            prop="portTo"
            label="目的端口"
            show-overflow-tooltip>
          </el-table-column>
          <el-table-column
            prop="type"
            label="协议类型"
            show-overflow-tooltip>
          </el-table-column>
        </el-table>
      </div>
      <div class="pagination-block">
        <div class="pagination">
          <el-pagination
            background
            @current-change="handleCurrentChange"
            @size-change="handleSizeChange"
            :current-page="currentPage"
            :page-size="pageSize"
            :page-sizes="[5,10,15,20]"
            layout="total, sizes, prev, pager, next, jumper"
            :total="tableData.length">
          </el-pagination>
        </div>
      </div>
      <div class="dialog-form">
        <el-dialog title="条件查询" :visible.sync="dialogFormVisible">
          <el-form ref="form" :model="form" label-width="80px">
            <el-form-item label="时间"  style="width: 80%;">
              <div class="time-picker">
                <el-date-picker value-format="timestamp" type="date" placeholder="选择起始日期" v-model="form.date1" style="width: 40%;"></el-date-picker>
                <div style="width: 1%; margin: 0 5px">-</div>
                <el-date-picker value-format="timestamp" type="date" placeholder="选择结束日期" v-model="form.date2" style="width: 40%;"></el-date-picker>
              </div>
          </el-form-item>
            <el-form-item label="IP"  style="width: 80%;">
              <el-input v-model="form.ip" style="width: 40%;"></el-input>
            </el-form-item>
            <el-form-item label="Port"  style="width: 80%;">
              <el-input v-model="form.port" style="width: 40%;"></el-input>
            </el-form-item>
            <el-form-item>
              <el-button type="primary" @click="submit()">查询</el-button>
              <el-button @click="reset()">重置</el-button>
            </el-form-item>
          </el-form>
        </el-dialog>
      </div>
      <div class="dialog-table">
        <el-dialog title="查询结果" :visible.sync="resultForm" width="70%">
          <el-table :data="result" tooltip-effect="dark" height="500">
          <el-table-column
            prop="date"
            label="数据包到达时间">
          </el-table-column>
          <el-table-column
            prop="ipFrom"
            label="源IP">
          </el-table-column>
          <el-table-column
            prop="ipTo"
            label="目的IP"
            show-overflow-tooltip>
          </el-table-column>
          <el-table-column
            prop="portFrom"
            label="源端口"
            show-overflow-tooltip>
          </el-table-column>
          <el-table-column
            prop="portTo"
            label="目的端口"
            show-overflow-tooltip>
          </el-table-column>
          <el-table-column
            prop="type"
            label="协议类型"
            show-overflow-tooltip>
          </el-table-column>
        </el-table>
        </el-dialog>
      </div>

    </div>
  </d2-container>
</template>

<script>
  var date = {
        isDuringDate: function (beginDateStr, endDateStr) {
            var curDate = new Date(),
                beginDate = new Date(beginDateStr),
                endDate = new Date(endDateStr);
            if (curDate >= beginDate && curDate <= endDate) {
                return true;
            }
            return false;
        }
    }
export default {
  name: 'dataTable',
  data () {
    return {
      tableData: [
        {
        date: '2022-7-1 7:31:20',
        ipFrom: '172',
        ipTo: '172.105.113.34',
        portFrom: '20',
        portTo: '50132',
        type: 'TCP'
      },{
        date: '2020-5-1 7:31:20',
        ipFrom: '172.105.113.33',
        ipTo: '172.105.113.34',
        portFrom: '53',
        portTo: '50132',
        type: 'TCP'
      },
        {
          date: '2020-5-2 7:31:20',
          ipFrom: '172.105.113.33',
          ipTo: '172.105.113.34',
          portFrom: '53',
          portTo: '50132',
          type: 'TCP'
        },
        {
          date: '2020-5-3 7:31:20',
          ipFrom: '172.105.113.33',
          ipTo: '172.105.113.34',
          portFrom: '53',
          portTo: '50132',
          type: 'TCP'
        },
        {
          date: '2020-5-4 7:31:20',
          ipFrom: '172.105.113.33',
          ipTo: '172.105.113.34',
          portFrom: '53',
          portTo: '50132',
          type: 'TCP'
        },
        {
          date: '2020-5-5 7:31:20',
          ipFrom: '172.105.113.33',
          ipTo: '172.105.113.34',
          portFrom: '53',
          portTo: '50132',
          type: 'TCP'
        },
        {
          date: '2020-5-6 7:31:20',
          ipFrom: '172.105.113.33',
          ipTo: '172.105.113.34',
          portFrom: '53',
          portTo: '50132',
          type: 'TCP'
        },
        {
          date: '2020-5-2 7:31:20',
          ipFrom: '172.105.113.33',
          ipTo: '172.105.113.34',
          portFrom: '53',
          portTo: '50132',
          type: 'TCP'
        },
        {
          date: '2020-5-3 7:31:20',
          ipFrom: '172.105.113.33',
          ipTo: '172.105.113.34',
          portFrom: '53',
          portTo: '50132',
          type: 'TCP'
        },
        {
          date: '2020-5-4 7:31:20',
          ipFrom: '172.105.113.33',
          ipTo: '172.105.113.34',
          portFrom: '53',
          portTo: '50132',
          type: 'TCP'
        },
        {
          date: '2020-5-5 7:31:20',
          ipFrom: '172.105.113.33',
          ipTo: '172.105.113.34',
          portFrom: '53',
          portTo: '50132',
          type: 'TCP'
        },
        {
          date: '2020-5-6 7:31:20',
          ipFrom: '172.105.113.33',
          ipTo: '172.105.113.34',
          portFrom: '53',
          portTo: '50132',
          type: 'TCP'
        }],
      //多选与分页
      multipleSelection: [],
      currentPage: 1,
      pageSize: 5,
      //表单项
      form: {
        date1: '',
        date2: '',
        ip: '',
        port: ''
      },

      //dialog是否弹出
      dialogFormVisible: false,
      resultForm: false,

      //查询结果
      result: []
    }
  },

  methods: {
    //多选
     toggleSelection(rows) {
        if (rows) {
          rows.forEach(row => {
            this.$refs.multipleTable.toggleRowSelection(row);
          });
        } else {
          this.$refs.multipleTable.clearSelection();
        }
      },
     handleSelectionChange(val) {
        this.multipleSelection = val;
      },
    //分页
    handleCurrentChange(val){
      this.currentPage = val;
    },
    handleSizeChange(val) {
      this.pageSize = val
    },
    //查询方法
    submit(){
      this.dialogFormVisible = false
      let list = []
      let date1 = this.form.date1
      let date2 = this.form.date2

      if(date1>0  && date2>0 ) {
        this.tableData.forEach(function (item) {
            let date = new Date(item.date)
            date = date.getTime()
            if(date>=date1 && date<=date2){
              list.push(item)
            }
          }
        )
      }else{
        list = this.tableData
      }
      //console.log(list)
      let list1 = []
      let ip = this.form.ip
      if(ip !== ''){
        list.forEach(function (item) {
          if(item.ipFrom == ip){
            list1.push(item)
          }
        })
      }else{
        list1 = list
      }
      //console.log(list1)
      let list2 = []
      let port = this.form.port
      if(port !== ''){
        list1.forEach(function (item) {
          if(item.portTo == port){
            list2.push(item)
          }
        })
      }else{
        list2 = list1
      }
      //console.log(list2)
      this.result = list2
      this.resultForm = true

    },
    //重置方法
    reset(){
        this.form.date1 = ''
        this.form.date2 = ''
        this.form.ip = ''
        this.form.port = ''
      },
  },
}
</script>

<style scoped>
.zd-container{
  width: 100%;
  height: 90%;
}
.table{
  margin-top: 0.5rem;
}
.button{
  display: flex;
  justify-content: flex-end;
  margin-top: 0.5rem;
}
.pagination-block{
  margin-top: 0.5rem;
  display: flex;
  justify-content: flex-end;
}
.time-picker{
  display: flex;
  justify-content: flex-start;
}

</style>
