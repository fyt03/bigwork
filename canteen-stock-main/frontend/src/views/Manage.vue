<template>
    <el-container style="height: 100vh;">
      这是Manage组件
        <el-aside :width="sideWidth + 'px'" style="background-color: rgb(238, 241, 246); height: 100%;">
            <Aside :isCollapse="isCollapse" :logoTextShow="logoTextShow"/>
        </el-aside>

        <el-container>
            <el-header style="border-bottom: 1px solid #ccc;">
                <Header :collapseBtnClass="collapseBtnClass" :collapse="collapse" :user="user"/>
            </el-header>

            <el-main>
                <!--表示当前页面的子路由会在<router-view />里展示 -->
                <router-view @refreshUser="getUser"/>
            </el-main>
        </el-container>
    </el-container>
</template>

<script>
import Aside from "../components/Aside"
import Header from "../components/Header"

export default {
  name: 'Manage',
  data() {
    return {
      collapseBtnClass: 'el-icon-s-fold',
      isCollapse: false,
      sideWidth: 200,
      logoTextShow: true,
      user: {},
    }
  },
  components: {Aside, Header},
  created() {
    //从后台获取User数据
    this.getUser()
  },
  methods: {
    collapse() {  //点击收缩按钮触发
      this.isCollapse = !this.isCollapse
      if (this.isCollapse) { //收缩
        this.sideWidth = 64
        this.collapseBtnClass = 'el-icon-s-unfold'
        this.logoTextShow = false
      } else {              //展开
        this.collapseBtnClass = 'el-icon-s-fold'
        this.sideWidth = 200
        this.logoTextShow = true
      }
    },
    getUser() {
      let username = localStorage.getItem("user") ? JSON.parse(localStorage.getItem("user")).username : ""
      //从后台获取数据
      this.user = JSON.parse(localStorage.getItem("user"))
      console.log("Manage:", this.user);
      // this.Request.get("/user/username/" + username).then(res => {
      //   //重新赋值后台的最新User数据
      //   this.user = res.data
      // })
    }
  }
}
</script>

<style>

</style>
