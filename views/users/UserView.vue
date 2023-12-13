<template>
  <div>
    <div>
      <el-input v-model="params.name" placeholder="输入用户名" clearable @keyup.enter="findBySearch()" style="width: 150px; margin-left: 20px; margin-top: 20px;">
        <i
            slot="prefix"
            class="el-input__icon el-icon-search"
            style="cursor: pointer"
            @click="findBySearch()"
        ></i>
      </el-input>
      <el-input v-model="params.phone" placeholder="输入手机号" clearable @keyup.enter="findBySearch()" style="width: 150px; margin-left: 10px; margin-top: 20px;">
        <i
            slot="prefix"
            class="el-input__icon el-icon-search"
            style="cursor: pointer"
            @click="findBySearch()"
        ></i>
      </el-input>
      <el-input v-model="params.email" placeholder="输入邮箱" clearable @keyup.enter="findBySearch()" style="width: 150px; margin-left: 10px; margin-top: 20px;">
        <i
            slot="prefix"
            class="el-input__icon el-icon-search"
            style="cursor: pointer"
            @click="findBySearch()"
        ></i>
      </el-input>
      <el-button type="warning" style="margin-top: 20px; margin-left: 20px;" @click="findBySearch()">查询</el-button>
      <el-button type="danger" style="margin-top: 20px; margin-left: 20px;" @click="reset()">清空查询</el-button>
      <el-button type="warning" @click="add()" style="display: flex; float: right; margin-top: 20px; margin-right: 40px;">+添加用户</el-button>
    </div>

    <el-table :data="tableData" style="width: 100%" :default-sort="{ prop: 'uid', order: 'descending' }">
      <el-table-column prop="uid" label="用户UID" width="100"></el-table-column>

      <el-table-column prop="username" label="账号" width="200"></el-table-column>

      <el-table-column prop="name" label="用户名" width="175"></el-table-column>

      <el-table-column prop="sex" label="性别" width="100"></el-table-column>

      <el-table-column prop="birthday" label="生日" width="150"></el-table-column>

      <el-table-column prop="phone" label="手机号" width="175"></el-table-column>

      <el-table-column prop="email" label="邮箱"></el-table-column>

      <!--操作-->
      <el-table-column fixed="right" label="操作" width="100">
          <el-button @click="edit(scope.row.uid)" type="text" size="small">编辑</el-button>
          <el-popconfirm title="确定删除该用户？" @confirm="del(scope.row.uid)">
            <el-button slot="reference"  style="color:red; margin-left:10px; font-size: 12px;" type="text" >删除</el-button>
          </el-popconfirm>
      </el-table-column>
    </el-table>

    <!--分页查询-->
    <div style="display: flex; justify-content: center; align-items: center; margin-top: 40px; padding-bottom: 40px;">
      <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="params.pageNum"
          :page-sizes="[5, 10, 15, 20]"
          :page-size="params.pageSize"
          layout="total, sizes, prev, pager, next, jumper"
          :total="total">
      </el-pagination>
    </div>

      <div>
        <el-dialog title="编辑用户信息" :visible.sync="dialogFormVisible" width="60%">
          <el-form :model="form">
            <el-form-item label="账号">
              <el-input placeholder="请输入账号" v-model="form.username" clearable style="display: inline-block; width: 40%; margin-left: 22px;"></el-input>
            </el-form-item>
            <el-form-item label="用户名">
              <el-input placeholder="请输入用户名" v-model="form.name" clearable style="display: inline-block; width: 40%; margin-left: 10px;"></el-input>
            </el-form-item>
            <el-form-item label="生日">
              <el-date-picker v-model="form.birthday" type="date" placeholder="选择日期" style="display: inline-block; width: 40%; margin-left: 22px;"></el-date-picker>
            </el-form-item>
            <el-form-item label="性别">
              <el-select v-model="form.sex" style="display: inline-block; width: 15%; margin-left: 22px;">
                <el-option label="男" value="男"></el-option>
                <el-option label="女" value="女"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="手机号">
              <el-input placeholder="请输入手机号" v-model="form.phone" clearable style="display: inline-block; width: 40%; margin-left: 10px;"></el-input>
            </el-form-item>
            <el-form-item label="邮箱">
              <el-input placeholder="请输入邮箱" v-model="form.email" clearable style="display: inline-block; width: 40%; margin-left: 22px;"></el-input>
            </el-form-item>
          </el-form>
          <div slot="footer" class="dialog-footer" style="text-align: center">
            <el-button @click="dialogFormVisible = false">取 消</el-button>
            <el-button type="success" @click="submit()">确 定</el-button>
          </div>
        </el-dialog>
      </div>

    <div>
      <el-dialog title="添加用户" :visible.sync="dialogFormVisible_add" width="60%">
        <el-form :model="form_add">
          <el-form-item label="账号">
            <el-input placeholder="请输入账号" v-model="form_add.username" clearable style="display: inline-block; width: 40%; margin-left: 22px;"></el-input>
          </el-form-item>
          <el-form-item label="用户名">
            <el-input placeholder="请输入用户名" v-model="form_add.name" clearable style="display: inline-block; width: 40%; margin-left: 10px;"></el-input>
          </el-form-item>
          <el-form-item label="生日">
            <el-date-picker v-model="form_add.birthday" type="date" placeholder="选择日期" style="display: inline-block; width: 40%; margin-left: 22px;"></el-date-picker>
          </el-form-item>
          <el-form-item label="性别">
            <el-select v-model="form_add.sex" style="display: inline-block; width: 15%; margin-left: 22px;">
              <el-option label="男" value="男"></el-option>
              <el-option label="女" value="女"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="手机号">
            <el-input placeholder="请输入手机号" v-model="form_add.phone" clearable style="display: inline-block; width: 40%; margin-left: 10px;"></el-input>
          </el-form-item>
          <el-form-item label="邮箱">
            <el-input placeholder="请输入邮箱" v-model="form_add.email" clearable style="display: inline-block; width: 40%; margin-left: 22px;"></el-input>
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer" style="text-align: center">
          <el-button @click="dialogFormVisible_add = false">取 消</el-button>
          <el-button type="success" @click="submit_add()">确 定</el-button>
        </div>
      </el-dialog>
    </div>

  </div>
</template>

<script>
import request from '@/utils/request'
export default {
  name: "UserView",
  data() {
    return {
      //用户数据
      params: {
        uid: null,
        username: '',
        name: '',
        phone: '',
        email: '',
        pageNum: 1,
        pageSize: 5,
      },
      // 总数据数
      total: 0,

      //表格数据
      tableData: [],

      //对话框
      dialogFormVisible: false,
      dialogFormVisible_add: false,
      dialogFormVisible_del: false,

      form: {
        uid: null,
        username: '',
        name: '',
        birthday: '',
        sex: '',
        phone: '',
        email: ''
      },
      //添加用户的表单
      form_add: {
        uid: null,
        username: '',
        password: null,
        name: '',
        birthday: '',
        sex: '',
        phone: '',
        email: ''
      },
    }
  },
  //页面加载的时候干一些事情
  created() {
    this.findBySearch();
  },
  //将js方法放着里面
  methods: {
    findBySearch(){
      request.get("/user/search",{
        params: this.params
      }).then(res =>{
        if(res.code === '1'){
          this.tableData = res.data.list;
          this.total = res.data.total;
        }else{
          this.$message.error('获取用户信息失败');
        }
      })
    },
    //将页面重置
    reset(){
      this.params = {
        username: '',
        name: '',
        phone: '',
        email: '',
        pageNum: 1,
        pageSize: 5,
      }
      this.findBySearch();
    },
    //每页显示数据的条数
    handleSizeChange(pageSize){
      this.params.pageSize = pageSize;
      this.findBySearch();
    },
    //切换当前显示的页数
    handleCurrentChange(pageNum){
      this.params.pageNum = pageNum;
      this.findBySearch();
    },
    //编辑用户信息
    edit(uid) {
      // alert(this.params.uid)
      // 调用获取用户信息的接口
      request.get("/user/" + uid).then(res => {
        if (res.code === '1') {
          // 将获取到的用户信息填写到form
          this.form = res.data;
        } else {
          this.$message.error('获取用户信息失败');
        }
      });
      this.dialogFormVisible =  true;
    },
    //提交用户信息
    submit(){
      request.post("/user/edit",this.form).then(res =>{
        if(res.code === '1'){
          this.$message({
            message: '用户信息修改成功',
            type: 'success'
          });
        }else{
          this.$message.error('用户信息修改失败');
        }
      })
      this.findBySearch()
      this.dialogFormVisible =  false;
    },

    //添加用户
    add(){
      this.dialogFormVisible_add =  true;
    },
    submit_add(){
      request.post("/user/add",this.form_add).then(res =>{
        if(res.code === '1'){
          this.$message({
            message: '用户添加成功',
            type: 'success'
          });
        }else{
          this.$message.error('用户添加失败');
        }
      });
      // 延迟0.5秒后再进行查询
      setTimeout(() => {
        // 在这里执行你的查询操作
        this.findBySearch()
      }, 500);
      this.dialogFormVisible_add =  false;
    },

    del(uid){
      if(uid === '1'){
        alert("不可删除老板账号！");
        this.dialogFormVisible_del =  false;
      }
      request.post("/user/del/" + uid).then(res => {
        if(res.code === '1'){
          this.$message({
            message: '用户删除成功',
            type: 'warning'
          })
        }else{
          this.$message.error('用户删除失败！');
        }
      })
      // 延迟0.5秒后再进行查询
      setTimeout(() => {
        // 在这里执行你的查询操作
        this.findBySearch()
      }, 500);
    },

  }
}
</script>
