<template>
  <div>
    <CommonCard
      title="累计订单量"
      value="22,039,165"
    >
      <template>
        <div id="total-orders-chart" :style="{ width: '100%', height: '100%' }"></div>
      </template>
      <template v-slot:footer>
        <span>昨日订单量</span>
        <span>2,000,000</span>
      </template>
    </CommonCard>
  </div>
</template>

<script>
import commonCardMixin from '../../../mixins/commonCardMixin'

export default {
  mixins:[commonCardMixin],
  data() {
    return {
      
    };
  },
  methods: {
    
  },
  mounted() {
    const chartDom = document.getElementById('total-orders-chart')
    const chart = this.$echarts.init(chartDom)
    chart.setOption({
      xAxis: {
        type: 'category',
        show: false,
        boundaryGap: false,
      },
      yAxis: {
        show: false
      },
      series: [{
        type: 'line',
        data: [620,120,223,434,567,234,590,234,666,321,122,366],
        areaStyle: {
          color: 'purple'
        },
        lineStyle: {
          width: 0,
        },
        itemStyle: {
          opacity: 0
        },
        smooth: true,
      }],
      grid: {
        top: 0,
        bottom: 0,
        left: 0,
        right: 0,
      }
    })
  },
}
</script>

<style lang='scss' scoped>

</style>