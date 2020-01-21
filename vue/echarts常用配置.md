常用图：
    柱形图
    扇形图
    折线图
    堆积图
    盒须图（箱形图）
常用配置：
    x轴（xAxis）
        xAxis: {
            show: true // 是否显示坐标轴
            position: top/bottom // x轴位置 
            offset:0 // x轴相对于默认位置的偏移
            type: value/category/time/log 数值/类目（默认）/时间/对数
            name: '坐标轴名称'
            nameLocation: start/center/end 坐标轴名称显示位置
            nameTextStyle: { // 坐标轴名称文字样式
                color: red,
                fontStyle: normal/italic/oblique,
                ...
            }
            nameGap:15 // 名称和坐标轴之间的距离
            data: this.axisList,
            boundaryGap: false, // 坐标轴两边留白策略  类目：ture/false  其他：['20%', '20%']
            axisTick: { // 刻度
                show: false
            },
            axisLine: { // 坐标轴样式设置
                lineStyle: {
                    color: 'rgba(0,0,0,.12)'
                }
            },
            axisLabel: { // 坐标轴文字设置
                show: true,
                textStyle: {
                    color: '#777C7C'
                }
            }
        }
    y轴 （yAxis）
        同x轴
    提示（tooltip）坐标指示器
        tooltip: {
          trigger: 'axis', // 触发方式 item/axis/none
          // formatter: '{c}%', // 显示为百分数
          axisPointer: { // 显示方式
            type: 'shadow', // line/cross
            shadowStyle: { // 阴影样式
              color: 'rgba(0,0,0,0)'
            }
          },
          padding: [5, 10], // 提示框浮层内边距
          backgroundColor: rgba(50,50,50,0.7) //提示框浮层的背景颜色
          borderColor: #333 // 提示框浮层的边框颜色
          borderWidth: 0px // 提示框浮层的边框宽
          textStyle: { // 提示框浮层的文本样式
            color: red,
            fontStyle: normal/italic/oblique,
            ...
          }
        },
    说明（legend）
    网格（grid）
    工具箱（toolbox）