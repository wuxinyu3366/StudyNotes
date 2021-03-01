# 1、基本概念

## **1.1、前言**

web开发：

- web，网页的意思 ， www.baidu.com
- **静态web**
  - html，css 
  - 提供给所有人看的，数据始终不会发生变化！
- **动态web**
  淘宝，几乎是所有的网站； 提供给所有人看的数据始终会发生变化，每个人在不同的时间，不同的地点看到的信息各不相同！
- 技术栈：Servlet/JSP，ASP，PHP

在Java中，动态web资源开发的技术统称为JavaWeb；

## **1.2、web应用程序**

web应用程序：可以提供浏览器访问的程序；

- a.html、b.html…多个web资源，这些web资源可以被外界访问，对外界提供服务；
- 你们能访问到的任何一个页面或者资源，都存在于这个世界的某一个角落的计算机上。
- URL
- 这个统一的web资源会被放在同一个文件夹下，web应用程序–>Tomcat：服务器
- 一个web应用由多部分组成 （静态web，动态web）

  - html，css，js，
  - jsp，servlet 
  - Java程序 
  - jar包 
  - 配置文件 （Properties）

web应用程序编写完毕后，若想提供给外界访问：需要一个**服务器**来统一管理；

## **1.3、静态web**

- *.htm, *.html,这些都是网页的后缀，如果服务器上一直存在这些东西，我们就可以直接进行读取。

![image-20210122201442186](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122201442.png)

- 静态web存在的缺点：
  - Web页面无法动态更新，所有用户看到都是同一个页面。
    - 1.轮播图，点击特效：伪动态
    - 2.JavaScript[实际开发中，它用的最多]
    - 3.VBScript
  - 它无法和数据库交互（数据无法持久化，用户无法交互）

## **1.4、动态web**

页面会动态展示： “Web的页面展示的效果因人而异”；
![image-20210122201617253](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122201620.png)
缺点：

- 加入服务器的动态web资源出现了错误，我们需要重新编写我们的**后台程序**,重新发布； 停机维护。

优点：

- Web页面可以**动态更新**，所有用户看到都不是同一个页面
- 它可以与**数据库交互** （数据持久化：注册，商品信息，用户信息…）

![image-20210122201724043](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122201724.png)

新手村：–魔鬼训练（分析原理，看源码）–> PK场

# 2、web服务器

## **2.1 技术讲解**

**ASP**:

- 微软：国内最早流行的就是ASP；
- 在HTML中嵌入了VB的脚本， ASP + COM；
- 在ASP开发中，基本一个页面都有几千行的业务代码，页面极其换乱
- 维护成本高！
- C#
- IIS

```html
<h1>
    <h1><h1>
        <h1>
            <h1>
                <h1>
        <h1>
            <%
            System.out.println("hello")
            %>
            <h1>
                <h1>
   <h1><h1>
<h1>
```

**php：**

- PHP开发速度很快，功能很强大，跨平台，代码很简单 （70% , WP）
- 无法承载大访问量的情况（局限性）

**JSP/Servlet :**

B/S：浏览器和服务器

C/S: 客户端和服务器

- sun公司主推的B/S架构
- 基于Java语言的 (所有的大公司，或者一些开源的组件，都是用Java写的)
- 可以承载三高（高并发、高可用、高性能）问题带来的影响；
- 语法像ASP ， ASP–--转----->JSP , 加强市场强度；

 ….................

## **2.2、web服务器**

服务器是一种**被动的操作**，用来处理用户的一些请求和给用户一些响应信息；

**IIS**

微软的； ASP…,Windows中自带的

**Tomcat**

![1567824446428](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122202606.png)

**面向百度编程**（新技术的一个快速上手的方法）；

Tomcat是Apache 软件基金会（Apache Software Foundation）的Jakarta 项目中的一个核心项目，最新的Servlet 和JSP 规范总是能在Tomcat 中得到体现，因为Tomcat 技术先进、性能稳定，而且免费，因而深受Java 爱好者的喜爱并得到了部分软件开发商的认可，成为目前比较流行的Web 应用服务器。

Tomcat 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用服务器，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP 程序的首选。对于一个Java初学web的人来说，它是最佳的选择

Tomcat 实际上运行JSP 页面和Servlet。Tomcat最新版本为9.0。

…

**工作3-5年之后，可以尝试手写Tomcat服务器；**

下载tomcat：

1. 安装 or 解压
2. 了解配置文件及目录结构
3. 这个东西的作用

# 3、Tomcat

## **3.1、 安装tomcat**

tomcat官网：http://tomcat.apache.org/
![image-20210122203058100](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122203058.png)
![image-20210122203113599](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122203113.png)

## **3.2、Tomcat启动和配置**

文件夹作用：

![image-20210122203129543](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122203129.png)

启动、关闭Tomcat

![image-20210122203152237](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122203152.png)

访问测试：http://localhost:8080/

可能遇到的问题：

1. Java环境变量没有配置

2. 闪退问题：需要配置兼容性

3. 乱码问题：配置文件中设置

   ```html
   java.util.logging.ConsoleHandler.encoding = GBK
   ```

   

## **3.3、配置**

![image-20210124103424412](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124103431.png)

可以配置启动的端口号

1. tomcat的默认端口号为：8080
2. mysql：3306
3. http：80
4. https：443

![image-20210124104015557](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124104015.png)

```java
<Connector port="8081" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" />

```

![image-20210124103747566](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124103747.png)



可以配置主机的名称

![image-20210124104030453](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124104030.png)

- 默认的主机名为：localhost->127.0.0.1
- 默认网站应用存放的位置为：webapps

```java
<Host name="www.qinjiang.com"  appBase="webapps"
        unpackWARs="true" autoDeploy="true">
```

***高难度面试题***：

**面试题：如果改成www.xxx.com类似的域名能不能访问到Tomcat主页面？**
不能访问到
如果想要访问到：
windows C盘

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124104235.png)

这里面是你的ip映射相关文件

![image-20210124104252675](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124104252.png)

可以看到ip对应的名称

![image-20210124104308015](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124104308.png)

在这个文件的最后加上一行域名映射,然后重启Tomcat就可以访问到了

```bash
127.0.0.1	www.xxx.com
```



**面试题:请你谈谈网站是如何进行访问的！**

1. 输入一个域名；回车

2. 检查本机的 C:\Windows\System32\drivers\etc\hosts配置文件下有没有这个域名映射；

   *有：直接返回对应的ip地址，这个地址中，有我们需要访问的web程序，可以直接访问

   ```java
   127.0.0.1 www.qinjiang.com
   ```


   *没有：去**DNS服务器**找，找到的话就返回，找不到就返回找不到；

   ![image-20210124104546531](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124104546.png)

3. 可以配置一下环境变量（可选性）

## **3.4、发布一个web网站**

**不会就先模仿**

> 将自己写的网站，放到服务器(Tomcat)中指定的web应用的文件夹（webapps）下，就可以访问了

1.进入webapps目录，复制一份ROOT文件夹

![image-20210124104749118](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124104749.png)

2.将复制好的副本改名，然后删除部分内容（选中的全删了）

![image-20210124104808415](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124104808.png)

3.进入剩下的WEB-INF文件夹，发现有一个web.xml文件，里面的名字和描述都可以删掉

![image-20210124104852281](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124104852.png)

4.回到上级目录，新建一个网页index.html,在里面写一些内容

![image-20210124104918582](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124104918.png)

5.然后进入bin目录下启动Tomcat

6.启动后在浏览器中输入（index.html是默认访问的，不需要写）
http://localhost:8080/你复制ROOT后改的名字

![image-20210124110012718](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124110012.png)

网站应该有的结构

```xml
--webapps ：Tomcat服务器的web目录
    -ROOT
    -kuangstudy ：网站的目录名
        - WEB-INF
            -classes : java程序
            -lib：web应用所依赖的jar包
            -web.xml ：网站配置文件
        - index.html 默认的首页
        - static 
            -css
                -style.css
            -js
            -img
         -.....

```

HTTP协议 ： 面试

Maven：构建工具

- Maven安装包

Servlet 入门

- HelloWorld！
- Servlet配置
- 原理

# 4、Http

## 4.1、什么是HTTP

HTTP（超文本传输协议）是一个简单的**请求-响应协议**，它通常运行在TCP之上。

- 文本：html，字符串，~ ….
- 超文本：图片，音乐，视频，定位，地图…….
- 80

Https：s代表   安全的

- 443

## **4.2、两个时代**

- http1.0
-  HTTP/1.0：客户端可以与web服务器连接后，只能获得一个web资源，断开连接
- http2.0
-  HTTP/1.1：客户端可以与web服务器连接后，可以获得多个web资源。

## **4.3、Http请求**

- 客户端—发请求（Request）—服务器

www.baidu.com百度：

![image-20210124112733666](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124112733.png)

```java
Request URL:https://www.baidu.com/   //请求地址
Request Method:GET           //get方法/post方法
Status Code:200 OK           //状态码：200
Remote（远程） Address:14.215.177.39:443   //远程地址

Accept:text/html  
Accept-Encoding:gzip, deflate, br
Accept-Language:zh-CN,zh;q=0.9    //语言
Cache-Control:max-age=0
Connection:keep-alive

```

**1、请求行**

![image-20210124113319271](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124113319.png)

- 请求行中的请求方式：GET
- 请求方式：**Get，Post，**HEAD,DELETE,PUT,TRACT…
-  get：请求能够携带的参数比较少，大小有限制，会在浏览器的URL地址栏显示数据内容，不安全，但高效   1次
-  post：请求能够携带的参数没有限制，大小没有限制，不会在浏览器的URL地址栏显示数据内容，安全，但不高效。  2次

https://www.cnblogs.com/logsharing/p/8448446.html

通过这里调节网络可以比较出速度

![image-20210124114451782](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124114451.png)

**2、消息头**

```java
Accept：告诉浏览器，它所支持的数据类型
Accept-Encoding：支持哪种编码格式  GBK   UTF-8   GB2312  ISO8859-1
Accept-Language：告诉浏览器，它的语言环境
Cache-Control：缓存控制
Connection：告诉浏览器，请求完成是断开还是保持连接
HOST：主机..../.
```

## **4.4、Http响应**

- 服务器—响应-----客户端

百度：

![image-20210124114514016](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124114514.png)

```java
Cache-Control:private    //缓存控制
Connection:Keep-Alive    //连接
Content-Encoding:gzip    //编码
Content-Type:text/html   //类型
```

**1.响应体**

```java
Accept：告诉浏览器，它所支持的数据类型
Accept-Encoding：支持哪种编码格式  GBK   UTF-8   GB2312  ISO8859-1
Accept-Language：告诉浏览器，它的语言环境
Cache-Control：缓存控制
Connection：告诉浏览器，请求完成是断开还是保持连接
HOST：主机..../.
Refresh：告诉客户端，多久刷新一次；
Location：让网页重新定位；

```

**2、响应状态码**
200：请求响应成功 200

3xx：请求重定向

- 重定向：你重新到我给你新位置去；

4xx：找不到资源 404

- 资源不存在；

5xx：服务器代码错误 500 502:网关错误

**常见面试题：**

当你的浏览器中地址栏输入地址并回车的一瞬间到页面能够展示回来，经历了什么？

# 5、Maven

**我为什么要学习这个技术？**

- 在Javaweb开发中，需要使用大量的jar包，我们手动去导入；
- 如何能够让一个东西**自动帮我导入和配置**这个jar包。

由此，Maven诞生了！

## **5.1 Maven项目架构管理工具**

我们目前用来就是方便导入jar包的！

Maven的核心思想：**约定大于配置**

- 有约束，不要去违反。

Maven会规定好你该如何去编写我们的Java代码，必须要按照这个规范来；

## **5.2 下载安装Maven**

官网：https://maven.apache.org/

![image-20210124120415600](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124120415.png)

![1567842350606](https://img-blog.csdnimg.cn/20200907163138991.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMyMTQ1MDk3,size_16,color_FFFFFF,t_70#pic_center)

下载完成后，解压即可；

小狂神友情建议：电脑上的所有环境都放在一个文件夹下，方便管理；

## **5.3 配置环境变量**

在我们的系统环境变量中

配置如下配置：

- `M2_HOME` maven目录下的bin目录
- `MAVEN_HOME` maven的目录
- 在系统的`path`中配置 `%MAVEN_HOME%\bin`

![image-20210124120802635](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124120802.png)

测试Maven是否安装成功，保证必须配置完毕！

## **5.4 阿里云镜像**

![1567844609399](https://img-blog.csdnimg.cn/20200907163213589.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMyMTQ1MDk3,size_16,color_FFFFFF,t_70#pic_center)

- 镜像：mirrors
- 作用：加速我们的下载
- 国内建议使用阿里云的镜像

```java
<mirror>
    <id>nexus-aliyun</id>  
    <mirrorOf>*,!jeecg,!jeecg-snapshots</mirrorOf>  
    <name>Nexus aliyun</name>  
    <url>http://maven.aliyun.com/nexus/content/groups/public</url> 
</mirror>
```

![image-20210124121046026](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124121046.png)

## **5.5 本地仓库**

在本地的仓库，远程仓库；

建立一个本地仓库：localRepository

![image-20210124121917178](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124121917.png)

```java
<localRepository>D:\Programming software\Environment\apache-maven-3.6.3\maven-localRepository</localRepository>
```



## **5.6、在IDEA中使用Maven**

1. **启动IDEA**
2. 创建一个MavenWeb**项目**

![image-20210124144912722](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124144912.png)

![image-20210124144928074](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124144928.png)

![image-20210124144952611](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124144952.png)

![image-20210124145022905](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145023.png)

![1567844956177](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145055.png)

![1567845029864](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145058.png)

3.**等待项目初始化完毕**

![image-20210124145202371](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145202.png)

初始化完成后，如下图所示

![image-20210124145239157](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145239.png)

1. 观察maven仓库中多了什么东西？

![image-20210124145308797](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145308.png)

**4.IDEA中的Maven设置**

注意：IDEA项目创建成功后，看一眼Maven的配置

![image-20210124134506045](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124134506.png)

![image-20210124145425904](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145426.png)

**5.到这里，Maven在IDEA中的配置和使用就OK了!**

![image-20210124145401473](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145401.png)

## **5.7、创建一个纯净的Maven项目**

![image-20210124135017146](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124135017.png)

![image-20210124134957727](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124134957.png)

![image-20210124145735314](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145735.png)

这个只有在Web应用下才会有！

![1567845782034](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124135027.png)

## **5.8 标记文件夹功能**

纯净的maven项目是无法创建类的：我们需要进行的是**标记文件夹**

![image-20210124145503849](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145503.png)

第一种方式：

![image-20210124145520221](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145520.png)

然后就发现，可以创建Java Class文件了

![image-20210124145530368](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145530.png)

同理，还要把resources文件夹标记为资源目录Resources Root（如果已经标记过就不用标记了）

第二种方式：

![image-20210124145557511](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145557.png)

通过点击高亮进行标记

![image-20210124145614707](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145614.png)

### Maven侧边栏解释

![image-20210124145654652](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145654.png)

## **5.9 在 IDEA中配置Tomcat**

![image-20210124150122666](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124150122.png)

这里选择本地（Local）的Tomcat

![image-20210124150145659](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124150145.png)



![image-20210124150205267](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124150205.png)

解决警告问题

必须要的配置：**为什么会有这个问题：我们访问一个网站，需要指定一个文件夹名字；**

![image-20210124150242372](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124150242.png)

![image-20210124150300434](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124150300.png)

![image-20210124150315249](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124150315.png)

启动Tomcat

![image-20210124150337102](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124150337.png)

启动成功后，会打开浏览器显示helloworld

![1567846640372](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124141214.png)

![image-20210124150404265](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124150404.png)

## **5.10 pom文件**

pom.xml 是Maven的核心配置文件

![1567846784849](https://img-blog.csdnimg.cn/20200907163605752.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMyMTQ1MDk3,size_16,color_FFFFFF,t_70#pic_center)

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!--Maven版本和头文件-->
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <!--这里就是我们刚才配置的GAV-->
  <groupId>com.kuang</groupId>
  <artifactId>javaweb-01-maven</artifactId>
  <version>1.0-SNAPSHOT</version>
  <!--Package：项目的打包方式
  jar：java应用
  war：JavaWeb应用
  -->
  <packaging>war</packaging>


  <!--配置-->
  <properties>
    <!--项目的默认构建编码-->
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--编码版本-->
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>

  <!--项目依赖-->
  <dependencies>
    <!--具体依赖的jar包配置文件-->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
    </dependency>
  </dependencies>

  <!--项目构建用的东西-->
  <build>
    <finalName>javaweb-01-maven</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>

```

![1567847410771](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124143121.png)

### 解决资源导出失败问题

maven由于他的约定大于配置，我们之后可以能遇到我们写的配置文件，无法被导出或者生效的问题，解决方案：

```xml
<build>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
        </resources>
    </build>
```



![image-20210124143325676](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124143325.png)

## 5.11添加其他jar包依赖（以Spring为例）

**百度搜maven仓库**
![image-20210124150013493](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124150013.png)
**地址**：https://mvnrepository.com/

进去之后搜索spring，假如要导入 Spring Web MVC，如下图
![image-20210124145959266](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145959.png)
点击去，选择一个版本
![image-20210124145944864](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145944.png)
把图中的代码粘贴到porm.xml文件里即可
![image-20210124145933301](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145933.png)
粘贴进去，如图所示
![image-20210124145922211](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124145922.png)

## **5.12 IDEA操作**

![image-20210124143409929](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124143409.png)

![image-20210124143428906](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124143428.png)

**使用maven侧边栏clean删除target目录**

我们可以使用clean来清除target目录，双击clean，就可以发现，target目录没有了。

![image-20210124150439793](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124150439.png)

## **5.13 解决遇到的问题**

1. Maven 3.6.2

   解决方法：降级为3.6.1

2. Tomcat闪退

3. IDEA中每次都要重复配置Maven 在IDEA中的全局默认配置中去配置

![1567905247201](https://img-blog.csdnimg.cn/2020090716364848.png#pic_center)

![1567905291002](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124151333.png)

4.Maven项目中Tomcat无法配置

5.maven默认web项目中的web.xml版本问题

![1567905537026](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124151337.png)

6.替换为webapp4.0版本和tomcat一致

```java
<?xml version="1.0" encoding="UTF-8"?>

<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
  version="4.0"
  metadata-complete="true">


</web-app>

```



# 6、Servlet

## **6.1、Servlet简介**

Servlet就是sun公司开发动态web的一门技术
Sun在这些API中提供一个接口叫做：Servlet，如果你想开发一个Servlet程序，只需要完成两个小步骤：
编写一个类，实现Servlet接口
把开发好的Java类部署到web服务器中。
把实现了Servlet接口的Java程序叫做，Servlet

## **6.2、HelloServlet**

Serlvet接口Sun公司有两个默认的实现类：HttpServlet，GenericServlet

1. 构建一个普通的Maven项目，删掉里面的src目录，以后我们的学习就在这个项目里面建立Moudel；这个空的工程就是Maven主工程；

![image-20210124181616816](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124181616.png)

​	

```xml
<dependencies>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>4.0.1</version>

        </dependency>

        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>jsp-api</artifactId>
            <version>2.0</version>
        </dependency>
    </dependencies>
```



2.关于Maven父子工程的理解：

父项目中会有

```java
<modules>
    <module>servlet-01</module>
</modules>

```

子项目会有   (local history ---->accept)

```java
<parent>
    <artifactId>javaweb-02-servlet</artifactId>
    <groupId>com.kuang</groupId>
    <version>1.0-SNAPSHOT</version>
</parent>

```

父项目中的java子项目可以直接使用

`son extends father`
3.Maven环境优化

-  修改web.xml为最新的

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                             http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">

</web-app>
```



-  将maven的结构搭建完整

![image-20210124185202442](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124185202.png)

4.编写一个Servlet程序



> 编写一个普通类 HelloServlet
>
> 实现Servlet接口，这里我们直接继承HttpServlet

![image-20210124185325781](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124185325.png)

重写方法（ctrl+o 快捷键）

```java
package com.kuang.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/24 - 01 - 24 - 18:57
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class HelloServlet extends HttpServlet {

    //由于get或者post只是请求实现的不同的方式，可以相互调用，业务逻辑都一样；
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //ServletOutputStream outputStream = resp.getOutputStream();
        PrintWriter writer = resp.getWriter(); //响应流
        writer.print("Hello,Serlvet");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

5.编写Servlet的映射

为什么需要映射：我们写的是JAVA程序，但是要通过浏览器访问，而浏览器需要连接web服务器(**web.xml**)，所以我们需要再web服务中注册我们写的Servlet，还需给他一个浏览器能够访问的路径；

```java
<!--注册Servlet-->
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.ylw.servlet.HelloServlet</servlet-class>
    </servlet>
    <!--Servlet的请求路径，上面的name和下面的name要一样-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
```

6.配置Tomcat

```
注意：配置项目发布的路径就可以了
```

7.启动测试，OK！

![image-20210124190418905](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124190419.png)

## **6.3、Servlet原理**

Servlet是由Web服务器调用，web服务器在收到浏览器请求之后，会：

![image-20210124185434400](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124185434.png)

## **6.4、Mapping问题**

1. 一个Servlet可以指定一个映射路径

```xml
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
```

2.一个Servlet可以指定多个映射路径

```xml
   <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello2</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello3</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello4</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello5</url-pattern>
    </servlet-mapping>
```

3.一个Servlet可以指定通用映射路径

```xml
   <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello/*</url-pattern>
    </servlet-mapping>

```

4.默认请求路径

```xml
  <!--默认请求路径-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/*</url-pattern>
    </servlet-mapping>

```

5.指定一些后缀或者前缀等等….注意：这时候 * 前面就不要加路径了

```xml
<!--可以自定义后缀实现请求映射
    注意点，*前面不能加项目映射的路径
    hello/sajdlkajda.qinjiang
    -->
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>*.qinjiang</url-pattern>
</servlet-mapping>
```

6.优先级问题 指定了固有的映射路径优先级最高，如果找不到就会走默认的(/*)处理请求；

```xml
<!--404-->
<servlet>
    <servlet-name>error</servlet-name>
    <servlet-class>com.kuang.servlet.ErrorServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>error</servlet-name>
    <url-pattern>/*</url-pattern>
</servlet-mapping>
```

![image-20210124192107134](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124192107.png)

![image-20210124192052844](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124192052.png)

7.携带参数

```xml
 <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.ylw.servlet.HelloServlet</servlet-class>
        <!--可以携带参数，不怎么用-->
<!--        <init-param>-->
<!--            <param-name></param-name>-->
<!--            <param-value></param-value>-->
<!--        </init-param>-->
    </servlet>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
```

## 6.5  **ServletContext 常用方法**

web容器在启动的时候，它会为每个web程序都创建一个对应的`ServletContext对象`，它代表了当前的web应用；
主要方法：

```java
ServletContext context = this.getServletContext();
```

注意下面的这些之后会被别的方法替换掉，不怎么用！

### 1、共享数据

用到的主要方法：

```java
//设置
context.setAttribute("参数名",参数值（可以是变量名）);
//获取
context.getAttribute("参数名");
```

在这个Servlet中保存的数据，可以在另外一个servlet中拿到；
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124200101.png)
在HelloServlet 里设置上下文数据

```java
package com.kuang.servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/24 - 01 - 24 - 19:54
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class HelloServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //this.getInitParameter() 初始化参数
        //this.getServletConfig() Servlet配置
        //this.getServletContext() Servlet上下文
        ServletContext context = this.getServletContext();

        String username = "武新宇"; //数据
        context.setAttribute("username",username); //将一个数据保存在了ServletContext，数据的名字为username，值为变量username的值

        System.out.println("Hello,进入doGet");
    }
}

```

在GetServlet 里获取上下文

```java
package com.kuang.servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/24 - 01 - 24 - 20:06
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class GetServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext(); //这里获取的上下文就是HellServlet里设置的

        String username = (String) context.getAttribute("username"); //获取上下文中名为username的值

        resp.setContentType("text/html"); //设置文本类型
        resp.setCharacterEncoding("utf-8"); //设置编码
        resp.getWriter().print("用户名："+username); //写在网页上
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp); //注意这里改成doGet(req, resp)，形成一个规范
    }
}

```

web.xml里的注册

```xml
 <servlet>
    <servlet-name>hello</servlet-name>
    <servlet-class>com.kuang.servlet.HelloServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello</url-pattern>
  </servlet-mapping>

  <servlet>
    <servlet-name>getContext</servlet-name>
    <servlet-class>com.kuang.servlet.GetServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>getContext</servlet-name>
    <url-pattern>/getContext</url-pattern>
  </servlet-mapping>

```

重启Tomcat。
然后打开浏览器，先访问/hello进行设置，再访问/getContext进行获取
![image-20210124200936267](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124200936.png)

![image-20210124200925027](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124200925.png)

### 2、获取初始化参数

用到的主要方法：

```java
context.getInitParameter("参数名");
```

现在web.xml文件里配置初始参数

```bash
    <!--配置一些web应用的初始化参数-->
    <context-param>
        <param-name>url</param-name>
        <param-value>jdbc:mysql://localhost:3306/mybatis</param-value>
    </context-param>
```

写一个类获取

```java
package com.kuang.servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/24 - 01 - 24 - 23:21
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class ServletDemo03 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext(); //这里获取的上下文就是HellServlet里设置的

        String url = context.getInitParameter("url"); //获取上web.xml文件中设置的参数<context-param>

        resp.getWriter().print(url); //写在网页上
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);//注意这里改成doGet(req, resp)，形成一个规范
    }
}


```

在web.xml里注册这个类

```bash
<servlet>
    <servlet-name>gp</servlet-name>
    <servlet-class>com.kuang.servlet.ServletDemo03</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>gp</servlet-name>
    <url-pattern>/gp</url-pattern>
  </servlet-mapping>
```

重启Tomcat。
然后打开浏览器，访问/gp进行获取
![image-20210124232352690](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210124232352.png)

### 3、请求转发

A要访问C中的资源：有两种方式

![image-20210125001115628](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210125001115.png)

用到的主要方法：

```java
context.getRequestDispatcher("转发路径").forward(req,resp);
```

转发代码

```java
package com.kuang.servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/25 - 01 - 25 - 0:12
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class ServletDemo04 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext(); //这里获取的上下文就是HellServlet里设置的
        System.out.println("进入了Demo04");
//        RequestDispatcher requestDispatcher = context.getRequestDispatcher("/gp"); //设置转发路径
//        requestDispatcher.forward(req,resp); //调用forward实现请求转发
        //合并上面两句
        context.getRequestDispatcher("/gp").forward(req,resp);

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);//注意这里改成doGet(req, resp)，形成一个规范
    }
}

```

在web.xml里注册类

```xml
    <servlet>
        <servlet-name>sd4</servlet-name>
        <servlet-class>com.ylw.servlet.ServletDemo04</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>sd4</servlet-name>
        <url-pattern>/sd4</url-pattern>
    </servlet-mapping>

```

重启Tomcat，
打开浏览器，进入/sd4，发现路径没有变，但是显示的是/gp的页面，这就是转发的作用（重定向才会改变路径）
![image-20210125001442817](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210125001442.png)
由于我们设置了输出语句，在控制台里可以看到，确实进入了demo04，只不过显示的是转发页面
![image-20210125001453657](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210125001453.png)

### 4、读取资源文件 getResourceAsStream()

用到的主要方法：

```java
//获取文件，变成流
this.getServletContext().getResourceAsStream("文件路径"）
//加载流
Properties prop = new Properties();
prop.load(inputStream); //加载上面文件转化成的流
prop.getProperty("属性名"); //获取文件中的一个属性

```

Properties

比较分析：

- 在java目录下新建properties
- 在resources目录下新建properties

发现：都被打包到了同一个路径下：classes，我们俗称这个路径为classpath:

![image-20210125001958291](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210125001958.png)

在java目录下的properties，发现导出的target中没有该文件，就需要在porm.xml中添加配置，详见博客https://blog.csdn.net/qq_43594119/article/details/106199248中的**解决资源导出失败问题**

读取资源文件：
1在resources目录下新建一个db.properties文件作为资源文件
![image-20210125001727604](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210125001727.png)

```properties
username=wuxinyu
password=123456
```

2.写一个类用来读取这个资源文件，下面是截图和代码
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200521202347385.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNTk0MTE5,size_16,color_FFFFFF,t_70)

```java
package com.kuang.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.InputStream;
import java.util.Properties;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/25 - 01 - 25 - 0:18
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class PropertiesServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //获得资源，变成一个流  路径是target下面的路径
        InputStream inputStream = this.getServletContext().getResourceAsStream("/WEB-INF/classes/db.properties");

        Properties prop = new Properties();
        prop.load(inputStream); //加载上面文件转化成的流
        String user = prop.getProperty("username"); //获取文件中的一个属性
        String pwd = prop.getProperty("password"); //获取文件中的一个属性

        //在网页上显示出来
        resp.getWriter().print("user: " + user +'\n' + "pwd: " + pwd);

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp); //注意这里改成doGet(req, resp)，形成一个规范
    }
}


```

注意这里的路径是 `/WEB-INF/classes/db.properties` 第一个 / 代表当前项目
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210125001931.png)
3.在web.xml中注册该类

```bash
    <servlet>
        <servlet-name>sd5</servlet-name>
        <servlet-class>com.ylw.servlet.ServletDemo05</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>sd5</servlet-name>
        <url-pattern>/sd5</url-pattern>
    </servlet-mapping>
```

4.重启tomcat，访问/sd5
![image-20210125002355108](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210125002355.png)

## 6.6、HttpServletResponse

web服务器接收到客户端的http请求，针对这个请求，分别创建一个代表请求的HttpServletRequest对象，代表响应的一个HttpServletResponse；



- 如果要获取客户端请求过来的参数：找HttpServletRequest
- 如果要给客户端响应一些信息：找HttpServletResponse

### 1、简单分类

负责向浏览器发送数据的方法

```java
 servletOutputstream getOutputstream() throws IOException;
 Printwriter getwriter() throws IOException;
```

负责向浏览器发送响应头的方法

```java
void setCharacterEncoding(String var1)；
void setContentLength(int var1)；
void setContentLengthLong(long var1);
void setContentType(String var1)；
void setDateHeader(String varl,long var2)
void addDateHeader(String var1,long var2)
void setHeader(String var1,String var2);
void addHeader(String var1,String var2)；
void setIntHeader(String var1,int var2);
void addIntHeader(String varl,int var2);
```

响应的状态码
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210125172019.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200505155821202.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70)

### 2、下载文件

1. 向浏览器输出消息（一直在讲，就不说了）
2. 下载文件
   1. 要获取下载文件的路径
   2. 下载的文件名是啥？
   3. 设置想办法让浏览器能够支持下载我们需要的东西
   4. 获取下载文件的输入流
   5. 创建缓冲区
   6. 获取OutputStream对象
   7. 将FileOutputStream流写入到bufer缓冲区
   8. 使用OutputStream将缓冲区中的数据输出到客户端！

```java
package com.kuang.servlet;

import javax.servlet.ServletException;
import javax.servlet.ServletOutputStream;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.FileInputStream;
import java.io.IOException;
import java.net.URLEncoder;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/25 - 01 - 25 - 17:25
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class FileServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
//        1. 要获取下载文件的路径
        String realPath = "D:\\WorkingSpace\\Idea_workingspace\\JavaWeb\\javaweb-02-servlet\\response\\src\\main\\resources\\1.png";
        System.out.println("下载文件的路径为："+realPath);
//        2. 下载的文件名是啥？
        String fileName = realPath.substring(realPath.lastIndexOf("\\") + 1);
//        3. 设置想办法让浏览器能够支持下载我们需要的东西
        System.out.println(fileName);
        resp.setHeader("Content-Disposition","attachment;filename="+ URLEncoder.encode(fileName,"UTF-8"));
//        4. 获取下载文件的输入流
        FileInputStream fileInputStream =new FileInputStream(realPath);
//        5. 创建缓冲区
        int len = 0;
        byte[] buffer = new byte[1024];
//        6. 获取OutputStream对象
        ServletOutputStream out = resp.getOutputStream();
//        7. 将FileOutputStream流写入到bufer缓冲区
        while((len=fileInputStream.read(buffer))!=-1){
            out.write(buffer,0,len);
        }
        fileInputStream.close();
        out.close();
//        8. 使用OutputStream将缓冲区中的数据输出到客户端！
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```

```xml
<servlet>
      <servlet-name>FileServlet</servlet-name>
      <servlet-class>com.kuang.servlet.FileServlet</servlet-class>
    </servlet>
  <servlet-mapping>
    <servlet-name>FileServlet</servlet-name>
    <url-pattern>/fs</url-pattern>
  </servlet-mapping>
```



![image-20210125181922095](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210125181929.png)

### 3、验证码功能

验证怎么来的?

- 前端实现
- 后端实现，需要用到Java的图片类，生产一个图片

```java
package com.kuang.servlet;

import javax.imageio.ImageIO;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.io.IOException;
import java.util.Random;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/25 - 01 - 25 - 18:25
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class ImageServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //如何让浏览器3秒自动刷新一次;
        resp.setHeader("refresh","3");
        //在内存中创建一个图片
        BufferedImage image = new BufferedImage(80,20,BufferedImage.TYPE_INT_RGB);
        //得到图片
        Graphics2D g= (Graphics2D) image.getGraphics();
        //设置图片的背景颜色
        g.setColor(Color.white);
        g.fillRect(0,0,80,20);
        //
        g.setColor(Color.BLUE);
        g.setFont(new Font("宋体", Font.BOLD,20));
        g.drawString(makeNum(),0,20);
        //告诉浏览器，这个请求用图片的方式打开
        resp.setContentType("image/jpg");
        //网站存在缓存，不让浏览器缓存
        resp.setDateHeader("expires",-1);
        resp.setHeader("Cache-Control","no-cache");
        resp.setHeader("Pragma","no-cache");
        //把图片写给浏览器
        ImageIO.write(image,"jpg", resp.getOutputStream());

    }
    //生成随机数
    private String makeNum(){
        Random random = new Random();
        String num = random.nextInt(9999999)+"";
        StringBuffer sb = new StringBuffer();
        for (int i = 0; i < 7-num.length(); i++) {
            sb.append("0");
        }
        num = sb.toString()+num;
        return num;
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```



```xml
<servlet>
        <servlet-name>imageServlet</servlet-name>
        <servlet-class>com.kuang.servlet.ImageServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>imageServlet</servlet-name>
        <url-pattern>/img</url-pattern>
    </servlet-mapping>
```



![image-20210125190006984](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210125190007.png)

### 4、实现重定向

![image-20210125190322378](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210125190322.png)

常见场景:

- 用户登录

```java
 void sendRedirect(String var1) throws IOException;
```

测试：

```java
package com.kuang.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/25 - 01 - 25 - 19:05
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class RedirectServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.sendRedirect("/img");//重定向
    /*
    resp. setHeader("Location","/r/img");
    resp. setstatus (302);
    */
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```



```xml
    <servlet>
        <servlet-name>RedirectServlet</servlet-name>
        <servlet-class>com.kuang.servlet.RedirectServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>RedirectServlet</servlet-name>
        <url-pattern>/reditect</url-pattern>
    </servlet-mapping>
```

面试题：请你聊聊重定向和转发的区别？

**forward（转发）**：307

是服务器请求资源,服务器直接访问目标地址的URL,把那个URL的响应内容读取过来,然后把这些内容再发给浏览器.浏览器根本不知道服务器发送的内容从哪里来的,因为这个跳转过程实在服务器实现的，并不是在客户端实现的所以客户端并不知道这个跳转动作，所以它的地址栏还是原来的地址.

**redirect（重定向）**：302

是服务端根据逻辑,发送一个状态码,告诉浏览器重新去请求那个地址.所以地址栏显示的是新的URL.

**转发是服务器行为，重定向是客户端行为。**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200505163946136.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200505163953854.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbGxfbG92ZQ==,size_16,color_FFFFFF,t_70)
**index.jsp**

```jsp
<html>
<body>
<h2>Hel1o World!</h2>
《%--这里超交的路径,需要寻找到项目的路径--%>
<%--${pageContext. request, contextPath}代表当前的项目--%>
<form action="${pageContext. request.contextPath}/login" method="get">
    用户名: <input type="text" name="username"> <br>
    密码: <input type="password" name="password"> <br>
    <input type="submit">
</form>

</body>
</html>
```

**RequestTest.java**

```java
package com.kuang.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/25 - 01 - 25 - 19:19
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class RequestTest extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //处理方求
        String username = req.getParameter( "username");
        String password =req.getParameter( "password");

        System.out.println(username+":"+password);

        resp.sendRedirect("/success.jsp");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```

**重定向页面success.jsp**

```html
<%@ page contentType="text/html; charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>success</h1>
</body>
</html>

```

**web.xml配置**

```xml
 <servlet>
        <servlet-name>requset</servlet-name>
        <servlet-class>com.kuang.servlet.RequestTest</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>requset</servlet-name>
        <url-pattern>/login</url-pattern>
    </servlet-mapping>
```

**导入依赖的jar包**

```xml
    <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
    </dependency>
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>4.0.1</version>
    </dependency>
    <dependency>
      <groupId>javax.servlet.jsp</groupId>
      <artifactId>javax.servlet.jsp-api</artifactId>
      <version>2.3.3</version>
    </dependency>

  </dependencies>
```

## 6.7、HttpServletRequest

HttpServletRequest代表客户端的请求,用户通过Http协议访问服务器, HTTP请求中的所有信息会被封装到HttpServletRequest,通过这个HttpServletRequest的方法,获得客户端的所有信息;
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210125193357.png)
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210125193405.png)

### 获取前端传递的参数、请求转发

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200505165652729.png)
**自己创建类，且需要继承HttpServlet类**

```java
package com.kuang.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.Arrays;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/25 - 01 - 25 - 19:49
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class LoginServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doGet(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
      	req.setCharacterEncoding("utf-8");
      resp.setCharacterEncoding("utf-8");
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        String[] hobbys = req.getParameterValues("hobbys");
        System.out.println("==========");
        //后台接收中文乱码问题
        System. out.println(username);
        System. out.println(password);
        System. out.println(Arrays.toString(hobbys));
        System. out.println("============");
        System. out.println(req.getContextPath());
        
        //通过请求转发
        //这里的/代表当前的web应用
        req.getRequestDispatcher("/success.jsp").forward(req,resp);
    }
}

```



```html
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/25
  Time: 19:52
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>登录</title>
</head>
<body>
<div style="text-align: center">
    <form action="${pageContext.request.contextPath}/login" method="post">
        用户名：<input type="text" name="username"><br>
        密码：<input type="password" name="password"><br>
        爱好：
        <input type="checkbox" name="hobbys" value="女孩">女孩
        <input type="checkbox" name="hobbys" value="代码">代码
        <input type="checkbox" name="hobbys" value="唱歌">唱歌
        <input type="checkbox" name="hobbys" value="电影">电影
        <br>

        <input type="submit">
    </form>

</div>
</body>
</html>

```



```html
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/25
  Time: 20:06
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>success</h1>
</body>
</html>

```



```xml
<servlet>
      <servlet-name>LoginServlet</servlet-name>
      <servlet-class>com.kuang.servlet.LoginServlet</servlet-class>
    </servlet>
  <servlet-mapping>
    <servlet-name>LoginServlet</servlet-name>
    <url-pattern>/login</url-pattern>
  </servlet-mapping>
```



# 7、Cookie、Session

## 7.1、会话

**会话**：用户打开一个浏览器，点击了很多超链接，访问多个web资源，关闭浏览器，这个过程可以称之为会话；

**有状态会话**：一个同学来过教室，下次再来教室，我们会知道这个同学，曾经来过，称之为**有状态会话**；

**你能怎么证明你是西开的学生？**

你-------------------------------------西开

1. 发票                      西开给你发票
2. 学校登记              西开标记你来过了

**一个网站，怎么证明你来过？**

客户端-------------------------------服务端

1. 服务端给客户端一个 信件，客户端下次访问服务端带上信件就可以了； **cookie**
2. 服务器登记你来过了，下次你来的时候我来匹配你； **seesion**

## 7.2、保存会话的两种技术

**cookie**

- 客户端技术 （响应，请求）

**session**

- 服务器技术，利用这个技术，可以保存用户的会话信息？ 我们可以把信息或者数据放在Session中！

常见常见：网站登录之后，你下次不用再登录了，第二次访问直接就上去了！

### Cookie获取上次访问浏览器的时间

```java
package com.kuang.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.xml.crypto.Data;
import java.io.IOException;
import java.io.PrintWriter;
import java.io.Writer;
import java.util.Date;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/25 - 01 - 25 - 20:42
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class CookieDemo01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //服务器给客户端发一个cookie 告你你来的时间，封装成一个信件，你下次来带来，我就知道你来了

        //解决中文乱码
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html;charset=utf-8");
        
        // 获取输出对象
        Writer out = resp.getWriter();
        out.write("上次访问时间: ");

        // 获取访问时间cookie
        Cookie[] cookies = req.getCookies();
        for (int i = 0; cookies != null && i < cookies.length; i++) {

            Cookie cookie = cookies[i];
            if (cookie.getName().equals("lastAccess")) {
                String value = cookie.getValue();
                Date date = new Date(Long.parseLong(value));

                out.write(date.toString());
            }
        }

// 设置最新的访问时间cookie
        Cookie cookie = new Cookie("lastAccess", System.currentTimeMillis() + "");
        // 设置cookie有效时间 单位：秒
        cookie.setMaxAge(3600);
        // 设置cookie有效路径
        cookie.setPath(req.getContextPath());
        //System.out.println(request.getContextPath());
        //System.out.println(this.getServletContext().getContextPath());
        resp.addCookie(cookie);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```

```xml
<servlet>
      <servlet-name>CookieDemo01</servlet-name>
      <servlet-class>com.kuang.servlet.CookieDemo01</servlet-class>
    </servlet>
  <servlet-mapping>
    <servlet-name>CookieDemo01</servlet-name>
    <url-pattern>/c1</url-pattern>
  </servlet-mapping>
```

![image-20210125211112759](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210125211112.png)



## 7.3、Cookie

![image-20210126111418829](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126111418.png)

1. 从请求中拿到cookie信息
2. 服务器响应给客户端cookie

```java
Cookie[] cookies = req.getCookies(); //获得Cookie
cookie.getName(); //获得cookie中的key
cookie.getValue(); //获得cookie中的vlaue
new Cookie("lastLoginTime", System.currentTimeMillis()+""); //新建一个cookie
cookie.setMaxAge(24*60*60); //设置cookie的有效期
resp.addCookie(cookie); //服务器响应给客户端一个cookie
```

**cookie：一般会保存在本地的 用户目录下 appdata；**

![image-20210125211236088](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210125211236.png)

一个网站cookie是否存在上限！**聊聊细节问题**

- 一个Cookie只能保存**一个信息**；
- 一个web站点可以给浏览器发送**多个cookie**，**最多存放20个cookie**；
- Cookie**大小有限制4kb**；
- **300个cookie浏览器上限**

### **删除Cookie；**

- 不设置有效期，关闭浏览器，自动失效；
- 设置有效期时间为 0 ；

```java
package com.kuang.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/25 - 01 - 25 - 21:14
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class CookieDemo02 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //删除一个Cookie
        //创建一个Cookie 必须和要删除的cookie一样

        Cookie cookie = new Cookie("lastAccess",System.currentTimeMillis()+"");

        //将Cookie有效期设置为0，就失效了
        cookie.setMaxAge(0);

        resp.addCookie(cookie);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```



```xml
<servlet>
        <servlet-name>CookieDemo02</servlet-name>
        <servlet-class>com.kuang.servlet.CookieDemo02</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>CookieDemo02</servlet-name>
        <url-pattern>/c2</url-pattern>
    </servlet-mapping>
```



![image-20210125211836545](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210125211836.png)

### **编码解码：**

```java
URLEncoder.encode("秦疆","utf-8")//编码
URLDecoder.decode(cookie.getValue(),"UTF-8")//解码
```

```java
package com.kuang.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.Writer;
import java.net.URLDecoder;
import java.net.URLEncoder;
import java.util.Date;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/25 - 01 - 25 - 21:19
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class CookieDemo03 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");

        // 获取输出对象
        Writer out = resp.getWriter();
        out.write("上次访问用户: ");

        // 获取访问时间cookie
        Cookie[] cookies = req.getCookies();
        for (int i = 0; cookies != null && i < cookies.length; i++) {

            Cookie cookie = cookies[i];
            if (cookie.getName().equals("name")) {
                String value = cookie.getValue();
                //解码
                out.write( URLDecoder.decode(cookie.getValue(),"utf-8"));


            }

        }
        //编码
        Cookie cookie = new Cookie("name", URLEncoder.encode("武新宇","utf-8"));
        resp.addCookie(cookie);

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```



## 7.4、Session（重点）

![image-20210126111619517](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126111619.png)
什么是Session：

- 服务器会给每一个用户（浏览器）创建一个Seesion对象；
- 一个Seesion独占一个浏览器，只要浏览器没有关闭，这个Session就存在；
- 用户登录之后，整个网站它都可以访问！–------> 保存用户的信息；保存购物车的信息……
- ![image-20210126105207193](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126105214.png)

…
…
…

Session和cookie的区别：

- Cookie是把用户的数据写给用户的浏览器，浏览器保存 （可以保存多个）
- Session把用户的数据写到用户独占Session中，服务器端保存 （保存重要的信息，减少服务器资源的浪费）
- Session对象由服务创建；

使用场景：

- 保存一个登录用户的信息；
- 购物车信息；
- 在整个网站中经常会使用的数据，我们将它保存在Session中；

使用Session：

### 一、

```java
package com.kuang.servlet;

import com.kuang.pojo.Person;

import javax.servlet.ServletException;
import javax.servlet.http.*;
import java.io.IOException;

public class SessionDemo01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        
        //解决乱码问题
        req.setCharacterEncoding("UTF-8");
        resp.setCharacterEncoding("UTF-8");
        resp.setContentType("text/html;charset=utf-8");
        
        //得到Session
        HttpSession session = req.getSession();
        //给Session中存东西
        session.setAttribute("name",new Person("秦疆",1));
        //获取Session的ID
        String sessionId = session.getId();

        //判断Session是不是新创建
        if (session.isNew()){
            resp.getWriter().write("session创建成功,ID:"+sessionId);
        }else {
            resp.getWriter().write("session以及在服务器中存在了,ID:"+sessionId);
        }

        //Session创建的时候做了什么事情；
//        Cookie cookie = new Cookie("JSESSIONID",sessionId);
//        resp.addCookie(cookie);

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

![image-20210126105518076](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126105518.png)

### 二、

```java
package com.kuang.pojo;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/26 - 01 - 26 - 10:57
 * @Description: com.kuang.pojo
 * @version: 1.0
 */
public class Person {
    private String name;
    private int age ;    //

    public Person() {
    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}

```

```java
package com.kuang.servlet;

import com.kuang.pojo.Person;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/26 - 01 - 26 - 11:00
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class SessionDemo02 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //解决乱码问题
        req.setCharacterEncoding("UTF-8");
        resp.setCharacterEncoding("UTF-8");
        resp.setContentType("text/html;charset=utf-8");

        //得到Session
        HttpSession session = req.getSession();

        Person person = (Person) session.getAttribute("name");

        System.out.println(person.toString());

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```

![image-20210126110336166](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126110336.png)

```xml
<servlet>
        <servlet-name>SessionDemo01</servlet-name>
        <servlet-class>com.kuang.servlet.SessionDemo01</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>SessionDemo01</servlet-name>
        <url-pattern>/s1</url-pattern>
    </servlet-mapping>

    <servlet>
        <servlet-name>SessionDemo02</servlet-name>
        <servlet-class>com.kuang.servlet.SessionDemo02</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>SessionDemo02</servlet-name>
        <url-pattern>/s2</url-pattern>
    </servlet-mapping>
```



### **会话自动过期：web.xml配置**

package com.kuang.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/26 - 01 - 26 - 11:08
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class SessionDemo03 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //解决乱码问题
        req.setCharacterEncoding("UTF-8");
        resp.setCharacterEncoding("UTF-8");
        resp.setContentType("text/html;charset=utf-8");

    ​    //得到Session
    ​    HttpSession session = req.getSession();
       session.removeAttribute("name");
	​			//删除session
    ​    session.invalidate();
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```xml
<!--设置Session默认的失效时间-->
<session-config>
    <!--15分钟后Session自动失效，以分钟为单位-->
    <session-timeout>15</session-timeout>
</session-config>

```

若有多个用户共有的数据时：

![image-20210126111713695](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126111713.png)

# 8、JSP

## 8.1、什么是JSP

Java Server Pages ： Java服务器端页面，也和Servlet一样，用于动态Web技术！

最大的特点：

- 写JSP就像在写HTML
- 区别：
  - HTML只给用户提供静态的数据
  - JSP页面中可以嵌入JAVA代码，为用户提供动态数据；

## 8.2、JSP原理

思路：JSP到底怎么执行的！

- 代码层面没有任何问题

- 服务器内部工作

  tomcat中有一个work目录；

  IDEA中使用Tomcat的会在IDEA的tomcat中生产一个work目录

  ![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126111950.png)

  ![image-20210126112133357](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126112133.png)

  我电脑的地址：

  **C:\Users\Administrator\AppData\Local\JetBrains\IntelliJIdea2020.3\tomcat\4c2427d8-18f1-41a5-9c10-3480b51c0536\work\Catalina\localhost\javaweb_01_maven01_war\org\apache\jsp**
  
  发现页面转变成了Java程序！
  ![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126112152.png)

**浏览器向服务器发送请求，不管访问什么资源，其实都是在访问Servlet！**

JSP最终也会被转换成为一个Java类！

**JSP 本质上就是一个Servlet**   帮助简化了Servlet的使用

```java
//初始化
  public void _jspInit() {
      
  }
//销毁
  public void _jspDestroy() {
  }
//JSPService
  public void _jspService(.HttpServletRequest request,HttpServletResponse response)
```

1. 判断请求

2. 内置一些对象

   ```java
   final javax.servlet.jsp.PageContext.pageContext;  //页面上下文
   javax.servlet.http.HttpSession session = null;    //session
   final javax.servlet.ServletContext application;   //applicationContext
   final javax.servlet.ServletConfig config;         //config
   javax.servlet.jsp.JspWriter out = null;           //out
   final java.lang.Object page = this;               //page：当前
   HttpServletRequest request                        //请求
   HttpServletResponse response                      //响应
   ```
   
3. 输出页面前增加的代码

   ```java
   response.setContentType("text/html");       //设置响应的页面类型
   pageContext = _jspxFactory.getPageContext(this, request, response,
          null, true, 8192, true);
   _jspx_page_context = pageContext;
   application = pageContext.getServletContext();
   config = pageContext.getServletConfig();
   session = pageContext.getSession();
   out = pageContext.getOut();
   _jspx_out = out;
   ```
   
4. 以上的这些个对象我们可以在JSP页面中直接使用！

![image-20210126112949285](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126112949.png)

在JSP页面中；

只要是 JAVA代码就会原封不动的输出；

![image-20210126113206794](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126113206.png)

![image-20210126113222123](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126113222.png)

如果是HTML代码，就会被转换为：

```java
out.write("<html>\r\n");
```

这样的格式，输出到前端！

## 8.3、JSP基础语法

任何语言都有自己的语法，JAVA中有,。 JSP 作为java技术的一种应用，它拥有一些**自己扩充的语法**（了解，知道即可！），Java所有语法都支持！

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>javaweb-04-jsp</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.11</version>
        </dependency>
<!--        Servlet依赖-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>4.0.1</version>
        </dependency>
<!--        JSP依赖-->
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>javax.servlet.jsp-api</artifactId>
            <version>2.3.3</version>
        </dependency>
<!--JSTL表达式依赖-->
        <dependency>
            <groupId>javax.servlet.jsp.jstl</groupId>
            <artifactId>jstl-api</artifactId>
            <version>1.2</version>
        </dependency>
<!--standard标签库-->
        <dependency>
            <groupId>taglibs</groupId>
            <artifactId>standard</artifactId>
            <version>1.1.2</version>
        </dependency>
    </dependencies>


    <build>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
        </resources>
    </build>
</project>
```



#### JSP表达式

```jsp
  <%--JSP表达式
  作用：用来将程序的输出，输出到客户端
  <%= 变量或者表达式%>
  --%>
  <%= new java.util.Date()%>
```

![image-20210126114447625](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126114447.png)

#### JSP脚本片段

```jsp
  <%--jsp脚本片段--%>
  <%
    int sum = 0;
    for (int i = 1; i <=100 ; i++) {
      sum+=i;
    }
    out.println("<h1>Sum="+sum+"</h1>");
  %>
```

![image-20210126114622588](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126114622.png)

#### **JSP脚本片段的再实现**

```jsp
  <%
    int x = 10;
    out.println(x);
  %>
  <p>这是一个JSP文档</p>
  <%
    int y = 2;
    out.println(y);
  %>

  <hr>

```

![image-20210126114902080](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126114902.png)



```jsp

  <%--在代码嵌入HTML元素--%>
  <%
    for (int i = 0; i < 5; i++) {
  %>
    <h1>Hello,World  <%=i%> </h1>
  <%
    }
  %>
```

![image-20210126114958474](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126114958.png)

**上面的会被生成到`jspService()`方法中！**

#### JSP声明

```java
  <%!
    static {
      System.out.println("Loading Servlet!");
    }

    private int globalVar = 0;

    public void kuang(){
      System.out.println("进入了方法Kuang！");
    }
  %>

```

JSP声明：会被编译到JSP生成`Java的类`中！其他的，就会被生成到`jspService()`方法中！

在JSP，嵌入Java代码即可！

```java
<%%>
<%=%>
<%!%>

<%--注释--%>
```

JSP的注释，不会在客户端显示（查看源码！），HTML就会！

## 8.4、JSP指令

### 自定制404、500页面

![image-20210126121041222](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126121041.png)

```jsp
<%@ page errorPage="errorpage/500.jsp"%>
<%@ page errorPage="errorpage/404.jsp"%>
```



```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/26
  Time: 12:03
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ page errorPage="errorpage/500.jsp"%>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <%
        int i = 1/0;
    %>
</body>
</html>

```

![image-20210126121000149](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126121000.png)



```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                             http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">

        <error-page>
            <error-code>404</error-code>
            <location>/errorpage/404.jsp</location>
        </error-page>
</web-app>
```

![](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126121525.png)

### 页面头部尾部共同构成

```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/26
  Time: 12:17
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
  
<%--@include会将两个页面合二为一--%>
<%@include file="common/header.jsp"%>
    你猜猜我是主页
<%@include file="common/footer.jsp"%>
  
  <%--jSP标签
    jsp:include：拼接页面，本质还是三个
    --%>
<jsp:include page="/common/header.jsp"/>
<h1>网页主体</h1>
<jsp:include page="/common/footer.jsp"/>
  
</body>
</html>

```



![image-20210126121925498](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126121925.png)



## 8.5、9大内置对象

- PageContext 存东西
- Request 存东西
- Response
- Session 存东西
- Application 【SerlvetContext】 存东西
- config 【SerlvetConfig】
- out
- page ，不用了解
- exception

### 数据存取

```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/26
  Time: 12:26
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <%
        pageContext.setAttribute("name1","秦疆1号"); //保存的数据只在一个页面中有效
        request.setAttribute("name2","秦疆2号"); //保存的数据只在一次请求中有效，请求转发会携带这个数据
        session.setAttribute("name3","秦疆3号"); //保存的数据只在一次会话中有效，从打开浏览器到关闭浏览器
        application.setAttribute("name4","秦疆4号");  //保存的数据只在服务器中有效，从打开服务器到关闭服务器
    %>

<%--    脚本代码中的代码，会被项目原封不动的生成到jsp.java
要求java代码必须写正确！
--%>

<%
    String name1 = (String) pageContext.findAttribute("name1");
    String name2 = (String) pageContext.findAttribute("name2");
    String name3 = (String) pageContext.findAttribute("name3");
    String name4 = (String) pageContext.findAttribute("name4");
    String name5 = (String) pageContext.findAttribute("name5");
%>

<%--使用输出 --%>
<h1>取出的值为：</h1>
<h1>${name1}</h1>
<h1>${name2}</h1>
<h1>${name3}</h1>
<h1>${name4}</h1>
<h1><%= name5%></h1>

</body>
</html>

```

![image-20210126123136297](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126123136.png)

### 请求转发

```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/26
  Time: 12:41
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>

    <%
        pageContext.forward("/index.jsp");
        request.getRequestDispatcher("/index.jsp").forward(request,response);
    %>
</body>
</html>

```





![image-20210126123732111](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126123732.png)

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126155513.png)

request：客户端向服务器发送请求，产生的数据，用户看完就没用了，比如：新闻，用户看完没用的！

session：客户端向服务器发送请求，产生的数据，用户用完一会还有用，比如：购物车；

application：客户端向服务器发送请求，产生的数据，一个用户用完了，其他用户还可能使用，比如：聊天数据；

## 8.6、JSP标签、JSTL标签、EL表达式

```xml
<!-- JSTL表达式的依赖 -->
<dependency>
    <groupId>javax.servlet.jsp.jstl</groupId>
    <artifactId>jstl-api</artifactId>
    <version>1.2</version>
</dependency>
<!-- standard标签库 -->
<dependency>
    <groupId>taglibs</groupId>
    <artifactId>standard</artifactId>
    <version>1.1.2</version>
</dependency>

```

EL表达式： `${ }`

- **获取数据**
- **执行运算**
- **获取web开发的常用对象**

**JSP标签**

```java
<%--jsp:include--%>

<%--
http://localhost:8080/jsptag.jsp?name=kuangshen&age=12
--%>
  
<%--设置参数--%>
<jsp:forward page="/jsptag2.jsp">
    <jsp:param name="name" value="kuangshen"></jsp:param>
    <jsp:param name="age" value="12"></jsp:param>
</jsp:forward>
  
  <%--取出参数--%>
名字：<%=request.getParameter("name")%>
年龄：<%=request.getParameter("age")%>
```

![image-20210126161202335](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126161202.png)

**JSTL表达式**

**JSTL标签库的使用就是为了弥补HTML标签的不足**；它自定义许多标签，可以供我们使用，标签的功能和Java代码一样！

**格式化标签**

**SQL标签**

**XML 标签**

**核心标签** （掌握部分）

```jsp
<%--引入JSTL核心标签库，我们才能使用JSTL标签--%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```



![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126161323.png)

**JSTL标签库使用步骤**

- 引入对应的 taglib
- 使用其中的方法
- **在Tomcat 也需要引入 jstl的包，否则会报错：JSTL解析错误**
- ![image-20210126172242975](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126172243.png)
- ![image-20210126165028006](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126165028.png)

**c：if**

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h4>if测试</h4>

<hr>

<form action="coreif.jsp" method="get">
    <%--
    EL表达式获取表单中的数据
    ${param.参数名}
    --%>
    <input type="text" name="username" value="${param.username}">
    <input type="submit" value="登录">
</form>

<%--判断如果提交的用户名是管理员，则登录成功--%>
<c:if test="${param.username=='admin'}" var="isAdmin">
    <c:out value="管理员欢迎您！"/>
</c:if>

<%--自闭合标签--%>
<c:out value="${isAdmin}"/>
</body>
</html>
```

**c:choose      c:when**

```java
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>
<head>
    <title>Title</title>
</head>
<body>

<%--定义一个变量score，值为85--%>
<c:set var="score" value="55"/>

<c:choose>
    <c:when test="${score>=90}">
        你的成绩为优秀
    </c:when>
    <c:when test="${score>=80}">
        你的成绩为一般
    </c:when>
    <c:when test="${score>=70}">
        你的成绩为良好
    </c:when>
    <c:when test="${score<=60}">
        你的成绩为不及格
    </c:when>
</c:choose>
</body>
</html>
```

**c:forEach**

```jsp

<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>
<head>
    <title>Title</title>
</head>
<body>

<%
    ArrayList<String> people = new ArrayList<>();
    people.add(0,"张三");
    people.add(1,"李四");
    people.add(2,"王五");
    people.add(3,"赵六");
    people.add(4,"田六");
    request.setAttribute("list",people);
%>


<%--
var , 每一次遍历出来的变量
items, 要遍历的对象
begin,   哪里开始
end,     到哪里
step,   步长
--%>
<c:forEach var="people" items="${list}">
    <c:out value="${people}"/> <br>
</c:forEach>

<hr>

<c:forEach var="people" items="${list}" begin="1" end="3" step="1" >
    <c:out value="${people}"/> <br>
</c:forEach>
</body>
</html>

```

# 9、JavaBean

实体类

JavaBean有特定的写法：

- 必须要有一个无参构造
- 属性必须私有化
- 必须有对应的get/set方法；

一般用来和数据库的字段做映射 ORM；

ORM ：**对象关系映射**

- 表—>类
- 字段–>属性
- 行记录---->对象

**people表**

| id   | name    | age  | address |
| ---- | ------- | ---- | ------- |
| 1    | 秦疆1号 | 3    | 西安    |
| 2    | 秦疆2号 | 18   | 西安    |
| 3    | 秦疆3号 | 100  | 西安    |

```java
class People{
    private int id;
    private String name;
    private int id;
    private String address;
}

class A{
    new People(1,"秦疆1号",3，"西安");
    new People(2,"秦疆2号",3，"西安");
    new People(3,"秦疆3号",3，"西安");
}

```

![image-20210126172944451](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126172944.png)

```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/26
  Time: 17:33
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ page import="com.kuang.pojo.People" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%--<%--%>
<%--    People people = new People();--%>
<%--    people.setAddress();--%>
<%--    people.setAge();--%>
<%--    people.setName();--%>
<%--    people.setId();--%>
<%--    --%>
<%--%>--%>

    <jsp:useBean id="people" class="com.kuang.pojo.People" scope="page">
    <jsp:setProperty name="people" property="address" value="西安"/>
    <jsp:setProperty name="people" property="age" value="3"/>
    <jsp:setProperty name="people" property="id" value="1"/>
    <jsp:setProperty name="people" property="name" value="狂神"/>
  </jsp:useBean>
<%--<%= people.getAddress()%>--%>

    姓名：<jsp:setProperty name="people" property="name"/>
    id：<jsp:setProperty name="people" property="id"/>
    年龄：<jsp:setProperty name="people" property="age"/>
    地址：<jsp:getProperty name="people" property="address"/>
</body>
</html>

```

**出现了大问题：**usebean无法初始化

解决方法：

![image-20210126183842837](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126183842.png)

![image-20210126183853716](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126183853.png)

获取了.class字节码文件后，将其复制到相干idea项目目录下的web文件的WEB-INF的classes下

![image-20210126183745735](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126183745.png)

# 10、MVC三层架构

- 什么是MVC： Model view Controller 模型、视图、控制器

## 10.1、以前的架构

![image-20210126184638367](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126184638.png)

用户直接访问控制层，控制层就可以直接操作数据库；

```java
servlet--CRUD-->数据库
弊端：程序十分臃肿，不利于维护  
servlet的代码中：处理请求、响应、视图跳转、处理JDBC、处理业务代码、处理逻辑代码

架构：没有什么是加一层解决不了的！
程序猿调用

          数据库
          JDBC （实现该接口）

Mysql    Oracle     SqlServer    ....（不同厂商）
```

## 10.2、MVC三层架构

![image-20210126184959830](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126185000.png)

**Model**

- 业务处理 ：业务逻辑（Service）
- 数据持久层：CRUD （Dao - 数据持久化对象）

**View**

- 展示数据
- 提供链接发起Servlet请求 （a，form，img…）

**Controller （Servlet）**

- 接收用户的请求 ：（req：请求参数、Session信息….）

- 交给业务层处理对应的代码

- 控制视图的跳转

  ```java
  登录--->接收用户的登录请求--->处理用户的请求（获取用户登录的参数，username，password）---->交给业务层处理登录业务（判断用户名密码是否正确：事务）--->Dao层查询用户名和密码是否正确-->数据库
  ```

# 11、Filter 过滤器（重点）

比如 Shiro安全框架技术就是用Filter来实现的

Filter：过滤器 ，用来过滤网站的数据；

- 处理中文乱码
- 登录验证….

（比如用来过滤网上骂人的话，我***我自己 0-0）

![](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126185525.png)
Filter开发步骤：

1. 导包

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.kuang</groupId>
    <artifactId>javaweb-05-filter</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>servlet-api</artifactId>
            <version>2.5</version>
        </dependency>

        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>javax.servlet.jsp-api</artifactId>
            <version>2.3.3</version>
        </dependency>

        <dependency>
            <groupId>javax.servlet.jsp.jstl</groupId>
            <artifactId>jstl-api</artifactId>
            <version>1.2</version>
        </dependency>

        <dependency>
            <groupId>taglibs</groupId>
            <artifactId>standard</artifactId>
            <version>1.1.2</version>
        </dependency>

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.49</version>
        </dependency>
    </dependencies>
</project>
```

### 中文乱码

1. 编写过滤器
   1. 导包不要错 **（注意）**

![[(img-HHsC3JBD-1588757845420)(JavaWeb.assets/1568425162525.png)]](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126193130.png)



**过滤器处理乱码问题**

1.未处理时

```java
package com.kuang.filter;

import javax.servlet.*;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/26 - 01 - 26 - 19:30
 * @Description: com.kuang.filter
 * @version: 1.0
 */
public class CharacterEncodingFilter implements Filter {
    //初始化
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {

    }

    //销毁
    @Override
    public void destroy() {

    }
}

```

```java
package com.kuang.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/26 - 01 - 26 - 19:33
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class ShowServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.getWriter().write("你好呀，世界！");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                             http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">

    <servlet>
      <servlet-name>ShowServlet</servlet-name>
      <servlet-class>com.kuang.servlet.ShowServlet</servlet-class>
    </servlet>
  <servlet-mapping>
    <servlet-name>ShowServlet</servlet-name>
    <url-pattern>/Servlet/Show</url-pattern>
  </servlet-mapping>
</web-app>
```

![image-20210126193841207](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126193841.png)

2.实现filer：

实现Filter接口，重写对应的方法即可

```java

  public class CharacterEncodingFilter implements Filter {
  
      //初始化：web服务器启动，就以及初始化了，随时等待过滤对象出现！
      public void init(FilterConfig filterConfig) throws ServletException {
          System.out.println("CharacterEncodingFilter初始化");
      }
  
      //Chain : 链
      /*
      1. 过滤中的所有代码，在过滤特定请求的时候都会执行
      2. 必须要让过滤器继续同行
          chain.doFilter(request,response);
       */
      public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
          request.setCharacterEncoding("utf-8");
          response.setCharacterEncoding("utf-8");
          response.setContentType("text/html;charset=UTF-8");
  
          System.out.println("CharacterEncodingFilter执行前....");
          chain.doFilter(request,response); //让我们的请求继续走，如果不写，程序到这里就被拦截停止！
          System.out.println("CharacterEncodingFilter执行后....");
      }
  
      //销毁：web服务器关闭的时候，过滤器会销毁
      public void destroy() {
          System.out.println("CharacterEncodingFilter销毁");
      }
  }
  
```
3.在web.xml中配置 Filter

```xml
 <servlet>
      <servlet-name>ShowServlet</servlet-name>
      <servlet-class>com.kuang.servlet.ShowServlet</servlet-class>
    </servlet>
  <servlet-mapping>
    <servlet-name>ShowServlet</servlet-name>
    <url-pattern>/Servlet/Show</url-pattern>
  </servlet-mapping>
<!--    访问/Show就不会通过服务器-->
    <servlet-mapping>
        <servlet-name>ShowServlet</servlet-name>
        <url-pattern>/Show</url-pattern>
    </servlet-mapping>

    <filter>
        <filter-name>CharacterEncodingFilter</filter-name>
        <filter-class>com.kuang.filter.CharacterEncodingFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>CharacterEncodingFilter</filter-name>
        <!--只要是 /servlet的任何请求，会经过这个过滤器-->
        <url-pattern>/Servlet/*</url-pattern>
        <!--<url-pattern>/*</url-pattern>-->
        <!-- 别偷懒写个 /* -->
    </filter-mapping>
```

![image-20210126195104343](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126195104.png)

# 12、Listener监听器

实现一个监听器的接口；（有n种监听器）

1. 编写一个监听器

   实现监听器的接口…

   依赖的jar包![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126195429.png)

   ### 统计网站在线人数

   ```java
   package com.kuang.listener;
   
   import javax.servlet.ServletContext;
   import javax.servlet.http.HttpSessionEvent;
   import javax.servlet.http.HttpSessionListener;
   
   /**
    * @author Administrator
    * @Auther: wuxy
    * @Date: 2021/1/26 - 01 - 26 - 20:02
    * @Description: com.kuang.listener
    * @version: 1.0
    * //统计网站在线人数 ： 统计session
    */
   public class OnlineCountListener implements HttpSessionListener {
       //创建session监听： 看你的一举一动
       //一旦创建Session就会触发一次这个事件！
       @Override
       public void sessionCreated(HttpSessionEvent httpSessionEvent) {
           ServletContext servletContext = httpSessionEvent.getSession().getServletContext();
   
           System.out.println(httpSessionEvent.getSession().getId());
   
           Integer onlineCount = (Integer) servletContext.getAttribute("OlineCount");
   
           if(onlineCount==null){
               onlineCount = new Integer(1);
           }else{
               int count = onlineCount.intValue();
               onlineCount = new Integer(count++);
           }
           servletContext.setAttribute("OlineCount",onlineCount);
       }
   
       //销毁session监听
       //一旦销毁Session就会触发一次这个事件！
       @Override
       public void sessionDestroyed(HttpSessionEvent httpSessionEvent) {
           ServletContext servletContext= httpSessionEvent.getSession().getServletContext();
   
           Integer onlineCount = (Integer) servletContext.getAttribute("OnlineCount");
   
           if (onlineCount==null){
               onlineCount = new Integer(0);
           }else {
               int count = onlineCount.intValue();
               onlineCount = new Integer(count-1);
           }
   
           servletContext.setAttribute("OnlineCount",onlineCount);
       }
   }
   
   
   /*
       Session销毁：
       1. 手动销毁  getSession().invalidate();
       2. 自动销毁
        */
   ```

2. web.xml中注册监听器

   ```xml
   <!--注册监听器-->
   <listener>
       <listener-class>com.kuang.listener.OnlineCountListener</listener-class>
   </listener>
   ```
   
3. 看情况是否使用！

4. ```jsp
   <%--
     Created by IntelliJ IDEA.
     User: Administrator
     Date: 2021/1/26
     Time: 20:10
     To change this template use File | Settings | File Templates.
   --%>
   <%@ page contentType="text/html;charset=UTF-8" language="java" %>
   <html>
   <head>
       <title>Title</title>
   </head>
   <body>
   <h1>当前在线人数：<span><%=this.getServletConfig().getServletContext().getAttribute("OlineCount")%></span></h1>
   </body>
   </html>
   
   ```

5. ![image-20210126201536381](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210126201536.png)

# 13、过滤器、监听器常见应用

## **监听器：GUI编程中经常使用；**

```java
package com.kuang.listener;

import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/26 - 01 - 26 - 20:21
 * @Description: com.kuang.listener
 * @version: 1.0
 */
public class TestPannel {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Frame frame = new Frame("hh");
        Panel panel = new Panel(null) ;

        frame.setLayout(null);

        frame.setBounds(300,300,500,500);
        frame.setBackground(new Color(0,0,255));

        panel.setBounds(50,50,300,300);
        panel.setBackground(new Color(0,255,0)); //设置背景颜色

        frame.add(panel);

        frame.setVisible(true);

        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                super.windowClosing(e);
                System.exit(0);
            }
        });
    }
}

```

## 过滤器：

用户登录之后才能进入主页！用户注销后就不能进入主页了！

1. 用户登录之后，向Sesison中放入用户的数据
2. 进入主页的时候要判断用户是否已经登录；要求：在过滤器中实现！

![image-20210127004208149](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127004208.png)

```java
package com.kuang.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/26 - 01 - 26 - 22:39
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class Loginservlet extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //
        String username = req.getParameter("username");
        if(username.equals("admin")){
            req.getSession().setAttribute("USER_SESSION",req.getSession().getId());
            resp.sendRedirect("/sys/success.jsp");
        }else{
            resp.sendRedirect("/error.jsp");
        }
    }

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doGet(req, resp);
    }
}

```

```java
package com.kuang.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/26 - 01 - 26 - 22:49
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class LogoutServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        Object user_session = req.getSession().getAttribute("USER_SESSION");
        if(user_session!=null){
            req.getSession().removeAttribute("USER_SESSION");
            resp.sendRedirect("/Login.jsp");
        }else{
            resp.sendRedirect("/Login.jsp");
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```

```java
package com.kuang.filter;

import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/26 - 01 - 26 - 22:54
 * @Description: com.kuang.filter
 * @version: 1.0
 */
public class SysFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        HttpServletRequest httpServletRequest = (HttpServletRequest) servletRequest;
        HttpServletResponse httpServletResponse = (HttpServletResponse) servletResponse;

        if((httpServletRequest.getSession().getAttribute("USER_SESSION"))==null){
            httpServletResponse.sendRedirect("/error.jsp");
        }
        filterChain.doFilter(servletRequest,servletResponse);
    }

    @Override
    public void destroy() {

    }
}

```

```xml
<servlet>
        <servlet-name>LoginServlet</servlet-name>
        <servlet-class>com.kuang.servlet.Loginservlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>LoginServlet</servlet-name>
        <url-pattern>/servlet/login</url-pattern>
    </servlet-mapping>

    <servlet>
        <servlet-name>LogoutServlet</servlet-name>
        <servlet-class>com.kuang.servlet.LogoutServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>LogoutServlet</servlet-name>
        <url-pattern>/servlet/logout</url-pattern>
    </servlet-mapping>

<filter>
        <filter-name>SysFilter</filter-name>
        <filter-class>com.kuang.filter.SysFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>SysFilter</filter-name>
        <!--只要是 /sys的任何请求，会经过这个过滤器-->
        <url-pattern>/sys/*</url-pattern>
        <!--<url-pattern>/*</url-pattern>-->
        <!-- 别偷懒写个 /* -->
    </filter-mapping>

```

```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/26
  Time: 22:37
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<form action="/servlet/login" method="post">
    <input type="text" name="username">
    <input type="submit">

</form>
</body>
</html>

```



```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/26
  Time: 22:47
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>主页</h1>

<p> <a href="/servlet/logout">注销</a> </p>
</body>
</html>

```



```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/26
  Time: 22:47
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>主页</h1>

<p> <a href="/servlet/logout">注销</a> </p>
</body>
</html>

```

![image-20210127004231313](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127004231.png)

![image-20210127004302056](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127004302.png)

![image-20210127004309504](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127004309.png)

3.分等级登录（过滤器）

![image-20210127004553931](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127004554.png)

# 14、JDBC

什么是JDBC ： Java连接数据库！

![[(img-rZzTXmtn-1588757845422)(JavaWeb.assets/1568439601825.png)]](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127010026.png)

需要jar包的支持：

- java.sql
- javax.sql
- mysql-conneter-java… 连接驱动（必须要导入）

**实验环境搭建**

```sql
CREATE TABLE users(
    id INT PRIMARY KEY,
    `name` VARCHAR(40),
    `password` VARCHAR(40),
    email VARCHAR(60),
    birthday DATE
);

INSERT INTO users(id,`name`,`password`,email,birthday)
VALUES(1,'张三','123456','zs@qq.com','2000-01-01');
INSERT INTO users(id,`name`,`password`,email,birthday)
VALUES(2,'李四','123456','ls@qq.com','2000-01-01');
INSERT INTO users(id,`name`,`password`,email,birthday)
VALUES(3,'王五','123456','ww@qq.com','2000-01-01');


SELECT	* FROM users;

```

![image-20210127010633106](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127010633.png)

导入数据库依赖

```xml
<dependencies>
    <!--mysql的驱动-->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.49</version>
    </dependency>
    </dependencies>
```

IDEA中连接数据库：

![[(img-XErw4ElS-1588757845423)(JavaWeb.assets/1568440926845.png)]](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127011606.png)

**JDBC 固定步骤：**

1. 加载驱动
2. 连接数据库,代表数据库
3. 向数据库发送SQL的对象Statement : CRUD
4. 编写SQL （根据业务，不同的SQL）
5. 执行SQL
6. 关闭连接（先开的后关）

```java
package com.kuang.test;

import java.sql.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/27 - 01 - 27 - 1:17
 * @Description: com.kuang.test
 * @version: 1.0
 */
public class JdbcTest {
    public static void main(String[] args) throws ClassNotFoundException, SQLException {
        //配置信息
        //useUnicode=true&characterEncoding=utf-8 解决中文乱码
        String url="jdbc:mysql://localhost:3306/jdbc?useUnicode=true&characterEncoding=utf-8";
        String username = "root";
        String password = "123456";

        //1.加载驱动
        Class.forName("com.mysql.jdbc.Driver");
        //2.连接数据库,代表数据库
        Connection connection = DriverManager.getConnection(url, username, password);

        //3.向数据库发送SQL的对象Statement,PreparedStatement : CRUD
        Statement statement = connection.createStatement();

        //4.编写SQL 查询使用的是executeQuery(sql)
      //受影响的行数，增删改都是使用executeUpdate(sql)
        String sql = "select * from users";

        //5.执行查询SQL，返回一个 ResultSet  ： 结果集
        ResultSet rs = statement.executeQuery(sql);

        while (rs.next()){
            System.out.println("id="+rs.getObject("id"));
            System.out.println("name="+rs.getObject("name"));
            System.out.println("password="+rs.getObject("password"));
            System.out.println("email="+rs.getObject("email"));
            System.out.println("birthday="+rs.getObject("birthday"));
        }

        //6.关闭连接，释放资源（一定要做） 先开后关
        rs.close();
        statement.close();
        connection.close();
    }
}

```

![image-20210127011822342](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127011822.png)

**预编译SQL**

```java
package com.kuang.test;

import java.sql.Connection;
import java.sql.Date;
import java.sql.DriverManager;
import java.sql.PreparedStatement;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/27 - 01 - 27 - 1:21
 * @Description: com.kuang.test
 * @version: 1.0
 */
public class JdbcTest2 {
    public static void main(String[] args) throws Exception {
        //配置信息
        //useUnicode=true&characterEncoding=utf-8 解决中文乱码
        String url="jdbc:mysql://localhost:3306/jdbc?useUnicode=true&characterEncoding=utf-8";
        String username = "root";
        String password = "123456";

        //1.加载驱动
        Class.forName("com.mysql.jdbc.Driver");
        //2.连接数据库,代表数据库
        Connection connection = DriverManager.getConnection(url, username, password);

        //3.编写SQL
        String sql = "insert into  users(id, name, password, email, birthday) values (?,?,?,?,?);";

        //4.预编译
        PreparedStatement preparedStatement = connection.prepareStatement(sql);

        preparedStatement.setInt(1,4);//给第一个占位符？ 的值赋值为1；
        preparedStatement.setString(2,"狂神说Java");//给第二个占位符？ 的值赋值为狂神说Java；
        preparedStatement.setString(3,"123456");//给第三个占位符？ 的值赋值为123456；
        preparedStatement.setString(4,"24736743@qq.com");//给第四个占位符？ 的值赋值为1；
        preparedStatement.setDate(5, Date.valueOf("2000-01-01"));//给第五个占位符？ 的值赋值为new Date(new java.util.Date().getTime())；

        //5.执行SQL
        int i = preparedStatement.executeUpdate();

        if (i>0){
            System.out.println("插入成功@");
        }

        //6.关闭连接，释放资源（一定要做） 先开后关
        preparedStatement.close();
        connection.close();
    }
}

```

![image-20210127012457847](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127012458.png)

**事务**

要么都成功，要么都失败！

ACID原则：保证数据的安全。

```java
开启事务
事务提交  commit()
事务回滚  rollback()
关闭事务

转账：
A:1000
B:1000
    
A(900)   --100-->   B(1100) 
12345678910
```

**Junit单元测试**

依赖

```xml
 <dependencies>
    <!--mysql的驱动-->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.49</version>
    </dependency>

        <!--单元测试-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
    </dependencies>
```

简单使用

@Test注解只有在**方法**上有效，只要加了**这个注解的方法**，就可以直接运行！

```java
@Test
public void test(){
    System.out.println("Hello");
}

```

![[(img-OsUubVNQ-1588757845424)(JavaWeb.assets/1568442261610.png)]](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127012656.png)

失败的时候是红色：

![[(img-qv2oTEGI-1588757845425)(JavaWeb.assets/1568442289597.png)]](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127012700.png)

**搭建一个环境**

```sql
CREATE TABLE account(
   id INT PRIMARY KEY AUTO_INCREMENT,
   `name` VARCHAR(40),
   money FLOAT
);

INSERT INTO account(`name`,money) VALUES('A',1000);
INSERT INTO account(`name`,money) VALUES('B',1000);
INSERT INTO account(`name`,money) VALUES('C',1000);
```

![image-20210127013024648](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127013024.png)

```sql
package com.kuang.test;

import org.junit.Test;

import java.sql.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/27 - 01 - 27 - 1:30
 * @Description: com.kuang.test
 * @version: 1.0
 */
public class JdbcTest3 {
    @Test
    public void test() {
        //配置信息
        //useUnicode=true&characterEncoding=utf-8 解决中文乱码
        String url="jdbc:mysql://localhost:3306/jdbc?useUnicode=true&characterEncoding=utf-8";
        String username = "root";
        String password = "123456";

        Connection connection = null;

        //1.加载驱动
        try {
            Class.forName("com.mysql.jdbc.Driver");
            //2.连接数据库,代表数据库
            connection = DriverManager.getConnection(url, username, password);

            //3.通知数据库开启事务,false 开启    关闭自动提交
            connection.setAutoCommit(false);

            String sql = "update account set money = money-100 where name = 'A'";
            connection.prepareStatement(sql).executeUpdate();

            //制造错误
            //int i = 1/0;

            String sql2 = "update account set money = money+100 where name = 'B'";
            connection.prepareStatement(sql2).executeUpdate();

            connection.commit();//以上两条SQL都执行成功了，就提交事务！
            System.out.println("success");
        } catch (Exception e) {
            try {
                //如果出现异常，就通知数据库回滚事务
                connection.rollback();
            } catch (SQLException e1) {
                e1.printStackTrace();
            }
            e.printStackTrace();
        }finally {
            try {
                connection.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}

```

![image-20210127013200756](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127013200.png)

![image-20210127013238922](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127013239.png)