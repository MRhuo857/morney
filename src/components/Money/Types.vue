<template>
    <div>
        <ul class="types">
            <li :class="type === '-' && 'selected'"
                @click="selectType('-')">支出
            </li>
            <li :class="type === '+' && 'selected'"
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
    type = '-';  //'-'代表支出，'+'代表收入
    @Prop(Number) xxx: number | undefined;
    //props 告诉Vue,xxx不是data,是prop
    // Number 告诉Vue, xxx运行时是个Number
    // xxx 是属性名
    // number | undefined 告诉TS,xxx的编译类型

    selectType(type: string) { //type只能是'+','-'中的一个
      if (type !== '-' && type !== '+') {
        throw new Error('type is unknown');
      }
      this.type = type;
    }
    mounted(){
      console.log(this.xxx);
    }
  }

  // export default {
  //     name: 'Types',
  //     data() {
  //         return {
  //             type: '-' //'-'代表支出，'+'代表收入
  //         }
  //     },
  //     methods: {
  //         selectType(type) { //type只能是'+','-'中的一个
  //             if (type !== '-' && type !== '+') {
  //                 throw new Error('type is unknown')
  //             }
  //             this.type = type
  //             console.log(type)
  //         }
  //     },
  // };
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