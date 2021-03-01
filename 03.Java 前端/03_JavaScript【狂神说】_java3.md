# 0、前端知识体系

想要成为真正的“互联网Java全栈工程师”还有很长的一段路要走，其中**前端**是绕不开的一门必修课。本阶段课程的主要目的就是带领Java后台程序员认识前端、了解前端、掌握前端，为实现成为“互联网Java全栈工程师”再向前迈进一步。

## 0.1、前端三要素

- **HTML**（结构）：超文本标记语言（Hyper Text Markup Language），决定网页的结构和内容
- **CSS**（表现）：层叠样式表（Cascading Style Sheets），设定网页的表现样式。
- **JavaScript**（行为）：是一种弱类型脚本语言，其源码不需经过编译，而是由浏览器解释运行，用于控制网页的行为

## 0.2、结构层（HTML）

太简单，略

## 0.3、表现层（CSS）

CSS层叠样式表是一门标记语言，并不是编程语言，因此不可以自定义变量，不可以引用等，换句话说就是不具备任何语法支持，它主要缺陷如下：

- 语法不够强大，比如无法嵌套书写，导致模块化开发中需要书写很多重复的选择器；
- 没有变量和合理的样式复用机制，使得逻辑上相关的属性值必须以字面量的形式重复输出，导致难以维护；
  这就导致了我们在工作中无端增加了许多工作量。为了解决这个问题，前端开发人员会使用一种称之为【CSS预处理器】的工具,提供CSS缺失的样式层复用机制、减少冗余代码，提高样式代码的可维护性。大大的提高了前端在样式上的开发效率。



**什么是CSS预处理器**

CSS预处理器定义了一种新的语言，其基本思想是，用一种专门的编程语言，为CSS增加了一些编程的特性，将CSS作为目标生成文件，然后开发者就只需要使用这种语言进行CSS的编码工作。转化成通俗易懂的话来说就是“**用一种专门的编程语言，进行Web页面样式设计，再通过编译器转化为正常的CSS文件，以供项目使用”**。



**常用的CSS预处理器有哪些**

- **SASS**：基于Ruby ，通过服务端处理，功能强大。解析效率高。需要学习Ruby语言，上手难度高于LESS。
- **LESS**：基于NodeJS，通过客户端处理，使用简单。功能比SASS简单，解析效率也低于SASS，但在实际开发中足够了，所以如果我们后台人员如果需要的话，建议使用LESS。

## 0.4、行为层（JavaScript）

JavaScript一门**弱类型脚本语言**，其源代码在发往**客户端运行之前不需要经过编译**，而是将**文本格式的字符代码**发送给浏览器，**由浏览器解释运行**。

## JavaScript框架

- **JQuery**：大家熟知的JavaScript库，优点就是简化了DOM操作，缺点就是DOM操作太频繁，影响前端性能；在前端眼里使用它仅仅是为了兼容IE6，7，8；
- **Angular**：Google收购的前端框架，由一群Java程序员开发，其特点是将后台的MVC模式搬到了前端并增加了**模块化开发**的理念，与微软合作，采用了TypeScript语法开发；对后台程序员友好，对前端程序员不太友好；最大的缺点是版本迭代不合理（如1代–>2 代，除了名字，基本就是两个东西；截止发表博客时已推出了Angular6）
- **React：Facebook** 出品，一款高性能的JS前端框架；特点是提出了新概念 【虚拟DOM】用于减少真实 DOM 操作，在内存中模拟 DOM操作，有效的提升了前端渲染效率；缺点是使用复杂，因为需要额外学习一门【JSX】语言；
- **Vue**：一款渐进式 JavaScript 框架，所谓渐进式就是逐步实现新特性的意思，如实现模块化开发、路由、状态管理等新特性。其特点是综合了 Angular（模块化）和React(虚拟 DOM) 的优点；
- **Axios**：前端通信框架；因为 Vue 的边界很明确，就是为了处理 DOM，所以并不具备通信能力，此时就需要额外使用一个通信框架与服务器交互；当然也可以直接选择使用jQuery 提供的AJAX 通信功能；

## UI框架

- **Ant-Design**：阿里巴巴出品，基于React的UI框架
- **ElementUI、iview、ice**：饿了么出品，基于Vue的UI框架
- **BootStrap**：Teitter推出的一个用于前端开发的开源工具包
- **AmazeUI**：又叫“妹子UI”，一款HTML5跨屏前端框架

## JavaScript构建工具

- **Babel**：JS编译工具，主要用于浏览器不支持的ES新特性，比如用于编译TypeScript
- **WebPack**：模块打包器，主要作用就是打包、压缩、合并及按序加载

> 注：以上知识点已将WebApp开发所需技能全部梳理完毕

## 0.5、三端同一

### 混合开发（Hybrid App）

主要目的是实现一套代码三端统一（PC、Android：.apk、iOS：.ipa）并能够调用到设备底层硬件（如：传感器、GPS、摄像头等），打包方式主要有以下两种：

- 云打包：HBuild -> HBuildX，DCloud 出品；API Cloud
- 本地打包： Cordova（前身是 PhoneGap）

### 微信小程序

详见微信官网，这里就是介绍一个方便微信小程序UI开发的框架：WeUI



# 1、什么是JavaScript

# 1.1、概述

javaScript 是一门世界上最流行的脚本语言

Java，JavaScript

10天

一个合格的后端人员，必须精通JavaScript

# 1.2、历史

见百度

**ECMAScript** 它可以理解为JavaScript的一个标准

最新版本已经到es6版本~

但是大部分浏览器还只停留在支持es5代码上！

开发环境–线上环境，版本不一致



# 2、快速入门

## 2.1、引入JavaScript

1、内部标签

```html
<!--    scrpit标签内，写JavaScript代码-->
   <script>
        alert('hello,world!');
     //......
    </script>
```

2、外部引入
hj.js

```javascript
alert("hello,world");
//......
```

test.html

```html
 <!--外部引入
        注意：script必须成对出现
    -->
    <script src="js/hj.js"></script>

    <!--不用显示定义type，也默认就是javaScript-->
    <script type="text/javascript"></script>

```

测试代码

```js
alert('hello,world!');
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<!--    scrpit标签内，写JavaScript代码-->
<!--    <script>-->
<!--        alert('hello,world!');-->
<!--    </script>-->

    <!--外部引入
       注意：script必须成对出现
   -->
    <script src="js/qj.js"></script>
</head>
<body>

</body>
</html>
```

![image-20210119104939123](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119104939.png)



## 2.2、基本语法入门

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <!--JavaScript严格区分大小写-->
    <script>
        // 1. 定义变量   变量类型 变量名 = 变量值
        var score = 1 ;
        //alert(num)

        // 2. 条件控制
        if (score > 60 && score < 70){
            alert("60~70");
        }else if(score > 70 && score < 80){
            alert("70~80");
        }else{
            alert("other")
        }
      //console.log(score)在浏览器控制台打印变量！相当于sout
    </script>
</head>
<body>

</body>
</html>
```

浏览器必备调试须知：
![image-20210119110036939](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119110037.png)

## 2.3、数据类型

数值，文本，图形，音频，视频......

==变量==

```javascript
var a=1 
```

==number==
js不区分小树和整数，Number

```javascript
123//整数123
123.1//浮点数123.1
1.123e3//科学计数法
-99//负数
NaN	//not a number
Infinity // 表示无限大
```

==字符串==
‘abc’   “abc”

==布尔值==
true，false

==逻辑运算==

```javascript
&& 两个都为真，结果为真

|| 一个为真，结果为真

! 	真即假，假即真

```

==比较运算符== ！！！重要！

```javascript
=
1，"1"
== 等于（类型不一样，值一样，也会判断为true）
=== 绝对等于（类型一样，值一样，结果为true）
```

这是一个JS的缺陷，坚持不要使用 == 比较   **使用===**

须知：

- NaN === NaN，**NaN与所有的数值都不相等**，包括自己
- 只能通过**isNaN**（NaN）来判断这个数是否是NaN

==浮点数==问题

```javascript
console.log((1/3) === (1-2/3))     //false
```

尽量避免使用浮点数进行运算，存在**精度问题**！

```javascript
Math.abs(1/3-(1-2/3))<0.00000001      //true
```

==null 和 undefined==

- null 空
- undefined 未定义

==数组==
Java的数组必须是相同类型的对象~，JS中不需要相同类型的对象

```javascript
//保证代码的可读性，尽量使用[]
var arr = [1,2,3,4,5,'hello',null,true];

//第二种定义方法
new Array(1,2,3,4,5,'hello');
```

取数字下标：如果越界了，就会 报undefined

```javascript
console.log(arr[8])

//undefined
```

==对象==
对象是大括号，数组是中括号

> 每个属性之间使用逗号隔开，最后一个属性不需要逗号

```javascript
// Person person = new Person(1,2,3,4,5);

var person = {
	name:'Tom',
	age:3,
	tags:['js','java','web','...']
}
```

取对象值

```javascript
person.name
> "Tom"
person.age
> 3
```

## 2.4、严格检查格式

![image-20210119113310398](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119113310.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--
    前提：IDEA需要设置支持ES6语法
        'use strict';严格检查模式，预防JavaScript的随意性导致产生的一些问题
        必须写在JavaScript的第一行！
        局部变量建议都使用let去定义~
    -->
    <script>
        'use strict';
        //全局变量
        let i=1
        //ES6 let
    </script>
</head>
<body>

</body>
</html>
```

# 3、数据类型

## 3.1、字符串

1、正常字符串我们使用 '单引号'，或者"双引号"包裹

2、注意转义字符 \

```java
\'
\n
\t
\u4e2d    \u##### Unicode字符

\x41	Ascall字符
```

![image-20210119113738823](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119113738.png)

3、多行字符串编写

```javascript
//tab 上面 esc下面
        var msg =
            'hello
            world
            你好呀
            nihao'
```

4、模板字符串

```javascript
//tab 上面 esc下面
let name = 'Tom';
let age = 3;
var msg = `你好，${name}`
```

![image-20210119114135515](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119114135.png)

5、字符串长度

```javascript
str.length
```

![image-20210119114103649](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119114103.png)

6、字符串的可变性，不可变
![image-20210119114211962](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119114212.png)
7、大小写转换

```javascript
//注意，这里是方法，不是属性了
student.toUpperCase();
student.toLowerCase();
```

8、student.indexof(‘t’)

![image-20210119114514309](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119114514.png)

9、substring，从0开始

```javascript
[ )     //左闭右开
student.substring(1)//从第一个字符串截取到最后一个字符串
student.substring(1,3)//[1,3)
```

![image-20210119114622652](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119114622.png)

## 3.2、数组

Array可以包含任意的数据类型

```javascript
var arr = [1,2,3,4,5,6];//通过下标取值和赋值
arr[0]
arr[1]=1
```

1、长度

```javascript
arr.length
```

注意：**假如给arr.lennth赋值，数组大小就会发生变化**(新增的数据都是undefined的)，

**如果赋值过小，元素就会丢失**

2、indexOf，通过元素获得下标索引

```javascript
arr.indexOf(2)
//1
```

字符串的"1"和数字 1 是不同的

![image-20210119115349528](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119115349.png)

**3、slice（）**截取Array的一部分，返回的一个新数组，类似于String中substring

**4、push()，pop()尾部**

```javascript
push：压入到尾部
pop：弹出尾部的一个元素
```

![image-20210119115725846](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119115725.png)

**5、unshift(),shift()   头部**

```javascript
unshift：压入到头部
shift：弹出头部的一个元素
```

![image-20210119120044905](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119120044.png)

6、排序sort()

```javascript
["B","C","A"]
arr.sort()
["A","B","C"]
```

![image-20210119121411704](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119121411.png)

7、元素反转reverse()

```javascript
["A","B","C"]
arr.reverse()
["C","B","A"]
```

![image-20210119121433048](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119121433.png)



**8、concat()**
注意：concat()并没有修改数组，只是会**返回一个新的数组**

![image-20210119121539562](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119121539.png)



9、连接符  join
打印拼接数组，使用特定的字符串连接

![image-20210119121646305](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119121646.png)



10、多维数组
![image-20210119121826827](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119121826.png)

数组：存储数据（如何存，如何取，方法都可以自己实现！）



## 3.3、对象

若干个键值对

```javascript
var 对象名 = {
	属性名：属性值，
	属性名：属性值，
	属性名：属性值
}

//定义了一个person对象，它有四个属性
var person = {
	name:"kuangshen",
	age:3,
	email:"123456798@QQ.com",
	score:66
}

```

![image-20210119122120338](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119122120.png)

Js中对象，{…}表示一个对象，建制对描述属性xxx：xxx，多个属性之间用逗号隔开，最后一个属性不加逗号！

JavaScript中的所有的**键都是字符串**，**值是任意对象**！

1、对象赋值

![image-20210119122823483](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119122823.png)

2、使用一个不存在的对象属性，不会报错！undefined

![image-20210119122809839](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119122809.png)

3、动态的删减属性，通过delete删除对象的属性

![image-20210119122402942](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119122403.png)

4、动态的添加，直接给新的属性添加值即可

![image-20210119122439759](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119122439.png)

5、判断属性值是否在这个对象中！xxx in xxx

![image-20210119122550678](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119122550.png)

6、判断一个属性是否是这个对象自身拥有的 hasOwnProperty()

![image-20210119122625321](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119122625.png)



## 3.4、流程控制

### if判断

```javascript
var age = 3;
if(age>3){
  alert("haha");
}else if(age<5){
  alert("kuwa~");
}else{
  alert("diwa~")；
}
```



### while循环，避免程序死循环

```javascript
while(age<100){
  age = age+1;
  console.log(age);
}

do{
  age=age+1;
  console.log(age);
}while(age<100);
```



### for循环

```javascript
// for(a;b;c){d}
//先执行初始化语句a 然后重复以下逻辑：
//判断b 为false则结束for循环，为true则执行d
//执行c 重新判断b

for(let i =0;i<100;i++){
  console.log(i);
}
```



### forEach循环

> ES5.1特性

```javascript
var age = [12,3,12,3,12,3,12,31,23,123];

age.forEach(function(value,index,array){
  console.log(value);
  console.log(index);
  console.log(array);
})
```



### for …in-------  num下标

```javascript
for(var num in age){
            if(age.hasOwnProperty(num)){
                console.log("存在");
                console.log(age[num]);
            }
        }
```



## 3.5、Map和Set

> ES6的新特性~

Map:   key-value对

```javascript
<script>
        //定义 就是一个一个的key-value对
        let map=new Map([['a',100],['b',90],['c',80]]);
        let a=map.get('a');//取得key为‘a’的值
        map.set('a',99);//改变key对应的value值，若key不存在，将会新建一个键值对
        map.delete('a');//删除key对应的键值对
</script>
```

Set：无序不重复的集合

```javascript
<script>
	let s=new Set([9,9,6,4,52,1]);//定义，Set会自动去重
	s.add(2);//添加值，若set里有，则不会改变
	console.log(s.has(9));//返回true或者false 判断是否含有元素
	s.delete(2);//删除
</script>
```



## 3.6、iterator

> es6新特性 如果有新增或者已删除的元素使用for in 打印有漏洞

作业：使用iterator来遍历迭代我们Map，Set！

for （.....   of.....）打印值

  for （.....   in.....）打下标

遍历数组

```javascript
var arr = [3,4,5];
for(var x of arr){
  console.log(x);
}
```



遍历Map

```javascript
var map = new Map([["tom",100],["jack",90],["haha",80]]);
for(var x of map){
  console.log(x);
}
```



遍历set

```javascript
var set = new Set([5,6,7]);
for(var x of set){
  console.log(x);
}
```



# 4、函数

## 4.1、定义函数

> 定义方式一

绝对值函数

```javascript
//函数定义
        function abs1(x) {
            if (x>=0){
                return x;
            }else {
                return -x;
            }
        }
```


一旦执行到return代表函数结束，返回结果！

如果没有执行return，函数执行完也会返回结果，结果就是undefined



> 定义方式二

```javascript
var abs2 =function(x) {
            if (x>=0){
                return x;
            }else {
                return -x;
            }
        }
```

function(x){…}这是一个匿名函数。但是可以吧结果赋值给abs，通过abs就可以调用函数！
方式一和方式二等价！

![image-20210119163051722](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119163051.png)





> 调用函数

```javascript
abs(10)//10
abs(-10) //10
```

参数问题：javaScript可以传任意个参数，也可以不传递参数~

参数进来是否存在问题？假设不存在参数，如何规避？

```javascript
var abs = function(x){
  //手动抛出异常来判断
  if(typeof x!== 'number'){
    throw 'Not a Number';
  }
  if (x>=0){
    return x;
  }else {
    return -x;
  }
}
```



> arguments

`arguments`是一个JS免费赠送的关键字；代表，传递进来的所有参数，是一个数组！

```javascript
function abs(x){
            console.log("x=>"+x);

            for(var i=0;i<arguments.length;i++){
                console.log(arguments[i]);
            }

            if (x>=0){
                return x;
            }else {
                return -x;
            }

        }
```



![image-20210119162532689](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119162532.png)


问题：arguments包含所有的参数，我们有时候想使用多余的参数来进行附加操作。需要排除已有参数~



> rest

以前：

```javascript
if(arguments.length>2){
                 for(var i = 2;i<arguments.length;i++){
                     //....
                 }
             }
```



ES6引入的新特性，获取除了已经定义的参数之外的所有参数~…

```javascript
function f(a, b,...rest) {
             console.log("a=>"+a);
             console.log("b=>"+b);
             console.log(rest);
        }
```



![image-20210119162850671](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119162850.png)

rest参数只能写在最后面，必须用…标识。

## 4.2、变量的作用域

在javascript中，var定义变量实际是有作用于的。

假设在函数体重声明，则在函数体外不可以使用~（闭包）

```javascript
function f() {
  var x=1;
  x+=1;
}
f();
x+=2;//Uncaught ReferenceError: x is not defined
```


如果两个函数使用了相同的变量名，只要在函数内部就不冲突

```javascript
function f1() {
  var x = 0;
  alert(x);//0
}

function f2() {
  var x=1;
  alert(x);//1
}
```

内部函数可以访问外部函数的成员，反之则不行

```java
function f1() {
  	var x = 0;
  
 		//内部函数可以访问外部函数的成员，反之则不行
		function f2() {
 	 		 var y=x+1;//2
  		 }
  
  	var z =y+1;//uncaught ReferenceError: y is not defined
}
```

假设，内部函数变量和外部函数变量，重名！

```javascript
function f1() {
  	var x = 1;
  
		function f2() {
 	 		 var x='A';
      console.log('inner:'+x);//innerA
  		 }
  	 console.log('outer:'+x);//outerA
  	f2();
}
```


假设在JavaScript中，函数查找变量从自身函数开始~， **由“内”向“外”查找**，假设外部存在这个同名的函数变量，则内部函数会屏蔽外部函数的变量。(**就近原则**)



> 提升变量的作用域

```javascript
function qj(){
  //var y  相当于提升到这里来了
  
  var x = "x"+y;
  console.log(x);
  var y ="y";
}
```


结果：x undefined

说明：js执行引擎，自动提升了y的声明，但是不会提升变量y的赋值；

这个是在javascript建立之初就存在的特性。 养成规范：所有的变量定义都放在函数的头部，不要乱放，便于代码维护；（**先声明后定义**）

```javascript
function qj2(){
  var x=1,y=x+1;
  z,i,a;//undefined
  console.log(x);
  //之后随意使用
}
```



> 全局变量

```javascript
//全局变量
var x=0;
function f() {
  alert(x);//0
}
f();
console.log(x);
```



> 全局对象window

```javascript
let a= 123;
alert(a);//123
alert(window.a);//123    默认的所有全局变量，都会自动绑定在window对象下
```



**alert()** 这个函数本身也是一个==window==的变量；

```javascript
var x = 'xxx';

window.alert(x);

var old_alert = window.alert;

//old_alert(x);
window.alert = function () {
};

//发现 alert()失效了
window.alert(123);

//恢复
window.alert = old_alert;
window.alert(456);

```


javascript实际上只有一个**全局作用域**，任何变量（函数也可以视为变量），假设没有在函数作用范围内找到，**就会向外查找**，如果在**全局作用域**都没有找到，就会**报错 Refrence**



> 规范

由于我们的所有变量都会绑定到window上

如果不同的js文件，使用了相同的全局变量，就会产生冲突—>如何减少这样的冲突？

```javascript
//唯一全局变量
var KuangApp = {};

//定义全局变量
KuangApp.name = kuangshen;
KuangApp.add = function (a,b) {
	return a + b;
}

```

把自己的代码全部放入自己定义的唯一空间名字中，降低全局命名冲突问题~
jQuery中就是使用的该方法：**jQuery.name**，简便写法：**$()**



> 局部作用域 let

```javascript
function aaa( {
	for (var i = o; i < 100; i++) {
		console.log(i)
	}
	console.log(i+1);//问题? i 出了这个作用域还可以使用
}
```


ES6的**let关键字**，解决了局部作用域冲突的问题！

```javascript
function aaa( {
	for (let i = o; i < 100; i++) {
		console.log(i)
	}
	console.log(i+1);//uncaught ReferenceError: y is not defined
}
```


建议大家都用==let==去定义局部作用域的变量；



> 常量

在ES6之前，怎么定义常量：只有用全部大写字母命名的变量就是常量；建议不要修改这样的值。

```javascript
var PI = '3.14';
console.1og(PI);
PI = '213';  //可以改变这个值
conso1e.1og(PI);
```


在ES6引入了常量**关键字 const**

```javascript
const PI = '3.14'; //只读变量
console. 1og(PI);
PI = '123'; // TypeError: Assignment to constant variable.
console.log(PI);
```



## 4.3、方法

> 定义方法

方法就是把函数放在**对象**的里面，对象只有两个东西：属性和方法

```javascript
var kuangshen = {
		name:'秦疆',
 		bitrh:2000,
  	//方法
		age: function (){
		//今年 –出生的年
		var now = new Date(. getFu11Year();
      return now-this.bitrh;
		}
}

//属性
kuangshen.name
//方法，一定要带
kuangshen.age()
```



this.代表什么？拆开上main的代码看看

```javascript
function getAge(){
		//今年 –出生的年
		var now = new Date(. getFu71Year();
  	return now-this.bitrh;
}

var kuangshen = {
		name:'秦疆',
  	bitrh:2000,
  	age:getAge
};

//kuangshen.age() ok
//getAge() NaN    window.getAge()当然无法使用了
```

this是无法指向的，是默认指向调用它的那个对象的；



> apply

在js中可以控制this指向

```javascript
apply<T, R>(this: (this: T) => R, thisArg: T): R;
```



```javascript
 function getAge() {
            let now =new Dat().getFullYear();
            return now-this.brith;
        }
        let hyx={
            name:"hyx",
            brith:1998,
            age:getAge()
        }
        hyx.age();//22
        getAge();//报错 this指向调用者，这里是window window没有brith
        getAge().apply(hyx,[]);//被动调用
```



# 5、内部对象

> 标准对象

typeof 检测

```javascript
typeof 123
"number"
typeof '123'
"string"
typeof true
"boolean"
typeof NaN
"number"
typeof []
"object"
typeof {}
"object"
typeof Math.abs
"function"
typeof undefined
"undefined"
```



## 5.1、Date

**基本使用**

```javascript
var now = new Date(); //sat Jan 04 2020 10:47:06 GMT+0800 (中国标准时间)
now. getFu11Year();//年
now.getMonth;//月0~11代表月
now.getDate();//日
now.getDayO;//星期几
now.getHours();// 时
now. getMinutes();//分
now.getseconds(); //秒
now.getTime();//时间戳  全世界统一1970 1.1 0:00:00毫秒数

console.log(new Date(1578106175991));//时间戳转为时间

```



> 转换

```javascript
now = new Date(1578106175991);
//sat an 04 2020 10:49:35 GMT+0800(中国标准时间)

now.toLocalestring // 注意，调用是一个方式，不是一个属性!
//f toLocalestring( { [native code] }

now.toLocalestring()
//"2020/1/4 上午10:49:35"

now.toGMTstring()
//"sat，04 3an 2020 02:49:35 GMT"

```



## 5.2、JSON

> JSON是什么

早期，所有数据传输习惯使用XML文件!

- JSON (JavaScript Object Notation,JS对象简谱) 是一种**轻量级的数据交换格式**。
- 简洁和清晰的层次结构使得JSON成为理想的数据交换语言。
- 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。



在javascript中，一切皆为对象，任何 js 支持的类型都可以用**JSON**表示(无缝转换)

格式：

- 对象都用{}
- 数组都用[]
- 所有的键值对 都是用key:value

JSON字符串和js对象转化

```javascript
<script>
        let user={
            name:'hyx',
            age:18
        }

        //对象转化为JSON字符串
        let jsonUser=JSON.stringify(user);

        //JSON字符串转化回对象 参数为json字符串
        let user1=JSON.parse(jsonUser);
        console.log(user1);
</script>
```



![image-20210119175142119](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119175142.png)

很多人搞不清楚，JSON和JS对象的区别

![image-20210119175424088](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119175424.png)



## 5.3、AJAX

- 原生的js写法     xhr异步请求
- jQuery封装好的方法  $("#name").ajax("")
- axios请求

# 6、面向对象编程

> 原型对象



javascript、java、c#------面向对象；但是javascript有些区别！

- 类：模板    原型对象
- 对象：具体实例

在javascript中，需要大家转换一下思维方式！

原型(相当于是个父类)：

```javascript
	var student = {
		name :"qinjiang",
    age: 3，
		run: function(){
			conso1e.log(this.name + " run. . .. ");
		}
	};

	var xiaoming = {
		name : "xiaoming"
  };


	//原型对象
	xiaoming.__proto__ = student;

	var Bird = {
		f1y: function() {
			console.log(this.name + " f1y.. .. ");
		}
  };

	//小明的原型是 student 
	xiaoming.__proto__ = Bird;

```

![image-20210119185434751](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119185434.png)




> class集继承



在ES6之前

```javascript
function Student(name) {
	this.name = name;
}

//给student新增一个方法
student.prototype.he11o = function () {
	alert( 'He11o')
};
```

引入ES6之后：

==class==关键字，是在ES6引入的

1、定义一个类、属性、方法

```javascript
//定义一个学生的类
class student{
  
	constructor(name){
		this.name = name ;
	}
  
	he1lo(){
		alert( 'he11o ')
	}
  
}
var xiaoming = new student("xiaoming");
var xiaohong = new student("xiaohong");
xiaoming.he11o()

```


2、继承

```javascript
<script>
	//ES6之后========================
	//定义一个学生的类
	class Student{
		constructor(name){
			this.name = name;
		}
		hello(){
			alert('hello');
		}
}

	class XiaoStudent extends Student{
		constructor(name,grade){
			super(name);
			this.grade = grade;
		}
		myGrade(){
			alert('我是一名小学生');
		}
	}

	var xiaoming = new Student("xiaoming");
	var xiaohong = new XiaoStudent("xiaohong",1);
</script>
```

本质：查看对象原型

![image-20210119190657823](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119190657.png)



> 原型链

`__proto__`

![image-20210119191221959](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119191222.png)



# 7、操作BOM对象（重点）

> 浏览器介绍

**javascript和浏览器关系？**

javascript的诞生就是为了在浏览器上运行！



**BOM：浏览器对象模型：**

- IE6~11
- Chrome
- Safari
- FireFox
- Opera

- 第三方浏览器
  - QQ浏览器
  - 360浏览器



> window

window代表浏览器窗口

![image-20210119203125156](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119203125.png)



> Navigator（不建议使用）

Navigator封装了浏览器的信息

```javascript
navigator.appName
"Netscape"
navigator.appVersion
"5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36"
navigator.userAgent
"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36"
navigator.platform
"Win32"
```

大多数时候，我们不会使用`navigator`对象，因为会被认为修改!
不建议使用这些属性来判断和编写代码



> screen

代表屏幕尺寸

```javascript
screen.width
1536
screen.height
864
```



> location(重要)

location代表当前页面的URL信息

```javascript
host : "www.baidu.com"
href : "https: / /www.baidu.com/"
protoco1 : "https : "
reload:f reload()//刷新网页
//设置新的地址
1ocation .assign( 'https : / /b1og. kuangstudy. com/ ')
```



> document（内容DOM）

document代表当前的页面，HTML DOM文档树

![image-20210119203858956](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119203859.png)

获取具体的文档树节点

```java
<script>
var dl = document.getElementById( 'app ' );
</script>

<body>
<d1 id="app">
		<dt>ava</dt>
  	<dd>JavasE</dd>
  	<dd>JavaEE</dd>
</d1>
</body>

```

![image-20210119204250659](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119204250.png)



获取cookie

![image-20210119204102044](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119204102.png)



劫持cookie原理
www.taobao.com

```javascript
<script src="aa.js "> </script>
<!--恶意人员;获取你的cookie上传到他的服务器―->
```

服务器端可以设置cookie :  httpOnly



> history（不建议使用 ）

history代表浏览器的历史记录

```javascript
history.back() //后退
history.forward()//前进
```



# 8、操作DOM对象（重点）

**DOM：文档对象模型**

> 核心

浏览器网页就是一个Dom树形结构！

![image-20210119204952714](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119204952.png)

JavaScript动态地操作上面的这些元素，让他的们的元素改变。

- 更新：更新Dom节点
- 遍历Dom节点：得到Dom节点
- 删除：删除一个Dom节点
- 添加：添加一个新的节点

要操作一个Dom节点，就必须要先获得这个Dom节点

> ## 获得Dom节点

```
<body id="father">
	<h1>123</h1>
	<h1>456</h1>
	<p id="p1"></p>
	<p class="p2"></p>
	<dl>
	</dl>
</body>
```



```javascript
 <script onload="this">
        //标签选择器
        let h1=document.getElementsByName('h1');
        //ID选择器
        let p1=document.getElementById('p1');
        //class选择器
        let p2=document.getElementsByClassName('p2');
        let father= document.getElementById('father');

        //获得最后一个、第一个、所有子节点
        father.lastChild;
        father.firstChild;
        father.childNodes;//返回NodeList
        father.children;//返回HTMLCollection
        // 获得父节点
        father.parentNode;
    </script>
```


这是原生代码，之后我们尽量都使用jQuery();

> ## 更新节点

**操作文本**

```javascript
<script>
    //先获取节点
    let div1=document.getElementById('div1');

		//操作javascript
    div1.innerText='hello';//改变文本内容
    div1.innerHTML='<a href="https://www.baidu.com">123</a>';//可以解析html文本标签

		//操作CSS
    div1.id='123';//更改id
    div1.className="hello";//更改class
    div1.style.background='red';//操作CSS

</script>


<body>
<div id="div1"></div>
</body>
```



**操作css**

```javascript
id1.style.color = 'ye11ow'; //属性使用 字符串 包裹
id1.style.fontsize='20px '; // 转驼峰命名问题
id1.style.padding = '2em';

```



> ## 删除节点

删除节点的步骤：先获取父节点，再通过父节点删除自己

```javascript
<body>
<div id="father">
	<h1>标题一</h1> 
	<p id="p1">p1</p>
	<p class="p2">p2</p>
</div>
</body>

<script>
    //通过父节点删除子节点
	var self = document.getElementByTd('p1 ');	
	var father = p1.parentE1ement;
	father.removechild(self)

	//删除是一个动态的过程; 删除0后后面的顶上来了
  father.removechi1d(father.chi1dren[0])
	father.removechild(father.children[1])
	father.removechild(father.chi1dren[2])
</script>

```


注意：删除多个节点的时候，children是在时刻变化的，删除节点的时候一定要注意。



> ## 插入节点

我们获得了某个Dom节点，假设这个dom节点是空的，我们通过`innerHTML`就可以增加一个元素了，但是这个Dom节点已经存在元素了，我们就不能这么干了！**会产生覆盖**

**追加**

```javascript

<p id="js ">avascript</p>
<div id="list">
<p id="se">JavaSE</p>
<p id="ee">avaEE</p>
<p id="me ">avaME</p>
</div>

<script>
	var js = document.getElementById('js ');
	var list = document.getElementById( 'list' );
	//list.appendchild(js);//追加到后面
</script>

```

![image-20210119211958163](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119211958.png)


> 创建一个新的标签,实现插入

```html
<script>
	var js = document.getElementById('js');//已经存在的节点
    var list = document.getElementById('list');
    //通过JS创建一个新的节点
    var newP = document.creatElement('p');//创建一个p标签
    newP.id = 'newP';
    newP.innerText = 'Hello,Kuangshen';
  	//list。appendChild(newP)
  
    //创建一个标签节点
    var myScript = document.creatElement('script');
    myScript.setAttribute('type','text/javascript');
  	
    
    //可以创建一个style标签
    var myStyle = document.creatElement('style');//创建了一个空style标签
    myStyle.setAttribute('type','text/css');
    myStyle.innerHTML = 'body{background-color:chartreuse;}';//设置标签内容
  	//获得<html>标签，追加子元素
    document.getElementByTagName('head')[0].appendChild(myStyle);
  
</script>
```

![image-20210119232435543](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119232435.png)

![image-20210119232542384](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119232542.png)

![image-20210119232950372](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119232950.png)

> insertBefore

```javascript
var ee = document.getElementById('ee');
var js = document.getElementById('js');
var list = document.getElementById('list');
//要包含的节点.insertBefore(newNode,targetNode)  没有直接向后方插入的函数
list.insertBefore(js,ee);												//插入到ee的前面
```

![image-20210119233135970](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119233136.png)



# 9、操作表单（验证）

> 表单是什么？form-----DOM树

- 文本框----text
- 下拉框----select
- 单选框----radio
- 多选框----checkbox
- 隐藏域----hidden
- 密码框----password
- …

**表单的目的**：     提交信息

> 获得要   提交的信息

```javascript
 <script>
   			var input_text = document.getElementById("username");
        var boy_radio = document.getElementById("boy");
        var girl_radio = document.getElementById("girl");
        //得到输入框的值
        input_text.value 
        //修改输入框的值
        input_text.value  = "value";
        
        //对于单选框，多选框等等固定的值，boy_radio.value只能取到当前的值
        boy_radio.checked;//查看返回的结果，是否为true，如果为true，则被选中。
        girl_radio.checked = true;//赋值
        
</script>

<body>
    <form action = "#" method="post">
        <p>
            <span>用户名：</span><input type="text" id = "username" />
        </p>
        <!--多选框的值就是定义好的value-->
        <p>
            <span>性别：</span>
            <input type = "radio" name = "sex" value = "man" id = "boy"/>男
           	<input type = "radio" name = "sex" value = "woman" id = "girl"/>女
        </p>
    </form>
</body>
```

![image-20210119233726989](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119233727.png)



> 提交表单。md5加密密码，表单优化

```html
<!DOCTYPE html>
<html lang = "en">
    <head>
        <meta charset = "UTF-8">
        <title>Title</title>
        <!--MD5加密工具类-->
        <script src = "https://cdn.bootcss.com/blueimp-md5/2.10.0/js/md5.min.js">
        	
        </script>
    </head>
    <body>
        <!--表达绑定提交事件
			οnsubmit= 绑定一个提交检测的函数，true，false
			将这个结果返回给表单，使用onsubmit接收   所以写成  return aaa()
		-->
        <form action = "https://www.baidu.com" method = "post" onsubmit = "return aaa()">
            <p>
            	<span>用户名：</span><input type="text" id = "username" name = "username"/>
        	</p>
            <p>
            	<span>密码：</span><input type="password" id = "password" />
        	</p>
            <input type = "hidden" id = "md5-password" name = "password"> 
            
            <!--绑定事件 onclick 被点击-->
            <button type = "submit">提交</button>
            
        </form>
        
        <script>
        	function aaa(){
                alert(1);
                var username = document.getElementById("username");
                var pwd = document.getElementById("password");
                var md5pwd = document.getElementById("md5-password");
                //pwd.value = md5(pwd,value);  		//一瞬间密码框边长，可能会v欸猜测到密码
                md5pwd.value = mad5(pwd.value);		//将输入的密码通过mad5加密
                //可以校验判断表单内容，true就是通过提交，false就是阻止提交
                return false;
                
            }
        </script>
        
    </body>
</html>
```

# 10、jQuery

文档工具站：http://jquery.cuishifeng.cn/

javaScript和jQuery的关系？

jQuery库: 里面存在大量的**JavaScript函数**

> 获取jQuery

![image-20210120101751954](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120101752.png)

![image-20210120101737159](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120101744.png)

**引用方式：**

```html
 <script src="http://code.jquery.com/jquery-3.5.1.js"></script>
    <script src="../lib/jquery-3.5.1.js"></script>
```



**公式：$(selector).action()**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
<!--    <script src="http://code.jquery.com/jquery-3.5.1.js"></script>-->
    <script src="../lib/jquery-3.5.1.js"></script>
</head>
<body>
<a href="index.html" id="test">点我啊</a>
<script>
    //使用格式：
    //$('选择器').动作  其中选择器即css中选择器
    $('#test').click(function () {
        alert("你还真点？");
    });
</script>
</body>
</html>
```



> 选择器

```javascript
//原生js，选择器少，麻烦不好记
//标签
document.getElementByTagName();
//id
document.getElementById();
//class
document.getElementByClassName();

//jQuery css中的选择器它全部都能用！
$('p').click();//标签选择器
$('#id1').click();//id选择器
$('.class1').click;//class选择器
```



> 事件

鼠标事件、键盘事件，其他事件

```html
mousedown()(jQuery)----按下
mouseenter()(jQuery)
mouseleave()(jQuery)
mousemove()(jQuery)----移动
mouseout()(jQuery)
mouseover()(jQuery)
mouseup()(jQuery)


<!DOCTYPE html>
<html lang = "en">
    <head>
        <meta charset = "UTF-8">
        <title>Title</title>
        <script src="../lib/jquery-3.4.1.js"></script>
        <style>
            #divMove{
                width:500px;
                height:500px;
                border:1px solid red;
            }
        </style>
    </head>
    <body>
        <!--要求：获取鼠标当前的一个坐标-->
        mouse：<span id = "mouseMove"></span>
        <div id = "divMove">
            在这里移动鼠标试试
        </div>
        <script>
        	//当网页元素加载完毕之后，响应事件
            //$(document).ready(function(){})简化为下面的：
            $(function(){
                $('#divMove').mousemove(function(e){
                    $('#mouseMove').text('x:'+e.pageX+"y:"+e.pageY)
                })
            });
        </script>
    </body>
</html>
```



> 操作DOM

节点文本操作

```javascript
<body>
  <ul id ="test-ul">
    <li class="js">JavaScript</li>
		<li name = "python">Python</li>
    </ul>
  </body>

```



节点文本操作

```javascript

$('#test-ul li[name=python]').text();//获得值
$('#test-ul li[name=python]').text('设置值');//设置值
$('#test-ul').html();//获得值
$('#test-ul').html('<strong>123</strong>');//设置值
```

CSS的操作

```javascript
$('#test-ul li[name=python]').css({"color","red"});
```

元素的显示和隐藏，：本质**display:none**

```javascript
$('#test-ul li[name=python]').show();
$('#test-ul li[name=python]').hide();
```

娱乐测试

```javascript
$(window).width()
$(window).height()
$('#test-ul li[name=python]').toggle();
```

未来ajax()；

```javascript
$('#form').ajax()

$.ajax({url:"test.html",context:document.body,success:function(){
	$(this).addClass("done");
}})
```



> 
>
> 小技巧

1、如何巩固JS（看jQuery源码，看游戏源码！）

![image-20210120104118845](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120104118.png)

2、巩固HTML、CSS（扒网站，全部down下来，然后对应修改看效果~）

![image-20210120104015756](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120104015.png)