<template>
    <button class="button" @click="$emit('click',$event)">
        <slot/>
    </button>
</template>

<script lang="ts">
  export default {
    name: 'Button'
  };
</script>

<style lang="scss" scoped>
    .button {
        color: #333;
        background: #ffd514;
        border: none;
        height: 40px;
        padding: 0 16px;
        border-radius: 4px;

        &-wrapper {
            text-align: center;
            padding: 16px;
            margin-top: 44-16px;
        }
    }
</style>