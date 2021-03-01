# CSS3

1.css是什么

2.CSS怎么用（快速入门）

**3.CSS选择器（重点 + 难点）**

4.美化页面（文字、阴影、超链接、列表、渐变…）

5.盒子模型

6.浮动

7.定位

8.网页动画（特效）

## 1.什么是CSS

### 1.1、什么是CSS

Cascading Style Sheet 层叠级联样式表

CSS：表现（美化网页）

字体，颜色，边距，高度，宽度，背景图片，网页定位，网页浮动

![image-20210118092411050](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118092411.png)

### 1.2、发展史

CSS1.0
CSS2.0：DIV（块）+CSS，HTML与CSS结构分离的思想，网页变得简单，SEO
CSS2.1：浮动，定位
CSS3.0：圆角、阴影、动画…浏览器兼容性~

## 2、快速入门

### 2.1.1、练习格式：

![image-20210118093142147](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118093142.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--规范，<style>可以编写CSS的代码，每一个声明最好以“;”结尾
        语法：
            选择器{
                    声明1;
                    声明2;
                    声明3;
                }	-->
    <style>
        h1{
            color: crimson;
        }
    </style>
</head>
<body>
    <h1>CSS测试</h1>
</body>
</html>

1234567891011121314151617181920212223
```

建议使用这种规范（**单独写一个css文件，用link标签引入css文件效果**）：
![image-20210118095130590](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118095130.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--规范，<style>可以编写CSS的代码，每一个声明最好以“;”结尾
        语法：
            选择器{
                    声明1;
                    声明2;
                    声明3;
                }	-->
  
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
<h1>CSS测试</h1>
</body>
</html>
```



### 2.1.2、CSS的优势：

1、内容和表现分离；
2、网页结构表现统一，可以实现复用
3、样式十分的丰富
4、建议使用独立于html的css文件
5、利用SEO，容易被搜索引擎收录！

### 2.1.3、CSS的3种常用导入方式

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <!--内部样式-->
    <style>
    h1{
        color: green;
    }
    </style>

    <!--外部样式-->
    <link rel="stylesheet" href="css/style.css" />
</head>
<body>

<!--优先级：就近原则 行内样式 > 内部样式 > 外部样式   (内部样式 和 外部样式看谁的位置离句子近用谁)-->
<!--行内样式：在标签元素中，编写一个style属性，编写样式即可-->
<h1 style="color: red">这是标签</h1>
</body>
</html>
```

```css
/*外部样式*/
h1{
    color: blue;
}
```

拓展：外部样式两种方法

- 链接式
  html

```html
<!--外部样式-->
<link rel="stylesheet" href="css/style.css" />
12
```

- 导入式
  @import是CSS2.1特有的！

```html
<!--导入式-->
<style>
    @import url("css/style.css");
</style>
1234
```

首页link和import语法结构不同，前者<link>是html标签，只能放入html源代码中使用，后者可看作为css样式，作用是引入css样式功能。import在html使用时候需要<style type="text/css">标签，同时可以直接"@import url(CSS文件路径地址);""放如css文件或css代码里引入其它css文件。
本质上两者使用选择区别不大，但为了软件中编辑布局网页html代码，一般使用link较多，也推荐使用link。

### 2.2选择器

> 作用：选择页面上的某一个后者某一类元素

#### 2.2.1、基本选择器

##### 1、标签选择器

 **选择一类标签**

 格式： **标签 { }**

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        /*标签选择器，会选择到页面上所有的这个标签的元素*/
        h1{
            color: orange;
            background: blue;
            border-radius: 10px;
        }
        h3{
            color: orange;
            background: blue;
            border-radius: 10px;
        }
        p{
            font-size: 80px;
        }
    </style>
</head>
<body>
<h1>标签选择器</h1>
<p>我爱学习</p>
<h3>学习JAVA</h3>
</body>
```

##### 2、类选择器class

 **选择所有class一致的标签，跨标签**

 格式： **.类名{}**

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        /*类选择器的格式 .class的名称{}
            好处：可以多个标签归类，是同一个class，可以复用*/
        .demo1{
            color: blue;
        }
        .demo2{
            color: red;
        }
        .demo3{
            color: aqua;
        }
    </style>
</head>
<body>
<h1 class = "demo1">类选择器：demo1</h1>
<h1 class="demo2">类选择器：demo2</h1>
<h1 class="demo3">类选择器：demo3</h1>
<p class="demo3">p标签</p>
</body>
```

##### 3、id 选择器

 **全局唯一**

 格式： **#id名{}**

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        /*id选择器：id必须保证全局唯一
            #id名称{}
            不遵循就近原则，优先级是固定的
            id选择器 > class类选择器  >  标签选择器
        */
        #demo1{
            color: red;
        }
        .demo2{
            color: green;
        }
        #demo2{
            color: orange;
        }
        h1{
            color: blue;
        }
    </style>
</head>
<body>
<h1 id="demo1" class="demo2">id选择器：demo1</h1>
<h1 class="demo2" id = "demo2">id选择器：demo2</h1>
<h1 class="demo2">id选择器：demo3</h1>
<h1 >id选择器：demo4</h1>
<h1>id选择器：demo5</h1>
</body>
```

**优先级：id选择器 > class选择器 > 标签选择器**

#### 2.2.2、高级选择器

##### 1. 层次选择器

![image-20210118121644221](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118121644.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <p>p1</p>
    <p>p2</p>
    <p>p3</p>
    <ul>
        <li>
            <p>p4</p>
        </li>
        <li>
            <p>p5</p>
        </li>
        <li>
            <p>p6</p>
        </li>
    </ul>
		<p>p7</p>
  	<p>p8</p>
</body>
</html>
```

![image-20210118151427726](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118151427.png)

- 1.**后代选择器**：在某个元素的后面

```css
/*后代选择器*/
<style>
body p{
	background:red;
}
</style>
```

![image-20210118151459659](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118151459.png)

- 2.**子选择器**，一代

```css
/*子选择器*/
<style>
body>p{
	background:orange;
}
</style>
```

![image-20210118151552419](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118151552.png)

- **相邻的兄弟选择器** 同辈

```css
/*相邻兄弟选择器：只选择一个，相邻（向下）*/
    <style>
        .active+p{
            background: red
        }
    </style>
<body>
<p>p1</p>
<p class="active">p2</p>
<p>p3</p>
<ul>
    <li>
        <p>p4</p>
    </li>
    <li>
        <p>p5</p>
    </li>
    <li>
        <p>p6</p>
    </li>
</ul>
<p>p7</p>
<p>p8</p>
</body>
```

![image-20210118151658763](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118151658.png)

- **通用选择器**

```css
<style>
/*通用兄弟选择器，当前选中元素的向下的所有兄弟元素*/
	.active~p{
	background:red;
}
</style>
<body>
<p>p1</p>
<p class="active">p2</p>
<p>p3</p>
<ul>
    <li>
        <p>p4</p>
    </li>
    <li>
        <p>p5</p>
    </li>
    <li>
        <p>p6</p>
    </li>
</ul>
<p>p7</p>
<p>p8</p>
</body>
```

![image-20210118151747091](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118151747.png)

##### 2.结构伪类选择器

伪类

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        ul li:first-child{/*ul的第一个子元素*/
            background: aqua;
        }
        ul li:last-child{/*ul的最后一个子元素*/
            background: blue;
        }
        /*选中p1：定位到父元素，选择当前的第一个元素
            选择当前p元素 的父级元素<body>，选中父级元素的第一个，并且是当前元素才生效！------顺序*/
        p:nth-child(2){
            background: orange;
        }
        /*选中父元素下的，第2个p元素,---类型*/
        p:nth-of-type(2){
            background: red;
        }
        /*选中就变化，动作型*/
        a:hover{
            color: green;
        }
    </style>
</head>
<body>
<a href="">123</a>
<p>p1</p>
<p>p2</p>
<p>p3</p>
<h3>h3</h3>
<ul>
    <li>1li1</li>
    <li>1li2</li>
    <li>1li3</li>
</ul>
<ul>
    <li>2li1</li>
    <li>2li2</li>
    <li>2li3</li>
</ul>
<a href="www.baidu.com">百度</a>
</body>
</html>
```

![image-20210118155538638](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118155538.png)

##### 3.属性选择器（常用）

id + class结合

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        <!--类选择器-->
        .demo a{
            float: left;
            display: block;
            height: 50px;
            width: 50px;
            border-radius: 10px;
            background: aquamarine;
            text-align: center;
            color: gray;
            text-decoration: none;
            margin-right: 5px;
            /*line-height:50px;*/
            font: bold 20px/50px Arial;
        }
        /*属性名，属性名=属性值（正则）
         = 表示绝对等于
         *= 表示包含
         ^= 表示以...开头
         $= 表示以...结尾
         存在id属性的元素
            a[]{}
         */
        a[id]{
            background: yellow;
        }
        a[id=first]{/*id=first的元素*/
            background: green;
        }

        a[class*="links"]{/*class 中有links的元素*/
            background: bisque;
        }

        a[href^=http]{/*选中href中以http开头的元素*/
            background: aquamarine;
        }
        a[href$=pdf]{/*选中href中以pdf结尾的元素*/
            background: aquamarine;
        }
    </style>
</head>
<body>
<p class="demo">
    <a href="http:www.baidu.com" class="links item first" id="first">1</a>
    <a href="" class="links item active" target="_blank " title="test">2</a>
    <a href="images/123.html" class="links item">3</a>
    <a href="images/1.png" class="links item">4</a>
    <a href="images/1.jpg" class="links item">5</a>
    <a href="abc" class="links item">6</a>
    <a href="/a.pdf" class="links item">7</a>
    <a href="/abc.pdf" class="links item">8</a>
    <a href="abc.doc" class="links item">9</a>
    <a href="abcd.doc" class="links item last">10</a>
</p>
</body>

```

效果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201030095642883.png#pic_center)

## 3、美化网页元素

### 3.1、为什么要美化网页

1. 有效的传递页面信息
2. 美化网页，页面漂亮才能吸引客户
3. 凸显页面的主题
4. 提高用户的体验

**span标签**：重点要突出的字，使用span标签套起来

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        #title1{
            font-size: 50px;
            color: blue;
        }
    </style>
</head>
<body>

学习语言<span id="title1">JAVA</span>
</body>
</html>
```

![image-20210118161911808](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118161911.png)



### 3.2、字体样式

- font-family：字体
- font-size：字体大小
- font-weight：字体粗细
- color：字体颜色

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        body {
            font-family: "Arial Black", 楷体;
            color: red;
        }

        h1 {
            font-size: 50px;
        }

        .p1 {
            font-weight: 600;
            color: gray;
        }
    </style>
</head>
<body>
    <h1>标题</h1>
    <p>设置为绝对定位的元素框从文档流完全删除，并相对于其包含块定位，包含块可能是文档中的另一个元素或者是初始包含块。元素原先在正常文档流中所占的空间会关闭，就好像该元素原来不存在一样。元素定位后生成一个块级框，而不论原来它在正常流中生成何种类型的框。</p>
    <p class="p1">正文2222222</p>
    <p>绝对定位使元素的位置与文档流无关，因此不占据空间。这一点与相对定位不同，相对定位实际上被看作普通流定位模型的一部分，因为元素的位置相对于它在普通流中的位置。</p>
</body>
</html>
```

![image-20210118162207937](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118162208.png)

常用写法：

```css
font-weight:bolder;/*也可以填px，但不能超过900,相当于bloder*/

/*常用写法：*/
font:oblique bloder 12px "楷体"
```





### 3.3、文本样式

1. 颜色–---------------->color:agb / rgba()
2. 文本对齐方式–---->text-align：center
3. 首行缩进–--->text-indent：2em
4. 行高–--------->line-height：300px；
5. 下划线–------>text-decoration

```css
text-decoration:underline/*下划线*/
text-decoration:line-through/*中划线*/
text-decoration:overline/*上划线*/
text-decoration:none/*超链接去下划线*/
```

#### **1.文本样式**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--
        颜色:
        单词
        RGB    #000000~#FFFFFF
        RGBA   rgba(0,0,0,0.9);

        排版：
        text-align:

        首行缩进：
        text-indent: 2em

        行高：
        line-height: 30px;
        块高：
        height：

        文字修饰符：

    -->
    <style>
        bpdy{
            color: rgba(0,0,0,0.9);
            text-align: center;
        }

        .p1{
            text-indent: 2em;
            line-height: 30px;
            height: 3000px;

        }
        .l1{text-decoration: underline;}
        .l2{text-decoration: line-through;}
        .l3{text-decoration: overline;}
    </style>
</head>
<body>
<h1>标题</h1>
<p class="l1">1111111111111</p>
<p class="l2">2222222222222</p>
<p class="l3">3333333333333</p>

<p>设置为绝对定位的元素框从文档流完全删除，并相对于其包含块定位，包含块可能是文档中的另一个元素或者是初始包含块。元素原先在正常文档流中所占的空间会关闭，就好像该元素原来不存在一样。元素定位后生成一个块级框，而不论原来它在正常流中生成何种类型的框。</p>
<p >正文2222222</p>
<p class="p1">绝对定位使元素的位置与文档流无关，因此不占据空间。这一点与相对定位不同，相对定位实际上被看作普通流定位模型的一部分，因为元素的位置相对于它在普通流中的位置。</p>

</body>
</html>
```

![image-20210118163834672](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118163834.png)

#### **2.图片、文字水平对齐**

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<!--    水平对齐，需要有参照物a，b-->
    <style>
        img,span{
            vertical-align: middle;/*而不是center*/
        }
    </style>
</head>
<body>
    <p>
        <img src="images/1.png" alt="">
        <span>123456789101123156489</span>
    </p>
</body>
</html>
```

![image-20210118164309078](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118164309.png)





### 3.4、文本，阴影和超链接伪类

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        /*默认的颜色*/
        a{
            text-decoration: none;
            color: black;
        }
        /*鼠标悬浮的颜色*/
        a:hover{
            color: orange;
            font-size:50px ;
        }
        /*鼠标按住未释放的颜色*/
        a:active{
            color: green;
        }
        /*text-shadow 阴影颜色 水平偏移 垂直偏移 阴影半径*/
        #price{
            text-shadow: blue 10px 10px 10px;
        }
    </style>
</head>
<body>

<a href="#">
    <img src="images/1.png" alt="">
</a>
<p>
    <a href="#">老婆</a>
</p>
<p>
    <a href="">作者：</a>
</p>
<p id="price">
    ￥500
</p>
</body>
</html>
```

![image-20210118165944920](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118165945.png)



### 3.5阴影：

![image-20210118165821303](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118165821.png)

```css
/*	第一个参数：表示水平偏移
	第二个参数：表示垂直偏移
	第三个参数：表示模糊半径
	第四个参数：表示颜色
*/
text-shadow:5px 5px 5px 颜色
<style>
#price{
        text-shadow: blue 10px 10px 10px;
     }
</style>
<body>
<p id="price">
    ￥500
</p>
</body>
```





### 3.6、列表ul li

主页index.html代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link href="css/style.css" rel="stylesheet" type="text/css">
</head>
<body>
<div id="nav">
    <h2 class="title">全部商品分类</h2>
    <ul>
        <li>
            <a href="#">图书</a>
            <a href="#">音像</a>
            <a href="#">数字商品</a>
        </li>
        <li>
            <a href="#">家用电器</a>
            <a href="#">手机</a>
            <a href="#">数码</a>
        </li>
        <li>
            <a href="#">电脑</a>
            <a href="#">办公</a>
        </li>
        <li>
            <a href="#">家居</a>
            <a href="#">家装</a>
            <a href="#">厨具</a>
        </li>
        <li>
            <a href="#">服饰鞋帽</a>
            <a href="#">个性化妆</a>
        </li>
        <li>
            <a href="#">礼品箱包</a>
            <a href="#">钟表</a>
            <a href="#">珠宝</a>
        </li>
        <li>
            <a href="#">食品饮料</a>
            <a href="#">保健食品</a>
        </li>
        <li>
            <a href="#">彩票</a>
            <a href="#">旅行</a>
            <a href="#">充值</a>
            <a href="#">票务</a>
        </li>
    </ul>
</div>
</body>
</html>
```

css代码：

```css
#nav{
    width: 300px;
    background: antiquewhite;
}
.title{
    font-size: 18px;
    font-weight: bold;
    text-indent: 1em;/*缩进*/
    line-height: 35px;
    background: red;
}

/*ul li*/
/*
list-style:
    non 去掉实心圆
    circle 空心圆
    decimal 数字
    square 正方形
*/
/*ul{!*nav替换效果*!
    background: antiquewhite;
}*/
ul li{
    height: 30px;
    list-style: none;
    text-indent: 1em;
}

a{
    text-decoration: none;
    font-size: 14px;
    color: black;
}
a:hover{
    color: burlywood;
    text-decoration: underline;
}
```

![image-20210118171031528](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118171031.png)



### 3.7、背景

```css
/*颜色 图片 图片位置 平铺方式*/
{
  background:red url("../images/xx.png") 270px 10px no-repeat;
}
```



1. 背景颜色：background
2. 背景图片

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
            height: 480px;
            width: 660px;
            border: 1px solid red;
            background-image: url("images/1.png");
        }
        .div1{
            background-repeat:repeat-x/*水平平铺*/
        }
        .div2{
            background-repeat:repeat-y/*垂直平铺*/
            }
        .div3{
            background-repeat:no-repeat/*不平铺*/
            }

    </style>
</head>
<body>
    <div class="div1"></div>
    <div class="div2"></div>
    <div class="div3"></div>
</body>
</html>
```

![image-20210118172011107](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118172011.png)



### 3.8、渐变

渐变背景网址：https://www.grabient.com
**径向渐变、圆形渐变**

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        body{
            background-color: #4158D0;
            background-image: -webkit-linear-gradient(309deg, #4158D0 0%, #C850C0 46%, #FFCC70 100%);
            background-image: -moz-linear-gradient(309deg, #4158D0 0%, #C850C0 46%, #FFCC70 100%);
            background-image: -o-linear-gradient(309deg, #4158D0 0%, #C850C0 46%, #FFCC70 100%);
            background-image: linear-gradient(309deg, #4158D0 0%, #C850C0 46%, #FFCC70 100%);
        }

    </style>
</head>
<body>


</body>
</html>
```

![image-20210118172837260](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118172837.png)





## 4、盒子模型

### 4.1什么是盒子模型

![image-20210118173417705](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118173417.png)

1. margin：外边距
2. padding：内边距
3. border：边框



### 4.2、边框

border：粗细 样式 颜色

1. 边框的粗细
2. 边框的样式
3. 边框的颜色

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
<!--        body总有一个默认的外边框 margin ：0 需要操作-->
h1,ul,li a body{
    margin: 0;
    padding: 0;
    text-decoration: none;
}
      <!--        border:粗细 样式 颜色-->
#box{
    width: 300px;
    border:1px solid red;
}
    h2{
        font-size: 16px;
        background-color: green;
        line-height: 30px;
        color: white;
    }

    form{
        background-color: blue;
    }
    div:nth-of-type(1) input{
        border: 3px solid black;
    }
    div:nth-of-type(2) input{
        border: 3px dashed #C850C0;
    }
    div:nth-of-type(3) input{
        border: 3px dashed orange;
    }

    </style>
</head>
<body>
<div id="box">
    <h2>用户登录</h2>
    <form action="#">
        <div>
            <span>用户名：</span>
            <input type="text">
        </div>
        <div>
            <span>密码：</span>
            <input type="password">
        </div>
        <div>
            <span>邮箱</span>
            <input type="email">
        </div>
    </form>
</div>
</body>
</html>
```

![image-20210118175426557](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118175426.png)





### 4.3、外边距----妙用：居中

```css
#box{ /*居中有前提条件：box在一个块元素中，且块元素有固定宽度*/
            width: 300px;
            border:1px solid red;
            margin:0 auto;
        }
```



![image-20210118180052504](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118180052.png)

margin-left/right/top/bottom–>表示四边，可分别设置，也可以同时设置如下

```css
margin:0 0 0 0/*分别表示上、右、下、左；从上开始顺时针*/
/*例1：居中*/
margin:0 auto /*auto表示左右自动-----------------》居中*/   
/*例2：*/
margin:4px/*表示上、右、下、左都为4px*/
/*例3*/
margin:10px 20px 30px/*表示上为10px，左右为20px，下为30px*/
```

盒子的计算方式（你这个盒子到底多大）：
margin+border+padding+内容的大小

总结：
body总有一个默认的外边距 margin:0
常见操作：初始化



### 4.4、圆角边框----border-radius

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<!--    左上 右上 右下 左下   顺时针-->
    <style>
        div{
            width: 100px;
            height:100px;
            border:10px solid red;
            border-radius: 50px 20px 10px 5px;
        }
    </style>
</head>
<body>
<div></div>
</body>
</html>
```

![image-20210118181143593](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118181143.png)

1.边框圆角（可以将头像变成圆的）

```html
<style>
        div{
            width: 100px;
            height:100px;
            border:10px solid red;
            border-radius: 100px;
        }
    </style>
```

![image-20210118181241284](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118181241.png)

2.半圆

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--    左上 右上 右下 左下
            圆圈：  圆角：半径！
    -->
    <style>
        div{
            width: 100px;
            height:50px;    /*需要调整长宽*/
            margin: 30px;
            background-color: red;
            border-radius: 50px 50px 0px 0px;
        }
    </style>
</head>
<body>
<div></div>
</body>
</html>
```

![image-20210118181628974](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118181629.png)







### 4.5、盒子阴影

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
            width: 100px;
            height: 100px;
            border: 10px solid red;
            box-shadow: 10px 10px 100px yellow;
        }
        img{
            box-shadow: 10px 10px 100px yellow;
        }
    </style>
</head>
<body>
    <div>
    </div>
    <img src="images/1.png">
</body>
</html>
```

![image-20210118183235743](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118183235.png)





## 5、浮动

### 5.1标准文档流

![image-20210118185722927](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118185723.png)

**块级元素**：独占一行 h1~h6 、p、div、 列表…

**行内元素**：不独占一行 span、a、img、strong

注： 行内元素可以包含在块级元素中，反之则不可以

### 5.2、display（重要）

1. block：块元素
2. inline：行内元素
3. inline-block：是块元素，但是可以内联，在一行

> 这也是一种实现行内元素排列的方式，但是我们很多情况用float

1. none：消失

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--block 块元素
        inline 行内元素
        inline-block 是块元素，但是可以内联 ，在一行
    -->
    <style>
        div{
            width: 100px;
            height: 100px;
            border: 1px solid red;
            display: inline-block;
        }
        span{
            width: 100px;
            height: 100px;
            border: 1px solid red;
            display: inline-block;
        }
    </style>
</head>
<body>
    <div>div块元素</div>
    <span>span行内元素</span>
</body>
</html>
```

![image-20210118203354542](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118203354.png)

QQ会员登录导航

```css
li {
    list-style: none;
    display: inline-block;
    padding-right: 19px;
}
div{
    width: 1080px;
    height: 72px;
    border: 1px solid gray;
    background: gray 50px center no-repeat ;
    background-size: 110px 60px;
}
ul{
    padding-left: 210px;
    margin-top: 25px;
}
a{
    font-size: 14px;
    color:white;
    text-decoration: none;
}
a:hover{
    text-decoration: none;
    color: #2633ff;
}
.entry{
    margin-left: 40px;
    padding: 5px 22px;
    border: 1px solid #feff49;
    border-radius: 15px;
    color: #fcfc3a;
}
li:nth-last-child(2){
    padding-right: 0;
}
li:nth-last-child(2) a:hover{
    color: #efcc2c;
}
.open{
    border: 1px solid yellow;
    border-radius: 15px;
    padding: 5px 25px;
    background-color: #ffe846;
    color: #eeba15;
    font-weight: bold;
}
li:nth-last-child(1) a:hover{
    color: #d3940b;
}
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="css/style.css" />
</head>
<body>
<div>
    <nav>
        <ul>
            <li><a href="#">功能特权</a></li>
            <li><a href="#">游戏特权</a></li>
            <li><a href="#">生活特权</a></li>
            <li><a href="#">会员活动</a></li>
            <li><a href="#">成长体系</a></li>
            <li><a href="#">年费专区</a></li>
            <li><a href="#">超级会员</a></li>
            <li><a href="#" class="entry">登录</a></li>
            <li><a href="#" class="open">开通超级会员</a></li>
        </ul>
    </nav>
</div>
</body>
</html>
```

![image-20210118195138767](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118195138.png)



### 5.3、float：left/right左右浮动

**标准文档流**(默认布局)是：       从上到下，从左到右，遇块(块级元素)换行。

浮动层：给元素的**float**属性赋值后，就是脱离文档流，进行left/right**左右浮动**，紧贴着父元素 (默认为body文本区域) 的左右边框 。

而此浮动元素在文档流空出的位置，由**后续的(非浮动)元素填充上去**：**块级元素**直接填充上去.

若跟浮动元素的范围发生重叠，**浮动元素**覆盖**块级元素**。

**Float**有4个值：

- ​    left：元素向左浮动
- 　right：元素向右浮动
- 　none：默认值
- 　inherit ：从父元素继承float属性。

浮动后的div宽度会变成0，但是其内边框可能撑起它的宽和高。

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Insert title here</title>
    <style type="text/css">
        .outside{
            font-size:12px;
            font-family: Arail;
            padding:10px;
            background-color:#fffcd3;
            border:1px solid black;
            width:50%;
        }
        .inside1{
            padding:10px;
            border:1px dashed black;
            background:#a9d6ff;
            margin:5px;
            float:left;
            /* 1.div1向左漂浮之后，宽度为0
               2.div1移到父元素的左边
               3.div1的原始位置被空出来，由后面的html元素来补上。
            */
        }
        .inside2{
            padding:10px;
            border:1px dashed black;
            background:#ffacd3;

        }
    </style>
</head>
<body>
<div class="outside">
    <div class="inside1">内部div1</div>
    <div class="inside2">内部div2</div>
</div>
</body>
</html>
```

![image-20210118200104520](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118200104.png)



**div浮动对html元素的影响**

如果浮动的div前面有同级别html元素，该浮动的div会排在html元素后面浮动，不会覆盖html元素

总结：div的浮动对前面的html元素没影响，对后面的html元素有影响。

```html
<div class="inside2">内部div3</div>
    <div class="inside1">内部div1</div>
    <div class="inside2">内部div2</div>
```

![image-20210118200247841](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118200247.png)



**CSS中多个div浮动**

多个同级块元素同时在一个方向浮动，则从该方向上水平依次排列

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>div浮动</title>
    <style type="text/css">
        .outside{
            font-size:12px;
            font-family: Arail;
            padding:10px;
            background-color:#fffcd3;
            border:1px solid black;
            width:50%;
        }
        .inside1{
            padding:10px;
            border:1px dashed black;
            background:#a9d6ff;
            margin-bottom:5px;
        }
        .inside2{
            padding:10px;
            border:1px dashed black;
            background:#ffacd3;
            margin:5px;
            float:left;
        }
    </style>
</head>
<body>
<h1>div浮动</h1>
<div class="outside">
    <div class="inside1">内部div1</div>
    <!--
        如果多个同级html元素同时浮动，这几个html元素就会从左到右浮动排列
        脱离了div的自动换行
     -->
    <div class="inside2">内部div2</div>
    <div class="inside2">内部div3</div>
    <div class="inside2">内部div4</div>
    <div class="inside2">内部div5</div>
    <div class="inside1">内部div6</div>
</div>
</body>
</html>
```



![image-20210118200443886](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118200444.png)



**CSS消除div漂浮的影响**

前面div的浮动会影响后面的div的布局，如果想消除该影响可以使用clear:left |  right | both

未消除之前：

![image-20210118200804446](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118200804.png)

消除之后：

![image-20210118200853331](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118200853.png)

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Insert title here</title>
    <style type="text/css">
        .outside{
            font-size:12px;
            font-family: Arail;
            padding:10px;
            background-color:#fffcd3;
            border:1px solid black;
            width:50%;
        }
        .inside1{
            padding:10px;
            border:1px dashed black;
            background:#a9d6ff;
            margin:5px;
            float:left;
            /* 1.div1向左漂浮之后，宽度为0
               2.div1移到父元素的左边
               3.div1的原始位置被空出来，由后面的html元素来补上。
            */
        }
        .inside2{
            padding:10px;
            border:1px dashed black;
            background:#a9d6ff;
            margin:5px;
            float:right;
        }
        .inside3{
            padding:10px;
            border:1px dashed black;
            background:#ffacd3;
            clear:both;
            /* left消除左边漂浮的影响
               right消除右边漂浮的影响
               both消除两边漂浮的影响
              */
        }
    </style>
</head>
<body>
<div class="outside">
    <div class="inside1">内部div1</div>
    <div class="inside2">内部div2</div>
    <div class="inside3">内部div3</div>
</div>
</body>
</html>
```



### 5.4、overflow及父级边框塌陷问题

clear：

- right：右侧不允许有浮动元素
- left：左侧不允许有浮动元素
- both：两侧不允许有浮动元素

none：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="css/style.css" />
</head>
<body>
<div id="father">
    <div class="layer01"><img src="img/1.jpg" alt=""></div>
    <div class="layer02"><img src="img/2.jpg" alt=""></div>
    <div class="layer03"><img src="img/3.jpg" alt=""></div>
    <div class="layer04">
        浮动的盒子可以向左，也可以向右。。。。。哈哈啊哈哈哈哈哈哈
    </div>
    <!-- <div class="clear"></div>-->
</div>
</body>
</html>
```

```css
div{
    margin: 10px;
    padding: 5px;
}
#father{
    border: 1px #000 solid;
    /*height: 500px;*/

    /*overflow: hidden;*/
}
/*#father:after{
    content: '';
    display: block;
    clear: both;
}*/
.layer01{
    border: 1px #F00 dashed;
    display: inline-block;
    float: left;
}
.layer02{
    border: 1px #00F dashed;
    display: inline-block;
    float: left;
}
.layer03{
    border: 1px #060 dashed;
    display: inline-block;
    float: left;
}
/*

clear: left; 左侧不允许有浮动元素
clear: right; 右侧不允许有浮动元素
clear: both; 两侧不允许有浮动元素

*/
.layer04{
    border: 1px #666 dashed;
    font-size: 12px;
    line-height: 23px;
    display: inline-block;
    float: left;
    clear: both;
}
/*
.clear{
    clear: both;
    margin: 0;
    padding: 0;
}
*/
```



问题出现了： 蓝色框不包含所有东西了

![image-20210118202656324](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118202656.png)

#### **解决塌陷问题方案：**

#### 方案一：增加父级元素的高度；

```css
#father{
    border: 1px #000 solid;
    height: 500px;
}
```



![image-20210118202718969](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118202719.png)

#### 方案二：增加一个空的div标签，清除浮动

```css
<body>
     <div class="clear"></div>
</body>

<style>
	.clear{
		clear:both;
		margin:0;
		padding:0;
}
</style>
```

![image-20210118202843345](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118202843.png)

#### 方案三：在父级元素中增加一个overflow属性

有超出父类可以表示范围的元素，父级元素添加

```css
overflow:hidden/*隐藏超出部分*/
overflow：scoll/*滚动*/

#father{
    border: 1px #000 solid;
    /*height: 500px;*/

    overflow: hidden;
}
```

![image-20210118202947267](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118202947.png)

#### 方案四：父类添加一个伪类:after

等同于方案二：增加一个空的div标签，清除浮动。

```css
#father:after{
    content: '';
    display: block;
    clear: both;
}
```

![image-20210118203257030](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118203257.png)

小结：

1. 浮动元素增加空div----> 简单、代码尽量避免空div
2. 设置父元素的高度-----> 简单，但是元素假设有了固定的高度，可能就会超出范围
3. overflow----> 简单，下拉的一些场景避免使用
4. **父类添加一个伪类:after**（推荐）----> 写法稍微复杂，但是没有副作用，**推荐使用**

### 5.5、display与float对比

1. display：方向不可以控制
2. float：浮动起来的话会**脱离标准文档流**，所以要解决**父级边框**塌陷的问题。





## 6、定位

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>初始样式</title>
    <style>

        div{
            margin: 10px;
            padding: 5px;
            font-size: 12px;
            line-height: 25px;
        }
        #father{
            border: #ffa538 1px solid;
            padding: 0;
        }
        #first{
            border: #b3ff38 1px solid;
            background-color: #ffa538;         
        }
        #second{
            border: #427b11 1px solid;
            background-color: #66c77f;
        }
        #third{
            background-color: #b3ff38;
            border: #38d7ff 1px solid;
        }
    </style>
</head>
<body>
<div id="father">
    <div id="first">第一个盒子</div>
    <div id="second">第二个盒子</div>
    <div id="third">第三个盒子</div>
</div>
</body>
</html>
```



![image-20210118204128135](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118204128.png)

### 6.1、相对定位relative

相对定位：**positon：relstive；**
相对于原来的位置，进行指定的偏移，相对定位的话，它仍然**在标准文档流中**！原来的位置会被保留

```css
top:-20px;/*向上偏移20px*/
left:20px;/*向右偏移20px*/
bottom:10px;/*向上偏移10px*/
right:20px;/*向左偏移20px*/
1234
```

代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>相对定位</title>
    <!--相对定位
            相对于自己原来的位置进行偏移
    -->
    <style>
        body{
            padding: 20px;
        }
        div{
            margin: 10px;
            padding: 5px;
            font-size: 12px;
            line-height: 25px;
        }
        #father{
            border: #ffa538 1px solid;
            padding: 0;
        }
        #first{
            border: #b3ff38 1px solid;
            background-color: #ffa538;
            position: relative;/*相对定位：上下左右*/
            top: -20px;/*向上偏移20px*/
            left: 20px;/*向右偏移20px*/
        }
        #second{
            border: #427b11 1px solid;
            background-color: #66c77f;
        }
        #third{
            background-color: #b3ff38;
            border: #38d7ff 1px solid;
            position: relative;
            bottom: -10px;/*向下偏移10px*/
        }
    </style>
</head>
<body>
<div id="father">
    <div id="first">第一个盒子</div>
    <div id="second">第二个盒子</div>
    <div id="third">第三个盒子</div>
</div>
</body>
</html>

```

![image-20210118204509226](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118204509.png)

练习：![在这里插入图片描述](https://img-blog.csdnimg.cn/20201030095804693.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTE0NTcyNg==,size_16,color_FFFFFF,t_70#pic_center)

实现代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        #box{
            height: 300px;
            width: 300px;
            border: 2px red solid;
            padding: 10px;
        }
        a{
            height: 100px;
            width: 100px;
            background-color: #ee73b7;
            color: white;
            text-align: center;
            text-decoration: none;
            line-height: 100px;/*设置行距100px*/
            display: block;/*设置方块*/
        }
        a:hover{
            background: #4158D0;
        }
        .a2{
            position: relative;
            left: 200px;
            top: -100px;
        }
        .a4{
            position: relative;
            left: 200px;
            top: -100px;
        }
        .a5{
            position: relative;
            left: 100px;
            top: -300px;
        }
    </style>
</head>
<body>
<body>
<div id="box">
    <div class="a1"><a href="" >连接1</a></div>
    <div class="a2"><a href="" >连接2</a></div>
    <div class="a3"><a href="" >连接3</a></div>
    <div class="a4"><a href="" >连接4</a></div>
    <div class="a5"><a href="" >连接5</a></div>
</div>
</body>
</body>
</html>
```

![image-20210118204613246](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118204613.png)



### 6.2、绝对定位-absolute和固定定位-fixed

![image-20210118235754712](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118235801.png)

#### 绝对定位：

定位：基于xxx定位，上下左右~
1、没有父级元素定位的前提下，相对于浏览器定位

2、假设父级元素存在定位，我们通常会相对于父级元素进行偏移

3、在父级元素范围内移动

相对于父级或浏览器的位置，进行指定的偏移，绝对定位的话，它不在在标准文档流中，原来的位置不会被保留

总结：相对一父级或浏览器的位置，进行指定的偏移，绝对定位的话，它不在标准文档流中，原来的位置不会被保留

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
            margin: 10px;
            padding: 5px;
            font-size: 12px;
            line-height: 25px;
        }
        #father{
            border: 1px solid #666;
            padding: 0;
            position: relative;
        }
        #first{
            background-color: #a13d30;
            border: 1px dashed #b27530;
        }
        #second{
            background-color: #255099;
            border: 1px dashed #255066;
            position: absolute;
            left: 50px;
        }
        #third{
            background-color: #1c6699;
            border: 1px dashed #1c6615;
        }
    </style>
</head>
<body>
<div id="father">
    <div id="first">第一个盒子</div>
    <div id="second">第二个盒子</div>
    <div id="third">第三个盒子</div>
</div>
</body>
</html>
```

![image-20210119000357246](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119000357.png)



#### 相对定位

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        body{
            height: 1000px;
        }
        div:nth-of-type(1){
            width: 100px;
            height: 100px;
            background-color: red;
            position: absolute;/*absolute 绝对定位*/
            right: 0;
            bottom: 0;
        }
        div:nth-of-type(2){
            width: 50px;
            height: 50px;
            background-color: #b3ff38;
            position: fixed;/*fixed 固定定位*/
            right: 0;
            bottom: 0;
        }
    </style>
</head>
<body>
<div>div1</div>
<div>div2</div>    <!--fixed 固定定位-->
</body>
</html>
```

![image-20210118204743664](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118204743.png)

![image-20210118204847381](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210118204847.png)

### 6.3、z-index

![image-20210119000925072](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119000925.png)

图层-z-index：默认是0，最高无限~999

```css
z-index: 999;
```

index.html代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="css/style.css" type="text/css">
    <style></style>
</head>
<body>
<div id="content">
    <ul>
        <li><img src="images/2020.jpg" alt=""/></li>
        <li class="tipText">学习微服务，找狂神</li>
        <li class="tipBg"></li>
        <li>时间：2099-01-01</li>
        <li>地点：月球一号基地</li>
    </ul>
</div>
</body>
</html>
1234567891011121314151617181920
```

css代码：  opacity: 0.5;背景透明度

```css
#content{
    width: 250px;
    padding: 0px;
    margin: 0px;
    overflow: hidden;
    font-size: 12px;
    line-height: 25px;
    border: 1px solid yellow;
}
ul,li{
    padding: 0px;
    margin: 0px;
    list-style: none;
}
/*父级元素相对定位*/
#content ul{
    position: relative;
}
.tipText,.tipBg{
    position: absolute;
    width: 380px;
    height: 25px;
    top:216px
}
.tipText{
    color: white;
    z-index: 999;
}
.tipBg{
    background: orange;
    opacity: 0.5;/*背景透明度*/
    filter: alpha(opacity=50);/*背景透明度*/
}
```

![image-20210119001551009](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210119001551.png)



## 7、动画及视野拓展

css做动画过于繁琐，已有很多工具间接性做出

百度搜索canvas动画、[卡巴斯基监控站](https://cybermap.kaspersky.com/cn)（仅作了解）

## 8、总结

![CSS导图](https://img-blog.csdnimg.cn/20201030100754543.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTE0NTcyNg==,size_16,color_FFFFFF,t_70#pic_center)