<template>
  <div>
    <a-spin :spinning="loading">
      <div :id="id" style="width:100%;height:230px;margin: 0 auto;"></div>
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
      myChart: null,
      xxdm: '',
      from: null,
      to: null,
      loading: false
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
      var xAxis = ['法学', '工学', '管理学', '教育学', '经济学', '理学', '历史学', '农学', '文学', '医学', '艺术学', '哲学']
      var data = [300, 280, 250, 260, 270, 300, 550, 500, 400, 390, 380, 390]
      // 基于准备好的dom，初始化echarts实例
      this.myChart = this.$echarts.init(document.getElementById(this.id))
      this.myChart.clear()
      const option = {
        title: {
          text: '专业布局 ',
          top: 12,
          left: 12,
          textStyle: {
            color: '#fff',
            fontSize: 14,
            fontweight: 400
          }
        },
        color: ['#0476d7'],
        tooltip: {
          trigger: 'axis',
          axisPointer: { // 坐标轴指示器，坐标轴触发有效
            type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'
          }
        },
        legend: {
          top: 20,
          right: 20,
          textStyle: {
            color: '#fff'
          },
          data: ['高校布点数', '专业布点数']
        },
        grid: {
          top: '20%',
          left: '6%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: [
          {
            type: 'category',
            data: xAxis,
            axisTick: {
              show: false,
              alignWithLabel: false
            },
            axisLine: { // 坐标轴轴线相关设置。数学上的x轴
              show: true,
              lineStyle: {
                color: '#29A8FF'
              }
            },
            axisLabel: { // 坐标轴刻度标签的相关设置
              fontSize: 12,
              color: '#d0d0d0',
              show: true,
              interval: 0,
              textStyle: {
                color: '#fff',
                margin: 12
              }
            }
          }
        ],
        yAxis: [
          {
            axisLabel: {
              margin: 20,
              textStyle: {
                color: '#fff'
              }
            },
            axisLine: { // 坐标轴轴线相关设置。数学上的x轴
              show: true,
              lineStyle: {
                color: '#29A8FF'
              }
            },
            axisTick: {
              show: false,
              alignWithLabel: false
            },
            splitLine: {
              show: false,
              lineStyle: {
                type: 'dashed', // 虚线
                color: '#233e64'
              }
            },
            type: 'value'
          }
        ],
        series: [
          {
            name: '专业布点数',
            type: 'bar',
            barWidth: 20,
            data: data,
            itemStyle: {
              normal: {
                color: new this.$echarts.graphic.LinearGradient(
                  0, 0, 0, 1,
                  [
                    { offset: 0, color: '#28a4fa' }, // 柱图渐变色
                    { offset: 0.5, color: '#1c68a5' }, // 柱图渐变色
                    { offset: 1, color: '#0c1936' } // 柱图渐变色
                  ]
                ),
                label: {
                  show: true, // 开启显示
                  position: 'top', // 在上方显示
                  textStyle: { // 数值样式
                    color: 'black',
                    fontSize: 16
                  }
                }
              }
            }

          },
          {
            name: '高校布点数',
            type: 'line',
            barWidth: 20,
            itemStyle: {
              normal: {
                color: '#E33AA3'
              }
            },
            data: data
          }
        ]
      }
      this.myChart.setOption(option)
    }
  }
}
</script>
