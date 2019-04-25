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
        <a slot="actions" @click="item.actions.callback">{{ item.actions.title }}</a>
      </template>
    </a-list-item>
    <PasswordModal ref="passwordmodal" @ok="passwordModalOk"></PasswordModal>
    <user-modal ref="userModalForm" @ok="userModalFormOk"></user-modal>
  </a-list>

</template>

<script>

  import PasswordModal from './PasswordModal'
  import UserModal from './UserModal'
  export default {
    components: {
      PasswordModal,
      UserModal
    },
    data () {
      return {
        data: [
          { title: '账户信息' , description: '可以对账户信息进行编辑', value: '', actions: { title: '修改', callback: () => { this.updateUserInfo(); } } },
          { title: '账户密码' , description: '请保证密码安全', value: '', actions: { title: '修改', callback: () => { this.handleChangePassword(); } } },
        ]
      }
    },
    methods:{
      handleChangePassword() {
        let userinfo = this.$store.getters.userInfo
        this.$refs.passwordmodal.show(userinfo.username);
      },
      passwordModalOk(){

      },
      updateUserInfo(){
        let userinfo = this.$store.getters.userInfo
        this.$refs.userModalForm.edit(userinfo);
        this.$refs.userModalForm.title = "编辑";
        this.$refs.userModalForm.disableSubmit = false;
      },
      userModalFormOk(){

      }
    }
  }
</script>

<style scoped>

</style>