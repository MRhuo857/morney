<template>
    <div class="tags">
        <div class="new">
            <button @click="createTag">新增按钮</button>
        </div>
        <UL class="current">
            <li v-for="tag in tagList" :key="tag.id"
                :class="{selected:selectedTags.indexOf(tag)>=0}"
                @click="toggle(tag)"> {{tag.name}}
            </li>
        </UL>

    </div>
</template>

<script lang="ts">
  import {Component} from 'vue-property-decorator';
  import {mixins} from 'vue-class-component';
  import TagHelper from '@/mixins/TagHelper';


  @Component

  export default class Tags extends mixins(TagHelper) {

    selectedTags: string[] = [];

    get tagList() {
      return this.$store.state.tagList;
    }

    created() {
      return this.$store.commit('fetchTags');
    }

    toggle(tag: string) {
      const index = this.selectedTags.indexOf(tag);
      if (index >= 0) {
        this.selectedTags.splice(index, 1);
      } else {
        this.selectedTags.push(tag);
      }
      this.$emit('update:value', this.selectedTags);
    }
  }
</script>

<style lang="scss" scoped>
    @import "~@/assets/style/helper.scss";

    .tags {
        background: white;
        font-size: 14px;
        padding: 16px;
        flex-grow: 1;
        display: flex;
        flex-direction: column-reverse;

        > .current {
            display: flex;
            flex-wrap: wrap;
            > li {
                background: #d9d9d9;
                height: 24px;
                line-height: 24px;
                border-radius: 6px;
                padding: 0 16px;
                margin-right: 12px;
                margin-top: 4px;
                box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
                &.selected {
                    background: $color-highlight;
                    color: white
                }
            }
        }

        > .new {
            padding-top: 16px;

            button {
                background: transparent;
                border: none;
                color: #999;
                border-bottom: 1px solid;
                padding: 0 4px;
            }

        }
    }
</style>