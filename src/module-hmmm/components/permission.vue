<template>
  <el-card>
    <div class="top">
      <el-row class="top-left">
        <el-col :span="4">
          <el-input v-model="input" placeholder="请输入内容"></el-input>
        </el-col>
        <el-col :span="2" class="clear">
          <el-button>清除</el-button>
        </el-col>
        <el-col :span="2">
          <el-button type="primary">搜索</el-button>
        </el-col>
      </el-row>
      <el-row class="top-right" type="flex" justify="end">
        <el-col :span="3">
          <el-button type="success" icon="el-icon-edit">新增权限组</el-button>
        </el-col>
      </el-row>
    </div>
    <el-alert title="共4条记录" type="info" show-icon></el-alert>
    <template>
      <el-table :data="tableData" style="width: 100%">
        <el-table-column type="selection" width="60"></el-table-column>
        <el-table-column prop="date" label="用户名" min-width="100"></el-table-column>
        <el-table-column prop="name" label="日期" min-width="100"></el-table-column>
        <el-table-column prop="address" label="操作" width="120">
          <el-button type="primary" icon="el-icon-edit" circle></el-button>
          <el-button type="danger" icon="el-icon-delete" circle></el-button>
        </el-table-column>
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
  async created () {
    const res = this.$
    console.log(res)
  },
  data () {
    return {
      input: '',
      pagelist: [],
      tableData: [],
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
  .top {
    margin-top: 10px;
    display: flex;
    margin-bottom: 20px;
    .top-left {
      width: 50%;
      .clear {
        margin: 0 10px 0 10px;
      }
    }
    .top-right {
      margin-right: 30px;
      width: 50%;
    }
  }
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
