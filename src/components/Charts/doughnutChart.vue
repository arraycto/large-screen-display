<template>
  <div style="width:100%;">
    <a-spin :spinning="loading">
      <div class="doughnut-block">
        <div v-for="item in 3" :key="item" :id="`${id}-${item}`"></div>
      </div>
    </a-spin>
  </div>
</template>

<script>
export default {
  props: {
    id: {
      type: String,
      default: null
    }
  },
  data () {
    return {
      xxdm: '',
      from: null,
      to: null,
      loading: false,
      legendData: [],
      seriesData: []
    }
  },
  mounted () {
    this.loadDom()
  },
  methods: {
    resize () {
      this.myChart && this.myChart.resize()
    },
    loadDom () {
      // 基于准备好的dom，初始化echarts实例
      var seriesData = [
        { value: 21, name: '一流大学' },
        { value: 28, name: '普通本科' }
      ]
      for (let i = 1; i < 4; i++) {
        var myChart = this.$echarts.init(document.getElementById(`${this.id}-${i}`))
        myChart.clear()
        const option = {
          title: {
            text: i === 1 ? '全国高校类型占比' : '',
            textStyle: {
              color: '#fff',
              fontSize: 14,
              fontweight: 400
            },
            top: 10,
            left: 10
          },
          tooltip: {
            trigger: 'item',
            formatter: '{a} <br/>{b}: {c} ({d}%)'
          },
          series: [
            {
              name: '全国高校类型占比',
              type: 'pie',
              radius: ['40%', '55%'],
              avoidLabelOverlap: false,
              label: {
                position: 'outside',
                formatter: '{d}%',
                color: '#fff'
              },
              labelLine: {
                normal: {
                  smooth: 0.2, // 此处是改变折线的长度
                  length: 5,
                  length2: 4
                },
                lineStyle: {
                  color: '#fff'
                }
              },
              itemStyle: {
                color: (params) => {
                  var colorArr = ['#289ff8', '#6817ce', '#3066f5', '#ea45a0', '#ef886f', '#ebb794']
                  return colorArr[params.dataIndex]
                }
              },
              data: seriesData
            }
          ]
        }
        myChart.setOption(option)
      }
    }
  }
}
</script>
<style lang="less" scoped>
.doughnut-block {
  display: flex;
  >div{
    flex: 1;
    height:198px;
  }
}
</style>
