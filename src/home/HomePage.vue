<template>
    <div>
        <h1>你好！ {{account.user.firstName}}</h1>
<!--        <h1>你好!</h1>-->
        <p>欢迎来到图书管理系统</p>
        <h3>来自安全api端点的用户：</h3>
        <em v-if="users.loading">加载用户...</em>
        <span v-if="users.error" class="text-danger">错误: {{users.error}}</span>
        <ul v-if="users.items">
            <li v-for="user in users.items" :key="user.id">
                {{user.firstName + ' ' + user.lastName}}
                <span v-if="user.deleting"><em> - 删除...</em></span>
                <span v-else-if="user.deleteError" class="text-danger"> - 错误: {{user.deleteError}}</span>
                <span v-else> - <a @click="deleteUser(user.id)" class="text-danger">删除</a></span>
            </li>
        </ul>
        <p>
            <router-link to="/login">登出</router-link>
            <router-link to="/book-list">进入图书管理系统</router-link>
        </p>
    </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
  name: 'HomePage',
  computed: {
    ...mapState({
      account: state => state.account,
      users: state => state.users.all
    })
  },
  created () {
    this.getAllUsers()
  },
  methods: {
    ...mapActions('users', {
      getAllUsers: 'getAll',
      deleteUser: 'delete'
    })
  }
}
</script>
