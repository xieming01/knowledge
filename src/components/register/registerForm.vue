<template>
    <div class="reister-container">
        <h3>请填写注册信息</h3>
        <div class="register-item" v-for="(item,i) in num" :key="i" >
            <div>
                
                <hr>
                <span class="register-title">{{item}}</span>
                <span><input type="text" label="用户名" placeholder="请输入用户名" v-model="username" class="register-input"></span>
            </div>
        </div>
         <hr>
                <span class="register-title">请上传头像</span>
                <span><input type="file"    class="register-input"></span>
        <mt-button type="primary" size="large" class="submit">提交</mt-button>
    </div>
</template>

<script>
export default {
    data(){
        return{
           username: '' ,
           email: '',
           password: '',
           phone: '',
           website: '',
           number: '',
           birthday: '',
           introduction: '',
           num:["用户名","邮箱","密码","手机号","自我介绍"]
        }
    },
    methods:{
        
    }
}
</script>

<style lang="scss" scoped>
    .reister-container{
        padding: 20px 10px 50px 10px;
       .register-input{
           display: inline-block;
           border: 0;
           width: 70%;
           margin-bottom: 0px;
       }
       .register-title{
           display: inline-block;
           width: 25%;
           color: #000
       }
       h3{
           text-align: center;
       }
       .submit{
           margin-top: 15px;
       }
           
    }
    
</style>
