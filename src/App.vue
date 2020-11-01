<template>
    <div id="app">
        <router-view/>
    </div>
</template>

<style lang="scss">
    @import "~@/assets/style/reset.scss";
    @import "~@/assets/style/helper.scss";

    body {
        line-height: 1.5;
        font-family: $font-hei;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #333333;
        font-size: 16px;
        background: #f5f5f5;
    }
    #app{
        max-width: 500px;
        margin: 0 auto;
        box-shadow: 0 2px 2px rgb(0,0,0,0.5);
    }
</style>
