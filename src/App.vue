<template>
    <div id="app">
        <router-view></router-view>
    </div>
</template>

<style lang="less">
html {
    font-size: calc(100vw / 1519);
    // font-size: 16px;
    // overflow: hidden;
    body {
        padding: 0;
        margin: 0;
        // max-width: 99999px;
        // max-height: 99999px;
        // * {
        //     max-width: 99999px;
        //     max-height: 99999px;
        // }
    }
}
@media only screen and (max-width: 701px) {
    html {
        font-size: calc(750px / 1519);
    }
}
</style>
