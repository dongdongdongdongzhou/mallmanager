<template>
  <div class="login-wrap">
    <el-form class="login-form" label-position="top" label-width="80px" :model="formData">
      <h2>用户登录</h2>
      <el-form-item label="姓名">
        <el-input v-model="formData.username"></el-input>
      </el-form-item>
      <el-form-item label="密码">
        <el-input v-model="formData.password"></el-input>
      </el-form-item>
      <el-button type="primary" @click="HandelLogin">登录</el-button>
    </el-form>
  </div>
</template>
<script>
export default {
  data () {
    return {
      formData: {
        username: '',
        password: ''
      }
    }
  },
  methods: {
    HandelLogin () {
      this.$http.post('login', this.formData).then(res => {
        // ES6对象解构赋值
        const {meta: {msg, status}} = res.data
        if (status === 200) {
          this.$message({
            message: '恭喜你，这是一条成功消息',
            type: 'success'
          })
          this.$router.push({name: 'Home'})
        } else {
          this.$message.error(msg)
        }
      })
    }
  }
}
</script>
<style lang="css">
    .login-wrap{
        height: 100%;
        width: 100%;
        background-color: #324152;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .login-wrap .login-form{
        width: 400px;
        background-color: white;
        padding: 20px 30px;
        border-radius: 5px;
    }
    button{
        width: 100%;
    }
</style>
