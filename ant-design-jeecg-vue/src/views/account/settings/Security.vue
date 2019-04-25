<template>
  <a-list
    itemLayout="horizontal"
    :dataSource="data"
  >
    <a-list-item slot="renderItem" slot-scope="item, index" :key="index">
      <a-list-item-meta>
        <a slot="title">{{ item.title }}</a>
        <span slot="description">
          <span class="security-list-description">{{ item.description }}</span>
          <span v-if="item.value"> : </span>
          <span class="security-list-value">{{ item.value }}</span>
        </span>
      </a-list-item-meta>
      <template v-if="item.actions">
        <a slot="actions" @click="handleChangePassword">修改</a>
      </template>
      <PasswordModal ref="passwordmodal" @ok="passwordModalOk"></PasswordModal>
    </a-list-item>
  </a-list>

</template>

<script>

  import PasswordModal from './PasswordModal'
  export default {
    components: {
      PasswordModal
    },
    data () {
      return {
        data: [
          { title: '账户密码' , description: '请保证密码安全', value: '', actions: { title: '修改', callback: () => { this.handleChangePassword('This is a normal message'); } } },

        ]
      }
    },
    methods:{
      handleChangePassword() {
        let userinfo = JSON.parse(localStorage.getItem('pro__Login_Userinfo'));
        console.info(userinfo.value.username);
        this.$refs.passwordmodal.show(userinfo.value.username);
      },
    }
  }
</script>

<style scoped>

</style>