<template>
  <div>
    <el-button type="primary" @click="showInvite = true">邀请新用户</el-button>
    <el-dialog title="邀请新用户" :visible.sync="showInvite">
      <el-form ref="inviteForm" :model="inviteInfo" :rules="rules">
        <el-form-item label="邮箱" prop="email">
          <el-input v-model="inviteInfo.email"></el-input>
        </el-form-item>
        <el-form-item label="电话号码" prop="phone">
          <el-input v-model="inviteInfo.phone"></el-input>
        </el-form-item>
        <el-form-item label="姓名" prop="name">
          <el-input v-model="inviteInfo.name"></el-input>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="showInvite = false">取消</el-button>
        <el-button type="primary" @click="submitInvite">确定</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      showInvite: false,
      inviteInfo: {
        email: '',
        phone: '',
        name: ''
      },
      rules: {
        // 自定义验证规则
        customRule: [
          { validator: this.validateInvite, trigger: 'submit' }
        ]
      }
    };
  },
  methods: {
    submitInvite() {
      this.$refs.inviteForm.validate((valid) => {
        if (valid) {
          this.sendInvite();
        } else {
          console.log('请至少填写邮箱、电话或姓名中的一项');
          return false;
        }
      });
    },
    sendInvite() {
      axios.post('/api/invite', this.inviteInfo)
          .then(response => {
            // 处理响应
            console.log(response);
            this.showInvite = false;
            this.resetForm();
          })
          .catch(error => {
            console.error(error);
          });
    },
    resetForm() {
      this.inviteInfo.email = '';
      this.inviteInfo.phone = '';
      this.inviteInfo.name = '';
    },
    validateInvite(rule, value, callback) {
      if (!this.inviteInfo.email && !this.inviteInfo.phone && !this.inviteInfo.name) {
        callback(new Error('请至少填写邮箱、电话或姓名中的一项'));
      } else {
        callback();
      }
    }
  }
};
</script>
