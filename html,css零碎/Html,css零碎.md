# html,css基础小知识

css里添加背景图片：

```
background-image: url('../img/fa-search.png');
```

透明度：

```
background: rgba(0,0,0,0.3);
```

## 背景固定：

![QQ截图20230221193507.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/49e38fe6189343188cf7fd714c73c100~tplv-k3u1fbpfcp-watermark.image?)

```
background: transparent url(image.jpg) repeat-y fixed top ;

background:black url(images/bg.jpg） no-repeat fixed center top;
```

> 设置背景图片的大小,
> background-size:宽度高度;

background-size属性规定背景图像的尺寸    

> background-size:背景图片宽度背景图片高度;    

单位:长度l百分比| cover | contain;    
cover把背景图像扩展至足够大，以使背景图像完全覆盖背景区域。  
contain把图像图像扩展至最大尺寸，以使其宽度和高度完全适应内 容区域  

![QQ截图20230221193819.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a6148a1109794fe0a315ec0a7c95eb66~tplv-k3u1fbpfcp-watermark.image?)

## CSS有三个非常重要的三个特性∶层叠性、继承性、优先级。

1. 相同选择器给设置相同的样式，此时一个样式就会覆盖（层叠）另一个冲突的样式。层叠性主要解决样式冲突的问题  
   层叠性原则∶  
   样式冲突，遵循的原则是就近原则，哪个样式离结构近，就执行哪个样式样式不冲突，不会层叠

2. cSS中的继承:子标签会继承父标签的某些样式，如文本颜色和字号。  
   恰当地使用继承可以简化代码，降低CSS样式的复杂性
   子元素可以继承父元素的样式( text- , font-, line-这些元素开头的可以继承，以及color属性

行高的继承性：

```
body {
font : 12px/ 1.5 Microsoft raHei ;
}
```

行高可以跟单位也可以不跟单位  
如果子元素没有设置行高，则会继承父元素的行高为1.5  
此时子元素的行高是:当前子元素的文字大小*1.5  
body行高1.5这样写法最大的优势就是里面子元素可以根据自己文字大小自动调整行高

![QQ截图20230221194543.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cd6b537b3d5a4c7ba995368250cd9e91~tplv-k3u1fbpfcp-watermark.image?)

块级盒子水平居中
margin：0 auto

行内元素或者行内块元素水平居中给其父元素添加text-align:center即可。

对于两个嵌套关系(父子关系)的块元素，父元素有上外边距同时子元素也有上外边距，此时父元素会塌陷较大的外边距值。

解决方案:
可以为父元素定义上边框。   
可以为父元素定义上内边距。  
可以为父元素添加overflow:hidden。

## 圆角边框：

border-radius属性用于设置元素的外边框圆角。  
语法︰  
`border-radius : length;`

参数值可以为数值或百分比的形式  
如果是正方形，想要设置为一个圆，把数值修改为高度或者宽度的一半即可，或者直接写为50%如果是个矩形,设置为高度的一半就可以做  

该属性是一个简写属性，可以跟四个值，分别代表左上角、右上角、右下角、左下角   
分开写:   

一定注意左下角不是圆角，其余三个是圆角写法:  
`border-radius:7px7px7px 0;`

```
border-top-left-radius、
border-top-right-radius、
border-bottom-right-radius，
border-bottom-left-radius
```

![QQ截图20230221195558.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8bae62dca2d745238523235b8f576418~tplv-k3u1fbpfcp-watermark.image?)

1.默认的是外阴影(outset),但是不可以写这个单词,否则导致阴影无效   
2盒子阴影不占用空间，不会影响其他盒子排列。

` box-shadow: 0 2px 3px 3px rgba(0,0,0,0.1);`

清除浮动的本质是清除浮动元素造成的影响如果父盒子本身有高度，则不需要清除浮动   
清除浮动之后，父级就会根据浮动的子盒子自动检测高度。父级有了高度，就不会影响下面的标准流了   

额外标签法会在浮动元素末尾添加一个空的标签。例如
`<div style=" clear:both”></div>`，或者其他标签(如`<br />`等）。

为什么需要清除浮动?  

1. 父级没高度。   
2. 子盒子浮动了。   
3. 影响下面布局了，我们就应该清除浮动了。

清除浮动：
1.额外标签法也称为隔墙法，是W3C推荐的做法  
2．父级添加overflow属性,overflow:hidden     
3.父级添加after伪元素 

![QQ截图20230226210631.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6844f0efe3de42129f5d252e2f38358b~tplv-k3u1fbpfcp-watermark.image?)
4.父级添加双伪元素  

![QQ截图20230226210840.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4c0a8e4ce8334f28bf6bae5bb9034ce4~tplv-k3u1fbpfcp-watermark.image?)

### 精灵图

使用精灵图核心总结:  
1.精灵图主要针对于小的背景图片使用。  
2.主要借助于背景位置来实现---background-position。  
3.一般情况下精灵图都是负值。(千万注意网页中的坐标∶x轴右边走是正值，左边走是负值，y轴同理。)

![QQ截图20230225131740.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a7861237e1b24493b0d5825accb6c187~tplv-k3u1fbpfcp-watermark.image?)

3D呈现**transfrom-style**   
控制子元素是否开启三维立体环境。    
transform-style: flat子元素不开启3d立体空间默认的   transform-style: preserve-3d;子元素开启立体空间代码写给父级，但是影响的是子盒子   
这个属性很重要，后面必用   

**transparent**： 透明  

1.
PC端
![QQ截图20230228174153.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/339203f507964557b2e56fdd19525c63~tplv-k3u1fbpfcp-watermark.image?)

2.
移动端：
![QQ截图20230305195118.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/df18b922afde4c76954ebf094c4261b9~tplv-k3u1fbpfcp-watermark.image?)

> 背景渐变必须添加浏览器私有前缀

## 理想视口ideal viewport

![QQ截图20230228221329.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a25066bb0e6c4c679f564dee21e4efa9~tplv-k3u1fbpfcp-watermark.image?)

物理像素就是我们说的分辨率iPhone8的物理像素是750   
在iPhone8里面  1px开发像素=2个物理像素

**移动端里：**
![QQ截图20230228224143.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/03284665da784d6eb3b251a83b451f6f~tplv-k3u1fbpfcp-watermark.image?)

 ---------------------------   

**粘性定位：**
![QQ截图20230303092455.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/181bfbcb15d44ba99c13a76b2359431d~tplv-k3u1fbpfcp-watermark.image?)

---------------------------------

**移动端布局：**
![QQ截图20230303100036.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c01759234c90437ab73f19bc0ebc7d0d~tplv-k3u1fbpfcp-watermark.image?)

### flex布局

> 总结flex布局原理∶
> 就是通过给父盒子添加flex属性，来控制子盒子的位置和排列方式

![QQ截图20230304100843.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4eae200cce6a4967a098e82bab510296~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230304101322.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e3ffa12f17414a3ba0e71b206ac9d15c~tplv-k3u1fbpfcp-watermark.image?)

### 固定定位：

固定定位应该有宽度。
固定定位跟父级没有关系，以屏幕为准
所以要加  
如

```
min-width: 320px;
max-width: 540px;
```

> 加定位会把元素直接变成块级。

#### 使用Less运算写法完成px单位到rem单位的转换

运算：  

1. 加、减、乘直接书写计算表达式   
   
   2. 除法需要添加 小括号 或 **.**   
   
   注意：  

表达式存在多个单位以第一个单位为准  

#### 使用Less导入写法引用其他Less文件

> @import 'base.less'

### vw / vh

相对单位   
相对视口的尺寸计算结果

vw：viewport width

1vw = 1/100视口宽度

vh：viewport height

1vh = 1/100视口高度

vh几乎少用
不管在什么屏幕下，我们把屏幕分为平均的100等份。

vw和1%有没有区别:  
1.vw永远是以视口的宽度为准。·在375设计稿下，1vw永远3.75px   
2.百分比以父盒子为准。假如父盒子是200px，则1%是2px

![QQ截图20230312094644.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e93c86d4ebd04fd7b9d495a41b211cc2~tplv-k3u1fbpfcp-watermark.image?)

> 响应式需要一个父级做为布局容器，来配合子级元素来实现变化效果。  
> 原理就是在不同屏幕下，通过媒体查询来改变这个布局容器的大小，再改变里面子元素的排列方式和大小，从而实现不同屏幕下，看到不同的页面布局和样式变化。

```
@media screen and (max-width: 767px) {
  .box {
    width: 100%;
  }
}
```

> 媒体查询要严格按照这种格式，有空格的加空格，如 and 左右都有空格，不能少加

### Bootstrap

![QQ截图20230312103405.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a0f7466b634746aaaeb1ee67a170bd3e~tplv-k3u1fbpfcp-watermark.image?)

```
<div class="container">123</div>
<div class="container-fluid">123</div>
自动定义好了宽度。
```

### 栅格系统

Bootstrap提供了一套响应式、移动设备优先的流式栅格系统，随着屏幕或视口( viewport)尺寸的增加，系统会自动分为最多12列。

#### 列嵌套

Bootstrap 提供了一套响应式、移动设备优先的流式栅格系统，随着屏幕或视口（viewport）尺寸的增加，系统会自动分为最多12列。    
栅格系统用于通过一系列的行（row）与列（column）的组合来创建页面布局  
栅格系统内置的栅格系统将内容再次嵌套。简单理解就是一个列内再分成若干份小列。我们可以通过添加一个新的.row元素和一系列.col-sm-*元素到已经存在的.col-sm-*元素内。
总列数是12。
列嵌套最好加行 row 可以取消父元素的padding 

#### 列偏移

使用 `.col-md-offset-*` 类可以将列向右侧偏移。

#### 列排序

通过使用.col-md-push-*和.col-md-pull-*类就可以很容易的改变列( column )的顺序。

往右 推 用.col-md-push-*
往左 拉 用 .col-md-pull-*

![QQ截图20230312180245.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6b868523bc184194a1eb73a5fdf0a512~tplv-k3u1fbpfcp-watermark.image?)

在移动端里怎么简便怎么写，一般不用ul 和 li,直接用a链接

## 标签

![QQ截图20230315221742.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d1181570000d4514a74e218d4da709e2~tplv-k3u1fbpfcp-watermark.image?)

图片标签的src属性  
属性名:src  
属性值:目标图片的路径  
当前网页和目标图片在同一个文件夹中，路径直接写目标图片的名字即可（包括后缀名)

图片标签的alt属性  
属性名:alt  
属性值:替换文本  
当图片加载失败时，才显示alt的文本  
当图片加载成功时，不会显示alt的文本  

图片标签的title属性   
属性名: title   
属性值:提示文本     
当鼠标悬停时，才显示的文本  
注意点:title属性不仅仅可以用于图片标签，还可以用于其他标签

绝对路径∶指目录下的绝对位置，可直接到达目标位置，通常从盘符开始的路径    
例如:   
盘符开头:D:\dayo1\images\7.jpg   
完整的网络地址:
https://www.itcast.cn/2018czgw/images/logo.gif(了解)

相对路径:  
从当前文件开始出发找目标文件的过程相对路径分类∶  
同级目录  
下级目录  
上级目录

音频标签的介绍   
场景:在页面中插入音频   
代码:`<audio src=" ./music.mp3" controls></audio>`

视频标签的介绍   
场景:在页面中插入视频   

代码: `<video src=" ./video.mp4" controls></video>`
