<template>
  <div class="sales-view">
    <el-card shadow="hover" :body-style="{ padding: 0}">
      <template v-slot:header>
        <div class="menu-wrapper">
          <el-menu
          class="menu-wrapper-menu"
            mode="horizontal"
            :default-active="activeIndex"
            @selsct="onMeunSelect(index)"
          >
            <el-menu-item index="1">销售额</el-menu-item>
            <el-menu-item index="2">访问量</el-menu-item>
          </el-menu>
          <div class="menu-right">
            <el-radio-group v-model="radioSelect" size="small">
              <el-radio-button label="今日"></el-radio-button>
              <el-radio-button label="本周"></el-radio-button>
              <el-radio-button label="本月"></el-radio-button>
              <el-radio-button label="本年"></el-radio-button>
            </el-radio-group>
            <el-date-picker
              type="daterange"
              v-model="date"
              range-separator="至"
              start-placeholde="开始日期"
              end-placeholde="结束日期"
              size="small"
              :picker-options="pickerOptions"
            >
            </el-date-picker>
          </div>
        </div>
      </template>
      <template>
        <div class="sales-view-chart-wrapper">
          <v-chart class="echarts" :options="chartOption"></v-chart>
          <div class="sales-view-list">
            <div class="sales-view-title">排行榜</div>
            <div class="list-item" v-for="item in rankData" :key="item.no">
              <div :class="['list-item-no', +item.no <= 3 ? 'top-no' : '']">{{item.no}}</div>
              <div class="list-item-name">{{item.name}}</div>
              <div class="list-item-money">{{item.money}}</div>
            </div>
          </div>
        </div>
      </template>
    </el-card>
  </div>
</template>

<script>

export default {
  components: {},
  data() {
    return {
      activeIndex: "1",
      radioSelect: '今日',
      date: '',
      pickerOptions: {
        shortcuts: [{
          text: '最近一周',
          onClick(picker) {
            const start = new Date()
            const end = new Date()
            start.setTime(start.getTime() - 3600 * 24 * 1000 * 7)
            picker.$emit('pick', [start, end])
          }
        }, {
          text: '最近一月',
          onClick(picker) {
            const start = new Date()
            const end = new Date()
            start.setTime(start.getTime() - 3600 * 24 * 1000 * 30)
            picker.$emit('pick', [start, end])
          }
        }, {
          text: '最近三月',
          oonClick(picker) {
            const start = new Date()
            const end = new Date()
            start.setTime(start.getTime() - 3600 * 24 * 1000 * 60)
            picker.$emit('pick', [start, end])
          }
        }]
      },
      chartOption: {
        title: {
          text: '年度销售额',
          textStyle: {
            fontSize: 12,
            color: '#666'
          },
          left: 50,
          top: 20,
        },
        xAxis: {
          type: 'category',
          data: ['1月', '2月', '3月', '4月', '5月', '6月', '7月', '8月', '9月', '10月', '11月', '12月' ],
          axixTick: {
            alignWidthLabel: true,
            lineStyle: {
              color: '#999'
            }
          },
          axixLine: {
            lineStyle: {
              color: '#999'
            }
          },
          axixLabel: {
            color: '#333'
          }
        },
        yAxis: {
          axixLine: {
            show: false
          },
          axixTick: {
            show: false
          },
          splitLine: {
            lineStyle: {
              type: 'dotted',
              color: '#eee'
            }
          }
        },
        series: [{
          type: 'bar',
          barWidth: '35%',
          data:[200, 250, 300, 350, 300, 250, 200, 250, 300, 350, 300, 250]
        }],
        color: ['#3398DB'],
        grid: {
          top: 70,
          left: 60,
          right:60,
          bottom: 50
        }
      },
      rankData: [
        {
          no: 1,
          name: '麦当劳',
          money: '323,21'
        }, {
          no: 2,
          name: '麦当劳',
          money: '323,21'
        }, {
          no: 3,
          name: '麦当劳',
          money: '323,21'
        }, {
          no: 4,
          name: '麦当劳',
          money: '323,21'
        }, {
          no: 5,
          name: '麦当劳',
          money: '323,21'
        }, {
          no: 6,
          name: '麦当劳',
          money: '323,21'
        }, {
          no: 7,
          name: '麦当劳',
          money: '323,21'
        }
      ]
    };
  },
  methods: {
    onMeunSelect(index) {
      this.activeIndex = index
    }
  },
  mounted() {
    
  },
}
</script>

<style lang='scss' scoped>
.sales-view{
  margin-top: 20px;
  position: relative;
  .menu-wrapper{
    display: flex;
    .menu-wrapper-menu{
      width: 100%;
    }
    .menu-right{
      position: absolute;
      top: 20px;
      right: 0px;
    }
  }
  .sales-view-chart-wrapper {
    display: flex;
    height: 270px;
    .echarts {
      flex: 0 0 70%;
      width: 70%;
      height: 100%;
    }
    .sales-view-list {
      flex: 1;
      width: 100%;
      height: 100%;
      overflow: hidden;
      margin-top: 15px;
      .sales-view-title {
        font-size: 20px;
        color: #666;
        font-weight: 500;
      }
      .list-item {
        display: flex;
        align-items: center;
        font-size: 12px;
        height: 20px;
        padding: 6px 20px 6px 0;

        .list-item-no {
          display: flex;
          align-items: center;
          justify-content: center;
          color: #666;
          height: 23px;
          width: 20px;

          &.top-no {
            background: #000;
            border-radius: 50%;
            color: #fff;
            font-weight: 500;
          }
        }
        .list-item-name {
          margin-left: 10px;
          color: #333;
        }
        .list-item-money {
          flex: 1;
          text-align: right;
        }
      }
    }
  }
}
</style>