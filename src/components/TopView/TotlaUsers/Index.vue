<template>
  <div>
    <CommonCard 
      title="累计用户数"
      value="1,087,503"
    >
      <template>
        <div id="total-users-chart" :style="{ width: '100%', height: '100%' }"></div>
      </template>
      <template v-slot:footer>
        <div class="total-users-footer">
          <div class="compare">
            <span>日同比</span>
            <span>7.33%</span>
            <span class="increase"></span>
          </div>
          <div class="compare">
            <span>月同比</span>
            <span>7.33%</span>
            <span class="decrease"></span>
          </div>
        </div>
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
    const chartDom = document.getElementById('total-users-chart')
    const chart = this.$echarts.init(chartDom)
    chart.setOption({
      grid: {
        left: 0,
        right: 0,
        bottom: 0,
        top: 0,
      },
      yAxis: {
        type: 'category',
        show: false,
      },
      xAxis: {
        type: 'value',
        show: false,
      },
      series: [{
        stack:'总量',
        type: 'bar',
        data: [200],
        barWidth: 10,
        itemStyle: {
          color: '#45c946'
        }
      }, {
        stack:'总量',
        type: 'bar',
        data: [250],
        itemStyle: {
          color: '#eee'
        },
      }, {
        type: 'custom',
        stack: '总量',
        data: [200],
        renderItem: (params, api) => {
          const value = api.value(0)
          const endPoint = api.coord([value, 0])
          return {
            type: 'group',
            position: endPoint,
            children: [{
              type: 'path',
              shape: {
                d: 'M512 640L256 384h512l-256 256z',
                x: -5,
                y: -20,
                width: 10,
                height: 10,
                layout: 'cover',
              },
              style: {
                fill: '#45c946'
              }
            }, {
              type: 'path',
              shape: {
                d: 'M512 384l-256 256h512L512 384z',
                x: -5,
                y: 10,
                width: 10,
                height: 10,
                layout: 'cover',
              },
              style: {
                fill: '#45c946'
              }
            }]
          }
        }
      }]
    })
  },
}
</script>

<style lang='scss' scoped>
.total-users-footer {
  display: flex;
}
.compare{
  display: flex;
  align-items: center;
  font-size: 12px;
  line-height: 24px;
  .increase {
    width: 0;
    height: 0;
    border-width: 3px;
    border-color: transparent transparent red transparent;
    border-style: solid;
    margin:  0 0 3px 5px;
  }
  .decrease {
    width: 0;
    height: 0;
    border-width: 3px;
    border-color: green transparent transparent transparent;
    border-style: solid;
    margin:  3px 0 0 5px;
  }
}
</style>
