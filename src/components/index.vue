<template>
    <el-container class="conBoby">
        <el-header>
            <div>
                <i class="navclass el-icon-s-unfold" @click="hangleshownav"></i>
                <span>向日葵点餐系统</span>
            </div>
            <el-button type="warning" plain @click="handleback">退出登录</el-button>
        </el-header>
        <el-container class="conMain">
            <el-aside :class="isshow ? '' : 'el-aside-none'" width="200px">
                <el-col :span="12" width="200px">
                    <el-menu
                        default-active="1"
                        class="el-menu-vertical-demo"
                        @open="handleOpen"
                        @close="handleClose"
                        background-color="#545c64"
                        text-color="#fff"
                        active-text-color="#ffd04b"
                    >
                        <el-menu-item index="1" @click="tobaseInfo">
                            <i class="el-icon-menu"></i>
                            <span slot="title">基本信息</span>
                        </el-menu-item>
                        <el-menu-item index="2" @click="toindexImg">
                            <i class="el-icon-s-tools"></i>
                            <span slot="title">主页图片</span>
                        </el-menu-item>
                        <el-menu-item index="3" @click="togoodsInfo">
                            <i class="el-icon-s-goods"></i>
                            <span slot="title">菜品信息</span> </el-menu-item
                        ><el-menu-item index="4" @click="toaddGoods">
                            <i class="el-icon-plus"></i>
                            <span slot="title">添加菜品</span>
                        </el-menu-item>
                        <el-menu-item index="5" @click="toorders">
                            <i class="el-icon-document"></i>
                            <span slot="title">订单管理</span>
                        </el-menu-item>
                        <el-menu-item index="6" @click="toreserve">
                            <i class="el-icon-document"></i>
                            <span slot="title">预定管理</span>
                        </el-menu-item>
                    </el-menu>
                </el-col>
            </el-aside>
            <el-main>
                <router-view></router-view>
            </el-main>
            <aside class="right-aside">
                <div class="content" v-show="sideshow">
                    <img src="../assets/index3.jpg" alt="" />
                    <div>
                        <div class="kefu">客服</div>
                        <div class="fankui">反馈</div>
                    </div>
                </div>
                <div class="hide" @click="hangleshowside">{{ sideshow ? "hide" : "show" }}</div>
            </aside>
        </el-container>
    </el-container>
</template>

<script>
export default {
    data() {
        return {
            isshow: false,
            sideshow: true,
        };
    },

    methods: {
        hangleshownav() {
            this.isshow = !this.isshow;
        },
        hangleshowside() {
            this.sideshow = !this.sideshow;
        },
        //退出登陆
        handleback() {
            sessionStorage.setItem("token", "");
            this.$router.push("/login");
        },
        handleOpen(key, keyPath) {
            console.log(key, keyPath);
        },
        handleClose(key, keyPath) {
            console.log(key, keyPath);
        },
        tobaseInfo() {
            this.$router.push("/index/baseInfo");
            this.isshow = !this.isshow;
        },
        toindexImg() {
            this.$router.push("/index/indexImg");
            this.isshow = !this.isshow;
        },
        togoodsInfo() {
            this.$router.push("/index/goodsList");
            this.isshow = !this.isshow;
        },

        toorders() {
            this.$router.push("/index/orders");
            this.isshow = !this.isshow;
        },

        toaddGoods() {
            this.$router.push("/index/addGoods");
            this.isshow = !this.isshow;
        },
        toreserve() {
            this.$router.push("/index/reserve");
            this.isshow = !this.isshow;
        },
    },
};
</script>

<style lang="less" scoped>
@backcolor: #545c64;
.conBoby {
    display: flex;
    flex-direction: column;
    .el-header {
        width: 100%;
        position: relative;
        background-color: @backcolor;
        color: rgb(255, 255, 255);
        font-size: 20px;
        font-weight: 400;
        text-align: center;
        line-height: 60rem;
        display: flex;
        justify-content: space-between;
        align-items: center;
        border-bottom: 2rem #ffd04b solid;
        z-index: 100;
        overflow: hidden;
        .el-button {
            background-color: rgba(255, 255, 255, 0);
        }
        div {
            .navclass {
                display: none;
            }
        }
    }
    .conMain {
        display: flex;
        flex: 1;
        position: relative;
        .el-aside {
            position: relative;
            background-color: @backcolor;
            color: #333;
            text-align: center;
            line-height: 200rem;
            z-index: 103;
            width: 200rem;
            height: calc(100vh - 60px);
            overflow: hidden;
            .el-col {
                width: 100%;
                float: none;
            }
        }
        .el-main {
            flex: 1;
            height: calc(100vh - 60px);
            overflow-y: scroll;
        }
        .right-aside {
            z-index: 200;
            position: absolute;
            right: 17rem;
            top: calc(50vh - 200rem);
            .content {
                width: 200rem;
                height: 200rem;
                display: flex;
                flex-direction: column;
                background: #ffffff;
                // border: 1px solid #ffd04b;
                box-shadow: 0rem 0rem 20rem #c2c2c1;
                img {
                    width: 200rem;
                    height: 150rem;
                }
                div {
                    display: flex;
                    font-size: 16rem;
                    width: 200rem;
                    height: 50rem;
                    div {
                        width: 100rem;
                        display: flex;
                        align-items: center;
                        justify-content: center;
                        color: black;
                    }
                    .kefu {
                        border-right: 1px solid #ffd04b;
                        &:hover {
                            background: #ffcf4bb0;
                        }
                    }
                    .fankui {
                        &:hover {
                            background: #ffcf4bb0;
                        }
                    }
                }
            }
            .hide {
                cursor: default;
                position: absolute;
                right: 5rem;
                top: 5rem;
                border-radius: 50%;
                background: rgba(218, 216, 216, 0.568);
                color: #000000;
                width: 30rem;
                height: 30rem;
                font-size: 12rem;
                display: flex;
                align-items: center;
                justify-content: center;
                &:hover {
                    cursor: default;
                    background: white;
                }
            }
        }
    }
}

@media only screen and (max-width: 701px) {
    .conBoby {
        .el-header {
            div {
                .navclass {
                    display: inline-block;
                    margin-right: 10rem;
                }
            }
        }
        .conMain {
            .el-aside-none,
            .right-aside {
                display: none;
            }
        }
    }
}
</style>
