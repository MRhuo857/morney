<template>
    <Layout class-prefix="layout">
        <NumberPad @update:value="onUpdateAmount" @submit="saveRecord"/>
        <Note filed-name="备注"
              @update:value="onUpdateNotes"
        placeholder="在这里输入备注"
        />
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
  import {recordListModel} from '@/models/recordListModel';
  import {tagListModel} from '@/models/tagListModel';

  const recordList = recordListModel.fetch();
  const tagList = tagListModel.fetch();

  @Component({
    components: {Types, Tags, Note, NumberPad},
  })
  export default class Money extends Vue {
    tags = tagList;
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
      const record2: RecordItem = recordListModel.clone(this.record);
      record2.createdAt = new Date();
      this.recordList.push(record2);
    }

    @Watch('recordList')
    onRecordListChange() {
      recordListModel.save(this.recordList);
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