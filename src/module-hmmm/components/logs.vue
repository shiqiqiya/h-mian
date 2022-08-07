<template>
  <el-card>
    <el-alert title="共4条记录" type="info" show-icon></el-alert>
    <template>
      <el-table :data="tableData" style="width: 100%">
        <el-table-column prop="date" label="操作类型" min-width="100"></el-table-column>
        <el-table-column prop="name" label="操作人" min-width="180"></el-table-column>
        <el-table-column prop="address" label="执行结果" min-width="294"></el-table-column>
        <el-table-column prop="dress" label="操作时间" min-width="130"></el-table-column>
        <el-table-column prop="addss" label="描述" min-width="80"></el-table-column>
      </el-table>
    </template>
    <div class="block">
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="currentPage4"
        :page-sizes="[100, 200, 300, 400]"
        :page-size="100"
        layout=" prev, pager, next, sizes, jumper"
        :total="400"
      ></el-pagination>
    </div>
  </el-card>
</template>

<script>
export default {
  created () { },
  data () {
    return {
      tableData: [{
        date: '2016-05-02',
        name: '王小虎',
        address: ' 1518 弄'
      }, {
        date: '2016-05-04',
        name: '王小虎',
        address: ' 1517 弄'
      }, {
        date: '2016-05-01',
        name: '王小虎',
        address: ' 1519 弄'
      }, {
        date: '2016-05-03',
        name: '王小虎',
        address: ' 1516 弄'
      }],
      currentPage4: 4
    }
  },
  methods: {
    handleSizeChange (val) {
      console.log(`每页 ${val} 条`)
    },
    handleCurrentChange (val) {
      console.log(`当前页: ${val}`)
    }
  },
  computed: {},
  watch: {},
  filters: {},
  components: {}
}
</script>

<style scoped lang='less'>
.el-card {
  margin: 0 10px 20px 10px;
  .el-alert {
    margin-bottom: 10px;
  }
  .el-table {
    margin-bottom: 20px;
  }
  .block {
    display: flex;
    justify-content: end;
  }
}
</style>
