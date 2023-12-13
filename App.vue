<template>
  <div id="app">
    <el-container>
      <!--侧边栏-->
      <el-aside style="overflow: hidden; min-height: 100vh; background-color: #545c64; width: 200px">
        <!--侧边标题-->
        <div style="display: flex;flex-direction: column; height: 100px; width: 200px;">
          <h style="color: white; font-size: 18px;margin-top: 40px; padding-left: 15px;">百院生活超市管理端</h>
        </div>
        <!--侧边导航-->
        <el-col :span="24">
          <el-menu
              :default-active="$route.path"
              router
              class="el-menu-vertical-demo"
              background-color="#545c64"
              text-color="#fff"
              active-text-color="#ffd04b">
            <el-menu-item index="/">
              <i class="el-icon-menu"></i>
              <span slot="title">系统首页</span>
            </el-menu-item>
            <el-submenu index="2">
              <template slot="title">
                <i class="el-icon-location"></i>
                <span>商品管理</span>
              </template>
              <el-menu-item-group>
                <el-menu-item index="2-1">选项1</el-menu-item>
                <el-menu-item index="2-2">选项2</el-menu-item>
              </el-menu-item-group>
            </el-submenu>
            <el-submenu index="3">
              <template slot="title">
                <i class="el-icon-location"></i>
                <span>订单管理</span>
              </template>
              <el-menu-item-group>
                <el-menu-item index="3-1">选项1</el-menu-item>
                <el-menu-item index="3-2">选项2</el-menu-item>
              </el-menu-item-group>
            </el-submenu>
            <el-submenu index="4">
              <template slot="title">
                <i class="el-icon-location"></i>
                <span>消息管理</span>
              </template>
              <el-menu-item-group>
                <el-menu-item index="4-1">选项1</el-menu-item>
                <el-menu-item index="4-2">选项2</el-menu-item>
              </el-menu-item-group>
            </el-submenu>
            <el-submenu index="5">
              <template slot="title">
                <i class="el-icon-location"></i>
                <span>用户管理</span>
              </template>
              <el-menu-item-group>
                <el-menu-item index="/admin">管理员信息</el-menu-item>
                <el-menu-item index="/user">用户信息</el-menu-item>
              </el-menu-item-group>
            </el-submenu>
            <el-menu-item index="/about">
              <i class="el-icon-setting"></i>
              <span slot="title">关于</span>
            </el-menu-item>
          </el-menu>
        </el-col>
      </el-aside>
      <!--侧边栏结束-->
      <el-container>
      <!--顶栏-->
      <el-header style="background-color: #ffffff;">
        <h1 style="margin-left: 5px;">牛逼</h1>
        <div style="float: right; width: 300px; height: 60px;">

        </div>
      </el-header>
      <!--顶栏结束-->

      <!--主体-->
      <el-main style="background-color: #f2f3f6;">
        <!--主题内容-->
        <div style="background-color: #ffffff;">
          <router-view/>
        </div>
      </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<style>
.el-menu{
  border-right: none !important;
}
</style>


