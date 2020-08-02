<template>
    <div>
        <label class="note">
            <span class="name">备注</span>
            <input type="text" placeholder="点击添加备注...">
        </label>
    </div>
</template>

<script lang="ts">
  export default {
    name: 'Note'
  };
</script>

<style lang="scss" scoped>
    @import "~@/assets/style/helper.scss";
    .note {
        font-size: 14px;
        background: #f5f5f5;
        padding-left: 16px;
        display: flex;
        align-items: center;

        .name {
            padding-right: 16px;
        }

        input {
            height: 64px;
            border: none;
            background: transparent;
            padding-right: 16px;
            flex-grow: 1;
        }
    }
</style>