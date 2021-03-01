# 一、计算机语言的发展历史

​        计算机编程语言的发展，是随着计算机本身硬件发展而发展的。硬件速度越快、体积越小、成本越低，应用到人类社会的场景就会越多，那么所需要的算法就会越复杂，也就要求计算机编程语言越高级。最初重达几十吨但一秒只能运算5000次的ENIAC(世界上第一台计算机)，只能做非常小的应用，比如：某些情况的弹道计算。现在任何一个人的手机运算能力都可以秒杀那个年代地球上所有计算机运算能力的总和。计算机编程语言的发展历经了从低级到高级发展。发展的核心思想就是“让人更容易编程”。越容易使用的语言，就有越多人使用；越多人使用，就有越多协作；越多协作，就可以创造越复杂的物体；计算机语言经历了三代：第一代是机器语言，第二代是汇编语言，第三代是高级语言。

![image-20201229081018174](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229081018174.png)

## 【1】第一代：机器语言（相当于人类的原始阶段）

​        （打孔机）机器语言是机器指令的集合，机器指令展开来讲就是一台机器可以正确执行的命令。电子计算机的机器指令是一列二进制数字。计算机将之转变为一列高低电平，以使计算机的电子器件受到驱动，从而进行运算。上面所说的计算机，指的是可以执行机器指令，进行运算的机器。这是早期计算机的概念。早期的程序设计均使用机器语言。程序员们将用 0、1 数字编程的程序代码打在纸袋或卡片上，1打孔，0不打孔，再将程序通过纸带机或卡片机输入计算机，从而进行运算。
​        应用8086CPU完成运算s=768+12288-1280，机器码如下:

![image-20201229081335287](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229081335287.png)

​        假如将程序错写成以下的错误，请你找出错误:

![image-20201229081349453](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229081349453.png)

​        书写和阅读机器码程序不是一件简单的工作，要记住所有抽象的二进制码。上面只是一个非常简单的小程序，就暴露出机器码的晦涩难懂和不易查错。写如此小的一个程序尚且如此，实际上一个有用的程序至少要有几十行的机器码。那么，情况将会怎么样呢？
​        在显示器输出“welcome to masm”，机器码如下：

![image-20201229081408601](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229081408601.png)

![image-20201229081429445](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229081429445.png)

​        看到这样的程序，你有什么感想？如果程序里有一个“1”被误写成为“0”，又如何去查找错误呢？                **找Bug**

## 【2】第二代：汇编语言（相当于人类的手工业阶段）

​        为了编程的方便，以及解决更加复杂的问题。程序员开始改进机器语言，使用**英文缩写的助记符**来表示基本的计算机操作。这些助记符构成了汇编语言的基础。如下是一些常见的汇编语言助记符(单词)比如：mov，add，sub之类，这样人更容易使用了。识别几百、几千个单词，感觉要比几百几千个数字，美妙多了。汇编语言相当于人类的手工业社会，需要技术极其娴熟的工匠，但是**开发效率也非常低**。汇编语言虽然能编写高效率的程序，但是学习和使用都不是易事，并且很难调试。另一个复杂的问题，汇编语言以及早期的计算机语言（Basic、Fortran等）**没有考虑结构化设计原则**，而是使用goto语句来作为**程序流程控制**的主要方法。这样做的后果是：一大堆混乱的调转语句使得程序几乎不可能被读懂。对于那个时代的程序员，能读懂上个月自己写的代码都成为一种挑战。 汇编语言仍然应用于工业电子编程领域、软件的加密解密、计算机病毒分析等。
​        下面以Masm软件为例，编写一个简单的“hello world!”程序。

![image-20201229081454005](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229081454005.png)

## 【3】第三代：高级语言（相当于人类的工业阶段）

​        对于简单的任务，汇编语言可以胜任。但是随着计算机的发展，渗透到了工作生活的更多的方面，一些复杂的任务出现了，汇编语言就显得力不从心（应该说是程序员使用汇编语言解决**复杂问题**出现了瓶颈）。于是，出现了**高级语言**。像我们熟知的**C、C++、Java**等等都是高级语言。
​        高级语言允许程序员使用接近日常英语的指令来编写程序。例如下图所示:

![image-20201229081510959](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229081510959.png)

# 二、JAVA简史

## 【1】SUN公司

美国SUN(Stanford University Network)公司
在中国大陆的正式中文名为“太阳计算机系统（中国）有限公司”
在台湾中文名为“升 阳电脑公司”。

## 【2】Java为什么被发明

Green项目。
应用环境：像电视盒这样的消费类电子产品
要求： 语言本身是中立的，也就是跨平台
        1996年Java第一次发布就引起了人们的极大兴趣。关注Java的人士不仅限于计算机出版界，  还有诸如《纽约时报》《华盛顿邮报》《商业周刊》这样的主流媒体。Java 是第一种也是唯一种在National Public Radio上占用了10分钟时间来进行介绍的程序设计语言，并且还得到了$100000000的风险投资基金。这些基金全部用来支持用这种特别的计算机语言开发的产品。重温那些令人兴奋的日子是很有意思的。我们将简要地介绍一下Java语言的发展历史：
        Java的历史要追溯到1991年，由Patrick Naughton 及其伙伴James Gosling (一个全能的计算机奇才)带领的Sun公同的工程师小组想要设计一种小型的计算机语言，主要用于像有线电视转换盒这类的消费设备。由于这些消费设备的处理能力和内存都很有限，所以语言必须非常小且能够生成非常紧凑的代码。另外，由于不同的厂商会选择不同的中央处理器(CPU)，因此这种语言的关键是不能与任何特定的体系结构捆绑在一起。这个项目被命名为"Green"。
        所有就要求有这样的一种代码： 代码短小、紧凑且与平台无关。但是，Sun公司的人都有UNIX的应用背景。因此，所开发的语言以C++为基础。 是Gosling率先创造了这个语言，把这种语言称为“Oak"(这么起名的原因大概是因为他非常喜欢自己办公室外的橡树)。Sun 公司的人后来发现Oak是一种已有的计算机语言的名字，于是，将其改名为Java。
![image-20201229082354362](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229082354362.png)                     

## 【3】Java的发明人

James  Gosling
         ![image-20201229082405950](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229082405950.png)          

## 【4】经历阶段

1991年，James Gosling在SUN公司的工程师小组想要设计这样一种小型计算机语言。该语言主要用于像电视盒这样的消费类电子产品。另外，由于不同的厂商选择不同的CPU和操作系统，因此，要求该语言不能和特定的体系结构绑在一起，要求语言本身是中立的，也就是跨平台的。所以，将这个语言命名为“Green”，类似于绿色软件的意思。后来，改名为Oak，橡树的意思。改名后发现已经有一种语言叫这个名字了，再改名叫Java。Java语言发展到今天经历了一系列的过程：
 1991年，SUN公司的Green项目，Oak橡树
 1995年，推出Java测试版
 1996年，JDK1.0
 1997年，JDK1.1
 1998年，JDK1.2，大大改进了早期版本缺陷，是一个革命性的版本，更名为Java2。
 2004年，J2SE 5.0 (1.5.0)  Tiger老虎 成为Java语言发展史上的又一里程碑。为了表示该版本的重要性，J2SE1.5更名为Java SE 5.0
 2005年，Java的各种版本已经更名，以取消其中的数字"2"： J2ME更名为Java ME， J2SE更名为Java SE， J2EE更名为Java EE；
 2006年，J2SE 6.0 (1.6.0)  Mustang野马
 2009年，甲骨文(oracle)收购SUN，交易高达价格74亿
 2011年，JavaSE7.0   Dolphin海豚
 **2014年，JavaSE8.0**
 2017年，JAVA 9.0
 2018年3月，JAVA 10
 2018年9月，JAVA 11
 2019年3月，JAVA 12
 2019年9月，JAVA 13
 2020年3月，JAVA 14
        注意：SUN公司已经被oracle公司收购，目前每半年更新一次java的版本。但是，企业中的主流仍然以7和8为主。对于初学者，应该以企业主流应用版本为核心进行学习，没有必须在此处追求最新版本。
![image-20201229082303788](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229082303788.png)         

## 【5】不同版本JDK说明

JDK Version 1.1
   于1997-02-19发行。
   引入的新特性包括：
   引入JDBC（Java Database Connectivity）；
   支持内部类；
   引入Java Bean；
   引入RMI（Remote Method Invocation）；
   引入反射（仅用于内省）。
J2SE Version 1.2
   开发代号为Playground（操场），于1998-12-08发行。
   引入的新特性包括：
   引入集合（Collection）框架；
   对字符串常量做内存映射；
   引入JIT（Just In Time）编译器；
   引入对打包的Java文件进行数字签名；
   引入控制授权访问系统资源的策略工具；
   引入JFC（Java Foundation Classes），包括Swing 1.0、拖放和Java 2D类库；
   引入Java 插件；
   在JDBC中引入可滚动结果集、BLOB、CLOB、批量更新和用户自定义类型；
   在Applet中添加声音支持。
J2SE Version 1.3
  开发代号为Kestrel（红隼），于2000-05-08发行。
   引入的新特性包括：
   引入Java Sound API；
   jar文件索引；
   对Java的各个方面都做了大量优化和增强。
J2SE Version 1.4
   开发代号为Merlin（隼），于2004-02-06发行（首次在JCP下发行）。
   引入的新特性包括:
   XML处理；
   Java打印服务；
   引入Logging API；
   引入Java Web Start；
   引入JDBC 3.0 API；
   引入断言；
   引入Preferences API；
   引入链式异常处理；
   支持IPv6；
   支持正则表达式；
   引入Image I/O slot machine API。
Java Version SE 5.0
   开发代号为Tiger（老虎），于2004-09-30发行。
   引入的新特性包括:
   引入泛型；
   增强循环，可以使用迭代方式；
   自动装箱与自动拆箱；
   类型安全的枚举；
   可变参数；
   静态引入；
   元数据（注解）；
   引入Instrumentation。
Java Version SE 6
   开发代号为Mustang（野马），于2006-12-11发行。
   引入的新特性包括：
   支持脚本语言；
   引入JDBC 4.0 API；
   引入Java Compiler API；
   可插拔注解；
   增加对Native PKI(Public Key Infrastructure)、Java GSS(Generic Security Service)、Kerberos和LDAP(Lightweight Directory Access   Protocol)的支持；
   继承Web Services；
   做了很多优化。
Java Version SE 7
   开发代号是Dolphin（海豚），于2011-07-28发行。
   引入的新特性包括：
   switch语句块中允许以字符串作为分支条件；
   在创建泛型对象时应用类型推断；
   在一个语句块中捕获多种异常；
   支持动态语言；
   支持try-with-resources；
   引入Java NIO.2开发包；
   数值类型可以用2进制字符串表示，并且可以在字符串表示中添加下划线；
   钻石型语法；
   null值的自动处理。
Java Version SE 8
   开发代号是Spider（蜘蛛），于2014-03-18发行。
   支持 lambda支持；
   增强日期与时间API的功能；
   对垃圾回收的性能也进行了改进；
   并且移除了permgen区。
   Lambdas表达式与Functional接口
   接口的默认与静态方法
   方法引用
   重复注解
   更好的类型推测机制
   扩展注解的支持
   ![image-20201229082225430](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229082225430.png)            

# 三、JAVA体系结构

**JavaSE（Java  Standard  Edition）：标准版，定位在个人计算机上的应用**
        这个版本是Java平台的核心，它提供了非常丰富的API来开发一般个人计算机上的应用程序，包括用户界面接口AWT及Swing，网络功能与国际化、图像处理能力以及输入输出支持等。在上世纪90年代末互联网上大放异彩的Applet也属于这个版本。Applet后来为Flash取代，Flash即将被HTML5取代。

**JavaEE（Java  Enterprise Edition）：企业版，定位在服务器端的应用**
        JavaEE是JavaSE的扩展，增加了用于服务器开发的类库。如：JDBC是让程序员能直接在Java内使用的SQL的语法来访问数据库内的数据；Servlet能够延伸服务器的功能，通过请求-响应的模式来处理客户端的请求；JSP是一种可以将Java程序代码内嵌在网页内的技术；

**JavaME（Java  Micro  Edition）：微型版，定位在消费性电子产品的应用上**
        JavaME是JavaSE的内伸，包含J2SE的一部分核心类，也有自己的扩展类,增加了适合微小装置的类库：javax.microedition.io.*等。该版本针对资源有限的电子消费产品的需求精简核心类库，并提供了模块化的架构让不同类型产品能够随时增加支持的能力。

![image-20201229090613596](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229090613596.png)

# 四、JAVA的特征和优势

** 跨平台/可移植性**
这是Java的核心优势。Java在设计时就很注重移植和跨平台性。比如：Java的int永远都是32位。不像C++可能是16，32，可能是根据编译器厂商规定的变化。这样的话程序的移植就会非常麻烦。

** 安全性**
Java适合于网络/分布式环境，为了达到这个目标，在安全性方面投入了很大的精力，使Java可以很容易构建防病毒，防篡改的系统。

** 面向对象**
面向对象是一种程序设计技术，非常适合大型软件的设计和开发。由于C++为了照顾大量C语言使用者而兼容了C，使得自身仅仅成为了带类的C语言，多少影响了其面向对象的彻底性！Java则是完全的面向对象语言。

** 简单性**
Java就是C++语法的简化版，我们也可以将Java称之为“C++-”。跟我念“C加加减”，指的就是将C++的一些内容去掉；比如：头文件，指针运算，结构，联合，操作符重载，虚基类等等。同时，由于语法基于C语言，因此学习起来完全不费力。

** 高性能**
Java最初发展阶段，总是被人诟病“性能低”；客观上，高级语言运行效率总是低于低级语言的，这个无法避免。Java语言本身发展中通过虚拟机的优化提升了几十倍运行效率。比如，通过JIT(JUST IN TIME)即时编译技术提高运行效率。 将一些“热点”字节码编译成本地机器码，并将结果缓存起来，在需要的时候重新调用。这样的话，使Java程序的执行效率大大提高，某些代码甚至接待C++的效率。
因此，Java低性能的短腿，已经被完全解决了。业界发展上，我们也看到很多C++应用转到Java开发，很多C++程序员转型为Java程序员。

** 分布式**
Java是为Internet的分布式环境设计的，因为它能够处理TCP/IP协议。事实上，通过URL访问一个网络资源和访问本地文件是一样简单的。Java还支持远程方法调用(RMI,Remote Method Invocation)，使程序能够通过网络调用方法。

** 多线程**
多线程的使用可以带来更好的交互响应和实时行为。 Java多线程的简单性是Java成为主流服务器端开发语言的主要原因之一。

** 健壮性**
Java是一种健壮的语言，吸收了C/C++ 语言的优点，但去掉了其影响程序健壮性的部分（如：指针、内存的申请与释放等）。Java程序不可能造成计算机崩溃。即使Java程序也可能有错误。如果出现某种出乎意料之事，程序也不会崩溃，而是把该异常抛出，再通过异常处理机制加以处理。

总结：**一句话：java很好！**
        但是，并不是说学习了java，以后所有的东西都要用java开发了：某些领域其他语言有更出色的表现，比如，Objective C和后来的Swift在iOS设备上就有着无可取代的地位。浏览器中的处理几乎完全由JavaScript掌控。Windows程序通常都用C++或C#编写。Java在服务器端编程和跨平台客户端应用领域则很有优势。
只能说，**不同的语言之间，平分秋色！**

# 五、JAVA核心机制

## 1.JAVA垃圾回收机制

​        垃圾收集的目的在除不再使用的对象，当对象建立的时候垃圾收集期，就开始监控对象的动态情况，垃圾收集主要是对内存的释放。创建对象的时候申请一个空间

    1.不再使用的内存空间应回收---》垃圾收集；
    2.Java消除了程序员回收无用内存空间的职责；提供一种系统级线程跟踪存储空间的分配情况。在JVM的空闲时，检查并释放可被释放的存储器空间；相比c++,开发人员负责要自己收回无用内存。
    3.垃圾收集在Java程序运行过程中自动进行，程序员无法精确控制和干预；
    4.GC的自动回收，提高了内存空间的利用效率，也提高了编程人员的效率，很大程度上减少了因为没有释放空间而导致的内存泄露。

后续：
更高级：
1.垃圾收集器有几种
2.垃圾收集器底层原理剖析
3.垃圾收集器算法，优化     

## 2.JAVA跨平台原理的解释：

JAVA跨平台原理的解释：

![image-20201229095458895](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229095458895.png)

C语言的跨平台解释：

![image-20201229102400768](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229102400768.png)
        **JVM(Java Virtual Machine)**就是一个虚拟的用于执行**bytecode字节码**的”虚拟计算机”。他也定义了指令集、寄存器集、结构栈、垃圾收集堆、内存区域。JVM负责将Java字节码解释运行，边解释边运行，这样，速度就会受到一定的影响。
不同的操作系统有不同的虚拟机。Java 虚拟机机制屏蔽了底层运行平台的差别，实现了“**一次编译，随处运行**”。 Java虚拟机是实现跨平台的核心机制。如图所示：

![image-20201229102417005](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229102417005.png)

​        我们说的语言跨平台是编译后的文件跨平台，而不是源程序跨平台。
​        接下来我们再比较下两种方式的差异：

第一，C语言是编译执行的，编译器与平台相关，编译生成的可执行文件与平台相关；

第二，Java是解释执行的，编译为中间码的编译器与平台无关，编译生成的中间码也与平台无关（一次编译，到处运行），中间码再由解释器解释执行，解释器是与平台相关的，也就是不同的平台需要不同的解释器.

# 六、常用的DOS命令

## 【1】DOS操作系统

--Microsoft公司推出的操作系统。（在windows之前的操作系统）
--DOS是英文"Disk Operating System"的缩写,其中文含意是"磁盘操作系统".
--DOS是单用户、单任务的操作系统.（只能执行一个任务）

![image-20201229102530622](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229102530622.png)

【2】DOS命令
--在windows中，我们通过鼠标菜单等来操作系统，而在dos操作系统中，要通过dos命令来操作系统。
--是DOS操作系统的命令，是一种面向磁盘的操作命令，
--不区分大小写。
【3】命令学习：
windows给我们保留了类似dos系统的操作界面，可以直接操作磁盘！
dos 也是一种操作系统，是在windows出现以前用的，后来windows出来后基本没人用了，但是当windows崩溃的时候，还是要的dos方式解决，它是一种纯命令方式，cmd其实就是在windows状态下进入dos方式。

控制命令台：win+r--->cmd

![image-20201229102544793](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229102544793.png)

【4】具体dos命令：
（1）切换盘符： c:  d:  e:   大小写没有区分
（2）显示详细信息：**dir**

![image-20201229105817977](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229105817977.png)

（3）改变当前目录：**cd**

![image-20201229105842120](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229105842120.png)

（4）
**.** 当前目录
**..**  代表上一层目录

![image-20201229105900608](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229105900608.png)

![image-20201229105911917](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229105911917.png)

（5）清屏：**cls**
（6）切换历史命令：**上下箭头** 
（7）补全命令： **tab按键**
（8）创建目录：**md**
          删除目录：**rd**

![image-20201229105941519](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229105941519.png)

（9）复制文件命令：**copy**:

![image-20201229105949199](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229105949199.png)

（10）删除文件：**del**
del后面如果接的是文件夹/目录：那么删除的就是这个文件夹下的文件，而不是文件夹

![image-20201229105957200](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229105957200.png)

# 七、JAVA环境准备--》JDK

## 【1】下载JDK

www.oracle.com/technetwork/java/javase/downloads/index.html

 ![image-20201229110203193](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229110203193.png)

## 【2】安装JDK

![image-20201229110218442](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229110218442.png)

![image-20201229110226436](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229110226436.png)

![image-20201229110239059](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229110239059.png)

## 【3】卸载JDK

控制面板卸载即可

![image-20201229110252855](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229110252855.png)

## 【4】 验证JDK是否安装成功

（1）方式1：去安装目录下看一眼：

![image-20201229110311392](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229110311392.png)

（2）方式2：通过控制命令台查看：

![image-20201229110323377](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229110323377.png)

（3）方式3：通过控制面板查看：

![image-20201229110329120](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229110329120.png)

## 【5】JDK和JRE：

**JDK**： Java Development kit   ---->编写Java程序的程序员使用的软件

**JRE** : Java Runtime Enviroment  ----》运行Java程序的用户使用的软件

# 八、安装notepad++，配置path环境变量

## 【1】安装记事本：notepad

## 【2】安装：一直下一步

![image-20201229113243458](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229113243458.png)

## 【3】打开记事本进行设置：

设置--》首选项：

![image-20201229113252388](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229113252388.png)

设置--》语言格式设置：

![image-20201229113300421](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229113300421.png)

## 【4】打开notepad++:

（1）方式1：通过快捷方式：

![image-20201229113309692](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229113309692.png)

（2）方式2：通过可执行文件：

![image-20201229113320102](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229113320102.png)

（3）方式3：利用控制命令台：
win+r-->cmd:

![image-20201229113329314](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229113329314.png)

(4)方式4：在任意的路径下去执行notepad++.exe这个命令：
但是发现报错：

![image-20201229113340885](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229113340885.png)

需要配置系统环境变量：

![](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229113352894.png)

找系统环境变量：

![image-20201229113410901](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229113410901.png)

![image-20201229113425690](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229113425690.png)

将notepad++.exe所在的路径配置到path环境变量中去：

![image-20201229113444371](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229113444371.png)

​        这样我就可以在任意的路径下去执行这个命令：（注意：控制命令台需要重启）

![image-20201229113452480](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229113452480.png)

**path环境变量作用：**
        将命令所在的路径配置到path中去，就相当于在计算机中“注册”了一样，以后找这个命令，会直接去你配置的路径下寻找。
达到了一个效果：在任意的路径下去执行某个命令---》path环境针对整个操作系统而言。

# 九、第一段程序

## 【1】用notepad编写代码：

```
public class HelloWorld{
        public static void main(String[] args){
                System.out.println("hi 这是一段Java程序。。。");
        }
}
```

记得保存  ctrl+s

## 【2】进行编译：

![image-20201229115649321](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229115649321.png)

发现出错了，分析出错原因：

![image-20201229115700064](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229115700064.png)

解决办法：
将javac.exe所在的路径 配置到 环境变量path中去，这样我就可以在任意的路径下去执行这个命令：

![image-20201229115719853](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229115719853.png)

配置好环境变量以后发现代码可以成功编译：

![image-20201229115731683](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229115731683.png)

验证：

![image-20201229115741152](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229115741152.png)

## 【3】进行解释/翻译/执行:

![image-20201229115750171](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229115750171.png)


上面执行过程成功的原因：

![image-20201229115757077](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229115757077.png)

# 十、程序中常见问题

【1】最低级的错误：单词拼写错误
【2】要求源文件名字和类名必须一模一样：

![image-20201229165540487](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229165540487.png)

出错：

![image-20201229165549859](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229165549859.png)

【3】所有的标点必须是英文状态下的：
中文状态：【】（）{} ！；：“‘《》？
英文状态：[]       ()  {}  !  ;   :   "  '  <> ?
【4】成对编程：
[] {} () <> ""  ''

【5】注意缩进 ：只要遇到{}就进行缩进  --->为了格式好看
缩进：tab 
向前缩进： shift+tab

【6】编译：
javac  HelloWorld.java
【7】执行：
java HelloWorld 
【8】java中**大小写严格区分，大小敏感**：
HelloWorld   Helloworld
a   A  
public PUBLIC


【9】我们要写代码：就当做有一个“框子”

```
public class HelloWorld{
        public static void main(String[] args){
               

  }

}
```


【10】一个源文件中可以有多个类，**只能有一个类被public修饰**，**源文件的名字必须跟public修饰的那个类名**保持一致。

![image-20201229165728174](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229165728174.png)


多个类会产生独立的字节码文件：

![image-20201229165742193](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229165742193.png)

执行的时候执行**各自独立**的字节码文件即可：

![image-20201229165753322](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229165753322.png)

# 十一、编译方式

【1】方式1：

![image-20201229171720733](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229171720733.png)

【2】方式2：

![image-20201229171727099](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229171727099.png)

【3】方式3：

![image-20201229171734369](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229171734369.png)

【4】方式4：
在notepad中右键文件 --》打开文件夹所在命令行

**(这是我们以后常用的方式)**

![image-20201229171746883](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229171746883.png)

# 十二、扩展：classpath环境变量

【1】系统有一个环境变量叫：classpath，现在我们将classpath环境变量**显式**的写出来：

![image-20201229171833948](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229171833948.png)

classpath作用：只要你配置到classpath中的路径，在执行**java的字节码文件**的时候，就会去这个配置的路径下找 对应的字节码文件：

现在我不配置.\了 我配置：

![image-20201229171842844](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229171842844.png)

自从我配置了这个环境变量以后，可以在任意的路径下去执行字节码文件：

总结：
        classpath作用：**针对java执行字节码文件而产生的环境变量，只要配置了字节码文件所在的路径以后，那么以后你在任意位置都可以执行对应的字节码文件**

# 十三、扩展：JAVA_HOME环境变量

后续我们会用到一个软件：tomcat，在执行startup.bat的时候会出现**闪退问题**：
解决：
必须要配置一个环境变量叫：**JAVA_HOME** 

![image-20201229171950756](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229171950756.png)


我再次启动才会成功：

然后我们的path环境变量中刚好可以借助JAVA_HOME里面的内容，通过%%做引入
**%JAVA_HOME%\bin**

![image-20201229172002530](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229172002530.png)

# 十三、API

![image-20201229172041202](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229172041202.png)

- JDK帮助文档
- SUN公司为JDK工具包提供了一整套文档资料,我们习惯上称之为JDK文档。
- JDK文档中提供了Java中的各种技术的详细资料,以及JDK中提供的各种类的帮助说明。
  JDk文档是Java语言的完整说明,大多数书籍中的类的介绍都要参照它来完成,它是编程者经常查阅的资料
- 如何理解API：就当做是一个“字典”，“使用手册”，API就相当于是一个电子的帮助文档，可以帮我们查看JDK提供的类的信息，平时查看的时候可结合百度一起看。

其实API没有什么神奇的，就是一个电子文档而已，帮助我们查看JAVA中涉及到的一些技能点：

![image-20201229172100132](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229172100132.png)

# 十四、代码量统计工具

![image-20201229172130530](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229172130530.png)

# 十五、注释

为了方便程序的阅读，Java语言允许程序员在程序中写上一些说明性的文字，用来提高程序的可读性，这些文字性的说明就称为注释。
注释不会出现在字节码文件中，即Java编译器编译时会跳过注释语句。
在Java中根据注释的功能不同，主要分为单行注释、多行注释和文档注释。
**单行注释**
单行注释使用“//”开头，“//”后面的单行内容均为注释。
**多行注释**
多行注释以“/*”开头以“*/”结尾，在“/*”和“*/”之间的内容为注释，我们也可以使用多行注释作为行内注释。但是在使用时要注意，多行注释不能嵌套使用。
**文档注释**
文档注释以“/**”开头以“*/”结尾， 注释中包含一些说明性的文字及一些JavaDoc标签（后期写项目时，可以生成项目的API）

## 1.单行注释和多行注释

```java
//下面是一段标准代码
//这是代码的“框子”，当前阶段你可以当做一个模板
//其实这就是一个类，类的名字是HelloWorld，这个名字可以随便起，但是一般首字母大写，驼峰命名，见名知意
public class HelloWorld{
        //下面是一个main方法，方法的格式是固定的
        public static void main(String[] args){
                //下面这句话的作用：将双引号中的内容进行原样输出
                /*
                这是多行注释
                每行都可以写
                单行注释和多行注释，按照你自己的需求去使用即可
                */
                System.out.println("hi....java");
        }
}
```

注意：
1.注释不会参与编译，编译后产生的**字节码文件**中不会有注释的内容
2.注释的作用：
（1）注释就起到了标注解释的作用，提高代码的**可读性**，方便自己，方便他人--》是一个非常良好，非常专业的习惯！！！
（2）方便代码的**调试**：

```java
public class HelloWorld2{
        public static void main(String[] args){	
                System.out.println("hi....java1");
                //System.out.println("hi....java2")
                System.out.println("hi....java3");
        }
}
```



## 2.文档注释

```java

/**
文档注释
@author zhaoss
@version 1.0
这是我们第一章文档注释的代码，比较重要
*/
public class HelloWorld3{
        public static void main(String[] args){	
                System.out.println("hi....java1");	
        }
        /**
        @param name 姓名
        @param age 年龄
        */
        public void eat(String name,int age){
                System.out.println("hello");	
        }
}
一般文档注释可以配合：jdk提供的工具javadoc.exe来一起使用，通过javadoc.exe可以对文档注释进行解析，生成一套以网页文件形式体现的该程序的说明文档。（自定义类对应的API）




```

一般文档注释可以配合：jdk提供的工具javadoc.exe来一起使用，通过javadoc.exe可以对文档注释进行解析，生成一套以网页文件形式体现的该程序的说明文档。（自定义类对应的API）



![image-20201229172800194](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229172800194.png)

![image-20201229172807413](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229172807413.png)

![image-20201229172815732](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229172815732.png)

![image-20201229172826994](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229172826994.png)

# 十六、反编译工具的使用

编译
源代码----->class

反编译
class---->源代码

反编译工具

jd-gui.exe

![image-20201229172905413](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229172905413.png)

# 十七、本章的最后一段代码

```java
public class HiWorld{
        public static void main(String[] args){
                //进行自我介绍：
                System.out.print("姓名：");
                System.out.print("\t丽丽\n");
                System.out.print("职业：");
                System.out.print("\t学生");
                /*
                (1)System.out.print和System.out.println区别联系：
                System.out.print ： 将双引号中内容原样输出，不换行
                System.out.println ：将双引号中内容原样输出，换行
                (2)转义字符：
                \就是转义字符：作用：将后面普通的字母转换为特殊含义
                \n  : 换行
                \t  : 距离前面有一个制表符位置
                */
                
                System.out.println();//换行
                System.out.println("1111111111111111111");
                System.out.println("11111111\t2222");
        }
}
```

# 十八、扩展面试题：JDK、JRE、JVM的区别

JDK,JRE,JVM的关系:

![image-20201229173252792](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229173252792.png)

**先说JDK和JRE:**
初学JAVA很容易被其中的很多概念弄的傻傻分不清楚，首先从概念上理解一下吧，**JDK**（Java Development Kit）简单理解就是**Java开发工具包**，**JRE**(Java Runtime Enviroment)是**Java的运行环境**，**JVM**( java virtual machine)也就是常常听到**Java虚拟机**。JDK是面向**开发者**的，JRE是面向使用**JAVA程序的用户**，上面只是简单的区别

通过上图发现发现有两个JRE文件夹，如果细看里面的内容基本上是一样的，如果是只是Java程序使用者，那么只会有最外层的那个JRE目录，JDK中是JRE自带的，你如果安装了JDK必然里面会有一个JRE.那么问题来了，为什么会有两套JRE呢？
从侧面证明:
利用javac.exe进行编译:

![image-20201229173230223](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229173230223.png)

然后我将C:\Program Files\Java\jdk1.8.0_151\lib\tools.jar改个名字,再去编译:

![image-20201229173221452](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229173221452.png)

证明:dt.jar和tools.jar是两个java最基本的包，里面包含了从java最重要的lang包到各种高级功能如可视化的swing包，是java必不可少的。而path下面的bin里面都是java的可执行的编译器及其工具，如java，javadoc等,报错的原因就是输入的javac的命令不是去JDK中bin目录去找的javac.exe，而是去JDK中lib目录中的tools.jar中com.sun.tools.javac.Main中执行，因此javac.exe只是一个**包装器（Wrapper）**，存在的目的是为了让开发者免于输入过长的指命。**这个时候发现JDK里的工具几乎是用Java所编写，同属于Java应用程序，因此要使用JDK所附的工具来开发Java程序，所以自身需要附一套JRE才能运行。**上图中与jdk同级目录下的JRE就是用来运行一般Java程序用的。
两套JRE运行的时候究竟运行哪一个呢，这个时候

1.JDK中java.exe先从**自身目录**中找，

2.然后**父级目录**中找，

3.如果都没有就去**注册表**中找

![image-20201229173211676](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229173211676.png)

**再说JRE和JVM:**
JVM -- java virtual machineJVM就是我们常说的java虚拟机，它是整个**java实现跨平台的最核心的部分**，所有的java程序会首先被编译为**.class的类文件**，这种类文件可以在虚拟机上执行，class文件并不直接与机器的操作系统相对应，而是经过虚拟机间接与操作系统交互，由虚拟机将程序解释给本地系统执行，类似于C#中的CLR。
JVM不能单独搞定class的执行，解释class的时候**JVM需要调用解释所需要的类库lib**。在JDK下面的的jre目录里面有两个文件夹bin和lib,在这里可以认为**bin里的就是jvm**，**lib中则是jvm工作所需要的类库**，**而jvm和 lib和起来就称为jre**。

![image-20201229173200895](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229173200895.png)

JVM+Lib=JRE，如果讲的具体点就是bin目录下的jvm.dll文件， jvm.dll无法单独工作，当jvm.dll启动后，会使用explicit的方法(就是使用Win32 API之中的LoadLibrary()与GetProcAddress()来载入辅助用的动态链接库)，而这些辅助用的动态链接库(.dll)都必须位 于jvm.dll所在目录的父目录之中。因此想使用哪个JVM，只需要设置PATH，指向JRE所在目录下的jvm.dll。

![image-20201229173152603](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20201229173152603.png)