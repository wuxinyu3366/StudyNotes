# HTML笔记

## 1、初识HTML

网页，是网站中的一个页面，通常是网页是构成网站的基本元素，是承载各种网站应用的平台。通

俗的说，网站就是由网页组成的。通常我们看到的网页都是以html或html后缀结尾的文件,俗称 

HTML文件。

- **Hyper** **Text** **Markup** **Language**（**超文本标记语言**）

- 超文本:页面内可以包含图片、链接，甚至音乐、程序等非文字元素

- 标记:标签,不同的标签实现不同的功能

- 语言:人与计算机的交互工具

- ![image-20210117094737137](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210117094737137.png)

- ![image-20210117094834110](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210117094834110.png)

- ![image-20210117094938576](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210117094938576.png)

  ![image-20210117122920467](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210117122920467.png)

  **HTML基本结构：**

  ![image-20210117100223784](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210117100223784.png)

- < body >、< /body>等成对的标签，分别叫做**开放标签**和**闭合标签**，

- 单独呈现的标签（空元素），如< hr/ >;意为用/来关闭空元素。

- html注释：< !– -注释内容- –>

  

```html
<!--DOCTYPE：告诉浏览器使用什么规范（默认是html）-->
<!DOCTYPE html>
<!--语言 zh中文 en英文-->
<html lang="zh">
<!--head标签代表网页头部-->
<head>
    <!--    meta 描述性标签，表示用来描述网站的一些信息-->
    <!--    一般用来做SEO-->
    <meta charset="UTF-8">
    <meta name="keywords" content="hyx的java学习">
    <meta name="description" content="一起来学习java">
    <!--网站标题-->
    <title>Title</title>
</head>
<!--body代表主体-->
<body>
Hello World！
</body>
</html>
```

## 2、网页基本标签

- 标题标签：随着数字增大文字逐渐变小，字体是加粗的，内置字号，默认占据一行
- 段落标签
- 换行标签
- 水平线标签
- 字体样式标签
- 注释和特殊符号

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>基本标签学习</title>
</head>
<body>
<!--标题标签-->
<h1>一级标签</h1>
<h2>二级标签</h2>
<h3>三级标签</h3>
<h4>四级标签</h4>
<h5>五级标签</h5>
<h6>六级标签</h6>

<!--段落标签-->
<p>p换行1</p>
<p>p换行2</p>

<hr/><!--水平线标签-->

<!--换行标签（自闭合标签）-->
换行1 <br/>
换行2 <br/>
<!--<br/>换行标签比较紧凑，</p>段落标签有明显段间距-->

<!--粗体 斜体-->
<h1>字体样式标签</h1>
粗体：<strong>I love you </strong><br/>
斜体：<em>I love you </em><br/>

<!--特殊符号-->
空格：&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>
空格：1 2  3   4<br/>
大于号&gt;<br/>
小于号&lt;<br/>
版权符号&copy;<br/>
<!--特殊符号记忆：& 开头;结尾，只要在idea中&敲出后就有提示-->
</body>
</html>

```



### 结构标签

![image-20210117120545079](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210117120545079.png)

### 排版标签

![image-20210117120520824](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210117120520824.png)

### 基本文字标签

`font`标签处理网页中文字的显示方式

| 属性  | 代码                       | 描述                                |
| ----- | -------------------------- | ----------------------------------- |
| size  | <font size="7"></font>     | 用于设置字体的大小,最小1号，最大7号 |
| color | <font color="#fo0"></font> | 用于设置字体的颜色                  |
| face  | <font face="宋体"></font>  | 用于设置字体的样式                  |



### 文本格式化标签

使用标签实现标签的样式处理

| 标签   | 代码              | 描述     |
| ------ | ----------------- | -------- |
| b      | <b></b>           | 粗体标签 |
| strong | <strong></strong> | 加粗     |
| em     | <em></em>         | 强调字体 |
| i      | <i></i>           | 斜体     |
| small  | <small></small>   | 小号字体 |
| big    | <big></big>       | 大号字体 |
| sub    | <sub></sub>       | 上标标签 |
| sup    | <sup></sup>       | 下标标签 |
| del    | <del></del>       | 删除线   |



### 图像标签

图像格式：JPG、GIF、PNG、BMP........

```html
<img src="path" alt="text" title="text" width="x" height="v"/>
图像地址
图像的替代文字
鼠标悬停提示文字
图像高度
图像宽度
```



| 属性名 | 描述                 |
| ------ | -------------------- |
| src    | 引入图片的地址       |
| width  | 图片的宽度           |
| height | 图片的高度           |
| border | 图片的边框           |
| align  | 与图片对齐显示方式   |
| alt    | 提示信息             |
| hspace | 在图片左右设定空白   |
| vspace | 在图片的上下设定空白 |



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<!--src:资源地址
    相对地址，绝对地址
    ../上级地址
    alt：在图片加载失败的时候，就会用文字代替
    title:鼠标悬停在图片上时，所显示的名字
    width height 图片的高和宽-->
<img src="../resources/image/屏幕截图(2).png" alt="oops!图像不见了" title="123">
</body>
</html>
```



### 链接标签

在页面中使用链接标签跳转到另一页面

```html
<a href="path" target="目标窗口位置" title="123">连接文本或图像</a>
```



**href**： 必填，表示要跳转到那个页面（链接路径）

**target**：表示窗口在哪里打开

- **_blank**：在新标签中打开
- **_self**： 在自己的网页中打开

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>链接标签学习</title>
</head>
<body>
<!--href：跳转页面的地址
    文本超链接：a标签内文字：即显示的文字
    图片超链接：可以把图片放在a标签内，点击图片跳转网页
    target:表示在哪打开新网页_self:当前标签打开（默认的） _blank:新的页面中打开-->
<a href="https://www.baidu.com" target="_blank" title="123">你xxxx不会百度吗</a>
<br/>
<a href="https://www.baidu.com"><img src="../resources/image/屏幕截图(2).png" alt="oops!图像不见了" title="123"></a>

<!--锚链接
    1.需要一个标记锚
    2.跳转到标记
    #页面内跳转-->
<a name="top"></a>
<a href="#top">回到顶部</a>
<br/>
<!--也可以在网址后添加#号跳到对应网站的对应位置-->
<a href="https://www.baidu.com#down">百度底部</a> <br/>

<!--功能性链接
邮箱链接：mailto
qq链接
-->
<a href="mailto:xxxxxxqq.com">点击联系我</a>
<a target="_blank"
   href="http://wpa.qq.com/msgrd?v=xxx&uin=&site=qq&menu=yes"/>
<a target="_blank"
   href="http://wpa.qq.com/msgrd?v=xxx&uin=&site=qq&menu=yes">
    <img border="0" src="http://wpa.qq.com/pa?p=2::52" alt="点击这里加我领取小电影"
         title="点击这里加我领取小电影"/>

</body>
</html>
```

### **行内元素和块元素**

- 块元素
  - 无论内容多少，该元素独占一行

```html
例如：<p></p><hr/> <h1>...<h6>
```

块标签

使用CSS+DIV是现下流行的一种布局方式

| 标签 | 代码          | 描述                          |
| ---- | ------------- | ----------------------------- |
| div  | <div></div>   | 行级块标签,独占一行,换行      |
| span | <span></span> | 行内块标签,所有内容都在同一行 |

-  行内元素：
  - 内容撑开宽度，左右都是行内元素的可以排在一行

```html
例如：<a><strong><em>
```

### 其他标签

```html
<meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
<!--该网页的描述-->
<meta http-equiv="description" content="this is my page">
<!--该网页的编码-->
<meta http-equiv="content-type" content="text/html;charset=UTF-8">
<!--href：引入css文件的地址-->
<link rel="stylesheet" type="text/css" href="./styles.css">
<!--src：js文件的地址-->
<script type="text/javascript" src=""></script>
```



## 3、列表标签（清单标签）

### 什么是列表

列表就是信息资源的一种展示形式。它可以使信息结构化和条理化，并以列表的样式显示出来，以便浏览者能更快捷地获得相应的信息。

### 列表的分类：

- 无序列表（使用一组无序的符号定义）

- | 属性值 | 描述     | 用法举例                 |
  | ------ | -------- | ------------------------ |
  | circle | 空心圆   | <ul type="circle"></ul>  |
  | disc   | 实心圆   | <ul type="disc"></ul>    |
  | square | 黑色方块 | <ul type="square" ></ul> |

```html
<!-- 无序列表
应用范围:导航、侧边栏.....
-->
<ul>
    <li>A</li>
    <li>B</li>
    <li>C</li>
    <li>D</li>
</ul>
```

- 有序列表:使用一组有序的符号定义

- | 属性值 | 描述         | 用法举例           |
  | ------ | ------------ | ------------------ |
  | 1      | 数字类型     | <ul type="1"></ul> |
  | A      | 大写字母类型 | <ul type="A"></ul> |
  | a      | 小写字母类型 | <ul type="a"></ul> |
  | I      | 大写古罗马   | <ul type="I"></ul> |
  | i      | 小写古罗马   | <ul type="i"></ul> |

```html
<!-- 有序列表
应用范围:试卷，问答.....
-->
    <ol>
        <li>A</li>
        <li>B</li>
        <li>C</li>
        <li>D</li>
    </ol>
```

- 自定义列表:

```html
<!--自定义列表
dl：标签
dt：列表名称
dd：列表内容
-->
<dl>
    <dt>学科</dt>

    <dd>语文</dd>
    <dd>数学</dd>
    <dd>英语</dd>

    <dt>语言</dt>

    <dd>中文</dd>
    <dd>英语</dd>
    <dd>日语</dd>


</dl>
```

## 4、表格

### 表格的基本结构：

- 单元格  普通表格(table,tr,td)
- 行
- 列
- 标题列：表格的列标签(th):内容有加粗和居中效果
- 跨行:表格的行合并属性(rowspan):在同一列跨多行合并
- 跨列:表格的列合并属性(colspan):在同一行内同时合并多个列

```html
<!DOCTYPE html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>表格学习</title>
</head>
<body>
<!--表格table
行 tr
列 td
-->
<table border="1px">
    <tr>
        <!-- colspan 跨列-->
        <td colspan="3">1-1</td>
    </tr>
    <tr>
        <!-- rowspan 跨行-->
        <td rowspan="2">2-1</td>
        <td>2-2</td>
        <td>2-3</td>
    </tr>
    <tr>
        <td>3-2</td>
        <td>3-3</td>
    </tr>
</table>
</body>
</html>
```

## 5、视频和音频

- video
- audio

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>媒体元素</title>
</head>
<body>
<!--视频
		src 资源路径
        controls 控制面板
        autoplay 自动播放
-->
<video src="xxx/xxx/xxx" controls autoplay></video>
<!--音频-->
<audio src="xxx/xxx/xxx" controls autoplay></audio>
</body>
</html>
```

## 6、页面结构

| 元素名  | 描述                                               |
| ------- | -------------------------------------------------- |
| header  | 标题头部区域的内容（用于页面或者页面中的一块区域） |
| footer  | 标记脚部区域的内容（用于整个页面或页面的一块区域） |
| section | Web页面中的一块独立区域                            |
| article | 独立的文章内容                                     |
| aside   | 相关内容或应用                                     |
| nav     | 导航类辅助内容                                     |

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>页面结构分析</title>
</head>
<body>
<!--页面头部-->
<header>
    <h2>网页头部</h2>
</header>
<section>
    <h2>网页主体</h2>
</section>
<footer>
    <h2>网页脚部</h2>
</footer>
</body>
</html>
```

## 7、iframe内联框架

- 通过使用框架，你可以在同一个浏览器窗口中显示不止一个页面。每份HTML文档称为一个框架，并且每个框架都独立于其他的框架。
- 使用框架的缺点:
  - 开发人员必须同时跟踪更多的HTML文档。
  - 很难打印整张页面

```html
<iframe src="path" name="mainFrame" ></iframe>
```

- ifram标签，必须要有src属性即引用页面的地址
- 给标签加上name属性后，可以做a标签的target属性，即在内联窗口中打开链接

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>iframe学习</title>
</head>
<body>
    <!--iframe  内联框架
    src 地址
    w-h 宽度高度

    -->
<iframe src="https://www.baidu.com" name="hello" frameborder="0" width="1000px"height="600px"></iframe>

<a href="https://www.baidu.com" target="hello">点击跳转</a>
</body>
</html>
```

![image-20210117234558337](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210117234558337.png)

## 8、表单语法(重点)

![image-20210117124208402](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210117124208402.png)

from标签，action属性为所提交的**目的地址**，method选择**提交方式**
可以选择使用post或者get方式提交

- get效率高，但在url中可以看到提交的内容，不安全，不能提交大文件
- post比较安全且可以提交大文件
- ![image-20210117234640759](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210117234640759.png)

| 标签         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| input标签    | 大部分表单元素对应的标签有text、password、checkbox、radio、submit、reset、file、hidden、image和button，**默认为text**，可以提交用户名、密码等等 |
| select标签   | 下拉选择框                                                   |
| textarea标签 | 文本域                                                       |

| 属性      | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| type      | 指定元素的类型。text、password、checkbox、radio、submit、reset、file、hidden、image和button，**默认为text** |
| name      | 指定表单元素的名称（提交时所对应的key）                      |
| value     | 元素的初始值，radio必须提供                                  |
| size      | 指定表单元素的初始宽度。当type为text或者password时，以字符为单位；其他type以像素为单位 |
| maxlength | type为text或者password时，输入的最大字符数                   |
| checked   | type为radio或者checkbox时，指定按钮是否被选中                |

- ![image-20210117234706176](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210117234706176.png)
- 一些其他的属性

| 属性       | 说明                                           |
| ---------- | ---------------------------------------------- |
| readonly   | 只读，不可更改                                 |
| disable    | 禁用                                           |
| hidden     | 隐藏，虽然不可见但是会提交                     |
| id         | 标识符，可以配合label的for属性增加鼠标的可用性 |
| placehoder | text 文字域等输入框内的提示信息                |
| required   | 不能为空                                       |
| patten     | 正则表达式验证                                 |

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>登录注册</title>
</head>
<body>
<h1>注册</h1>
<!--表单from
        action：表单提交的动作，可以是交给一个网址，也可以是交给一个请求处理地址
        method：post get请求方式-->
<form action="xxx/xxx" method="get">

    <!--文本输入框：input type="text"-->
    <p>
        用户名：<input type="text" name="username" value="请输入用户名" maxlength="10" size="20">
    </p>

    <!--密码输入框：input type="password"-->
    <p>
        密&nbsp;&nbsp;&nbsp;码：<input type="password" name="password" placeholder="请输入密码" required="required">
    </p>

    <!--radio单选框标签 value即单选框的值，在提交时对应value
    name：单选框组名，在同一个组内的radio标签同时只能选中一个，name值在提交时对应key
    checked:默认被选中
    -->
    <p>
        性别：<input type="radio" value="boy" name="sex" checked/>
            <input type="radio" value="girl" name="sex"/>
    </p>

    <!--多选框-->
    <p>爱好：
        <input type="checkbox" value="b" name="hobby">打篮球
        <input type="checkbox" value="s" name="hobby" checked>唱rap
        <input type="checkbox" value="d" name="hobby">跳舞
    </p>

    <!--按钮
      input type="button"	普通按钮
      input type="image"	图像按钮
      input type="submit"	提交按钮
      input type="reset"	重置
  -->
    <p>
        <input type="button" name="btn1" value="按钮上文字">
        <!--图片按钮默认是提交：和submit类似-->
        <input type="image" src="xxx/xxx">
    </p>

    <!--下拉框：selected:默认选项-->
    <p>
        你来自：
        <select name="location">
            <option value="china">中国</option>
            <option value="us" selected>美国</option>
            <option value="japan">日本</option>
        </select>
    </p>

    <!--文本域-->
    <p>
        反馈：
        <textarea name="text" id="10" cols="30" rows="10">文本内容</textarea>
    </p>

    <!--文件域-->
    <p>
        <input type="file" name="files">
        <input type="button" name="upload" value="上传">
    </p>

    <!--邮件：会简单验证是否是邮箱地址
		url：会简单验证是否是网络地址
        number：数字验证-->
    <p>
        邮箱：<input type="email" name="email">
        邮箱2：<input type="text" name="email" pattern="/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
/^[a-z\d]+(\.[a-z\d]+)*@([\da-z](-[\da-z])?)+(\.{1,2}[a-z]+)+$/或\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*">
        url：<input type="url">
    </p>

    <!--数字验证
           max最大数量
           min 最小数量
           step 每次点击增加或减少的数量-->
    <p>
        商品数量<input type="number" name="num" max="100" min="1" step="1">
    </p>

    <!--滑块-->
    <p>
        音量：<input type="range" min="0" max="100" name="voice" step="2">
    </p>

    <!--搜索框-->
    <p>
        搜索：<input type="search" name="search">
    </p>

    <p><!--增强鼠标可用性-->
        <label for="mark">你点我试试</label>
        <input type="text" id="mark">
    </p>

    <!--submit提交表单，reset清空-->
    <p>
        <input type="submit"> <input type="reset">
    </p>
</form>
</body>
</html>
```

**表单的应用**

- 隐藏域`hidden`
- 只读`readonly`
- 禁用`disabled`

**表单的初级验证**

`placeholder`	提示信息

`required`	非空判断

`pattern` 正则表达式

​	https://www.jb51.net/tools/regexsc.htm

## 9.总结：