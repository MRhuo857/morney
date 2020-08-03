<template>
    <Layout class-prefix="layout">
        <NumberPad/>
        <Note/>
        <Tags/>
        <Types :xxx=" 333 "/>
    </Layout>
</template>

<script lang="ts">
  import NumberPad from '@/components/Money/NumberPad.vue';
  import Note from '@/components/Money/Note.vue';
  import Tags from '@/components/Money/Tags.vue';
  import Types from '@/components/Money/Types.vue';

  export default {
    name: 'Money',
    components: {Types, Tags, Note, NumberPad},
  };
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