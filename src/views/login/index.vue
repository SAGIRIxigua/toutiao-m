<template>
  <div class="login-container">
   <el-form ref="form" :model="user"  class="login-form">
        <el-form-item >
            <el-input v-model="user.mobile" placeholder="请输入手机号"></el-input>
        </el-form-item>
        <el-form-item >
            <el-input v-model="user.code" placeholder="验证码"></el-input>
        </el-form-item>
        <el-form-item >
            <el-checkbox v-model="checked">我已阅读并且同意条款</el-checkbox>
        </el-form-item>
        <el-form-item>
            <el-button type="primary" @click="onLogin" class="login-btn" :loading="loginLoading">立即创建</el-button>
        </el-form-item>

   </el-form>
 </div>
</template>

<script>
import request from '@/util/request'
export default {
  name: 'LoginIndex',
  data () {
    return {
      user: {
        moblie: '',
        code: ''

      },
      checked: false,
      loginLoading: false
    }
  },
  methods: {
    onLogin () {
      const user = this.user
      this.loginLoading = true

      request({
        method: 'POST',
        url: '/mp/v1_0/authorizations',
        data: user
      }).then(res => {
        console.log(res)
        // 登录成功提示
        this.$message({
          message: '登录成功',
          type: 'success'
        })
        this.loginLoading = false
      }).catch(err => {
        console.log('登录失败', err)
        // 登录失败
        this.$message({
          message: '登录失败',
          type: 'error'
        })
        this.loginLoading = false
      })
    }
  }

}
</script>

<style lang="less">
  .login-container{
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    background: url("./background-login.jpg") no-repeat;
    background-size: cover;
    .login-form{
      background-color: #fff;
      padding: 50px;
      min-width: 300px;
      .login-btn{
        width: 100%;
      }
    }
  }
</style>
