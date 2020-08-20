<template>
    <ul class="tabs">
        <li v-for="item in dataSource" :key="item.value"
            :class="liClass(item)"
            @click="select(item)">{{item.text}}
        </li>
    </ul>
</template>

<script lang="ts">
  import Vue from 'vue';
  import {Component, Prop} from 'vue-property-decorator';

  type DataSource = { text: string, value: string }
  @Component
  export default class Tabs extends Vue {
    @Prop({required: true, type: Array})
    dataSource!: DataSource;
    @Prop(String) readonly value!: string;
    @Prop(String) classPrefix?: string;
    liClass = (item: DataSource) => {
      return {
        selected: item.value === this.value,
        [this.classPrefix + '-tabs-item']: this.classPrefix
      };

    };

    select(item: DataSource) {
      this.$emit('update:value', item.value);

    }
  }
</script>

<style lang="scss" scoped>
    @import "~@/assets/style/helper.scss";

    .tabs {
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