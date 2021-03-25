<template>
<div class="qf-regist">
  <QfNavbar title="注册">
    <template>
      <span @touchstart='$router.replace("/login")'>登录</span>
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
    <van-field
      v-model="password2"
      type="password"
      name="密码"
      label="确认密码"
      placeholder="密码"
      :rules="[{ required: true, message: '请确认密码' }]"
    />
    <div style="margin: 16px;">
      <van-button round block type="info" native-type="submit">注册</van-button>
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
      password: '',
      password2: ''
    }
  },
  methods: {
    onSubmit() {
      const data = {
        username: this.username,
        password: this.password,
        password2: this.password2
      }
      this.$api.fetchRegist(data).then(res=>{
        console.log('注册', res)
        // 进一步根据res信息，判断用户是否真的注册成功
        if(res) {
          // 弹框提示注册成功
          this.$router.replace('/login')
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
</style>
