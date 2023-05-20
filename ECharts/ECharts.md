# 数据可视化 - ECharts

数据可视化主要目的:借助于图形化手段，清晰有效地传达与沟通信息。   
数据可视化在我们互联网公司中经常用于通用数据报表，移动端图表，大屏可视化，图编辑等

## 基本使用

> 步骤1:下载并引入echarts.js文件—图表依赖这个js库

> 步骤2∶准备一个具备大小的DOM容器—→生成的图表会放入这个容器内

> 步骤3∶初始化echarts实例对象→实例化echarts对象

> 步骤4∶指定配置项和数据(option)—→根据具体需求修改配置选项

> 步骤5∶将配置项设置给echarts实例对象——让echarts对象根据修改好的配置生效

## 配置讲解

title :标题组件  
tooltip∶提示框组件   
legend :图例组件   
toolbox:工具栏   
grid:直角坐标系内绘图网格  
xAxis:直角坐标系grid中的×轴  
yAxis:直角坐标系grid 中的y轴    
series:系列列表。每个系列通过   
type 决定自己的图表类型(什么类型的图标)  
color:调色盘颜色列表

series:系列列表
type:类型(什么类型的图表)比如line是折线 bar 柱形等  name:系列名称，用于tooltip的显示，legend的图例筛选变化stack:数据堆叠。如果设置相同值，则会数据堆叠。   
数据堆叠︰第二个数据值=第一个数据值＋第二个数据值
第三个数据值=第二个数据值＋第三个数据值...依次叠加   

如果给stack指定不同值或者去掉这个属性则不会发生数据堆
叠

# EChsrts项目

用到 flexible.js + rem + 媒体查询

## 边框图片

盒子大小不一，但是边框样式相同，此时就需要边框图片来完成
新增了border-image属性，这个新属性允许指定一幅图像作为元素的边框。   

2.边框图片切图原理︰(重要)
把四个角切出去(九宫格的由来），中间部分可以铺排、拉伸或者环绕。按照上右下左顺序切割

### 语法：

border-image-source   
用在边框的图片的路径。（那个图片?)   
border-image-slice  
图片边框向内偏移。（裁剪的尺寸，一定不加单位，上右下左顺序>   
border-image-width  
图片边框的宽度（需要加单位)(不是边框的宽度是边框图片的宽度)，不会挤压文字，默认和边框宽度相等。

border-image-repeat  
图像边框是否应平铺(repeat)、铺满(round)或拉伸(stretch)默认拉伸

![QQ截图20230420143959.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f4f1ead6c44e48a2b5f2b74a9864c4be~tplv-k3u1fbpfcp-watermark.image?)

```
border-image-source: url( images/border.png);
border-image-slice: 30 30 30 30;
*border-image-sLice: 30;*/



/*这个属性默认的是border的宽度但是有区别，这个是边框图片的宽度不会挤压文字*/
border-image-width: 30px:
```

## 类名调用字体图标

![QQ截图20230420150437.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c83af6046f6f4601a2723f40dc3de4f8~tplv-k3u1fbpfcp-watermark.image?)

### 柱形图：

```
X轴和Y轴线条颜色:xAxis/yAxis配置:axisLine: {
lineStyle: {
color: "green"}
}

坐标轴分割线颜色:xAxis/yAxis配置:splitLine: {
lineStyle: {
color: 'red'
}
}

网格边框颜色:grid 配置:show: true,
borderColor: "rgba(0,240,255,0.3)"
```
