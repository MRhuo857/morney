<template>
    <div>
        <ul class="types">
            <li :class="value === '-' && 'selected'"
                @click="selectType('-')">支出
            </li>
            <li :class="value === '+' && 'selected'"
                @click="selectType('+')">收入
            </li>
        </ul>
    </div>
</template>

<script lang="ts">
  import Vue from 'vue';
  import {Component, Prop} from 'vue-property-decorator';
  @Component
  export default class Types extends Vue {
    @Prop() readonly value!: string;
    selectType(type: string) {
      if (type !== '-' && type !== '+') {
        throw new Error('type is unknown');
      }
      this.$emit('update:value', type);
    }
  }
</script>
<style lang="scss" scoped>
    @import "~@/assets/style/helper.scss";

    .types {
        font-size: 24px;
        display: flex;
        text-align: center;
        background: $color-highlight;

        > li {
            width: 50%;
            height: 64px;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;

            &.selected::after {
                content: '';
                position: absolute;
                bottom: 0;
                left: 0;
                width: 100%;
                height: 4px;
                background: #333;
            }
        }
    }
</style>