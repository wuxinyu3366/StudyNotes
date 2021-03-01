# 1、初识MySQL

JavaEE：企业级Java开发 Web

前端（页面：展示：数据!）

后台 （连接点：连接数据库JDBC,连接前端（控制视图跳转，给前端传递数据））

数据库（存数据，Txt,Excel,Word）

> 只会写代码，学好数据库，基本混饭吃：
>
> 操作系统，数据结构与算法！当一个不错的程序猿！
>
> 离散数学，数字电路，体系结构，编译原理。+实战经验，优秀程序猿



## 1.1为什么学数据库

1、岗位需求

2、现在的世界，大数据时代，得数据者得天下

3、被迫需求：存数据

`4、数据库是所有软件体系中最核心的存在` DBA

5、**数据库是几乎软件体系中最核心的一个存在。**

## 1.2 什么是数据库

数据库：(**DB**,**DataBase**)

**概念** : 长期存放在计算机内,有组织,可共享的大量数据的集合,是一个数据 "仓库"

数据仓库，软件，安装在操作系统之（windows,Linux。mac）上的！SQL,可以存储大量的数据，500万!

**作用** : 存储数据,并能安全管理数据(如:增删改查等),减少冗余...

## 1.3 数据库分类

关系型数据库：(SQL)

- MySQL, Oracle, sql Server, DB2, SQLite
- 通过表和表之间，行和列之间的关系进行数据的存储     （学员信息表、考勤表）

非关系型数据库：(NoSQL) Not Only SQL

- Redis, MongDB
- 非关系型数据库，对象存储，通过对象自身的属性来决定。

**==DBMS(数据库管理系统)== **

- 数据库的管理软件，科学有效的管理我们的数据，维护和获取
- MySQL ，数据管理系统！

![image-20210120110629169](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120110629.png)

## 1.4 MySQL简介

MySQL是一个**[关系型数据库管理系统](https://baike.baidu.com/item/关系型数据库管理系统/696511)**

前世： 瑞典MySQL AB 公司

今身： 属于 [Oracle](https://baike.baidu.com/item/Oracle) 旗下产品

MySQL是最好的 [RDBMS](https://baike.baidu.com/item/RDBMS/1048260) (Relational Database Management System，关系数据库管理系统) 应用软件之一。

开源的数据库软件

体积小，速度快，总体拥有成本低，招人成本比较低。

中小型网站，或者大型网站，集群

官网： https://www.mysql.com/

## 1.5 安装MySQL

> 安装步骤

1、下载后得到zip压缩包.

2、解压到自己想要安装到的目录，本人解压到的是D:\Programming software\Environment\mysql-5.7.33

3、添加环境变量：我的电脑->属性->高级->环境变量

```php
选择PATH,在其后面添加: 你的mysql 安装文件下面的bin文件夹
```

4、编辑 my.ini 文件 ,注意替换路径位置

```ini
[mysqld]
basedir=D:\Programming software\Environment\mysql-5.7.33\
datadir=D:\Programming software\Environment\mysql-5.7.33\data\
port=3306
skip-grant-tables
```

5、启动管理员模式下的CMD，并将路径切换至mysql下的bin目录，然后输入mysqld –install (安装mysql)

6、再输入  mysqld --initialize-insecure --user=mysql 初始化数据文件

7、然后再次启动mysql 然后用命令 mysql –u root –p 进入mysql管理界面（密码可为空）

8、进入界面后更改root密码

```bash
update mysql.user set authentication_string=password('123456') where user='root' and Host = 'localhost';
```

9、刷新权限

```bash
flush privileges;
```

10、修改 my.ini文件删除最后一句skip-grant-tables

11、重启mysql即可正常使用

```bash
net stop mysql
net start mysql
```

12、连接上测试出现以下结果就安装好了

![img](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120123002.png)

一步步去做 , 理论上是没有任何问题的 .

如果您以前装过,现在需要重装,一定要将环境清理干净 .

好了,到这里大家都装好了,因为刚接触,所以我们先不学习命令.

这里给大家推荐一个工具 : **SQLyog** .

即便有了可视化工具,可是基本的DOS命名大家还是要记住!

## 1.6 安装SQLyog

![image-20210120162343624](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120162343.png)

![image-20210120162300981](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120162301.png)

==每一个sqlyog的执行操作，本质就是对应了一个sql，可以在软件的历史记录中查看==

![image-20210120162231978](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120162232.png)

![image-20210120162905388](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120162905.png)

## 1.7连接数据库

命令行连接！

```sql
mysql -u root -p123456 --连接数据库

update mysql.user set authentication_string=password('123456') where user='root' and Host='localhost';  --修改密码

flush privileges;--刷新权限

--------------------------------------------------
--所有语句使用;结尾--


show databases;--查看所有的数据库

mysql> use school--切换数据库， use 数据库名
Database changed

--

show tables;--查看数据库中所有的表
describe student;--显示数据库中指定的表的信息
create database westos;--创建一个数据库

exit;--退出连接

--单行注释（sql本来注释）
/*
多行注释
*/
```

![image-20210120165248623](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120165248.png)

# 2、操作数据库

操作数据库----->操作数据库中的表----->操作数据库中表的数据

**MySQL关键字不区分大小写**

## 2.1操作数据库

1.创建数据库

```sql
CREATE DATABASE [IF NOT EXISTS] westos;
```

2.删除数据库

```sql
DROP DATABASE [IF EXISTS] westos
```

3.使用数据库

```sql
--  tab上面的 ``,如果你的表名或者字段名是一个特殊字符，需要带``

USE 'school'
```

4.产看数据库

```sql
SHOW DATABASES   --查看所有数据库
```



对比：

![image-20210120164413759](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120164413.png)

属于DDL的一种，语法 :

```sql
create table [if not exists] `表名`(
    '字段名1' 列类型 [属性][索引][注释],
    '字段名2' 列类型 [属性][索引][注释],
    #...
    '字段名n' 列类型 [属性][索引][注释]
)[表类型][表字符集][注释];
```

**说明 :** 反引号用于区别MySQL保留字与普通字符而引入的 (键盘esc下面的键).

## 2.2数据库的列类型

> 数值

![image-20210120165419816](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120165419.png)

- tinyint 	  	十分小的数据                  1个字节
- smallint         较小的数据                     2个字节
- mediumint    中等大小                        3个字节
- **int                   标准的整数                    4个字节（常用）**
- bigint              较大的数据                     8个字节
- float                浮点数                            4个字节
- double            浮点数                            8个字节 （精度问题）
- decimal           字符串形式的浮点数,金融计算的时候，一般用

> 字符串

![image-20210120165814030](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120165814.png)

- char                字符串固定大小               0-255
- **varchar         可变字符串                        0-65535**（常用）
- tinytext           微型文本                           2^8-1
- **text             文本串 2^16-1**                     (保存大文本)

> 时间日期

![image-20210120165449646](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122183652.png)

java.util.Date

- date YYYY-MM-DD，日期
- time HH:mm:ss 时间格式
- **datetime YYYY-MM-DD HH:mm:ss 最常用的时间格式**
- **timestamp 时间戳 1970.1.1到现在的毫秒数**
- year 年份表示

> null

- 没有值，未知
- **注意，不要使用null进行运算**，结果为null



## 2.3数据库的字段类型（重点）

> unsigened:

- 无符号的整数
- 声明该列不能声明负数

> zerofill:

- 0填充的
- 10的长度 1 – 0000000001 不足位数用0 填充  
- int(3)     5........005

> 自增：AUTO_INCREMENT

- 通常理解为自增，自动在上一条记录的基础上+1(默认)
- 通常用来设计唯一的主键 index,必须是整数类型
- 可以自定义设置主键自增的起始值和步长
- ![image-20210120195643791](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120195643.png)



> 非空 NULL not Null

- 假设设置为 not null，如何不给他赋值，就会报错
- NULL 如果不填写，默认为NULL



> 默认：DEFAULT

- 设置默认的值！

  性别字段,默认为"男" , 否则为 "女" ; 若无指定该列的值 , 则默认值为"男"的值

  

![image-20210120200009638](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120200009.png)





## 2.4 创建数据库表

```sql
--目标:创建一个schoo1数据库
--创建学生表(列,字段)使用SQL 创建
--学号int 登录密码varchar(20)姓名,性别varchar(2),出生日期(datatime)，家庭住址，emai1--注意点，使用英文()，表的名称和字段尽量使用括起来
-- AUTO_ INCREMENT 自增
--字符串使用单引号括起来!
--所有的语句后面加，(英文的)，最后一个不用加
-- PRIMARY KEY 主键，一般- 一个表只有一个唯一 -的主键!

CREATE DATABASE school
CREATE TABLE IF NOT EXISTS `student` (
`id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
`name` VARCHAR(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
`pwd` VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT '密码',
`sex` VARCHAR(2) NOT NULL DEFAULT '男' COMMENT '性别',
`birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
`address` VARCHAR(100) DEFAULT NULL COMMENT '家庭住址',
`email` VARCHAR(50) DEFAULT NULL COMMENT '邮箱',
PRIMARY KEY (`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8

```

格式

```sql
CREATE TABLE [IF NOT EXISTS] `表名`(
`字段名` 列类型[属性][索引][注释],
`字段名` 列类型[属性][索引][注释],
...
`字段名` 列类型[属性][索引][注释]
)[表类型][表的字符集设置][注释]
```

常用命令

```sql
-- 查看数据库的定义（语句）
SHOW CREATE DATABASE school;
-- 查看数据表的定义（语句）
SHOW CREATE TABLE student;
-- 显示表结构
DESC student;  -- 设置严格检查模式(不能容错了)SET sql_mode='STRICT_TRANS_TABLES';
```



## 2.5数据表的类型

```sql
-- 关于数据库引擎
/*
INNODB 默认使用
MYISAM 早些年使用

*/

```

|              | MYISAM | INNODB                 |
| ------------ | ------ | ---------------------- |
| 事务支持     | 不支持 | 支持                   |
| 数据行锁定   | 不支持 | 支持                   |
| 外键约束     | 不支持 | 支持                   |
| 全文索引     | 支持   | 不支持                 |
| 表空间的大小 | 较小   | 较大，约为MYISAM的两倍 |

常规使用操作：

- MYISAM 节约空间，速度较快，
- INNODB 安全性高，事务处理，多表多用户操作

> 在物理空间存在的位置

所有的数据库文件都存在data目录下，一个文件夹就对应一个数据库

本质还是文件的存储! (特定的格式)

MySQL 引擎在物理文件上的区别

- innoDB 在数据库表中，只有一个*.frm文件，以及上级目录下的ibdata1文件

- ![image-20210120201226381](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120201226.png)

- MYISAM 对应的文件
  - *.frm - 表结构的定义文件
  - *. MYD -数据文件
  - *.MYI 索引文件
  - ![image-20210120201208408](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210120201208.png)
  
  

> 设置数据库字符集编码

```sql
CHARTSET=UTF8
```

不设置的话，会是mysql默认的字符集编码-（不支持中文）

可以在my.ini中配置默认的编码(但是不建议使用，换机器使用sql语句会出问题)

```sql
character-set-server=utf8
```

## 2.6修改删除表

> 修改

```sql
-- 修改表名 ALTER TABLE 旧表名 AS 新表名
ALTER TABLE student RENAME  AS student1

-- 增加表的字段 ALTER TABLE 表名 ADD 字段名 列属性
ALTER TABLE student1 ADD age INT(11)

-- 修改表的字段（重命名，修改约束）
ALTER TABLE student1 MODIFY age VARCHAR(11)  -- 修改约束
ALTER TABLE student1 CHANGE age age1 INT(1)  -- 字段重命名

-- 删除表的字段
ALTER TABLE student1 DROP age1

```

> 删除

```sql
-- 删除表
DROP TABLE IF EXISTS student1

```

==**所有的创建和删除操作尽量加上判断，以免报错**==

注意点：

- `` 字段名，使用这个包裹
- 注释 – /**/
- sql 关键字大小写不敏感，建议写小写
- 所有的符号全部用英文

# 3、MySQL数据管理

## 3.1外键（了解）

![image-20210121120101100](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210121120108.png)

> 方式一：在创建表的时候，增加约束（麻烦，比较复杂）
>
> ```sql
> CREATE TABLE `grade`(
> `gradeid` INT(10) NOT NULL AUTO_INCREMENT COMMENT '年级id',
> `gradename` VARCHAR(50) NOT NULL COMMENT '年级名称',
> PRIMARY KEY (`gradeid`)
> )ENGINE=INNODB DEFAULT CHARSET=utf8
> 
> -- 学生表的 gradeid 字段 要去引用年级表的gradeid
> -- 定义外键KEY
> -- 给这个外键添加约束（执行引用） references 引用
> CREATE TABLE IF NOT EXISTS `student` (
> `id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
> `name` VARCHAR(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
> `pwd` VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT '密码',
> `sex` VARCHAR(2) NOT NULL DEFAULT '男' COMMENT '性别',
> `birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
> `gradeid` INT(10) NOT NULL COMMENT '学生年级',
> `address` VARCHAR(100) DEFAULT NULL COMMENT '家庭住址',
> `email` VARCHAR(50) DEFAULT NULL COMMENT '邮箱',
> PRIMARY KEY (`id`),
> KEY `FK_gardeid` (`gradeid`),
> CONSTRAINT `FK_gardeid` FOREIGN KEY (`gradeid`) REFERENCES `grade` (gradeid)
> )ENGINE=INNODB DEFAULT CHARSET=utf8
> ```

删除有外键关系的表的时候，必须先删除引用的表（从表），再删除被引用的表（主表）

> 方式二： 创建表成功后添加外键

```sql
CREATE TABLE `grade`(
`gradeid` INT(10) NOT NULL AUTO_INCREMENT COMMENT '年级id',
`gradename` VARCHAR(50) NOT NULL COMMENT '年级名称',
PRIMARY KEY (`gradeid`)
)ENGINE=INNODB DEFAULT CHARSET=utf8

-- 学生表的 gradeid 字段 要去引用年级表的gradeid
-- 定义外键KEY
-- 给这个外键添加约束（执行引用） references 引用
CREATE TABLE IF NOT EXISTS `student` (
`id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
`name` VARCHAR(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
`pwd` VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT '密码',
`sex` VARCHAR(2) NOT NULL DEFAULT '男' COMMENT '性别',
`birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
`gradeid` INT(10) NOT NULL COMMENT '学生年级',
`address` VARCHAR(100) DEFAULT NULL COMMENT '家庭住址',
`email` VARCHAR(50) DEFAULT NULL COMMENT '邮箱',
PRIMARY KEY (`id`)

)ENGINE=INNODB DEFAULT CHARSET=utf8

-- 创建表的时候没有外键关系
ALTER TABLE `student`
ADD CONSTRAINT `FK_gradeid` FOREIGN KEY (`gradeid`) REFERENCES `grade`(`gradeid`);

-- ALTER TABLE`表`  ADD CONSTRAINT 约束名 FOREIGN KEY（作为外键的列） 引用到哪个表的哪个字段
```

以上的操作都是物理外键，**数据库级别**外键，不建议使用。（避免数据库过多造成困扰）

**最佳实践**

- 数据库就是单纯的表，只用来存数据，只有行（数据）和列（字段）
- 我们想使用多张表的数据，想使用外键（程序去实现）

## 3.2 DML语言（全记住）

数据库意义：数据存储，数据管理

DML语言：数据操作语言

- Insert
- update
- delete

## 3.3添加

> insert

语法：`insert into 表名（[字段一], [字段二]）values('值1'),('值2')`

```sql
-- 插入语句（添加）
-- insert into 表名（[字段一], [字段二]）values('值1'),('值2')

INSERT INTO `grade` (`gradename`) VALUES('大四')

-- 由于主键自增我们可以省略（如何不写表的字段，他会一一匹配）
INSERT INTO `grade` VALUES('大三')
INSERT INTO `grade` (`gradeid`,`gradename`) VALUES ('大三','null')

-- 一般写插入语句，我们一定要数据和字段一一对应。
-- 插入多个字段
INSERT INTO `grade`(`gradename`) VALUES ('大二'),('大一');


INSERT INTO `student`(`name`) VALUES ('张三')
INSERT INTO `student`(`name`,`pwd`,`sex`) VALUES ('张三','aaaaa','男')
-- 插入多个字段
INSERT INTO `student`(`name`,`pwd`,`sex`) 
VALUES ('李四','aaaaa','男'),('王五','23232','女')


```

语法：-- 

```sql
insert into `表名`(`字段一`,`字段二`,`字段三`) VALUES ('值1','值2','值3')
```

注意事项：

1.字段和字段之间用逗号分开

2.字段可以省略，但是后面的值必须一一对应

3.可以同时插入多条数据，VALUES后面的值需要使用，隔开即可

```sql
INSERT INTO `student`(`name`,`pwd`,`sex`) 
VALUES ('李四','aaaaa','男'),('王五','23232','女')

```



## 3.4 修改

> update 命令



语法：`update '谁' set 原来的值=新值 where (条件)`

```sql
-- 修改学员名字

UPDATE `student` SET `name`='囷' WHERE id =1;

-- 不指定条件的情况下，会改动所有表！！！（千万不要执行这样的操作）
UPDATE `student` SET `name`='233'

--修改多个属性，使用逗号隔开
UPDATE `student` 
SET `birthday`=CURRENT_TIME where `name`='李四' AND SEX = '男',
SET `birthday`=CURRENT_TIME where `name`='李四' AND SEX = '女',
SET `birthday`=CURRENT_TIME where `name`='张三' AND SEX = '女'

-- 语法；
-- UPDATE 表名 set column_name,[] = value where 条件

```

条件：where 子句 **运算符** id 等于 某个值，大于某个值，在某个区间内修改

操作符返回布尔值

| 操作符              | 含义                   | 范围      | 结果  |
| ------------------- | ---------------------- | --------- | ----- |
| =                   | 等于                   | 5=6       | false |
| != <>               | 不等于                 | 5！=6     | true  |
| >                   | 大于                   |           |       |
| <                   | 小于                   |           |       |
| >=                  |                        |           |       |
| <=                  |                        |           |       |
| between ... and.... | 在某个范围内，闭合区间 |           |       |
| and                 | 我和你&&               | 5>1and1>2 | false |
| or                  | 我或你\|\|             | 5>1or1>2  | true  |

注意：

- column_name 是数据库的列，带上``
- 条件，是筛选的条件，如果没有指定，则会修改所有的列
- value 是一个具体的值，也可以是一个变量

```sql
UPDATE `student` SET `birthday`=CURRENT_TIME where `name`='李四' AND SEX = '男'
```

- 多个设置的属性之间，使用英文逗号隔开

  

## 3.5 删除

> delete 命令

语法 `delete from 表名 [where 条件]`

```sql
-- 删除数据 (避免这样写，会全部删除)
DELETE FROM `student`

-- 删除指定
DELETE FROM `student` where id= 1

```



> TRUNCATE 命令

作用：完全清空一个数据库，表的结构和索引不会变



> delete 和 TRUNCATE 区别

- 相同点： 都能删除数据，都不会删除表结构
- 不同：
  - TRUNCATE 重新设置自增列 计数器会归零
  - TRUNCATE 不会影响事务

```sql
-- 测试delete 和 truncate 区别

CREATE TABLE `test`(
`id` INT(4) NOT NULL AUTO_INCREMENT,
`coll` VARCHAR(20) NOT NULL,
PRIMARY KEY (`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8

INSERT INTO `test`(`coll`) VALUES('1'),('2'),('3')

DELETE FROM `test` -- 不会影响自增  新增加的数据从多开始

TRUNCATE TABLE `test` -- 自增会归零   新增加的数据从1开始

```

了解即可：`delete删除的问题` 重启数据库，现象

- innoDB 自增列会从1开始（存在内存当中，断电即失）
- MyISAM 继续从上一个自增量开始（存在文件中，不会丢失）

# 4、DQL查询数据（最重点）

```sql
CREATE DATABASE IF NOT EXISTS `school`;
-- 创建一个school数据库
USE `school`;-- 创建学生表
DROP TABLE IF EXISTS `student`;
CREATE TABLE `student`(
	`studentno` INT(4) NOT NULL COMMENT '学号',
    `loginpwd` VARCHAR(20) DEFAULT NULL,
    `studentname` VARCHAR(20) DEFAULT NULL COMMENT '学生姓名',
    `sex` TINYINT(1) DEFAULT NULL COMMENT '性别，0或1',
    `gradeid` INT(11) DEFAULT NULL COMMENT '年级编号',
    `phone` VARCHAR(50) NOT NULL COMMENT '联系电话，允许为空',
    `address` VARCHAR(255) NOT NULL COMMENT '地址，允许为空',
    `borndate` DATETIME DEFAULT NULL COMMENT '出生时间',
    `email` VARCHAR (50) NOT NULL COMMENT '邮箱账号允许为空',
    `identitycard` VARCHAR(18) DEFAULT NULL COMMENT '身份证号',
    PRIMARY KEY (`studentno`),
    UNIQUE KEY `identitycard`(`identitycard`),
    KEY `email` (`email`)
)ENGINE=MYISAM DEFAULT CHARSET=utf8;

-- 创建年级表
DROP TABLE IF EXISTS `grade`;
CREATE TABLE `grade`(
	`gradeid` INT(11) NOT NULL AUTO_INCREMENT COMMENT '年级编号',
  `gradename` VARCHAR(50) NOT NULL COMMENT '年级名称',
    PRIMARY KEY (`gradeid`)
) ENGINE=INNODB AUTO_INCREMENT = 6 DEFAULT CHARSET = utf8;

-- 创建科目表
DROP TABLE IF EXISTS `subject`;
CREATE TABLE `subject`(
	`subjectno`INT(11) NOT NULL AUTO_INCREMENT COMMENT '课程编号',
    `subjectname` VARCHAR(50) DEFAULT NULL COMMENT '课程名称',
    `classhour` INT(4) DEFAULT NULL COMMENT '学时',
    `gradeid` INT(4) DEFAULT NULL COMMENT '年级编号',
    PRIMARY KEY (`subjectno`)
)ENGINE = INNODB AUTO_INCREMENT = 19 DEFAULT CHARSET = utf8;

-- 创建成绩表
DROP TABLE IF EXISTS `result`;
CREATE TABLE `result`(
	`studentno` INT(4) NOT NULL COMMENT '学号',
    `subjectno` INT(4) NOT NULL COMMENT '课程编号',
    `examdate` DATETIME NOT NULL COMMENT '考试日期',
    `studentresult` INT (4) NOT NULL COMMENT '考试成绩',
    KEY `subjectno` (`subjectno`)
)ENGINE = INNODB DEFAULT CHARSET = utf8;



-- 插入学生数据 其余自行添加 这里只添加了2行
INSERT INTO `student` (`studentno`,`loginpwd`,`studentname`,`sex`,`gradeid`,`phone`,`address`,`borndate`,`email`,`identitycard`)
VALUES
(1000,'123456','张伟',0,2,'13800001234','北京朝阳','1980-1-1','text123@qq.com','123456198001011234'),
(1001,'123456','赵强',1,3,'13800002222','广东深圳','1990-1-1','text111@qq.com','123456199001011233');

-- 插入成绩数据  这里仅插入了一组，其余自行添加
INSERT INTO `result`(`studentno`,`subjectno`,`examdate`,`studentresult`)
VALUES
(1000,1,'2013-11-11 16:00:00',85),
(1000,2,'2013-11-12 16:00:00',70),
(1000,3,'2013-11-11 09:00:00',68),
(1000,4,'2013-11-13 16:00:00',98),
(1000,5,'2013-11-14 16:00:00',58);

-- 插入年级数据
INSERT INTO `grade` (`gradeid`,`gradename`) VALUES(1,'大一'),(2,'大二'),(3,'大三'),(4,'大四'),(5,'预科班');


-- 插入科目数据
INSERT INTO `subject`(`subjectno`,`subjectname`,`classhour`,`gradeid`)VALUES
(1,'高等数学-1',110,1),
(2,'高等数学-2',110,2),
(3,'高等数学-3',100,3),
(4,'高等数学-4',130,4),
(5,'C语言-1',110,1),
(6,'C语言-2',110,2),
(7,'C语言-3',100,3),
(8,'C语言-4',130,4),
(9,'Java程序设计-1',110,1),
(10,'Java程序设计-2',110,2),
(11,'Java程序设计-3',100,3),
(12,'Java程序设计-4',130,4),
(13,'数据库结构-1',110,1),
(14,'数据库结构-2',110,2),
(15,'数据库结构-3',100,3),
(16,'数据库结构-4',130,4),
(17,'C#基础',130,1);
```



## 4.1DQL

(Data Query Language) :数据查询语言

- 所有的查询操作都用它 Select
- 简单的查询，复杂的查询它都能做
- **数据库中最核心的语言**
- 使用频率最高的语言

> SELECT 语法

```sql
SELECT [ALL | DISTINCT]
{* | table.* | [table.field1[as alias1][,table.field2[as alias2]][,...]]}
FROM table_name [as table_alias]
    [left | right | inner join table_name2]  -- 联合查询
    [WHERE ...]  -- 指定结果需满足的条件
    [GROUP BY ...]  -- 指定结果按照哪几个字段来分组
    [HAVING]  -- 过滤分组的记录必须满足的次要条件
    [ORDER BY ...]  -- 指定查询记录按一个或多个条件排序
    [LIMIT {[offset,]row_count | row_countOFFSET offset}];
    --  指定查询的记录从哪条至哪条

```

注意 : [ ] 括号代表可选的 , { }括号代表必选得

## 4.2指定查询字段

```sql
-- 查询  SELECT 字段 FROM 表

-- 查询指定字段  such as
SELECT `StudentNo`,`StudentName` FROM student

-- 别名，给结果起一个名字 AS   可以给字段起别名 也可以给表起别名
SELECT `StudentNo` AS 学号,`StudentName`AS 学生姓名 FROM student AS S

-- 函数 Concat(a,b)
SELECT CONCAT('姓名：',StudentName) AS 新名字 FROM student

```

![image-20210121174938754](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210121174938.png)

语法： `SELECT 字段 ... FROM 表`

有时候，列名字不是那么见名知意。我们**起别名** AS 字段名 AS 别名 表名 AS 别名



> 去重 DISTINCE

作用：去除select语句查询出来的结果中重复的语句，重复的语句只显示一条

```sql
-- 查询一下有哪些同学参加了考试，成绩
SELECT * FROM result -- 查询全部的考试成绩
-- 查询有哪些同学参加了考试(从成绩表中得到学号即可)
SELECT `studentNo` FROM result 

-- 发现重复数据，去重
SELECT DISTINCT `studentNo` FROM result 

```



> 数据库的列（表达式）

```sql
SELECT VERSION()  --查询系统版本（函数）
SELECT 100*3-1 AS 计算结果 -- 用来计算（表达式）
SELECT @@auto_increment_increment --查询自增的步长（变量）

-- 学员考试成绩+1 分 查看
SELECT `StudentNo`,`StudentResult`+1 AS '提分后' FROM result


```



数据库中的表达式： 文本值，列，Null , 函数，计算表达式，系统变量…

```sql
 select 表达式 from 表
```



## 4.3where 条件子句

作用：检索数据中==符合条件==的值

搜索的条件由一个或多个表达式组成！ 结果  **布尔值**

> 逻辑运算符

| 运算符  | 语法          | 结果   |
| ------- | ------------- | ------ |
| and &&  | a and b a&&b  | 逻辑与 |
| or \|\| | a or b a\|\|b | 逻辑或 |
| Not !=  | not a !a      | 逻辑非 |

**尽量使用英文**

```sql
-- 查询考试成绩在95分到100分之间
-- and &&
SELECT `StduentNo`,`StudentResult` FROM result
WHERE StudentResult >=95 AND StudentResult<=100

SELECT `StduentNo`,`StudentResult` FROM result
WHERE StudentResult >=95 && StudentResult<=100

-- 模糊查询（区间）
SELECT `StduentNo`,`StudentResult` FROM result
WHERE StudentResult BETWEEN 95 AND 100

-- 除了1000号学生之外的同学成绩
-- !=  not
SELECT `StduentNo`,`StudentResult` FROM result
WHERE  StudentNo != 1000

SELECT `StduentNo`,`StudentResult` FROM result
WHERE NOT StudentNo = 1000

```



> 模糊查询：比较运算符

| 运算符      | 语法              | 描述                                  |
| ----------- | ----------------- | ------------------------------------- |
| I S NULL    | a is null         | 如果操作符为null 结果为真             |
| IS NOT NULL | a is not null     | 如果操作符为not null 结果为真         |
| BETWEEN     | a between b and c | 若a在b 和c之间则为真                  |
| **LIKE**    | a like b          | SQL匹配，如果a 匹配到b 则为真         |
| **IN**      | a in (a1,a2,a3…)  | 假设a 在 a1,a2,a3其中的某一个中，为真 |

```sql
--  查询姓刘的同学
-- like结合 %（代表0到任意字符）  _(一个字符)
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentName LIKE '刘%';

-- 查询姓刘的同学，名字后只有一个字
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentName LIKE '刘_';

-- 查询姓刘的同学，名字后只有两个字
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentName LIKE '刘__';

-- 查询名字中间有嘉字的同学 %嘉%
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentName LIKE '%嘉%';



===================IN(具体的一个或者多个值)===========================
-- 查询1001 1002 1003 学员信息
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentNo = 1001
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentNo = 1002
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentNo = 1003

SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentNo IN (1001,1002,1003);

-- 查询在安徽或河南洛阳的学生
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE `Address` IN('安徽','河南洛阳');

-- 查询在北京的学生
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE `Address` IN('北京',.....);


===================NULL NOT NULL===================================
-- 查询地址为空的学生 null ''
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE address='' OR address IS NULL

-- 查询有出生日期的同学  不为空
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE `BornDate` IS NOT NULL;

-- 查询没有出生日期的同学  为空
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE `BornDate` IS  NULL;
```

## 4.4 联表查询

> JOIN 对比

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210121182716.png)

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210121182719.png)

```sql
======================联表查询 join ==============================
-- 查询参加考试的同学 （学号，姓名，考试编号，分数）

SELECT * FROM student 
SELECT * FROM result

/*
1. 分析需求，分析查询的字段来自哪些表
2.确定使用哪种连接查询？7种
确定交叉点（这两个表中哪个数据是相同的）
判断的条件： 学生表中 studentNo = 成绩表中 studentNo 

*/

-- JION（链接的表） ON （判断的条件）连接查询
--           where          等值查询
SELECT s.studentNo,studentName,SubjectNo,StudentResult
FROM student AS s
INNER JOIN result AS r
WHERE s.studentNo=r.studentNo

--Right Join
SELECT s.studentNo,studentName,SubjectNo,StudentResult
FROM student AS s
RIGHT JOIN result AS r
ON s.studentNo = r.studentNo

--LEFT Join
SELECT s.studentNo,studentName,SubjectNo,StudentResult
FROM student AS s
LEFT JOIN result AS r
ON s.studentNo = r.studentNo

```

| 操作       | 描述                                         |
| ---------- | -------------------------------------------- |
| Inner join | 如果表中至少有一个匹配，就返回行             |
| left join  | 即使左表中没有匹配，也会从左表中返回所有的值 |
| right jion | 即使右表中没有匹配，也会从右表中返回所有的值 |

```sql
-- 查询缺考的同学
SELECT s.studentNo,studentName,SubjectNo,StudentResult
FROM student AS s
LEFT JOIN result AS r
ON s.studentNo = r.studentNo
WHERE StudentResult IS NULL

-- 查询了参加考试同学的信息：学号：学生姓名：科目名：分数
SELECT s.`studentNo`,`studentName`,`SubjectName`,`studentResult`
FROM student s
RIGHT JOIN result r
ON r.studentNo=s.studentNo
INNER JOIN `subject` sub
ON r.SubjectNo=sub.SubjectNo

-- 我要查询哪些数据 SELECT ....
-- 从哪几个表中查 FROM 表 xxx JOIN 连接的表 ON 交叉条件
-- 假设存在一中多张表查询，先查询两章表，然后再慢慢增加

--FROM a LEFT JOIN b   左为准
--FROM a RIGHT JOIN b	  右为准
--FROM a INNER JOIN b	  交叉为基准



-- 查询学员及所属的年级(学号,学生姓名,年级名)
SELECT studentno AS 学号,studentname AS 学生姓名,gradename AS 年级名称
FROM student s
INNER JOIN grade g
ON s.`GradeId` = g.`GradeID`
 
-- 查询科目及所属的年级(科目名称,年级名称)
SELECT subjectname AS 科目名称,gradename AS 年级名称
FROM SUBJECT sub
INNER JOIN grade g
ON sub.gradeid = g.gradeid
 
-- 查询 数据库结构-1 的所有考试结果(学号 学生姓名 科目名称 成绩)
SELECT s.studentno,studentname,subjectname,StudentResult
FROM student s
INNER JOIN result r
ON r.studentno = s.studentno
INNER JOIN `subject` sub
ON r.subjectno = sub.subjectno
WHERE subjectname='数据库结构-1'
```



> 自连接

自己的表跟自己的表连接，核心：**一张表拆为两张一样的表**

```sql
CREATE TABLE `school`.`category`( `categoryid` INT(3) NOT NULL COMMENT 'id', `pid` INT(3) NOT NULL COMMENT '父id 没有父则为1', `categoryname` VARCHAR(10) NOT NULL COMMENT '种类名字', PRIMARY KEY (`categoryid`) ) ENGINE=INNODB CHARSET=utf8 COLLATE=utf8_general_ci; 

INSERT INTO `school`.`category` (`categoryid`, `pid`, `categoryname`) VALUES ('2', '1', '信息技术');
insert into `school`.`CATEGOrY` (`categoryid`, `pid`, `categoryname`) values ('3', '1', '软件开发');
insert into `school`.`category` (`categoryid`, `PId`, `categoryname`) values ('5', '1', '美术设计');
insert iNTO `School`.`category` (`categoryid`, `pid`, `categorynamE`) VAlUES ('4', '3', '数据库'); 
insert into `school`.`category` (`CATEgoryid`, `pid`, `categoryname`) values ('8', '2', '办公信息');
insert into `school`.`category` (`categoryid`, `pid`, `CAtegoryname`) values ('6', '3', 'web开发'); 
inserT INTO `SCHool`.`category` (`categoryid`, `pid`, `categoryname`) valueS ('7', '5', 'ps技术');
```



父类

| categoryid | categoryName |
| ---------- | ------------ |
| 2          | 信息技术     |
| 3          | 软件开发     |
| 5          | 美术设计     |
|            |              |

子类（pid是指parent id ）

例如  数据库（4）是 软件开发（3）主科目下的科目

| pid  | categoryid | categoryName |
| ---- | ---------- | ------------ |
| 3    | 4          | 数据库       |
| 2    | 8          | 办公信息     |
| 3    | 6          | web开发      |
| 5    | 7          | ps技术       |



操作：查询父类对应子类关系（类似于  先修课）

| 父类     | 子类     |
| -------- | -------- |
| 信息技术 | 办公信息 |
| 软件开发 | 数据库   |
| 软件开发 | web开发  |
| 美术设计 | ps技术   |

```sql
-- 查询父子信息

SELECT a.`categoryname` AS `父栏目`,b.`categoryname` AS `子栏目`
FROM `category` AS a,`category` AS b
WHERE a.`categoryid`=b.`pid`

-- 查询学员所属的年级（学号，学生的姓名，年级）
SELECT 	studentNo,studentName,gradeName
FROM student s
INNER JOIN `grade` g
ON s.`GradeId`=g.`GradeId`

```

![image-20210121194433785](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210121194433.png)

![image-20210121194621125](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210121194621.png)

## 4.5分页和排序

```sql
============================分页 limit 和排序order by=================

-- 排序：  升序ASC  降序  DESC
SELECT  xx
FROM xx
JOIN xx
WHERE  xx
ORDER BY  xx
ASC   ||  DESC

```

> 分页

```sql
/*============== 分页 ================
语法 : SELECT * FROM table LIMIT [offset,] rows | rows OFFSET offset
好处 : (用户体验,网络传输,查询压力)
语法 ：limit  起始的序号  单页面显示条数
推导:
    第一页 : limit 0,5
    第二页 : limit 5,5
    第三页 : limit 10,5
    ......
    第N页 : limit (pageNo-1)*pageSzie,pageSzie
    [pageNo:页码,pageSize:单页面显示条数]
    [n:当前页]
    [数据总数/页面大小=总页数]
    
*/
 
-- 每页显示5条数据
SELECT s.studentno,studentname,subjectname,StudentResult
FROM student s
INNER JOIN result r
ON r.studentno = s.studentno
INNER JOIN `subject` sub
ON r.subjectno = sub.subjectno
WHERE subjectname='数据库结构-1'
ORDER BY StudentResult DESC , studentno
LIMIT 0,5
 
-- 查询 JAVA第一学年 课程成绩前10名并且分数大于80的学生信息(学号,姓名,课程名,分数)
SELECT s.studentno,studentname,subjectname,StudentResult
FROM student s
INNER JOIN result r
ON r.studentno = s.studentno
INNER JOIN `subject` sub
ON r.subjectno = sub.subjectno
WHERE subjectname='JAVA第一学年'
ORDER BY StudentResult DESC
LIMIT 0,10

```



语法 `limit(查询起始下标，pagesize)`



> 排序

```sql
/*============== 排序 ================
语法 : ORDER BY
    ORDER BY 语句用于根据指定的列对结果集进行排序。
    ORDER BY 语句默认按照ASC升序对记录进行排序。
    如果您希望按照降序对记录进行排序，可以使用 DESC 关键字。
    
*/
 
-- 查询 数据库结构-1 的所有考试结果(学号 学生姓名 科目名称 成绩)
-- 按成绩降序排序
SELECT s.studentno,studentname,subjectname,StudentResult
FROM student s
INNER JOIN result r
ON r.studentno = s.studentno
INNER JOIN `subject` sub
ON r.subjectno = sub.subjectno
WHERE subjectname='数据库结构-1'
ORDER BY StudentResult DESC

```



## 4.6 子查询

where (这个值是计算出来的)

本质：`在where语句中嵌套一个子查询语句`

```sql

/*============== 子查询 ================
什么是子查询?
    在查询语句中的WHERE条件子句中,又嵌套了另一个查询语句
    嵌套查询可由多个子查询组成,求解的方式是由里及外;
    子查询返回的结果一般都是集合,故而建议使用IN关键字;
*/
-- ===========================where=========================

-- 1.查询 数据库结构-1的所有考试结构（学号，科目编号，成绩） 降序
-- 方式一： 连接查询
SELECT `StudentNo`,r.`SubjectName`,`StudentResult`
FROM `result` r
INNER JOIN `subject` sub
ON r.SubjectNo = sun.SubjectNo
WHERE subjectName = '数据库结构-1'
ORDER BY StudentResult DESC;

-- 方式二：使用子查询(由里及外)
SELECT `StudentNo`,r.`SubjectName`,`StudentResult`
FROM `result`
WHERE StudentNo=(
	SELECT SubjectNo FROM  `subject` 
    WHERE SubjectName = '数据库结构-1'
)
ORDER BY StudentResult DESC;


--原题目：
-- 查询课程为 高等数学-2 且分数不小于80分的同学的学号和姓名
--解法一：
SELECT s.`StudentNo`,`StudentName`
FROM student s
INNER JOIN result r
ON s.StudentNo = r.StudentNo
INNER JOIN `subject` sub
ON r.`SubjectName`='高等数学-2'
WHERE `SubjectaName`='高等数学-2' AND StudentResult >=80


--解法二（分成两步）：
-- 1.分数不少于80分的学生的学号和姓名
SELECT DISTINCT s.`StudentNo`,`StudentName`
FROM student s
INNER JOIN result r
ON r.StudentNo = s.StudentNo
WHERE StudentResult>=80

-- 2.在这个基础上 增加一个科目 ，高等数学-2
SELECT DISTINCT s.`StudentNo`,`StudentName`
FROM student s
INNER JOIN result r
ON r.StudentNo = s.StudentNo
WHERE StudentResult>=80 AND `SubjectNo`=(
    SELECT Subject FROM `subject`
    WHERE SubjectName='高等数学-2'
)

--解法三：
-- 再改造 (由里即外)
SELECT `StudentNo`,`StudentName` FROM student
WHERE StudentNo IN(
SELECT StudentNo result WHERE StudentResult >80 AND SubjectNo =(
SELECT SubjectNo FROM `subject` WHERE `SubjectaName`='高等数学-2'
)
)


/*
练习题目:
    查 C语言-1 的前5名学生的成绩信息(学号,姓名,分数)
    使用子查询,查询郭靖同学所在的年级名称
*/
```

## 4.7 分组

```sql
-- 查询不同课程的平均分，最高分，最低分，平均分大于80
-- 核心：（根据不同的课程分组）

SELECT `SubjectName`,AVG(StudentResult),MAX(StudentResult)
FROM result r
INNER JOIN `Subject` sub
ON r.SubjectNo=sub.SubjectNo

GROUP BY r.SubjectNo -- 通过什么字段来分组
HAVING AVG(StudentResult)>80


```

# 5、MySQL函数

官网：https://dev.mysql.com/doc/refman/5.7/en/sql-function-reference.html

## 5.1 常用函数

```sql
-- 数学运算
 SELECT ABS(-8);  /*绝对值*/
 SELECT CEILING(9.4); /*向上取整*/
 SELECT FLOOR(9.4);   /*向下取整*/
 SELECT RAND();  /*随机数,返回一个0-1之间的随机数*/
 SELECT SIGN(0); /*符号函数: 负数返回-1,正数返回1,0返回0*/

-- 字符串函数
 SELECT CHAR_LENGTH('狂神说坚持就能成功'); /*返回字符串包含的字符数*/
 SELECT CONCAT('我','爱','程序');  /*合并字符串,参数可以有多个*/
 SELECT INSERT('我爱编程helloworld',1,2,'超级热爱');  /*替换字符串,从某个位置开始替换某个长度*/
 SELECT LOWER('KuangShen'); /*小写*/
 SELECT UPPER('KuangShen'); /*大写*/
 SELECT LEFT('hello,world',5);   /*从左边截取*/
 SELECT RIGHT('hello,world',5);  /*从右边截取*/
 SELECT REPLACE('狂神说坚持就能成功','坚持','努力');  /*替换字符串*/
 SELECT SUBSTR('狂神说坚持就能成功',4,6); /*截取字符串,开始和长度*/
 SELECT REVERSE('狂神说坚持就能成功'); /*反转*/
 
 -- 查询姓周的同学,改成邹
 SELECT REPLACE(studentname,'周','邹') AS 新名字
 FROM student WHERE studentname LIKE '周%';
-- 查询姓 周 的同学 ，改成邹
SELECT REPLACE(studentname,'周','邹') FROM student
WHERE studentname LIKE '周%'

-- 时间跟日期函数（记住）
 SELECT CURRENT_DATE();   /*获取当前日期*/
 SELECT CURDATE();   /*获取当前日期*/
 SELECT NOW();   /*获取当前日期和时间*/
 SELECT LOCALTIME();   /*获取本地当前日期和时间*/
 SELECT SYSDATE();   /*获取系统当前日期和时间*/

-- 获取年月日,时分秒
SELECT YEAR(NOW())
SELECT MONTH(NOW())
SELECT DAY(NOW())
SELECT HOUR(NOW())
SELECT MINUTE(NOW())
SELECT SECOND(NOW())

-- 系统信息函数
SELECT SYSTEM_USER()
SELECT USER()					/*用户*/
SELECT VERSION()			/*版本*/

```

## 5.2 聚合函数（常用）

| 函数名称    | 描述   |
| ----------- | ------ |
| **COUNT()** | 计数   |
| SUM()       | 求和   |
| AVG()       | 平均值 |
| MAX()       | 最大值 |
| MIN()       | 最小值 |
| …           |        |



```sql
--========================聚合函数=======================
 /*COUNT:非空的*/
 --想查询表中有多少个记录，就使用这个count（）
 SELECT COUNT(studentname) FROM student;
 SELECT COUNT(*) FROM student;
 SELECT COUNT(1) FROM student;  /*推荐*/
 
 -- 从含义上讲，count(1) 与 count(*) 都表示对全部数据行的查询。
 -- count(字段) 会统计该字段在表中出现的次数，忽略字段为null 的情况。即不统计字段为null 的记录。
 -- count(*) 包括了所有的列，相当于行数，在统计结果的时候，包含字段为null 的记录；
 -- count(1) 用1代表代码行，在统计结果的时候，包含字段为null 的记录 。
 /*
 很多人认为count(1)执行的效率会比count(*)高，原因是count(*)会存在全表扫描，而count(1)可以针对一个字段进行查询。其实不然，count(1)和count(*)都会对全表进行扫描，统计所有记录的条数，包括那些为null的记录，因此，它们的效率可以说是相差无几。而count(字段)则与前两者不同，它会统计该字段不为null的记录条数。
 
 下面它们之间的一些对比：
 
 1）在表没有主键时，count(1)比count(*)快
 2）有主键时，主键作为计算条件，count(主键)效率最高；
 3）若表格只有一个字段，则count(*)效率较高。
 */
 
 SELECT SUM(StudentResult) AS 总和 FROM result;
 SELECT AVG(StudentResult) AS 平均分 FROM result;
 SELECT MAX(StudentResult) AS 最高分 FROM result;
 SELECT MIN(StudentResult) AS 最低分 FROM result;
```



题目：

```sql
-- 查询不同课程的平均分,最高分,最低分
 -- 前提:根据不同的课程进行分组
 
 SELECT subjectname,AVG(studentresult) AS 平均分,MAX(StudentResult) AS 最高分,MIN(StudentResult) AS 最低分
 FROM result AS r
 INNER JOIN `subject` AS s
 ON r.subjectno = s.subjectno
 GROUP BY r.subjectno      --通过什么字段分组
 HAVING 平均分>80;      --分组之后用这个过滤
 
 /*
 where写在group by前面.
 要是放在分组后面的筛选
 要使用HAVING..
 因为having是从前面筛选的字段再筛选，而where是从数据表中的>字段直接进行的筛选的
 */
```



## 5.3 数据库级别MD5加密（拓展）

**一、MD5简介**

MD5即Message-Digest Algorithm 5（**信息-摘要算法5**），用于确保信息传输完整一致。是计算机广泛使用的杂凑算法之一（又译摘要算法、哈希算法），主流编程语言普遍已有MD5实现。将数据（如汉字）运算为另一固定长度值，是杂凑算法的基础原理，MD5的前身有MD2、MD3和MD4。

主要增强算法复杂度**不可逆性**。

MD5不可逆，具体的MD5是一样的

MD5破解原理，背后有一个字典，MD5加密后的值，加密前的值(暴力破解)

**二、实现数据加密**

```sql
--新建一个表 testmd5
CREATE TABLE `testmd5`(
`id` INT(4) NOT NULL,
`name` VARCHAR(20) NOT NULL,
`pwd` VARCHAR(50) NOT NULL,
PRIMARY KEY (`id`)
)ENGINE=INNODB DEFAULT CHARSET=UTF8


-- 明文密码   插入一些数据
INSERT INTO testmd5 VALUES(1,'张三','123456'),(2,'李四','123456'),(3,'王五','123456');

-- 加密
UPDATE testmd5 SET pwd=MD5(pwd) WHERE id =1
UPDATE testmd5 SET pwd=MD5(pwd) 							-- 加密全部
UPDATE testmd5 SET pwd=MD5(pwd) WHERE id !=1  

-- 插入时加密
INSERT INTO testmd5 VALUES(4,'小明',MD5('123456'))
INSERT INTO testmd5 VALUES(5,'红',MD5('123456'))

-- 如何校验，将用户传递过来的密码，进行MD5加密，然后对比加密后的值
SELECT * FROM testmd5 WHERE `name`='红' AND pwd=MD5('123456')

```



## 5.4小结

![image-20210121210936007](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210121210936.png)

```sql
 -- ================ 内置函数 ================
 -- 数值函数
 abs(x)            -- 绝对值 abs(-10.9) = 10
 format(x, d)    -- 格式化千分位数值 format(1234567.456, 2) = 1,234,567.46
 ceil(x)            -- 向上取整 ceil(10.1) = 11
 floor(x)        -- 向下取整 floor (10.1) = 10
 round(x)        -- 四舍五入去整
 mod(m, n)        -- m%n m mod n 求余 10%3=1
 pi()            -- 获得圆周率
 pow(m, n)        -- m^n
 sqrt(x)            -- 算术平方根
 rand()            -- 随机数
 truncate(x, d)    -- 截取d位小数
 
 -- 时间日期函数
 now(), current_timestamp();     -- 当前日期时间
 current_date();                    -- 当前日期
 current_time();                    -- 当前时间
 date('yyyy-mm-dd hh:ii:ss');    -- 获取日期部分
 time('yyyy-mm-dd hh:ii:ss');    -- 获取时间部分
 date_format('yyyy-mm-dd hh:ii:ss', '%d %y %a %d %m %b %j');    -- 格式化时间
 unix_timestamp();                -- 获得unix时间戳
 from_unixtime();                -- 从时间戳获得时间
 
 -- 字符串函数
 length(string)            -- string长度，字节
 char_length(string)        -- string的字符个数
 substring(str, position [,length])        -- 从str的position开始,取length个字符
 replace(str ,search_str ,replace_str)    -- 在str中用replace_str替换search_str
 instr(string ,substring)    -- 返回substring首次在string中出现的位置
 concat(string [,...])    -- 连接字串
 charset(str)            -- 返回字串字符集
 lcase(string)            -- 转换成小写
 left(string, length)    -- 从string2中的左边起取length个字符
 load_file(file_name)    -- 从文件读取内容
 locate(substring, string [,start_position])    -- 同instr,但可指定开始位置
 lpad(string, length, pad)    -- 重复用pad加在string开头,直到字串长度为length
 ltrim(string)            -- 去除前端空格
 repeat(string, count)    -- 重复count次
 rpad(string, length, pad)    --在str后用pad补充,直到长度为length
 rtrim(string)            -- 去除后端空格
 strcmp(string1 ,string2)    -- 逐字符比较两字串大小
 
 -- 聚合函数
 count()
 sum();
 max();
 min();
 avg();
 group_concat()
 
 -- 其他常用函数
 md5();
 default();
```



# 6、事务

## 6.1 什么是事务

**要么都成功，要么都失败**

------

1. SQL执行， A给B转账 A 1000–> 200 B200
2. SQL 执行， B收到A的钱 A800 — B400

------

将一组SQL放在一个批次中执行

> 事务原则 ： ACID原则 原子性，一致性，隔离性，持久性 （脏读，幻读…）

**原子性（Atomicity）**

原子性是指事务是一个不可分割的工作单位，事务中的操作要么都发生，要么都不发生。

**一致性（Consistency）**

事务前后的数据完整性要保持一致

**持久性（Durability）**–事务提交

事务一旦提交就不可逆转，被持久化到数据库中，持久性是指一个事务一旦被提交，它对数据库中数据的改变就是永久性的，接下来即使数据库发生故障也不应该对其有任何影响

**隔离性（Isolated）**

事务的隔离性是多个用户并发访问数据库时，数据库为每一个用户开启的事务，不能被其他事务的操作数据所干扰，多个并发事务之间要相互隔离。事务产生多并发时，互不干扰

详解：



### **原子性（Atomicity）**

针对同一个事务

![image-20210122111908329](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122111908.png)



这个过程包含两个步骤

A： 800 - 200 = 600
B: 200 + 200 = 400

原子性表示，这两个步骤一起成功，或者一起失败，不能只发生其中一个动作

### 一致性（Consistency）

针对一个事务操作前与操作后的状态一致

![image-20210122112029759](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210122112029759.png)

操作前A：800，B：200
操作后A：600，B：400

一致性表示事务完成后，符合逻辑运算

### **持久性（Durability）**

表示事务结束后的数据不随着外界原因导致数据丢失

操作前A：800，B：200
操作后A：600，B：400
如果在操作前（事务还没有提交）服务器宕机或者断电，那么重启数据库以后，数据状态应该为
A：800，B：200
如果在操作后（事务已经提交）服务器宕机或者断电，那么重启数据库以后，数据状态应该为
A：600，B：400

### **隔离性（Isolation）**

针对多个用户同时操作，主要是排除其他事务对本次事务的影响

![image-20210122112146424](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122112146.png)



两个事务同时进行，其中一个事务读取到另外一个事务还没有提交的数据，B

![image-20210122112157522](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122112157.png)





**原子性(Atomic)**

- 整个事务中的所有操作，要么全部完成，要么全部不完成，不可能停滞在中间某个环节。事务在执行过程中发生错误，会被回滚（ROLLBACK）到事务开始前的状态，就像这个事务从来没有执行过一样。

**一致性(Consist)**

- 一个事务可以封装状态改变（除非它是一个只读的）。事务必须始终保持系统处于一致的状态，不管在任何给定的时间并发事务有多少。也就是说：如果事务是并发多个，系统也必须如同串行事务一样操作。其主要特征是保护性和不变性(Preserving an Invariant)，以转账案例为例，假设有五个账户，每个账户余额是100元，那么五个账户总额是500元，如果在这个5个账户之间同时发生多个转账，无论并发多少个，比如在A与B账户之间转账5元，在C与D账户之间转账10元，在B与E之间转账15元，五个账户总额也应该还是500元，这就是保护性和不变性。

**隔离性(Isolated)**

- 隔离状态执行事务，使它们好像是系统在给定时间内执行的唯一操作。如果有两个事务，运行在相同的时间内，执行相同的功能，事务的隔离性将确保每一事务在系统中认为只有该事务在使用系统。这种属性有时称为串行化，为了防止事务操作间的混淆，必须串行化或序列化请求，使得在同一时间仅有一个请求用于同一数据。

**持久性(Durable)**

- 在事务完成以后，该事务对数据库所作的更改便持久的保存在数据库之中，并不会被回滚。



> 隔离产生的问题

### 脏读：

指一个事务读取了另外一个事务未提交的数据。

![image-20210122112437632](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122112437.png)

### 不可重复读：

在一个事务内读取表中的某一行数据，多次读取结果不同。（这个不一定是错误，只是某些场合不对）

![image-20210122112509373](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122112509.png)

### 虚读(幻读)

是指在一个事务内读取到了别的事务插入的数据，导致前后读取不一致。
（一般是行影响，多了一行）

![image-20210122184314059](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122184314.png)

## 6.2执行事务



> 执行事务

```sql
-- 使用set语句来改变自动提交模式
SET autocommit = 0;   /*关闭*/
SET autocommit = 1;   /*开启*/
 
-- 注意:
---  1.MySQL中默认是自动提交
---  2.使用事务时应先关闭自动提交
 
-- 开始一个事务,标记事务的起始点
START TRANSACTION  
 
-- 提交一个事务给数据库
COMMIT
 
-- 将事务回滚,数据回到本次事务的初始状态
ROLLBACK
 
-- 还原MySQL数据库的自动提交
SET autocommit =1;
 
-- 保存点
SAVEPOINT 保存点名称 -- 设置一个事务保存点
ROLLBACK TO SAVEPOINT 保存点名称 -- 回滚到保存点
RELEASE SAVEPOINT 保存点名称 -- 删除保存点
```

![image-20210122113006860](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122113006.png)



> 模拟场景

```sql
CREATE DATABASE shop CHARACTER SET utf8 COLLATE utf8_general_ci
USE shop
CREATE TABLE `account`(
`id` INT(3) NOT NULL AUTO_INCREMENT,
`name` VARCHAR(30) NOT NULL,
`money` DECIMAL(9,2) NOT NULL,
PRIMARY KEY (`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8

INSERT INTO account(`name`,`money`)
VALUES('A',2000),('B',10000)

-- 模拟转账：事务
SET autocommit = 0; -- 关闭自动提交
START TRANSACTION -- 开启事务（一组事务）
UPDATE account SET money = money-500 WHERE `name` = 'A' -- A 转账给B
UPDATE account SET money = money+500 WHERE `name` = 'B' -- B 收到钱

COMMIT ; -- 提交事务，事务就被持久化了，再回滚就没有意义了！
ROLLBACK ; -- 回滚

SET autocommit=1 -- 恢复默认值

```

![image-20210122152654516](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122152654.png)

# 7、索引

> MySQL索引的建立对于MySQL的高效运行是很重要的，索引可以大大提高MySQL的检索速度。

> 索引的作用

- 提高查询速度
- 确保数据的唯一性
- 可以加速表和表之间的连接 , 实现表与表之间的参照完整性
- 使用分组和排序子句进行数据检索时 , 可以显著减少分组和排序的时间
- 全文检索字段进行搜索优化.

## 7.1索引的分类

> 在一个表中，主键索引只能有一个，唯一索引可以有多个

- 主键索引 （PRIMARY KEY）
  
  - 唯一的标识，主键不可重复，只能有一个列作为主键
  
    特点 :
  
    - 最常见的索引类型
    - 确保数据记录的唯一性
    - 确定特定数据记录在数据库中的位置
  
- 唯一索引 （UNIQUE KEY）
  
  - 避免重复的列出现，唯一索引可以重复，多个列都可以标识唯一索引
  
    与主键索引的区别
  
    - 主键索引只能有一个
    - 唯一索引可能有多个
  
  ```sql
  CREATE TABLE `Grade`(
      `GradeID` INT(11) AUTO_INCREMENT PRIMARYKEY,
      `GradeName` VARCHAR(32) NOT NULL UNIQUE
      -- 或 UNIQUE KEY `GradeID` (`GradeID`)
  )
  ```
  
  
  
- 常规索引（KEY / INDEX）
  
  - 默认的，index,key关键字来设置
  
    注意 :
  
    - index 和 key 关键字都可以设置常规索引
    - 应加在查询找条件的字段
    - 不宜添加太多常规索引,影响数据的插入,删除和修改操作
  
  ```sql
  CREATE TABLE `result`(
      -- 省略一些代码
      INDEX/KEY `ind` (`studentNo`,`subjectNo`) -- 创建表时添加
  )
  
  -- 创建后添加
  ALTER TABLE `result` ADD INDEX `ind`(`studentNo`,`subjectNo`);
  ```
  
  
  
- 全文索引（FULLTEXT）
  - 在特点的数据库引擎下才有，MyISAM
  - 快速定位数据

  注意 :

  ​			只能用于MyISAM类型的数据表

  ​			只能用于CHAR , VARCHAR , TEXT数据列类型

  ​			适合大型数据集

```sql
-- 索引的使用
-- 1.在创建表的时候给字段增加索引
-- 2.创建完毕后，增加索引

-- 显示所有的索引信息
SHOW INDEX FROM 表

-- 增加一个索引
ALTER TABLE 表 ADD FULLTEXT INDEX 索引名（字段名）

-- EXPLAIN 分析sql执行状况
EXPLAIN SELECT * FROM student -- 非全文索引


/*
#方法一：创建表时
    　　CREATE TABLE 表名 (
                字段名1  数据类型 [完整性约束条件…],
                字段名2  数据类型 [完整性约束条件…],
                [UNIQUE | FULLTEXT | SPATIAL ]   INDEX | KEY
                [索引名]  (字段名[(长度)]  [ASC |DESC])
                );
#方法二：CREATE在已存在的表上创建索引
        CREATE  [UNIQUE | FULLTEXT | SPATIAL ]  INDEX  索引名
                     ON 表名 (字段名[(长度)]  [ASC |DESC]) ;
#方法三：ALTER TABLE在已存在的表上创建索引
        ALTER TABLE 表名 ADD  [UNIQUE | FULLTEXT | SPATIAL ] INDEX
                             索引名 (字段名[(长度)]  [ASC |DESC]) ;
                            
                            
#删除索引：DROP INDEX 索引名 ON 表名字;
#删除主键索引: ALTER TABLE 表名 DROP PRIMARY KEY;
#显示索引信息: SHOW INDEX FROM student;
*/
 
/*增加全文索引*/
ALTER TABLE `school`.`student` ADD FULLTEXT INDEX `studentname` (`StudentName`);
 
/*EXPLAIN : 分析SQL语句执行性能*/
EXPLAIN SELECT * FROM student WHERE studentno='1000';
 
/*使用全文索引*/
-- 全文搜索通过 MATCH() 函数完成。
-- 搜索字符串作为 against() 的参数被给定。搜索以忽略字母大小写的方式执行。对于表中的每个记录行，MATCH() 返回一个相关性值。即，在搜索字符串与记录行在 MATCH() 列表中指定的列的文本之间的相似性尺度。
EXPLAIN SELECT *FROM student WHERE MATCH(studentname) AGAINST('love');
 
/*
开始之前，先说一下全文索引的版本、存储引擎、数据类型的支持情况
MySQL 5.6 以前的版本，只有 MyISAM 存储引擎支持全文索引；
MySQL 5.6 及以后的版本，MyISAM 和 InnoDB 存储引擎均支持全文索引;
只有字段的数据类型为 char、varchar、text 及其系列才可以建全文索引。
测试或使用全文索引时，要先看一下自己的 MySQL 版本、存储引擎和数据类型是否支持全文索引。
*/
```

## 7.2 测试索引

```sql
CREATE TABLE `app_user` (
`id` BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
`name` VARCHAR(50) DEFAULT '',
`email` VARCHAR(50) NOT NULL,
`phone` VARCHAR(20) DEFAULT '',
`gender` TINYINT(4) UNSIGNED DEFAULT '0',
`password` VARCHAR(100) NOT NULL DEFAULT '',
`age` TINYINT(4) DEFAULT NULL,
`create_time` DATETIME DEFAULT CURRENT_TIMESTAMP,
`update_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
PRIMARY KEY (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8

-- 插入100万数据
DELIMITER $$ --  写函数之前必写
CREATE FUNCTION mock_data()
RETURNS INT 
BEGIN
DECLARE num INT DEFAULT 1000000;
DECLARE i INT DEFAULT 0;

WHILE i<num DO
-- 插入语句
INSERT INTO app_user(`name`,`email`,`phone`,`gender`,`password`,`age`)
VALUE(CONCAT('用户',i),'534240118@qq.com',FLOOR (CONCAT('18',RAND()*9999999)),FLOOR (RAND()*2),
UUID(),FLOOR (RAND()*100));

SET i = i+1;
END WHILE;
RETURN i;

END;

INSERT INTO app_user(`name`,`email`,`phone`,`gender`,`password`,`age`)
VALUE(CONCAT('用户',i),'534240118@qq.com',FLOOR (CONCAT('18',RAND()*9999999)),FLOOR (RAND()*2),
UUID(),FLOOR (RAND()*100))

--执行这句话才能成功
SELECT mock_data();

SELECT * FROM app_user WHERE `name`='用户9999' -- 接近半秒

EXPLAIN SELECT * FROM app_user WHERE `name`='用户9999'  -- 查询99999条记录

-------------------创建索引测试
-- id _ 表名_字段名
-- create index on 字段
CREATE INDEX id_app_user_name ON app_user(`name`); -- 0.001 s

EXPLAIN SELECT * FROM app_user WHERE `name`='用户9999'  -- 查询一条记录


```

索引在小数据的时候，用处不大，但是在大数据的时候，区别十分明显

![image-20210122152334244](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122152334.png)

## 7.3 索引原则

- 索引**不是越多越好**
- 不要对经常变动的数据加索引
- 小数据量的表不需要加索引
- 索引一般加在**常用来查询**的字段上

> 索引的数据结构

Hash 类型的索引

Btree: 默认innodb 的数据结构

阅读： http://blog.codinglabs.org/articles/theory-of-mysql-index.html

# 8、权限管理和备份

## 8.1用户管理

> SQLyog 可视化管理
>
> 使用SQLyog 创建用户，并授予权限演示

![image-20210122153316118](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122153316.png)

> SQL命令操作

用户表：**mysql.user**

本质：对这张表进行，增删改查

```sql
-- 创建用户  CREATE USER 用户名 IDENTIFIED BY '密码'
CREATE USER sanjin IDENTIFIED BY '123456'

-- 修改密码（修改当前密码）
SET PASSWORD = PASSWORD('111111')


-- 修改密码（修改指定用户密码）  --for

SET PASSWORD FOR sanjin = PASSWORD('111111')


-- 重命名  rename user 原名字 to 新名字
RENAME USER sanjin TO sanjin2

-- 用户授权   ALL PRIVILEGES 全部的权限   库，表   to  谁
-- 相比于root权限  ，ALL PRIVILEGES 除了给别人授权 grant ，其他都能干
GRANT ALL PRIVILEGES ON *.* TO sanjin2

-- 查询权限
SHOW GRANTS FOR sanjin2  -- 查看指定用户的权限
SHOW GRANTS FOR root@localhost   --写出主机


-- 撤销权限 REVOKE 哪些权限，在哪个库撤销，给谁撤销  from   谁
REVOKE ALL PRIVILEGES ON *.* FROM sanjin2

-- 删除用户
DROP USER sanjin2

```



> 基本命令

```sql
/* 用户和权限管理 */ ------------------
用户信息表：mysql.user

-- 刷新权限
FLUSH PRIVILEGES

-- 增加用户  CREATE USER kuangshen IDENTIFIED BY '123456'
CREATE USER 用户名 IDENTIFIED BY [PASSWORD] 密码(字符串)
    - 必须拥有mysql数据库的全局CREATE USER权限，或拥有INSERT权限。
    - 只能创建用户，不能赋予权限。
    - 用户名，注意引号：如 'user_name'@'192.168.1.1'
    - 密码也需引号，纯数字密码也要加引号
    - 要在纯文本中指定密码，需忽略PASSWORD关键词。要把密码指定为由PASSWORD()函数返回的混编值，需包含关键字PASSWORD

-- 重命名用户  RENAME USER kuangshen TO kuangshen2
RENAME USER old_user TO new_user

-- 设置密码
SET PASSWORD = PASSWORD('密码')    -- 为当前用户设置密码
SET PASSWORD FOR 用户名 = PASSWORD('密码')    -- 为指定用户设置密码

-- 删除用户  DROP USER kuangshen2
DROP USER 用户名

-- 分配权限/添加用户
GRANT 权限列表 ON 表名 TO 用户名 [IDENTIFIED BY [PASSWORD] 'password']
    - all privileges 表示所有权限
    - *.* 表示所有库的所有表
    - 库名.表名 表示某库下面的某表

-- 查看权限   SHOW GRANTS FOR root@localhost;
SHOW GRANTS FOR 用户名
  
    -- 查看当前用户权限
    SHOW GRANTS; 或 SHOW GRANTS FOR CURRENT_USER; 或 SHOW GRANTS FOR CURRENT_USER();

-- 撤消权限
REVOKE 权限列表 ON 表名 FROM 用户名
REVOKE ALL PRIVILEGES, GRANT OPTION FROM 用户名    -- 撤销所有权限
```

> 权限解释

```sql
-- 权限列表
ALL [PRIVILEGES]    -- 设置除GRANT OPTION之外的所有简单权限
ALTER    -- 允许使用ALTER TABLE
ALTER ROUTINE    -- 更改或取消已存储的子程序
CREATE    -- 允许使用CREATE TABLE
CREATE ROUTINE    -- 创建已存储的子程序
CREATE TEMPORARY TABLES        -- 允许使用CREATE TEMPORARY TABLE
CREATE USER        -- 允许使用CREATE USER, DROP USER, RENAME USER和REVOKE ALL PRIVILEGES。
CREATE VIEW        -- 允许使用CREATE VIEW
DELETE    -- 允许使用DELETE
DROP    -- 允许使用DROP TABLE
EXECUTE        -- 允许用户运行已存储的子程序
FILE    -- 允许使用SELECT...INTO OUTFILE和LOAD DATA INFILE
INDEX     -- 允许使用CREATE INDEX和DROP INDEX
INSERT    -- 允许使用INSERT
LOCK TABLES        -- 允许对您拥有SELECT权限的表使用LOCK TABLES
PROCESS     -- 允许使用SHOW FULL PROCESSLIST
REFERENCES    -- 未被实施
RELOAD    -- 允许使用FLUSH
REPLICATION CLIENT    -- 允许用户询问从属服务器或主服务器的地址
REPLICATION SLAVE    -- 用于复制型从属服务器（从主服务器中读取二进制日志事件）
SELECT    -- 允许使用SELECT
SHOW DATABASES    -- 显示所有数据库
SHOW VIEW    -- 允许使用SHOW CREATE VIEW
SHUTDOWN    -- 允许使用mysqladmin shutdown
SUPER    -- 允许使用CHANGE MASTER, KILL, PURGE MASTER LOGS和SET GLOBAL语句，mysqladmin debug命令；允许您连接（一次），即使已达到max_connections。
UPDATE    -- 允许使用UPDATE
USAGE    -- “无权限”的同义词
GRANT OPTION    -- 允许授予权限


/* 表维护 */

-- 分析和存储表的关键字分布
ANALYZE [LOCAL | NO_WRITE_TO_BINLOG] TABLE 表名 ...
-- 检查一个或多个表是否有错误
CHECK TABLE tbl_name [, tbl_name] ... [option] ...
option = {QUICK | FAST | MEDIUM | EXTENDED | CHANGED}
-- 整理数据文件的碎片
OPTIMIZE [LOCAL | NO_WRITE_TO_BINLOG] TABLE tbl_name [, tbl_name] ...
```

## 8.2 MySQL备份

为什么备份：

- 保证重要数据不丢失
- 数据转移

MySQL数据库备份的方式

- 直接拷贝物理文件

- 在SQLyog这种可视化工具中手动导出

  - 在想要导出的表或者库中，右键选择  **备份和导出**
  - ![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122160447.png)

- 使用**命令行CMD**导出 `mysqldump`

  作用 :

  - 转储数据库
  - 搜集数据库进行备份
  - 将数据转移到另一个SQL服务器,不一定是MySQL服务器
  - ![image-20210122160634927](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122160635.png)

```sql

-- 导出
1. 导出一张表 -- mysqldump -uroot -p123456 school student >D:/a.sql
　　mysqldump -u用户名 -p密码 库名 表名 > 文件名(D:/a.sql)
2. 导出多张表 -- mysqldump -uroot -p123456 school student result >D:/a.sql
　　mysqldump -u用户名 -p密码 库名 表1 表2 表3 > 文件名(D:/a.sql)
3. 导出所有表 -- mysqldump -uroot -p123456 school >D:/a.sql
　　mysqldump -u用户名 -p密码 库名 > 文件名(D:/a.sql)
4. 导出一个库 -- mysqldump -uroot -p123456 -B school >D:/a.sql
　　mysqldump -u用户名 -p密码 -B 库名 > 文件名(D:/a.sql)
 
    可以-w携带备份条件
 
-- 导入
1. 在登录mysql的情况下：-- source D:/a.sql
　　source  备份文件
　　
2. 在不登录的情况下
　　mysql -u用户名 -p密码 库名 < 备份文件
```



# 9、规范数据库设计

## 9.1为什么需要设计

**当数据库比较复杂的时候，我们就需要设计了**

糟糕的数据库设计：

- 数据冗余，浪费空间
- 数据库插入和删除都会麻烦，异常【屏蔽使用物理外键】
- 程序的性能差

良好的数据库设计：

- 节省内存空间
- 保证数据库的完整性
- 方便我们开发系统

软件开发中，关于数据库的设计

- 分析需求：分析业务和需要处理的数据库的需求
- 概要设计：设计关系图 E-R图

**设计数据库的步骤（个人博客）**

- 收集信息，分析需求
  - 用户表（用户登录注销，用户的个人信息，写博客，创建分类）
  - 分类表（文章分类，谁创建的）
  - 文章表（文章的信息）
  - 友链表（友链信息）
  - 自定义表（系统信息，某个关键的字，或者某些主字段）
  - 说说表（发表心情…id ,content ,time）
- 标识实体（把需求落地到每个字段）
- 标识实体之间的关系
  - 写博客 user–>blog
  - 创建分类 user–>category
  - 关注 user–>user
  - 友链–>links
  - 评论 user–>user

## 9.2三大范式

为什么需要数据规范化？

- 信息重复
- 更新异常
- 插入异常
- 删除异常
  - 无法正常显示异常
- 删除异常
  - 丢失有效的信息

> 三大范式

**第一范式**（1NF）

原子性：保证每一列不可再分

![](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122162237.png)

**第二范式**（2NF）

前提：满足第一范式

**每张表只描述一件事情**

![image-20210122162253140](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122162253.png)

**第三范式**（3NF）

前提：满足第一范式和第二范式

第三范式需要确保数据表中的每一列数据都和**主键直接相关**，而不能间接相关。

（规范数据库的设计）

![image-20210122162505283](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122162505.png)

**规范性 和 性能 的问题**

关联查询的表，不得超过三张表

- 考虑商业化的需求和目标（成本和用户体验） 数据库的**性能**更加重要
- 再规范性能的问题的时候，需要适当的考虑一下，规范性
- 故意给某些表加一些冗余的字段（从多表，变成单表查询）
- 故意增加一些**计算列**（从大数据量降低为小数据量的查询：索引）

# 10、JDBC(重点)

## 10.1 数据库驱动

驱动：声卡，显卡，数据库

![](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122162822.png)

我们的程序会通过数据库驱动，和数据库打交道！

有多种数据库怎么办呢？

## 10.2 JDBC

SUN 公司为了简化开发人员的（对数据库的统一）操作，提供了一个**(Java操作数据库的)规范**，JDBC

这些规范的实现由具体的厂商（MySQL、Oracle......）去做

对于开发人员来说，我们只需要掌握JDBC的接口操作即可

![image-20210122162955631](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122162955.png)

java.sql

javax.sql

还需要导入数据库驱动包

## 10.3 第一个JDBC程序

> 创建测试数据库

```sql
CREATE DATABASE jdbcStudy CHARACTER SET utf8 COLLATE utf8_general_ci;

USE jdbcStudy;

CREATE TABLE `users`(
id INT PRIMARY KEY,
NAME VARCHAR(40),
PASSWORD VARCHAR(40),
email VARCHAR(60),
birthday DATE
);

INSERT INTO `users`(id,NAME,PASSWORD,email,birthday)
VALUES(1,'zhansan','123456','zs@sina.com','1980-12-04'),
(2,'lisi','123456','lisi@sina.com','1981-12-04'),
(3,'wangwu','123456','wangwu@sina.com','1979-12-04')

```

![image-20210122164117924](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122164118.png)

1.创建一个普通项目

2.导入数据库驱动

![image-20210122163956649](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122163956.png)

3.编写测试代码

```java
package com.kuang.lesson01;

import java.sql.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/22 - 01 - 22 - 16:42
 * @Description: com.kuang.lesson01
 * @version: 1.0
 */
public class JdbcFirstDemo {
    public static void main(String[] args) throws Exception {
        //1. 加载驱动
        Class.forName("com.mysql.jdbc.Driver");//固定写法
        //2. 用户信息和url
        //useUnicode=true&characterEncoding=utf8&&useSSL=true
        String url ="jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEncoding=utf8&&useSSL=false";
        String name = "root";
        String password = "123456";

        //3. 连接成功，返回数据库对象  connection代表数据库
        Connection connection= DriverManager.getConnection(url,name,password);
        //4. 执行SQL的对象 statement 执行SQL的对象
        Statement statement = connection.createStatement();

        //5. 执行SQL的对象 去执行SQL   可能存在结果，查看返回结果
        String sql="SELECT * FROM users";
        ResultSet resultSet = statement.executeQuery(sql);//返回的结果集,结果集中封装了我们全部查询的结果
        while(resultSet.next()){
            System.out.println("id+"+resultSet.getObject("id"));
            System.out.println("name+"+resultSet.getObject("NAME"));
            System.out.println("password+"+resultSet.getObject("PASSWORD"));
            System.out.println("email+"+resultSet.getObject("email"));
            System.out.println("birthday+"+resultSet.getObject("birthday"));
        }
        //6. 释放连接
        resultSet.close();
        statement.close();
        connection.close();
    }
}


```

步骤总结：
1.加载驱动

2.连接数据库 DriverManager

3.获取执行SQL的对象 Statement

4.获得返回的结果集

5.释放连接



> DriverManager

```java
//1. 加载驱动
//DriverManager.registerDriver(new com.mysql.jdbc.Driver());  //加载了两次
Class.forName("com.mysql.jdbc.Driver");//固定写法

//3. 连接成功，返回数据库对象  connection代表数据库
Connection connection= DriverManager.getConnection(url,name,password);

//connection代表数据库
//数据库设置自动提交
//事务提交
//事务回滚
connection.rollback();
connection.commit();
connection.setAutoCommit();

```

> URL

```java
String url ="jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEncoding=utf8&&useSSL=false";

//mysql 默认3306
//协议://主机地址:端口号/数据库名？参数1&参数2&参数3

//Oracle   1521
//jdbc:oralce:thin:@localhost:1521:sid


```

> statement 执行SQL的对象 pPrepareStatement 执行SQL的对象

```java
String sql="SELECT * FROM users"; //编写SQL

statement.executeQuery(); //查询操作并返回ResultSet
statement.execute();//执行任何SQL
statement.executeUpdate();//更新，插入，删除，返回一个受影响的行数

```

> ResultSet 查询的结果集，封装了所以的查询结果

获得指定的数据类型

```java
ResultSet resultSet = statement.executeQuery(sql);//返回的结果集,结果集中封装了我们全部查询的结果
        resultSet.getObject();//在不知道列类型下使用
        resultSet.getString();//如果知道则指定使用
        resultSet.getInt();
				resultSet.getDouble();
				.........
        
```

遍历,指针

```java
        resultSet.next(); //移动到下一个
        resultSet.afterLast();//移动到最后
        resultSet.beforeFirst();//移动到最前面
        resultSet.previous();//移动到前一行
        resultSet.absolute(row);//移动到指定行

```

> 释放内存

```java
//6. 释放连接
        resultSet.close();
        statement.close();
        connection.close();//耗资源

```

## 10.4 statement对象

**Jdbc中的statement对象用于向数据库发送SQL语句，想完成对数据库的增删改查，只需要通过这个对象向数据库发送增删改查语句即可。**

Statement对象的executeUpdate方法，用于向数据库发送增、删、改的sq|语句， executeUpdate执行完后， 将会返回一个整数(即增删改语句导致了数据库几行数据发生了变化)。

Statement.executeQuery方法用于向数据库发生查询语句，executeQuery方法返回代表查询结果的ResultSet对象。

> CRUD操作-create

使用executeUpdate(String sql)方法完成数据添加操作，示例操作：

```java
 				Statement statement = connection.createStatement();
        String sql = "insert into user(...) values(...)";
				//executeUpdate
        int num = statement.executeUpdate(sql);
        if(num>0){
            System.out.println("插入成功");
        }

```

> CRUD操作-delete

使用executeUpdate(String sql)方法完成数据删除操作，示例操作：

```java
				Statement statement = connection.createStatement();
        String sql = "delete from user where id =1";
     		//executeUpdate
				int num = statement.executeUpdate(sql);
        if(num>0){
            System.out.println("删除成功");
        }

```

> CURD操作-update

使用executeUpdate(String sql)方法完成数据修改操作，示例操作：

```java
				Statement statement = connection.createStatement();
        String sql = "update user set name ='' where name = ''";
				//executeUpdate
        int num = statement.executeUpdate(sql);
        if(num>0){
            System.out.println("修改成功");
        }

```

> CURD操作-read

使用executeQuery(String sql)方法完成数据查询操作，示例操作：

```java
Statement statement = connection.createStatement();
        String sql = "select * from  user where id =1";
				//executeQuery
        ResultSet rs= statement.executeQuery(sql);
        if(rs.next()){
            System.out.println("");
        }


```

> 
>
> **代码实现**

1.提取工具类

```properties
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEncoding=utf8&&useSSL=true
username=root
password=123456
```



```java
package com.kuang.JdbcUtils.utils;


import java.io.IOException;
import java.io.InputStream;
import java.sql.*;
import java.util.Properties;


/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/22 - 01 - 22 - 17:03
 * @Description: com.kuang.JdbcUtils.utils
 * @version: 1.0
 */
public class JdbcUtils {
    private static String driver = null;
    private static String url = null;
    private static String username = null;
    private static String password = null;

    static {
        try {
            InputStream in = JdbcUtils.class.getResourceAsStream("db.properties");
            Properties properties = new Properties();
            properties.load(in);

            driver = properties.getProperty("driver");
            url = properties.getProperty("url");
            username = properties.getProperty("username");
            password = properties.getProperty("password");

            //1.驱动只用加载一次
            Class.forName(driver);

        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }

    //2.获取连接
    public static Connection getConnection() throws Exception {
        return DriverManager.getConnection(url, username, password);
    }

    //3.释放资源
    public static void release(Connection conn, Statement st, ResultSet rs) throws SQLException {

        if (rs != null) {
            rs.close();
        }
        if (st != null) {
            st.close();
        }
        if (conn != null) {
            conn.close();
        }

    }
}

```

## 问题解决

- property文件位置问题
  应处于src目录下

![image-20210122174219463](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122174219.png)

- 在撰写JedisUtils工具类时

```java
//会出现NullPointerException: inStream parameter is null 去掉类加载器后成功
InputStream is = JedisUtils.class.getClassLoader().getResourceAsStream("jedis.properties");
//InputStream is = JedisUtils.class.getResourceAsStream("jedis.properties");

```



2.编写增删改的方法，`exectueUpdate`

```java
package com.kuang.lesson02.utils;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import static com.kuang.lesson02.utils.JdbcUtils.*;

public class TestInnsert {
    public static void main(String[] args){
        Connection conn =null;
        Statement st = null;
        ResultSet rs =null;

        try {
             conn = getConnection();//获取连接
            st = conn.createStatement();//获取SQL执行对象
            String sql = "INSERT INTO users(id,`NAME`,`PASSWORD`,`email`,`birthday`)" +
                    "VALUES(5,'sanjin','123456','233223@qq.com','2020-01-01')";

          //String sql = "DELETE from users where id = 4";
          //String sql = "update users set name='lisi2' where name='lisi'";

            int i = st.executeUpdate(sql);
            if(i>0){
                System.out.println("插入成功");
            }
        JdbcUtils.release(conn,st,rs);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}

```

3.查询 `executeQuery`

```java
package com.kuang.lesson02.utils;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import static com.kuang.lesson02.utils.JdbcUtils.*;

public class TestSelect {
    public static void main(String[] args) throws SQLException {
        Connection conn =null;
        Statement st = null;
        ResultSet rs =null;
        try {
             conn = getConnection();//获取连接
            st = conn.createStatement();//获取SQL执行对象
            String sql = "select * from users";
            rs=st.executeQuery(sql);//查询完毕返回结果集

            while (rs.next()){
                System.out.println(rs.getString("NAME"));
            }
        JdbcUtils.release(conn,st,rs);
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            JdbcUtils.release(conn,st,rs);
        }
    }

}

```

> SQL注入问题

![image-20210122175342835](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122175342.png)

sql存在漏洞，会被攻击导致数据泄露 **SQL会被拼接  or  **     

`or 1=1`

`1 and version()>0`

```java
package com.kuang.lesson02.utils;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import static com.kuang.lesson02.utils.JdbcUtils.getConnection;

public class SQL注入 {
    public static void main(String[] args) {

        //SQL注入
 login("' or '1=1","123456");
    }
    public static void login(String name,String password){


        Connection conn =null;
        Statement st = null;
        ResultSet rs =null;



        try {
            conn = getConnection();//获取连接
            st = conn.createStatement();//获取SQL执行对象
            String sql = "select * from users where `NAME`='"+ name +"'  AND `PASSWORD`='"+ password +"'" ;
            rs=st.executeQuery(sql);//查询完毕返回结果集

            while (rs.next()){
                System.out.println(rs.getString("NAME"));
            }
            JdbcUtils.release(conn,st,rs);
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            try {
                JdbcUtils.release(conn,st,rs);
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
        }
    }
}

```

![image-20210122175923312](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122175923.png)



## 10.5 PreparedStatement对象

PreparedStatement 可以防止SQL注入 ，效率更高。

### 新增

```sql
package com.kuang.lesson02;

import com.kuang.JdbcUtils.utils.JdbcUtils;

import java.sql.*;
import java.sql.SQLException;

import static com.kuang.lesson02.utils.JdbcUtils.getConnection;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/22 - 01 - 22 - 18:04
 * @Description: com.kuang.lesson02.utils
 * @version: 1.0
 */
public class TestInsert {
    public static void main(String[] args) throws SQLException {
        Connection conn =null;
        PreparedStatement st = null;
        ResultSet rs =null;

        try {
            conn = getConnection();

            //注意PreparedStatement与Statement的区别
            //书写SQL语句,使用?占位符代替参数
            String sql = "insert into users(`id`,`NAME`,`PASSWORD`,`email`,`birthday`) values (?,?,?,?,?)";
            st = conn.prepareStatement(sql);//预编译sql，先写sql，然后不执行
            //手动给参数赋值,第一个参数是?的下标（从1开始），第二个参数是?的值
            st.setInt(1,4);
            st.setString(2,"ylw");
            st.setString(3,"123456");
            st.setString(4,"123456@qq.com");
            //注意时间转换,sql.Date数据库时间，util.Date Java时间，new Date().getTime()获得时间戳
            st.setDate(5,new java.sql.Date(System.currentTimeMillis()));
            //执行
            int i = st.executeUpdate();
            if (i>0){
                System.out.println("插入成功！");
            }

        } catch (SQLException e) {
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            JdbcUtils.release(conn,st,rs);
        }
    }
}

```

### 删除

```java
package com.kuang.lesson02;

import com.kuang.lesson02.utils.JdbcUtils;

import java.sql.*;
import java.sql.SQLException;

import static com.kuang.lesson02.utils.JdbcUtils.getConnection;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/22 - 01 - 22 - 18:10
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class TestDelete {
    public static void main(String[] args) throws SQLException {
        Connection conn = null;
        PreparedStatement st = null;
        ResultSet rs =null;

        try {
            conn = getConnection();

            //注意PreparedStatement与Statement的区别
            //书写SQL语句,使用?占位符代替参数
            String sql = "delete from users where id =?";
            st = conn.prepareStatement(sql);//预编译sql，先写sql，然后不执行
            //手动给参数赋值,第一个参数是?的下标（从1开始），第二个参数是?的值
            st.setInt(1,4);

            //执行
            int i = st.executeUpdate();
            if (i>0){
                System.out.println("删除成功！");
            }

        } catch (SQLException e) {
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            JdbcUtils.release(conn,st,null);
        }
    }
}

```

### 修改

```java
package com.kuang.lesson02;

import com.kuang.lesson02.utils.JdbcUtils;

import java.sql.*;
import java.sql.SQLException;

import static com.kuang.JdbcUtils.utils.JdbcUtils.getConnection;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/22 - 01 - 22 - 18:13
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class TestUpdate {
    public static void main(String[] args) throws SQLException {
        Connection conn = null;
        PreparedStatement st = null;
        ResultSet rs =null;

        try {
            conn = getConnection();

            //注意PreparedStatement与Statement的区别
            //书写SQL语句,使用?占位符代替参数
            String sql = "update users set `NAME` = ? where id =?;";
            st = conn.prepareStatement(sql);//预编译sql，先写sql，然后不执行
            //手动给参数赋值,第一个参数是?的下标（从1开始），第二个参数是?的值
            st.setString(1,"wuxinyu");
            st.setInt(2,1);

            //执行
            int i = st.executeUpdate();
            if (i>0){
                System.out.println("更新成功！");
            }

        } catch (SQLException e) {
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            JdbcUtils.release(conn,st,null);
        }
    }
}

```



### 查询

```java
package com.kuang.lesson02;

import com.kuang.lesson02.utils.JdbcUtils;

import java.sql.*;
import java.sql.ResultSet;
import java.sql.SQLException;

import static com.kuang.lesson02.utils.JdbcUtils.getConnection;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/22 - 01 - 22 - 18:15
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class TestSelect {
    public static void main(String[] args) throws SQLException {
        Connection conn = null;
        PreparedStatement st = null;
        ResultSet rs = null;

        try {
            conn = getConnection();

            //注意PreparedStatement与Statement的区别
            //书写SQL语句,使用?占位符代替参数
            String sql = "select * from users where id =?";
            st = conn.prepareStatement(sql);//预编译sql，先写sql，然后不执行
            //手动给参数赋值,第一个参数是?的下标（从1开始），第二个参数是?的值
            st.setInt(1,1);

            //执行
            rs = st.executeQuery();

            //打印查询结果
            while (rs.next()){
                System.out.println(rs.getString("NAME"));
                System.out.println(rs.getString("password"));
            }

        } catch (SQLException e) {
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            JdbcUtils.release(conn,st,rs);
        }
    }
}
```

防止SQL注入本质，传递字符 带有“ ”，转义字符会被转义

```java
package pers.ylw.lesson03;

import pers.ylw.lesson02.utils.JdbcUtils;

import java.sql.*;

//测试PreparedStatement防止SQL注入
public class SQL注入 {
    public static void main(String[] args) {

        //正常登陆
        //login("zhangsan","123456");

        //sql注入
        login("''or 1=1","123456");

    }

    //登录业务
    public static void login(String username,String password){
        Connection conn = null;
        PreparedStatement st = null;
        ResultSet rs = null;

        //PreparedStatement 防止SQL注入的本质，把传递进来的参数当做字符
        //假设其中存在转义字符，比如说'会被直接转义

        try {
            conn= JdbcUtils.getConnection(); //使用自己写的JdbcUtils类获取数据库连接

            //书写SQL语句
            String sql = "select * from users where `NAME` = ? AND `password` = ?"; //与Mybatis类似
            //预编译
            st = conn.prepareStatement(sql);
            //手动设置参数
            st.setString(1,username);
            st.setString(2,password);

            //执行sql查询语句，接收返回的结果集
            rs = st.executeQuery();
            while (rs.next()){
                System.out.println(rs.getString("NAME"));
                System.out.println(rs.getString("password"));
                System.out.println("==================================");
            }

        } catch (SQLException e) {
            e.printStackTrace();
        } finally { //finally最后一定会执行
            JdbcUtils.release(conn,st,rs);
        }
    }
}
```



## 10.6 使用IDEA连接数据库

**1.点击右侧边栏的Database,右边的侧边栏应该有**
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122182052.png)
没有这个的话点一下左下角，应该就有了
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122182052.png)

**2.点击+，选择数据库，这里以MySQL为例**
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122182052.png)
**3.填写连接信息**
![image-20210122183149433](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122183149.png)
测试连接出现下图是因为没有包，点击Download Driver Files 下载
等他下载好
还是报错可以改一下驱动版本
![image-20210122183201171](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122183201.png)
好了，换好版本之后就测试成功了，可以使用了
![image-20210122183214810](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122183214.png)
如果版本还是不对可以如图操作

![image-20210122183230499](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122183230.png)

![image-20210122183248695](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122183248.png)
如果还是不行可以参考博客改时区 https://blog.csdn.net/liuqiker/article/details/102455077

**4.点击设置**
![image-20210122183302499](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122183302.png)
勾选想用的数据库，apply然后ok
![image-20210122183312108](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122183312.png)
就可以看到你想用的数据库了

![image-20210122183340828](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122183341.png)
点进去，双击表就可以看到信息了
![image-20210122183351522](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122183351.png)
**5.对表里的数据进行修改**
![image-20210122183401916](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122183402.png)
提交后点击刷新就可以看到成功修改

**6.调出sql控制台，书写sql语句**

![image-20210122183437851](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122183438.png)
![image-20210122183455596](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122183455.png)



## 10.7 JDBC事务

**要么都成功，要么都失败**

> ACID原则

A原子性：要么全部完成，要么都不完成

C一致性：结果总数不变

I隔离性：**多个进程互不干扰**

D持久性：一旦提交不可逆，持久化到数据库了

隔离性的问题：

脏读： 一个事务读取了另一个没有提交的事务

不可重复读：在同一个事务内，重复读取表中的数据，表发生了改变

虚读（幻读）：在一个事务内，读取到了别人插入的数据，导致前后读出来的结果不一致



> 代码实现

1. 开启事务`conn.setAutoCommit(false);`

2. 一组业务执行完毕，提交事务

3. 可以在catch语句中显示的定义回滚，但是默认失败会回滚

   
   
   ```sql
   CREATE TABLE account(
     id Int PRIMARY KEY AUTO_INCREMENT,
     NAME VARCHAR(40),
     money FLOAT
   );
   
   /*插入测试数据*/
   insert into account(name,money) values('A',1000);
   insert into account(name,money) values('B',1000);
   insert into account(name,money) values('B',1000);
   ```
   
   
   
   ```java
   package com.kuang.lesson03;
   
   import com.kuang.lesson03.utils.JdbcUtils;
   
   import java.sql.*;
   import java.sql.ResultSet;
   import java.sql.SQLException;
   
   import static com.kuang.lesson03.utils.JdbcUtils.getConnection;
   
   /**
    * @author Administrator
    * @Auther: wuxy
    * @Date: 2021/1/22 - 01 - 22 - 18:49
    * @Description: com.kuang.lesson03
    * @version: 1.0
    */
   public class Action {
       public static void main(String[] args) {
   
           Connection conn =null;
           PreparedStatement ps = null;
           ResultSet rs = null;
   
           try {
               conn = getConnection();
               
               //1.关闭数据库的自动提交功能， 开启事务
               conn.setAutoCommit(false);
               //2.自动开启事务
               String sql = "update account set money = money-500 where id = 1";
               ps =conn.prepareStatement(sql);
               ps.executeUpdate();
   
               //int i=1/0;
   
               String sql2 = "update account set money = money-500 where id = 2";
               ps=conn.prepareStatement(sql2);
               ps.executeUpdate();
   
               //3.业务完毕，提交事务
               conn.commit();
               System.out.println("操作成功");
           } catch (Exception e) {
               try {
                   //如果失败，则默认回滚
                   conn.rollback();//如果失败，回滚
               } catch (SQLException throwables) {
                   throwables.printStackTrace();
               }
               e.printStackTrace();
           }finally {
               try {
                   JdbcUtils.release(conn,ps,rs);
               } catch (SQLException throwables) {
                   throwables.printStackTrace();
               }
           }
       }
   }
   
   ```

## 10.8数据库连接池

### 数据库连接池简介

数据库连接—>执行完毕—>释放，

其中连接—>释放十分浪费系统资源

**池化技术：** 准备一些预先的资源，过来就连接预先准备好的
比如银行，开门—>服务—>关门，如果每一个客户都这样的话浪费时间，所以开门后准备业务员服务，这样就不用每一次都执行多余的步骤了。

开门—>业务员:等待客户—>服务—>关门。

那一个银行最少需要多少个服务员呢？

这就涉及到 **最小连接数** ，**最大连接数**就是业务最高承载上限，如果银行的客户很多，那么客户需要等待时间，这就是**等待超时**

例如：

最小连接数 10个（通常为你常用的连接数）

最大连接数 15个

等待超时 100ms

### 实现简介

编写连接池，需要实现一个接口 `DataSource`

- 开源数据源实现
  - DBCP
  - C3P0
  - Druid：阿里巴巴

使用了这些**数据库连接池**后，我们在项目开发中就不需要编写连接数据库的代码了

------

### DBCP

#### 需要用到的jar包

1.commons-dbcp 下载地址 http://commons.apache.org/proper/commons-dbcp/download_dbcp.cgi
选择好版本后点击下载
![image-20210122190235110](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122190235.png)
解压后用到这个文件
![image-20210122190300059](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122190300.png)
2.commons-pool 下载地址 http://commons.apache.org/proper/commons-pool/download_pool.cgi 下载方法同上，
用到的jar包是这个
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122190307.png)
把这两个包粘贴到你idea项目的lib目录下，如果你第一次导包就右击lib目录，选择下图选中的。
![image-20210122190324707](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122190324.png)
如果你的idea是版本比较新的，以前这个lib目录Add as Library过了的话，直接粘贴进去就行了，
如果版本比较旧的话，可能需要如下图删除原来的Library里的lib，然后再重新add一遍
右上角点击项目结构，或者在左上角的File里也有
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122190342.png)
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122190345.png)
打开后进行如下操作，然后再次将你的lib目录右击Add as Library
![image-20210122190400390](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122190400.png)
最后，总之只要你的lib目录里的jar包能如图显示分层，就能用了
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122190427.png)

#### 代码相关

在src下新建一个DBCP的配置文件dbcpconfig.properties（新建File，命名加后缀为就行）

```properties
#连接设置 (这里面的变量名，是DBCP数据源中定义好的，不要自己起名字)
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEncoding=utf8&useSSL=false
username=root
password=123456

# 下面的全都可以不设置，不写
#<!-- 初始化连接 -->
initialSize=10

#最大连接量
maxActive=50

#<!-- 最大空闲连接 --> 没人用也空着不释放，等超时之后再释放
maxIdle=20

#<!-- 最小空闲连接 -->
minIdle=5

#<!-- 超时等待时间，以毫秒为单位 60000/1000 = 60秒 -->
maxWait=60000


#JDBC驱动建立连接时附带的连接属性的格式必须为这样：[属性名=property;]
#注意："user"与"password"连个属性会被明确传递，因此这里不需要包含他们
connectionProperties=useUnicode=true;characterEncoding=UTF8

#指定由连接池所创建的连接的自动提交（auto-commit）状态。
defaultAutoCommit=true

#driver default 指定由连接池所创建的连接的只读(read-only) 状态。
#如果没有设置该值，则"setReadOnly"方法将不被调用。(某些驱动并不支持只读模式，如: Informix)
defaultReadOnly=

#driver default 指定由连接池所创建的连接的事务级别(TransactionIsolation)。
#可用值为下列之一: (详情可见javadoc)NONE,READ_ UNCOMMITTED,READ_ COMMITTED,REPEATABLE_ READ等
defaultTransactionIsolation=READ_UNCOMMITTED

```

自己封装一个工具类 JdbcUtils_DBCP

```java
package com.kuang.lesson04.utils;

import org.apache.commons.dbcp2.BasicDataSource;
import org.apache.commons.dbcp2.BasicDataSourceFactory;

import java.io.InputStream;
import java.sql.*;
import java.sql.SQLException;
import java.util.Properties;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/22 - 01 - 22 - 19:11
 * @Description: com.kuang.lesson04.utils
 * @version: 1.0
 */
public class JdbcUtils_DBCP {

    private static BasicDataSource dataSource = null;

    static {
        try{
            //通过反射获取配置文件资源流
            InputStream in = JdbcUtils_DBCP.class.getClassLoader().getResourceAsStream("dbcpconfig.properties");
            Properties properties = new Properties();
            properties.load(in);

            //创建数据源 工厂模式-->创建对象
            dataSource = BasicDataSourceFactory.createDataSource(properties);

        }catch (Exception e){
            e.printStackTrace();
        }
    }

    //获取连接
    public static Connection getConnection() throws SQLException {
        return dataSource.getConnection(); //从数据源中获取连接
    }

    //释放连接资源
    public static void release(Connection conn, Statement st, ResultSet rs){
        if (rs!=null){
            try {
                rs.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (st!=null){
            try {
                st.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (conn!=null){
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}

```

使用这个 JdbcUtils_DBCP 工具类进行操作

```java
package com.kuang.lesson04;

import com.kuang.lesson04.utils.JdbcUtils_DBCP;

import java.sql.*;
import java.sql.SQLException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/22 - 01 - 22 - 19:14
 * @Description: com.kuang.lesson04.utils
 * @version: 1.0
 */
public class TestDBCP {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement st = null;
        ResultSet rs = null;

        try {
            conn = JdbcUtils_DBCP.getConnection(); //只是改了这一行和最后关闭资源的时候，使用的类，其他的和前面的笔记没有区别

            //注意PreparedStatement与Statement的区别
            //书写SQL语句,使用?占位符代替参数
            String sql = "insert into users(`id`,`NAME`,`PASSWORD`,`email`,`birthday`) values (?,?,?,?,?)";
            st = conn.prepareStatement(sql);//预编译sql，先写sql，然后不执行
            //手动给参数赋值,第一个参数是?的下标（从1开始），第二个参数是?的值
            st.setInt(1,5);
            st.setString(2,"wxy");
            st.setString(3,"123456");
            st.setString(4,"123456@qq.com");
            //注意时间转换,sql.Date数据库时间，util.Date Java时间，new Date().getTime()获得时间戳
            st.setDate(5,new java.sql.Date(System.currentTimeMillis()));
            //执行
            int i = st.executeUpdate();
            if (i>0){
                System.out.println("插入成功！");
            }

        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JdbcUtils_DBCP.release(conn,st,rs); //关资源
        }
    }
}
```

如果你使用的包版本比较新可能会出现异常：
用DBCP进行数据连接池连接的时候出现java.lang.NoClassDefFoundError: Could not initialize class xxx.xxx.util.JdbcUtils_DBCP异常
解决方案:导入commanns-logging包
下载地址 https://commons.apache.org/proper/commons-logging/download_logging.cgi
![image-20210122191900061](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122191900.png)

### C3P0

#### 需要用到的jar包

1.c3p0 下载地址 https://sourceforge.net/projects/c3p0/
点击下载，你得等一会他才下载
![image-20210122192145878](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122192146.png)
包在lib文件夹里
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122192150.png)
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122192153.png)
2.mchange-commons-java
下载地址 https://mvnrepository.com/artifact/com.mchange/mchange-commons-java
推荐倒数第二新版本
![image-20210122192349542](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122192349.png)
点击jar进行下载
![image-20210122192403440](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122192403.png)
导包在上面DBCP中讲的很详细了

#### 代码相关

在src下新建一个c3p0的配置文件c3p0-config.xml（新建File，命名加后缀为就行）

```bash
<?xml version="1.0" encoding="UTF-8" ?>
<c3p0-config>
    <!--c3p0的缺省（默认）配置
    如果在代码中"ComboPooledDataSource ds = new ComboPooledDataSource();"这样写就表示使用的是C3P0的缺省(默认)配置
    -->
    <default-config>
        <property name="driverClass">com.mysql.jdbc.Driver</property>
        <!--改成你自己的url-->
        <property name="jdbcUrl">jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&amp;characterEncoding=utf8&amp;useSSL=false</property>
        <!--改成你自己的用户名-->
        <property name="user">root</property>
        <!--改成你自己的密码-->
        <property name="password">123456</property>

        <property name="acquireIncrement">5</property>
        <property name="initialPoolSize">10</property>
        <property name="minPoolSize">5</property>
        <property name="maxPoolSize">20</property>
    </default-config>

    <!--
    C3P0的命名配置,
    如果在代码中"ComboPooledDataSource ds = new ComboPooledDataSource("MySQL");"这样写就表示使用的是name是MySQL
    -->
    <named-config name="MySQL">
        <property name="driverClass">com.mysql.jdbc.Driver</property>
        <!--改成你自己的url-->
        <property name="jdbcUrl">jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&amp;characterEncoding=utf8&amp;useSSL=false</property>
        <!--改成你自己的用户名-->
        <property name="user">root</property>
        <!--改成你自己的密码-->
        <property name="password">123456</property>

        <property name="acquireIncrement">5</property>
        <property name="initialPoolSize">10</property>
        <property name="minPoolSize">5</property>
        <property name="maxPoolSize">20</property>
    </named-config>

</c3p0-config>
```

自己封装一个工具类 JdbcUtils_C3P0

```java
package com.kuang.lesson04.utils;

import com.mchange.v2.c3p0.ComboPooledDataSource;

import java.sql.*;
import java.sql.SQLException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/22 - 01 - 22 - 19:27
 * @Description: com.kuang.lesson04.utils
 * @version: 1.0
 */
public class JdbcUtils_C3P0 {

    private static ComboPooledDataSource dataSource = null;

    static {
        try{
            //代码版配置,不写在配置文件里
//            dataSource = new ComboPooledDataSource();
//            dataSource.setDriverClass();
//            dataSource.setUser();
//            dataSource.setPassword();
//            dataSource.setJdbcUrl();
//
//            dataSource.setMaxPoolSize();
//            dataSource.setMinPoolSize();

            //c3p0的配置文件不需要向DBCP那样获取，可以自动加载
            //创建数据源 工厂模式-->创建对象
            dataSource = new ComboPooledDataSource("MySQL");//配置文件写法

        }catch (Exception e){
            e.printStackTrace();
        }
    }

    //获取连接
    public static Connection getConnection() throws SQLException {
        return dataSource.getConnection(); //从数据源中获取连接
    }

    //释放连接资源
    public static void release(Connection conn, Statement st, ResultSet rs){
        if (rs!=null){
            try {
                rs.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (st!=null){
            try {
                st.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (conn!=null){
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}

```

使用这个 JdbcUtils_C3P0 工具类进行操作

```java
package com.kuang.lesson04;

import com.kuang.lesson04.utils.JdbcUtils_C3P0;

import java.sql.SQLException;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.Date;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/22 - 01 - 22 - 19:27
 * @Description: com.kuang.lesson04
 * @version: 1.0
 */
public class TestC3P0 {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement st = null;

        try {
            conn = JdbcUtils_C3P0.getConnection(); //只是改了这一行和最后关闭资源的时候，使用的类，其他的前面的笔记没有区别

            //注意PreparedStatement与Statement的区别
            //书写SQL语句,使用?占位符代替参数
            String sql = "insert into users(`id`,`NAME`,`PASSWORD`,`email`,`birthday`) values (?,?,?,?,?)";
            st = conn.prepareStatement(sql);//预编译sql，先写sql，然后不执行
            //手动给参数赋值,第一个参数是?的下标（从1开始），第二个参数是?的值
            st.setInt(1,4);
            st.setString(2,"ylw");
            st.setString(3,"123456");
            st.setString(4,"123456@qq.com");
            //注意时间转换,sql.Date数据库时间，util.Date Java时间，new Date().getTime()获得时间戳
            st.setDate(5,new java.sql.Date(new Date().getTime()));
            //执行
            int i = st.executeUpdate();
            if (i>0){
                System.out.println("插入成功！");
            }

        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JdbcUtils_C3P0.release(conn,st,null); //关资源
        }
    }
}

```

C3P0运行成功还会显示配置文件
![image-20210122193024436](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210122193024.png)

### 总结

无论使用什么数据，本质还是一样的，DateSource接口不会变，方法就不会变