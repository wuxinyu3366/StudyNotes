# 一、面向过程和面向对象的区别

**面向过程**：当事件比较简单的时候，利用面向过程，注重的是事件的具体的**步骤/过程**，注重的是过程中的**具体的行为**，以**函数**为最小单位，考虑**怎么**做。

**面向对象**：注重找“**参与者**”,将功能封装进对象，强调具备了功能的对象，以**类/对象**为最小单位，考虑**谁**来做。

案例：
人把大象装进冰箱：
面向过程：
函数1：打开冰箱(){人站在冰箱前，打开冰箱，冰箱卡到30度角的时候，冰箱的灯打开了.........}
函数2：储存大象(){大象先迈左腿，再迈右退，考虑冰箱能不能装下......}
函数3：关闭冰箱(){人站在冰箱前，关闭冰箱，冰箱开到30度角的时候，冰箱的灯关闭了..........}

面向对象：

```
人{
        打开(冰箱){
                 冰箱.打开();
        }

        存储(大象){
        大象.进入();
                }


  关闭(冰箱){
                        冰箱.关闭();
        }


}


冰箱{

        打开（）{ 1.2.3.}
 关闭（）{}
}


柜子{


}


大象{
        进入(冰箱){

        }

}
```



面向过程 ---> 面向对象 , 其实就是由执行者 ---> 指挥者的 一个过渡



面向过程：编年体
面向对象：纪传体



二者相辅相成,并不是对立的。解决复杂问题,通过面向对象方式便于我们从宏观上把握事物之间复杂的关系、方便我们分析整个系统;具体到微观操作,仍然使用面向过程方式来处理

# 二、类和对象的关系

【1】万事万物皆对象

【2】
对象：具体的事物，具体的实体，具体的实例，模板下具体的产品
类：对对象向上抽取出像的部分，公共的部分，形成类，类是抽象的，是一个模板

【3】一般在写代码的时候先写类，然后在根据类创建对应的对象。

# 三、面向对象三个阶段

面向对象三个阶段：
【1】**面向对象分析OOA**  --  Object Oriented Analysis
对象：张三，王五，朱六，你，我
抽取出一个类----》人类

类里面有什么：
动词--》动态特性--》方法
名词--》静态特性--》属性
【2】**面向对象设计OOD**  --  Object Oriented Design
先有类，再有对象：
类：人类： Person
对象：zhangsan ，lisi，zhuliu
【3】**面向对象编程OOP**  --  Object Oriented Programming

# 四、创建类

创建类：
（1）属性（field 成员变量）
属性用于定义该类或该类对象包含的数据或者说静态特征。属性作用范围是整个类体。
属性定义格式：

```java
[修饰符]  属性类型  属性名 = [默认值] ;
```



（2）方法
方法用于定义该类或该类实例的行为特征和功能实现。方法是类和对象行为特征的抽象。方法很类似于面向过程中的函数。面向过程中，函数是最基本单位，整个程序由一个个函数调用组成。面向对象中，整个程序的基本单位是类，方法是从属于类和对象的。
方法定义格式：

```java
[修饰符]  方法返回值类型  方法名(形参列表) {
        // n条语句
}
```

void代表没有返回值；方法的作用：重用代码，封装功能，便于修改

代码：

```java
package com.msb;
/**
 * @Auther: msb-zhaoss
 * 创建类：人类
 */
public class Person {
    //名词---》属性---》成员变量---》放在类中方法外（注意：我们只把有需要的内容写到代码里，不相关的东西不要放在代码中）
    int age ;//年龄
    String name;//姓名
    double height;//身高
    double weight;//体重
    //动词---》方法
    //吃饭
    public void eat(){
        int num = 10;//局部变量：放在方法中
        System.out.println("我喜欢吃饭");
    }
    //睡觉：
    public void sleep(String address){
        System.out.println("我在"+address+"睡觉");
    }
    //自我介绍：
    public String introduce(){
        return "我的名字是："+name+"，我的年龄是："+age+",我的身高是："+height+",我的体重是："+weight;
    }
}

```



# 五、创建对象

```java
package com.msb;
/**
 * @Auther: msb-zhaoss
 */
public class Test {//测试类
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //创建一个人类的具体的对象/实例：
        //创建一个对象，对象的名字叫：zs
        //Person 属于 引用数据类型
        //第一次加载类的时候，会进行类的加载，初始化创建对象的时候，对象的属性没有给赋值，有默认的初始化的值。
        Person zs = new Person();
        zs.name = "张三";
        zs.age = 19;
        zs.height = 180.4;
        zs.weight = 170.4;
        //再创建一个对象：
        //再次创建类的时候，就不会进行类的加载了，类的加载只在第一次需要的时候加载一次
        Person ls = new Person();
        ls.name = "李四";
        ls.age = 18;
        ls.height = 170.6;
        ls.weight = 160.5;
        //对属性值进行读取：
        System.out.println(zs.name);
        System.out.println(ls.age);
        //对方法进行操作：
        //不同的对象，属性有自己的特有的值，但是方法都是调用类中通用的方法。
        //属性：各个对象的属性是独立的，
        //方法：各个对象的方法是共享的。
        zs.eat();
        ls.eat();
        zs.sleep("教室");
        /*String str = zs.introduce();
        System.out.println(str);*/
        System.out.println(zs.introduce());
    }
}

```



# 六、局部变量和成员变量的区别

区别1：代码中位置不同
         成员变量：类中方法外定义的变量
         局部变量：方法中定义的变量  代码块中定义的变量
区别2：代码的作用范围
         成员变量：当前类的很多方法
         局部变量：当前一个方法（当前代码块）   

区别3：是否有默认值
         成员变量：有
         局部变量：没有

 ![image-20210105150355503](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105150355503.png)

**引用数据类型**：															 **null**



区别4：是否要初始化
         成员变量：不需要，不建议初始化，后续使用的时候再赋值即可
         局部变量：一定需要，不然直接使用的时候报错

区别5：内存中位置不同
         成员变量：堆内存
         局部变量：栈内存   
区别6：作用时间不同
         成员变量：当前对象从创建到销毁
         局部变量：当前方法从开始执行到执行完毕


代码：

```java
package com.msb;
/**
 * @Auther: msb-zhaoss
 */
public class Student {
    byte e;
    short s;
    int c ;//成员变量：在类中方法外
    long num2;
    float f ;
    double d;
    char ch;
    boolean bo;
    String name;
    public void study(){
        int num = 10 ; //局部变量：在方法中
        System.out.println(num);//10
        //int num ;重复命名，出错了
        {
            int a;//局部变量：在代码块中
        }
        int a;
        if(1==3){
            int b;
        }
        System.out.println(c);
    }
    public void eat(){
        System.out.println(c);
    }
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Student s = new Student();
        System.out.println(s.c);
        System.out.println(s.bo);
        System.out.println(s.ch);
        System.out.println(s.d);
        System.out.println(s.e);
        System.out.println(s.f);
        System.out.println(s.name);
        System.out.println(s.num2);
        System.out.println(s.s);
        s.d = 10.4;
    }
}

```

运行结果：

![image-20210105150428098](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105150428098.png)

# 七、构造器

```java
package com.msb2;
/**
 * @Auther: msb-zhaoss
 */
public class Person {
    //构造器：没有任何参数的构造器我们叫做：空参构造器--》空构造器
    public Person(){
        /*age = 19;
        name = "lili";
        height = 169.5;*/
    }
    //属性：
    String name;
    int age;
    double height;
    //方法：
    public void eat(){
        System.out.println("我喜欢吃饭");
    }
}

```

```java
package com.msb2;
/**
 * @Auther: msb-zhaoss
 */
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //创建一个Person类的具体的对象/实例/实体：
        /*
        创建对象的过程：
        1.第一次遇到Person的时候，进行类的加载（只加载一次）
        2.创建对象，为这个对象在堆中开辟空间
        3.为对象进行属性的初始化动作
        new关键字实际上是在调用一个方法，这个方法叫构造方法（构造器）
        调用构造器的时候，如果你的类中没有写构造器，那么系统会默认给你分配一个构造器，只是我们看不到罢了。
        可以自己显式 的将构造器编写出来：
        构造器的格式：
        [修饰符] 构造器的名字(){
        }
        构造器和方法的区别：
        1.没有方法的返回值类型
        2.方法体内部不能有return语句
        3.构造器的名字很特殊，必须跟类名一样
        构造器的作用：不是为了创建对象，因为在调用构造器之前，这个对象就已经创建好了，并且属性有默认的初始化的值。
        调用构造器的目的是给属性进行赋值操作的。
        注意：我们一般不会在空构造器中进行初始化操作，因为那样的话每个对象的属性就一样了。
        实际上，我们只要保证空构造器的存在就可以了，里面的东西不用写
         */
        Person p = new Person();
        System.out.println(p.age);
        System.out.println(p.name);
        System.out.println(p.height);
        Person p2 = new Person();
        System.out.println(p2.age);
        System.out.println(p2.name);
        System.out.println(p2.height);
    }
}
```



# 八、构造器的重载

```java
package com.msb3.msb2;
/**
 * @Auther: msb-zhaoss
 */
public class Person {
    //属性：
    String name;
    int age;
    double height;
    //空构造器
    public Person(){
    }
    public Person(String name,int age,double height){
        //当形参名字和属性名字重名的时候，会出现就近原则：
        //在要表示对象的属性前加上this.来修饰 ，因为this代表的就是你创建的那个对象
        this.name = name;
        this.age = age;
        this.height = height;
    }
    public Person(String a,int b){
        name = a;
        age = b;
    }
    //方法：
    public void eat(){
        System.out.println("我喜欢吃饭");
    }
}
```



```java
package com.msb3.msb2;
/**
 * @Auther: msb-zhaoss
 */
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        /*
        1.一般保证空构造器的存在，空构造器中一般不会进行属性的赋值操作
        2.一般我们会重载构造器，在重载的构造器中进行属性赋值操作
        3.在重载构造器以后，假如空构造器忘写了，系统也不会给你分配默认的空构造器了，那么你要调用的话就会出错了。
        4. 当形参名字和属性名字重名的时候，会出现就近原则：
        在要表示对象的属性前加上this.来修饰 ，因为this代表的就是你创建的那个对象
         */
        Person p = new Person();
        /*p.age = 19;
        p.name = "lili";
        p.height = 180.4;*/
        Person p2 = new Person("lili",19,180.4);
        System.out.println(p2.age);
        System.out.println(p2.height);
        System.out.println(p2.name);
    }
}
```



# 九、内存分析

## 代码1

```java
 public class Person {
        int  id;
        int  age;

        public static void main(String args[]){
                Person p1= new Person();
        }
}
```

内存分析：

![image-20210105150549451](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105150549451.png)

## 代码2

```java
public class Person {
        int id;
        int age;
        String school;
        public Person (int a,int b,String c){
                id=a;
                age=b;
                school=c;
        }
        public static void main(String args[]){
                Person p= new Person(1,20, "海淀");
        }
}
```

![image-20210105150848093](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105150848093.png)

## 代码3

```java
class Person{
        int id;
        int age;
        String school;
        Person (int a,int b,String c){
                id=a;
                age=b;
                school=c;
        }

        public void setAge(int a){
                age=a;
        }
}
```



```java
public class Test {
    public static void main(String[] args) {
                  Test t=new Test();
                  int age=40;
                  Person tom=new Person(1,20,"海淀");
                  Person jack=new Person(2,30,"朝阳");
                  t.change1(age);
                  t.change2(tom);
                  t.change3(jack);
                  System.out.println(age); //40
                  System.out.println("id:"+jack.id+",age:"+jack.age+",school:"+jack.school); //id:2,age:66,school:"朝阳"
    }
    public void change1(int i){
                i=3366;
    }

    public void change2(Person p){
              p=new Person(3,22,"西城");
    }

    public void change3(Person p){
        p.setAge(66);
    }

}
```

![image-20210105150924134](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105150924134.png)

# 十、this

【1】创建对象的过程：
（1）在第一次遇到一个类的时候，对这个类要进行加载，只加载一次。
（2）创建对象，在堆中开辟空间
（3）对对象进行初始化操作，属性赋值都是默认的初始值。
（4）new关键字调用构造器，执行构造方法，在构造器中对属性重新进行赋值


this:

![image-20210105151053245](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105151053245.png)

![image-20210105151101570](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105151101570.png)


从上面的效果能够看到：this指代的就是当前对象：

内存：

![image-20210105151109733](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105151109733.png)

this关键字 用法：
（1）this可以修饰属性：
总结：当**属性名字**和**形参**发生重名的时候，或者  **属性名字** 和**局部变量**重名的时候，都会发生就近原则，所以如果我要是直接使用变量名字的话就指的是离的近的那个形参或者局部变量，这时候如果我想要表示属性的话，在前面要加上：**this.修饰**

如果不发生重名问题的话，实际上你要是访问属性也可以省略this.

```java
package com.msb4;
/**
 * @Auther: msb-zhaoss
 */
public class Person {
    //属性
    int age;
    String name;
    double height;
    //空构造器
    public Person(){
    }
    //有参构造器
    public Person(int age,String name,double height){
        this.age = age;
        this.name = name;
        this.height = height;
    }
    //方法：
    public void eat(){
        int age = 10;
        System.out.println(age);//就近原则，age指的是离它近的age--》局部变量的age
        System.out.println(this.age);//这里指代的就是属性的age
        System.out.println("我喜欢吃饭");
    }
}

```



（2）this修饰方法：
总结：在同一个类中，方法可以互相调用，**this.可以省略不写**。

```java
package com.msb4;
/**
 * @Auther: msb-zhaoss
 */
public class Person {
    //属性
    int age;
    String name;
    double height;
    //空构造器
    public Person(){
    }
    //有参构造器
    public Person(int age,String name,double height){
        this.age = age;
        this.name = name;
        this.height = height;
    }
    //方法：
    /*public void eat(){
        int age = 10;
        System.out.println(age);//就近原则，age指的是离它近的age--》局部变量的age
        System.out.println(this.age);//这里指代的就是属性的age
        System.out.println("我喜欢吃饭");
    }*/
    public void play(){
        /*this.*/eat();
        System.out.println("上网");
        System.out.println("洗澡");
    }
    public void eat(){
        System.out.println(/*this.*/age);
        System.out.println("吃饭");
    }
}

```



（3）this可以修饰构造器：
总结：同一个类中的构造器可以相互用this调用，注意：**this修饰构造器必须放在第一行**

```java
package com.msb4;
/**
 * @Auther: msb-zhaoss
 */
public class Person {
    //属性
    int age;
    String name;
    double height;
    //空构造器
    public Person(){
    }
    //有参构造器
    public Person(int age,String name,double height){
        this(age,name);
        this.height = height;
    }
    public Person(int age,String name){
        this(age);
        this.name = name;
    }
    public Person(int age){
        this.age = age;
    }
    //方法：
    /*public void eat(){
        int age = 10;
        System.out.println(age);//就近原则，age指的是离它近的age--》局部变量的age
        System.out.println(this.age);//这里指代的就是属性的age
        System.out.println("我喜欢吃饭");
    }*/
    public void play(){
        /*this.*/eat();
        System.out.println("上网");
        System.out.println("洗澡");
    }
    public void eat(){
        System.out.println(/*this.*/age);
        System.out.println("吃饭");
    }
}

```



# 十一、static

【1】static可以修饰：属性，方法，代码块，内部类。

【2】static修饰属性；

```java
package com.msb5;
/**
 * @Auther: msb-zhaoss
 */
public class Test {
    //属性：
    int id;
    static int sid;
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //创建一个Test类的具体的对象
        Test t1 = new Test();
        t1.id = 10;
        t1.sid = 10;
        Test t2 = new Test();
        t2.id = 20;
        t2.sid = 20;
        Test t3 = new Test();
        t3.id = 30;
        t3.sid = 30;
        //读取属性的值：
        System.out.println(t1.id);
        System.out.println(t2.id);
        System.out.println(t3.id);
        System.out.println(t1.sid);
        System.out.println(t2.sid);
        System.out.println(t3.sid);
    }
}

```

![image-20210107013415802](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210107013415802.png)

内存分析：

![image-20210105151307040](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105151307040.png)

一般官方的推荐访问方式：可以通过类名.属性名的方式去访问：

![image-20210105151315750](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105151315750.png)

static修饰属性总结：
（1）在类加载的时候一起加载入方法区中的**静态域**中
（2）先于对象存在
（3）访问方式： 对象名.属性名    **类名.属性名（推荐）**


static修饰属性的应用场景：**某些特定的数据想要在内存中共享**，只有一块 --》这个情况下，就可以用static修饰的属性

```java
package com.msb5;
/**
 * @Auther: msb-zhaoss
 */
public class MsbStudent {
    //属性：
    String name;
    int age;
    static String school;
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        MsbStudent.school = "马士兵教育";
        //创建学生对象：
        MsbStudent s1 = new MsbStudent();
        s1.name = "张三";
        s1.age = 19;
        //s1.school = "马士兵教育";
        MsbStudent s2 = new MsbStudent();
        s2.name = "李四";
        s2.age = 21;
        //s2.school = "马士兵教育";
        System.out.println(s2.school);
    }
}

```



属性：
**静态属性 （类变量）**
**非静态属性（实例变量）**

【3】static修饰方法；

```java
package com.msb5;
/**
 * @Auther: msb-zhaoss
 */
public class Demo {
    int id;
    static int sid;
    public void a(){
        System.out.println(id);
        System.out.println(sid);
        System.out.println("------a");
    }
    //1.static和public都是修饰符，并列的没有先后顺序，先写谁后写谁都行
    static public void b(){
        //System.out.println(this.id);//4.在静态方法中不能使用this关键字
        //a();//3.在静态方法中不能访问非静态的方法
        //System.out.println(id);//2.在静态方法中不能访问非静态的属性
        System.out.println(sid);
        System.out.println("------b");
    }
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //5.非静态的方法可以用对象名.方法名去调用
        Demo d = new Demo();
        d.a();
        //6.静态的方法可以用   对象名.方法名去调用  也可以 用  类名.方法名 （推荐）
        Demo.b();
        d.b();
       
    }
}

```



# 十二、代码块

【1】类的组成：属性，方法，构造器，代码块，内部类
【2】代码块分类：普通块，构造块，静态块，同步块（多线程）
【3】代码：

```java
package com.msb6;
/**
 * @Auther: msb-zhaoss
 */
public class Test {
    //属性
    int a;
    static int sa;
    //方法
    public void a(){
        System.out.println("-----a");
        {
            //普通块限制了局部变量的作用范围
            System.out.println("这是普通块");
            System.out.println("----000000");
            int num = 10;
            System.out.println(num);
        }
        //System.out.println(num);
        //if(){}
        //while(){}
    }
    public static void b(){
        System.out.println("------b");
    }
    //构造块
    {
        System.out.println("------这是构造块");
    }
    //静态块
    static{
        System.out.println("-----这是静态块");
        //在静态块中只能方法：静态属性，静态方法
        System.out.println(sa);
        b();
    }
    //构造器
    public Test(){
        System.out.println("这是空构造器");
    }
    public Test(int a){
        this.a = a;
    }
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Test t = new Test();
        t.a();
        Test t2 = new Test();
        t2.a();
    }
}

```

![image-20210107094018948](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210107094018948.png)



总结：
（1）代码块执行顺序：
最先执行静态块，只在类加载的时候执行一次，所以一般以后实战写项目：创建工厂，数据库的初始化信息都放入静态块。
一般用于执行一些**全局性的初始化操作**。

再执行构造块，（不常用）
再执行构造器，
再执行方法中的普通块。

# 十三、包，import

【1】生活案例：
邮寄快递：中国.北京.通州区.****小区.5号楼.3单元.101房.赵珊珊
历史：常山赵子龙

【2】包的作用：
为了解决重名问题（实际上包对应的就是**盘符上的目录**）
解决**权限**问题

【3】创建包：

![image-20210105151502372](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105151502372.png)

![image-20210105151512202](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105151512202.png)



包名定义：
（1）名字全部小写
（2）中间用.隔开
（3）一般都是公司域名倒着写 ：  com.jd   com.msb
（4）加上模块名字：
															com.jd.login    com.jd.register
（5）不能使用系统中的关键字：nul,con,com1---com9.....
（6）包声明的位置一般都在非注释性代码的第一行：

![image-20210105151524780](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105151524780.png)

【4】导包问题：

```java
//声明包：
package com.msb7;
import com.msb2.Person; //导包：就是为了进行定位
import java.util.Date;
/**
 * @Auther: msb-zhaoss
 */
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new Person();
        new Date();
        new java.sql.Date(1000L);//在导包以后，还想用其他包下同名的类，就必须要手动自己写所在的包。
        new Demo();
    }
}

```

总结：
（1）使用不同包下的类要需要导包： import **.*.*;  例如：import java.util.Date;
（2）在导包以后，还想用其他包下同名的类，就必须要手动自己写所在的包。
（3）同一个包下的类想使用不需要导包，可以直接使用。
（4）在java.lang包下的类，可以直接使用无需导包：

![image-20210105151544537](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105151544537.png)

（5）IDEA中导包快捷键：alt+enter  
        可以自己设置自动导包

（6）可以直接导入*：

![image-20210105151721085](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105151721085.png)


【5】在Java中的导包没有包含和被包含的关系：
设置目录平级的格式（不是包含和被包含的显示）：

![image-20210105152517763](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105152517763.png)

![image-20210105152526348](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105152526348.png)



【6】静态导入：

```java
package com.msb11;
//静态导入：
import static java.lang.Math.*;
//导入：java.lang下的Math类中的所有静态的内容
/**
 * @Auther: msb-zhaoss
 */
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        System.out.println(random());
        System.out.println(PI);
        System.out.println(round(5.6));
    }
    //在静态导入后，同一个类中有相同的方法的时候，会优先走自己定义的方法。
    public static int round(double a){
        return 1000;
    }
}

```

![image-20210107104200373](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210107104200373.png)



# 十四、三大特性

## 封装(Encapsulation)

【1】生活案例：
ATM ,  电线
【2】Java中封装的理解：
将某些东西进行隐藏，然后提供相应的方式进行获取。

![image-20210105153143517](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105153143517.png)

我们程序设计追求“高内聚，低耦合”。
➢**高内聚**:类的内部数据操作细节自己完成，不允许外部干涉;
➢**低耦合**:仅对外暴露少量的方法用于使用。 
隐藏对象内部的复杂性，只对外公开简单的接口。便于外界调用，从而提
高系统的可扩展性、可维护性。通俗的说，把**该隐藏的隐藏起来，该暴露**
**的暴露出来**。这就是封装性的设计思想。 
【3】封装的好处：
提高代码的安全性

【4】代码：通过一个属性感受封装：

```java
package com.msb.test01;
/**
 * @Auther: msb-zhaoss
 */
public class Girl {//女孩
    //属性：
    private int age;
    //读取年龄：
    public int duquAge(){
        return age;
    }
    //设置年龄：
    public void shezhiAge(int age){
        if(age >= 30 ){
            this.age = 18;
        }else{
            this.age = age;
        }
    }
}

```



```java
package com.msb.test01;
/**
 * @Auther: msb-zhaoss
 */
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //创建一个Girl类的对象：
        Girl g = new Girl();
        /*g.age = 33;
        System.out.println(g.age);*/
        //设置年龄：
        g.shezhiAge(31);
        //读取年龄：
        System.out.println(g.duquAge());
    }
}

```

![image-20210107110340554](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210107110340554.png)



上面的代码，对于属性age来说，我加了**修饰符private**，这样外界对它的访问就受到了限制，现在我还想加上其他的**限制条件**，但是在属性本身上没有办法再加了，所以我们通过**定义方法****来进行限制条件的添加。
以属性为案例：
进行封装：
（1）将属性私有化，被private修饰--》加入权限修饰符
**一旦加入了权限修饰符，其他人就不可以随意的获取这个属性**
（2）提供**public修饰的方法**让别人来访问/使用
（3）即使外界可以通过方法来访问属性了，但是也不能随意访问，因为咱们在方法中可以加入 限制**条件**。

【5】实际开发中，方法一般会写成 **setter，getter**方法：
可以利用IDEA快捷键生成：alt+insert -->getter and setter:

```java
public class Girl {//女孩
    //属性：
    private int age;
    //读取年龄：
    public int getAge(){
        return age;
    }
    //设置年龄：
    public void setAge(int age){
        if(age >= 30 ){
            this.age = 18;
        }else{
            this.age = age;
        }
    }
}

```



【6】加深练习：

```java
package com.msb.test2;
/**
 * @Auther: msb-zhaoss
 */
public class Student {
    //属性：
    private int age;
    private String name;
    private String sex;
    //加入对应的setter和getter方法：
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public String getSex() {
        return sex;
    }
    public void setSex(String sex) {
        if("男".equals(sex) || "女".equals(sex) ){//sex是男 或者 是 女
            this.sex = sex;
        }else{
            this.sex = "男";
        }
    }
    //加入构造器：
    public Student(){
    }
    public Student(int age,String name,String sex){
        this.age = age;
        this.name = name;
        //this.sex = sex;
        this.setSex(sex);
    }
}

```





```java
package com.msb.test2;
/**
 * @Auther: msb-zhaoss
 */
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //创建一个Student对象：
        Student s1 = new Student();
        s1.setName("nana");
        s1.setAge(19);
        s1.setSex("女");
        System.out.println(s1.getName()+"---"+s1.getAge()+"----"+s1.getSex());
        Student s2 = new Student(18,"菲菲","asdfasdfsadf");
        System.out.println(s2.getName()+"---"+s2.getAge()+"----"+s2.getSex());
    }
}

```

![image-20210107111004553](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210107111004553.png)





## 继承(Inheritance)

【1】类是对对象的抽象：
举例：
荣耀20 ，小米 红米3，华为 p40 pro   ---> 类：手机类

【2】继承是对类的抽象：
举例：
学生类：Student：
属性：姓名，年龄，身高，学生编号
方法：吃饭，睡觉，喊叫，学习

教师类：Teacher:
属性：姓名，年龄，身高，教师编号
方法：吃饭，睡觉，喊叫，教学

员工类：Emploee:
属性：姓名，年龄，身高，员工编号
方法：吃饭，睡觉，喊叫，工作

共同的东西：
人类：
属性：姓名，年龄，身高
方法：吃饭，睡觉，喊叫

学生类/教师类/员工类  **继承** 自   人类  

以后定义代码：
先定义人类：
人类： ---》**父类，基类，超类**
属性：姓名，年龄，身高
方法：吃饭，睡觉，喊叫

再定义 ： ---》**子类，派生类**

学生类：Student：
属性：学生编号
方法：学习

教师类：Teacher:
属性：教师编号
方法：教学

员工类：Emploee:
属性：员工编号
方法：工作 


子类  **继承**自  父类 


狗类：
属性：姓名，年龄，身高
方法：吃饭，睡觉，喊叫


我们的继承关系，是在合理的范围中进行的抽取 ，抽取出子类父类的关系：
上面的案例中：
学生类/教师类/员工类  继承 自   人类   ---》合理
学生类/教师类/员工类  继承 自   狗类   ---》不合理

区分：
学生是一个人
教师是一个人
员工是一个人   ---》合理

学生是一个狗    ---》不合理

总结：继承 就是  **is - a** 的关系 

【3】代码层面的解释：
先写父类，再写子类：

父类：人类  Person
子类：学生类   Student

```java
package com.msb.test03;
/**
 * @Auther: msb-zhaoss
 */
public class Person {
    //属性：
    private int age;
    private String name;
    private double height;
    //提供setter getter方法：
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public double getHeight() {
        return height;
    }
    public void setHeight(double height) {
        this.height = height;
    }
    //方法：
    public void eat(){
        System.out.println("可以吃饭。。。");
    }
    public void sleep(){
        System.out.println("可以睡觉。。。");
    }
}

```



```java
package com.msb.test03;
/**
 * @Auther: msb-zhaoss
 */
public class Student extends Person {//子类Student 继承  父类Person
    //属性：
    private int sno;//学号
    public int getSno() {
        return sno;
    }
    public void setSno(int sno) {
        this.sno = sno;
    }
    //方法：
    public void study(){
        System.out.println("学生可以学习");
    }
}
```



```java
package com.msb.test03;
/**
 * @Auther: msb-zhaoss
 */
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //创建子类Student的对象
        Student s = new Student();
        s.setSno(1001);
        s.setAge(18);
        s.setName("菲菲");
        s.setHeight(180.4);
        System.out.println("学生名字为："+s.getName()+",学生的年纪："+s.getAge());
        //访问方法：
        s.study();
        s.eat();
        s.sleep();
    }
}

```

![image-20210107112204578](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210107112204578.png)



【4】继承的好处：提高代码的复用性
父类定义的内容，子类可以直接拿过来用就可以了，不用代码上反复重复定义了

需要注意的点：
父类private修饰的内容，子类实际上也继承，只是因为封装的特性阻碍了直接调用，但是提供了间接调用的方式，可以间接调用。


【5】总结：

（1）继承关系 ：
**父类/基类/超类**
**子类/派生类**
子类继承父类一定在合理的范围进行继承的    子类 **extends**  父类
（2）继承的好处：
1.提高了代码的**复用性**，父类定义的内容，子类可以直接拿过来用就可以了，不用代码上反复重复定义了
2.便于代码的**扩展**
3.为了以后多态的使用。是**多态的前提**。

（3）父类private修饰的内容，子类也继承过来了。
（4）一个父类可以有多个子类。
（5）一个子类只能有一个直接父类。
但是可以间接的继承自其它类。

![image-20210105153411818](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105153411818.png)

（6）继承具有传递性：

Student --》继承自  Person  ---》继承自Object
Object类是所有类的**根基父类**。
所有的类都**直接或者间接的继承自**Object。

### 内存分析

![image-20210105153450486](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105153450486.png)

### 权限修饰符

![image-20210105153512443](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105153512443.png)

【1】private：权限：在当前类中可以访问

![image-20210105153520506](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105153520506.png)

![image-20210105153535662](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105153535662.png)

![image-20210105153545671](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105153545671.png)

【2】default:缺省修饰符：权限：到同一个包下的其他类都可以访问

![image-20210105153606737](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105153606737.png)

![image-20210105153745188](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105153745188.png)

![image-20210105153754434](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105153754434.png)

【3】protected：权限：最大到不同包下的子类

![image-20210105153802337](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105153802337.png)

![image-20210105153815249](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105153815249.png)

![image-20210105153823773](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105153823773.png)



【4】public：在整个项目中都可以访问



总结：
**属性，方法**：修饰符：**四种**：private，缺省，protected，public
**类**：修饰符：**两种**：缺省，public

以后写代码
一般属性：用private修饰 ，方法：用public修饰

### 方法的重写

【1】重写：
发生在子类和父类中，当子类对父类提供的方法不满意的时候，要对父类的方法进行重写。

【2】重写有严格的格式要求：
子类的**方法名字**和父类必须一致，**参数列表**（个数，类型，顺序）也要和父类一致。

【3】代码：

```java
public class Person {
    public void eat(){
        System.out.println("吃食物");
    }
    public void sleep(){
        System.out.println("睡觉");
    }
}

```



```java
public class Student extends Person {
    public void study(){
        System.out.println("学习");
    }
    public void eat(){
        System.out.println("我喜欢吃小龙虾喝啤酒。。");
    }
}
```

![image-20210105153917604](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105153917604.png)

```java
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //创建一个Student类的对象：
        Student s = new Student();
        s.eat();
    }
}
```





【4】内存：

![image-20210105154923994](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105154923994.png)

【5】重载和重写的区别：
重载：在同一个类中，当方法名相同，形参列表不同的时候  多个方法构成了重载
重写：在不同的类中，子类对父类提供的方法不满意的时候，要对父类的方法进行重写。

![image-20210105154934355](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105154934355.png)

### super

【1】super:指的是：  父类的
【2】super可以修饰属性，可以修饰方法；

在子类的方法中，可以通过  super.属性  super.方法 的方式，显示的去**调用父类提供的属性，方法**。在通常情况下，**super.可以省略不写**：

![image-20210105155105263](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155105263.png)

在特殊情况下，当子类和父类的**属性重名**时，你要想使用父类的属性，必须加上修饰符super.，只能通过super.属性来调用
在特殊情况下，当子类和父类的**方法重名**时，你要想使用父类的方法，必须加上修饰符super.，只能通过super.方法来调用
在这种情况下，**super.就不可以省略不写**。

![image-20210105155130349](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155130349.png)

![image-20210107155154761](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210107155154761.png)

【3】super修饰构造器：
其实我们平时写的构造器的第一行都有：super()  -->作用：调用父类的空构造器，只是我们一般都省略不写
（所有构造器的**第一行默认情况下都有super()**,但是一旦你的构造器中显示的使用super调用了父类构造器，那么这个super()就不会给你默认分配了。如果构造器中没有显示的调用父类构造器的话，那么第一行都有super(),可以省略不写）

![image-20210105155142874](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155142874.png)

如果构造器中**已经显示的调用super父类构造器，那么它的第一行就没有默认分配的super()**;了

![image-20210105155204932](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155204932.png)

在构造器中，super调用父类构造器和this调用子类构造器只能存在一个，两者不能共存：
因为super修饰构造器要放在第一行，this修饰构造器也要放在第一行：

![image-20210105155221245](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155221245.png)

改正二选一即可：

![image-20210105155232645](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155232645.png)





【4】以后写代码构造器的生成可以直接使用IDEA提供的快捷键：
alt+insert

![image-20210105155242611](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155242611.png)

### 继承条件下构造方法的执行过程

![image-20210105155254513](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155254513.png)

```java
package com.msb.test10;
/**
 * @Auther: msb-zhaoss
 */
public class Person {
    int age;
    String name;
    public Person(int age, String name) {
        super();
        this.age = age;
        this.name = name;
    }
    public Person() {
    }
}

```



```java
public class Student extends Person {
    double height ;
    public Student() {
    }
    public Student(int age, String name, double height) {
        super(age, name);
        this.height = height;
    }
}

```



```java
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Student s = new Student(19,"feifei",160.8);
    }
}

```



### Object类

所有类都**直接或间接的继承**自Object类，**Object类**是所有Java类的**根基类**。
也就意味着所有的Java对象都拥有Object类的属性和方法。
如果在类的声明中未使用extends关键字指明其父类，则默认继承Object类。

![image-20210105155354961](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155354961.png)

#### 1.toString()方法

【1】Object类的toString()的作用：

![image-20210105155436625](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155436625.png)

方法的原理：

![image-20210105155444698](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155444698.png)

现在，使用toString方法的时候，打印出来的东西 “不好看”，对于其他人来说不友好，可读性不好
我们现在是想知道对象的信息，名字，年龄，身高。。。。。。
现在的格式不好：

![image-20210105155452863](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155452863.png)

出现的问题：**子类Student对父类Object提供的toString方法不满意**，不满意--》对toString方法进行重写：

```java
package com.msb.test01;
/**
 * @Auther: msb-zhaoss
 */
public class Student /*extends Object*/{
    private String name;
    private int age;
    private double height;
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
    public double getHeight() {
        return height;
    }
    public void setHeight(double height) {
        this.height = height;
    }
    public Student() {
    }
    public Student(String name, int age, double height) {
        this.name = name;
        this.age = age;
        this.height = height;
    }
    public String toString() {
        return "这是一个Student对象，这个对象的名字："+name+",年龄："+age+",身高："+height;
    }
}

```

测试类：

![image-20210105155508145](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155508145.png)


总结：**toString**的作用就是对对象进行“**自我介绍**”，一般子类对父类提供的toString都不满意，都要进行重写。



IDEA提供了快捷键：

```java
package com.msb.test01;
/**
 * @Auther: msb-zhaoss
 */
public class Student /*extends Object*/{
    private String name;
    private int age;
    private double height;
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
    public double getHeight() {
        return height;
    }
    public void setHeight(double height) {
        this.height = height;
    }
    public Student() {
    }
    public Student(String name, int age, double height) {
        this.name = name;
        this.age = age;
        this.height = height;
    }
    /*public String toString() {
        return "这是一个Student对象，这个对象的名字："+name+",年龄："+age+",身高："+height;
    }*/
    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", height=" + height +
                '}';
    }
}

```



#### 2.equals方法

```java
package com.msb.test02;
/**
 * @Auther: msb-zhaoss
 */
public class Phone {//手机类：
    //属性：
    private String brand;//品牌型号
    private double price;//价格
    private int year ;//出产年份
    //方法：
    public String getBrand() {
        return brand;
    }
    public void setBrand(String brand) {
        this.brand = brand;
    }
    public double getPrice() {
        return price;
    }
    public void setPrice(double price) {
        this.price = price;
    }
    public int getYear() {
        return year;
    }
    public void setYear(int year) {
        this.year = year;
    }
    @Override
    public String toString() {
        return "Phone{" +
                "brand='" + brand + '\'' +
                ", price=" + price +
                ", year=" + year +
                '}';
    }
    //构造器：
    public Phone() {
    }
    public Phone(String brand, double price, int year) {
        this.brand = brand;
        this.price = price;
        this.year = year;
    }
    //对equals方法进行重写：
    public boolean equals(Object obj) {
        //Object obj = new Phone();
        //将obj转为Phone类型：
        Phone other = (Phone)obj;//向下转型，为了获取子类中特有的内容
        		      if(this.getBrand()==other.getBrand()&&this.getPrice()==other.getPrice()&&this.getYear()==other.getYear()){
            return true;
        }
        return false;
    }
}

```



```java
package com.msb.test02;
/**
 * @Auther: msb-zhaoss
 */
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //创建Phone类的对象：
        Phone p1 = new Phone("华为P40",2035.98,2020);
        Phone p2 = new Phone("华为P40",2035.98,2020);
        //比较两个对象：p1和p2对象：
        //==的作用：比较左右两侧的值是否想的，要么相等，返回true,要么不相等,返回false
        System.out.println(p1==p2);//-->>>对于引用数据类型来说，比较的是地址值。--->一定返回的是false
        //Object类提供了一个方法 equals方法 ：作用：比较对象具体内容是否相等。
        boolean flag = p1.equals(p2);//点进源码发现：底层依旧比较的是==，比较的还是地址值。
        System.out.println(flag);
    }
}

```

总结：
equals作用：这个方法提供了对**对象的内容是否相等 的一个比较方式**，对象的内容指的就是属性。
父类Object提供的equals就是在**比较==地址**，没有实际的意义，我们一般不会直接使用父类提供的方法，
而是在子类中对这个方法进行重写。

##### instanceof

![image-20210105155608153](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155608153.png)

##### 利用集成开发工具生成equals方法

【1】利用eclipse：

![image-20210105155627004](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155627004.png)

【2】利用idea：

![image-20210105155636140](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155636140.png)

### 类和类的关系

#### 代码

总结：
【1】面向对象的思维：找参与者，找女孩类，找男孩类
【2】体会了什么叫方法的形参，什么叫方法的实参：

![image-20210105155710794](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155710794.png)

具体传入的内容 实参：

![image-20210105155720147](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155720147.png)

【3】类和类可以产生关系：
（1）将一个类作为另一个类中的方法的**形参**
（2）将一个类作为另一个类的**属性**

```java
public class Girl {
    //属性：
    String name;
    double weight;
    Mom m /*= new Mom()*/;
    //方法：
    public void add(int a){//参数是基本数据类型
        System.out.println(a);
        System.out.println(a+100);
    }
    //谈恋爱的方法：
    public void love(Boy b){//参数是引用数据类型Boy
        System.out.println("我男朋友的名字是："+b.name+"，我男朋友的年龄是："+b.age);
        b.buy();
    }
    //女孩跟妈妈聊天：
    public void wechat(){
        m.say();
    }
    //构造器：
    public Girl(String name, double weight) {
        this.name = name;
        this.weight = weight;
    }
}
```



```java
public class Boy {
    //属性：
    int age;
    String name;
    //方法：
    public void buy(){
        System.out.println("跟我谈恋爱，我给你买买买。。。");
    }
    //构造器：
    public Boy(int age, String name) {
        this.age = age;
        this.name = name;
    }
}
```



```java
public class Mom {
    //方法：
    public void say(){
        System.out.println("妈妈唠唠叨叨 都是爱，听妈妈的话。。");
    }
}

```



```java
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //创建一个Boy类的具体的对象：
        Boy boy = new Boy(30,"鹿晗");
        //创建一个Girl类的具体的对象：
        Girl girl = new Girl("关晓彤",100);
        //谈恋爱：
        //girl.love(boy);
        Boy boy2 = new Boy(35,"陈伟霆");
        girl.love(boy2);
        //还可以跟妈妈微信聊天：
        //必须先声明对象类
        girl.m = new Mom();
        girl.wechat();
    }
}
```

![image-20210107164420021](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210107164420021.png)



#### 总结

一、**继承关系**      
继承指的是一个类（称为子类、子接口）继承另外的一个类（称为父类、父接口）的功能，并可以增加它自己的新功能的能力。在Java中继承关系通过关键字**extends**明确标识，在设计时一般没有争议性。在UML类图设计中，继承用**一条带空心三角箭头的实线**表示，从子类指向父类，或者子接口指向父接口。

![image-20210105155822999](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155822999.png)

二、**实现关系**      
实现指的是一个class类实现interface接口（可以是多个）的功能，实现是**类与接口**之间最常见的关系。在Java中此类关系通过关键字**implements**明确标识，在设计时一般没有争议性。在UML类图设计中，实现用一条带空心三角箭头的虚线表示，从类指向实现的接口。

![image-20210105155829985](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155829985.png)

三、**依赖关系**      
简单的理解，依赖就是一个**类A使用到了另一个类B**，而这种使用关系是具有**偶然性的、临时性**的、非常弱的，但是类B的变化会影响到类A。比如某人要过河，需要借用一条船，此时人与船之间的关系就是依赖。表现在代码层面，让类B作为参数被类A在某个method方法中使用。在UML类图设计中，依赖关系用由类A指向类B的带箭头虚线表示。

![image-20210105155838217](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155838217.png)

四、**关联关系**  
关联体现的是两个类之间语义级别的一种**强依赖**关系，比如我和我的朋友，这种关系比依赖更强、不存在依赖关系的偶然性、关系也不是临时性的，一般是**长期性**的，而且双方的关系一般是**平等的**。关联可以是**单向、双向**的。表现在代码层面，为被关联类B以类的**属性形式**出现在关联类A中，也可能是关联类A引用了一个类型为被关联类B的**全局变量**。在UML类图设计中，关联关系用由关联类A指向被关联类B的**带箭头实线**表示，在关联的两端可以标注**关联双方的角色和多重性标记。**

![image-20210105155845999](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155845999.png)

五、**聚合关系**      
聚合是关联关系的一种特例，它体现的是**整体与部分**的关系，即**has-a**的关系。此时整体与部分之间是可分离的，它们**可以具有各自的生命周期**，**部分可以属于多个整体对象，也可以为多个整体对象共享**。比如计算机与CPU、公司与员工的关系等，比如一个航母编队包括海空母舰、驱护舰艇、舰载飞机及核动力攻击潜艇等。表现在代码层面，和关联关系是一致的，只能从语义级别来区分。在UML类图设计中，聚合关系以**空心菱形**加实线箭头表示。

![image-20210105155854400](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155854400.png)

六、**组合关系**     
组合也是关联关系的一种特例，它体现的是一种**contains-a**的关系，这种关系比聚合更强，也称为强聚合。它同样体现整体与部分间的关系，但此时整体与部分是不可分的，**整体的生命周期结束也就意味着部分的生命周期结束**，比如人和人的大脑。表现在代码层面，和关联关系是一致的，只能从语义级别来区分。在UML类图设计中，组合关系以**实心菱形加实线箭头**表示。

![image-20210105155901105](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105155901105.png)

七、总结     
对于继承、实现这两种关系没多少疑问，它们体现的是一种类和类、或者类与接口间的纵向关系。其他的四种关系体现的是类和类、或者类与接口间的引用、横向关系，是比较难区分的，有很多事物间的关系要想准确定位是很难的。前面也提到，这四种关系都是语义级别的，所以从代码层面并不能完全区分各种关系，但总的来说，后几种关系所表现的强弱程度依次为：**组合>聚合>关联>依赖**。

## 多态(Polymorphism)

【1】多态跟属性无关，多态指的是**方法的多态**，而不是属性的多态。
【2】案例代入：

```java
public class Animal {//父类：动物：
    public void shout(){
        System.out.println("我是小动物，我可以叫。。。");
    }
}
```



```java
public class Cat extends Animal{
    //喊叫方法：
    public void shout(){
        System.out.println("我是小猫，可以喵喵叫");
    }
    public void scratch(){
        System.out.println("我是小猫，我可以挠人");
    }
}
```



```java
public class Dog extends Animal{
    //喊叫：
    public void shout(){
        System.out.println("我是小狗，我可以汪汪叫");
    }
    public void guard(){
        System.out.println("我是小狗，我可以看家护院，保护我的小主人。。。");
    }
}
```



```java
public class Pig extends Animal{
    public void shout(){
        System.out.println("我是小猪，我嗯嗯嗯的叫");
    }
    public void eat(){
        System.out.println("我是小猪，我爱吃东西。。");
    }
}
```



```java
public class Girl {
    //跟猫玩耍：
    /*public void play(Cat cat){
        cat.shout();
    }*/
    //跟狗玩耍：
    /*public void play(Dog dog){
        dog.shout();
    }*/
    //跟小动物玩耍：
    public void play(Animal an){
        an.shout();
    }
}
```



```java
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //具体的猫：--》猫的对象
        //Cat c = new Cat();
        //具体的小女孩：--》女孩的对象
        Girl g = new Girl();
        //小女孩跟猫玩：
        //g.play(c);
        //具体的狗---》狗的对象：
        //Dog d = new Dog();
        //小女孩跟狗玩：
        //g.play(d);
        //具体的动物：--》动物的对象：
        //Cat c = new Cat();
        //Dog d = new Dog();
        Pig p = new Pig();
        Animal an = p;
        g.play(an);
    }
}
```



【3】总结：
（1）先有父类，再有子类：--》**继承**   先有子类，再抽取父类 ----》**泛化** 
（2）什么是多态：
**多态**就是**多种状态**：**同一个行为，不同的子类表现出来不同的形态**。
多态指的就是**同一个方法调用，然后由于对象不同会产生不同的行为。**

（3）多态的好处：
为了提高代码的**扩展性**，符合面向对象的设计原则：**开闭原则**。
开闭原则：指的就是**扩展是 开放的，修改是关闭的**。
注意：多态可以提高扩展性，但是扩展性没有达到最好，以后我们会学习 **反射**

（4）**多态的要素**：
一，**继承**：   Cat extends Animal  ,Pig extends Animal,   Dog extends Animal
二，**重写**：子类对父类的方法shout()重写
三， 父类引用指向子类对象：

```java
Pig p = new Pig();
Animal an = p;
```

将上面的代码合为一句话：
Animal an = new Pig();
=左侧：编译期的类型
=右侧：运行期的类型

Animal an = new Pig();
g.play(an); //

```java
public void play(Animal an){//Animal an = an = new Pig();
        an.shout();
    }
```



上面的代码，也是多态的一种非常常见的应用场合：父**类当方法的形参，然后传入的是具体的子类的对象**，
然后调用同一个方法，**根据传入的子类的不同展现出来的效果也不同**，构成了多态。

### 内存分析

![image-20210105160128289](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105160128289.png)

### 向下转型，向上转型

![image-20210105160158757](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105160158757.png)

![image-20210105160206489](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105160206489.png)

现在我就想访问到eat()方法和weight属性：

```java
public class Demo {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Pig p = new Pig();
        Animal an = p;//转型：向上转型
        an.shout();
        //加入转型的代码：
        //将Animal转为Pig类型：
        Pig pig = (Pig)an ;//转型：向下转型
        pig.eat();
        pig.age = 10;
        pig.weight = 60.8;
    }
}
```

对应内存：

![image-20210105160225181](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105160225181.png)

思考之前的equals方法：

![image-20210105160233140](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105160233140.png)

### 简单工厂设计模式

多态的应用场合：

不仅可以使用**父类做方法的形参**，还可以使用**父类做方法的返回值类型**，真实返回的对象可以是该类的**任意一个子类对象**。


简单工厂模式的实现，它是解决**大量对象创建问题**的一个解决方案。将创建和使用分开，**工厂负责创建**，**使用者直接调用**即可。简单工厂模式的基本要求是

定义一个**static方法，通过类名直接调用**

返回值类型是**父类类型**，返回的可以是其**任意子类类型**

传入一个字符串类型的参数，工厂根据参数创建对应的子类产品

```java
public class Test {
    public static void main(String[] args) {
        Girl g = new Girl();
        //Cat c = new Cat();
        //Dog d = new Dog();
        //Pig p = new Pig();
        Animal an = PetStore.getAnimal("狗");
        g.play(an);
    }
}
```



```java
public class PetStore {//宠物店 ---》工厂类
    //方法：提供动物
    public static Animal getAnimal(String petName){//多态的应用场合（二）
        Animal an = null;
        if("猫".equals(petName)){//petName.equals("猫") --》这样写容易发生空指针异常
            an = new Cat();
        }
        if("狗".equals(petName)){
            an = new Dog();
        }
        if("猪".equals(petName)){
            an = new Pig();
        }
        return an;
    }
}
```



# 十五、final

【1】修饰变量；

```java
public class Test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //第1种情况：
        //final修饰一个变量，变量的值不可以改变，这个变量也变成了一个字符常量，约定俗称的规定：名字大写
        final int A = 10;//final修饰基本数据类型
        //A = 20; 报错：不可以修改值
        //第2种情况：
        final Dog d = new Dog();//final修饰引用数据类型，那么地址值就不可以改变
        //d = new Dog(); -->地址值不可以更改
        //d对象的属性依然可以改变：
        d.age = 10;
        d.weight = 13.7;
        //第3种情况：
        final Dog d2 = new Dog();
        a(d2);
        //第4种情况：
        b(d2);
    }
    public static void a(Dog d){
        d = new Dog();
    }
    public static void b(final Dog d){//d被final修饰 ，指向不可以改变
        //d = new Dog();
    }
}
```



【2】修饰方法；
final修饰方法，那么这个方法**不可以被该类的子类重写**：

![image-20210105160403830](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105160403830.png)

【3】修饰类；
**final修饰类**，代表没有子类，**该类不可以被继承**：
一旦一个类被final修饰，那么里面的方法也没有必要用final修饰了（final可以省略不写）

![image-20210105160414350](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105160414350.png)

【4】案例：JDK提供的Math类：看源码发现：
（1）使用Math类的时候无需导包，**直接使用**即可：

![image-20210105160425433](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105160425433.png)

（2）Math类没有子类，**不能被其他类继承**了

![image-20210105160435328](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105160435328.png)

（3）里面的属性全部被final修饰，方法也是被final修饰的，只是省略不写了
原因：**子类没有必要进行重写**。

（4）**外界不可以创建对象**：
Math m = new Math();

![image-20210105160444777](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105160444777.png)

（5）发现Math类中的所有的属性，方法都被**static**修饰
那么不用创建对象去调用，只能通过类名.属性名  **类名.方法名** 去调用

# 十六、抽象类，抽象方法

【1】抽象类和抽象方法的关系：
**抽象类中可以定义0-n个抽象方法。**
【2】抽象类作用：
在抽象类中定义抽象方法，目的是为了为子类提供一个**通用的模板**，子类可以在模板的基础上进行开发，**先重写父类的抽象方法，然后可以扩展子类自己的内容**。抽象类设计**避免了子类设计的随意性**，通过抽象类，子类的设计变得更加**严格**，进行某些程度上的**限制**。
使子类更加的通用。

【3】代码：

```java
package com.msb.test03;
//4.一个类中如果有方法是抽象方法，那么这个类也要变成一个抽象类。
//5.一个抽象类中可以有0-n个抽象方法
public abstract class Person {
    //1.在一个类中，会有一类方法，子类对这个方法非常满意，无需重写，直接使用
    public void eat(){
        System.out.println("一顿不吃饿得慌");
    }
    //2.在一个类中，会有一类方法，子类对这个方法永远不满意，会对这个方法进行重写。
    //3.一个方法的方法体去掉，然后被abstract修饰，那么这个方法就变成了一个抽象方法
    public abstract void say();
    public abstract void sleep();
}
//6.抽象类可以被其他类继承：
//7.一个类继承一个抽象类，那么这个类可以变成抽象类
//8.一般子类不会加abstract修饰，一般会让子类重写父类中的抽象方法
//9.子类继承抽象类，就必须重写全部的抽象方法
//10.子类如果没有重写父类全部的抽象方法，那么子类也可以变成一个抽象类。
class Student extends Person{
    @Override
    public void say() {
        System.out.println("我是东北人，我喜欢说东北话。。");
    }
    @Override
    public void sleep() {
        System.out.println("东北人喜欢睡炕。。");
    }
}
class Demo{
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //11.创建抽象类的对象：-->抽象类不可以创建对象
        //Person p = new Person();
        //12.创建子类对象：
        Student s = new Student();
        s.sleep();
        s.say();
        
        //13.多态的写法：父类引用只想子类对象：
        Person p  = new Student();
        p.say();
        p.sleep();
    }
}

```

【4】面试题：
（1）抽象类不能创建对象，那么抽象类中是否有构造器？
          抽象类中一定有构造器。构造器的作用  给子类初始化对象的时候要先super调用父类的构造器。

（2）抽象类是否可以被final修饰？
          不能被final修饰，因为抽象类设计的初衷就是给子类继承用的。要是被final修饰了这个抽象类了，就不存在继承了，就没有子类。

# 十七、接口

【1】接口声明格式：

```java
[访问修饰符]  interface 接口名   [extends  父接口1，父接口2…]  {
         常量定义；  //public static final     
         方法定义；	//public abstract
}
```



【2】代码：

```java
package com.msb.test04;
/**
 * 1.类是类，接口是接口，它们是同一层次的概念。
 * 2.接口中没有构造器
 * 3.接口如何声明：interface
 * 4.在JDK1.8之前，接口中只有两部分内容：
 * （1）常量：固定修饰符：public static final
 * （2）抽象方法：固定修饰符：public abstract
 * 注意：修饰符可以省略不写，IDE会帮你自动补全，但是初学者建议写上，防止遗忘。
 */
/**
 * java中的继承关系是单继承，如果拥有多个父类的时候，可以考虑使用接口进行实现
 *       java中的接口具备广泛的使用：
 *       用法：
 *           使用interface来修饰
 *           接口中可以包含多个方法，且方法跟抽象类中的抽象方法一致，可以不写实现，子类在实现的时候必须要实现代码逻辑
 *           子类实现接口使用implements关键字
 *       特征：
 *           1、接口中的所有方法都是抽象方法，不能包含方法的实现
 *           2、接口中的所有方法的访问修饰权限都是public，不写并不是默认访问权限，而是public
 *           3、接口不能被实例化
 *           4、接口的子类必须要实现接口中的所有方法，跟抽象类有所不同，抽象类中的抽象方法必须要被子类实现
 *           5、子类可以拥有实现多个接口  单继承多实现
 *           6、接口中的变量都是静态常量,如果变量没有使用static关键字修饰，它也表示静态常量,不用final关键字修饰，也是常量
 *           7、接口中的方法和常量无论是否添加public修饰，默认的权限有且仅有一个，就是public
 *
 *      接口的使用：
 *           1、接口代表一种能力，接口中可以定义N多个方法，子类在进行实现的时候，必须要实现这些方法
 *               将这些方法进行实现，就意味着具体了方法的能力
 *               关心实现类有何能力，而不关心实现细节
 *					2.接口代表一种约定，体现在接口名称和注释上
 									有些接口只有名称
 									方法的实现方式要通过注释来约定
 									程序设计时面向接口的约定而不考虑具体实现
 *      抽象类和接口的区别：
 *           1、抽象类中的方法可以有抽象方法，也可以有普通方法，但是接口中只能包含抽象方法
 *           2、抽象类需要使用abstract关键字来修饰，而接受使用interface关键字来修饰
 *           3、子类使用extends关键字来继承抽象类，使用implements来实现接口
 *           4、子类继承抽象类的时候必须要实现所有的抽象方法，普通方法可以不重写，而接口中的所有方法必须实现
 *           5、抽象类中可以定义成员变量，而接口中只能定义静态常量
 *           6、抽象类在子类实现的时候是单继承，而接口时多继承
 *           7、抽象类和接口都不能实例化，但是抽象类中可以有构造方法，而接口中不能有构造方法
 *           8、抽象类中可以实现接口，并且不实现接口中方法，而接口只能继承接口，不能实现接口
 *       注意：
 *           在实际的项目开发过程中，如果可以使用接口，尽量使用接口，将单继承的父类留在最关键的地方
 * */
public interface TestInterface01 {
    //常量：
    /*public static final*/ int NUM = 10;
    //抽象方法：
    /*public abstract*/ void a();
    /*public abstract*/ void b(int num);
    /*public abstract*/ int c(String name);
}
interface TestInterface02{
    void e();
    void f();
}
/*
5.类和接口的关系是什么？ 实现关系  类实现接口：
6.一旦实现一个接口，那么实现类要重写接口中的全部的抽象方法：
7.如果没有全部重写抽象方法，那么这个类可以变成一个抽象类。
8.java只有单继承，java还有多实现
一个类继承其他类，只能直接继承一个父类
但是实现类实现接口的话，可以实现多个接口
9.写法：先继承 再实现：extends Person implements TestInterface01,TestInterface02
 */
class Student extends Person implements TestInterface01,TestInterface02 {
    @Override
    public void a() {
        System.out.println("---1");
    }
    @Override
    public void b(int num) {
        System.out.println("---2");
    }
    @Override
    public int c(String name) {
        return 100;
    }
    @Override
    public void e() {
        System.out.println("---3");
    }
    @Override
    public void f() {
        System.out.println("---4");
    }
}
class Test{
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //10.接口不能创建对象：
        //TestInterface02 t = new TestInterface02();
        TestInterface02 t = new Student();//接口指向实现类 ---》多态
        //11.接口中常量如何访问：
        System.out.println(TestInterface01.NUM);
        System.out.println(Student.NUM);
        Student s = new Student();
        System.out.println(s.NUM);
        TestInterface01 t2 = new Student();
        System.out.println(t2.NUM);
    }
}

```

【3】接口的作用是什么？

定义规则，只是跟抽象类不同地方在哪？它是接口不是类。
接口定义好规则之后，实现类负责实现即可。

【4】
继承：子类对父类的继承
实现：实现类对接口的实现

手机  是不是  照相机  

继承：手机   extends 照相机     “is-a”的关系，手机是一个照相机 

上面的写法 不好：

实现：  手机    implements   拍照功能   “has-a”的关系，手机具备照相的能力

案例：飞机，小鸟，风筝
  定义一个接口： Flyable

我们前面用继承关系，描述了动物、哺乳动物、爬行动物的各种关系。

现在我们描述：

飞机、导弹、子弹、篮球、石头------》飞的方式     Flyable



【5】**多态的应用场合**：
（1）父类当做方法的形参，传入具体的子类的对象
（2）父类当做方法的返回值，返回的是具体的子类的对象
（3）接口当做方法的形参，传入具体的实现类的对象
（4）接口当做方法的返回值，返回的是具体的实现类的对象



【6】接口的相关规则

– 接口中所有方法都是抽象的 **public abstract**。 

– 即使没有显式的将接口中的成员用**public**标示，也是public访问类型的 

– 接口中变量默认用 **public static final**标示，所以接口中定义的变量就是**全局静态常量**。 



– 可以定义一个新接口，**新接口**用extends去**继承**一个**已有的接口** 

– 可以定义一个类，**类**用implements去**实现**一个**接口中所有方法**。 

– 可以定义一个抽象类，**抽象类**用implements去**实现**一个**接口中部分方法**。



【7】接口和抽象类的区别：

​    ![image-20210105160630810](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105160630810.png)

![image-20210105160639284](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105160639284.png)

接口就是比“抽象类”还“抽象”的“抽象类”，可以更加规范的对子类迚行约束。 全面地专业地实现了：**规范和具体实现的分离。****（解耦）**

 接口就是规范，定义的是一组规则，体现了现实世界中“如果你是…则必须 能…”的思想。如果你是天使，则必须能飞。如果你是汽车，则必须能跑。如果你好人，则必须干掉坏 人；如果你是坏人，则必须欺负好人。

接口的本质是契约，就像我们人间的法律一样。制定好后大家都遵守。 –

项目的具体需求是多变的，我们必须以不变应万变才能从容开发，此处的 “不变”就是“规范”。因此，我们开发项目往往都是**面向接口编程**



【8】上机练习

![image-20210108170755217](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108170755217.png)

![image-20210108170806931](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108170806931.png)











## JDK1.8以后的接口新增内容

在JDK1.8之前，接口中只有两部分内容：
（1）常量：固定修饰符：public static final
（2）抽象方法：固定修饰符：public abstract 

在JDK1.8之后，新增非抽象方法：
（1）被**public default**修饰的**非抽象方法**：
注意1：**default修饰符**必须要加上，否则出错
注意2：实现类中要是想**重写**接口中的非抽象方法，那么**default修饰符必须不能加**，否则出错。

```java
public interface TestInterface {
    //常量：
    public static final int NUM= 10;
    //抽象方法：
    public abstract void a();
    //public default修饰的非抽象方法：
    public default void b(){
        System.out.println("-------TestInterface---b()-----");
    }
}
class Test implements TestInterface{
    public void c(){
        //用一下接口中的b方法：
        b();//可以
        //super.b();不可以
        TestInterface.super.b();//可以
    }
    @Override
    public void a() {
        System.out.println("重写了a方法");
    }
    @Override
    public void b() {
    }
}
```





（2）静态方法：
注意1：static不可以省略不写
注意2：静态方法不能重写

```java
public interface TestInterface2 {
    //常量：
    public static final int NUM = 10;
    //抽象方法：
    public abstract  void a();
    //public default非抽象方法；
    public default void b(){
        System.out.println("-----TestInterface2---b");
    }
    //静态方法：
    public static void c(){
        System.out.println("TestInterface2中的静态方法");
    }
}
class Demo implements TestInterface2{
    @Override
    public void a() {
        System.out.println("重写了a方法");
    }
    public static void c(){
        System.out.println("Demo中的静态方法");
    }
}
class A {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Demo d = new Demo();
        d.c();
        Demo.c();
        TestInterface2.c();
    }
}
```

![image-20210107202250969](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210107202250969.png)

静态方法不重写



疑问：为什么要在接口中加入非抽象方法？？？
如果接口中只能定义抽象方法的话，那么我要是**修改接口中的内容**，那么对实现类的影响太大了，所有实现类都会受到影响。
现在在接口中加入**非抽象方法**，对实现类没有影响，想调用就去调用即可。



# 十八、内部类

把一个类定义在另一个类的内部称为**内部类**

```java
package com.mashibing.demo;//声明包
//声明外部类
class Outer
{
  //声明私有属性
	private String info="hello World";
  //声明内部类
	class Inner
	{
		public void print(){//打印输出的方法
			System.out.println(info);
		}
	}
  //定义方法
	public void fun(){
		new Inner().print();								//1.new Inner().print();通过内部类调用内部类方法
	}
}
	public class TestOuterAndInner2//测试类
	{
		public static void main(String [] args){
			new Outer().fun();//调用方法
		}
	} 
```



```java
package com.mashibing.innerdemo;

/**
 * @author: 马士兵教育
 * @create: 2019-09-01 15:04
 */
public class InnerClassDemo {

    private int id;
    private String name;

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

    public void show(){
        System.out.println("show");
//        System.out.println(age);
        InnerClass inner = new InnerClass();		//2.外部类访问内部类的私有方法必须先声明内部类
        System.out.println(inner.age);
    }

    class InnerClass{
        private int age;
//        static String name = "zhangsan";			//3.内部类不能有static静态方法

        public void test(){
            System.out.println("test");
            System.out.println(id);
            System.out.println(name);
        }
				
      	//5.内部类中嵌套内部类可以吗？
        class InnerInner{
            private int id;
            public void print(){
                System.out.println("print");
            }
        }
    }

    public static void main(String[] args) {
      //在main方法中声明内部类
        InnerClass innerClass = new InnerClassDemo().new InnerClass();
    }
}

```



```java
package com.mashibing.innerdemo;

/**
 * @author: 马士兵教育
 * @create: 2019-09-01 15:07
 */

/**
* 内部类（当作类中的一个普通成员变量，只不过此成员变量是class的类型）：
*       一个java文件中可以包含多个class，但是只能有一个public class
*       如果一个类定义在另一个类的内部，此时可以称之为内部类
*   使用：
*       创建内部类的时候，跟之前的方法不一样，需要在内部类的前面添加外部类来进行修饰
*             InnerClassDemo.InnerClass inner = new InnerClassDemo().new InnerClass();
    特点：
        1、内部类可以方便的访问外部类的私有属性
        2、外部类不能访问内部类的私有属性,但是如果创建了内部类的对象，此时可以在外部类中访问私有属性
        3、内部类中不能定义static静态属性
        4、当内部类和外部类具有相同的私有属性的时候，在内部类中访问的时候，可以直接访问内部类的属性(就近原则)，
            如果需要访问外部类的属性，那么需要添加  外部类类名.this.属性。
            如果属性是静态属性才能    外部类类名.属性。
    分类：
        匿名内部类：当定义了一个类，实现了某个接口的时候，在使用过程中只需要使用一次，没有其他用途
               其实考虑到代码编写的简洁，可以考虑不创建具体的类，而采用new interface(){添加未实现的方法}
               就叫做匿名内部类
        静态内部类：在内部类中可以定义静态内部类，使用static关键字进行修饰，使用规则
                外部类.内部类 类的引用名称 = new 外部类.内部类（）；
        方法内部类：在外部类的方法中也可以定义类，此时叫做方法内部类（了解即可）
                    使用的时候需要注意，只能在方法中创建对象，因为此class的作用域就是当前方法


 * */
public class TestInnerClass {
    public static void main(String[] args) {
//        System.gc();
        InnerClassDemo innerClassDemo = new InnerClassDemo();
        innerClassDemo.show();
        System.out.println(innerClassDemo.getName());

        InnerClassDemo.InnerClass inner = new InnerClassDemo().new InnerClass();
        inner.test();
//        System.out.println(inner.age);
				
      	//5.内部类的内部类的创建：
        InnerClassDemo.InnerClass.InnerInner innerInner = new InnerClassDemo().new InnerClass().new InnerInner();
    }
}

```

## 内部类的分类

### 匿名内部类：

当定义了一个类，实现了某个接口的时候，在使用过程中**只需要使用一次**，没有其他用途

其实考虑到代码编写的简洁，可以考虑**不创建具体的类**，而采用new interface(){添加未实现的方法}
就叫做**匿名内部类**

看样子是new 了一个接口，但是接口和抽象类都是不能实例化的，所以他们其实是**匿名内部类**

![image-20210108181442549](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108181442549.png)

### 静态内部类：

在内部类中可以定义静态内部类，使用static关键字进行修饰，使用规则
                外部类.内部类 类的引用名称 = new 外部类.内部类（）；

```java
package com.mashibing.innerdemo2;

/**
 * @author: 马士兵教育
 * @create: 2019-09-01 15:42
 */
public class StaticClass {

    private int id;

    public void test(){
        System.out.println("test");
    }
    static class InnerClass{
        private String name;
        public void show(){
          //不能访问外部类的id属性
            System.out.println("show");
        }

    }

    public static void main(String[] args) {
        InnerClass innerClass = new StaticClass.InnerClass();
      //当成一个静态成员成员用类名直接访问
//        InnerClass innerClass = new StaticClass().new InnerClass();

    }
}

```

使用static修饰的内部类不能访问非static 的外部属性

### 方法内部类：

在外部类的方法中也可以定义类，此时叫做方法内部类（了解即可）
                    使用的时候需要注意，只能在方法中创建对象，因为此class的作用域就是当前方法

```java
package com.mashibing.innerdemo2;

/**
 * @author: 马士兵教育
 * @create: 2019-09-01 15:50
 */
public class MethodInnerClass {

    public void show(int number){
        System.out.println("show");

        class InnerClass{
            private String name;
            public void test(int a){
                System.out.println("test");
                System.out.println(a);
                System.out.println(number);
            }
        }

        new InnerClass().test(12);
    }

    public static void main(String[] args) {
        MethodInnerClass  methodInnerClass = new MethodInnerClass();
        methodInnerClass.show(1234);

    }
}

```

注意事项：

（1）方法内部类不能在外部类的方法以外的地 方使用，所以方法内部类丌能使用访问控制符和static修饰符

（2）方法内部如果想使用方法的参数，那么参数前面必须加上final



## 成员内部类

```java
package com.msb.test07;
/**
 * 1.类的组成：属性，方法，构造器，代码块（普通块，静态块，构造块，同步块），内部类
 * 2.一个类TestOuter的内部的类SubTest叫内部类， 内部类 ：SubTest  外部类：TestOuter
 * 3.内部类：成员内部类 (静态的，非静态的) 和  局部内部类（位置：方法内，块内，构造器内）
 * 4.成员内部类:
 *      里面属性，方法，构造器等
 *      修饰符：private，default，protect，public，final,abstract
 */
public class TestOuter {
    //非静态的成员内部类：
    public class D{
        int age = 20;
        String name;
        public void method(){
            //5.内部类可以访问外部类的内容
            /*System.out.println(age);
            a();*/
            int age = 30;
            //8.内部类和外部类属性重名的时候，如何进行调用：
            System.out.println(age);//30
            System.out.println(this.age);//20
            System.out.println(TestOuter.this.age);//10
        }
    }
  
    //静态成员内部类：
    static class E{
        public void method(){
            //6.静态内部类中只能访问外部类中被static修饰的内容
            /*System.out.println(age);
            a();*/
        }
    }
    //属性：
    int age = 10;
    //方法：
    public void a(){
        System.out.println("这是a方法");
        {
            System.out.println("这是一个普通块");
            class B{
            }
        }
        class A{
        }
        //7.外部类想要访问内部类的东西，需要创建内部类的对象然后进行调用
        D d = new D();
        System.out.println(d.name);
        d.method();
    }
    static{
        System.out.println("这是静态块");
    }
    {
        System.out.println("这是构造块");
    }
    //构造器：
    public TestOuter(){
        class C{
        }
    }
    public TestOuter(int age) {
        this.age = age;
    }
}
class Demo{
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //创建外部类的对象：
        TestOuter to = new TestOuter();
        to.a();
        //9.创建内部类的对象：
        //静态的成员内部类创建对象：
        TestOuter.E e = new TestOuter.E();
        //非静态的成员内部类创建对象：
        //错误：TestOuter.D d = new TestOuter.D();
        TestOuter t = new TestOuter();
        TestOuter.D d = t.new D();
    }
}

```

![image-20210107203033253](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210107203033253.png)



## 局部内部类

```java
package com.msb.test08;
/**
 * @Auther: msb-zhaoss
 */
public class TestOuter {
    //1.在局部内部类中访问到的变量必须是被final修饰的
    public void method(){
        final int num = 10;
        class A{
            public void a(){
                //num = 20;
                System.out.println(num);
            }
        }
    }
    //2.如果类B在整个项目中只使用一次，那么就没有必要单独创建一个B类，使用内部类就可以了
    public Comparable method2(){
        class B implements Comparable{
            @Override
            public int compareTo(Object o) {
                return 100;
            }
        }
        return new B();
    }
    public Comparable method3(){
        //3.匿名内部类
        return new Comparable(){
            @Override
            public int compareTo(Object o) {
                return 200;
            }
        };
    }
    public void test(){
        Comparable com = new Comparable(){
            @Override
            public int compareTo(Object o) {
                return 200;
            }
        };
        System.out.println(com.compareTo("abc"));
    }
}

```



# 十九、面向对象项目

![image-20210105160848836](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105160848836.png)

