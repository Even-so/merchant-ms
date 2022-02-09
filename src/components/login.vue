<template>
    <div class="login">
        <div class="form">
            <h3 class="login-title">密码登录</h3>
            <div class="zhanghao">
                <input
                    id="zhanghao"
                    type="num"
                    v-model.trim="zhanghao"
                    placeholder="请输入手机号"
                />
            </div>
            <div class="password">
                <input
                    id="password"
                    type="password"
                    v-model.trim="password"
                    placeholder="请输入登陆密码"
                />
                <router-link class="retrievePwd" to="/retrievePwd">忘记密码</router-link>
            </div>
            <div class="button">
                <!-- <button type="button" class="submit" @click="submit">登陆</button> -->
                <el-button type="button" class="submit" :plain="true" @click="submit"
                    >登陆</el-button
                >
            </div>
            <div class="other">
                <router-link class="register" to="/register">注册</router-link>
            </div>
        </div>
        <div class="info">
            <div class="title">
                <span>向日葵点餐系统</span>
            </div>
            <div class="infotoken">
                <span class="infotoken1">我们提供</span>
                <span class="infotoken2">更简单</span>
                <span class="infotoken3">更简洁</span>
                <span class="infotoken4">的小程序点餐系统</span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            zhanghao: "",
            password: "",
            error: "",
        };
    },
    methods: {
        //登陆
        async submit() {
            let data = new URLSearchParams();
            data.append("telNumber", this.zhanghao);
            data.append("merchantPwd", this.password);
            const { data: res } = await this.$http.post("/merchant.php?action=login", data);
            if (res.code == 200) {
                sessionStorage.setItem("token", res.token);
                //页面main中的title
                sessionStorage.setItem("title", "基本信息");
                //路由跳转需要放在token值后面
                this.$router.push("/index");
                this.error = "登陆成功";
                this.$message({
                    message: this.error,
                    center: true,
                    type: "success",
                });
                // console.log(res.token);
            } else {
                if (res.code == 401) {
                    sessionStorage.setItem("token", "");
                    this.error = "密码错误";
                    this.$message({
                        message: this.error,
                        center: true,
                    });
                } else {
                    sessionStorage.setItem("token", "");
                    this.error = "该账号未注册";
                    this.$message({
                        message: this.error,
                        center: true,
                    });
                }
            }
        },
    },
};
</script>

<style lang="less" scoped>
.login {
    width: 100vw;
    height: 100vh;
    background-image: url(../assets/index3.jpg);
    background-position: center;
    -o-background-size: cover;
    background-size: cover;
    background-attachment: fixed;
    background-clip: border-box;
    display: -webkit-box;
    display: -webkit-flex;
    display: -moz-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: center;
    -webkit-align-items: center;
    -moz-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    -webkit-box-pack: center;
    -webkit-justify-content: center;
    -moz-box-pack: center;
    -ms-flex-pack: center;
    justify-content: center;
    position: relative;
    .form {
        width: 550rem;
        height: 520rem;
        background-color: rgba(255, 255, 255, 0.856);
        -webkit-box-shadow: 0rem 0rem 20rem rgba(100, 100, 100, 0.5);
        box-shadow: 0rem 0rem 20rem rgba(100, 100, 100, 0.5);
        padding: 50rem 56rem 60rem;
        -webkit-box-sizing: border-box;
        -moz-box-sizing: border-box;
        box-sizing: border-box;
        border-radius: 6rem;

        .login-title {
            font-weight: 500;
            font-size: 26rem;
            color: #323233;
            cursor: default;
        }
        .zhanghao {
            width: 438rem;
            height: 38.6rem;
            margin-bottom: 30rem;
            border-bottom: 2rem solid #bb8888;
            #zhanghao {
                padding: 10rem 10rem 10rem 10rem;
                background: none;
                outline: none;
                border: none;
                font-size: 16rem;
                width: 418rem;
                :focus {
                    border: none;
                }
            }
            input::-moz-placeholder {
                color: #989999;
                font-size: 16rem;
            }
        }
        .password {
            width: 438rem;
            height: 38.6rem;
            margin-bottom: 30rem;
            border-bottom: 2rem solid #bb8888;
            position: relative;
            #password {
                padding: 10rem;
                background: none;
                outline: none;
                border: none;
                width: 334rem;
                font-size: 16rem;
                :focus {
                    border: none;
                }
            }
            input::-moz-placeholder {
                color: #989999;
                font-size: 16rem;
            }
            a {
                text-decoration: none;
                color: #a67c51;
                position: absolute;
                right: 0;
                top: 50%;
                -webkit-transform: translateY(-50%);
                -moz-transform: translateY(-50%);
                -o-transform: translateY(-50%);
                transform: translateY(-50%);
                width: 84rem;
                font-size: 16rem;
                height: 14rem;
                line-height: 14rem;
                border-left: 1rem solid #bb8888;
                padding-left: 18rem;
                -webkit-box-sizing: border-box;
                -moz-box-sizing: border-box;
                box-sizing: border-box;
                white-space: nowrap;
                cursor: pointer;
            }
            /*正常的未被访问过的链接*/
            a:link {
                text-decoration: none;
            }
            /*已经访问过的链接*/
            a:visited {
                text-decoration: none;
            }
            /*鼠标划过(停留)的链接*/
            a:hover {
                text-decoration: none;
            }
            /* 正在点击的链接*/
            a:active {
                text-decoration: none;
            }
        }
        .submit {
            margin-top: 50rem;
            width: 438rem;
            height: 48rem;
            border-style: none;
            cursor: unset !important;
            pointer-events: unset;
            border-color: #ebedf0;
            background-color: #bb8888;
            border-radius: 20rem;
            font-size: 18rem;
            font-weight: 300;
            color: white;
        }
        button:hover {
            background-color: none;
        }
        .other {
            width: 438rem;
            height: 48rem;
            position: relative;
            a {
                text-align: right;
                text-decoration: none;
                color: #a67c51;
                position: absolute;
                right: 0;
                top: 50%;
                -webkit-transform: translateY(50%);
                -moz-transform: translateY(50%);
                -o-transform: translateY(50%);
                transform: translateY(50%);
                width: 84rem;
                font-size: 16rem;
                height: 14rem;
                line-height: 14rem;
                padding-left: 18rem;
                -webkit-box-sizing: border-box;
                -moz-box-sizing: border-box;
                box-sizing: border-box;
                white-space: nowrap;
                cursor: pointer;
            }
            /*正常的未被访问过的链接*/
            a:link {
                text-decoration: none;
            }
            /*已经访问过的链接*/
            a:visited {
                text-decoration: none;
            }
            /*鼠标划过(停留)的链接*/
            a:hover {
                text-decoration: none;
            }
            /* 正在点击的链接*/
            a:active {
                text-decoration: none;
            }
        }
    }
    .info {
        font-family: "FangSong", Courier, monospace;
        margin-left: 20rem;
        position: relative;
        width: 382rem;
        height: 520rem;
        border-radius: 6rem;
        background-color: rgba(255, 255, 255, 0.856);
        -webkit-box-shadow: 0rem 0rem 20rem rgba(100, 100, 100, 0.5);
        box-shadow: 0rem 0rem 20rem rgba(100, 100, 100, 0.5);
        .title {
            width: 382rem;
            height: auto;
            display: -webkit-box;
            display: -webkit-flex;
            display: -moz-box;
            display: -ms-flexbox;
            display: flex;
            -webkit-box-align: center;
            -webkit-align-items: center;
            -moz-box-align: center;
            -ms-flex-align: center;
            align-items: center;
            -webkit-box-pack: center;
            -webkit-justify-content: center;
            -moz-box-pack: center;
            -ms-flex-pack: center;
            justify-content: center;
            margin-top: 20rem;
            span {
                padding: 20rem;
                font-size: 30rem;
                font-weight: 400;
                border-bottom: 2rem solid #bb8888;
            }
        }
        .infotoken {
            font-size: 20rem;
            font-weight: 400;
            display: -webkit-box;
            display: -webkit-flex;
            display: -moz-box;
            display: -ms-flexbox;
            display: flex;
            -webkit-box-align: center;
            -webkit-align-items: center;
            -moz-box-align: center;
            -ms-flex-align: center;
            align-items: center;
            -webkit-box-pack: center;
            -webkit-justify-content: center;
            -moz-box-pack: center;
            -ms-flex-pack: center;
            justify-content: center;
            -webkit-box-orient: vertical;
            -webkit-box-direction: normal;
            -webkit-flex-direction: column;
            -moz-box-orient: vertical;
            -moz-box-direction: normal;
            -ms-flex-direction: column;
            flex-direction: column;
            margin-top: 100rem;
            background-image: url(../assets/logo.png);
            background-repeat: no-repeat;
            background-position: 130% 100%;
            -o-background-size: 40% auto;
            background-size: 40% auto;
            // .infotoken1 {
            //     // align-self: flex-start;
            //     // padding-left: 40rem;
            // }

            // .infotoken2 {
            //     // align-self: flex-start;
            //     // padding-left: 110rem;
            // }
        }
        .infotoken > span {
            margin-bottom: 20rem;
        }
    }
}
@media only screen and (max-width: 701px) {
    .login {
        // .form {
        //     -webkit-transform: scale(1.2, 1.2);
        //     -moz-transform: scale(1.2, 1.2);
        //     -o-transform: scale(1.2, 1.2);
        //     transform: scale(1.2, 1.2);
        // }
        .info {
            display: none;
        }
    }
}
</style>
