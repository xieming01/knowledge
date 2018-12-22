<template>
  <div>
    <div class="user-sculpture">
        <img src="https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=4244768030,2657343839&fm=173&app=25&f=JPEG?w=218&h=146&s=5EB605C50048874F1C89E51C0300C0D2" alt="">
    </div>
    <form class="mui-input-group">
      <div class="mui-input-row">
        <label>用户名</label>
        <input type="text" class="mui-input-clear" placeholder="请输入用户名">
      </div>
      <div class="mui-input-row">
        <label>密码</label>
        <input type="password" class="mui-input-password" placeholder="请输入密码">
      </div>

      <!-- <div class="mui-button-row"> -->
        <mt-button type="primary" class="login" size="large">登录</mt-button>
         <div class="subtitle">
           <router-link to="/member/register" tag="span" class="register">免费注册</router-link>
           <span>忘记密码</span>
         </div>
      <!-- </div> -->
    </form>
  </div>
</template>

<script>
export default {
  methods: {
    //  register(){
    //    this.$router.push('/member/register');
    //  },
     forgetPwd(){

     }
  },
  data() {
    return {
    };
  }
};
</script>

<style lang="scss" scoped>
.user-sculpture{
  height: 150px;
  width: 150px;
  border-radius: 50%;
  overflow: hidden;
  margin: 10px auto
}
.mui-input-group{
  padding:20px 10px 0px 10px;
  .mui-input-row{
    height: 40px;
    border: 1px solid #aaa;
    margin-bottom: 10px;
  }
.login{
  margin-top: 10px;
}

.subtitle{
  text-align: right;
  margin: 5px 5px 0 0;
  font-size: 15px;
  color: #aaa;

}
}
.mui-input-group:after{
  height:0px;
}
.mui-input-group:before{
  height: 0px;
}
</style>
