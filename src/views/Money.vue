<template>
    <Layout class-prefix="layout">
        <NumberPad @update:value="onUpdateAmount" @submit="saveRecord"/>
        <div class="createdAt">
            <FormItem field-name="选择日期:"
                      type="date"
                      placeholder="在这里输入备注"
                      :value.sync="record.createdAt"
            />
        </div>
        <div class="notes">
            <FormItem field-name="备注:"
                      placeholder="在这里输入备注"
                      :value.sync="record.notes"
            />
        </div>
        <Tags @update:value="record.tags=$event"/>
        <Tabs :data-source="recordTypeList"
              :value.sync="record.type"/>
    </Layout>
</template>

<script lang="ts">
  import Vue from 'vue';
  import NumberPad from '@/components/Money/NumberPad.vue';
  import FormItem from '@/components/Money/FormItem.vue';
  import Tags from '@/components/Money/Tags.vue';
  import {Component} from 'vue-property-decorator';
  import recordTypeList from '@/constants/recordTypeList';
  import Tabs from '@/components/Tabs.vue';

  @Component({
    components: {Tabs, Tags, FormItem, NumberPad},
  })
  export default class Money extends Vue {
    get recordList() {
      return this.$store.state.recordList;
    }

    recordTypeList = recordTypeList;
    record: RecordItem = {
      tags: [], notes: '', amount: 0, type: '-',createdAt:new Date().toISOString()
    };
    onUpdateAmount(value: string) {
      this.record.amount = parseFloat(value);
    }

    saveRecord() {
      if (!this.record.tags || this.record.tags.length === 0) {
        return window.alert('请至少选择一个标签');
      }
      this.$store.commit('createRecord', this.record);
      if (this.$store.state.createRecordError === null) {
        window.alert('记账成功');
        this.record.notes = '';
      }

    }

  }
</script>

<style lang="scss">
    .layout-content {
        display: flex;
        flex-direction: column-reverse;
    }

    .notes {
        padding: 12px 0;
    }
</style>

<style lang="scss" scoped>
    @import "~@/assets/style/helper.scss";

</style>