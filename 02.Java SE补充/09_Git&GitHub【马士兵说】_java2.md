[官方文档](https://guides.github.com/activities/hello-world/)

# Git

## 一、Git简史

![image-20210301093414592](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301093414.png)

Linux---->人越来越多---->代码优化越来愈好------->项目管理工具-------->Bitkeeper------->

终止合作------>一周GIt------->将linux发布在Git上

## 二、Git 概念

Git 是一个免费的、开源的**分布式   版本控制系统**，可以快速高效地处理从小型到大型的项目。

## 三、Git版本控制系统

**什么是版本控制？**

版本控制（Revision control）是一种记录一个或若干文件内容变化，以便将来查阅特定版本修订情况的系统。 

- 实现跨区域多人协同开发
- 追踪和记载一个或者多个文件的历史记录
- 组织和保护你的源代码和文档
- 统计工作量
- 并行开发、提高开发效率
- 跟踪记录整个软件的开发过程
- 减轻开发人员的负担，节省时间，同时降低人为错误

**为什么要使用版本控制？** 

软件开发中采用版本控制系统是个明智的选择。 有了它你就可以将某个文件**回溯**到之前的状态，甚至将整个项目都回退到过去某个时间点的状态。 就算你乱来一气把整个项目中的文件改的改删的删，你也照样可以轻松恢复到原先的样子。 但额外增加的**工作量却微乎其微**。你可以比较文件的变化细节，查出最后是谁修改了哪个地方,从而找出导致怪异问题出现的原因，又是谁在何时报告了某个功能缺陷等等。 

![图片](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301101555.jpeg)

### **版本控制系统的分类**:

- **本地版本控制**

记录文件每次的更新，可以对每个版本做一个快照，或是记录补丁文件，适合个人用，如RCS。

![图片](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301101729.webp)

- **集中化的版本控制系统--------->SVN：**

  ![image-20210301092708641](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301092708.png)

  集中化的版本控制系统诸如CVS、SVN以及Perforce等，都有一个**单一的集中管理的服务器**,保存所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器**取出最新的文件或者提交更新**。多年以来，这已成为版本控制系统的标准做法，这种做法带来了许多好处现在每个人都可以在一定程度上看到项目中的其他人正在做些什么。而管理员也可以轻松掌控每个开发者的权限，并且管理一个集中化的版本控制系统;要远比在各个客户端上维护本地数据库来得轻松容易。 

  事分两面，有好有坏。这么做最显而易见的缺点是中央服务器的***单点故障***。如果服务器宕机一小时，那么在这一小时内， 谁都无法提交更新， 也就无法协同工作。

- **分布式的版本控制系统-------->Git：**

  由于上面集中化版本控制系统的那些缺点，于是分布式版本控制系统面世了。 在这类系统中，像 Git、 BitKeeper 等，==客户端并不只提取最新版本的文件快照，而是把代码仓库完整地镜像下来。==

  ![image-20210301092731492](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301092731.png)

  更进一步，许多这类系统都可以指定和若干不同的==远端代码仓库==进行交互。这样，你就可以在同一个项目中分别和不同工作小组的人相互协作。

  ![image-20210301092945065](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301092945.png)

  分布式的版本控制系统在管理项目时存放的不是项目版本与版本之间的差异。它存的是索引(所需磁盘空间很少所以每个客户端都可以放下整个项目的历史记录)

  ![image-20210301093044036](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301093044.png)

我们学习的东西，一定是当下最流行的！

### 常见的版本控制工具

主流的版本控制器有如下这些：

- **Git**
- **SVN**（Subversion）
- **CVS**（Concurrent Versions System）
- **VSS**（Micorosoft Visual SourceSafe）
- **TFS**（Team Foundation Server）
- Visual Studio Online

版本控制产品非常的多（Perforce、Rational ClearCase、RCS（GNU Revision Control System）、Serena Dimention、SVK、BitKeeper、Monotone、Bazaar、Mercurial、SourceGear Vault），现在影响力最大且使用最广泛的是Git与SVN

## 四、Git的安装及环境配置

1.访问 Git 官网地址（https://git-scm.com/download/），直接访问即可，这里下载根据你的系统选择，我这里选择 Windows系统，然后点击该 "**Windows**" 进入到下载页面。

![img](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301095251.jpeg)

2.进入到下载页面后，我们会看到如下界面。这里有两种类型的版本，一个是**安装版**，另一个是**便携版**。安装版是需要安装到本机的，便携版不需要安装，也就是可以放到移动U盘来用的。

![img](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301095314.jpeg)

- 我这里选择安装版64位（64-bit Git for Windows Setup），点击该串英文字母即可下载！
- Git 软件下载较慢，大家耐心等待...(如果等不住，可以到我的公众号下载，我已经把四个版本都下载了，后台回复 “ 图床 ” 即可获取链接)

3.下载好安装包之后，点击打开。这是软件说明，我们选择 “Next” 进行下一步。

![image-20210301094607371](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301094607.png)

4.接着，设置安装路径，点击 “**Browse...**” 选择安装 Git 到该文件夹，我建议选择 D 盘（非系统盘）。然后，点击 "**Next**" 进行下一步。

![image-20210301094559439](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301094559.png)

5.这里根据自己的需要选择，我已经把这些都翻译了。我演示就都默认了，然后 "**Next**" 下一步。

![image-20210301094617956](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301094618.png)

6.这里是询问你是否创建开始菜单，**并设置名称**。我这里不改变文本内容，直接 "**Next**" 下一步。

![image-20210301094626447](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301094626.png)

7. 这里是设置 Git **默认编辑器**，我们这里直接下一步 "**Next**"。

![image-20210301094636398](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301094636.png)

8. **调整新仓库中初始分支的名称**，你希望 Git 在 "**git init** "之后给初始分支取什么名字？

![image-20210301094835927](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301094835.png)

这里有两种选择：

1）Let git decide（让git决定）
2）Override the default branch name for new repositories（重写新存储库的默认分支名称）

我们在这里选择 第一种 默认的，然后点击 "Next" 进行下一步。

**9. 这是调整您的PATH环境的设置**

![image-20210301094849697](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301094849.png)

这里有三种选择：

1. Use Git from Git Bash only (只在Git Bash中使用Git)
2. Git from the command line and also from 3rd-party software (在命令行和第三方软件中使用Git)
3. Use Git and optional Unix tools from the Command prompt (在命令提示符下使用Git和可选的Unix工具。)

我们这步选择第二项默认的，毕竟还是新手嘛~接着 "**Next**" 下一步。

**10. 选择Https传输后台配置**

![image-20210301094909913](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301094909.png)

**这里有两种选择：**

1）Use the OpenSSL library.（使用OpenSSL库。服务器证书将使用ca-bundle crt文件进行验证。）

2）Use the native Windows Secure Channel library. (使用本机Windows安全通道库。服务器证书将使用Windows证书库进行验证，这个选项也允许你使用公司内部的根CA证书，例如通过活动目录域服务分发。使用本机的Windows安全通道库服务器证书将使用Windows证书库进行验证，这个选项也允许你使用公司内部的根CA证书，例如通过活动目录域服务分发的证书。这个选项也允许你使用公司内部的根CA证书。例如通过Active Directory Domain Services。)

这里我们选择 第一项，接着 "**Next**"进行下一步。

**11. 配置行尾转换，我们选择第一项（Windows推荐），接着 "Next" 下一步。**

![image-20210301094920382](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301094920.png)

**12. 配置与Git Bash一起使用的终端仿真器**

![image-20210301095009772](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301095009.png)

这里有两种选择：

1）Use MinTTY (the default terminal of MSYS2) 使用MinTTY（MSYS2的默认终端）相对于控制台，MinTTY 有更好的字体显示效果，以及舒服的操作方式。

2）Use windows default console window （使用Windows默认的控制台窗口，这个想必大家都是用过吧，也就是常见的CMD窗口）

我们这里选择默认的第一项，然后点击 "**Next**" 进行下一步。

**13. 选择git pull的默认行为**

![image-20210301095035327](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301095035.png)

这里有三种选择：

1）Default(fast-forward or merge) 默认(快进或合并)：这是git pull的标准行为：尽可能将当前分支快进到获取的分支，否则就创建一个合并提交。

2）Rebase 重设：如果没有 locacommits 要重设，则将当前分支重垒到获取的分支上，这相当于快进。

3）Only ever fast-forward 只有快进：快进到获取的分支。如果不可能，则失败。

这里我们也选择默认的第一项，然后 "Next"下一步。

**14. 配置凭证助手**

![image-20210301095101736](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301095101.png)

这里有三种选项：

1）Git Credential Manager Core （Git凭据管理器核心）
2）Git Credential Manager （Git证书管理器）
3）None （无，不需要凭证助手）

这里我们选择第一项，Git凭据管理器核心，然后 "**Next**"

**15. 配置额外的选项**

![image-20210301095116114](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301095116.png)

这里有两种选项：

1）Enable file system caching （启用文件系统缓存）
2）Enable symbolic links （启用符号链接）

**16. 配置实验选项，我们就不体验了，直接 "Next"。**

![image-20210301095137312](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301095137.png)

**17. 等他自行安装...**

![image-20210301095153414](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301095153.png)

18. 安装完成后，显示如下，我们点击 "finish"完成安装。至此，我们才仅仅安装好了 Git。哈哈哈，继续~

![image-20210301095219499](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301095219.png)

![image-20210301095900615](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301095900.png)

![image-20210301101802515](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301101802.png)

## 五、Git 的本地结构

![](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301100046.png)

![图片](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301145608.png)

### 代码托管中心

**代码托管中心作用是什么?** 

我们已经有了本地库，本地库可以帮我们进行版本控制，为什么还需要代码托管中心呢? 

它的任务是帮我们**维护远程库**, 下面说一下本地库和远程库的交互方式， 也分为两种:

1. 团队内部协作

   ![image-20210301100214077](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301100214.png)

2. 跨团队协作

   ![image-20210301100357261](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301100357.png)

**托管中心种类:** 

局域网环境下：可以搭建` GitLab` 服务器作为代码托管中心，GitLab 可以自己去搭建 

外网环境下：可以由 `GitHub` 或者 `Gitee` 作为代码托管中心，GitHub 或者 Gitee 是现成的托管中心，不用自己去搭建

## 六、Git基本理论（重要）

### 三个区域

Git本地有三个工作区域：**工作目录（Working Directory）**、**暂存区(Stage/Index)**、**资源库(Repository或Git Directory)**。如果在加上**远程的git仓库(Remote Directory)**就可以分为四个工作区域。文件在这四个区域之间的转换关系如下：

![图片](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301102042.webp)

- Workspace：工作区，就是你平时存放项目代码的地方
- Index / Stage：暂存区，用于临时存放你的改动，事实上它只是一个文件，保存即将提交到文件列表信息
- Repository：仓库区（或本地仓库），就是安全存放数据的位置，这里面有你提交到所有版本的数据。其中HEAD指向最新放入仓库的版本
- Remote：远程仓库，托管代码的服务器(Gitee GitHub)，可以简单的认为是你项目组中的一台电脑用于远程数据交换

本地的三个区域确切的说应该是git仓库中HEAD指向的版本：

![图片](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301102221.webp)

- Directory：使用Git管理的一个目录，也就是一个仓库，包含我们的工作空间和Git的管理空间。
- WorkSpace：需要通过Git进行版本控制的目录和文件，这些目录和文件组成了工作空间。
- .git：存放Git管理信息的目录，初始化仓库的时候自动创建。
- Index/Stage：暂存区，或者叫待提交更新区，在提交进入repo之前，我们可以把所有的更新放在暂存区。
- Local Repo：本地仓库，一个存放在本地的版本库；HEAD会只是当前的开发分支（branch）。
- Stash：隐藏，是一个工作状态保存栈，用于保存/恢复WorkSpace中的临时状态。



### 工作流程

git的工作流程一般是这样的：

１、在工作目录中添加、修改文件；

２、将需要进行版本管理的文件放入暂存区域 `git add .`；

３、将暂存区域的文件提交到git仓库 `git commit`。

因此，git管理的文件有三种状态：已修改（modified）,已暂存（staged）,已提交(committed)

![图片](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301102316.webp)

## 七、初始化本地仓库及Git常用命令

### 初始化本地仓库

1. 创建一个文件夹

   ![image-20210301101055763](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301101055.png)

2. 打开 Git 终端

   Git Bush Here：

   进入以后先对字体和编码进行设置：

   ![](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301101142.png)

![image-20210301101156630](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301101156.png)

### 常用的Git命令

**在 Git 中命令跟 Linux 是一样的：**

1. 查看 Git 安装版本：

   `$ git --version`

   ![image-20210301101210406](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301101210.png)

2. 清屏：

   `$ clear`

   ![image-20210301101220915](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301101220.png)

3. 设置签名：

   设置用户名和邮箱：

   `$ git config --global user.name "用户名"`

   `$ git config --global user.email "邮箱"`

   ![image-20210301101232026](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301101232.png)

4. 本地仓库的初始化：

   `$ git init`

   ![image-20210301101305130](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301101305.png)

   > .git 目录是隐藏的：可以调出来查看 

   ![image-20210301101328910](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301144937.png)

5. 查看 .git 下的内容：

   查看当前目录下的文件：`$ ll`

   查看当前目录下的子目录：`$ ll -la`

   回退到本目录上一级：`cd ..`

   打开子目录：`cd 子目录名`

   ![image-20210301101340875](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301101340.png)

   ![image-20210301101349419](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301101349.png)

   > .git 目录下的本地库相关的子目录和子文件不要删除，不要胡乱修改。

   

#### add&commit

添加文件： add 提交文件：commit

   1. 先创建一个文件：

      ![image-20210301101410986](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301101411.png)

   2. 将文件提交到暂存区：

      `$ git add 文件名`

      `$ git add Demo.txt`

      ![image-20210301101422910](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301101422.png)

   3. 将暂存区的内容提交到本地库

      `$ git commit -m "提交时的文字说明" 文件名`

      `$ git commit -m "This is the first submission" Demo.txt`

      ![image-20210301103218443](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301103218.png)

   > ![image-20210301101446939](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301101447.png)
   >
   > 1. 不放在本地仓库中的文件，git 是不进行管理的
   > 2. 即使放在本地仓库的文件，git 也不管理，必须通过 add、cimmit 命令操作才可以将内容提交到本地库

#### status

查看工作区和暂存区的状态

   `$ git status`

   1.创建一个文件，然后查看状态：

   ![image-20210301104225921](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301104225.png)

   ![image-20210301104249705](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301104249.png)

   2.然后将新创建的文件通过 `git add` 命令提交至暂存区：

   ![image-20210301104408203](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301104408.png)

3. 查看状态：

   ![image-20210301104423823](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301104423.png)

   4.使用 `git commit` 命令将文件提交至文本库：

   ![image-20210301104547612](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301104547.png)

   5.修改新创建文件中的文本内容：

   ![image-20210301104619272](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301104619.png)

   6.然后查看状态：

   ![image-20210301104643851](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301104643.png)

   7.重新添加至暂存区，然后将暂存区的文件提交至本地库：

   ![image-20210301104909208](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301104909.png)

   8.提交完再查看状态：

   ![image-20210301104925077](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301104925.png)

#### log

查看提交（显示从最近时间提交到最远时间提交）：

`$ git log`

![image-20210301105137714](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301105137.png)

> 当前历史记录对应的索引是通过哈希算法得到的。

当历史记录过多的时候，查看日志的时候有**分页效果**（一页展示不下）：

![image-20210301105800960](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301105801.png)

相应操作：

下一页：`空格`

上一页：`b`

到尾页后会显示 `(END)`

退出： `q`

![image-20210301105824689](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301105824.png)

![image-20210301105841258](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301105841.png)

##### **日志展示方式**：

- 方式1：`$ git log`

- 方式2：`$ git log --pretty=oneline`

  ![image-20210301105910233](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301105910.png)

- 方式3：`$ git log --oneline`

  ![image-20210301105930635](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301105930.png)

- 方式4：`git reflog`

  增加了信息：`HEAD@{数字}`

  > 数字的含义：指针回到当前这个历史版本需要走多少步

  ![image-20210301105959269](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301105959.png)

#### reset

前进或后退到历史：

- reset命令：前进或者后退历史版本

  `$ git reset --hard 版本索引`

  ![image-20210301110143722](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301110143.png)

  ![image-20210301110155926](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301110155.png)

  ![image-20210301110257908](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301110257.png)

  ![image-20210301110242381](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301110242.png)

  #### 版本回退或恢复

  

  ![image-20210301103621960](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301103632.png)

  1. hard参数

     `$ git reset --hard [索引]`

     本地库的指针移动的同时，重置暂存区和工作区

     ![image-20210301103632166](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301103632.png)

  2. mixed参数

     `$ git reset --mixed [索引]`

     本地库的指针移动的同时，重置暂存区，但是工作区不动
  
     ![image-20210301103642870](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301103642.png)
  
  3. soft参数
  
     `$ git reset --soft [索引]`
  
     本地库的指针移动的时候，暂存区、工作区都不动
  
     ![image-20210301103652561](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301103652.png)
  
  > 总结：以后用的多的是第一种 `hard` 参数

> 复制：鼠标在终端拖动选中完成复制
>
> 粘贴：右键 -> Paste

#### rm

删除/找回文件：

`$ rm 文件名`

`$ rm Test.txt`

![image-20210301111437218](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301111437.png)

将删除操作同步到暂存区和本地库：

![image-20210301111539786](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301111539.png)

查看日志：

![image-20210301111629581](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301111629.png)

找回**本地库**中删除的文件（**实际上就是将历史版本切换到删除文件前的那个版本**）

![image-20210301111736704](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301111736.png)

找回**暂存区**删除的文件：

删除工作区数据并同步到暂存区：

![image-20210301111807884](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301111807.png)

恢复暂存区中的数据：

![image-20210301103749190](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301103749.png)

#### 查看工作区与暂存区、暂存区与本地仓库的差异：

`$ git diff 文件名`：将工作区中的文件和暂存区中的文件进行对比

更改工作区中 Test.txt 中的内容：

![image-20210301112334591](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301112334.png)

导致工作区和暂存区不一致，对比：

![image-20210301112717030](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301112717.png)

`$ git diff`：比较工作区中和暂存区中所有文件的差异

![image-20210301112813479](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301112813.png)

`$ git diff 历史版本 文件名`：比较暂存区和工作区中的内容

![image-20210301112912372](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301112912.png)

![image-20210301103838903](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301103838.png)

## 八、分支

什么是分支？

![image-20210301113204264](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210301113204264.png)

在版本控制过程中，使用多条线同时推进多个任务。这里面说的多条线就是多个分支。

图示：

![image-20210301103850004](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301103850.png)

分支的好处：同时多个分支可以**并行开发**，互相不耽误，互相不影响，提高开发效率。如果有有一个分支功能开发失败，直接删除这个分支就可以，**不会对其他分支产生任何影响**。

#### **操作分支**

1.在工作区创建一个Test2.txt文件，然后提交到暂存区，提交到本地库:

![image-20210301142132349](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301142132.png)

![image-20210301141255312](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301141255.png)

2.查看分支：

`$ git branch -v`

![image-20210301141344569](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301141344.png)

3.创建分支：

`$ git branch 分支名称`

![image-20210301141437899](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301141437.png)

4.切换分支：

`$ git checkout 分支名称`

![image-20210301141513491](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301141513.png)

#### **冲突问题**

1.在主分支上创建一个文件

![image-20210301142335228](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301142335.png)

![image-20210301142458144](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301142458.png)

2.进入`branchSecondary` 分支，增加内容

![image-20210301142653831](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301142653.png)

![image-20210301142646876](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301142646.png)

3.将分支切换为 `master`，查看文件仍为主分支创建的文件

![image-20210301142754122](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301142754.png)

![image-20210301143347553](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301143347.png)

4.然后在主分支下添加内容

![image-20210301143409998](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301143410.png)

![image-20210301143448616](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301143448.png)

5.再次切换到 `branchSecondary` 分支查看

`cat 文件名`：查看文本文件中的内容

![image-20210301143536942](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301143537.png)

##### 分支合并

将` branchSecondary` 分支 合并到 主分支`master`

1. 进入主分支，并将 `branchSecondary`中的内容和主分支内容合并

   `$ git merge 分支名称`

   ![image-20210301143727044](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301143727.png)

   2.查看文件：

   ![image-20210301143901532](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301143901.png)

**什么时候会出现冲突问题？**

 **在同一个文件的同一个位置修改**

##### 解决冲突问题

**解决：**公司内部商议解决，或者自己决定，留下想要的即可。

![image-20210301143917012](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301143917.png)

1. 将工作区的内容添加到暂存区并查看当前状态

   ![image-20210301144048337](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301144048.png)

2. 进行 commit 操作

   ![image-20210301144204467](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301144204.png)

# GitHub

回顾本地库和远程库交互方式;

![image-20210301151708534](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301151708.png)

## 一、创建本地仓库

![image-20210301151835544](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301151835.png)

![image-20210301151941075](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301151941.png)

![image-20210301152050554](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301152050.png)

## 二、创建GitHub远程仓库

1.创建远程库

![image-20210205214202033](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301152121.png)

2.在本地仓库创建远程仓库别名

![image-20210301152323529](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301152323.png)

3.远程仓库的地址：

![image-20210301152445616](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301152445.png)

4.点击进去！

![image-20210301152547203](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301152547.png)

远程仓库地址比较长，每次复制比较麻烦

https://github.com/wuxinyu3366/GitRespTest.git

5.在 Git 本地将地址保存，通过别名访问

`$ git remote -v`：查看别名

![image-20210301152739829](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301152739.png)

`$ git remote add 别名 远程仓库地址`：为远程创库起别名

别名可以安装随意取（在本地为远程库取别名）

![image-20210301152848244](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301152848.png)

![image-20210301152859987](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301152900.png)

碰到远端仓库服务器迁移，或者原来的克隆镜像不再使用，又或者某个参与者不再贡献代码，那么需要移除对应的远端仓库，可以运行 `git remote rm` 命令：

```bash
$ git remote rm paul
$ git remote

```

![image-20210301194235603](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301194235.png)

## 三、本地库&远程库使用

### 推送操作

```
$ git push 远程仓库名/远程仓库别名 要推送的分支名
```

![image-20210205221422777](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301153546.png)

![image-20210301153605973](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301153606.png)

![image-20210301153653958](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301153654.png)

推送成功后，查看远程仓库：

![image-20210301153824449](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301153824.png)



### 克隆操作

1. 找一个新的目录，远程地址复制

   ![image-20210301154121290](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301154121.png)

   ![image-20210301154239751](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301154239.png)

2. 克隆操作

   `$ git clone 远程仓库地址`

   ![image-20210301154338343](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301154338.png)

克隆操作可以帮我们完成：

1. 初始化本地库

2. 将远程库内容完整的克隆到本地库

3. 替我们创建远程仓库别名（进入到GitRespTest目录下）

   ![image-20210301154518308](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301154518.png)

## 四、邀请加入团队push操作

```
$ git push 远程仓库别名 推送分支的名称
```

1. 更新工作区的内容，然后添加到暂存区，又提交到本地库(更新操作)

   ![image-20210301163339726](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301163339.png)

   ![image-20210301163512682](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301163512.png)

2. push内容到远程库中

   ![image-20210301163747208](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301163747.png)

   发现可以直接 `push` 进去，并没有让我录入账号密码或者没有提示错误

   原因：`git` 使用的时候在本地有缓存

   ![image-20210301164142665](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301164142.png)

   删除缓存：

   ![image-20210301164716975](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301164717.png)

   ![image-20210301164311120](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301164311.png)

   ![image-20210301164242132](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301164242.png)

3. 再次重新 `push` ，发现出错了

   ```bash
   remote: Permission to GitHub-anonymousV/Notes.git denied to GitHub-anonymousV/Notes.git
   fatal: unable to access 'https://github.com/GitHub-anonymousV/Notes.git'
   requested URL returned error: 403
   ```

4. 必须要加入团队：登录项目经理的账号，邀请普通成员

   ![image-20210301164415567](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301164415.png)

   ![image-20210301164431907](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301164432.png)

   ![image-20210301164517335](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301164517.png)

   

5. 登录被邀请者的账号，接收邀请：

   ![image-20210301164636973](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301164637.png)

6. 再次提交即可提交成功

   ![image-20210301164854359](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301164854.png)

## 五、远程仓库修改的拉取操作

```
$ git pull 远程仓库名/远程仓库别名 要拉取的分支名
```

1. 拉取操作 `pull` 操作，相当于 `fetch + merge`

   ![image-20210301165012844](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301165012.png)

2. 项目经理先确认远程库内容是否更新了

   ![image-20210301165710990](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301165711.png)

3. 项目经理进行拉取

   1. 先是抓取操作：`fetch`

      ![image-20210301165830419](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301165830.png)

   2. 在抓取操作执行后，只是将远程库的内容下载到本地，但是**工作区中的文件并没有更新**。工作区中还是原先的内容

      ![image-20210301165958854](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301165958.png)

   3. 抓取后可以去远程库中查看内容是否正确

      ![image-20210301170025876](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301170026.png)

   4. 检查内容正确，进行合并操作（合并前应该讲分支切换回来）

      `$ git checkout 分支名称`：切换分支

      ![image-20210301170107468](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301170107.png)

      `$ git merge 远程仓库名/分支名`
      
      ![image-20210301170121377](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301170121.png)

远程仓库的拉取可以直接用 `pull` 命令来完成：

![image-20210301170211883](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301170211.png)

![image-20210301172117393](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301172117.png)

![image-20210301172139295](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301172139.png)

> `fetch+merge`操作 -> 检查正确性，保险
>
> `pull` -> 代码简单

## 六、协同开发合作

#### 冲突产生

- 产生冲突

  1. 第一个程序员创建工作区内容后向远程仓库推送数据

     ![image-20210301172235173](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301172235.png)

     

  2. 第二个程序员修改了工作区的相同内容后向远程仓库推送数据

     先做一个拉取操作：

     ![image-20210301172325415](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301172325.png)

     到这里为止，现在远程合作没有任何问题。|
     
     再次用第二个程序员修改+推送
     
     ![image-20210301172433822](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301172433.png)
     
     ![image-20210301172504305](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301172504.png)
     
     3.第一个程序员修改工作区内容后向远程仓库推送数据
     
     ![image-20210301172638807](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301172638.png)
     
     ![image-20210301172700975](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301172701.png)
     
     ![image-20210301172719578](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301172719.png)
     
     **产生了冲突，推送失败**

  

#### 解决冲突

  在冲突情况下，**先应该拉取下来修改冲突，然后再推送到远程服务器**

  1. 拉取并查看冲突

     ![image-20210301172801080](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301172801.png)

  2. 个人解决冲突（该删的删、该留的留）

     ![image-20210301172813820](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301172813.png)

  3. 解决完冲突后，向服务器推送

     ![image-20210301172846960](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301172847.png)

     **推送**：

     ![image-20210301172942294](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301172942.png)

  4. 冲突解决

     ![image-20210301173400282](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301173400.png)

#### 跨团队合作

![image-20210301173656047](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301173656.png)

1. 得到远程仓库的地址

   ![](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301173908.png)

   ![image-20210301173803562](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301173803.png)

   地址：https://github.com/wuxinyu3366/GitRespTest.git

2. 进行 `fork` 操作

   ![image-20210301173853988](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301173854.png)

   进入GitHub账号后，在浏览器地址栏复制地址：https://github.com/TheAlgorithms/Java.git

   ![image-20210301174006735](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174006.png)

   ![image-20210301174037224](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174037.png)

   ![image-20210301174052157](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174052.png)

3. 然后就可以克隆到本地（小猪），并且进行修改

   ![image-20210301173853988](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174116.png)

   `$ git clone 远程仓库地址`：将远程仓库克隆到本地

   ![image-20210301174146566](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174146.png)

   ![image-20210301174158992](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174159.png)

4. 然后更改数据、添加到暂存区、提交到本地仓库、`push` 到远程仓库

   ![image-20210301173853988](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174246.png)

   ![image-20210301174259495](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174259.png)

   ![image-20210301174334270](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174334.png)

   已经到远程库B了

   ![image-20210301174406465](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174406.png)

5. 进行 `pull request` 操作

   ![image-20210301173853988](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174443.png)

   ![image-20210301174454671](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174454.png)

   ![image-20210301174546106](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174546.png)

   ![image-20210301174608415](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174608.png)

6. 进行审核操作

   ![](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174647.png)

   查看具体提交内容

   ![image-20210301174728832](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174728.png)

   可以互相留言：

   ![image-20210301174813237](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174813.png)

   ![image-20210301174843875](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174843.png)

   查看内容：

   ![image-20210301174946966](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174947.png)

   确定通过以后，进行合并

   ![image-20210301174911474](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301174911.png)

## 七、SSH免密码登录

1. 进入用户的主目录

   `cd ~`：进入用户主目录

   ![image-20210301175057336](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301175057.png)

2. 执行命令，生成一个 `.ssh` 的目录

   `$ ssh-keygen -t rsa -C GitHub 账号对应的邮箱`

   ![image-20210301175214770](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301175214.png)

   > keygen --> key generation
   >
   > C 要大写
   >
   > 后面的邮箱是GitHub注册账号的时候对应的邮箱
   >
   > 输入后 按三次回车使用默认值即可

   发现在 .ssh 目录下有两个文件

   ![image-20210301175314799](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301175314.png)

3. 打开 id.rsa.pub 文件，将里面的内容进行复制操作

   ```
   ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC5nv9pHo0PEkHTf9+yERFz4RG0wFUdi8jzTNLDDCmSL0tq6B/nOSinO99LQPA3v3aCu02O8QWDOWqP+NHmFzPImTZleJv0Lq2U814Me8ezmCIEl92fRGcc9+uDfOL3++w1QYWKEEBiGVlyzIGpRBkku9MeijeH0qYvP2aW8pSEqtNpX+b7NFBHOPF4U2iieZwcQ9a4kWKlCIkTJ7bMny8mhGWbvB2xm5wf7HgSddgQAFugIpjq/SBGruieUki0Qto7dKgXldY96V5ytvODsYydCApQS6LMwYmOW7f7nTv2SSliViQLitODu/gwYkJp18drAmRWalf6oO4gRZHVNXPoBW/QRvZsMRxBW9X5bI7u94LUmZ+j+H9X1sXIN9mjKzhb2M1N1nhTFGv3zv9uU847HqjUUT+k8Ksc/3KV0qRCkKs+PPFeRxrBo8KXcL8ABb7uuyQ9I+obG5whASbirZkHjlsxM9wbEhadXfWVrcxMMwej2Cer19VsCKJIcIBAZ0M= 957904804@qq.com
   
   ```

4. 打开GitHub账号，生成密钥

   ![image-20210301175814217](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301175814.png)

   ![image-20210301175922593](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301175922.png)

   ![image-20210301180048813](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301180048.png)

   ![image-20210301180107040](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301180107.png)

5. 生成密钥以后，就可以正常进行 `push` 操作了

   1. 对 `ssh`远程地址起别名并查看别名

      ![image-20210301193825904](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301193825.png)

      ![image-20210301194107846](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301194107.png)

   2. 创建一个文件，添加到暂存区，提交到本地仓库，然后push到远程仓库（地址用 `ssh` 方式地址）
   
      ![image-20210301195833274](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301195833.png)
   
      ![image-20210301195800846](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301195800.png)
   
      ![image-20210301195907878](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301195907.png)

> SSH方式好处：不需要每次都进行身份验证
>
> 缺陷：只能针对一个账号

## 八、IDEA集成Git

### IDEA集成Git/初始化本地仓库/添加到暂存区/提交到本地库

- IDEA集成Git

![image-20210301200611204](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301200611.png)

![image-20210301200758260](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301200758.png)

- 本地库的初始化操作

![image-20210301200900655](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301200900.png)

本地库初始化完成，生成了 .git 目录

![image-20210301200929756](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301200952.png)

> 进行 `add` 操作即将文件添加到暂存区

- 再模块`Module`进行`add`操作将其添加到暂存区

![image-20210301201114474](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301201114.png)

![image-20210301201210061](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301201210.png)

![image-20210301201315471](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301201315.png)

- 模块`Module`进行`commit`操作，将暂存区中的模块内容添加到本地仓库

![image-20210301201701054](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301201701.png)

![image-20210301201345268](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301201345.png)

![image-20210301201611511](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301201611.png)



在类中修改内容后再次提交

修改内容后，和本地库内容不一样的位置前面会显示绿色：

![image-20210301201821956](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301201822.png)

可以再次进行 `add` 和 `commit` 操作将工作区中修改后的内容同步到本地仓库：

![image-20210301201941893](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301201942.png)

### 使用IDEA拉取和推送资源

因为它们是两个不同的项目，要把两个不同的项目合并，`git`需要添加一句代码，在 `git pull` 之后。这句代码是在 `git 2.9.2` 版本发生的，最新的版本需要添加 `--allow-unrelated-histories` 告诉 `git` 允许不相关的历史合并。

假如我们的源是 `origin`，分支是 `master`，那么我们需要这样写 `$ git pull origin master --allow-unrelated-histories`这个方法只解决因为两个仓库有不同的开始点，也就是两个仓库没有共同的 `commit` 出现的无法提交。如果使用文本的方法还无法提交，需要看一下是不是发生了冲突，解决冲突再提交。

```bash
拉取
$ git pull 远程仓库地址/远程仓库别名 拉取的分支 --allow-unrelated-histories
```

![image-20210301202302547](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301202302.png)

![image-20210301202245869](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301202245.png)

点击i进入编辑模式记录信息/添加备注（添加完 按`Esc` -> 按 `:` -> 输入 `wq`）：

![image-20210301202541032](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301202541.png)

![image-20210301202708007](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301202708.png)

```bash
推送
push`推送：`$ git push -u origin master -f
$ git push -u 远程仓库地址/远程仓库别名 推送到的分支 -f
```

![image-20210301203117670](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301203117.png)

经过 `pull` 和 `push` 操作后，

==远程仓库和本地仓库就可以进行交互了。==

![image-20210301203251797](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301203251.png)

- 在IDEA中进行推送

  ![image-20210301203505927](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301203506.png)

  ![image-20210301203631966](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301203632.png)

  ![image-20210301203726873](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301203727.png)

  ![image-20210301203825272](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301203825.png)

  ![image-20210301203836964](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301203837.png)

  在以后创建的时候可以直接`commit并且push`

  ![image-20210301204012942](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301204013.png)

  **一般在开发中先进行 `pull` 操作，再进行 `push` 操作，不会直接进行 `push` 操作，这是为了防止因冲突出现而导致推送失败。**

  ![image-20210301204254300](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301204254.png)

  

### 使用IDEA克隆远程仓库到本地

以后创建项目时直接创建本地仓库

![image-20210301204523222](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301204523.png)

![image-20210301204828782](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301204828.png)

**克隆到本地后，这个目录即变成了一个本地仓库，又变成了工作空间。**

![image-20210301204934676](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301204934.png)

### 使用IDEA解决冲突及如何避免冲突

在 `push` 后，有冲突时会提示合并操作：

程序员B先将远程仓库克隆下来，修改后，提交修改后项目

![image-20210301205031434](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301205031.png)

远程库被程序员B进行了修改

![image-20210301205134235](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301205134.png)

程序员A也在相同的行数上进行了值的修改

![image-20210301205205058](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301205205.png)

![image-20210301205239913](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301205240.png)

![image-20210301205254459](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301205254.png)

**出现冲突**

![image-20210301205443600](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301205443.png)

解决冲突并成功推送到远程仓库

![image-20210301205432669](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301205432.png)

![image-20210301205354080](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301205354.png)

![image-20210301205419446](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210301205419.png)

如何避免冲突？

- 在团队开发的时候避免在一个文件中改代码
- 在==修改一个文件后，在 `push` 操作推送前，先进行 `pull` 操作拉取，使内容同步进而避免冲突==