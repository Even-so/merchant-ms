<template>
    <div class="sign-upload">
        <el-upload
            action="http://120.76.52.65/phpsaomaserver/uploads/upload.php?action=update"
            list-type="picture-card"
            :on-preview="handlePictureCardPreview"
            :on-remove="handleRemove"
            :on-success="hangleSuccess"
            v-show="isshow"
            limit="1"
        >
            <i class="el-icon-plus"></i>
        </el-upload>
        <el-dialog :visible.sync="dialogVisible">
            <img width="100%" :src="dialogImageUrl" alt="" />
        </el-dialog>
    </div>
</template>

<script>
export default {
    name: "upload-img",
    // props: ["title",],
    data() {
        return {
            dialogImageUrl: "",
            dialogVisible: false,
            isshow: true,
        };
    },
    methods: {
        async handleRemove(file, fileList) {
            console.log(file, fileList);
            const { data: res } = await this.$http.get(
                "http://120.76.52.65/phpsaomaserver/upload.php?action=delete&&name=" + file
            );
            if (res) {
                this.isshow = !this.isshow;
            }
        },
        handlePictureCardPreview(file) {
            this.dialogImageUrl = file.url;
            this.dialogVisible = true;
        },
        hangleSuccess() {
            // this.isshow = !this.isshow;
        },
    },
};
</script>

<style scoped>
/* @media only screen and (max-width: 1144px) {
} */
</style>
