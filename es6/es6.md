# ES6--知识

## 1.箭头函数面试题

```
var obj ={
age:20,
say:()=>{
alert(this.age)
}
}
obj.say();
```

   因为obj是一个对象，**对象没有作用域**，所以箭头函数的指向不是obj，箭头函数被定义在全局作用域下，箭头函数指向window，而window没有age属性,所以弹出警示框为undefined.

```
var age =10;
var obj ={
age:20,
say:()=>{
alert(this.age)
}
}
obj.say();
```

加上`var age =10;`后var声明的变量在全局作用域下，window就有了age。弹出的值为10.

## 2.箭头函数里的this指向

```
const obj ={name:'zs'}
 function fn(){
   console.log(this);
   return ()=>{
     console.log(this);
   }
 }
  let fea =fn.call(obj)
 fea()
```

1. 箭头函数里的this指向fn
2. fn通过call调用并把this指向obj
3. fn返回值是一个箭头函数，而返回值又赋值到fea,所以调用fea就是调用箭头函数
4. 由于fea返回值（`return`）为箭头函数，箭头函数有指向fn,fn有指向obj,所以两次打印都是obj对象

## 3.查询商品案例----forEach,filter,some的运用

> 主要代码：

```//
 // 1.把数据用tr放在tbody里面，获取tbody，用forEach遍历data里面的数据，用createElement创建tr,在tr里面用
innerHTML添加td数据，把tr用appendChild放到tbody里面。
 var tbody = document.querySelector('tbody')
 var search_price = document.querySelector('.search-price')
 var end = document.querySelector('.end')
 var start = document.querySelector('.start')
 var product = document.querySelector('.product')
 var search_pro = document.querySelector('.search-pro')
 setData(data)
 // 封装渲染页面的方法（把数据传到页面）
 function setData(mydata) {
   //不能放在forEach里面不然遍历一遍清空一边，最后只生成一条数据
   tbody.innerHTML = ''
   mydata.forEach(function (value) {
     // console.log(value);
     var tr = document.createElement('tr')
     tr.innerHTML = '<td>' + value.id + '</td><td>' + value.pname + '</td><td>' + value.price + '</td>'
     tbody.appendChild(tr)
   });
 }
 // 2.带点击按钮，根据商品价格筛选数组里的对象
 // 3.把点击后的数据渲染到页面上
 // 遍历最后如果有条件都需要return
 search_price.addEventListener('click', function () {
   var newData = data.filter(function (value) {
     // console.log(value);
     // start.value 添加数据的值
     return value.price <= end.value && value.price >= start.value
   })
   setData(newData)
 })
 //  4.点击按钮查询上商品，用some查找唯一值,some返回值为布尔值，需要return true
 search_pro.addEventListener('click', function () {
   // 把匹配的值（用户填写的值）放进一个数组便于调用
   var arr = []
   data.some(function (value) {
     if (value.pname === product.value) {
       arr.push(value)
       return true
     }
   })
   setData(arr)
 })
```

forEach和filter一样不会终止遍历。

## 4.函数

- 所有的函数都是Function的实例对象
- 所有的函数都是Function创建出来的

![QQ截图20230205205302.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a024e0c63f84427a915fa857c6a4b867~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230205212337.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/880081e1ce6f41d3872e98c9b4ea072d~tplv-k3u1fbpfcp-watermark.image?)

# ES6---知识2

## 一.闭包应用

### 1.点击i输出索引号

```
<ul>
    <li>苹果</li>
    <li>梨</li>
    <li>香蕉</li>
    <li>橘子</li>
</ul>
<script>
var lis = document.querySelector('ul').querySelectorAll('li')
for(var i=0; i<lis.length;i++){
lis[i].onclick(function(){
console.log(i)
})
</script>
```

但实际上打印结果都为4，因为`for`循环是同步任务，会立即执行，最终执行到`i`为4时停止，所以每次点击都为4.

解决方法1：

```
var lis = document.querySelector('ul').querySelectorAll('li')
for(var i=0; i<lis.length;i++){
lis[i].index= i;
lis[i].onclick(function(){
console.log(this.index)
})
```

使用动态添加属性的方式` lis[i].index= i;`

解决方法2：

```
for(var i=0; i<lis.length;i++){
（function(i){
    lis[i].onclick(function(){
console.log(i)
})(i)
}
```

利用闭包方式，for循环创建4个立即执行函数。

### 2.打车价格--闭包应用

![QQ截图20230206110926.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/08947b23a34c4adcbe8e263b9f012b49~tplv-k3u1fbpfcp-watermark.image?)

```
var car=(function(){
    var start =13;
    var total=0;
    return{
    commonprice:function(n){
    if(n<3){
    total=13
    }else{
    total=start+(n-start)*5
    }
    return total
    jamprice:function(flag){
    return flag? total+10:total
    }
})()
console.log(car.commonprice(5)) //23
console.log(car.jamprice(true)) //33
```

### 3.闭包题

> 闭包产生的前提：外层函数必须有变量

![QQ截图20230206113918.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a21b527293da4d2cbd1ea395959196ad~tplv-k3u1fbpfcp-watermark.image?)

> 输出的为：`The Window`
> 把`object.getNmaeFunc()()`拆解

![QQ截图20230206114119.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/edb424d2da084d6198381e3c359d5f78~tplv-k3u1fbpfcp-watermark.image?)

> 拆解后为：` f()() `相当于一立即执行函数，而立即执行函数`this`指向`window`

![QQ截图20230206114734.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/efca2d34c12f40179f91349ffcb49d53~tplv-k3u1fbpfcp-watermark.image?)

这个题在外部函数有变量` var that = this;`
所以产生闭包。因为` return that.name;` 中的that是变量与` var that = this;`的that相对应（是同一个that）。所以指向obj.

## 二.递归

> 闭包：能够读取其他函数内部变量的函数；     
> 作用：延伸变量的作用范围。

> 递归：函数可以在内部调用其本身（函数在内部自己调用自己）。   
> 作用：和循环效果一样。

> 递归里必须加return跳出循环（如果这个条件本身可以自己结束循环则不需要加return）

详细作用看纸质笔记。。。。

## 三.浅拷贝和深拷贝

### 1.浅拷贝

浅拷贝只是拷贝一层，更深层次对象只拷贝地址。

```
var obj ={
id:1,
name:'zs',
msg:{
age:18
}
}
var o={}
```

方法1

```
 for(var k in obj ){
   // k是属性名，obj[k]是属性值
   o[k]=obj[k]
 }
 console.log(o);
```

方法2

```
  Object.assign(o,obj)
  console.log(o);
```

> `msg `就是更深层次对象，只拷贝地址的意思是：当拷贝后的`o`对象修改属性值时`obj`里的**属性值**也会改变。

### 2.深拷贝

   每个级别的数据都会被拷贝，当拷贝后的对象的数据发生变化后，不影响原对象的数据。

>    **用法如下**：

![QQ截图20230206131740.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4e1a0651154b483c9f0140ffcac0d651~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230206131402.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3e2548a03def4b4f9d06ab3ad170446f~tplv-k3u1fbpfcp-watermark.image?)

![QQ截图20230206131812.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c320f75d7a9242f6a65352ddcc449fe3~tplv-k3u1fbpfcp-watermark.image?)

>   这里的深拷贝是一层套一层，比如一个函数里面套着一个对象，对象里面又套着一个数组，但最里面一层都是一个简单数据类型，通过递归的方法，可以从最面复制，在一层一层复制。

## 四.正则表达式

> input文本框中输入的值就是value。

### 1.用户名验证

![QQ截图20230206144915.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c9f7a8ab4c024326825c35b277ff0cda~tplv-k3u1fbpfcp-watermark.image?)

## 五.ES6面向对象知识点

> 1.es6中插入元素

```
 that.ul.insertAdjacentHTML('beforeend',li)
```

2.`e.stoppropagation`阻止冒泡

3.`remove()` remove可以删除指定元素

4.`ondblclick` 双击事件

5.双击禁止选中文字

![QQ截图20230207113538.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/44af1820e37540aeb873cf414fa9d7fd~tplv-k3u1fbpfcp-watermark.image?)

6.`input.select()` 让文本框文字处于选中状态

array.reduce(function(total, currentValue, currentIndex, arr), initialValue); /* total: 必需。初始值, 或者计算结束后的返回值。 currentValue： 必需。当前元素。 currentIndex： 可选。当前元素的索引； arr： 可选。当前元素所属的数组对象。 initialValue: 可选。传递给函数的初始值，相当于total的初始值。 */

```
array.reduce(function(total, currentValue, currentIndex, arr), initialValue);
/*
  total: 必需。初始值, 或者计算结束后的返回值。
  currentValue： 必需。当前元素。
  currentIndex： 可选。当前元素的索引；                     
  arr： 可选。当前元素所属的数组对象。
  initialValue: 可选。传递给函数的初始值，相当于total的初始值。
*/
```

# ES6--后续

## 1.Symbol

   ES6 引入了一种新的原始数据类型 Symbol ，表示独一无二的值，最大的用法是用来定义对象的唯一属性名。

Symbol为ES6新增的基本数据类型，表示独一无二的值。  
**Symbol()函数会返回symbol类型的值，每个从Symbol()返回的symbol值都是唯一的。**  
*Symbol.for() 返回由给定的 key 找到的 symbol，否则就是返回新创建的 symbol*

```
 const s = Symbol();
 console.log(typeof s); // "symbol"
```

   即使是传入相同的参数，生成的 symbol 值也是不相等的，因为 Symbol 本来就是独一无二的意思

```
const foo = Symbol('foo'); const bar = Symbol('foo'); console.log(foo === bar); // false
```

## 正则表达式（Regular Expression）

是用于匹配字符串中字符组合的模式。   
通常用来查找、替换那些符合正则表达式的文本，许多语言都支持正则表达式。

2.正则表达式有什么作用?   
表单验证（匹配）  
过滤敏感词（替换)    
字符串中提取我们想要的部分（提取)

1.定义正则表达式语法:  
const 变量名=/表达式/

2.判断是否有符合规则的字符串:  
test()方法用来查看正则表达式与指定的字符串是否匹配,返回true或false

3.检索（查找）符合规则的字符串;
exec()方法在一个指定字符串中执行一个搜索匹配,匹配成功返回数组，否则返回null

什么是元字符以及它的好处是什么?   
是一些具有特殊含义的字符，可以极大提高了灵活性和
强大的匹配功能     
比如英文26个英文字母，我们使用元字符[a-z]简介和灵活

元字符分三大类：  
边界符（表示位置，开头和结尾，必须用什么开头，用什么结尾)   
量词（表示重复次数)   
字符类(比如\d 表示0~9)

### 边界符

^  表示匹配行首的文本(以谁开始)   
$  表示匹配行尾的文本(以谁结束)

![QQ截图20230402145714.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/896f9053f5b845c28b6bb1e0fa88cab9~tplv-k3u1fbpfcp-watermark.image?)

字符类:
[ ]里面加上–连字符使用连字符 – 表示一个范围

比如:
[a-z]表示a 到z 26个英文字母都可以[a-zA-Z]表示大小写都可以  
[0-9]表示0 ~ 9的数字都可以

```
[1-9][0-9]{4,}$

大括号匹配最近的次数
```

[ ]里面加上 ^ 取反符号比如:  
[a-z] 匹配除了小写字母以外的字符注意要写到中括号里面

预定义:指的是某些常见模式的简写方式。
![QQ截图20230402151344.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1ab6542c14cd4b81b4bc56070e090a40~tplv-k3u1fbpfcp-watermark.image?)

### 修饰符

语法:   
/表达式/修饰符

i是单词ignore的缩写，正则匹配时字母不区分大小写   
g是单词global的缩写，匹配所有满足正则表达式的结果

替换replace替换  
语法:  
字符串.replace(/正则表达式/，'替换的文本')   
| 为或的意思

**正则表达式中的小括号"()"。是代表分组的意思。 如果再其后面出现\1则是代表与第一个小括号中要匹配的内容相同。**

> $1代表第一个分组

## 局部作用域

局部作用域分为函数作用域和块级作用域   
函数作用域：在函数内部  
块级作用域：使用{}包裹的代码   
局部作用域声明的变量外部不能使用  

## 全局作用域

`<script>`标签和.js文件的【最外层】就是所谓的全局作用域，在此声明的变量在函数内部也可以被访问全局作用域中声明的变量，任何其它作用域都可以被访问

## 作用域链本质上是底层的变量查找机制。

在函数被执行时，会优先查找当前函数作用域中查找变量   
如果当前作用域查找不到则会依次逐级查找父级作用域直到全局作用域
嵌套关系的作用域串联起来形成了作用域链   
相同作用域链中按着从小到大的规则查找变量   
子作用域能够访问父作用域，父级作用域无法访问子级作用域

![QQ截图20230402172552.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7b9352f0c91e4bb7bb9399e11143ae46~tplv-k3u1fbpfcp-watermark.image?)

堆栈空间分配区别:   
1.栈（操作系统）∶由操作系统自动分配释放函数的参数值、局部变量等，基本数据类型放到栈里面。   
⒉.堆（操作系统）∶一般由程序员分配释放，若程序员不释放，由垃圾回收机制回收。复杂数据类型放到堆里面。

两种常见的浏览器垃圾回收算法:引用计数法和标记清除法

### IE采用的引用计数算法

，定义“内存不再使用”，就是看一个对象是否有指向它的引用，没有引用了就回收对象   
算法:   
1.跟踪记录被引用的次数   
2．如果被引用了一次，那么就记录次数1,多次引用会累加++3．如果减少一个引用就减1 --  
4．如果引用次数是0，则释放内存

#### 缺点

但它却存在一个致命的问题:嵌套引用（循环引用)   
如果两个对象相互引用，尽管他们已不再使用，垃圾回收器不会进行回收，导致内存泄露。  
因为他们的引用次数永远不会是0。这样的相互引用如果说很大量的存在就会导致大量的内存泄露

## 标记清除算法

1.标记清除算法将“不再使用的对象”定义为“无法达到的对象”。    
2．就是从根部（在JS中就是全局对象）出发定时扫描内存中的对象。凡是能从根部到达的对象，都是还需要使用的。  
3．那些无法由根部出发触及到的对象被标记为不再使用，稍后进行回收。

![QQ截图20230402173910.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d5ba3c4c96d44696b0a42772f7521bda~tplv-k3u1fbpfcp-watermark.image?)

> 闭包=内层函数＋外层函数的变量

闭包的作用?
封闭数据，实现数据私有，外部也可以访问函数内部的变量  
闭包很有用，因为它允许将函数与其所操作的某些数据（环境）关联起来

闭包可能引起的问题?  
内存泄漏

## 变量提升

把声明的变量提升到最前面,变量赋值不提升
它允许在变量声明之前即被访问（仅存在于var声明变量)

```
console.log(str)
var str =1
相当于
var str
console.log(str)
str =1
```

变量在var声明之前即被访问，变量的值为undefined

## 函数提升

只提升函数声明，不提升函数调用

函数表达式不存在函数提升

```
var fun =function(){}
```

### 动态参数

当不确定传递多少个实参的时候，用arguments

arguments是**函数内部内置**的伪数组变量，它包含了调用函数时传入的所有实参   
arguments是一个**伪数组**，只存在于函数中arguments的作用是动态获取函数的实参   
可以通过for循环依次得到传递过来的实参   
arguments是一个**伪数组**，只存在于函数当中。

```
 function sum(){
   let s=0
   for (let i = 0; i < arguments.length; i++) {
     s+=arguments[i]

   }
   console.log(s);
 }
 sum(10,22)  //32
```

### 剩余参数

目标:能够使用剩余参数   
...是语法符号
剩余参数允许我们将一个不定数量的参数表示为一个数组
只存在于函数当中

```
function str(...arr){
  console.log(arr);
}
str(11,22)
```

...是语法符号，置于最末函数形参之前，用于获取多余的实参  借助...获取的剩余实参，是个真数组   
开发中，还是提倡多使用剩余参数。

### 展开运算符

目标:能够使用展开运算符并说出常用的使用场景       
展开运算符(...),将一个 **数组进行展开**   
不会修改原数组

```
const arr = [1，5，3，8，2]
console.log(. ..arr)// 1 53 8 2

求最大值
const arr = [1，5，3，8，2]
//console.Log ( ...arr)  // 1 5 3 8 2
console. log(Math.max ( ...arr)) //8 console.log(Math.min(...arr))   // 1

合并数组
const arr1 = [1，2，3]
const arr2 =[4，5，6]
const arr3 = [...arr1,...arr2] 
console.log(arr3)  //  [1,2,3,4,5,6]
```

箭头函数里面有arguments动态参数吗?可以使用什么参数?
没有arguments动态参数   
可以使用剩余参数  
箭头函数不会创建自己的this,它只会从自己的作用域链的上一层沿用this。

### 数组解构

数组解构是将数组的单元值快速批量赋值给一系列变量的简洁语法。

```
 const arr=[1,2,3]
 const [a,b,c,d]=arr
 console.log(a); // 1
 console.log(d); //undefined

  // 数组解构 交换变量
 let brr=[1,2,3];
 let [a,b,c,d]=brr;
 [a,b]=[b,a];
 console.log(a);
 console.log(b);
```

## js 前面必须加分号情况

```
1.立即执行函数
( function t() { })();
//或者
; (function t() { })()

2．数组解构
//数组开头的，特别是前面有语句的一定注意加分号
;[b, a] = [a, b]
```

## 对象解构

```
1。对象解构的变量名可以重新改名旧变量名:新变量名
const { uname: username,age } = { uname: 'pink老师', age: 18 }
console.Log(username)
console.Log(age)

//数组
const pig = [{
uname :'佩奇',age: 6
} 
]
const [{ uname,age }] = pig
console.log(uname)  // 佩奇
console.log(age)  // 6
```

#### 多级对象解构

```
const people = [{
name:'佩奇',family: {
mother:猪妈妈',father: '猪爸爸',sister:,、'乔治'},
age: 6}

const [{ name，family: { mother，father, sister }}]= person 
```

> forEach就是遍历加强版的for循环

## a链接事件对象

e.target.dataset.index (a链接的索引)
e.target.tagName='A' （判断对a链接操作）

> H5新增element.dataset.index或者element.dataset['index’ ] ie 11才开始支持

## 创建构造函数

```
//创建一个猪构造函数
function Pig(uname, age){this.uname
this.age = age}
new Pig('佩奇',6)
```

> 通过构造函数创建的对象称为实例对象，实例对象中的属性和方法称为实例成员
> （实例属性和实例方法)

> 构造函数的属性和方法被称为静态成员（静态属性和静态方法)

使用new关键字调用函数的行为被称为实例化  
实例化构造函数时没有参数时可以省略()   
构造函数内部无需写return，返回值即为新创建的对象  
构造函数内部的return返回的值无效，所以不要写return   
new Object ( ) new Date ( )也是实例化构造函数  

### 静态方法

Object.keys静态方法获取对象中所有属性（键)   
Object.values静态方法获取对象中所有属性值（值)   
Object. assign静态方法常用于对象拷贝（常用于添加属性）

```
 Object.assign(o,{gander:'女'})
```

返回的是一个数组

```
 const o ={ name:'撒啊',age:14}
 const sd =Object.keys(o)
 const sb =Object.values(o)
 console.log(sd);
```

## Array

reduce返回累计处理的结果，经常用于求和等
如果有初始值，上一次值就是初始值。

```
arr.reduce(function(){}，起始值)
arr.reduce(function(上一次值，当前值){}，初始值)

 const ad = [1, 3, 5]
 const adc = ad.reduce(function (a, b) {
   return a + b
 }, 10)
 console.log(adc);  //  19
```

> 构造函数方法很好用，但是存在浪费内存的问题,因为不同的实例对象，会用不同的地址。

原型会解决上述问题

# 原型

构造函数通过原型分配的函数是所有对象所共享的。  
JavaScript 规定，每一个构造函数都有一个prototype属性，指向另一个对象，所以我们也称为原型对象    
这个对象可以挂载函数，对象实例化不会多次创建原型上函数，节约内存   
我们可以把那些不变的方法，直接定义在 prototype对象上，这样所有对象的实例就可以共享这些方法。   
构造函数和原型对象中的this都指向实例化的对象    

constructor属性的作用是什么?

> 指向该原型对象或实例对象的构造函数， prototype和_proto_里面都有。

原型对象 prototype 共享一些属性和方法。

对象都会有一个属性_proto__ 指向构造函数的prototype原型对象。  
所以实例化对象就能使用prototype上的属性和方法。

> `__proto__`

[[prototype]]和_proto_意义相同，都是只读的

## 原型继承

new每次都会创建一个新的对象
不同的对象使用相同的属性和方法

```
function Star() {
this.age = 18this.say = function (){ }}
const ldh = new Star()const zxy = new Star()console.l1og( ldh)
console.log(zxy)
console.log(ldh === zxy)  // false每个实例对象都不一样
```

#### 作用域

**作用域就是一个独立的地盘，让变量不会外泄、暴露出去**。也就是说**作用域最大的用处就是隔离变量，不同作用域下同名变量不会有冲突。**

#### 作用域链

当在 Javascript 中使⽤⼀个变量的时候，⾸先 Javascript 引擎会尝试在当前作⽤域下去寻找该变 量，如果没找到，再到它的上层作⽤域寻找，以此类推直到找到该变量或是已经到了全局作⽤域

## 原型链

是一种查找规则，
基于原型对象的继承使得不同构造函数的原型对象关联在一起，并且这种关联的关系是一种链状的结构，我们将原型对象的链状结构关系称为原型链

1. 当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性。
2. 如果没有就查找它的原型（也就是_proto_指向的prototype原型对象)
3. 如果还没有就查找原型对象的原型（ Object的原型对象)
4. 依此类推一直找到Object为止 ( null)
   5._proto_对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线
   6.可以使用instanceof运算符用于检测构造函数的prototype属性是否出现在某个实例对象的原型链上

```
console.log(ldh instanceof Object) // true
```

> 原型链是一种查找规则，当我们访问一个对象的属性或方法时，首先查看这个对象自身有没有这个属性或方法，如果没有就查找这个对象的原型，如果还没有就查找原型对象的原型，以此类推，找不到就返回null。

### 浅拷贝

针对引用类型
如果是简单数据类型拷贝值，引用数据类型拷贝的是地址(简单理解:如果是单层对象，没问题，如果有多层就有问题)

1.拷贝对象:Object.assgin()/展开运算符{...obj}拷贝对象⒉.拷贝数组:Array.prototype.concat()或者[...arr]

### 深拷贝

深拷贝:拷贝的是对象，不是地址常见方法:  

1. 通过递归实现深拷贝   
   如果一个函数在内部可以调用其本身，那么这个函数就是递归函数。   
   由于递归很容易发生“栈溢出”错误（ stack overflow)，所以必须要加退出条件return

```
var obj = {
  id: 1,
  uname: 'zs',
  msg: {
    age: 18
  },
  hobbey: ['乒乓球', '篮球']
}
var o = {}
function deepCopy(newObj, oldObj) {
  for (let k in oldObj) {
    // 数组一定要写在对象的前面，因为数组也属于对
    if (obj[k] instanceof Array) {
      newObj[k] = []
      deepCopy(newObj[k], oldObj[k])
    } else if (obj[k] instanceof Object) {
      newObj[k] = {}
      deepCopy(newObj[k], oldObj[k])
    } else {
      newObj[k] = oldObj[k]
    }
  }
}
deepCopy(o, obj)
// console.log(o);
o.uname = 'ls'
o.hobbey[1] = '羽毛球'
o.msg.age = '21'
console.log(o);
console.log(obj);
```

2. lodash/cloneDeep   
   js库lodash里面cloneDeep内部实现了深拷贝

```
const o= _.cloneDeep(obj)
```

3． 通过JSON.stringify()实现

```
const o = JSON.parse( JSON.stringify (obj))
```

> new Date().toLocaleString() 显示当前时间

> 基本数据类型 赋值 是深拷贝，引用类型赋值是复制的地址，会影响原数据。引用类型浅拷贝针对于引用类型里的简单数据类型。

### 异常处理

异常处理是指预估代码执行过程中可能发生的错误，然后最大程度的避免错误的发生导致整个程序无法继续运行

throw抛异常  

```
function counter(x，y) {
if (!x|l !y) {
// throw '参数不能为空! ';
throw new Error(参数不能为空!”}
return X +y}
counter()
```

throw抛出异常信息，程序也会终止执行   
throw后面跟的是错误提示信息  
Error对象配合throw使用，能够设置更详细的错误信息

try /catch捕获异常

1. try...catch 用于捕获错误信息
2. 将预估可能发生错误的代码写在try 代码段中
3. 如果try代码段中出现错误后，会执行catch 代码段，并截获到错误信息
4. finally不管是否有错误，都会执行

```
unction foo(){
try {
//查找DOM节点
const p = document. queryselector( '.p')p.style.color = 'red'
} catch (error) {
// try 代码段中执行有错误时，会执行catch 代码段1/查看错误信息
console.log(error.message)//终止代码继续执行
return
}
finally {
alert( 执行')
}
console.log("如果出现错误，我的语句不会执行')}
foo()
```

debugger
断点调式

> 箭头函数中的this引用的就是最近作用域中的this

### call apply bind总结

相同点:
都可以改变函数内部的this指向.   
区别点:
call和 apply 会调用函数,并且改变函数内部this指向.   
call和apply传递的参数不一样, call传递参数aru1, aru2..形式 apply 必须数组形式[arg]   
bind不会调用函数,可以改变函数内部this指向.   
主要应用场景:   
call 调用函数并且可以传递参数   
apply经常跟数组有关系.比如借助于数学对象实现数组最大值最小值  

bind 不调用函数,但是还想改变this指向.比如改变定时器内部的this指向.

```
document.querySelector('button ' ).addEventListener ( ' click ', function () {
//禁用按钮
this.disabled = true
window.setTimeout(function (){
//在这个普通函数里面，我们要this由原来的window改为btnthis.disabled = false
}.bind(this),2000)
})
```

# 性能优化

## 防抖

单位时间内，频繁触发事件，只执行最后一次
简单说：当触发第一次事件还没完成时，又触发一次，这时事件会从头开始执行。可以说只执行最后一次   
使用场景   
搜索框搜索输入、手机号、邮箱验证输入检测

1. lodash 提供的防抖来处理（js库）

```
box.addEventListener( ' mousemove '， _.debounce(mouseMove，5oo))
```

3. 手写一个防抖函数来处理
   相当于lodash的原理
   
   ```
   //手写防抖函数
   //核心是利用setTimeout定时器来实现
   // 1．声明定时器变量
   //2．每次鼠标移动（事件触发）的时候都要先判断是否有定时器，如果有先清除以前的定时器
   // 3．如果没有定时器，则开启定时器，存入到定时器变量里面
   // 4．定时器里面写函数调用
   //简单说只有当你停止时，他才执行，因为你一直触发事件，他不会执行，它会一直等最后一次 才执行。
   ```

function debounce(fn, t){
let timer
// return返回一个匿名函数
return function () {
// 2.3.4
if (timer) clearTimeout(timer)timer = setTimeout(function () {
fn() //加小括号调用fn函数}, t)
}
}
box.addEventListener( ' mousemove ', debounce(mouseMove, 500))

```
## 节流
节流:单位时间内，频繁触发事件，只执行一次
简单说：频繁触发事件，它只会等第一次事件结束后，才会触发下一次事件。   
使用场景     
高频事件:鼠标移动mousemove、页面尺寸缩放resize.滚动条滚动scroll 等等

实现方式:
1.  lodash提供的节流函数来处理
2.  2.手写一个节流函数来处理
```

// 你连续触发它，他也只会根据时间一次一次的触发（就像英雄普攻）

/节流的核心就是利用定时器(setTimeout）来实现1.声明一个定时器变量
2.当鼠标每次滑动都先判断是否有定时器了，如果有定时器则不开启新定时器
3.如果没有定时器则开启定时器，记得存到变量里面
3.1定时器里面调用执行的函数
/3.2定时器 里面 要把定时器清空

function throttle(fn, t){let timer = null
return function () {if ( !timer) {
timer = setTimeout(function (圜fn()
//清空定时器timer = null
I
,t)
}
}}
box.addEventListener( ' mousemove ' , throttle(mouseMove，3000))

```
> 数组中map，可以进行加法减法操作，不能进行大于小于操作

> split 把字符串拆分成数组
```

const stt='大幅拉升,发觉覅欧吉安'
console.log(stt.split(',')) // ['大幅拉升', '发觉覅欧吉安']

上下逗号必须相匹配，也就是分隔符相匹配。

```
> 
> this永远指向最后调用它的对象，跟this定义的位置无关。
> 谁调用他，它指向谁

除了抛出异常以外，没有办法中止或跳出 forEach() 循环。（摘自MDN）

所以，即使有return，还是会执行完所有回调    
在forEach中使用 return false 或者 break无法跳出整个循环，并且使用break会直接报错  
```
