<template>
    <div class="content">
        <div class="head">
            <main-title title="订单信息"></main-title>
            <el-button type="primary" size="small" @click="goback">返回</el-button>
        </div>
        <el-descriptions class="margin-top" title="" :column="2" :size="size">
            <el-descriptions-item label="订单编号"> {{ orderInfo.orderId }} </el-descriptions-item>
            <el-descriptions-item label="购买者"> {{ userName }} </el-descriptions-item>
            <el-descriptions-item label="桌号"> {{ orderInfo.tableNumber }} </el-descriptions-item>
            <el-descriptions-item label="取餐码"> {{ orderInfo.mealCode }} </el-descriptions-item>
            <el-descriptions-item label="支付时间">
                {{ orderInfo.paymentTime }}
            </el-descriptions-item>
            <el-descriptions-item label="支付状态">
                <el-tag size="small">{{
                    orderInfo.paymentStatus == 1 ? "已支付" : "未支付"
                }}</el-tag>
            </el-descriptions-item>
            <el-descriptions-item label="打包费"> {{ orderInfo.packingFee }} </el-descriptions-item>
            <el-descriptions-item label="支付金额"> {{ orderInfo.payPrice }} </el-descriptions-item>
            <el-descriptions-item label="备注"> {{ orderInfo.remarks }} </el-descriptions-item>
        </el-descriptions>
        <el-table
            :data="tableData"
            style="width: 100%"
            :header-cell-style="{ background: 'antiquewhite' }"
            :cell-style="{ 'text-align': 'center' }"
        >
            <el-table-column prop="img" label="图片" width="" align="center">
                <template #default="scope">
                    <div class="block">
                        <el-avatar
                            shape="square"
                            :size="50"
                            :src="imgUrl + scope.row.menuImg"
                        ></el-avatar>
                    </div>
                </template>
            </el-table-column>
            <el-table-column prop="dishName" label="菜名" width="" align="center">
            </el-table-column>
            <el-table-column prop="dishPrice" label="价格" width="" align="center">
            </el-table-column>
            <el-table-column prop="className" label="分类" width="" align="center">
            </el-table-column>
            <el-table-column prop="goodsNumber" label="数量" align="center"> </el-table-column>
        </el-table>
    </div>
</template>

<script>
export default {
    data() {
        return {
            goodsNumber: [],
            orderInfo: {},
            userName: "tao",
            tableData: [],
            size: "",
        };
    },
    methods: {
        goback() {
            this.$router.go(-1);
        },
    },
    created() {
        let row = JSON.parse(this.$route.query.row);
        this.orderInfo = row;
        //获取菜品信息
        let data = new URLSearchParams();
        data.append("purchasedGoods", row.purchasedGoods);
        this.$http.post("/menuLsit.php?action=readArr", data).then((res) => {
            this.tableData = res.data.dishList;
            for (let index = 0; index < res.data.dishList.length; index++) {
                var Number = this.orderInfo.goodsNumber.split(",");
                this.tableData[index].goodsNumber = Number[index];
            }
        });
        //获取支付者的名字
        let name = new URLSearchParams();
        name.append("userId", this.orderInfo.userId);
        this.$http.post("/users.php?action=readUserId", name).then((res) => {
            this.userName = res.data.user[0].nickName;
        });
    },
};
</script>

<style lang="less" scoped>
.content {
    display: flex;
    align-items: flex-start;
    flex-direction: column;
    .head {
        display: flex;
        justify-content: space-between;
        width: 100%;
        .el-button {
            height: 35.6px;
            font-size: 12px;
        }
    }
    .el-descriptions {
        margin-bottom: 50px;
    }
}
@media only screen and (max-width: 1144px) {
    .content {
        .head {
            .el-button {
                height: 25.7px;
                font-size: 9px;
            }
        }
    }
}
</style>
