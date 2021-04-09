<template>
  <!-- Material form login -->
  <form>
    <p class="h4 text-center mb-4">欢迎！</p>
    <div class="grey-text">
      <mdb-input label="用户名" icon="envelope" type="email"/>
      <mdb-input label="密码" icon="lock" type="password"/>
    </div>
    <div class="text-center">
      <mdb-btn>登录</mdb-btn>
    </div>
  </form>
  <!-- Material form login -->
</template>

<script>
  import { mdbInput, mdbBtn } from 'mdbvue';
  export default {
    name: 'Login',
    components: {
      mdbInput,
      mdbBtn
    },
  }
</script>

<style scoped>

</style>
