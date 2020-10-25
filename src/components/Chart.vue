<template>
    <div class="wrapper" ref="wrapper"></div>
</template>

<script lang="ts">
    import Vue from 'vue'
    import {Component, Prop} from 'vue-property-decorator';
    import eCharts from 'echarts'
    @Component
  export default class Chart extends Vue{
      @Prop() options?:any;
      mounted(){
        if (this.options===undefined){return console.log('option为空')}
       const chart=eCharts.init(this.$refs.wrapper as HTMLDivElement)
        chart.setOption(this.options)
      }
  }
</script>

<style lang="scss" scoped>
    .wrapper{
        height: 400px;
    }

</style>