<template lang="html">
  <GChart
    v-if="chartData"
    :type="chartType"
    :data="chartData"
    :options="chartOptions"
  />
</template>

<script>
import { GChart } from 'vue-google-charts'
import { eventBus } from '@/main.js'

export default {
  name: 'energy-tracker-chart',
  data(){
    return {
      chartOptions: {
        width: 800,
        height: 240,
        title: 'Generation Mix for the GB power system',
        colors: ['#084887', '#f58a07', '#f9ab55', '#f7f5fb', '#909cc2', '#C1BB8F', '#A176BC']
      },
      chartType: "ColumnChart"
    }
  },
  props: ['mixData'],
  components : {
    GChart
  },
  mounted(){
    eventBus.$on('chart-select', (chartType) => {
      this.chartType = chartType
    })
  },
  computed: {
    chartData: function(){
      if(this.mixData){
        const chartData = this.mixData.map(mix => Object.values(mix))
        chartData[0] = Object.keys(this.mixData[0])
        return chartData
      }
      return null
    }
  }
}
</script>

<style lang="css" scoped>
</style>
