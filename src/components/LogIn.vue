<template>
<el-main>
    <el-row >

            <div class="login_container">
                <div class="login_box">
                <div class="avatar_box">
                    <img src="../assets/e.png" style="margin-top:3%">
                </div>
                <el-form label-width="0px" :model="form" class="login_in" ref="loginForm"  :rules="rules" >
                    <el-form-item prop="userName" >
                    <i class="el-icon-user"></i>

                    <el-input type="text" v-model="form.username" prefix-icon="el-icon-user" placeholder="请输入用户名" style="width:60%; margin:auto" ></el-input>
                    
                    </el-form-item>

                    <el-form-item prop="passWord" >
                    <el-input type="password" v-model="form.password" prefix-icon="el-icon-user" placeholder="请输入密码" style="width:60%; margin:auto"></el-input>
                    </el-form-item>

                    <el-form-item >
                    <el-select v-model="form.role"  placeholder="选择身份" style="width:30%; margin:auto">
                        <el-option label="用户" value="user" />
                        <el-option label="机构" value="company" />
                        <el-option label="管理员" value="manger" />
                        <el-option label="专家" value="expert" />

                    </el-select>
                    </el-form-item>
           

                    <el-form-item class="btns">
                    <el-button type="primary" @click = "logevent">登录</el-button>
                    <el-button type="primary" @click = "signup">注册</el-button>
                    </el-form-item>
                </el-form>
                </div>
            </div>



                <!-- <el-form label-width="0px" class="login_in">
                    <el-form-item prop="username">
                    <el-input type="text" prefix-icon="el-icon-user"></el-input>
                    </el-form-item>
                    <el-form-item prop="password">
                    <el-input type="password" prefix-icon="el-icon-thumb"></el-input>
                    </el-form-item>
                    <el-form-item class="btns">
                    <el-button type="primary">登录</el-button>
                    <el-button>重置</el-button>
                    </el-form-item>
                </el-form> -->
    </el-row>
</el-main>
</template>


<script>

    export default {
        name: "LogIn",
        data(){
            return {
                form: {
                    username: "",
                    password: "",
                    role: "user"
                },
            }
        },
        methods:{
            async logevent(){
                const ret = await this.$http.get('login.json')
                console.log(ret)
                console.log(this.form)
                if(ret.status == 200 ){
                    this.$message.success('登录成功');
                    if (this.form.role == "user"){
                        this.$router.push('/usersearch')
                    }
                    else if (this.form.role == "company"){
                        this.$router.push('/companyinfo')
                    }
                    else if (this.form.role == "manger"){
                        this.$router.push('/mangerorder')
                    }
                    else if (this.form.role == "expert"){
                        this.$router.push('/expertupload')
                    }
                    // this.$router.push({path :'/companyinfo',  query : { username: this.form.username, role: this.form.role, password: this.form.password}});
                    //this.$http.post('/companyinfo',{ username: this.form.username, role: this.form.role, password: this.form.password})
                }
                else{
                    this.$message.error('登录失败');
                }
                    },
            signup(){
                
                
                this.$router.push('/signup')
            }
    }
    }
</script>

<style scoped >
  .login_container {
    background-color: #42b983;
    height: 30%;
    margin-left: 35%;
    margin-top: 5%;
    width: 400px;
    height: 250px;
  }

  .login_box {
    width: 450px;
    height: 300px;
    background-color: #fff;
    border-radius: 3px;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    margin-left: 50%;
    margin-top: 30%;


  }

  .btns {
    display: flex;
    justify-content: flex-end;
    margin-left: 35%;

  }

  .login_in {
    position: absolute;
    bottom: 0;
    width: 100%;
    padding: 0 20px;
    box-sizing: border-box;
  }
</style>