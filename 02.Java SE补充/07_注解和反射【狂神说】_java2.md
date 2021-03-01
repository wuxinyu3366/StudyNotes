# 注解Annotation

# 一、注解概念

- Annotation是从JDK5.0开始引入的新技术
- Annotation的作用：
  - 可以对程序作出解释，这一点和(注释comment)类似
  - 对程序进行检查和约束，例如@Override
  - ==可以被其他程序（比如：编译器等）读取==
- Annotation的格式：
  - 注解是以“`@注释名`”在代码中存在的，还可以添加一些参数值，例如：@SuppressWarning(value=”unchecked”)
- Annotation在哪里使用？
  - 可以附加在package、class、method、field等上面，相等于给他们添加了**额外的辅助信息**，然后结合==**反射机制**==实现对这些**元数据的访问**



# 二、内置注解

`@override`:定义重写声明

定义在java.lang包中，此注解只适用于修饰方法，表示该方法打算重写父类中的同名方法，并且具有检查作用

![image-20210116173847494](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116173847494.png)

`@Deprecated`：表示不鼓励使用

定义在java.lang包中，此注释可以修饰方法、属性、类，注释@Deprecated的程序元素是程序员不鼓励使用的程序元素，通常是因为它

是危险的，或者因为它已经过时了，然后存在更好的替代方法，但是你使用也没有任何影响，使用案例如下：

![image-20210116173907272](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116173907272.png)

`@SuppressWarnings`：抑制警告(灰色)信息

定义在java.lang包中，用来抑制编译时产生的黄色警告信息，虽然这些警告信息不会影响编译结果，但是看着不舒服，然后该注释和前两

个注释有所不同，你需要添加一个参数才能正确使用，这些参数都是已经定义好了的，具体参数信息如下所示：

​	使用需要参数 参数已经定义好了 选择使用即可

​	1.`@SuppressWarnings（“all”）`// 压制所有警告

​	2.`@SuppressWarnings（“unchecked”）`// 压制"unchecked"警告

​	3.`@SuppressWarnings（value={“unchecked”,“deprecation”}）`// 压制"unchecked", "deprecation"警告

![image-20210116174035679](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116174035679.png)

```java
package com.kuang.lesson01;

import java.util.ArrayList;
import java.util.List;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 17:36
 * @Description: com.kuang.lesson01
 * @version: 1.0
 */
public class Test01 extends Object{
    //@Override 重写的注解
    @Override
    public String toString() {
        return "Demo01{}";
    }
    
    //@Deprecated 不推荐程序员使用 但是可以使用 一般有更好的方法
    @Deprecated
    public  static void test(){
        System.out.println("Deprecated");
    }
    @SuppressWarnings("all") //下方未使用的警告不再提示
    public  static void test02(){
        List list = new ArrayList();
    }

    public static void main(String[] args) {
        test();
    }
}

```

# 三、元注解 meta-annotation

- 元注解作用：负责**注解其他注解**，Java中定义了4个标准的元注解（`meta-annotation`）类型，他们被用来对其他`Annotation`注解类型进行解释说明限制

- 元注解位置：在java.lang.annotation包中

- 元注解四大类型

  - **@Target**：用于描述注解的使用范围，也就是描述注解**可以使用在什么地方**，`public @interface Target {ElementType[] value();}`可以看出可以它是一个数组，可以有多个值，里面的值设置的都是定义的注解MyAnnotation的使用范围，比如在类上、方法上等等，你可以通过@Target，然后点击里面的ElementType去查看

  ![image-20210116174149974](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116174149974.png)

  - `@Retention`：表示需要在什么级别保存该注释信息，用于描述注解的**生命周期**==（SOURCE < CLASS < **RUNTIME**）==，SOURCE是源码级别，CLASS 是源码级别和编译之后的字节码文件中有效，RUNTIME是在源码级别、编译之后的字节码文件、JVM中运行都有效，最常用的就是RUNTIME

  ![在这里插入图片描述]![image-20210116174203700](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116174203700.png)

  - `@Documented`：说明该注解将被包含在javadoc文档中

  ![image-20210116174215140](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116174215140.png)

  - `@Inherited`：说明子类可以继承父类中的该注解

  ![image-20210116174225906](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116174225906.png) 

```java
package com.kuang.lesson01;

import java.lang.annotation.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 17:49
 * @Description: com.kuang.lesson01
 * @version: 1.0
 */
@MyAnnotation
public class Test02 {
    @MyAnnotation
    public void test(){

    }
}

//定义一个注解
//Target 表示我们的注解可以用在那些地方  值为ElementType枚举中的方法和类
@Target(value = {ElementType.METHOD,ElementType.TYPE})

//Retention 表示我们的注解在什么地方有效
//runtime>class>sources
    @Retention(value = RetentionPolicy.RUNTIME)

//Documented 表示是否将我们的注解生成在JAVADOC当中
    @Documented

//Inherited 子类可以继承父类的注解
    @Inherited
@interface MyAnnotation{
}

```



# 四、自定义注解 @interface

- 使用@interface自定义注解时，自动继承了java.lang.annotation.Annotation接口

- @interface 用来声明一个注解，格式是：

  ```java
  修饰符 @interface 注解名{定义内容}
  ```

  - 内容中的每一个**方法**实际上是声明了一个**配置参数**，方法的名称就是参数的名称，方法的返回值类型就是参数的类型

  - 返回值类型只能是基本类型、Class、String、enum，如果返回值是String[]的时候，赋值的时候要用{“X1”, “X2”}这种形式；

  - 可以通过default来声明参数的默认值，声明默认值的可以不在自定义注解中赋值，反之必须赋值

  - 如果只有一个参数成员，一般参数名使用value字段，这是因为当参数名称是value并且自定义注解中只需要写一个参数的时候，可以省略参数名称，只有value可以这样，其他的都不行

  - 注解元素必须有值，我们定义注解元素时，经常使用空字符串、0、-1等作为默认值，当默认值为-1，代表不存在

![image-20210116174321055](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116174321055.png)



```java
package First;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

public class Test03 {
  //注解可以显示赋值，如果没有默认值，我们必须要给注解赋值
    @MyAnnotation03(name="当场注解")
    @MyAnnotation02(age = 10,name = "alin")//参数顺序可以调换 必许带参数名
    public void test03(){
        
    }
    
}

@Target({ElementType.TYPE,ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@interface MyAnnotation02{
    //参数定义 参数类型 参数名()
    String name() default "";//default 进行默认赋值
    int age() default 0;
    int id()  default -1;//如果默认值为-1，则表示不存在
    String[] students() default {"青岛大学","南京邮电大学" };
}

@Target({ElementType.TYPE,ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@interface  MyAnnotation03{
    String value();//一个参数时 最好命名为value 命名为value时 在使用此注解时可以不加value
}
```

# 反射Reflection

**动态语言**

- 是一类在**运行时可以改变其结构**的语言:例如新的函数、对象、甚至代码可以被引进，已有的函数可以被删除或是其他结构上的变化。通俗点说就是在运行时代码可以根据某些条件改变自身结构。
- 主要动态语言:Object-C、C#、JavaScript、PHP、Python等。
- ![image-20210116180639090](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116180639090.png)

**静态语言**

- 与动态语言相对应的，**运行时结构不可变**的语言就是静态语言。如Java、C、C++。
- Java不是动态语言，但Java可以称之为“**准动态语言**”。即Java有一定的动态性，我们可以利用**反射机制**获得类似**动态语言**的特性。Java的动态性让编程的时候更加灵活!

# 一、反射概念

- Reflection(反射)是Java被视为**动态语言**的关键，反射机制允许程序在执行期间借助于**Reflection API**取得任何**类的内部信息**，并且能**直接操作任意对象的内部属性以及方法**

  ```java
  Class c = Class.forName("java.lang.String")
  ```

- 加载完类之后，在**堆内存**的方法区中就产生了一个**Class类型**的对象（一个类只有一个Class对象），这个对象就包含了完整的类的结构信息。我们可以通过这个对象看到类的结构，这个对象就像一面镜子，透过这个镜子可以看到类的结构，这就是反射

![image-20210116180821051](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116180821051.png)

# 二、获取反射对象

## 反射机制提供的功能

- 在运行时判断任意一个对象所属的类
- 在运行时构造任意一个类的对象
- 在运行时判断任意一个类所具有的成员变量和方法
- 在运行时获取泛型信息
- 在运行时调用任意一个对象的成员变量和方法
- 在运行时处理注解
- 生成动态代理
- ……

## 反射的优点和缺点

优点:

- 可以实现**动态**创建对象和编译，体现出很大的灵活性

缺点:

- 对性能有影响。使用反射基本上是一种解释操作，我们可以告诉JVM，我们希望做什么并且它满足我们的要求。这类操作总是慢于直接执行相同的操作。

## 反射相关的主要API

- `java.lang.Class`：代表一个类，它就是Object类getClass()方法的返回值，它是唯一的所以类都指向它
- `java.lang.reflect.Method`：代表类的方法
- `java.lang.reflect.Field`：代表类的成员变量
- `java.lang.reflect.Constructor`：代表类的构造器
- ……

## 反射初体验

```java
package com.kuang.lesson02;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 18:13
 * @Description: com.kuang.lesson02
 * 什么叫反射
 * @version: 1.0
 */
public class Test01 {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) throws ClassNotFoundException {
        // 通过反射返回类的Class对象，这里的Class就是Object类中getClass()方法的返回值Class是一样的，获取的c1是Class类的对象
        Class c1 =  Class.forName("com.kuang.lesson02.User");
        System.out.println(c1);

        // 一个类在方法区中只有一个Class对象
        // 一个类被加载之后，类的整个结构(构造器、方法、属性等等)都会被封装在Class对象中
        Class c2 =  Class.forName("com.kuang.lesson02.User");
        System.out.println(c1.hashCode());
        System.out.println(c2.hashCode());
    }
}

//实体类 poji entity
class User{
    private Integer id;
    private String name;
    private Integer age;

    public User(Integer id, String name, Integer age) {
        this.id = id;
        this.name = name;
        this.age = age;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }
}
```

![image-20210116181821835](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116181821835.png)



## Class类详解

![image-20210116182104254](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116182104254.png)

# 三、得到Class类的几种方式

## 1.Class类

对象照镜子后可以得到的信息:某个类的**属性、方法和构造器**、某个类到底实现了哪些**接口**。对于每个类而言，`JRE `都为其保留一个不变的Class类型的对象。一个Class对象包含了特定某个结构(`class`、`interface`、`enum`、`annotation`、`primitive type`、`void`、`[]`)的有关信息。

- Class本身也是一个类，不过这个类只有一个，所有的类都执行它，例如User类、Person类等

- Class对象是Class类的对象，一个加载的类(例如User.java)在JVM中只会有一个Class对象

- 一个Class对象对应的是一个加载到JVM中的对应的XXX.class文件

- 每个类(例如User.java)的实例(例如User u = new User()中的u)都会**记着自己是由哪个Class对象**所生成

- 通过CLass对象可以完整地得到一个类(例如User.java)中所有被加载的信息

- Class类(只有一个，和Object类中getClass()方法中返回的Class是同一个)是**Reflection的根源**，针对任何你想动态加载、运行的类、唯有先获得类(例如User.java)对应的Class对象

- 以上说了三个部分：Class类、Class对象、类、类的实例，通过类可以创建类的实例，通过Class类可以获取某类的Class对象，通过Class对象可以获取类中的所有信息(方法、属性等等)，当然也可以创建类的实例，另外Class对象是类具有的，类可以做的它也能做

  

## 2.Class类的常用方法

![image-20210116182557940](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116182557940.png)
![image-20210116182625454](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116182625454.png)

## 3.获取Class类的实例

1.通过类的class属性获取，该方法最为安全可靠，程序性能最高

```java
Class c1 = User.class;
```

2.通过类的实例中的getClass()方法获取

```java
Class c2 = user.getClass();
```

3.通过类的全限定类名获取

```java
Class c3 = Class.forName("com.kuang.lesson02.Student");
```

4通过基本内置类型的包装类的Type属性（了解）

```java
Class c4 = Integer.TYPE;
```
5.获得父类类型

```java
Class c5 = c1.getSuperclass();
```



1. 通过ClassLoader类加载器获取

```java
Constructor constructor = c1.getDeclaredConstructor(String.class);
Class c5 = constructor.getDeclaringClass();
System.out.println(c5.hashCode());
```



```java
package com.kuang.lesson02;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 18:32
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class Test02 {
    public static void main(String[] args) throws ClassNotFoundException {
        Person person = new Student();
        System.out.println("这个人是:"+person.name);
        //通过对象获得class
        Class c1 = person.getClass();
        System.out.println(c1.hashCode());
        //通过类获得class
        Class c2 = Student.class;
        System.out.println(c2.hashCode());
        //通过forname获得class
        Class c3 = Class.forName("com.kuang.lesson02.Student");
        System.out.println(c3.hashCode());
        //通过内置函数的包装类获得class
        Class c4 = Integer.TYPE;
        System.out.println(c4);
        //获得父类的class
        Class c5 = c1.getSuperclass();
        System.out.println(c5);

    }
}

class Person{
    public String name;

    public Person() {
    }

    public Person(String name) {
        this.name = name;
    }
}
class Student extends Person{
    public Student() {
        this.name="学生";
    }
}
class Teacher extends  Person{
    public Teacher() {
        this.name = "教师";
    }
}


```

![image-20210116183321907](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116183321907.png)

## 4.哪些类型可以有Class对象

`class:外部类`，成员(成员内部类，静态内部类)，局部内部类，匿名内部类

`interface`:接口

`[]`数组

`enum`:枚举

`annotation`:注解@interface

`primitive type`: 基本数据类型

`void`

```java
package com.kuang.lesson02;

import java.util.Enumeration;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 18:52
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class Test03 {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {

        Class c1 = Object.class;		//类
        Class c2 = Comparable.class;//接口
        Class c3 = String[].class;//一维数组
        Class c4 = int[][].class;//二维数组
        Class c5 = Enumeration.class;//枚举
        Class c6 = Integer.class;//基本数据类型
        Class c7 = Override.class;//注解
        Class c8 = Void.class;//void
        Class c9 = void.class;//void
        Class c10 = Class.class;//Class
        System.out.println(c1 );
        System.out.println(c2 );
        System.out.println(c3 );
        System.out.println(c4 );
        System.out.println(c5 );
        System.out.println(c6 );
        System.out.println(c7 );
        System.out.println(c8 );
        System.out.println(c9 );
        System.out.println(c10);

        //当类型和维数相同时只有一个class对象
        int[] a = new int[10];
        int[] b = new int[100];
        System.out.println(a.getClass().hashCode());
        System.out.println(b.getClass().hashCode());

    }
}

```

![image-20210116185248129](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116185248129.png)



### 元素类型、维度和Class对象的关系

```java
public class Test {
    public static void main(String[] args) {
        Class c1 = int[].class; // 一维整型数组
        Class c2 = int[][].class; // 二维整型数组
        Class c3 = String[].class; // 一维字符串数组
        int[] i1 = new int[10]; // 初值容量为10的一维整型数组
        int[] i2 = new int[100]; // 初始容量为100的一维整型数组

        System.out.println("一维整型数组：" + c1.hashCode());
        System.out.println("二维整型数组：" + i1.getClass().hashCode());
        System.out.println("一维字符串数组：" + i2.getClass().hashCode());
        System.out.println("初值容量为10的一维整型数组：" + c2.hashCode());
        System.out.println("初始容量为100的一维整型数组：" + c3.hashCode());
    }
}
```

![image-20210116201950397](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116201950397.png)

结论：

1. 元素类型不同，Class对象不同，例如int[ ]、String[ ]
2. 元素类型相同，但是维度不同，Class对象不同，例如int[ ]和int[  ][ ]
3. 元素类型相同，维度相同，但是具体内容不同，Class对象相同，例如：int[10]和int[100]

## 5.类加载内存分析

![image-20210116191320528](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116191320528.png)

![image-20210116191401478](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116191401478.png)

![image-20210116191447222](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116191447222.png)

加载时

![image-20210116191718804](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116191718804.png)

链接时

![image-20210116191120820](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116191120820.png)

初始化

![image-20210116191154856](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116191154856.png)

```java
package com.kuang.lesson02;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 19:21
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class Test04 {
    public static void main(String[] args) {
        A a = new A();
        System.out.println(A.m);

    }
}
/*
    1.加载到内存，会产生一个类对应Class对象在堆区
    2.链接，在栈中产生 main m=0;
    3.初始化
    <clinit>{
    System.out.println("A类静态代码块初始化");
        m=300;
        m=100;  静态 按顺序执行的 若把 int m =100 ;放上面 则为300；
        }

 */

class A{
    static {
        System.out.println("A类静态代码块初始化");
        m=300;
    }
    /*
    m=300;
    m=100; 覆盖上方300
     */
    static int m =100;

    public A() {
        System.out.println("A类的无参构造器");
    }
}

```

![image-20210116192204059](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116192204059.png)

## 6.什么时候会发生类的初始化

类的**主动引用(一定会发生类的初始化)**

- 当虚拟机启动，先初始化main方法所在的类
- new一个类的对象
- 调用类的静态成员(除了final常量)和静态方法
- 使用java.lang.reflect包的方法对类进行**反射**调用
- 当初始化一个类，如果其父类没有被初始化，则**先会初始化它的父类**



类的**被动引用(不会发生类的初始化)**

- 当访问一个静态域时，只有真正声明这个域的类才会被初始化。如:当通过子类引用父类的静态变量，不会导致子类初始化
- 通过数组定义类引用，不会触发此类的初始化
- 引用常量不会触发此类的初始化（常量在链接阶段就存入调用类的常量池中了)

```java
package com.kuang.lesson02;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 19:24
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class Test05 {
    static {
        System.out.println("Main类被调用了");
    }

    public static void main(String[] args) throws ClassNotFoundException {
        //----------------主动引用------------------
        //1.创建对象 若父类没初始化 先初始化父类
        //Son son = new Son();
        /*
        Main类被调用了
        父类被加载
        子类被加载了
        100
         */
        //2.通过反射
        //Class c1 = Class.forName("com.kuang.lesson02.Son");//Main类被调用  父类被加载  子类被加载了
        //3.调用静态
        //System.out.println(Son.m);//Main类被调用了 父类被加载 子类被加载了 200
        /*
        Main类被调用了
        父类被加载
        子类被加载了
        200
        * */

        //----------------被动引用-----------------
        //被动引用
        //子类引用父类静态变量，子类不加载
        //System.out.println(Son.b);//Main类被调用了 父类被加载 100
        //数组定义类引用  只有main类加载
        //Son[] a1 = new Son[5]; //Main类被调用了
        //引用常量
        //System.out.println(Son.M);      //Main类被调用了 1

    }
}

class Father {
    static {
        System.out.println("父类被加载");
        //int b=10;
    }

    static int b = 100;
}

class Son extends Father {
    static {
        System.out.println("子类被加载了");
        m = 300;
    }

    static int m = 200;
    static final int M = 1;
}

```

## 7.类加载器

**类加载的作用**:将class文件字节码内容加载到内存中，并将这些静态数据转换成方法区的运行时数据结构，然后在堆中生成一个代表这个类的**java.lang.Class对象**，作为方法区**中类数据的访问入口**。

**类缓存**:标准的JavaSE类加载器可以按要求查找类，但一旦某个类被加载到类加载器中，它将维持**加载（缓存)一段时间**。不过JVM垃圾回收机制可以回收这些Class对象

![image-20210116193117780](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116193117780.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201111081304313.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMjAzMjQ2,size_16,color_FFFFFF,t_70#pic_center)

```java
package com.kuang.lesson02;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 19:35
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class Test06 {
    public static void main(String[] args) throws ClassNotFoundException {
    //获得系统类加载器
    ClassLoader systemClassLoader = ClassLoader.getSystemClassLoader();
    System.out.println(systemClassLoader);
    //获得系统类加载器的父类-->扩展类加载器
    ClassLoader parent = systemClassLoader.getParent();
    System.out.println(parent);
    //获得扩展类加载器的父类-->根加载器（c/c++）无法直接获得
    ClassLoader parentparent = parent.getParent();
    System.out.println(parentparent);
    
    //测试当前类由哪个加载器产生
    ClassLoader classLoader = Class.forName("com.kuang.lesson02.Test06").getClassLoader();
    System.out.println(classLoader);
    
    //测试jdk类
    classLoader = Class.forName("java.lang.Object").getClassLoader();
    System.out.println(classLoader);
    //如何获得系统类加载器的加载路径
    System.out.println(System.getProperty("java.class.path"));
        /*
        D:\Java\jdk1.8.0_261\jre\lib\charsets.jar;
        D:\Java\jdk1.8.0_261\jre\lib\deploy.jar;
        D:\Java\jdk1.8.0_261\jre\lib\ext\access-bridge-64.jar;
        D:\Java\jdk1.8.0_261\jre\lib\ext\cldrdata.jar;
        D:\Java\jdk1.8.0_261\jre\lib\ext\dnsns.jar;
        D:\Java\jdk1.8.0_261\jre\lib\ext\jaccess.jar;
        D:\Java\jdk1.8.0_261\jre\lib\ext\jfxrt.jar;
        D:\Java\jdk1.8.0_261\jre\lib\ext\localedata.jar;
        D:\Java\jdk1.8.0_261\jre\lib\ext\nashorn.jar;
        D:\Java\jdk1.8.0_261\jre\lib\ext\sunec.jar;
        D:\Java\jdk1.8.0_261\jre\lib\ext\sunjce_provider.jar;
        D:\Java\jdk1.8.0_261\jre\lib\ext\sunmscapi.jar;
        D:\Java\jdk1.8.0_261\jre\lib\ext\sunpkcs11.jar;
        D:\Java\jdk1.8.0_261\jre\lib\ext\zipfs.jar;
        D:\Java\jdk1.8.0_261\jre\lib\javaws.jar;
        D:\Java\jdk1.8.0_261\jre\lib\jce.jar;
        D:\Java\jdk1.8.0_261\jre\lib\jfr.jar;
        D:\Java\jdk1.8.0_261\jre\lib\jfxswt.jar;
        D:\Java\jdk1.8.0_261\jre\lib\jsse.jar;
        D:\Java\jdk1.8.0_261\jre\lib\management-agent.jar;
        D:\Java\jdk1.8.0_261\jre\lib\plugin.jar;
        D:\Java\jdk1.8.0_261\jre\lib\resources.jar;
        D:\Java\jdk1.8.0_261\jre\lib\rt.jar;
        D:\Program Files\IDEA\IntelliJ IDEA Community Edition 2020.2.2\Annotation\out\production\Annotation;
        D:\Program Files\IDEA\IntelliJ IDEA Community Edition 2020.2.2\lib\idea_rt.jar
         */
    //双亲委派机制
    //当你定义的与根加载器中有类重复 为保证安全 仍使用根加载器中的类(向上检索)
}

}

```

![image-20210116193933918](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116193933918.png)

双亲委派机制: 当某个类加载器需要加载某个`.class`文件时，它首先把这个任务委托给他的**上级类加载器**，递归这个操作，如果上级的类加载器没有加载，自己才会去加载这个类。

![img](https://img-blog.csdnimg.cn/img_convert/927c9f30a2a646a501593535e8150302.png)

## 8.获取类的运行的完整结构

通过反射获取运行时类的完整结构

`Field`、`Method`、`Constructor`、`Superclass`、`Interface`、`Annotation`

- 实现的全部接口
- 所继承的父类
- 全部的构造器
- 全部的方法
- 全部的Field
- 注解
- ......



```java
package com.kuang.lesson02;

import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.Method;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 19:49
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
//获得类的信息
public class Test07 {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) throws Exception {
        Class c1 = Class.forName("com.kuang.lesson02.User");

        //User user = new User();
        //c1 =User.Class();

        //------------获得类的名字------------
        System.out.println("------------获得类的名字------------");
        System.out.println(c1.getName());//获取包名+类名
        System.out.println(c1.getSimpleName());//获取类名

        //------------获取属性Field------------
        System.out.println("------------获取属性------------");
        Field[] fields = c1.getFields();//只能获得public属性
        for (Field field:fields) {
            System.out.println(field);
        }
        fields = c1.getDeclaredFields();//获得全部属性
        for (Field field:fields) {
            System.out.println(field);
        }
        //获得指定属性
        System.out.println(c1.getDeclaredField("name"));

        //------------获取方法Method------------
        System.out.println("------------获取方法------------");
        //获取方法
        Method[] methods = c1.getMethods();//获得当前类与父类的public方法
        for (Method method : methods) {
            System.out.println("正常的"+method);
        }
        methods =c1.getDeclaredMethods();//获得当前类的所有方法
        for (Method method : methods) {
            System.out.println("getDeclaredMethods"+method);
        }
        //------------获得指定方法------------
        //加参数 处理重载
        System.out.println(c1.getMethod("getId",null));
        System.out.println(c1.getMethod("setName", String.class));//含参数需指定

        //------------获取构造器Constructor------------
        System.out.println("------------获取构造器------------");
        Constructor[] constructors = c1.getConstructors();//获得public构造器
        for (Constructor constructor : constructors) {
            System.out.println(constructor);
        }
        constructors = c1.getDeclaredConstructors();//获得全部构造器
        for (Constructor constructor : constructors) {
            System.out.println(constructor);
        }
        //获得指定构造器
     System.out.println(c1.getConstructor(Integer.class,String.class,Integer.class));

    }
}

```

![image-20210116195918357](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116195918357.png)

![image-20210116195932764](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116195932764.png)

# 四、Class作用

## 有了Class对象，能做什么？

创建类的对象 : 调用Class对象的==`newlnstance()`==方法

- 1）类必须有一个无参数的构造器
- 2 ) 类的构造器的访问权限需要足够

**思考**?难道没有无参的构造器就不能创建对象了吗?只要在操作的时候明确的调用类中的构造器，并将参数传递进去之后，才可以**实例化操作**。

步骤如下:

- 1）通过Class类的`getDeclaredConstructor(Class ... parameterTypes)`取得本类的指定形参类型的构造器
- 2 )  向构造器的形参中传递一个对象数组进去，里面包含了构造器中所需的各个参数。
- 3 )  通过`Constructor`实例化对象



## 动态创建对象

![image-20210116201259837](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116201259837.png)

![image-20210116201334216](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116201334216.png)

![image-20210116201351428](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116201351428.png)

```java
package com.kuang.lesson02;

import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.Method;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 20:14
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class Test08 {
    public static void main(String[] args) throws Exception {
        Class c1 = Class.forName("com.kuang.lesson02.User");

        //1.反射得到对象
        User user = (User) c1.newInstance();//调用无参构造器 new一个对象  高版本此方法已过时 使用c1.getDeclaredConstructor().newInstance()
        System.out.println(user);

        //2.使用构造器
        Constructor constructor = c1.getDeclaredConstructor(Integer.class,String.class,Integer.class);
        User user1=(User)constructor.newInstance(18,"小米",001);
        System.out.println(user1);

        //3.1反射调用普通方法
        User user2= (User) c1.newInstance();
        //通过反射获取一个方法
        Method setName = c1.getMethod("setName",String.class);
        //invoke 激活 （对象，"方法的值"）
        setName.invoke(user2,"ck");
        System.out.println(user2.getName());

        //3.2通过反射操作属性
        System.out.println("==========");
        User user3=(User)c1.newInstance();
        Field name = c1.getDeclaredField("name");
     		 //关闭安全检测 对私有属性可以操作
        name.setAccessible(true);
        name.set(user3,"小小");
        System.out.println(user3.getName());

    }
}

```

![image-20210116201714391](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116201714391.png)

# 五、性能检测

```java
package com.kuang.lesson02;

import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 20:21
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class Test10 {
    //普通调用
    public static void test01() {
        User user = new User();
        long startTime = System.currentTimeMillis();
        for (int i = 0; i < 1000000000; i++) {
            user.getName();
        }
        long endTime = System.currentTimeMillis();
        System.out.println("普通调用10亿次耗费" + (endTime - startTime) + "ms");
    }

    //反射调用
    public static void test02() throws NoSuchMethodException, InvocationTargetException, IllegalAccessException {
        User user = new User();
        Class c1 = user.getClass();
        Method getName = c1.getDeclaredMethod("getName", null);
        long startTime = System.currentTimeMillis();
        for (int i = 0; i < 1000000000; i++) {
            getName.invoke(user, null);
        }
        long endTime = System.currentTimeMillis();
        System.out.println("反射调用10亿次耗费" + (endTime - startTime) + "ms");
    }

    //关闭安全检测
    public static void test03() throws NoSuchMethodException, InvocationTargetException, IllegalAccessException {
        User user = new User();
        Class c1 = user.getClass();
        Method getName = c1.getDeclaredMethod("getName", null);
        getName.setAccessible(true);
        long startTime = System.currentTimeMillis();
        for (int i = 0; i < 1000000000; i++) {
            getName.invoke(user, null);
        }
        long endTime = System.currentTimeMillis();
        System.out.println("关闭安全检测后反射调用10亿次耗费" + (endTime - startTime) + "ms");
    }

    public static void main(String[] args) throws NoSuchMethodException, IllegalAccessException, InvocationTargetException {
        test01();
        test02();
        test03();
    }


}
```

![image-20210116202519623](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116202519623.png)

可以看出 反射的方式调用 耗时较久

# 六、获取泛型

**反射操作泛型**

Java采用**泛型**擦除的机制来引入泛型,Java中的泛型仅仅是给编译器javac使用的,确保**数据的安全性**和**免去强制类型转换**问题，但是，一旦编译完成,所有和泛型有关的类型全部擦除.

为了通过反射操作这些类型，Java新增了`ParameterizedType` , `GenericArrayType` ,`TypeVariable`和 `WildcardType`几种类型来代表不能被归一到Class类中的类型但是又和原始类型齐名的类型.

`ParameterizedType`:表示一种**参数化类型**,比如Collection<String>

`GenericArrayType`:表示一种**元素类型**是参数化类型或者类型变量的数组类型

`TypeVariable` :是各种**类型变量**的公共父接口

`WildcardType`:代表一种**通配符类型**表达式

```java
package com.kuang.lesson02;

import java.lang.reflect.Method;
import java.lang.reflect.ParameterizedType;
import java.lang.reflect.Type;
import java.util.List;
import java.util.Map;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 20:30
 * @Description: com.kuang.lesson02
 *通过反射获得泛型
 * @version: 1.0
 */
public class Test11 {
    public void test01(Map<String ,User> map, List<String> list){
        System.out.println("这不重要");
    }
    public  Map<String ,User> test02(){
        System.out.println("这不重要");
        return null;
    }
		
  	//获得泛型
    public static void main(String[] args) throws NoSuchMethodException {
      //根据参数值先获得方法
        Method method = Test11.class.getDeclaredMethod("test01",Map.class,List.class);
      //根据方法获得方法中的参数化类型
        Type[] genericParameterTypes = method.getGenericParameterTypes();
      、
        for (Type genericParameterType : genericParameterTypes) {
            System.out.println(genericParameterType);
          //判断是否为参数化类型，如果是，将其强制转化为参数化类型，就可以调用getActualTypeArguments获得真实的类型的方法
            if(genericParameterType instanceof ParameterizedType){
                Type[] actualTypeArguments = ((ParameterizedType) genericParameterType).getActualTypeArguments();
                for (Type actualTypeArgument : actualTypeArguments) {
                    System.out.println(actualTypeArgument);
                }

            }
        }
        System.out.println("=========================");
      //方法没有参数列表，
        method = Test11.class.getDeclaredMethod("test02",null);
      //获得一个返回值式泛型，只有一个
        Type genericReturnType = method.getGenericReturnType();
      //不用遍历判断
        if(genericReturnType instanceof ParameterizedType){
            Type[] actualTypeArguments = ((ParameterizedType) genericReturnType).getActualTypeArguments();
            for (Type actualTypeArgument : actualTypeArguments) {
                System.out.println(actualTypeArgument);
            }

        }
    }
}

```

![image-20210116203039851](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116203039851.png)

# 七、通过反射获得注解

![image-20210116203105167](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116203105167.png)

![image-20210116203118226](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116203118226.png)

```java
package com.kuang.lesson02;

import java.lang.annotation.*;
import java.lang.reflect.Field;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 20:34
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class Test12 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchFieldException {
        Class c1 = Class.forName("com.kuang.lesson02.Student2");

        //获得类的注解
        System.out.println("获得类的注解");
        Annotation[] annotations = c1.getAnnotations();
        for (Annotation annotation : annotations) {
            System.out.println(annotation);
        }

        //获得注解的值
        System.out.println("获得注解的值");
        Typekang typekang = (Typekang) c1.getAnnotation(Typekang.class);
        String value = typekang.value();
        System.out.println(value);

        //获得指定注解的值
        System.out.println("获得指定注解的值");
        Field field = c1.getDeclaredField("name");  //根据属性获得属性
        Fieldkang fieldkang = field.getAnnotation(Fieldkang.class);         //获得注解
        System.out.println(fieldkang.columname());
        System.out.println(fieldkang.type());
        System.out.println(fieldkang.length());
    }

}

@Typekang("db_Student")
class Student2 {
  	//数据库就可以根据注解操作表
    @Fieldkang(columname = "db_name", type = "varchar", length = 10)
    private String name;
    @Fieldkang(columname = "db_age", type = "int", length = 10)
    private int age;
    @Fieldkang(columname = "db_id", type = "int", length = 10)
    private int id;

    public Student2(String name, int age, int id) {
        this.name = name;
        this.age = age;
        this.id = id;
    }

    public Student2() {
    }

    @Override
    public String toString() {
        return "Student2{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", id=" + id +
                '}';
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

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }
}

//类的注解
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@interface Typekang {
    String value();
}

//属性的注解
@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
@interface Fieldkang {
    String columname();

    String type();

    int length();
}

```

![image-20210116204005026](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116204005026.png)