<template>
  <div class="bottom-view">
    <div class="view">
      <el-card shadow="hover">
        <template v-slot:header>
          <div class="title-wrapper">关键字搜索</div>
        </template>
        <template>
          <div class="chart-wrapper">
            <div class="chart-inner">
              <div class="chart">
                <div class="chart-title">搜索用户数</div>
                <div class="chart-data">93，634</div>
                <v-chart :options="searchUser"></v-chart>
              </div>
              <div class="chart">
                <div class="chart-title">搜索用户数</div>
                <div class="chart-data">93，634</div>
                <v-chart :options="searchNumber"></v-chart>
              </div>
            </div>
            <div class="table-inner">
              <el-table :data="tableData">
                <el-table-column prop="rank" label="排名" width="180"></el-table-column>
                <el-table-column prop="keyword" label="关键字" width="180"></el-table-column>
                <el-table-column prop="count" label="总搜索量"></el-table-column>
                <el-table-column prop="user" label="搜索用户数"></el-table-column>
              </el-table>
              <el-pagination
                layout="prev, pager, next"
                :total="100"
                :page-size="4"
                background=""
                @current-change="onPagehange"
              />
            </div>
          </div>
        </template>
      </el-card>
    </div>
    <div class="view">
      <el-card shadow="hover">
        <template v-slot:header>
          <div class="title-wrapper">
            <div class="title">分类销售排行</div>
            <div class="radio-wrapper">
              <el-radio-group v-model="radioSelect" size="small">
                <el-radio-button label="品类"></el-radio-button>
                <el-radio-button label="商品"></el-radio-button>
              </el-radio-group>
            </div>
          </div>
        </template>
        <template>
          <v-chart :options="categoryOptions" />
        </template>
      </el-card>
    </div>
  </div>
</template>

<script>

export default {
  components: {},
  data() {
    return {
      searchUser: {
        xAxis: {
          type: 'category',
          boundaryGap: false
        },
        yAxis: {
          show:false
        },
        series: [{
          type: 'line',
          areaStyle: {
            color: 'rgba(95,187,255,.5)'
          },
          lineStyle: {
            color: 'rgb(95,187,255)'
          },
          itemStyle: {
            opacity: 0
          },
          smooth: true,
          data: [100,150,200,250,200,150,100,50,100,150]
        }],
        grid: {
          top: 0,
          left:0,
          right: 0,
          bottom: 0
        }
      },
      searchNumber: {},
      tableData: [
        { id: 1, rank: 1, keyword: '北京', count: 100, user: 90, range: '90%'},
        { id: 2, rank: 2, keyword: '北京', count: 100, user: 90, range: '90%'},
        { id: 3, rank: 3, keyword: '北京', count: 100, user: 90, range: '90%'},
        { id: 4, rank: 4, keyword: '北京', count: 100, user: 90, range: '90%'}
      ],
      radioSelect: '品类',
      categoryOptions: {}
    };
  },
  methods: {
    onPagehange(page) {
      console.log(page)
    },
    renderPieChart() {
      const mockData = [
        {
          legendname: '分娩粥店',
          value: 67,
          percent: '15.40%',
          name: '分娩粥店 | 15.40%'
        },
        {
          legendname: '简餐便当',
          value: 97,
          percent: '22.30%',
          name: '简餐便当 | 22.30%'
        },
        {
          legendname: '汉堡披萨',
          value: 92,
          percent: '21.35%',
          name: '汉堡披萨 | 21.35%'
        }
      ]
      this.categoryOptions = {
        title: [{
          text: '品类分布',
          textStyle: {
            fontSize: 14,
            color: '#666',
          },
          left: 20,
          top: 20
        }, {
          text: '累计订单量',
          subtext: '320',
          x: '34.5%',
          y: '42.5%',
          textStyle: {
            fontSize: 14,
            color: '#999'
          },
          subtextStyle: {
            fontSize: 28,
            color: '#333'
          },
          textAlign: 'center'
        }],
        series: [{
          type: 'pie',
          data: mockData,
          label: {
            normal: {
              show: true,
              position: 'outter',
              formatter: params => {
                return `${params.data.legendname} | ${params.data.percent}`
              }
            }
          },
          center:['35%', '50%'],
          radius:['45%', '60%'],
          labelLine: {
            normal: {
              length: 5,
              length2: 3,
              smooth: true
            }
          },
          clockwise: true,
          itemStyle: {
            borderWidth: 10,
            borderColor: '#fff'
          }
        }],
        legend: {
          type: 'scroll',
          orient: 'vertical',
          height: 250,
          left: '70%',
          top: 'middle'
        },
        tooltip: {
          trigger: 'item',
          formatter: params => {
            const str = params.seriesName + '<br />' +params.marker + params.data.legendname + '<br />' + '数量' + params.data.value
            return str
          }
        }
      }
    }
  },
  mounted() {
    this.renderPieChart()
  },
}
</script>

<style lang='scss' scoped>
.bottom-view {
  display: flex;
  margin-top: 20px;
  .view {
    flex: 1;
    &:first-child {
      padding-right: 10px;
    }
    &:last-child {
      padding-left: 10px;
    }
    .title-wrapper {
      display: flex;
      align-items: center;
      height: 60px;
      box-sizing:  border-box;
      border-bottom: 1px solid #eee;
      font-size: 14px;
      font-weight: 500;
      padding:  0 0 0 20px;
      .radio-wrapper {
        flex: 1;
        display: flex;
        justify-content: flex-end;
        padding-right: 20px;
      }
    }
    .chart-wrapper {
      display: flex;
      flex-direction: column;
      height: 452px;
      .chart-inner {
        display: flex;
        padding:  0 10px;
        margin-top: 20px;
        .chart {
          flex: 1;
          padding: 0 10px;
          .chart-title {
            color: #999;
            font-size: 14px;
          };
          .chart-data {
            font-size: 22px;
            color: #333;
            font-weight: 500;
            letter-spacing: 2px;
          }
          .echarts{
            height: 50px;
            width: 100%;
          }
        }
      }
      .table-wrapper{
        margin-top: 20px;
        flex: 1;
        padding:  0 20px 20px;
        .el-pagination {
          display: flex;
          justify-content: flex-end;
          margin-top: 15px;
        }
      }
    }
  }
}
</style>