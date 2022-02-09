<template>
    <div class="maintitle">
        {{ title }}
    </div>
</template>

<script>
export default {
    name: "main-title",
    props: ["title"],
};
</script>

<style scoped>
.maintitle {
    font-size: 30px;
    font-weight: bold;
    display: block;
    height: 35.6px;
    /* width: 100%; */
    border-bottom: 1px solid rgb(160, 160, 160);
    margin-bottom: 20px;
}
@media only screen and (max-width: 1144px) {
    .maintitle {
        font-size: 22px;
        height: 25.7px;
    }
}
</style>
