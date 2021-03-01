# MyBatis

# 1.简介

MyBatis3官网：https://mybatis.org/mybatis-3/zh/index.html

软件版本：
MyBatis 3.5.2
IDEA 2020.1
JDK 1.8
Maven 3.6.3
MySQL 5.7.30
Tomcat 9.0.35

## 什么是MyBatis

![image-20210130101358291](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130101358.png)

- MyBatis 是一款优秀的**持久层框架**
- 它支持定制化 SQL、存储过程以及高级映射。
- MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。
- MyBatis 可以使用简单的 XML 或注解来配置和映射原生类型、接口和 Java 的 POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。

## 下载MyBatis

Github上MyBatis的地址： https://github.com/mybatis/mybatis-3/releases
![image-20210130101618500](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130101618.png)
Maven地址：https://mvnrepository.com/artifact/org.mybatis/mybatis/3.5.6
Maven依赖：

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.6</version>
</dependency>

```

## 持久化

数据持久化

- 持久化就是将程序的数据在**持久状态**和**瞬时状态**转化的过程
- 内存：**断电即失**（瞬时状态）
- 数据库(Jdbc)，IO文件   持久化。
- 生活中的持久化：冷藏. 罐头。（持久状态）

**为什么需要持久化？**

- 有一些对象，不能让他丢掉。
- 内存太贵了

## 持久层

Dao层，Service层，Controller层….

- 完成持久化工作的代码块
- 层界限十分明显。

## 为什么需要Mybatis？

- 帮助程序员将数据存入到数据库中。
- 方便
- 传统的JDBC代码太复杂了。简化。框架。自动化。
- 不用Mybatis也可以。学了更容易上手。 **技术没有高低之分**
- 优点：
  - 简单易学
  - 灵活
  - sql和代码的分离，提高了可维护性。
  - 提供映射标签，支持对象与数据库的orm字段关系映射
  - 提供对象关系映射标签，支持对象关系组建维护
  - 提供xml标签，支持编写动态sql。

# 2.第一个Mybatis程序

![image-20210130103427679](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130103427.png)

## 环境搭建

### 建立一个mybatis数据库用来使用，建立一张user表

```sql
CREATE DATABASE `mybatis`;

USE `mybatis`;

CREATE TABLE `user`(
  `id` INT(20) NOT NULL PRIMARY KEY,
  `name` VARCHAR(30) DEFAULT NULL,
  `pwd` VARCHAR(30) DEFAULT NULL
)ENGINE=INNODB DEFAULT CHARSET=utf8;

INSERT INTO `user`(`id`,`name`,`pwd`) VALUES 
(1,'狂神','123456'),
(2,'张三','123456'),
(3,'李四','123890')
```

### 新建一个Maven项目并导入相关依赖

![image-20210130104055287](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130104055.png)

![image-20210130104025937](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130104026.png)

删除src目录，让这个项目变成一个父工程，方便以后建立子工程

![image-20210130104259647](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130104259.png)

导入需要的依赖

```xml
<!--  导入依赖  -->
    <dependencies>
        <!--mysql驱动-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.49</version>
        </dependency>
        <!--mybatis--><!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.6</version>
        </dependency>
        <!--junit-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
    </dependencies>
```

爆红就说明没有这个包，点击右上角的同步按钮等待下载

### 在父Maven项目中创建一个子模块

在上一步的Maven项目里new一个module

![image-20210130104518924](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130104518.png)

![image-20210130104535178](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130104535.png)

![image-20210130104559316](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130104559.png)

这时候在父项目里的pom.xml文件里可以看到多出了modules，就是我们刚刚建立的mybatis-01，好处就是在子模块里就不用每次都导入依赖了

```xml
 <modules>
        <module>mybatis-01</module>
    </modules>
```

### 编写MyBatis的核心配置文件

在resources文件夹下新建文件mybatis-config.xml

![image-20210130104824236](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130104824.png)

```xml
<?xml version="1.0" encoding="UTF8"?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--configuration核心配置文件-->
<configuration>

    <!--environments为复数，表示里面可以配置多个环境default表示选择这里面的其中一个环境的id，-->
    <environments default="development">

        <!--environment表示一个环境的开始，id是它的标志-->
        <environment id="development">
            <!--使用jdbc的事物管理-->
            <transactionManager type="JDBC"/>
            <!--里面这4个就是连接数据库要用的东西，把自己的数据库相关信息写进去就行-->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useUnicode=true&amp;characterEncoding=utf-8&amp;useSSL=false"/>
                <property name="username" value="root"/>
                <property name="password" value="123456"/>
            </dataSource>
        </environment>

    </environments>

    <!--每一个Mapper .xml都需要在HyBatis核心配置文件中注册-->
    <!--mappers复数表示可以配置多个-->
    <mappers>
        <mapper resource="com/kuang/dao/UserMapper.xml"/>
    </mappers>

</configuration>
```

注意：这里的url是针对MySQL5.7，useSSL=true如果不行就改成false
在正常.properties配置文件中&符号直接写就行

```properties
mysql://localhost:3306/mybatis?useUnicode=true&characterEncoding=utf-8&useSSL=false
```

但是在.xml文件中&符号需要转义为`&`.

```xml
<property name="url" value="jdbc:mysql://localhost:3306/mybatis?useUnicode=true&amp;characterEncoding=utf-8&amp;useSSL=false"/>
```

### 编写MyBatis的工具类

一般把下图中的读取配置文件封装成工具类

![image-20210130105039215](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130105039.png)

目录结构如下图

![image-20210130105103836](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130105103.png)

```java
package com.kuang.utils;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/30 - 01 - 30 - 10:57
 * @Description: com.kuang.utils
 * @version: 1.0
 * 获取配置文件的工具类，MyBatis使用的是工厂模式，工厂用来生产产品
 * SqlSessionFactory 生产 SqlSession
 */
public class MyBatisUtils {
    //提升sqlSessionFactory作用域，方便在getSqlSession中使用static代码块里的东西
    private static SqlSessionFactory sqlSessionFactory = null;

    static {
        //使用Mybatis第一步：获取sqlSessionFactory对象
        try {
            String resource = "mybatis-config.xml"; //定义资源文件
            InputStream inputStream = Resources.getResourceAsStream(resource); //加载资源文件变成流
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream); //通过流获取工厂
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    //既然有了 SqlSessionFactory，顾名思义，我们就可以从中获得 SqlSession 的实例了。
    // SqlSession 完全包含了面向数据库执行 SQL 命令所需的所有方法。
    public static SqlSession getSqlSession(){
        return sqlSessionFactory.openSession();
    }
}

```

## 编写代码

### 与数据库表相关的实体类

目录结构如下图

![image-20210130110043313](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130110043.png)

然后照着数据库表把实体类写好就可以了（注意类的属性名和数据库表的列名要一致）

```java
package com.kuang.pojo;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/30 - 01 - 30 - 11:05
 * @Description: com.kuang.pojo
 * @version: 1.0
 */
//与数据库表对应的实体类
public class User {
    private int id;
    private String name;
    private String pwd;

    public User() {
    }

    public User(int id, String name, String pwd) {
        this.id = id;
        this.name = name;
        this.pwd = pwd;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPwd() {
        return pwd;
    }

    public void setPwd(String pwd) {
        this.pwd = pwd;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", pwd='" + pwd + '\'' +
                '}';
    }
}

```

### Dao（Mapper）接口和实现类（配置文件）

**接口：**

![image-20210130110709240](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130110709.png)

````java
package com.kuang.dao;

import com.kuang.pojo.User;

import java.util.List;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/30 - 01 - 30 - 11:06
 * @Description: com.kuang.dao
 * @version: 1.0
 */
public interface UserDao {
    List<User> getUserList();
}

````



**配置文件：**

![image-20210130110829634](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130110829.png)

在JDBC中需要再实现上面的UserDao接口，但是MyBatis就不需要了，写一个配置文件即可，可以理解为通过配置文件来实现接口。

这里把配置文件起名为UserMapper.xml也可以写UserDao.xml但是相对于MyBatis后面都是用Mapper了，前面的写Dao是为了便于通过JDBC来理解MyBatis

接口实现类由原来的UserdaoImpl转换为Mapper配置文件

![image-20210130114030159](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130114030.png)

```xml
<?xml version="1.0" encoding="UTF8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--namespace命名空间，绑定一个对应的Dao或者说是Mapper接口-->
<!--这里namespace的值要改成自己的接口，可以理解为通过这个配置文件实现接口，
下面的标签都可以与接口实现类对应-->
<mapper namespace="com.kuang.dao.UserDao">

    <!--写一个查询语句-->
    <!--select表示查询，id对应要重写的方法名，resultType对应查询语句返回的结果类型-->
    <select id="getUserList" resultType="com.kuang.pojo.User">
        select * from mybatis.user
    </select>
</mapper>
```

## 测试

**使用junit测试**

目录结构：
测试程序一般写在test目录下的绿色java包里

![image-20210130110321348](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130110321.png)

测试的目录结构尽量和普通的目录结构对应

![image-20210130110352932](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130110353.png)

测试代码

```java
package com.kuang.dao;

import com.kuang.pojo.User;
import com.kuang.utils.MyBatisUtils;
import org.apache.ibatis.session.SqlSession;
import org.junit.Test;

import java.util.List;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/30 - 01 - 30 - 11:13
 * @Description: com.kuang.dao
 * @version: 1.0
 */
public class UserDaoTest {
    @Test
    public void test(){
        //通过写的MyBatisUtils类里的getSqlSession()方法，获取sqlSession对象
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        //执行SQL语句
        UserDao userDao = sqlSession.getMapper(UserDao.class);//通过UserDao接口，返回接口实现类信息
        List<User> userList = userDao.getUserList();//执行口实现类的方法，即配置文件里的id
        //输出结果
        for (User user : userList) {
            System.out.println(user);
        }
        //关闭sqlSession
        sqlSession.close();

    }
}

```

![image-20210130114056041](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130114056.png)

![image-20210130111934362](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130111934.png)

## 测试中的错误

### 错误一：绑定异常MapperRegitry

org.apache.ibatis.binding.BindingException: Type interface com.ylw.dao.UserDao is not known to the MapperRegitry.

![](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130112322.png)

**解决方法：**
在MyBatis核心配置文件中注册Mapper配置文件

![image-20210130112610878](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130112611.png)

```xml
 <!--每一个Mapper .xml都需要在HyBatis核心配置文件中注册-->
    <!--mappers复数表示可以配置多个-->
    <mappers>
        <mapper resource="com/kuang/dao/UserMapper.xml"/>
    </mappers>

```



但是由于Mapper配置文件不在resources目录下，会造成资源导出失败问题，造成下面的错误二

![image-20210130112532885](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130112532.png)

### 错误二： java.lang.ExceptionInInitializerError

**产生问题的原因：**
maven由于他的约定大于配置，我们之后可以能遇到我们写的配置文件，无法被导出或者生效的问题。
详见博客https://blog.csdn.net/qq_43594119/article/details/106199248中 解决资源导出失败问题
**解决方法：**

在pom.xml中添加下面的代码

```xml
<!--在build中配置resources，来防止我们资源导出失败的问题-->
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

### 错误三：Cause: org.xml.sax.SAXParseException; lineNumber: 5; columnNumber: 14; 1 字节的 UTF-8 序列的字节 1 无效。

解决方法：

```xml
<?xml version="1.0" encoding="UTF8" ?>
```

解决办法就是将配置文件头部的utf-8改成utf8

## 总结，测试时正确的做法

方法一：直接将UserMapper.xml文件放到resources文件夹中，同时MyBatis核心配置文件的注册路径为路径为resource="UserMapper.xml"就可以了，不用在pom.xml再加build配置

方法二：UserMapper.xml文件不放在resources文件夹中，而是放在java目录下，MyBatis核心配置文件的注册路径为路径为resource=“包名路径/UserMapper.xml”，但是要在pom.xml中添加build配置，按照错误二，解决方法二的方式进行

# 3.CURD

![image-20210130163029470](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130163029.png)

## namespace注意点

namespace中的包名要和 Dao/mapper 接口的包名一致！

## select

选择，查询语句;
Mapper.xml配置文件的一些标签：

- id : 就是对应的namespace中的方法名；
- resultType：Sql语句执行的返回值！
- parameterType ： 参数类型！

### 接口

![image-20210130163449868](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130163449.png)

### Mapper配置文件

![image-20210130163611489](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130163611.png)

```java
//    根据ID查询用户
    User getUserById(int id );
```

```xml
<!--    根据ID查询用户-->
    <select id="getUserById" parameterType="int" resultType="com.kuang.pojo.User">
        select * from mybatis.user where id = #{id}
    </select>
```

### 测试代码

```java
public class UserDaoTest {
@Test
    public void getUserById(){
        //通过写的MyBatisUtils类里的getSqlSession()方法，获取sqlSession对象
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        //执行SQL语句
        UserDao userDao = sqlSession.getMapper(UserDao.class);//UserMapper，返回接口实现类信息
        User user = userDao.getUserById(1);//执行口实现类的方法，即配置文件里的id
        System.out.println(user);

        //关闭sqlSession
        sqlSession.close();
    }
}
```

![image-20210130164707715](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130164707.png)

## insert

### 接口

![image-20210130170155197](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130170155.png)

### Mapper配置文件

![image-20210130170209537](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130170209.png)
**注意**：配置文件可以使用HTML的注释，但是在SQL语句中不能使用注释，会报错，下面是错误示范

```perl
    <!--这里的尖括号可以写注释-->
    <insert id="addUser" parameterType="com.ylw.pojo.User">
    	--这里不能这样写sql注释
        insert into mybatis.user (id,name,pwd) values (#{id},#{name},#{pwd})
    </insert>
12345
```

```xml
<!--插入一个用户-->
    <insert id="addUser" parameterType="com.kuang.pojo.User" >
        insert into mybatis.user (id,name,pwd) values (#{id},#{name},#{pwd})
    </insert>
```

```java
//插入一个用户
    int addUser(User user);
```

### 测试代码

```java
    //增删改需要提交事物否则表是不会变的
@Test
    public void addUser(){
        //通过写的MyBatisUtils类里的getSqlSession()方法，获取sqlSession对象
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        //执行SQL语句
        UserDao userDao = sqlSession.getMapper(UserDao.class);//UserMapper，返回接口实现类信息
        int res = userDao.addUser(new User(4,"赵六","123333"));//执行口实现类的方法，即配置文件里的id
        if (res > 0){ //插入成功的话，返回值一般是1
            System.out.println("插入成功");
        }
        //提交事务
        sqlSession.commit();
        //关闭sqlSession
        sqlSession.close();
    }
```

**！必须要提交事务！**

![image-20210130170015330](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130170015.png)

## update

### 接口

![image-20210130171051807](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130171051.png)

![image-20210130171106229](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130171106.png)

### Mapper配置文件

```perl
<!--修改用户    -->
    <!--注意#{}里的参数id,name,pwd是与实体类User里面的属性名对应的-->
    <update id="updateUser" parameterType="com.kuang.pojo.User">
        update mybatis.user set name = #{name},pwd= #{pwd} where id = #{id};
    </update>
```

### 测试代码

```java
@Test
    public void updateUser(){
        //通过写的MyBatisUtils类里的getSqlSession()方法，获取sqlSession对象
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        //执行SQL语句
        UserDao userDao = sqlSession.getMapper(UserDao.class);//UserMapper，返回接口实现类信息
        int res = userDao.updateUser(new User(4,"嗷嗷","129999"));//执行口实现类的方法，即配置文件里的id
        if (res > 0){ //修改成功的话，返回值一般是1
            System.out.println("修改成功");
        }
        //提交事务
        sqlSession.commit();
        //关闭sqlSession
        sqlSession.close();
    }
```

![image-20210130171115777](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130171115.png)

## delete

### 接口

![image-20210130171618697](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130171618.png)

![image-20210130171605220](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130171605.png)

### Mapper配置文件

```perl
<!--   删除用户 -->
    <!--注意#{}里的参数id,name,pwd是与实体类User里面的属性名对应的-->
    <delete id="deleteUser" parameterType="int">
        delete from mybatis.user where id = #{id}
    </delete>
```

### 测试代码

```java
   @Test
    public void deleteUser(){
        SqlSession sqlSession =MyBatisUtils.getSqlSession();

        UserDao userDao = sqlSession.getMapper(UserDao.class);

        int res = userDao.deleteUser(4);//执行口实现类的方法，即配置文件里的id
        if (res>0){
            System.out.println("删除成功");
        }

        sqlSession.commit();
        sqlSession.close();

    }
```

![image-20210130171550314](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130171550.png)

## 常见错误

1.全限定类名使用  .  来分隔，不要使用    / 

2.标签不要匹配错误

3.程序必须符合规范

4.空指针问题，没有注册到资源

5.输出的xml文件中有中文乱码问题

6.xml文件的导出问题

# 4.Map和模糊查询拓展

## 使用map

假设，我们的实体类，或者数据库中的表，字段或者参数过多，我们应当考虑使用Map！

如果只修改密码，只需要在map中放入id 和pwd就可以了！！！

### 接口

```java
//万能的Map
int addUser2(Map<String,Object> map);
```

### Mapper配置文件

```xml
<!--对象中的属性，可以直接取出来    传递map的key-->
    <insert id="addUser2" parameterType="map">
        insert into mybatis.user (id, pwd) values (#{userid},#{passWord});
    </insert>
```

### 测试例子

```java
@Test
    public void addUser2(){
        SqlSession sqlSession =MyBatisUtils.getSqlSession();

        UserDao userDao = sqlSession.getMapper(UserDao.class);


        Map<String, Object> map = new HashMap<String, Object>();

        map.put("userid",5);
        map.put("passWord","2222333");

        userDao.addUser2(map);

        sqlSession.commit();
        sqlSession.close();
    }
```



Map传递参数，直接在sql中取出key即可！ 【parameterType=“map”】

对象传递参数，直接在sql中取对象（实体类）的属性即可！【parameterType=“Object”】

只有一个基本类型参数的情况下，可以直接在sql中取到！

多个参数用Map，或者注解！

## 模糊查询like

### 接口

```java
//模糊查询
    List<User> getUserLike(String name);
```

### Mapper配置文件

注意配置文件里不要使用类似%的符号，可能会造成SQL   1 or 1==1注入问题

```xml
<!--    like 模糊查询-->
    <select id="getUserLike" resultType="com.kuang.pojo.User">
        select * from mybatis.user where name like #{value}
    </select>
```

另一种写法（）

```sql
select * from mybatis.user where name like #{value}"%"

```

### 测试例子

```java
@Test
    public void getUserLike(){
        SqlSession sqlSession = MyBatisUtils.getSqlSession();

        UserDao userDao = sqlSession.getMapper(UserDao.class);
        List<User> users = userDao.getUserLike("李%");
        for (User user : users) {
            System.out.println(user);
        }

        sqlSession.close();
    }

```

![image-20210130175217397](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130175217.png)

# 5.配置解析

## 核心配置解析

- 官方推荐文件名称：mybatis-config.xml

- MyBatis 的配置文件包含了会深深影响 MyBatis 行为的设置和属性信息。

- 一些标签的意思：

  ```xml
  configuration（配置）
  properties（属性）
  settings（设置）
  typeAliases（类型别名）
  typeHandlers（类型处理器）
  objectFactory（对象工厂）
  plugins（插件）
  environments（环境配置）
  environment（环境变量）
  transactionManager（事务管理器）
  dataSource（数据源）
  databaseIdProvider（数据库厂商标识）
  mappers（映射器）
  ```

## 环境配置（environments）

### environments和environment

下面的environments 标签里包含了两个environment ，一个id是development，一个id是test，但是environments 只能选择一个environment ，如图environments 的default属性的值，就对应选中的environment 的id的值

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--configuration核心配置文件-->
<configuration>

    <!--environments为复数，表示里面可以配置多个环境default表示选择这里面的其中一个环境的id，-->
    <environments default="development">

        <!--environment表示一个环境的开始，id是它的标志-->
        <environment id="development">
        <!--使用jdbc的事物管理-->
            <transactionManager type="JDBC"/>
            <!--里面这4个就是连接数据库要用的东西，把自己的数据库相关信息写进去就行-->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useUnicode=true&amp;characterEncoding=utf-8&amp;useSSL=false"/>
                <property name="username" value="root"/>
                <property name="password" value="root"/>
            </dataSource>
        </environment>

        <!--environment表示一个环境的开始，id是它的标志-->
        <environment id="test">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useUnicode=true&amp;characterEncoding=utf-8&amp;useSSL=false"/>
                <property name="username" value="root"/>
                <property name="password" value="root"/>
            </dataSource>
        </environment>

    </environments>

    <!--每一个Mapper.xml都需要在MyBatis核心配置文件中注册-->
    <!--mappers复数表示可以配置多个-->
    <mappers>
        <mapper resource="com/ylw/dao/UserMapper.xml"/>

    </mappers>

</configuration>

```

### transactionManager

基本上只使用jdbc类型的
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130180833.png)

### dataSource

基本上都是用POOLED类型有**连接池**的
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716111402580.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNTk0MTE5,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130180934.png)

Mybatis默认的事务管理器就是`JDBC`，默认是数据池是`POOLED`

学会使用配置多套运行环境<environment id="development"> 

使用<environments default="development"> 配置

## 属性（properties）

我们可以通过properties属性来实现引用配置文件

这些属性都是可外部配置且可动态替换的，既可以在典型的 Java 属性文件中配置，亦可通过 properties 元素的子元素来传递。

### 示例

编写一个数据库配置文件db.properties

![image-20210130181508084](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130181508.png)

```properties
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/mybatis?useUnicode=true&characterEncoding=utf-8&useSSL=false
username=root
password=123456
```

在mybatis核心配置文件mybatis-config.xml中引入数据库配置文件db.properties，所以properties只能放在最上面
![image-20210130181549150](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130181549.png)

### 方式一、在引用的时候，可以只写一个resource路径，然后在value里使用${对应的名称}就行

```perl
<?xml version="1.0" encoding="UTF8"?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--configuration核心配置文件-->
<configuration>
    <!--这里用一个自闭和标签，只要写一个resource就行了-->
    <properties resource="db.properties"/>

    <environments default="development">
        <!--environment表示一个环境的开始，id是它的标志-->
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${driver}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${username}"/>
                <property name="password" value="${password}"/>
            </dataSource>
        </environment>


    </environments>
    <mappers>
        <mapper resource="com/kuang/dao/UserMapper.xml"/>
    </mappers>

</configuration>
```

![image-20210130182751859](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130182751.png)



### 方式二、在引用的时候，也可以设置一些值

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130182609.png)
但是，如果和外部配置文件有冲突的时候，会优先使用外部配置文件的

## 类型别名（typeAliases）

- 类型别名是为Java类型设置一个短的名字。
- 存在的意义仅在于用来减少类完全限定名的冗余。

让下图这种返回值类型更加人性化
![image-20210130184038004](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130184038.png)
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130190059.png)

### 第一种typeAlias方法

如图在MyBatis核心配置文件中添加别名如下，注意标签顺序
![image-20210130190312849](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130190312.png)

```xml
<!--可以给实体类起别名-->
    <typeAliases>
        <typeAlias type="com.kuang.pojo.User" alias="User"></typeAlias>
    </typeAliases>
```



然后在使用到com.kuang.pojo.User时，就可以使用User代替
![image-20210130190400647](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130190400.png)

### 第二种package方法

指定包名的方法：扫描实体类的包，它的默认别名就为这个类的类名，首字母小写

![image-20210130194357717](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130194357.png)

```xml
<typeAliases>
        <package name="com.kuang.pojo" />
    </typeAliases>
```



大小写都可以，但是建议小写
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130194405.png)

在实体类比较少的时候，使用第一种方式。
如果实体类十分多，建议使用第二种。

第一种可以DIY别名，第二种则不行，如果非要改，需要在实体上增加注解

### 注解

注意，注解和package要一起使用
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716120848846.png)
在实体类里添加注解，就使用注解的别名
![image-20210130194451384](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130194451.png)

```java
    @Alias("hello")
public class User {
}
```



![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130194514.png)

### Java 类型内建的类型别名

下面是一些为常见的 Java 类型内建的类型别名。它们都是不区分大小写的，注意，为了应对原始类型的命名重复，采取了特殊的命名风格。

| 别名       | 对应的类型 |
| ---------- | ---------- |
| _byte      | byte       |
| _long      | long       |
| _short     | short      |
| _int       | int        |
| _integer   | int        |
| _double    | double     |
| _float     | float      |
| _boolean   | boolean    |
| string     | String     |
| byte       | Byte       |
| long       | Long       |
| short      | Short      |
| int        | Integer    |
| integer    | Integer    |
| double     | Double     |
| float      | Float      |
| boolean    | Boolean    |
| date       | Date       |
| decimal    | BigDecimal |
| bigdecimal | BigDecimal |
| object     | Object     |
| map        | Map        |
| hashmap    | HashMap    |
| list       | List       |
| arraylist  | ArrayList  |
| collection | Collection |
| iterator   | Iterator   |

## 设置（settings）

这是 MyBatis 中极为重要的调整设置，它们会改变 MyBatis 的运行时行为。
常用的一些设置
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130194726.png)
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130194738.png)
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130194732.png)
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130194729.png)
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130194745.png)

## 其他配置

不重要的一些配置

- typeHandlers（类型处理器
- objectFactory（对象工厂）
- 常用plugins插件
  - mybatis-generator-core
  - mybatis-plus
  - 通用mapper

## 映射器（mappers）

绑定异常`MapperRegitry`

MapperRegistry：注册绑定我们的Mapper配置文件；

### 方式一： resource【推荐使用】

```xml
<!--每一个Mapper.XML都需要在Mybatis核心配置文件中注册！-->
<mappers>
        <mapper resource="com/kuang/dao/UserMapper.xml"/>
</mappers>
```

没有特殊的限制！！

### 方式二：使用class文件绑定注册

```xml
<!--每一个Mapper.XML都需要在Mybatis核心配置文件中注册！-->
<mappers>
    <mapper class="com.kuang.dao.UserDao"/>
</mappers>

```

注意点：

- 接口和他的Mapper配置文件必须同名！
- 接口和他的Mapper配置文件必须在同一个包下！

### 方式三：使用扫描包进行注入绑定

```xml
<!--每一个Mapper.XML都需要在Mybatis核心配置文件中注册！-->
<mappers>
    <package name="com.kuang.dao"/>
</mappers>
```

注意点：

- 接口和他的Mapper配置文件必须同名！
- 接口和他的Mapper配置文件必须在同一个包下！

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716124059230.png)

## 生命周期和作用域

![image-20210130200620777](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130200620.png)
生命周期，和作用域，是至关重要的，因为错误的使用会导致非常严重的**并发问题**。

**SqlSessionFactoryBuilder：**

- 一旦创建了 SqlSessionFactory，就不再需要它了
- **局部变量**

**SqlSessionFactory：**

- 说白了就是可以想象为 ：**数据库连接池**
- SqlSessionFactory 一旦被创建就应该在应用的运行期间一直存在，**没有任何理由丢弃它或重新创建另一个实例。**
- 因此 SqlSessionFactory 的最佳作用域是**应用作用域**。
- 最简单的就是使用**单例模式**或者静态单例模式。

**SqlSession**

- 连接到连接池的一个请求！
- SqlSession 的实例不是线程安全的，因此是不能被共享的，所以它的最佳的作用域是**请求或方法作用域**。
- 用完之后需要**赶紧关闭**，否则资源被占用！

![image-20210130200854532](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130200854.png)

如果不及时关闭的话，容易引发严重的宕机，并发问题！！

这里面的每一个Mapper，就代表一个具体的业务！

# 6.resultMap结果集

**解决属性名和字段名不一致的问题**

## 属性名和字段名不一致的情况

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130202144.png)
运行测试发现，数据库表中pwd对应的值查不出来
![image-20210130203416239](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130203416.png)

## 原因

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200716191207638.png)
**类型处理器**把这句话转化成了下面这句话    pwd找不到

```sql
select id,name,pwd from mybatis.user where id = #{id}
```

## 解决方法

### 方法一，改写SQL语句

改为如下所示，加一个 as 别名 

```sql
select id,name,pwd as password from mybatis.user where id = #{id}
```

### 方法二，resultMap结果集映射

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130233427.png)
改为，其实只要映射不一样的字段就行，type对应原来resultType的值

首先  mybatis-config.xml

```xml
<typeAliases>
        <typeAlias type="com.kuang.pojo.User" alias="User"/>
    </typeAliases>
```

UserMapper.xml

```xml
<!--    结果集映射-->
    <resultMap id="UserMap" type="User">
<!--        column数据库中的字段，property实体类的属性-->
        <result column="id" property="id"></result>
        <result column="name" property="name"></result>
        <result column="pwd" property="password"></result>
    </resultMap>

    <!--根据ID查询用户-->
    <select id="getUserById" parameterType="int" resultMap="UserMap">
        select * from mybatis.user where id = #{id}
    </select>
```



![image-20210130233720044](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210130233720.png)

- 官方的一些解释

- `resultMap` 元素是 MyBatis 中最重要最强大的元素
- resultMap的设计思想是，对于简单的语句根本不需要配置显式的结果映射，而对于复杂一点的语句只需要描述它们的关系就行了。
- `resultMap` 最优秀的地方在于，虽然你已经对它相当了解了，但是根本就不需要显式地用到他们。

# 7.**日志相关**

## 日志工厂

如果一个数据库操作，出现了异常，我们需要排错。日志就是最好的助手！
以前可以通过输出`sout`和`调试`来差错
现在可以使用：日志工厂！
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717113208133.png)
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131120806.png)

- 值

- SLF4J
- LOG4J【重要】
- LOG4J2
- JDK_LOGGING java自带的日志输出
- COMMONS_LOGGING 工具包
- STDOUT_LOGGING【重要】控制台输出
- NO_LOGGING 没有日志输出

在Mybatis中具体使用那个一日志实现，在**设置**中设定！

**STDOUT_LOGGING标准日志输出**

在mybatis核心配置文件中，配置我们的日志！（注意settings标签的位置）
注意一个引号里一个空格都不能多，大小写也必须完全一致

```xml
    <settings>
        <!--配置日志-->
        <!--标准的日志工厂实现，不用导包-->
        <setting name="logImpl" value="STDOUT_LOGGING"/>
    </settings>
```

输出解析
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131121215.png)

## LOG4J

### 什么是LOG4J？

- LOG4J是[Apache](https://baike.baidu.com/item/Apache/8512995)的一个开源项目，通过使用Log4j，我们可以控制日志信息输送的目的地是[控制台](https://baike.baidu.com/item/控制台/2438626)、文件、[GUI](https://baike.baidu.com/item/GUI)组件
- 我们也可以控制每一条日志的输出格式；
- 通过定义每一条日志信息的**级别**，我们能够更加**细致地控制**日志的生成过程。
- 通过一个[配置文件](https://baike.baidu.com/item/配置文件/286550)来灵活地进行配置，而不需要修改应用的代码。

### LOG4J导包

[官网maven依赖](https://mvnrepository.com/artifact/log4j/log4j/1.2.17)

```xml
<!-- https://mvnrepository.com/artifact/log4j/log4j -->
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
</dependency>
```

### LOG4J配置文件

导完包之后，新建一个配置文件
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131121548.png)
内容：

```properties
#将等级为DEBUG的日志信息输出到console和file这两个目的地，console和file的定义在下面的代码
log4j.rootLogger=DEBUG,console,file

#控制台输出的相关设置
log4j.appender.console = org.apache.log4j.ConsoleAppender
log4j.appender.console.Target = System.out
log4j.appender.console.Threshold=DEBUG
log4j.appender.console.layout = org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern=[%c]-%m%n

#文件输出的相关设置
log4j.appender.file = org.apache.log4j.RollingFileAppender
log4j.appender.file.File=./log/log4j.log
log4j.appender.file.MaxFileSize=10mb
log4j.appender.file.Threshold=DEBUG
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=[%p][%d{yy-MM-dd}][%c]%m%n

#日志输出级别
log4j.logger.org.mybatis=DEBUG
log4j.logger.java.sql=DEBUG
log4j.logger.java.sql.Statement=DEBUG
log4j.logger.java.sql.ResultSet=DEBUG
log4j.logger.java.sql.PreparedStatement=DEBUG
```

注意这是文件输出路径
![image-20210131122020213](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131122020.png)

### 在MyBatis核心配置文件中设置输出日志为LOG4J

```xml
    <settings>
        <!--配置日志-->
        <setting name="logImpl" value="LOG4J"/>
    </settings>
```

配置完成后就可以使用了

![image-20210131122230108](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131122230.png)

### 其他简单使用方法

1、在类中使用：导入包import org.apache.log4j.Logger;
注意不到导入错了，java有个自带的logger
2、获取日志对象，参数为当前类.class
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131122638.png)
3、使用不同级别的输出来代替System.out.println();
![image-20210131122706738](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131122706.png)

日志级别

```java
public class UserDaoTest {

    static Logger logger = Logger.getLogger(UserDaoTest.class);
    @Test
    public void testLog4j(){
        //三种级别的输出
        //提示
        logger.info("info:进入了testLog4j");
        //调试
        logger.debug("debug:进入了testLog4j");
        //错误
        logger.error("error:进入了testLog4j");
    }
}
```

# 8.分页

为什么要分页？

- 减少数据的处理量

## sql分页方法limit 关键字

下标从0开始，pagesize>0时表示是每页的数量

```sql
语法：SELECT * from user limit startIndex,pageSize;
例如：
SELECT * from user limit 3;  #[0,n]
```

## 使用MyBatis实现分页

### 接口

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717182553364.png)

### Mapper.xml配置文件

```xml
    <!--分页-->
    <select id="getUserByLimit" parameterType="map" resultType="com.ylw.pojo.User">
        select * from mybatis.User limit #{startIndex},#{pageSize}
    </select>

```

### 测试

```java
    @Test
    public void getUserByLimit(){
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);

        //传入参数键值对
        HashMap<String, Integer> map = new HashMap<String, Integer>();
        map.put("startIndex",0);
        map.put("pageSize",2);

        //获取查询结果并输出
        List<User> userList = userMapper.getUserByLimit(map);
        for (User user : userList) {
            System.out.println(user);
        }

        sqlSession.close();
    }

```

![image-20210131171523778](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131171523.png)

## 通过RowBounds分页(不常用)

即面向对象，不在Mapper配置文件中通过sql语句进行分页，而是在方法里去实现，而且在方法里还要使用MyBatis官方不推荐使用的方法

### 接口

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131175555.png)

### Mapper.xml配置文件

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131175603.png)

### 测试

```java
   @Test
   public void getUserByRowBounds(){
       SqlSession sqlSession = MyBatisUtils.getSqlSession();

       //通过RowBounds实现,从下标为1往后（不包括）,每页显示2行
       RowBounds rowBounds = new RowBounds(1, 2);

       //通过java代码层面实现分页
       List<User> userList = sqlSession.selectList("com.kuang.dao.UserMapper.getUserByRowBounds",null,rowBounds);
       for (User user : userList) {
           System.out.println(user);
       }

       sqlSession.close();
   }

```

## 分页插件mybatis pagehelper

官网：https://pagehelper.github.io/![在这里插入图片描述](https://img-blog.csdnimg.cn/20200717204034678.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNTk0MTE5,size_16,color_FFFFFF,t_70)
官方使用文档：

(需要外网访问)

https://pagehelper.github.io/docs/howtouse/

# 9.**注解开发**

## 9.1、面向接口编程

大家之前都学过面向对象编程，也学习过接口，但在真正的开发中，很多时候我们会选择面向接口编程

**根本原因∶==解耦==，可拓展，提高复用，分层开发中，上层不用管具体的实现，大家都遵守共同的标准，使得开发变得容易，规范性更好**

在一个面向对象的系统中，系统的各种功能是由许许多多的不同对象协作完成的。在这种情况下，各个对象内部是如何实现自己的,对系统设计人员来讲就不那么重要了;
-而各个对象之间的协作关系则成为系统设计的关键。小到不同类之间的通信，大到各模块之间的交互，在系统设计之初都是要着重考虑的，这也是系统设计的主要工作内容。面向接口编程就是指按照这种思想来编程。
**关于接口的理解**

接口从更深层次的理解，应是定义(规范，约束）与实现(名实分离的原则）的分离。

接口的本身反映了系统设计人员对系统的抽象理解。

-接口应有两类:
第一类是对一个个体的抽象，它可对应为一个抽象体(abstract class);

第二类是对一个个体某一方面的抽象，即形成一个抽象面(interface) ;-一个体有可能有多个抽象面。抽象体与抽象面是有区别的。

**三个面向区别**

-面向对象是指，我们考虑问题时，以对象为单位，考虑它的属性及方法.

-面向过程是指，我们考虑问题时，以一个具体的流程（事务过程）为单位，考虑它的实现.

-接口设计与非接口设计是针对复用技术而言的，与面向对象(过程）不是一个问题.更多的体现就是对系统整体的架构

## 9.2、使用注解开发的步骤

### 一、写接口

注解写在接口上面，括号里是SQL语句

![image-20210131194406695](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131194406.png)

```java
package com.kuang.dao;

import com.kuang.pojo.User;
import org.apache.ibatis.annotations.Select;

import java.util.List;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/31 - 01 - 31 - 19:33
 * @Description: com.kuang.dao
 * @version: 1.0
 */
public interface UserMapper {
//
    @Select("select * from mybatis.user")
    List<User> getUsers();
}

```



### 二、在mybatis核心配置文件中绑定接口

![image-20210131194440109](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131194440.png)

```xml
 <!--每一个Mapper .xml都需要在HyBatis核心配置文件中注册-->
    <!--mappers复数表示可以配置多个-->
    <mappers>
        <mapper class="com.kuang.dao.UserMapper"/>
    </mappers>
```

### 三、测试

![image-20210131194528685](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131194528.png)

```java
package com.kuang.dao;

import com.kuang.pojo.User;
import com.kuang.utils.MyBatisUtils;
import org.apache.ibatis.session.SqlSession;
import org.junit.Test;

import java.util.List;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/31 - 01 - 31 - 19:36
 * @Description: com.kuang.dao
 * @version: 1.0
 */
public class UserMapperTest {
    @Test
    public void test(){
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);

        List<User> users = userMapper.getUsers();
        for(User user:users){
            System.out.println(user);
        }

        sqlSession.close();

    }
}

```



### 官方推荐，复杂的语句不要使用注解

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131194329.png)

本质：反射机制实现
底层：动态代理！

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131194334.png)

## Mybatis详细的执行流程

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131194340.png)

# 10.**使用注解实现CRUD**

我们可以在工具类创建的时候实现自动提交事务！

```java
public static SqlSession  getSqlSession(){
    return sqlSessionFactory.openSession(true);
}
```

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131210029.png)

## 接口

```java
package com.kuang.dao;

import com.kuang.pojo.User;
import org.apache.ibatis.annotations.*;

import java.util.List;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/31 - 01 - 31 - 19:33
 * @Description: com.kuang.dao
 * @version: 1.0
 */
public interface UserMapper {
//
    @Select("select * from mybatis.user")
    List<User> getUsers();

    //方法存在多个参数时，所有的参数必须加上@Param()，SQL语句中的参数名对应的是@Param()里的参数名
    @Select("select * from user where id = #{id} and name = #{name}")
    User getUserByID(@Param("id") int id, @Param("name") String name);

    @Insert("insert into user(id,name,pwd) values (#{id},#{name},#{password})")
    int addUser(User user);

    @Update("update user set name=#{name},pwd=#{password} where id = #{id}")
    int updateUser(User user);

    //SQL语句中的参数名对应的是@Param()里的参数名
    @Delete("delete from user where id = #{uid}")
    int deleteUser(@Param("uid") int id);

}

```

## 在mybatis核心配置文件中绑定接口

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200719101450398.png)

## 测试

```java
package com.kuang.dao;

import com.kuang.pojo.User;
import com.kuang.utils.MyBatisUtils;
import org.apache.ibatis.session.SqlSession;
import org.junit.Test;

import java.util.List;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/31 - 01 - 31 - 19:36
 * @Description: com.kuang.dao
 * @version: 1.0
 */
public class UserMapperTest {
    @Test
    public void test(){
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);

        //查找全部
//        List<User> users = mapper.getUsers();
//        for (User user : users) {
//            System.out.println(user);
//        }

        //根据id查找
//        User userByID = mapper.getUserByID(1,"张三");
//        System.out.println(userByID);

        //添加用户
//        mapper.addUser(new User(4, "Hello","123456"));

        //更新
//        mapper.updateUser(new User(4,"赵四","123456"));

        //删除
        mapper.deleteUser(4);

        sqlSession.close();

    }
}

```

## 关于@Param() 注解

- 基本类型的参数或者String类型，需要加上
- 引用类型不需要加
- 如果只有一个基本类型的话，可以忽略，但是建议大家都加上！
- 我们在SQL中引用的(#{})就是我们这里的 @Param() 中设定的属性名！

![image-20210131200238270](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131200238.png)

# 11.**Lombok**

(外网)Lombok官网： https://projectlombok.org/

## 什么是Lombok

> Project Lombok is a java library that automatically plugs into your editor and build tools, spicing up your java.
> Never write another getter or equals method again, with one annotation your class has a fully featured builder, Automate your logging variables, and much more.

翻译：

> Project Lombok是一个java库，它可以自动插入到编辑器和构建工具中，增强java的性能。
> 永远不要再写另一个getter或equals方法，只要有一个注释，你的类就有一个功能齐全的构建器，自动记录变量等等。

## 使用方法

### 在IDEA2020.1中安装Lombok插件

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131210524.png)
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131210812.png)
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131210817.png)

### 在项目中导入Lombok jar包

maven依赖 https://mvnrepository.com/artifact/org.projectlombok/lombok/1.18.18

在pom.xml文件中添加依赖

```java
<!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.18</version>
    <scope>provided</scope>
</dependency>

```

### 可供使用的注解

```java
@Getter and @Setter
@FieldNameConstants
@ToString
@EqualsAndHashCode
@AllArgsConstructor, @RequiredArgsConstructor and @NoArgsConstructor
@Log, @Log4j, @Log4j2, @Slf4j, @XSlf4j, @CommonsLog, @JBossLog, @Flogger
@Data
@Builder
@Singular
@Delegate
@Value
@Accessors
@Wither
@SneakyThrows
```

### 常用的Lombok注解

```java
@Data 生成无参构造，get、set、tostring、hashcode，equals
@AllArgsConstructor 生成有参构造
@NoArgsConstructor 生成无参构造
@EqualsAndHashCode 生成Equals和HashCode相关的方法
@ToString 生成tostring方法
@Getter
```

### 使用示例

可以看得到下面的实体类中有get、set、构造方法等
![image-20210131211643202](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131211643.png)
可以使用注解来代替这些代码
![image-20210131211724171](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131211724.png)

![image-20210131211427205](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131211427.png)

![image-20210131211459327](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131211459.png)

# 12.多对一处理

## 多对一关系

![image-20210131212400418](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131212400.png)

- 多个学生，对应一个老师
- 对于学生这边而言， **关联** … 多个学生，关联一个老师 【多对一】
- 对于老师而言， **集合** ， 一个老师，有很多学生 【一对多】
- ![image-20210131212533294](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131212533.png)

## 创建一个多对一的表

```sql
CREATE TABLE `teacher` (
  `id` INT(10) NOT NULL,
  `name` VARCHAR(30) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8;

INSERT INTO teacher(`id`, `name`) VALUES (1, '秦老师'); 

CREATE TABLE `student` (
  `id` INT(10) NOT NULL,
  `name` VARCHAR(30) DEFAULT NULL,
  `tid` INT(10) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `fktid` (`tid`),
  CONSTRAINT `fktid` FOREIGN KEY (`tid`) REFERENCES `teacher` (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8;


INSERT INTO `student` (`id`, `name`, `tid`) VALUES ('1', '小明', '1'); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES ('2', '小红', '1'); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES ('3', '小张', '1'); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES ('4', '小李', '1'); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES ('5', '小王', '1');

```

![image-20210131222322167](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131222322.png)

## 建立数据库表对应的实体类

老师类

```java
package com.kuang.pojo;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/31 - 01 - 31 - 22:27
 * @Description: com.kuang.pojo
 * @version: 1.0
 */
public class Teacher {
    private int id;
    private String name;

    public Teacher() {
    }

    public Teacher(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "Teacher{" +
                "id=" + id +
                ", name='" + name + '\'' +
                '}';
    }
}

```

学生类

```java
package com.kuang.pojo;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/31 - 01 - 31 - 22:28
 * @Description: com.kuang.pojo
 * @version: 1.0
 */
public class Student {
    private int id;
    private String name;

    //学生需要关联一个老师，外键通过类来关联，不能写死
    private Teacher teacher;

    public Student() {
    }

    public Student(int id, String name, Teacher teacher) {
        this.id = id;
        this.name = name;
        this.teacher = teacher;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Teacher getTeacher() {
        return teacher;
    }

    public void setTeacher(Teacher teacher) {
        this.teacher = teacher;
    }

    @Override
    public String toString() {
        return "Student{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", teacher=" + teacher +
                '}';
    }
}
```

## 相关接口准备

一个学生接口，一个老师接口

![image-20210131224629841](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131224630.png)

## 接口相关的Mapper配置文件准备

![image-20210131224758805](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131224758.png)

```java
package com.kuang.dao;

import com.kuang.pojo.Teacher;
import org.apache.ibatis.annotations.Param;
import org.apache.ibatis.annotations.Select;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/31 - 01 - 31 - 22:29
 * @Description: com.kuang.dao
 * @version: 1.0
 */
public interface TeacherMapper {

    @Select("select * from teacher where id = #{tid}")
    Teacher getTeacher(@Param("tid") int id);
}

```

```java
package com.kuang.dao;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/31 - 01 - 31 - 22:28
 * @Description: com.kuang.dao
 * @version: 1.0
 */
public interface StudentMapper {
}

```





![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131224638.png)

![image-20210131224731335](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131224731.png)

```xml
<?xml version="1.0" encoding="UTF8"?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.kuang.dao.TeacherMapper">

</mapper>
```

```xml
<?xml version="1.0" encoding="UTF8"?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.kuang.dao.StudentMapper">

</mapper>
```



## 在mybatis核心配置文件中绑定Mapper配置文件

![image-20210131224941854](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131224942.png)

```xml
<?xml version="1.0" encoding="UTF8"?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--configuration核心配置文件-->
<configuration>
    <!--这里用一个自闭和标签，只要写一个resource就行了-->
    <properties resource="db.properties"/>
    <settings>
        <!--配置日志-->
        <setting name="logImpl" value="LOG4J"/>
    </settings>
    <typeAliases>
        <package name="com.kuang.pojo"/>
    </typeAliases>
    <environments default="development">
        <!--environment表示一个环境的开始，id是它的标志-->
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${driver}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${username}"/>
                <property name="password" value="${password}"/>
            </dataSource>
        </environment>


    </environments>

    <!--每一个Mapper .xml都需要在HyBatis核心配置文件中注册-->
    <!--mappers复数表示可以配置多个-->
    <mappers>
        <mapper resource="com/kuang/dao/StudentMapper.xml"/>
        <mapper resource="com/kuang/dao/TeacherMapper.xml"/>
    </mappers>

</configuration>
```

## 测试类TeacherTest

```java
package com.kuang.dao;

import com.kuang.pojo.Student;
import com.kuang.pojo.Teacher;
import com.kuang.utils.MyBatisUtils;
import org.apache.ibatis.annotations.Mapper;
import org.apache.ibatis.session.SqlSession;

import java.util.List;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/31 - 01 - 31 - 22:42
 * @Description: com.kuang.dao
 * @version: 1.0
 */
public class TeacherTest {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        TeacherMapper teacherMapper = sqlSession.getMapper(TeacherMapper.class);
        Teacher teacher = teacherMapper.getTeacher(1);

        System.out.println(teacher);
        sqlSession.close();

    }
}

```

![image-20210131225044316](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131225044.png)



## 按照查询嵌套处理（子查询）

![image-20210131225229545](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131225230.png)

### StudentMapper.xml配置文件

```java
package com.kuang.dao;

import com.kuang.pojo.Student;

import java.util.List;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/31 - 01 - 31 - 22:28
 * @Description: com.kuang.dao
 * @version: 1.0
 */
public interface StudentMapper {
    List<Student> getStudent();
}

```



```java
<?xml version="1.0" encoding="UTF8"?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.kuang.dao.StudentMapper">

    <!--
   思路:
       1. 查询所有的学生信息
       2. 根据查询出来的学生的tid，寻找对应的老师！  子查询
   -->

    <resultMap id="StudentTeacher" type="com.kuang.pojo.Student">
        <result property="id" column="id"/>
        <result property="name" column="name"/>
        <!--复杂的属性，我们需要单独处理 对象： association ;集合： collection -->
        <!--javaTyped对应column外键的实体类，select里是一个select语句的id-->
        <association property="teacher" column="tid" javaType="com.kuang.pojo.Teacher" select="getTeacher"/>
    </resultMap>

    <select id="getStudent" resultMap="StudentTeacher">
        select * from student
    </select>

    <select id="getTeacher" resultType="com.kuang.pojo.Teacher">
        select * from teacher where id = #{id}
    </select>
</mapper>
```

### 测试

```java
package com.kuang.dao;

import com.kuang.pojo.Student;
import com.kuang.utils.MyBatisUtils;
import org.apache.ibatis.session.SqlSession;

import java.util.List;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/31 - 01 - 31 - 22:56
 * @Description: com.kuang.dao
 * @version: 1.0
 */
public class TestStudent {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        StudentMapper studentMapper = sqlSession.getMapper(StudentMapper.class);
        List<Student> studentList = studentMapper.getStudent();

        for (Student student : studentList) {
            System.out.println(student);
        }
        sqlSession.close();
    }
}

```

![image-20210131231122961](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131231123.png)

## 按照结果嵌套处理（联表查询）

```java
package com.kuang.dao;

import com.kuang.pojo.Student;

import java.util.List;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/31 - 01 - 31 - 22:28
 * @Description: com.kuang.dao
 * @version: 1.0
 */
public interface StudentMapper {
    List<Student> getStudent();
    List<Student> getStudent2();
}

```



### StudentMapper.xml配置文件

```java
  <!--按照结果嵌套处理-->
    <select id="getStudent2" resultMap="StudentTeacher2">
        select s.id sid, s.name sname, t.name tname
        from student s,
             teacher t
        where s.tid = t.id;
    </select>

    <resultMap id="StudentTeacher2" type="com.kuang.pojo.Student">
        <result property="id" column="sid"/>
        <result property="name" column="sname"/>
        <association property="teacher" javaType="com.kuang.pojo.Teacher">
            <result property="name" column="tname"/>
        </association>
    </resultMap>
```

### 测试

```java
@Test
    public void testStudent(){
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        StudentMapper studentMapper = sqlSession.getMapper(StudentMapper.class);
        List<Student> studentList = studentMapper.getStudent2();

        for (Student student : studentList) {
            System.out.println(student);
        }

        sqlSession.close();
    }
```

![image-20210131231344745](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210131231344.png)



# 13.一对多处理

比如：一个老师拥有多个学生！
对于老师而言，就是一对多的关系!

## 实体类

学生类

```java
package com.kuang.pojo;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/31 - 01 - 31 - 22:28
 * @Description: com.kuang.pojo
 * @version: 1.0
 */
public class Student {
    private int id;
    private String name;
    private int tid;

    public Student() {
    }

    public Student(int id, String name, int tid) {
        this.id = id;
        this.name = name;
        this.tid = tid;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getTid() {
        return tid;
    }

    public void setTid(int tid) {
        this.tid = tid;
    }

    @Override
    public String toString() {
        return "Student{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", tid=" + tid +
                '}';
    }
}
```

老师类

```java
package com.kuang.pojo;

import java.util.List;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/31 - 01 - 31 - 22:27
 * @Description: com.kuang.pojo
 * @version: 1.0
 */
public class Teacher {
    private int id;
    private String name;

    //一个老师拥有多个学生，使用集合
    private List<Student> students;

    public Teacher() {
    }

    public Teacher(int id, String name, List<Student> students) {
        this.id = id;
        this.name = name;
        this.students = students;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public List<Student> getStudents() {
        return students;
    }

    public void setStudents(List<Student> students) {
        this.students = students;
    }

    @Override
    public String toString() {
        return "Teacher{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", students=" + students +
                '}';
    }
}

```

## 按照查询嵌套处理（子查询）

### 接口

```java
Teacher getTeacher2(@Param("tid") int id);
```

### StudentMapper.xml配置文件

```xml
<!--按照查询嵌套处理-->
    <select id="getTeacher2" resultMap="TeacherStudent2">
        select * from mybatis.teacher where id = #{tid}
    </select>

    <resultMap id="TeacherStudent2" type="com.kuang.pojo.Teacher">
      <!--复杂的属性，我们需要单独处理 对象： association 集合： collection
        javaType="" 指定属性的类型！
        集合中的泛型信息，我们使用ofType获取
        -->
        <collection property="students" javaType="ArrayList" ofType="com.kuang.pojo.Student" select="getStudentByTeacherId" column="id"/>
    </resultMap>

    <select id="getStudentByTeacherId" resultType="com.kuang.pojo.Student">
        select * from mybatis.student where tid = #{tid}
    </select>
```

### 测试

```java
    @Test
    public void test(){
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        TeacherMapper mapper = sqlSession.getMapper(TeacherMapper.class);
        Teacher teacher = mapper.getTeacher2(1);

        System.out.println(teacher);

        sqlSession.close();
    }
```

![image-20210201175938456](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201175938.png)

## 按照结果嵌套处理（联表查询）

### 接口

```java
//获取指定老师下的所有学生及老师的信息
    Teacher getTeacher(@Param("tid") int id);
```

### StudentMapper.xml配置文件

```xml
    <!--按结果嵌套查询-->
    <select id="getTeacher" resultMap="TeacherStudent">
        select s.id sid, s.name sname, t.name tname,t.id tid
        from student s,teacher t
        where s.tid = t.id and t.id = #{tid}
    </select>

    <resultMap id="TeacherStudent" type="com.kuang.pojo.Teacher">
        <result property="id" column="tid"/>
        <result property="name" column="tname"/>
        <!--复杂的属性，我们需要单独处理 对象： association 集合： collection
        javaType="" 指定属性的类型！
        集合中的泛型信息，我们使用ofType获取
        -->
        <collection property="students" ofType="com.kuang.pojo.Student">
            <result property="id" column="sid"/>
            <result property="name" column="sname"/>
            <result property="tid" column="tid"/>
        </collection>
    </resultMap>
```

### 测试

```java
  @Test
    public void test(){
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        TeacherMapper mapper = sqlSession.getMapper(TeacherMapper.class);
        Teacher teacher = mapper.getTeacher(1);

        System.out.println(teacher);

        sqlSession.close();
    }
```

![image-20210201174653250](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201174653.png)

## 小结

1. 关联 - association 【多对一】
2. 集合 - collection 【一对多】
3. javaType & ofType
   1. JavaType 用来指定实体类中属性的类型
   2. ofType 用来指定映射到List或者集合中的 pojo类型，泛型中的约束类型！

注意点：

- 保证SQL的可读性，尽量保证通俗易懂
- 注意一对多和多对一中，属性名和字段的问题！
- 如果问题不好排查错误，可以使用日志 ， 建议使用 Log4j
- 遇到爆红找不到symbol但是可以运行，将冲突的module remove出项目

# 14.动态 SQL常用标签

## 什么是动态SQL

![image-20210201201617211](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201201617.png)

![image-20210201183041193](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201183041.png)

![image-20210201183134265](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201183134.png)

**什么是动态SQL：动态SQL就是指根据不同的条件生成不同的SQL语句**

> 动态 SQL 元素和 JSTL 或基于类似 XML 的文本处理器相似。在 MyBatis 之前的版本中，有很多元素需要花时间了解。MyBatis 3 大大精简了元素种类，现在只需学习原来一半的元素便可。MyBatis 采用功能强大的基于 OGNL 的表达式来淘汰其它大部分元素。

> 关键字
> if
> choose (when, otherwise)
> trim (where, set)
> foreach

## 搭建测试环境

### 建表

```sql
CREATE TABLE `blog` (
  `id` varchar(50) NOT NULL COMMENT '博客id',
  `title` varchar(100) NOT NULL COMMENT '博客标题',
  `author` varchar(30) NOT NULL COMMENT '博客作者',
  `create_time` datetime NOT NULL COMMENT '创建时间',
  `views` int(30) NOT NULL COMMENT '浏览量'
) ENGINE=InnoDB DEFAULT CHARSET=utf8

```

### 数据库表对应的实体类

```java
package com.kuang.pojo;

import java.util.Date;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/2/1 - 02 - 01 - 18:42
 * @Description: com.kuang.pojo
 * @version: 1.0
 */
public class Blog {
    private String id;
    private String title;
    private String author;
    private Date createTime; //属性名和字段名不一致，可以在配置文件里设置转换
    private int views;

    public Blog() {
    }

    public Blog(String id, String title, String author, Date createTime, int views) {
        this.id = id;
        this.title = title;
        this.author = author;
        this.createTime = createTime;
        this.views = views;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getAuthor() {
        return author;
    }

    public void setAuthor(String author) {
        this.author = author;
    }

    public Date getCreateTime() {
        return createTime;
    }

    public void setCreateTime(Date createTime) {
        this.createTime = createTime;
    }

    public int getViews() {
        return views;
    }

    public void setViews(int views) {
        this.views = views;
    }

    @Override
    public String toString() {
        return "Blog{" +
                "id='" + id + '\'' +
                ", title='" + title + '\'' +
                ", author='" + author + '\'' +
                ", createTime=" + createTime +
                ", views=" + views +
                '}';
    }
}

```

### 用来随机生成ID的工具类

```java
package com.kuang.utils;

import org.junit.Test;

import java.util.UUID;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/2/1 - 02 - 01 - 18:44
 * @Description: com.kuang.utils
 * @version: 1.0
 */
public class IDUtils {

    public static String getId(){
        //随机生成id，并把-替换成空
        return UUID.randomUUID().toString().replaceAll("-","");
    }

    @Test
    public void test(){
        System.out.println(IDUtils.getId());
    }
}

```

![image-20210201184439183](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201184439.png)

### MyBatis核心配置文件

设置开启驼峰命名转换规则

```sql
    <settings>
        <!--配置日志-->
        <setting name="logImpl" value="STDOUT_LOGGING"/>
        <!--开启驼峰命名转换-->
        <setting name="mapUnderscoreToCamelCase" value="true"/>
    </settings>
```

```java
package com.kuang.dao;

import com.kuang.pojo.Blog;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/2/1 - 02 - 01 - 18:46
 * @Description: com.kuang.dao
 * @version: 1.0
 */
public interface BlogMapper {
    int addBlog(Blog blog);
}

```



```xml
<?xml version="1.0" encoding="UTF8"?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.kuang.dao.BlogMapper">
    <insert id="addBlog" parameterType="Blog">
        insert into mybatis.blog(id, title, author, create_time, views)
        VALUES (#{id}, #{title}, #{author}, #{createTime}, #{views});
    </insert>
</mapper>
```

```java
package com.kuang.dao;

import com.kuang.pojo.Blog;
import com.kuang.utils.IDUtils;
import com.kuang.utils.MyBatisUtils;
import org.apache.ibatis.session.SqlSession;
import org.junit.Test;

import java.util.Date;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/2/1 - 02 - 01 - 18:55
 * @Description: com.kuang.dao
 * @version: 1.0
 */
public class MyTest {
    @Test
    public void addBlogTest() {
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);
        Blog blog = new Blog();
        blog.setId(IDUtils.getId());
        blog.setTitle("Mybatis");
        blog.setAuthor("狂神说");
        blog.setCreateTime(new Date());
        blog.setViews(9999);

        mapper.addBlog(blog);

        blog.setId(IDUtils.getId());
        blog.setTitle("Java");
        mapper.addBlog(blog);

        blog.setId(IDUtils.getId());
        blog.setTitle("Spring");
        mapper.addBlog(blog);

        blog.setId(IDUtils.getId());
        blog.setTitle("微服务");
        mapper.addBlog(blog);

        sqlSession.commit();
        sqlSession.close();

    }
}

```

![image-20210201190005617](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201190005.png)

## if标签

![image-20210201190237722](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201190237.png)

### 接口

```java
    //查询博客
    List<Blog> queryBlogIf(Map map);
```

### Mapper.xml配置文件

```xml
   <!--这里写where是为了便于后面的if拼接，并且当if都不符合的时候也可以确保查询语句正确,还可以写where标签-->
    <select id="queryBlogIf" parameterType="map" resultType="com.kuang.pojo.Blog">
        select * from mybatis.blog where 1=1
        <if test="title != null">
            and title = #{title}
        </if>
        <if test="author != null">
            and author = #{author}
        </if>
    </select>
```

### 测试类

```java
   @Test
    public void queryBlogIf(){
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);

        HashMap map = new HashMap();
        map.put("title","Java");

        List<Blog> blogs = mapper.queryBlogIf(map);

        for (Blog blog : blogs) {
            System.out.println(blog);
        }

        sqlSession.close();
    }
```

## where标签

![image-20210201191438446](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201191438.png)

![image-20210201191535572](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201191535.png)

where 元素只会在子元素返回任何内容的情况下才插入 “WHERE” 子句。而且，若子句的开头为 “AND” 或 “OR”，where 元素也会将它们去除。

把上面的where 1=1语句改成下面的where标签

```java
    <select id="queryBlogIf" parameterType="map" resultType="com.ylw.pojo.Blog">
        select * from mybatis.blog
        <where>
            <if test="title != null">
                and title = #{title}
            </if>
            <if test="author != null">
                and author = #{author}
            </if>
        </where>
    </select>
```

## choose (when, otherwise)

![image-20210201191212941](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201191213.png)

choose标签里有when和otherwise
可以理解为
**switch语句里的case和default，**
先执行符合条件的when，没有就执行otherwise（注意只会执行一个when）

### 接口

```java
List<Blog> queryBlogChoose(Map map);
```

### Mapper.xml配置文件

```xml
 <select id="queryBlogChoose" parameterType="map" resultType="com.ylw.pojo.Blog">
        select * from mybatis.blog
        <where>
            <choose>
                <when test="title != null">
                    title = #{title}
                </when>
                <when test="author != null">
                    and title = #{author}
                </when>
                <otherwise>
                    and views = #{views}
                </otherwise>
            </choose>
        </where>
    </select>
```

### 测试

```java
@Test
    public void queryBlogChoose(){
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);

        HashMap map = new HashMap();
        map.put("title","java如此简单"); //这里由于choose语句只会执行第一个when
        map.put("author","狂神说");
        map.put("views",9999);

        List<Blog> blogs = mapper.queryBlogChoose(map);

        for (Blog blog : blogs) {
            System.out.println(blog);
        }

        sqlSession.close();
    }
```

![image-20210201200232433](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201200232.png)

## set标签

set去除逗号
![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201200317.png)

```java
//更新博客
    int updateBlog(Map map);
```

```xml
<update id="updateBlog" parameterType="map">
        update mybatis.blog
        <set>
            <if test="title!=null">
                title = #{title},
            </if>
            <if test="author!=null">
                author = #{author}
            </if>
        </set>
        where id =#{id}
    </update>
```

```java
 @Test
    public void updateBlog(){
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);

        HashMap map = new HashMap();
        map.put("title","JavaSE"); //这里由于choose语句只会执行第一个when
        map.put("author","狂神说");
        map.put("views",9999);
        map.put("id","652c250b75d342adbeb442d08d8f634a");

        int blogs = mapper.updateBlog(map);

        sqlSession.commit();
        sqlSession.close();
    }
```

![image-20210201201350188](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201201350.png)

![image-20210201201446326](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201201446.png)

![image-20210201201517715](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201201517.png)



## sql片段

有的时候，我们可能会将一些功能的部分抽取出来，方便复用！

1. 使用SQL标签抽取公共的部分

   ```xml
   <sql id="if-title-author">
       <if test="title != null">
           title = #{title}
       </if>
       <if test="author != null">
           and author = #{author}
       </if>
   </sql>
   ```

2. 在需要使用的地方使用Include标签引用即可

   ```xml
    <!--这里写where是为了便于后面的if拼接，并且当if都不符合的时候也可以确保查询语句正确,还可以写where标签-->
       <select id="queryBlogIf" parameterType="map" resultType="com.kuang.pojo.Blog">
           select * from mybatis.blog
           <where>
               <include refid="if-title-author"></include>
           </where>
       </select>
   ```

![image-20210201202625239](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201202625.png)

注意事项：

- 最好基于单表来定义SQL片段！
- sql标签里不要存在where标签

# 15.动态 SQL之foreach

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201202703.png)

```sql
select * from user where 1=1 and
<foreach item="id" index="index" co1lection="ids"
	open="(" separator="or" close=")">
		#{id}
</foreach>

(id=1 or id=2 or id=3)

```

## 接口

```java
//查询第1-2-3号
List<Blog> queryBlogForeach(Map map);
```

![image-20210201203732127](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201203732.png)

## Mapper配置文件

```xml
 <!--
       select * from mybatis.blog where 1=1 and (id=1 or id = 2 or id=3)
      相当于IN 
			我们现在传递一个万能的map ， 这map中可以存在一个集合！
-->
    <select id="queryBlogForeach" parameterType="map" resultType="com.kuang.pojo.Blog">
        select * from mybatis.blog
        <where>
            <foreach collection="ids" item="id" open="(" close=")" separator="or">
                id = #{id}
            </foreach>
        </where>
    </select>
```

## 测试

```java
 @Test
    public void queryBlogForeach(){
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);

        HashMap map = new HashMap();

        ArrayList<Integer> ids = new ArrayList<Integer>();
        ids.add(1);
        ids.add(2);

        map.put("ids",ids);

        List<Blog> blogs = mapper.queryBlogForeach(map);

        for (Blog blog : blogs) {
            System.out.println(blog);
        }

        sqlSession.close();
    }
```

![image-20210201204154050](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201204154.png)

==动态SQL就是在拼接SQL语句，我们只要保证SQL的正确性，按照SQL的格式，去排列组合就可以了==

建议：

- 现在Mysql中写出完整的SQL,再对应的去修改成为我们的动态SQL实现通用即可！

# 16.缓存

## 缓存简介

```
查询 ： 连接数据库 ，耗资源！
	一次查询的结果，给他暂存在一个可以直接取到的地方！--------->内存 ： 缓存
	
我们再次查询相同数据的时候，直接走缓存，就不用走数据库了
```

1. 什么是**缓存 [ Cache ]**？
   - 存在内存中的临时数据。
   - 将用户经常查询的数据放在缓存（内存）中，用户去查询数据就不用从磁盘上(关系型数据库数据文件)查询，从缓存中查询，从而提高查询效率，解决了高并发系统的性能问题。
2. 为什么使用缓存？
   - 减少和数据库的交互次数，减少系统开销，提高**系统效率（性能）**。
3. 什么样的数据能使用缓存？
   - **经常查询并且不经常改变**的数据。【可以使用缓存】

![image-20210201204607660](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201204607.png)

## Mybatis缓存

- MyBatis包含一个非常强大的查询缓存特性，它可以非常方便地**定制和配置缓存**。缓存可以极大的提升查询效率。
- MyBatis系统中默认定义了两级缓存：**一级缓存**和**二级缓存**
  - 默认情况下，只有**一级缓存开启**。（SqlSession级别的缓存，也称为**本地缓存**）
  - 二级缓存需要手动开启和配置，他是基于namespace级别的缓存，也称为**接口级别缓存**。
  - 为了提高扩展性，MyBatis定义了缓存接口Cache。我们可以通过实现**Cache接口**来自定义二级缓存
    - ![image-20210201204908215](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201204908.png)

## 一级缓存

==一级缓存默认是开启的，只在一次SqlSession中有效，也就是拿到连接到关闭连接这个区间段!==

一级缓存默认开启

- 一级缓存也叫本地缓存： SqlSession
  - 与数据库同一次会话期间查询到的数据会放在本地缓存中。
  - 以后如果需要获取相同的数据，直接从缓存中拿，没必须再去查询数据库；

### 开启日志

在mybatis核心配置文件中配置开启日志，便于查看缓存

```xml
    <settings>
        <!--配置日志-->
        <setting name="logImpl" value="STDOUT_LOGGING"/>
    </settings>
```

### 接口

```java
package com.kuang.dao;

import com.kuang.pojo.User;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/2/1 - 02 - 01 - 20:58
 * @Description: com.kuang.dao
 * @version: 1.0
 */
public interface UserMapper {
    //    根据ID查询用户
    User getUserById(int id );
}

```

### Mapper配置文件

```java
<?xml version="1.0" encoding="UTF8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--namespace命名空间，绑定一个对应的Dao或者说是Mapper接口-->
<!--这里namespace的值要改成自己的接口，可以理解为通过这个配置文件实现接口，
下面的标签都可以与接口实现类对应-->
<mapper namespace="com.kuang.dao.UserMapper">

<!--    结果集映射-->
    <resultMap id="UserMap" type="User">
<!--        column数据库中的字段，property实体类的属性-->
        <result column="id" property="id"></result>
        <result column="name" property="name"></result>
        <result column="pwd" property="password"></result>
    </resultMap>

    <!--根据ID查询用户-->
    <select id="getUserById" parameterType="int" resultMap="UserMap">
        select * from mybatis.user where id = #{id}
    </select>

</mapper>

```

### 测试

测试在一个Sesion中查询两次相同记录

```java
package com.kuang;

import com.kuang.dao.UserMapper;
import com.kuang.pojo.User;
import com.kuang.utils.MyBatisUtils;
import org.apache.ibatis.session.SqlSession;
import org.junit.Test;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/2/1 - 02 - 01 - 21:02
 * @Description: com.kuang
 * @version: 1.0
 */
public class MyTest {
    @Test
    public void getUserById(){
        //通过写的MyBatisUtils类里的getSqlSession()方法，获取sqlSession对象
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        //执行SQL语句
        UserMapper userMapper1 = sqlSession.getMapper(UserMapper.class);//UserMapper，返回接口实现类信息
        User user1 = userMapper1.getUserById(1);//执行口实现类的方法，即配置文件里的id
        System.out.println(user1);
//        ---------------------------
        //执行SQL语句
        UserMapper userMapper2 = sqlSession.getMapper(UserMapper.class);//UserMapper，返回接口实现类信息
        User user2 = userMapper2.getUserById(1);//执行口实现类的方法，即配置文件里的id
        System.out.println(user2);

        //比较两次查询结果
        System.out.println(user1==user2);

        //关闭sqlSession
        sqlSession.close();
    }
}

```

可以看到只预编译了一次sql语句
![image-20210201210955968](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201210956.png)

### 缓存失效的情况

![image-20210201205317988](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201205318.png)

1. 查询不同的东西
2. 增删改操作，可能会改变原来的数据，所以必定会刷新缓存！

![image-20210201205407402](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201205407.png)

​	3.查询不同的Mapper.xml

​	4.手动清理缓存！
![](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201211934.png)

## 二级缓存

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201211107.png)

![image-20210201211251858](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201211252.png)

- 二级缓存也叫全局缓存，一级缓存作用域太低了，所以诞生了二级缓存
- 基于namespace级别的缓存，一个名称空间，对应一个二级缓存；
- 工作机制
  - 一个会话查询一条数据，这个数据就会被放在当前会话的一级缓存中；
  - 如果当前会话关闭了，这个会话对应的一级缓存就没了；但是我们想要的是，会话关闭了，一级缓存中的数据被保存到二级缓存中；
  - 新的会话查询信息，就可以从二级缓存中获取内容；
  - 不同的mapper查出的数据会放在自己对应的缓存（map）中；

### 步骤一、开启全局缓存

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201211419.png)
默认开启，通常把它写出来，在mybatis核心配置文件中配置

```xml
<settings>
    <!--显示开启全局缓存-->
    <setting name="cacheEnabled" value="true"/>
    <!--配置日志-->
    <setting name="logImpl" value="STDOUT_LOGGING"/>
</settings>
```

### 在Mapper中使用二级缓存

```java
<!--在当前Mapper.xml中使用二级缓存-->
 <cache
            eviction="FIFO"
            flushInterval="60000"
            size="512"
            readOnly="true"/>
  

    <!--根据ID查询用户-->
    <select id="getUserById" parameterType="int" resultMap="UserMap" useCache="true">
        select *
        from mybatis.user
        where id = #{id}
    </select>
```

### 也可以给cache自定义参数

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201211432.png)

问题:我们需要将实体类序列化！否则就会报错！

```java
Caused by: java.io.NotSerializableException: com.kuang.pojo.User
```

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201212029.png)

```java
package com.kuang;

import com.kuang.dao.UserMapper;
import com.kuang.pojo.User;
import com.kuang.utils.MyBatisUtils;
import org.apache.ibatis.session.SqlSession;
import org.junit.Test;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/2/1 - 02 - 01 - 21:02
 * @Description: com.kuang
 * @version: 1.0
 */
public class MyTest {
    @Test
    public void getUserById(){
        //通过写的MyBatisUtils类里的getSqlSession()方法，获取sqlSession对象
        SqlSession sqlSession1 = MyBatisUtils.getSqlSession();
        SqlSession sqlSession2 = MyBatisUtils.getSqlSession();
        //执行SQL语句
        UserMapper userMapper1 = sqlSession1.getMapper(UserMapper.class);//UserMapper，返回接口实现类信息
        User user1 = userMapper1.getUserById(1);//执行口实现类的方法，即配置文件里的id
        System.out.println(user1);
        sqlSession1.close();

//        ---------------------------
        //执行SQL语句
        UserMapper userMapper2 = sqlSession2.getMapper(UserMapper.class);//UserMapper，返回接口实现类信息
        User user2 = userMapper2.getUserById(1);//执行口实现类的方法，即配置文件里的id
        System.out.println(user2);

        //比较两次查询结果
        System.out.println(user1==user2);

        //关闭sqlSession
        sqlSession2.close();
    }
}

```

![image-20210201212845389](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201212845.png)

小结：

- 只要开启了二级缓存，在同一个Mapper下就有效
- 所有的数据都会先放在一级缓存中；
- 只有当会话提交，或者关闭的时候，才会提交到二级缓存中！（转存的概念）



## 缓存原理

![image-20210201212914055](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201212914.png)

## 自定义缓存-ehcache

![image-20210201213157648](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210201213157.png)

要在程序中使用ehcache，先要导包！
maven依赖

```java
<!-- https://mvnrepository.com/artifact/org.mybatis.caches/mybatis-ehcache -->
<dependency>
    <groupId>org.mybatis.caches</groupId>
    <artifactId>mybatis-ehcache</artifactId>
    <version>1.2.1</version>
</dependency>
```

在mapper中指定使用我们的ehcache缓存实现！

```java
<!--在当前Mapper.xml中使用二级缓存-->
<cache type="org.mybatis.caches.ehcache.EhcacheCache"/>
```

新建配置文件ehcache.xml

```java
<?xml version="1.0" encoding="UTF8"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="http://ehcache.org/ehcache.xsd"
         updateCheck="false">
    <!--
       diskStore：为缓存路径，ehcache分为内存和磁盘两级，此属性定义磁盘的缓存位置。参数解释如下：
       user.home – 用户主目录
       user.dir  – 用户当前工作目录
       java.io.tmpdir – 默认临时文件路径
     -->
    <diskStore path="./tmpdir/Tmp_EhCache"/>

    <defaultCache
            eternal="false"
            maxElementsInMemory="10000"
            overflowToDisk="false"
            diskPersistent="false"
            timeToIdleSeconds="1800"
            timeToLiveSeconds="259200"
            memoryStoreEvictionPolicy="LRU"/>

    <cache
            name="cloud_user"
            eternal="false"
            maxElementsInMemory="5000"
            overflowToDisk="false"
            diskPersistent="false"
            timeToIdleSeconds="1800"
            timeToLiveSeconds="1800"
            memoryStoreEvictionPolicy="LRU"/>
    <!--
       defaultCache：默认缓存策略，当ehcache找不到定义的缓存时，则使用这个缓存策略。只能定义一个。
     -->
    <!--
      name:缓存名称。
      maxElementsInMemory:缓存最大数目
      maxElementsOnDisk：硬盘最大缓存个数。
      eternal:对象是否永久有效，一但设置了，timeout将不起作用。
      overflowToDisk:是否保存到磁盘，当系统当机时
      timeToIdleSeconds:设置对象在失效前的允许闲置时间（单位：秒）。仅当eternal=false对象不是永久有效时使用，可选属性，默认值是0，也就是可闲置时间无穷大。
      timeToLiveSeconds:设置对象在失效前允许存活时间（单位：秒）。最大时间介于创建时间和失效时间之间。仅当eternal=false对象不是永久有效时使用，默认是0.，也就是对象存活时间无穷大。
      diskPersistent：是否缓存虚拟机重启期数据 Whether the disk store persists between restarts of the Virtual Machine. The default value is false.
      diskSpoolBufferSizeMB：这个参数设置DiskStore（磁盘缓存）的缓存区大小。默认是30MB。每个Cache都应该有自己的一个缓冲区。
      diskExpiryThreadIntervalSeconds：磁盘失效线程运行时间间隔，默认是120秒。
      memoryStoreEvictionPolicy：当达到maxElementsInMemory限制时，Ehcache将会根据指定的策略去清理内存。默认策略是LRU（最近最少使用）。你可以设置为FIFO（先进先出）或是LFU（较少使用）。
      clearOnFlush：内存数量最大时是否清除。
      memoryStoreEvictionPolicy:可选策略有：LRU（最近最少使用，默认策略）、FIFO（先进先出）、LFU（最少访问次数）。
      FIFO，first in first out，这个是大家最熟的，先进先出。
      LFU， Less Frequently Used，就是上面例子中使用的策略，直白一点就是讲一直以来最少被使用的。如上面所讲，缓存的元素有一个hit属性，hit值最小的将会被清出缓存。
      LRU，Least Recently Used，最近最少使用的，缓存的元素有一个时间戳，当缓存容量满了，而又需要腾出地方来缓存新的元素的时候，那么现有缓存元素中时间戳离当前时间最远的元素将被清出缓存。
   -->

</ehcache>
```

实际中都用非关系数据库（Redis）来做缓存！ K-V键值对