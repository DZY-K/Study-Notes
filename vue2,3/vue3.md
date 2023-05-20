# VUE3--初学

## 任务列表案例

### 任务大致流程：

> 注解：本案例把v-for渲染在子组件里，而vue2的购物车案例是在父（根）组件中用v-for渲染的。

**Todo-List组件：**

> 1. 在根组件App中data输入list(数据)以后,进行父传子输入数据（这里传值是引用，而不是复制），利用porps属性渲染页面（这里接收的直接是一个数组，可能实际开发要把数据一条一条输入上去），在li里面用v-for把数据都循环渲染上去。v-if根据数据状态控制隐藏元素，再根据需求修改组件样式。      
> 2. v-model双向绑定直接在input里面绑定状态就行了，不用再子传父。原因看上面注解。     
> 3. 最后修改样式，在label添加类名，根据状态用三元表达式进行判断。  
> 4. 先给根组件定义一个索引，用子传父，props定义一个默认值接收，给页面通过索引绑定一个类，改变样式，点击按钮后，绑定事件，传索引，子传父，把索引传给根组件。用v-model1更新索引。`v-model:active="activeBtnIndex"`
> 5. 点击那个按钮，显示那个列表，在跟组件中，先获取列表，用计算属性，根据索引值，动态计算列表数据，用switch匹配，返回计算的结果。switch中的参数索引是与三个按钮绑定，返回结果，用过滤器过滤符合条件的数据。

**todo-input组件：**

> 1. Bootstrap提供的辅助类 class=“m2-n" 相当于 margin-top
> 2. 用户在页面写入的值，相当于先传入input（用v-model接收）里面（子组件里面），需要用data先return一个变量用来存用户输入的数据，在进行子传父。用$emit,还要阻止表单表单提交（用submit事件）。因为在input里面传值后，失去表单焦点，会默认刷新所以还要阻止表单表单提交。点击按钮即为提交，按钮和submit事件也是绑定的。
> 3. 添加任务，需要在根组件定义一个id值以绑定添加的值，用一个对象存添加的**任务**：**用push（）方法**，添加的格式与list里面的格式一样，之后定义的i值加一，如：nextId++。

> :root是一个伪类，表示文档根元素，所有主流浏览器均支持

> :root 选择器，除了 IE8 及更早的版本。在:root中声明相当于全局属性

建好项目在src中新建index.css写下如下代码

```
:root{
font-size:12px
}
```

> Bootstrap 使用的时候先看版本，目前使用只用组件，点击组件，找合适的组件，进行cv.

# VUE3----继续

## 一.侦听器

![QQ截图20230208120510.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5537da024d294488be90ea7a4dcdbedc~tplv-k3u1fbpfcp-watermark.image?)

> get请求返回值是promise

调某个方法返回值是promise,前面加await

![QQ截图20230208121424.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/933c2789002941d48eebdd098c15a2bc~tplv-k3u1fbpfcp-watermark.image?)

> 1. 用immediate必须把username写成配置对象，不能写成方法。应用handle方法，  
> 2. 监听谁把谁作为对象

![QQ截图20230208122157.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/303925eb1d584ce3aff0782963bb6709~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230208122506.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/50f01f7967a9402abd5acf68438e468e~tplv-k3u1fbpfcp-watermark.image?)

> 用deep会把对象的每个属性都监听到，但是我们只想监听单个属性，就需要把属性值作为对象，但要用单引号包裹。

**面试：**

![QQ截图20230208123301.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e007761d4a7b405880db3e9f81e24fd6~tplv-k3u1fbpfcp-watermark.image?)

## 二.生命周期

![QQ截图20230208123738.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/97e8c5fb1add45d0974ba6d60eed8ed2~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230208123910.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5a337bf18bdd4b75a79762745fcfa696~tplv-k3u1fbpfcp-watermark.image?)

> 当隐藏组件时组件会被认定为销毁

![QQ截图20230208124457.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2946525aef4347f584557e53a760f67a~tplv-k3u1fbpfcp-watermark.image?)

所以`update`监听组件的渲染

![QQ截图20230208124702.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/61f9ac4452d9479ba5504049b1454fa0~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230208125508.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f9d5235297f54ee8988e3a47ee9ee7ac~tplv-k3u1fbpfcp-watermark.image?)

> 回答上面的问题，beforeCreate无法访问data里面的数据所以无法发ajax.

## 生命周期流程：

> 1. 首先执行，beforeCreate 在内存中开始创建组件,但组建还没创建完毕,执行created组建在内存中创建完毕,此时可以发起ajax 请求初始数据,然后要把内存中的组件渲染到页面上,
> 2. 此时再执行beforemount将要把组件渲染到页面上但还没有渲染,然后再执行mounted把组件第一次在页面上渲染完毕,就可以操作组件里的dom 元素,然后创建阶段的生命周期函数都执行完了,
> 3. 然后再进行运行阶段的生命周期函数,当数据发生变化时,根据最新的数据更新dom 结构,执行beforeupdate这时将要更新，还没有完成更新,当执行updated 那当前组件根据这个数据在页面上渲染完毕了，以后只要数据更新就会根据这个顺序执行这两个函数。
> 4. 在组件被销毁的时候，先执行Beforeunmont,在执行unmount,当执行Beforeunmont表示组件将要被销毁，但还没完成销毁,执行unmount时组件被完全销毁。

![QQ截图20230208164649.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6d21efcd47a44c26882b83f804336d80~tplv-k3u1fbpfcp-watermark.image?)

> v-model子传父，父又传子时使用。

![QQ截图20230208164906.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2611bdadc490400db946f30982c16850~tplv-k3u1fbpfcp-watermark.image?)

数据接收方（bus.on）需要在created()中声明

----------------------------------

![QQ截图20230208170301.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/78277c3d73e146019b8540eee53b1031~tplv-k3u1fbpfcp-watermark.image?)

安装包：npm i mitt@2.1.0 -S

创建EventBus文件

![QQ截图20230210103025.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/74281769b88c4b1faffdc7268f5c4f26~tplv-k3u1fbpfcp-watermark.image?)

> 后代关系用法：**相当**于父传子，provide等于data传数据，inject等于props接收值。

```
父：
provide(){
    color:this.color,
    count:1
    }

   其子孙：
   export default{
   inject:['color','count']
```

> 用provide可以父传子孙，但是当外界使data数据改变时，provide里的数据无法响应变化。需要结合computed函数

![QQ截图20230208202551.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8c0b4ff956864757847c140b9c14d215~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230208202706.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/488828ef1f9947e1a1195be0d7c77b12~tplv-k3u1fbpfcp-watermark.image?)

父节点：
color：computer（（）=>this.color
子孙： 标签中color.value

## VUEX：管理共享组件的方案

![QQ截图20230208213704.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3242f5b152234bb5ae63751af56cffe3~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230208213945.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/eefdff4194e3493188cbf6ce7d6d38ed~tplv-k3u1fbpfcp-watermark.image?)

## vue3中全局配置axios

![QQ截图20230208215649.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7ab4aefcc9ac4d9bb0e7a2275dae3c94~tplv-k3u1fbpfcp-watermark.image?)

`axios.defaults.baseURL = 'https : / / www.escook.cn'
app.config.globalProperties.$http = axios`

# VUE3----继续2

## 购物车案例：

搭建基本组件后，在heater子组件里用props自定义属性，渲染样式：

```
<div class="heater-contaion" :style="{backgroundColor:bgcolor,color:color,fontSize:fsize+'px'}">{{ title }} </div>

.....
props:{
  title:{
    type:String,
    default:'es-header'
  },
  bgcolor:{
    type:String,
    default:'#007BFF'
  },
  color:{
    type:String,
    default:'#ffffff'
  },
  fsize:{
    type:Number,
    default:12
  }


  .......


  .heater-contaion{
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 45px;
  text-align: center;
  line-height: 45px;
  z-index: 999;
}
```

title在根组件传入数据  `<EsHeater title="购物车案例"></EsHeater>`

导入npm i axios -S
在main.js中import axios,把axios全局配置。
然后在app根组件导入数据，先在data中写一个空数组存数据，
在computed（）{}中预调用一个方法(方法名是自己起的)。 this.getGoodslist()调用这个方法就会发起请求拿到数据转存到goodslist:[]中。
在methodes中发起请求。

```
created(){
  this.getGoodslist()

},
methods:{
  async getGoodslist(){
    const {data:res}=await this.$http.get('/api/cart')
    if(res.status !==200) return alert('数据请求失败')
    //把列表数据转存到goodslist
    this.goodslist=res.list
  }
}
```

### 设置footer组件样式：

justify-content 属性用来设置项目在主轴方向上的对齐方式。

```
.container {
    justify-content: flex-start（默认值） | flex-end | center | space-between | space-around;
}
```

```
1. flex-start 沿着主轴方向 起点 对齐（默认值）。
2. flex-end 沿着主轴方向 结尾 对齐。
3. center 沿着主轴方向 居中 对齐。
4. space-between 沿着主轴方向 间隔 对齐，头尾没有间距。
5. space-around 沿着主轴方向 间隔 对齐，头尾有间距。
```

————————>主轴方向为横向
修改bootstrp的样式，在控制台选中样式修改后复制，导入自己代码组件中。

# CSS align-items 属性

居中对齐弹性盒的各项` <div> `
`align-items: center;

css中min-width属性是用于设置元素的最小宽度；该属性会对元素的宽度设置一个最小限制，所以元素可以比指定值宽，但不能比其窄，也不允许指定负值。`

min-width的应用：

当子元素宽度设置为父元素的30%，父元素宽度在减小时，子元素的宽度会跟着减小，但是子元素宽度太小时可能会导致内部元素错位等情况。在这种情况下可以设置min-width为一个固定的单位，如100px，当30%父元素的宽度已经小于100px时，子元素的宽度不会再减小，保持为100px。

把一些值通过props变成动态的（要接收根组件传过来的数据）
amount.toFixed(2)
amount表示总价格，toFixed(2)方法表示保留两位小数。

全选按钮需要根据状态选中，定义一个状态属性。(父传子)当根组件按钮全部选中后，会传给子组件状态，根据状态（true或false）选中全选按钮。
因为用户点击后(子传父)，就需要根据这个状态，使根组件里的按钮全选。用change事件，进行传` e.target.checked 是复选框最新的选中状态` 传到跟组件在一个事件中接收

> ## # HTML` <input>` 标签的 checked 属性定义和用法
> 
> checked 属性规定在页面加载时应该被预先选定的 input 元素。
> 
> checked 属性 与 <input type="checkbox"> 或 <input type="radio"> 配合使用。
> 
> checked 属性也可以在页面加载后，通过 JavaScript 代码进行设置。

> // 最终生成的选择器为 .goods-container + .goods-container
> 
> // 在 css 中，

> (+)是“相邻兄弟选择器”，表示：选择紧连着另一元素后
> 
> 的元素，二者具有相同的父元素。
> 
> ` + .goods-container {
> 
> border-top: 1px solid #efefef;
> 
> }`

### 求总价格：

要用机器的思维，求总价格最先看什么，先看勾选了几件商品，不勾选商品，计算也没用啊，机器就是一步一步来。勾选商品之后，再看商品数量。最后相加。

父传子：v-bind 自定义属性，子传父：v-on 自定义事件

../ 是跳到上上一层文件

*NaN*（Not a Number，非数）是计算机科学中数值数据类型的一类值，表示未定义或不可表示的值。
isNaN()  返回值是一个布尔值，true为NaN,false则不为NAN

parseInt() 函数可解析一个字符串，并返回一个整数。

```
 data(){
   return{
     number:this.num
   }
 }
 .....

  watch:{
   number(newVal){
     const parseResult =parseInt(newVal)
     if(isNaN(parseResult) || parseResult < 1){
       this.number = 1
       return
     }
     if(String(newVal).indexOf('.')!==-1){
       this.number = parseResult
       return
     }
   }
 }
```

用监听器watch,监听数据number,当数据变化时，watch会做出判断，把数据改成合理的值

# VUE3----继续3

## ref:

> 用来获取DOM元素或组件的引用  
> 如ref在h3标签上，ref属性可获取h3

![QQ截图20230212220923.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4a4fb98b0baf47b2923245a68ece02c8~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230212222120.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/326e36540c61468786b28be2c97330ec~tplv-k3u1fbpfcp-watermark.image?)

> 组件是异步更新DOM结构。（先执行js中代码在执行HTML页面元素。但这样js中代码声明的值是未定义的）

![QQ截图20230212222706.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/da838509f06c49a0ad848fa68fa560aa~tplv-k3u1fbpfcp-watermark.image?)

## 动态组件：

> 动态控制组件的显示与隐藏

![QQ截图20230212224249.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9f1b5050718742f1a26f353bb0143f6e~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230212224845.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/aab07c4bb58f4f6c9934f4be013494c2~tplv-k3u1fbpfcp-watermark.image?)

如果只有两个组件，因为组件刚开始先被创建，而后切换的时候，切换前的组件会被销毁。在切换，被销毁的组件又被创建，这样里面的值都会被重置。用`<keep-alive>`会防止里面的值被重置。

## 插槽：

插槽（Slot)是vue为组件的封装者提供的能力。允许开发者在封装组件时，把不确定的、希望由用户指定的部分定义为插槽。

可以把插槽认为是组件封装期间，为**用户预留的内容**的占位符。

在封装组件时，可以通过<slot>元素定义插槽，从而为用户预留内容占位符。示例代码如下:

子组件：

![QQ截图20230212230032.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6a289c8e79164ec9be93b5873d5a18da~tplv-k3u1fbpfcp-watermark.image?)

父组件内的子组件标签：p标签的内容就是slot标签内容。

![QQ截图20230212230115.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8bc2c81669b644d4b68210cfa8af3920~tplv-k3u1fbpfcp-watermark.image?)

封装组件时，可以为预留的<slot>插槽提供后备内容（默认内容）。如果组件的使用者没有为插槽提供任何内容，则后备内容会生效。示例代码如下:

```
<template>
<p>这是 MyCom1组件的第1个p标签</p>
<slot>这是后备内容</slot>
<p>这是 MyCom1组件最后一个p 标签</p>
</template>
```

当用户在插槽内输入内容，slot里的内容这不显示

![QQ截图20230212231211.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d9214128e35f417bab7435d10dc75c77~tplv-k3u1fbpfcp-watermark.image?)

> 如果填写的内容没用指定的名称，则会放在没用指定的名称的插槽default。

![QQ截图20230212231533.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/be101cf173464c50834b5086ec9c3edd~tplv-k3u1fbpfcp-watermark.image?)

v-slot 只能被用在组件内和`<template>`中。

跟v-on和v-bind一样，v-slot也有缩写，即把参数之前的所有内容(v-slot.)替换为字符#。例如v-slot:header可以被重写为#header

在封装组件的过程中，可以为预留的<slot>插槽绑定props 数据，这种带有props 数据的<slot>叫做“作用域插槽”。

![QQ截图20230212232644.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6b55858df08e4e01a33721633c655a1e~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230212232706.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/74f99f3eb2984434994fb9e7a988b551~tplv-k3u1fbpfcp-watermark.image?)

 子组件传给父组件值（传给插槽），父组件子定义接收参数。

 解构作用域插槽的**prop**：

![QQ截图20230212233420.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d0df332a4eab4838bb96ea1176bf4160~tplv-k3u1fbpfcp-watermark.image?)

$event 代表传过来的数据。$event是事件发送者传过来的参数，可以防止在处理函数中被其他参数覆盖掉

![QQ截图20230213220607.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4fa243d9e7884051845296f10af89425~tplv-k3u1fbpfcp-watermark.image?)

# VUE3-----继续4

`<input type="text" class="form-control" v-focus />`

![QQ截图20230213103016.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1eaf37d733634cb0bc904592a0d300b4~tplv-k3u1fbpfcp-watermark.image?)

全局自定义指令：在main.js中写入
![QQ截图20230213111731.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/34db05bdf22745bebd9ca749b3085602~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230213112135.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/52037dafe1014232b90dfedcb7d3dabb~tplv-k3u1fbpfcp-watermark.image?)

注意:在vue2的项目中使用自定义指令时， 【mounted -> bind 】 【 updated ->update】

当业务相同是可简写成一个：
![QQ截图20230213112515.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d6672c0749554006bfbbfa9084f1c372~tplv-k3u1fbpfcp-watermark.image?)

binding绑定的参数,用于同一个指令传不同的参数。
![QQ截图20230213112838.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5ac4de3759044efd9daa129ec3924ccf~tplv-k3u1fbpfcp-watermark.image?)

@keyup.enter="",@keyup.esc="",键盘事件

## 路由

![QQ截图20230214142926.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0df90f56307e48f3baa8d5c3660d118c~tplv-k3u1fbpfcp-watermark.image?)

   SPA指的是一个web网站只有唯一的一个 HTML页面，所有组件的展示与切换都在这唯一的一个页面内完成此时，不同组件之间的切换需要通过前端路由来实现。

结论:在SPA项目中，不同功能之间的切换，要依赖于前端路由来完成!

什么是前端路由：
通俗易懂的概念: Hash地址与组件之间的对应关系。Hash地址发生变化，组件进行切换（相当于页面切换）

![QQ截图20230214143752.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/43e0cca8e3fc484c88921ee9b4496dac~tplv-k3u1fbpfcp-watermark.image?)

location.hash：拿到当前hash值。

```
created() {
//监听hash值变化的事件
window. onhashchange = ( =>{
//通过location.hash 获取到最新的hash 值，并进行匹配
switch (location.hash) {
case '#/home ' :
this.comName = 'MyHome'break
case ' #/movie' :
this.comName = 'MyMovie'break
case '# / about' :
this.comName = 'MyAbout'break
}
```

![QQ截图20230214151748.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8596264e6f534e7a9d5640a747eba131~tplv-k3u1fbpfcp-watermark.image?)

路由占位符相当于放置展示组件的切换。

![QQ截图20230214153133.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ff647a327c2f43cdb15fce1208fae012~tplv-k3u1fbpfcp-watermark.image?)

```
// 3．创建路由实例对象
const router = createRouter({
// 3.1通过 history属性指定路由的工作模式
history: createwebHashHistoryo(),
// 3.2通过routes 数组，指定路由规则
routes: [
 //  path 是 hash 地址，component是要展示的组件
 { path: '/home ',component: Home },
 { path: '/movie',component: Movie },
 { path: ' /about ' , component: About },
 ],
})
```

在main.js中

```
import router from './ components/02.start/router'
const app = createApp (App)
//挂载路由模块
app.use(router)
I
app. mount( ' #app ')
```

> 流程：
> 当点击连接，hash地址发生变化，就会被路由模块监听到（router.js），进行匹配hash地址，匹配成功后，把匹配成功的component对应的组件，放到路由占位符的位置进行呈现。

![QQ截图20230214220954.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/79b9d53c0ce041b69addd8ba58863790~tplv-k3u1fbpfcp-watermark.image?)

1.
默认的高亮class类:  
被激活的路由链接，默认会应用一个叫做 router-link-active 的类名。开发者可以使用此类名选择器，为激活的路由链接设置高亮的样式.

2.
![QQ截图20230214224646.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/07860199fccf4468bcf2c5c4fd987d04~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230214225254.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d2bfe6e0325c4d2fbdb75f3e1ad6d493~tplv-k3u1fbpfcp-watermark.image?)

1.声明子路由链接和子路由占位符  
2.在父路由规则中，通过children属性嵌套声明子路由规则

![QQ截图20230214225838.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/538503d2cdbf4b18b90951b6cc5b40e3~tplv-k3u1fbpfcp-watermark.image?)

```
 routes:[
   {path:'/',redirect:'/MyHome'},
   {
     path:'/MyHome',
     component:MyHome,
     children:[
     {path:'MyTabs1',component:MyTabs1},
     {path:'MyTabs2',component:MyTabs2}
   ]},
```

嵌套路由里路由重定向：

```
{
  path:'/MyHome',
  component:MyHome,
  redirect:'/MyHome/MyTabs1',
  children:[
  {path:'MyTabs1',component:MyTabs1},
  {path:'MyTabs2',component:MyTabs2}
]},
```

在子路由中  
` {path:'MyTabs2',component:MyTabs2}`
`{path:'user/:id',component:MyUserDetail,props:true}`

hash地址前面不加 '/'

## 动态路由：

![QQ截图20230215131200.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d1fac83a859543d6b6bae87f5a0d2d1e~tplv-k3u1fbpfcp-watermark.image?)

### 路由参数获取方式：

1. 通过动态路由匹配的方式渲染出来的组件中，可以使用$route.params对象访问到动态匹配的参数值。

```
<template>
<!-- $route.params是路由的“参数对象”-->
<h3>MyMovie组件--- {{$route.params.id}}</h3></template>
<script>
export default {name: 'MyMovie ',
< / script>
```

2. 为了简化路由参数的获取形式，vue-router允许在路由规则中开启props传参。

```
// 1、在定义路由规则时，声明props : true选项，
//即可在 Movie 组件中，以 props的形式接收到路由规则匹配到的参数项
{ path: '/movie/:id', component: Movie, props: true}
<template>
<!-- 3、直接使用props中接收的路由参数-->
<h3>MyMovie组件--- {{id}}</h3>
</template>

<script>
export default {
props: [ 'id'] //2、使用props接收路由规则中匹配到的参数项
</script>
```

>    通过调用API实现导航的方式，叫做编程式导航。与之对应的，通过点击链接实现导航的方式，叫做声明式导航。例如:
> 普通网页中**点击**`<a>`**链接**、vue项目中点击`<router-link>`都属于声明式导航，
> 普通网页中调用location.href 跳转到新页面的方式，属于编程式导航

> vue-router提供了许多编程式导航的API，其中最常用的两个API分别是:  

> `this.$router.push('hash地址')`
> 跳转到指定Hash地址，从而展示对应的组件

> `this.$router.go(数值n)`
> 实现导航历史的前进、后退

调用this.$router.push()方法，可以跳转到指定的 hash地址，从而展示对应的组件页面。示例代码如下:

```
<template>
<h3>MyHome组件</h3>
<button @click="gotoMovie(3)">go to Movie</button></template>
<script>
export default {
methods : {
gotoMovie(id) { 
// id参数是电影的id值
this.$router.push(`/movie/${id}`)}，
},}
</script>
```

调用this.$router.go()方法，可以在浏览历史中进行前进和后退。示例代码如下

```
<template>
<h3>MyMovie组件--- {{id}}</h3>
<button @click="goBack">后退</button></template>
<script>
export default {
props: [ 'id'],
methods: {
goBack() { this.$router.go(-1)}//后退到之前的组件页面
}，
}
</script>
```

通过name属性为路由规则定义名称的方式，叫做命名路由。
实现声明式导航
示例代码如下:

```
{
path: '/movie/:id' ,
//使用name属性为当前的路由规则定义一个“名称”
name: 'mov',
component: Movie,
props: true,
}
```

注意:命名路由的name值不能重复，必须保证唯一性!

![QQ截图20230215161619.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5b2e228de6a6454c9113cb7a2ca2f913~tplv-k3u1fbpfcp-watermark.image?)

> 在router-link里不在写hash地址，而是写一个对象里面填name属性和id，to要动态绑定。

路由规则：
` { name:'zs',path:'/MyMovie/:id',component:MyMovie,props:true}`

router-link相当于a链接，那个组件需要跳转在哪个组件里添加router-link链接。

#### 使用命名路由实现编程式导航

调用push 函数期间指定一个配置对象，name是要跳转到的路由规则、params是携带的路由参数:

```
<template>
<h3>MyHome组件</h3>
<button @click="gotoMovie(3)">go to Movie</button></template>
<script>
export default {
methods: {
gotoMovie(id){
this.$router.push({ name: 'mov', params: {id:3}})},
}，}
</scrint>
```

两种导航的命名路由格式大致相同。当hash地址较长时，就用命名路由。

# VUE3----继续5

![QQ截图20230215165414.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d4e7ffac7b814a47beff5ce79ab8b2e9~tplv-k3u1fbpfcp-watermark.image?)

> route是路由信息对象，每一个路由都会有一个route对象，是一个局部的对象,里面主要包含路由的一些基本信息，比如name、meta、path、hash、query、params、fullPath、matched、redirectedFrom...

> router是VueRouter的实例，通过Vue.use(VueRouter)和VueRouter构造函数得到一个router的实例对象，这个对象中是一个全局的对象，他包含了所有的路由包含了许多关键的对象和属性

![QQ截图20230215170639.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6fb69961198d458e8a2b2556f0bb57f7~tplv-k3u1fbpfcp-watermark.image?)

> 在守卫方法中如果不声明next形参，则默认允许用户访问每一个路由!

> 在守卫方法中如果声明了next 形参，则必须调用next()函数，否则不允许用户访问任何一个路由!

> 直接放行:next()  
> 强制其停留在当前页面:next(false)  
> 强制其跳转到登录页面:next('/login')

导航守卫会监听用户登陆状态，如果未登录，next('/login')会强制其跳转到登录页面。如果处于登陆状态，next() 直接放行

```
//全局路由导航守卫
router.beforeEach((to，from，next) =>{
if (to.path === '/main') {
//证明用户要访问后台主页
next('/ login')
}else {
//访问的不是后台主页
next()
}
```

token 这是指浏览器内是否存有登入的用户信息,就是登录状态，后端给的.

![QQ截图20230215172121.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7a4848115779427abae9a7092cf1a2f2~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230217113100.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/dcead449389e44799e0b444e55c71191~tplv-k3u1fbpfcp-watermark.image?)

# VUE3-----继续6--配置内容

> vue-cli（俗称: vue脚手架）是vue官方提供的、快速生成 vue工程化项目的工具。  
> 特点:  
> ①开箱即用  
> ②基于webpack  
> ③功能丰富且易于扩展  
> ④支持创建vue2和vue3的项目

![QQ截图20230218101008.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8cb35342d83b409499839a87f804872b~tplv-k3u1fbpfcp-watermark.image?)

> vue-cli 提供了创建项目的两种方式:  
> 1 #基于【命令行】的方式创建vue项目  
> vue create项目名称    

> 2#基于【可视化面板】创建vue项目
> vue ui

> 在vue2的项目中，只能安装并使用3.x版本的vue-router。  
> 版本3和版本4的路由最主要的区别:创建路由模块的方式不同!

![QQ截图20230218110045.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b893fe4a64d046d3806d51791f6ef894~tplv-k3u1fbpfcp-watermark.image?)

在实际开发中，前端开发者可以把自己封装的.vue组件整理、打包、并发布为npm 的包，从而供其他人下载和使用。这种可以直接下载并在项目中使用的现成组件，就叫做vue 组件库。

**网页端用element-ui，移动端用vant**

> bootstrap只提供了纯粹的原材料（css样式、HTML结构以及」S特效），需要由开发者做进一步的组装和改造 .    
> vue组件库是遵循vue语法、高度定制的现成组件，开箱即用.

3.最常用的vue组件库  
PC端:   
Element Ul ( https://lelement.eleme.cn/#/zh-CN)  
View ul ( http://v1.iviewui.com/)   

移动端:  
Mint ul ( http://mint-ui.github.io/#!/zh-cn)   
Vant ( https://vant-contrib.gitee.io/vant/#/zh-CN/ )

Element Ul是饿了么前端团队开源的一套PC端vue组件库。支持在vue2和vue3的项目中使用:   

 vue2的项目使用旧版的Element UI ( https://element.eleme.cn/#/zh-CN   

vue3的项目使用新版的Element Plus (https://lelement-plus.gitee.io/#/zh-CN)

开发者可以一次性完整引入所有的element-ui组件，或是根据需求，只按需引入用到的element-ui组件  

完整引入:操作简单，但是会额外引入一些用不到的组件，导致项目体积过大

按需引入:操作相对复杂一些，但是只会引入用到的组件，能起到优化项目体积的目的

vue2中使用：

#### 完整引入

![QQ截图20230218111443.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8362496ff6d24531a7c1dedc6ef0bacc~tplv-k3u1fbpfcp-watermark.image?)

#### 按需引入

借助 [babel-plugin-component](https://github.com/QingWei-Li/babel-plugin-component)，我们可以只引入需要的组件，以达到减小项目体积的目的。

首先，安装 babel-plugin-component：

> npm install babel-plugin-component -D

然后，将 .babelrc 修改为(在babel.config.js文件中写入)：

```
{ "presets": [["es2015", { "modules": false }]], "plugins": [
[ 
"component", 
{
"libraryName": "element-ui", 
"styleLibraryName": "theme-chalk" 
} 
] 
]
} 
```

接下来，如果你只希望引入部分组件，比如 Button 和 Select，那么需要在 main.js 中写入以下内容：

```
import Vue from 'vue';
import { Button, Select } from 'element-ui'; 
import App from './App.vue';

Vue.component(Button.name, Button); 
Vue.component(Select.name, Select);

/* 或写为 
** Vue.use(Button) 这种写法比较常用
* Vue.use(Select) 
*/ 

new Vue({
el: '#app', 
render: h => h(App)
});
```

把组件的导入和注册封装为独立的模块  
在src目录下新建element-ui/index.js模块，并声明如下的代码:

```
//→模块路径/src/element-ui/index.js
import Vue from 'vue'
//按需导入 element ui的组件
import { Button，Input } from 'element-ui'
//注册需要的组件
Vue.use(Button)
Vue.use( Input)
//→在main.js 中导入
import '.lelement-ui'
```

![QQ截图20230218175408.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e4da242da5b94a76a582fa6984593dda~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230218175435.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/329ea6be348241e69c0d4ad28d06d32f~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230218175828.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/29afe5cf3624438195e6993a23431250~tplv-k3u1fbpfcp-watermark.image?)

> **在main.js中写：**

![QQ截图20230218180003.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/20a17e19f1f44e488bcc1d41c87bb6e1~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230218224359.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b60f6fd17c0e4f5088746c496a72fd9d~tplv-k3u1fbpfcp-watermark.image?)

> 请求

![QQ截图20230218224757.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1ac8967fbbcb45cdb17a7223b7f35ec5~tplv-k3u1fbpfcp-watermark.image?)

> Fullstreen表示全屏。    
> 请求之后需要响应。

![QQ截图20230218225101.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b9ef1a27fcbe473791ba78043d73eab3~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230218225140.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d6e7073fd5e442d596d9920ae92db32c~tplv-k3u1fbpfcp-watermark.image?)

### proxy 跨域代理

![QQ截图20230218231152.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/02bacd62ef664561a6f256abb7270977~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230218231422.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8f8b52524dfe46a78095e623d5e022e5~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230218231505.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1868f8e3ca2c440290cd497f8327c5f3~tplv-k3u1fbpfcp-watermark.image?)

> 注意:   
> devServer.proxy提供的代理功能，仅在开发调试阶段生效  
> 
> 项目上线发布时，依旧需要API接口服务器开启CORS跨域资源共享

**修改端口号并自动打开浏览器：** 

![QQ截图20230219150526.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/965d95e7a7cb4794b016c68dfdec472b~tplv-k3u1fbpfcp-watermark.image?)

我自己的浏览器打开：

```
const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({
  transpileDependencies: true,
  devServer: {
    // 修改dev期间的端口号
    port: 3000,
    // 自动打开浏览器
    open: true,
    host: 'localhost'
  }
})
```

# VUE--后续

vue2-->vue-router@3.x  
vue3-->vue-router@4.x  
在router3.x官网即使默认安装，也会是4.x版本，用vue2时最好指定版本号。

### 

### 在Element-ui中

添加索引列：
` <el-table-column type="index" label="#"></el-table-column>  
`    
通过 `Scoped slot` 可以获取到 row, column, $index 和 store（table 内部的状态管理）的数据，
如row可获得列表数据。

组件库中如Element-ui中，`<el-table :data="userList" stripe  border>`  

**el-table**即为类名。

`trigger:'blur'`失去焦点自动触发。

```
 <el-form-item label="用户名称" prop="name">
   <el-input v-model="form.name"></el-input>
```

验证规则：prop里的'name与from的属性一致。

当在列表添加新数据后，需要发起Ajax(post)请求，添加之后，需要再次调用初始发起请求的方法。

```
this.$message.info('取消了删除')    
 this.$message.success('删除成功')   
 this.$message.error('发送数据失败')
```

![QQ截图20230220163258.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7a9c10078bf84bbdbb659371dd277214~tplv-k3u1fbpfcp-watermark.image?)
