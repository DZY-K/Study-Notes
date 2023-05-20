# JS高级---零碎

## 数组中map方法迭代数组

使用场景:    
map可以遍历数组处理数据，并且返回新的数组

```
const arr = [ 'red ', 'blue', 'green ']
const newArr = arr.map( function (ele, index) {console.log(ele)//数组元素
console.log(index)//数组索引号
return ele +'颜色'
})
console.log ( newArr)
//[ 'red颜色'， 'bLue颜色', 'green颜色']
```

> map 也称为映射。映射是个术语，指两个元素的集之间元素相旦“对应”的天系。map重点在于有返回值，forEach没有返回值

## 数组中join方法

作用:
join()方法用于把数组中的所有元素转换一个字符串

```
const arr = [ ' red颜色','blue颜色','green颜色]
console.log(arr.join('')) // red颜色blue颜色green颜色
```

参数:  
数组元素是通过参数里面指定的分隔符进行分隔的，空字符串('')，则所有元素之间都没有任何字符。小括号为空则默认逗号分隔。

## Window对象

location的数据类型是对象，它拆分并保存了URL地址的各个组成部分  
常用属性和方法:   
href属性获取完整的URL地址，对其赋值时用于地址的跳转

```
//可以得到当前文件URL地址
console.log ( location.href) //可以通过js方式跳转到目标地址
location.href = 'http: // www.itcast.cn'
```

## location对象

location的数据类型是对象，它拆分并保存了URL地址的各个组成部分   
常用属性和方法:  
reload方法用来刷新当前页面，传入参数true时表示强制刷新

```
<button>点击刷新</button><script>
let btn = document.queryselector( ' button ')btn.addEventListener( 'click ' , function () {
location.reload(true)
//强制刷新类似ctrL + f5
})
</ script>
```

> search属性获取地址中携带的参数，符号?后面部分
> hash属性获取地址中的啥希值，符号#后面部分

### css

```
table tr: not( :first-child):hover {
background-color:#eee;
}
//意思是除了第一行都变色
```

## 对于let和const的用法

const声明的值不能更改，而且const声明变量的时候需要里面进行初始化  
但是对于引用数据类型，const声明的变量，里面存的不是值，不是值，不是值,是地址。

为什么const声明的对象可以修改里面的属性?   
因为对象是引用类型，里面存储的是地址，只要地址不变，就不会报错建议数组和对象使用const 来声明

什么时候使用let声明变量?     
如果基本数据类型的值或者引用类型的地址发生变化的时候，需要用let比如一个变量进行加减运算，比如for循环中的 i++

```
const img = document.querySelector( '.sd img ')
//获取 .sd元素里面的img元素。
```

## Set

**`Set`** 对象允许你存储任何类型的唯一值，无论是[原始值](https://developer.mozilla.org/zh-CN/docs/Glossary/Primitive)或者是对象引用。

`Set`对象是值的集合，你可以按照插入的顺序迭代它的元素。Set 中的元素只会**出现一次**，即 Set 中的元素是唯一的。

Set:创建一个新的 `Set` 对象。 

**静态属性**  
get.Set[@@specise]  
构造函数用来创建派生对象。   

**实例属性**   
Set.prototype.size  
返回 Set 对象中的值的个数

**实例方法**   
Set.prototype.add(value)   
在`Set`对象尾部添加一个元素。返回该 `Set` 对象。

Set.prototype.clear()   
移除`Set`对象内的所有元素

Set.prototy.delete(value)   
移除值为 `value` 的元素，并返回一个布尔值来表示是否移除成功。`Set.prototype.has(value)` 会在此之后返回 `false`。

Set.prototy.enntries()   
返回一个新的迭代器对象，该对象包含 `Set` 对象中的按插入顺序排列的所有元素的值的 `[value, value]` 数组。为了使这个方法和 `Map` 对象保持相似，每个值的键和值相等。

Set.prototy.foreach()   
按照插入顺序，为 Set 对象中的每一个值调用一次 callBackFn。如果提供了`thisArg`参数，回调中的 `this` 会是这个参数。

Set.prototy.has(value)  
返回一个布尔值，表示该值在 `Set` 中存在与否。

Set.prototy.keys()   
与 **`values()`**  方法相同，返回一个新的迭代器对象，该对象包含 `Set` 对象中的按插入顺序排列的所有元素的值。

Set.prototy.values()   
返回一个新的迭代器对象，该对象包含 `Set` 对象中的按插入顺序排列的所有元素的值。

## Map

**`Map`** 对象保存键值对，并且能够记住键的原始插入顺序。任何值（对象或者[基本类型](https://developer.mozilla.org/zh-CN/docs/Glossary/Primitive)）都可以作为一个键或一个值。

`Map` 对象是键值对的集合。`Map` 中的一个键**只能出现一次**；它在 `Map` 的集合中是独一无二的。Map 对象按键值对迭代——一个 for...of 循环在每次迭代后会返回一个形式为 [key，value] 的数组。迭代按插入顺序进行，即键值对按 set() 方法首次插入到集合中的顺序（也就是说，当调用 set() 时，map 中没有具有相同值的键）进行迭代。

```
const contacts = new Map()
contacts.set('Jessie', {phone: "213-555-1234", address: "123 N 1st Ave"})
contacts.has('Jessie') // true
```

**实例属性**

Map.prototype.size  
返回 `Map` 对象中的键值对数量

**实例方法**  
Map.prototype.clear()  
移除 `Map` 对象中所有的键值对。

Map.prototype.delete()  
移除 Map 对象中所有的键值对。

Map.prototype.get()  
返回与指定的键 `key` 关联的值，若不存在关联的值，则返回 `undefined`。

Map.prototype.has()  
返回一个布尔值，用来表明 `Map` 对象中是否存在与指定的键 `key` 关联的值。

Map.prototype.set()  
在 `Map` 对象中设置与指定的键 `key` 关联的值，并返回 `Map` 对象。

＋号两边只要有一个是字符串，都会把另外一个转成字符串除了+以外的算术运算符比如–*/等都会把数据转成数字类型

+号（加号开头）作为正号解析可以转换成数字型任何数据和字符串相加结果都是字符串

在控制台：  
数字型是蓝色，字符型是黑色。

### 随机数

如何生成N-M之间的随机数    
Math.floor(Math.random() *(M- N +1)) +N

1．阻止冒泡如何做?   
事件对象.stopPropagation()  
2.阻止元素默认行为如何做?  
e. preventDefault()  

```
    date.toLocaleString() //2023/4/9 14:14:12 
```

### 时间戳 （用于倒计时）

> 获取时间戳有哪三种方式?重点记住那个?   
> 1.const date =new Date   
>  date.getTime() 
> 2. +new Date()    
> 3. Date.now()  
> 重点记住+new Date()因为可以返回当前时间戳或者指定的时间戳

```
通过时间戳得到是毫秒，需要转换为秒在计算转换公式:
d = parselnt(总秒数/60/60/24);//计算天数   
h = parseInt(总秒数/60/60 %24) //计算小时   
m = parselnt(总秒数/60 %60 );//计算分数  
s = parselnt(总秒数%60); //计算当前秒数
```

> e.target.dataset.id 自定义属性的索引
> data-id="0" 从0开始

> 数据存储在用户浏览器中
> 设置、读取方便、甚至页面刷新不丢失数据

isNaN()可用于判断一个值是否为数字，isNaN()结果为false，该值为一个数字。   
可用于判断表单里的值是否为文字

```
if(isNaN(username.value)){
  return true //如果是数字，return true
}
```

> e.target.src 获得当前图片的路径

盒子在页面中的坐标 middle.getBoundingClientRect()，getBoundingClientRect() 不受定位的父元素的影响

```
 let xx = x - middle.getBoundingClientRect().left
```

Object.create() 方法用于创建一个新对象，使用现有的对象来作为新创建对象的原型（prototype）。  
返回值为一个新对象，带着指定的原型对象及其属性。

> currentTime 属性设置或返回视频播放的当前位置（以秒计）。

> promise对象的then()方法属于微任务，而setTimeout()定时器函数为宏任务。在执行顺序处理上，js会先执行所有同步代码，然后执行微任务队列中的所有微任务，最后再继续执行宏任务。

> :only-child 选择器匹配属于其父元素的唯一子元素的每个元素

## 事件委托例子

```
<div class="num">
  <a href="javascript:;">-</a>
  <input type="text" value="1">
  <a href="javascript:;">+</a>
</div>

num.addEventListener('click',function(e){
if(e.target.tagName==='A'){
  // console.log(e.target.nodeName);
  if(e.target.innerText==='-'){
    if(this.querySelector('input').value>0){
      this.querySelector('input').value--
    }
  }
  if(e.target.innerText==='+'){
    this.querySelector('input').value++
  }
}
}

用事件委托进行相同标签下的不同操作，首先看相同标签有什么不同的地方，该题为两个a链接，不同的地方只有文本内容，
e.target.innerText==='-' 获得相同标签下的不同内容。

e.target.nodeName与e.target.tagName用法相同。
```

> 事件委托是指将事件处理程序添加到父元素上，而不是添加到每个子元素上。这样就可以利用事件冒泡机制，只需在父元素上处理一次事件即可。当子元素触发该事件时，该事件会逐级向上传播到父级，并由父级处理该事件。  
> 
> 使用事件委托的好处是可以减少代码量，并且可以提高性能，因为减少了事件处理程序的数量。此外，它还能够更灵活地处理动态添加或删除的子元素。常见的应用场景包括列表、表格、菜单等元素的点击事件处理。

`event.keyCode === 13 `回车键的ASCLL值是13

> 如果想要调用父页面中的方法，使用 `window.parent`

> 如果用户自定义的属性，放在扩展运算符后面，则扩展运算符内部的同名属性会被覆盖掉

```
let a = {x: 3,y:4}
console.log({...a,x:1,y:2});//{ x:1, y:2}
console.log({...a,. . .{x:1,y:2}});// x:1， y:2}
```

## iterable类型

遍历`Array`可以采用下标循环，遍历`Map`和`Set`就无法使用下标。为了统一集合类型，ES6标准引入了新的`iterable`类型，`Array`、`Map`和`Set`都属于`iterable`类型。

具有`iterable`类型的集合可以通过新的`for ... of`循环来遍历。

> 匿名函数按照完整语法需要在函数体末尾加一个`;`，表示赋值语句结束。

> 加号优先级高于 三目运算。低于括号。 所以括号中无论真假 加上前边的字符串都为 TRUE 三目运算为TRUE是 输出 define
