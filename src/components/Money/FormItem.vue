<template>
    <div>
        <label class="formItem">
            <span class="name">{{this.filedName}}</span>
            <input type="text"
            v-model="value"
            :placeholder="this.placeholder">
        </label>
    </div>
</template>

<script lang="ts">
  import Vue from 'vue';
  import {Component, Prop, Watch} from 'vue-property-decorator';

  @Component
  export default class FormItem extends Vue {
    value = '';
    @Prop({required:true})filedName!:string
    @Prop()placeholder?:string
    @Watch('value')
    onValueChanged(value:string){
      this.$emit('update:value',value)
    }
    oninput(event: KeyboardEvent) {
      const input = event.target as HTMLInputElement;
      this.value = input.value;
    }

  }
</script>

<style lang="scss" scoped>
    @import "~@/assets/style/helper.scss";

    .formItem {
        font-size: 14px;
        padding-left: 16px;
        display: flex;
        align-items: center;

        .name {
            padding-right: 16px;
        }

        input {
            height: 40px;
            border: none;
            background: transparent;
            padding-right: 16px;
            flex-grow: 1;
        }
    }
</style>