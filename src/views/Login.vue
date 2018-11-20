<template>
  <div>
      <div class="login-wrap">
        <div class="lgnheader">
          <em class="milogo">
              <img src="/static/huawei-logo.png">
          </em>
          <h4 class="header-tit-txt">华为帐号登录</h4>
        </div>
        <div class="login-form">
          <label for="" class="labelbox">
            <input class="item-account" type="text" name="user" autocomplete="off" placeholder="邮箱/手机号码" v-model="userName">
          </label>
          <label for="" class="labelbox">
            <input class="item-account" type="password" name="password" autocomplete="off" placeholder="密码" v-model="password">
            <div class="eye-wrap">
              <i class="icon iconfont icon-yanjing"></i>
            </div>
          </label>
        </div>
        <div class="btn-login-wrap">
          <input type="button" class="btn-login" value="登录" @click="login">
        </div>
        <div class="btn-back-wrap">
          <input type="button" class="btn-back" value="返回" @click="back">
        </div>
      </div>
  </div>
</template>

<script>
import '@/assets/css/reset.css'
import '@/assets/css/login.css'
import { MessageBox } from 'mint-ui'
import axios from 'axios'
export default {
  data(){
    return {
      userName: '',
      password: ''
    }
  },
  methods: {
    login(){
      axios.get('/static/mock/User.json').then(result=>{
        var res = result.data;
        if(this.userName == res.userName && this.password == res.password){
          // 本地localStorage存储用户信息
          localStorage.setItem('userId', '0001');

          this.$router.push({path: 'user'});
        }else{
          MessageBox.alert('用户名或者密码错误！', '提示');
        }
      });
    },
    back(){
      this.$router.push({path: 'user'});
    }
  }
}
</script>

