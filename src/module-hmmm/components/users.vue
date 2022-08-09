<template>
  <div>
    <el-card style="margin: 20px">
      <template>
        <el-form style="display: flex">
          <el-form-item style="flex-grow: 1">
            <el-input
              v-model="input"
              placeholder="根据用户名搜索"
              style="width: 240px; height: 10px"
            ></el-input>
            <el-button style="margin-left: 10px">清空</el-button>
            <el-button type="primary">搜索</el-button>
            <el-button style="float: right" type="success" @click="showDialog"
              ><i class="el-icon-edit"></i>新增用户</el-button
            >
          </el-form-item>
        </el-form>
        <el-alert type="info" show-icon :closable="false"
          >共 {{ tableData.length }} 条记录
        </el-alert>
        <el-table
          :data="tableData"
          style="width: 100%"
          :row-class-name="tableRowClassName"
        >
          <el-table-column label="序号" prop="id"> </el-table-column>
          <el-table-column label="邮箱" prop="email"> </el-table-column>
          <el-table-column label="联系电话" prop="phone"> </el-table-column>
          <el-table-column label="用户名" prop="username"> </el-table-column>
          <el-table-column label="权限组名称" prop="permission_group_title">
          </el-table-column>
          <el-table-column label="角色" prop="role"> </el-table-column>
          <el-table-column label="操作">
            <el-button type="primary" icon="el-icon-edit" circle></el-button>
          </el-table-column>
        </el-table>
      </template>
    </el-card>
    <template>
      <el-dialog title="新增用户" :visible.sync="dialogVisible" width="30%">
        <el-form :model="upuser">
          <el-form-item label="用户名">
            <el-input v-model="upuser.username"></el-input>
          </el-form-item>
          <el-form-item label="邮箱">
            <el-input v-model="upuser.email"></el-input> </el-form-item
          ><el-form-item label="密码">
            <el-input v-model="upuser.password"></el-input> </el-form-item
          ><el-form-item label="角色">
            <el-input v-model="upuser.role"></el-input> </el-form-item
          ><el-form-item label="权限组名称">
            <el-select
              placeholder="请选择"
              v-model="upuser.permission_group_title"
            >
              <el-option
                v-for="item in tempGroupTitle"
                :key="item.id"
                :label="item.title"
                :value="item.title"
                @click="save"
              ></el-option>
            </el-select> </el-form-item
          ><el-form-item label="联系电话">
            <el-input v-model="upuser.phone"></el-input> </el-form-item
          ><el-form-item label="介绍">
            <el-input
              type="textarea"
              :rows="2"
              placeholder="请输入内容"
              v-model="upuser.introduction"
            >
            </el-input>
          </el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="dialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="save">确 定</el-button>
        </span>
      </el-dialog>
    </template>
  </div>
</template>

<script>
import { permissionsList } from '@/api/base/permissions'
import { list } from '@/api/base/users'
export default {
  data () {
    return {
      input: '',
      userinfo: [],
      tableData: [],
      dialogVisible: false,
      tempGroupTitle: [], // 接收权限组
      upuser: {
        avatar: '', // 头像
        create_time: '', // 创建时间
        email: '', // 电子邮箱
        id: '', // 用户id
        introduction: '', // 介绍
        is_deleted: '', //
        last_update_time: '', // 最近一次更新时间
        permission_group_id: '', // 权限组ID
        permission_group_title: '', // 权限组名称
        phone: '', // 电话号码
        role: '', // 角色
        username: '' // 用户名

      }
    }
  },
  created () {
    this.list()
    this.detail()
  },
  methods: {
    tableRowClassName ({ row, rowIndex }) {
      if (rowIndex === 1) {
        return 'warning-row'
      } else if (rowIndex === 3) {
        return 'success-row'
      }
      return ''
    },
    async list () {
      const res = await list(this.id)
      console.log('获取已有数据')
      console.log(res)
      this.tableData = res.data.list
    },
    async detail () {
      const res1 = await permissionsList(this.id)
      console.log(res1)
      this.tempGroupTitle = res1.data.list
    },
    showDialog () {
      this.dialogVisible = true
    },
    AddUsers () {
      this.dialogVisible = false
    },
    save () {
      this.upuser.create_time = Date()
      console.log(this.upuser)
    }

  },
  computed: {},
  watch: {},
  filters: {},
  components: {}
}
</script>

<style scoped lang='less'>
.el-alert {
  width: unset;
  ::v-deep .el-icon-info {
    font-size: 16px;
    width: 16px;
    list-style: 16px;
  }
  ::v-deep .el-alert__description {
    font-size: 14px;
    line-height: 14px;
    margin-top: 0;
  }
}
.el-table {
  .el-button {
    color: #409eff;
    background: #ecf5ff;
    border-color: #b3d8ff;
  }
  .el-button:hover {
    background: #409eff;
    border-color: #409eff;
    color: #fff;
  }
}
</style>
