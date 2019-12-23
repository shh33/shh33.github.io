---
title: 关于echarts的使用
typora-root-url: ..
date: 2019-10-17 16:56:03
tags: Echarts
categories: Echarts
password:
top:
---



# 关于Echarts的使用

**主要的及格配置项**

> title  **图表标题**
>
> tooltip **提示框**
>
> legend **图例**
>
> grid
>
> xAxis **X轴样式**
>
> yAxis **Y轴样式**
>
> series **配置**

### title 图表标题

```javascript
title: {
        x: 'left',                 // 水平安放位置，默认为左对齐，可选为：
                                   // 'center' ¦ 'left' ¦ 'right'
                                   // ¦ {number}（x坐标，单位px）
        y: 'top',                  // 垂直安放位置，默认为全图顶端，可选为：
                                   // 'top' ¦ 'bottom' ¦ 'center'
                                   // ¦ {number}（y坐标，单位px）
        //textAlign: null          // 水平对齐方式，默认根据x设置自动调整
        backgroundColor: 'rgba(0,0,0,0)',
        borderColor: '#ccc',       // 标题边框颜色
        borderWidth: 0,            // 标题边框线宽，单位px，默认为0（无边框）
        padding: 5,                // 标题内边距，单位px，默认各方向内边距为5，
                                   // 接受数组分别设定上右下左边距，同css
        itemGap: 10,               // 主副标题纵向间隔，单位px，默认为10，
        textStyle: {
            fontSize: 18,
            fontWeight: 'bolder',
            color: '#333'          // 主标题文字颜色
        },
        subtextStyle: {
            color: '#aaa'          // 副标题文字颜色
        }
    },

```

### tooltip 提示框

```javascript
// 提示框
    tooltip: {
        trigger: 'item',           // item只会显示该点的数据，axis显示该列下所有坐标轴所对应的数据
        showDelay: 20,             // 显示延迟，添加显示延迟可以避免频繁切换，单位ms
        hideDelay: 100,            // 隐藏延迟，单位ms
        transitionDuration : 0.4,  // 动画变换时间，单位s
        backgroundColor: 'rgba(0,0,0,0.7)',     // 提示背景颜色，默认为透明度为0.7的黑色
        borderColor: '#333',       // 提示边框颜色
        borderRadius: 4,           // 提示边框圆角，单位px，默认为4
        borderWidth: 0,            // 提示边框线宽，单位px，默认为0（无边框）
        padding: 5,                // 提示内边距，单位px，默认各方向内边距为5，
                                   // 接受数组分别设定上右下左边距，同css
        axisPointer : {            // 坐标轴指示器，坐标轴触发有效
            type : 'line',         // 默认为直线，可选为：'line' | 'shadow'
            lineStyle : {          // 直线指示器样式设置
                color: '#48b',
                width: 2,
                type: 'solid'
            },
            shadowStyle : {                       // 阴影指示器样式设置
                width: 'auto',                   // 阴影大小
                color: 'rgba(150,150,150,0.3)'  // 阴影颜色
            }
        },
        textStyle: {
            color: '#fff'
        }
    },

```

### legend 图例

```javascript
legend: {
 2         orient: 'horizontal',      // 布局方式，默认为水平布局，可选为：
 3                                    // 'horizontal' ¦ 'vertical'
 4         x: 'center',               // 水平安放位置，默认为全图居中，可选为：
 5                                    // 'center' ¦ 'left' ¦ 'right'
 6                                    // ¦ {number}（x坐标，单位px）
 7         y: 'top',                  // 垂直安放位置，默认为全图顶端，可选为：
 8                                    // 'top' ¦ 'bottom' ¦ 'center'
 9                                    // ¦ {number}（y坐标，单位px）
10         backgroundColor: 'rgba(0,0,0,0)',
11         borderColor: '#ccc',       // 图例边框颜色
12         borderWidth: 0,            // 图例边框线宽，单位px，默认为0（无边框）
13         padding: 5,                // 图例内边距，单位px，默认各方向内边距为5，
14                                    // 接受数组分别设定上右下左边距，同css
15         itemGap: 10,               // 各个item之间的间隔，单位px，默认为10，
16                                    // 横向布局时为水平间隔，纵向布局时为纵向间隔
17         itemWidth: 20,             // 图例图形宽度
18         itemHeight: 14,            // 图例图形高度
19         textStyle: {
20             color: '#333'          // 图例文字颜色
21         }
22     },
```

### Axis 分为category和value

```javascript
categoryAxis: {
 2         position: 'bottom',    // 位置
 3         nameLocation: 'end',   // 坐标轴名字位置，支持'start' | 'end'
 4         boundaryGap: true,     // 类目起始和结束两端空白策略
 5         axisLine: {            // 坐标轴线
 6             show: true,        // 默认显示，属性show控制显示与否
 7             lineStyle: {       // 属性lineStyle控制线条样式
 8                 color: '#48b',
 9                 width: 2,      //设置为0也是不现在坐标线
10                 type: 'solid'
11             }
12         },
13         axisTick: {            // 坐标轴小标记
14             show: true,       // 属性show控制显示与否，默认不显示
15             interval: 'auto',
16             // onGap: null,
17             inside : false,    // 控制小标记是否在grid里 
18             length :5,         // 属性length控制线长
19             lineStyle: {       // 属性lineStyle控制线条样式
20                 color: '#333',
21                 width: 1
22             }
23         },
24         axisLabel: {           // 坐标轴文本标签，详见axis.axisLabel
25             show: true,
26             interval: 'auto',
27             rotate: 0,
28             margin: 8,
29             // formatter: null,
30             textStyle: {       // 其余属性默认使用全局文本样式，详见TEXTSTYLE
31                 color: '#333'
32             }
33         },
34         splitLine: {           // 分隔线
35             show: true,        // 默认显示，属性show控制显示与否
36             // onGap: null,
37             lineStyle: {       // 属性lineStyle（详见lineStyle）控制线条样式
38                 color: ['#ccc'],
39                 width: 1,
40                 type: 'solid'
41             }
42         },
43         splitArea: {           // 分隔区域
44             show: false,       // 默认不显示，属性show控制显示与否
45             // onGap: null,
46             areaStyle: {       // 属性areaStyle（详见areaStyle）控制区域样式
47                 color: ['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)']
48             }
49         }
50     },
```

```javascript
valueAxis: {
 2         position: 'left',      // 位置
 3         nameLocation: 'end',   // 坐标轴名字位置，支持'start' | 'end'
 4         nameTextStyle: {},     // 坐标轴文字样式，默认取全局样式
 5         boundaryGap: [0, 0],   // 数值起始和结束两端空白策略
 6         splitNumber: 5,        // 分割段数，默认为5
 7         axisLine: {            // 坐标轴线
 8             show: true,        // 默认显示，属性show控制显示与否
 9             lineStyle: {       // 属性lineStyle控制线条样式
10                 color: '#48b',
11                 width: 2,
12                 type: 'solid'
13             }
14         },
15         axisTick: {            // 坐标轴小标记
16             show: false,       // 属性show控制显示与否，默认不显示
17             inside : false,    // 控制小标记是否在grid里 
18             length :5,         // 属性length控制线长
19             lineStyle: {       // 属性lineStyle控制线条样式
20                 color: '#333',
21                 width: 1
22             }
23         },
24         axisLabel: {           // 坐标轴文本标签，详见axis.axisLabel
25             show: true,
26             rotate: 0,
27             margin: 8,
28             // formatter: null,
29             textStyle: {       // 其余属性默认使用全局文本样式，详见TEXTSTYLE
30                 color: '#333'
31             }
32         },
33         splitLine: {           // 分隔线
34             show: true,        // 默认显示，属性show控制显示与否
35             lineStyle: {       // 属性lineStyle（详见lineStyle）控制线条样式
36                 color: ['#ccc'],
37                 width: 1,
38                 type: 'solid'
39             }
40         },
41         splitArea: {           // 分隔区域
42             show: false,       // 默认不显示，属性show控制显示与否
43             areaStyle: {       // 属性areaStyle（详见areaStyle）控制区域样式
44                 color: ['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)']
45             }
46         }
47     },
48 
49     polar : {
50         center : ['50%', '50%'],    // 默认全局居中
51         radius : '75%',
52         startAngle : 90,
53         splitNumber : 5,
54         name : {
55             show: true,
56             textStyle: {       // 其余属性默认使用全局文本样式，详见TEXTSTYLE
57                 color: '#333'
58             }
59         },
60         axisLine: {            // 坐标轴线
61             show: true,        // 默认显示，属性show控制显示与否
62             lineStyle: {       // 属性lineStyle控制线条样式
63                 color: '#ccc',
64                 width: 1,
65                 type: 'solid'
66             }
67         },
68         axisLabel: {           // 坐标轴文本标签，详见axis.axisLabel
69             show: false,
70             textStyle: {       // 其余属性默认使用全局文本样式，详见TEXTSTYLE
71                 color: '#333'
72             }
73         },
74         splitArea : {
75             show : true,
76             areaStyle : {
77                 color: ['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)']
78             }
79         },
80         splitLine : {
81             show : true,
82             lineStyle : {
83                 width : 1,
84                 color : '#ccc'
85             }
86         }
87     }
```



### 饼图

```javascript
//饼图
    use_chart();
    function use_chart() {
        var myChart = echarts.init(document.getElementById('name_chart'));//绑定盒子ID
        var Data = [
            {value:21, name:'违章建筑',itemStyle:{
                    color:"#54cd78"
                }},
            {value:18, name:'非法船舶',itemStyle:{
                    color:"#2ab6f9"
                }},
            {value:12, name:'占用水域',itemStyle:{
                    color:"#f2637b"
                }},
            {value:18, name:'非法游泳',itemStyle:{
                    color:"#cbf119"
                }},
            {value:14, name:'非法采砂',itemStyle:{
                    color:"#36cbcb"
                }},
            {value:14, name:'违法垂钓',itemStyle:{
                    color:"#8944f5"
                }},
            {value:14, name:'违法捕捞',itemStyle:{
                    color:"#ffa06d"
                }}
        ];
        myChart.setOption({
            title: {
                text:'',
            },
            tooltip: {
                trigger: 'item',
                formatter: "{a} <br/>{b}: {c} ({d}%)"
            },
            //图例名
            legend: {
                orient: 'horizontal',
                x: 'center',
                y: '65%',
                data:['违法垂钓','违法捕捞','非法采砂','非法游泳','占用水域','非法船舶','违章建筑'],
                textStyle: {
                    color: '#999'
                }
            },
            series: [
                {
                    name:'水质概况',
                    type:'pie',
                    center: ['50%', '30%'],
                    radius: ['40%', '63%'],
                    avoidLabelOverlap: false,
                    label: {
                        normal: {
                            show: true,
                            position: 'center',
                            formatter:function (argument) {
                                var html;
                                html='101\r\n\r\n'+'违法事件';
                                return html;
                            },
                            textStyle:{
                                fontSize: 14,
                                color:'#333'
                            }
                        },
                        emphasis: {
                            show: false,
                            textStyle: {
                                fontSize: '15',
                                fontWeight: 'bold'
                            }
                        }
                    },
                    labelLine: {
                        normal: {
                            show: false
                        }
                    },
                    data: Data,
                    itemStyle : {
                        normal : {
                            // color:'#0364d9'
                        }
                    }
                }
            ]
        })
    }
```

### 折线图

```javascript
line_chart();
    function line_chart(){
        var xData = ["1月","2月","3月","4月","5月","6月","7月","8月","9月","10月","11月","12月"];
        var yData = [5,6,6,7,6,8,9,8,6,7,9,7,5];
        var myChart = echarts.init(document.getElementById('youID_chart'));
        myChart.setOption({
            title:{
                // 主副标题
                text:'',
                subtext: ''
            },
            grid: {
                left: 45,
                top: 20,
                right: 20,
                bottom: 35
            },
            tooltip: {
                trigger: 'axis'//item只会显示该点的数据，axis显示该列下所有坐标轴所对应的数据
            },
            xAxis: [
                {
                    splitLine:{
                        lineStyle:{
                            type:'dotted',//'dotted'虚线 'solid'实线
                            color:'#ebebeb'
                        },
                        show: true
                    },
                    axisTick:{       //刻度线
                        "show":false
                    },
                    type: 'category',
                    data: xData,
                    axisPointer: {
                        type: 'shadow'
                    },
                    axisLine: {
                        lineStyle:{
                            color:'#bfbfbf ',
                            width:0 //这里是坐标轴的宽度,为0就是不显示
                        }
                    },
                    axisLabel: {
                        show: true //这行代码控制着坐标轴x轴的文字是否显示
                    },
                }
            ],
            yAxis: [
                {
                    show: true,
                    splitLine:{
                        show: false
                    },
                    type: 'value',
                    name: '',
                    nameTextStyle: {
                        color:'#bfbfbf'
                    },
                    axisLine: {
                        lineStyle:{
                            color:'#bfbfbf'
                        }
                    }
                }
            ],
            series: [{
                name:'',
                data: yData,
                type: 'line',
                smooth: true,
                itemStyle:{
                    normal:{
                        color:'#147aff', //折点颜色
                        lineStyle:{
                            color:'#147aff' //折线颜色
                        }
                    }
                },
                areaStyle: {
                    normal: {
                        color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                            {offset: 0, color: '#d1e5ff'},
                            {offset: 0.5, color: '#eaf3ff'},
                            {offset: 1, color: '#fdfeff'}
                        ])
                    }
                }
            }]
        });
    }
```

https://www.cnblogs.com/1996zy/p/8963385.html