<template>
    <Layout class-prefix="layout">
        {{record}}
        <NumberPad @update:value="onUpdateAmount" @submit="saveRecord"/>
        <Note @update:value="onUpdateNotes"/>
        <Tags :data-source.sync="tags" @update:value="onUpdateTags"/>
        <Types @update:value="onUpdateType"/>
    </Layout>
</template>

<script lang="ts">
  import Vue from 'vue';
  import NumberPad from '@/components/Money/NumberPad.vue';
  import Note from '@/components/Money/Note.vue';
  import Tags from '@/components/Money/Tags.vue';
  import Types from '@/components/Money/Types.vue';
  import {Component, Watch} from 'vue-property-decorator';
  import {model} from '@/model';

  const recordList = model.fetch();

  @Component({
    components: {Types, Tags, Note, NumberPad},
  })
  export default class Money extends Vue {
    tags = ['衣', '食', '住', '行', '吃'];
    recordList: RecordItem[] = recordList;
    record: RecordItem = {
      tags: [], notes: '', amount: 0, type: '-'
    };

    onUpdateTags(value: string[]) {
      this.record.tags = value;
    }

    onUpdateNotes(value: string) {
      this.record.notes = value;
    }

    onUpdateType(value: string) {
      this.record.type = value;
    }

    onUpdateAmount(value: string) {
      this.record.amount = parseFloat(value);
    }

    saveRecord() {
      const record2: RecordItem = model.clone(this.record);
      record2.createdAt = new Date();
      this.recordList.push(record2);
      console.log(this.recordList);
    }

    @Watch('recordList')
    onRecordListChange() {
      model.save(this.recordList);
    }

  }
</script>

<style lang="scss">
    .layout-content {
        display: flex;
        flex-direction: column-reverse;
    }

</style>

<style lang="scss" scoped>
    @import "~@/assets/style/helper.scss";

</style>