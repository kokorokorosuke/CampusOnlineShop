<template>
  <div>
    <div>
      <el-input v-model="input" placeholder="搜索管理员" style="width: 200px; margin-left: 40px; margin-top: 20px;"></el-input>
      <el-button type="warning" style="display: flex; float: right; margin-top: 20px; margin-right: 40px;">+添加管理员</el-button>
    </div>
    <el-table :data="tableData" style="width: 100%">
      <el-table-column prop="username" label="账号" width="180"></el-table-column>

      <el-table-column prop="name" label="姓名" width="180"></el-table-column>

      <el-table-column prop="address" label="地址"></el-table-column>

      <el-table-column prop="phone" label="手机号"></el-table-column>

      <el-table-column prop="email" label="邮箱"></el-table-column>

      <!--操作-->
      <el-table-column fixed="right" label="操作" width="100">
        <template slot-scope="scope">
          <el-button @click="handleClick(scope.row)" type="text" size="small">查看</el-button>
          <el-button type="text" size="small">编辑</el-button>
        </template>
      </el-table-column>
    </el-table>

    <!--分页查询-->
    <div style="display: flex; justify-content: center; align-items: center; margin-top: 40px; padding-bottom: 40px;">
      <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="currentPage4"
          :page-sizes="[10, 20, 30, 40]"
          :page-size="10"
          layout="total, sizes, prev, pager, next, jumper"
          :total="400">
      </el-pagination>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input: '',
      tableData: [{
        username: 'laoliu01',
        name: '老六',
        address: '百色学院东合校区6栋211号',
        phone: '19976226636',
        email: '2507666370@qq.com'
      }]
    }
  }
}
</script>