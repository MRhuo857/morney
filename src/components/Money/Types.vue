<template>
    <div>
        <ul class="types">
            <li class="selected">支出</li>
            <li class="selected">收入</li>
        </ul>
    </div>
</template>

<script lang="ts">
  export default {
    name: 'Types'
  };
</script>

<style lang="scss" scoped>
    @import "~@/assets/style/helper.scss";
    .types {
        font-size: 24px;
        display: flex;
        text-align: center;
        position: relative;
        background: $color-highlight;

        > li {
            width: 50%;
            height: 64px;
            display: flex;
            align-items: center;
            justify-content: center;

            &.selected::after {
                content: '';
                position: absolute;
                bottom: 0;
                left: 0;
                width: 50%;
                height: 4px;
                background: #333;
                color: #fff;
            }
        }
    }
</style>