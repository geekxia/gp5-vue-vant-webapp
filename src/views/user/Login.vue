<template>
<div class="qf-login">
  <QfNavbar title="登录">
    <template>
      <span @touchstart='$router.replace("/regist")'>注册</span>
    </template>
  </QfNavbar>
  <van-form @submit="onSubmit">
    <van-field
      v-model="username"
      name="用户名"
      label="用户名"
      placeholder="用户名"
      :rules="[{ required: true, message: '请填写用户名' }]"
    />
    <van-field
      v-model="password"
      type="password"
      name="密码"
      label="密码"
      placeholder="密码"
      :rules="[{ required: true, message: '请填写密码' }]"
    />
    <div style="margin: 16px;">
      <van-button round block type="info" native-type="submit">登录</van-button>
    </div>
  </van-form>
</div>
</template>

<script>
import { QfNavbar } from '@/components'
export default {
  components: {
    QfNavbar
  },
  data() {
    return {
      username: '',
      password: ''
    }
  },
  methods: {
    onSubmit() {
      // submit
      const data = {
        username: this.username,
        password: this.password
      }
      this.$api.fetchLogin(data).then(res=>{
        console.log('登录', res)
        // 存储token，给axios请求拦截器使用
        localStorage.setItem('token', res.token)
        // 登录成功，返回到上一页
        this.$router.back()
      })
    }
  }
}
</script>

<style lang="scss" scoped>
</style>
