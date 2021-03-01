# 一、异常的概念

编译时可以通过的，但是运行时出错

异常:

​		在程序运行过程中，出现的不正常情况叫做异常

注意：
 * 1、相同的代码在运行的时候，根据**输入的参数或者操作**的不同，有可能会发生异常，有可能不会发生异常

   应该在写代码的过程中尽可能的保证代码的正确性，不要到处都bug

 * 2、如果要解决代码中出现的异常，需要添加非常复杂的**代码逻辑if**来进行判断，会使代码变得非常臃肿，不利于维护，可读性比较差

   因此，推荐大家使用**异常机制**来处理程序运行过程中出现的问题

 * 3、程序在运行过程中如果出现了问题，会导致后面的代码无法正常执行，而使用异常机制之后，可以对异常情况进行处理同时后续的代码会继续执行，不会中断整个程序

   ![image-20210108184650159](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108184650159.png)

 * 4、在异常的处理过程中，不要只是简单的输出错误，要尽可能的讲详细的异常信息进行输出    **e.printStackTrace():**     打印异常的**堆栈信息**，可以从异常信息的最后一行开始追踪，**寻找自己编写的java类**

   ​	**e.getMessage()**获得错误的相关信息

   | 方法名                 | 说 明                                                        |
   | ---------------------- | ------------------------------------------------------------ |
   | void printStackTrace() | 输出异常的堆栈信息                                           |
   | String getMessage()    | 返回异常信息描述字符串， 是printStackTrace()输出信息的一部分 |

   ![image-20210108190635689](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108190635689.png)

```java
package com.mashibing;

import java.io.File;
import java.util.InputMismatchException;
import java.util.Scanner;

/**
 * @author: 马士兵教育
 * @create: 2019-09-01 16:20
 */
public class TestException {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        try {
            System.out.print("请输入被除数:");
            int num1 = in.nextInt();
            System.out.print("请输入除数:");
            int num2 = in.nextInt();
            System.out.println(String.format("%d / %d = %d",
                    num1, num2, num1 / num2));
            System.out.println("前面没有出现异常");
        /*}catch(Exception e){
//            System.out.println("出现异常");
            e.printStackTrace();
//            System.out.println("--------");
            System.out.println(e.getMessage());
        }*/
       }catch(ArithmeticException e){
            System.out.println("数学异常，除数不能是0");
            e.printStackTrace();
        }catch (InputMismatchException e){
            System.out.println("输入的参数值类型不匹配");
            e.printStackTrace();
        }catch (NullPointerException e){
            System.out.println("空指针异常");
            e.printStackTrace();
        }
        System.out.println("感谢使用本程序！");

    }
}

```



# 二、异常的分类 

![image-20210108201446879](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108201446879.png)

Checked异常：编译时异常-----》必须声明或捕获抛出

Runtime异常：运行时异常，有时会异常，有时可能不会出错-----》不要求声明或捕获抛出

| 异 常 类 型                    | 说 明                                 |
| ------------------------------ | ------------------------------------- |
| Exception                      | 异常层次结构的父类                    |
| ArithmeticException            | 算术错误情形，如以零作除数            |
| ArrayIndexOutOfBoundsException | 数组下标越界                          |
| NullPointerException           | 尝试访问 null 对象成员                |
| ClassNotFoundException         | 不能加载所需的类                      |
| IllegalArgumentException       | 方法接收到非法参数                    |
| ClassCastException             | 对象强制类型转换出错                  |
| NumberFormatException          | 数字格式转换异常，如把"abc"转换成数字 |





# 三、异常处理（try, catch, finally, throws, throw）

Java的异常处理是通过5个关键字来实现的：try、catch、 finally、throw、throws



![image-20210108184820410](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108184820410.png)

## try-catch块

```java
/**异常处理的方式：
*          1、捕获异常
*              try{代码逻辑}catch(Exception e){异常处理逻辑}
*              try{代码逻辑}catch(具体的异常Exception e){异常处理逻辑}catch(具体的异常)：
*          		可以针对每一种具体的异常做相应的更丰富的处理
*          注意：当使用多重的catch()的时候一定要注意相关异常的顺序，将子类放在最前面的catch()，父类放在后面的catch()
*          3、执行过程中可能存在的情况：
*             1、正常执行，只执行try{}中的代码
*             2、遇到异常情况，会处理try{}中异常代码之前的逻辑，后面的逻辑不会执行，最后会执行catch(){....}中的代码
*             3、使用多重catch(){....}的时候，会遇到异常子类不匹配的情况，此时依然会报错，因此建议在catch的最后将所有的异常的父类写上
*InputMismatchException
* ArithmeticException
*/
```

![image-20210108185236176](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108185236176.png)

![image-20210108185308451](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108185308451.png)

![image-20210108185338859](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108185338859.png)

## try-catch-finally块

![image-20210108191752011](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108191752011.png)

![image-20210108193752751](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108193752751.png)

### 面试代码问题

```java
1、情况一（try中有return，finally中没有return）：
	public class TryTest{
		public static void main(String[] args){
			System.out.println(test());
		}
	
		private static int test(){
			int num = 10;
			try{
				System.out.println("try");
				return num += 80;
			}catch(Exception e){
				System.out.println("error");
			}finally{
				if (num > 20){
					System.out.println("num>20 : " + num);
				}
				System.out.println("finally");
			}
			return num;
		}
	}
```

![image-20210108193028727](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108193028727.png)

分析：显然“return num += 80”被拆分成了“num = num+80”和“return num”两个语句，线执行try中的“num = num+80”语句，将其保存起来，在try中的”return num“执行前，先将finally中的语句执行完，而后再将90返回。


```java
2、情况二（try和finally中均有return）：
	public class TryTest{
		public static void main(String[] args){
			System.out.println(test());
		}
	
		private static int test(){
			int num = 10;
			try{
				System.out.println("try");
				return num += 80;
			}catch(Exception e){
				System.out.println("error");
			}finally{
				if (num > 20){
					System.out.println("num>20 : " + num);
				}
				System.out.println("finally");
				num = 100;
				return num;
			}
		}
	}
```

![image-20210108193146222](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108193146222.png)

分析：try中的return语句同样被拆分了，finally中的return语句先于try中的return语句执行，因而try中的return被”覆盖“掉了，不再执行。


```java
3、情况三（finally中改变返回值num）：
public class TryTest{
	public static void main(String[] args){
		System.out.println(test());
	}
 
	private static int test(){
		int num = 10;
		try{
			System.out.println("try");
			return num;
		}catch(Exception e){
			System.out.println("error");
		}finally{
			if (num > 20){
				System.out.println("num>20 : " + num);
			}
			System.out.println("finally");
			num = 100;
		}
		return num;
	}
}
```

![image-20210108193304212](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108193304212.png)

分析：虽然在finally中改变了返回值num，但因为finally中没有return该num的值，因此在执行完finally中的语句后，test（）函数会得到try中返回的num的值，而try中的num的值依然是程序进入finally代码块前保留下来的值，因此得到的返回值为10。


```java
情况四（将num的值包装在Num类中）：

public class TryTest{
	public static void main(String[] args){
		System.out.println(test().num);
	}
 
	private static Num test(){
		Num number = new Num();
		try{
			System.out.println("try");
			return number;
		}catch(Exception e){
			System.out.println("error");
		}finally{
			if (number.num > 20){
				System.out.println("number.num>20 : " + number.num);
			}
			System.out.println("finally");
			number.num = 100;
		}
		return number;
	}
}
 
class Num{
	public int num = 10;
}

```

![image-20210108193356685](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108193356685.png)

分析：从结果中可以看出，同样是在finally中改变了返回值num的值，在情况三中，并没有被try中的return返回（test（）方法得到的不是100），但在这里却被try中的return语句返回了。

```tex
总结：
	 try语句在返回前，将其他所有的操作执行完，保留好要返回的值，而后转入执行finally中的语句，而后分为以下三种情况：

    情况一：如果finally中有return语句，则会将try中的return语句”覆盖“掉，直接执行finally中的return语句，得到返回值，这样便无法得到try之前保留好的返回值。

    情况二：如果finally中没有return语句，也没有改变要返回值，则执行完finally中的语句后，会接着执行try中的return语句，返回之前保留的值。

    情况三：如果finally中没有return语句，但是改变了要返回的值，这里有点类似与引用传递和值传递的区别，分以下两种情况，：

        1）如果return的数据是基本数据类型或文本字符串，则在finally中对该基本数据的改变不起作用，try中的return语句依然会返回进入finally块之前保留的值。

        2）如果return的数据是引用数据类型，而在finally中对该引用数据类型的属性值的改变起作用，try中的return语句返回的就是在finally中改变后的该属性的值。

```

## 多重catch块

引发多种类型的异常 

– 排列catch 语句的顺序：**先子类后父类** 

– 发生异常时**按顺序逐个**匹配 

– **只执行****第一个**不异常类型匹配的catch语句

```java
public void method(){
	try {
		 // 代码段
		 // 产生异常(异常类型2)
	} catch (异常类型1 ex) {
		 // 对异常进行处理的代码段
	} catch (异常类型2 ex) {
		 // 对异常进行处理的代码段
	} catch (异常类型3 ex) {
 		 // 对异常进行处理的代码段
	}
	// 代码段
}
```

## throws声明异常

![image-20210108194514337](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108194514337.png)

```java
package com.mashibing;

import java.io.File;
import java.io.FileInputStream;

/**
 * @author: 马士兵教育
 * @create: 2019-09-07 15:28
 */
/**
throws:声明异常
* 在异常情况出现的时候，可以使用try...catch...finally的方式对异常进行处理，除此之外，可以将异常向外跑出，由外部的进行处理
*   1、在方法调用过程中，可以存在N多个方法之间的调用，此时假如每个方法中都包含了异常情况    f1(){f2(){f3(){}}}
*       那么就需要在每个方法中都进行try。。catch 非常的麻烦，另外一种比较简单的方式，就是在方法的最外层f1() throws 调用处理一次即可
*       使用throws的方法，对所有执行过程中的所有方法出现的异常进行统一集中处理
*   2、如何判断是使用throws还是使用try...catch..
*       最稳妥的方式是在每个方法中都进行异常的处理
*       偷懒的方式是判断在整个调用的过程中，外层的调用方法是否有对异常的处理，如果有，直接使用throws,如果没有
*           那么就要使用try...catch...
* throw：抛出异常
*
* */
public class Excepton2 {
    public static void main(String[] args) {
        try {
            show();
        } catch (GenderException e) {
            e.printStackTrace();
        }

//        new FileInputStream(new File(""));
        System.out.println("hehe");
    }

    public static void show() throws GenderException{
        String gender = "1234";
        if (gender.equals("man")){
            System.out.println("man");
        }else if(gender.equals("woman")){
            System.out.println("woman");
        }else{
//            throw new Exception("性别出现错误");
          //throw抛出异常，需要和throws配合使用
            throw new GenderException("gender is wrong");
        }
    }

		//注释doc中问题1
    public static void test1() throws Exception{
        System.out.println(1/0);
    }
    public static void test2() throws Exception {
        test1();
        System.out.println(100/0);
    }
    public static void test3() throws Exception{
        test2();
    }
    public static void test4() throws Exception{
        test3();
    }
}

```

## throw抛出异常

```java
    public static void show() throws GenderException{
        String gender = "1234";
        if (gender.equals("man")){
            System.out.println("man");
        }else if(gender.equals("woman")){
            System.out.println("woman");
        }else{
//            throw new Exception("性别出现错误");
          //throw抛出异常，需要和throws配合使用
            throw new GenderException("gender is wrong");
        }
    }
```



# 四、异常和重写的关系

# 五、自定义异常

自定义异常：

在java的api中提供了非常丰富的异常类，但是在某些情况下不太满足我们的需求，此时需要自定义异常

步骤：

![image-20210108202144653](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108202144653.png)

1、**继承Exception类**

2、**自定义实现构造方法**

3、需要使用的时候，使用**throw new 自定义异常的名称**；

什么时候需要自定义异常？

**一般情况下不需要**

但是在公司要求明确，或者要求**异常格式规范统一**的时候是必须要自己实现的


```java
package com.mashibing;

/**
 * @author: 马士兵教育
 * @create: 2019-09-07 15:44
 */
public class GenderException extends Exception {

    public GenderException(){
        System.out.println("性别异常");
    }

    public GenderException(String msg){
        System.out.println(msg);
    }
}

```



```java
 throw new GenderException("gender is wrong");
```



# 六、Jdk7-12异常处理



# 一、基本数据类型的包装类

包装类是将基本类型封装到一个类中 

​	包含**属性**和**方法**，方便对象操作 

包装类位于**java.lang**包中

![image-20210108202234044](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108202234044.png)

## 包装类与基本数据类型

包装类是将基本数据类型封装成一个类，包含属性和方法

使用：

​	在使用过程中，会涉及到自动装箱和自动拆箱

*       装箱：将**基本数据类型**转换成**包装类**
*       拆箱：将**包装类**转换成**基本数据类型**

```java
package com.mashibing;
/**
 * @author: 马士兵教育
 * @create: 2019-09-07 16:09
 */

public class IntegerDemo {
    public static void main(String[] args) {
//        int a = 10;
//        Integer i = new Integer(10);
      		System.out.println(a == i);				//true
//        //通过方法进行类型的转换
//        Integer i2 = Integer.valueOf(a);	//装箱
//        int i3 = i.intValue();						//拆箱
//        System.out.println(a == i);
      
//        Float f1 = new Float(3.14);
//        Double d1 = new Double(3.14);
//        int i =100;
//        Integer i1 = 100;
//        Integer i2 = 100;
//        Integer i3 = 200;
//        Integer i4 = 200;
//        System.out.println(i1==i2);				//true
//        System.out.println(i3==i4);				//flase   
      		//必须在-127到127之间的数才能在cache[]找到对应的值，如果找不到的的话，会return new Integer对象，造成不在同一个堆空间中
/*
*public static Integer valueOf(int i){
	if(i>=IntegerCache.low&&i<=IntegerCache.high)
	return IntegerCache.cache[i+(-IntegerCache.low)];
return new Integer(i);
}
*/
//        Double d1 = 1.0;
//        Double d2 = 1.0;
//        Double d3 = 2.0;
//        Double d4 = 2.0;
//        System.out.println(d1==d2);		//false
//        System.out.println(d3==d4);		//false
      //return new Double(parseDouble(s));

        Integer i = 10;
        int a = i;
        System.out.println(a==i);			//true  会将Integer类型自动拆箱
    }
}

```



## 自动装箱

基本类型就自动地封装到与它相同类型的包装中，如： 

– Integer i = 100; 

– 本质上是，**编译器**编译时为我们添加了： 

– Integer i = Integer.valueOf(100);

## 自动拆箱

包装类对象自动转换成基本类型数据。如： 

– int a = new Integer(100); 

– 本质上，**编译器**编译时为我们添加了： 

– int a = new Integer(100).intValue()

```java
1、装箱 与拆箱
装箱: 基本 -->类
	new Integer(int)
	Integer.valueOf(int i) ;
拆箱: 类 -->基本
intValue()
2、方法
1)、与字符串转换的方法
a)、字符串 -->Integer
	Integer(String s)
	Integer.parseInt(String s)
	Integer.valueOf(String s);
b)、Integer -->字符串
	toString()
	String.valueOf(Object obj) ;
	Integer -->int +""
```



# 二、字符串相关类

 **字符串**的本质
*               字符串的本质是**字符数组**或者叫做**字符序列**
*               String类使用**final**修饰，不可以被继承
*               使用**equals方法**比较的是字符数组的**每一个位置的值**
*               String是一个**不可变对象**(数组的引用不能变)（而不是堆中”abcde“这个对象a[n]的值不能变）反射中就可以改变

![image-20210108210236256](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108210236256.png)

常量池在1.7之后放置于堆空间中

```java
package com.mashibing;

/**
 * @author: 马士兵教育
 * @create: 2019-09-07 16:28
 */
public class StringDemo {
    public static void main(String[] args) {
        String str = "abc";
        String str2 = new String("abc");
//        str2 = str2.intern();						//==  的结果成为true
        System.out.println(str==str2);     //false  比较的是栈中地址值
        System.out.println(str.equals(str2));		//true  每一位的值进行比较
        System.out.println(str.charAt(0));  //String字符串0-n-1进行存储
        //数组的复制过程
      	//完成字符串的拼接
        System.out.println(str.concat("cde"));
        //返回指定下标的元素
        System.out.println(str.indexOf("a"));
        String s = "abcdefghijklmn";
      	//在截取字符串的时候，填入的是子字符串开始的位置
        System.out.println(s.substring(3));	//defghijklmn
        //在截取字符串的时候，需要注意是左闭右开区间
        System.out.println(s.substring(3,5));//de
        System.out.println(s.length());//计算字串的长度
        System.out.println("-----------------");
//        String a = "abc";
//        String b = new String("abc");
//        b = b.intern();
//        System.out.println(a==b);			//true
      //intern()详解：
      //原因：当调用intern方法时，如果池已经包含与equals(Object)方法确定的相当于此String对象的字符串，则返回来自池的字符串。 否则，此String对象将添加到池中，并返回对此String对象的引用。看看b是不是在常量池中存放 
      //结果 
      //一个字符串与该字符串具有相同的内容，但保证来自一个唯一的字符串池。 


        String a = "abc";
        String b = "def";
        String c = "abcdef";
        System.out.println(c==d);  //false  d在编译的时候并不知道它指向的是什么，a、b
        String d = a+b;
        String e = "abc"+"def";
      	System.out.println(c==e);   //true
      	
      	String d = (a+b).intern();
      	System.out.println(c==d);		//true   "abcdef"在常量池中之能存在于一次
     
        String f = "a" + "b" +"c";
        String a1 = "a";
        String a2 = "b";
        String a3 = "c";							
        String f1 = a1+a2+a3;
															//在堆中一共有 四个 对象"abc" "a" "b" "c"

    }
}

```

## 字符串的相关用法

Java字符串就是Unicode字符序列，例如串“Java”就是4个 Unicode字符J,a,v,a组成的。 

▪Java允许使用符号"+"把两个字符串连接起来 

```java
String s1 = “Hello”;String s2 = “World!”;
String s = s1 + s2; 		//HelloWorld!
```

| 代码                                                         | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| char charAt(int index)                                       | 返回字符串中第index个字符。                                  |
| boolean equals(String other)                                 | 如果字符串与other相等，返回true                              |
| boolean equalsIgnoreCase(String other)                       | 如果字符串与other相等（忽略大小写），则返回true              |
| int indexOf(String str)      lastIndexOf(String str,int idx) |                                                              |
| int length()                                                 | 返回字符串的长度。                                           |
| String replace(char oldChar,char newChar)                    | 返回一个新串，它是通过用 newChar 替换此字符串中出现的所有oldChar而生成的 |
| boolean startsWith(String prefix)                            | 如果字符串以prefix开始，则返回true                           |
| boolean endsWith(String prefix)                              | 如果字符串以prefix结尾，则返回true                           |
| String substring(int beginIndex)                             |                                                              |
| String substring(int beginIndex,int endIndex)                | 返回一个新字符串，该串包含从原始字符串beginIndex到串尾戒endIndex-1的所有字符（**左闭右开**） |
| String toLowerCase()                                         | 返回一个新字符串，该串将原始字符串中的所有大写字母改成小写字母 |
| String trim()                                                | 返回一个新字符串，该串删除了原始字符串头部和尾部的空格       |
| String toUpperCase()                                         | 返回一个新字符串，该串将原始字符串中的所有小写字母改成大写字母 |

## 字符串的比较内存分析

![image-20210108213755018](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108213755018.png)

## 字符串的提取与拆分

字符串的提取

![image-20210108214242922](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108214242922.png)

![image-20210108214304452](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108214304452.png)

字符串的拆分

有一段歌词，每句都以空格“ ”结尾，请将歌词每句按行输出

![image-20210108214437220](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108214437220.png)

| 方法           | 说明                                               |
| -------------- | -------------------------------------------------- |
| String split() | 将一个字符串分割为子字符串，结果作为字符串数组返回 |

## StringBuffer类与StringBuilder类

StringBuffer：String增强版      -------    **字符串缓冲区**，是一个**容器**

声明

```java
//创建空StringBuffer对象
StringBuffer sb = new StringBuffer();
//创建一个变量存储字符串aaa
StringBuffer sb = new StringBuffer("aaa");

sb.toString(); //转化为String类型
```

使用

```java
sb.append("**"); //追加字符串
```



```java
package com.mashibing;

/**
 * @author: 马士兵教育
 * @create: 2019-09-07 20:04
 */
/**
* 可变字符串
*   StringBuffer：线程安全，效率低
*   StringBuilder: 线程不安全，效率高
*		线程可以理解为同时存取   账户中一边存，一边取
*
* */
public class StringBufferDemo {
    public static void main(String[] args) {
        StringBuffer stringBuffer = new StringBuffer();
        stringBuffer.append(1).append(1.234).append("abc").append(true);
        System.out.println(stringBuffer); //11.234abctrue
        System.out.println(stringBuffer.length());//13
        System.out.println(stringBuffer.capacity());//16,长度并没有占满
        StringBuilder stringBuilder = new StringBuilder();
        stringBuilder.append("123").append(1).append(false);
        System.out.println(stringBuilder);
    }
}

```



## String、StringBuffer、StringBuilder对比：

String：不可变字符序列

StringBuilder：可变字符序列、效率高、线程不安全

StringBuffer：可变字符序列、效率低、线程安全

## String使用陷阱：

```java
  string s="a"; //创建了一个字符串 

  s=s+"b"; //实际上原来的"a"字符串对象已经丢弃了，现在又产生了一个字符串 s+"b"。
```

如果多次执行这些改变串内容的操作，会导致大量副本字符串对象存留在内 存中，降低效率。如果这样的操作放到循环中，会极大影响程序的性能。

# 三、时间处理相关类

![image-20210108215631250](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108215631250.png)

```java
package com.mashibing;

import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;

/**
 * @author: 马士兵教育
 * @create: 2019-09-07 20:14
 */
public class DateDemo {
    public static void main(String[] args) throws ParseException {
        Date date = new Date();
        System.out.println(date);  //Fri Jan 08 21:57:12 CST 2021
      
        System.out.println(date.getTime());//返回当时时间的毫秒值   1610114232245
      
        DateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");//其实SimpleDateFormat是DateFormat的子类，这是个向上转型（用于定制日期时间的格式y-M-d H:m:s）   2021-01-08 21:57:12
        //将Date类按照规范转换为字符串格式
        String str = dateFormat.format(date);
        System.out.println(str);
      
        //将字符串转换成对应的日期类
        Date d1 = dateFormat.parse("2010-10-10 20:20:20");
        System.out.println(d1); 
      //Sun Oct 10 20:20:20 CST 2010
      
        
      // Calendar是protected修饰的，在子类中访问
      //获取的是当前系统的时间
        Calendar calendar = Calendar.getInstance();
        System.out.println(calendar);    //java.util.GregorianCalendar[time=1610114232299,areFieldsSet=true,areAllFieldsSet=true,lenient=true,zone=sun.util.calendar.ZoneInfo[id="Asia/Shanghai",offset=28800000,dstSavings=0,useDaylight=false,transitions=31,lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,YEAR=2021,MONTH=0,WEEK_OF_YEAR=2,WEEK_OF_MONTH=2,DAY_OF_MONTH=8,DAY_OF_YEAR=8,DAY_OF_WEEK=6,DAY_OF_WEEK_IN_MONTH=2,AM_PM=1,HOUR=9,HOUR_OF_DAY=21,MINUTE=57,SECOND=12,MILLISECOND=299,ZONE_OFFSET=28800000,DST_OFFSET=0]

     
        //设置指定时间的日历类
        calendar.setTime(d1);
        System.out.println(calendar);
 //java.util.GregorianCalendar[time=1286713220000,areFieldsSet=true,areAllFieldsSet=true,lenient=true,zone=sun.util.calendar.ZoneInfo[id="Asia/Shanghai",offset=28800000,dstSavings=0,useDaylight=false,transitions=31,lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,YEAR=2010,MONTH=9,WEEK_OF_YEAR=42,WEEK_OF_MONTH=3,DAY_OF_MONTH=10,DAY_OF_YEAR=283,DAY_OF_WEEK=1,DAY_OF_WEEK_IN_MONTH=2,AM_PM=1,HOUR=8,HOUR_OF_DAY=20,MINUTE=20,SECOND=20,MILLISECOND=0,ZONE_OFFSET=28800000,DST_OFFSET=0]

  //Calendar中的常量池    
     System.out.println(calendar.get(Calendar.YEAR));//2010
      System.out.println(calendar.get(Calendar.MONTH));//9
        System.out.println(calendar.get(Calendar.DAY_OF_MONTH));//10
        System.out.println(calendar.get(Calendar.HOUR_OF_DAY));//20
        System.out.println(calendar.get(Calendar.MINUTE));//20
        System.out.println(calendar.get(Calendar.SECOND));//20

    }
}

```

## Date时间类

Date类：表示日期和时间 

​	提供操作日期和时间各组成部分的方法 

DateFormat类 与SimpleDateFormat类 

​	用于定制日期时间的格式

```java
Date date = new Date(); //创建日期对象
SimpleDateFormat formater = new SimpleDateFormat("yyyy-
 MM-dd HH:mm:ss");//定制日期格式
String now = formater.format(date);
System.out.println(now);

```



## Calendar

Calendar类： 

抽象类 

用于设置和获取日期/时间数据的特定部分 

​	Calendar类提供一些**方法**和**静态字段**来操作日历

| 方法或属性         | 说明                 |
| ------------------ | -------------------- |
| int get(int field) | 返回给定日历字段的值 |
| MONTH              | 指示月               |
| DAY_OF_MONTH       | 指示一个月中的某天   |
| DAY_OF_WEEK        | 指示一个星期中的某天 |



# 四、Math类

采用静态导包 的方式

```java
import static java.lang.Math
int a = (int)(10*random());
```

包含了常见的数学运算函数。 

▪ random()	生成[0,1)之间的随机浮点数 

```java
//生成：0-10之间的任意整数： 
int a = (int)(10*Math.random());

//生成：20-30之间的任意整数： 
int b = 20 + (int)(10*Math.random());
```



```java
package com.mashibing;

/**
 * @author: 马士兵教育
 * @create: 2019-09-07 20:42
 */
public class MathDemo {
    public static void main(String[] args) {
        System.out.println(Math.abs(-1));//1
        System.out.println(Math.sqrt(2));//1.4142135623730951
        System.out.println(Math.ceil(-3.14));//-3.0
        System.out.println(Math.floor(-3.14));//-4.0
        System.out.println(Math.pow(2,3));//8.0

    }
}

```



# 五、File类

# 六、枚举类 Jdk1.5

枚举指由**一组固定的常量组成的类型**

枚举类也是一种类，也包括了属性，也包括了方法

```java
[Modifier] enum enumName{
 enumContantName1[，
enumConstantName2...[;]]
 //[field，method]
}
```

```java
package com.mashibing;

public enum EventEnum {
//这才是真正的枚举
    LAUNCH("launch"),PAGEVIEW("pageview"),EVENT("event");

    EventEnum(String name){
        this.name = name;
    }
  //可以定义属性
    private String name;
	//可以定义方法
    public void show(){
        System.out.println(this.name);
        EventEnum[] ee = values();
        for(int i = 0;i<ee.length;i++){
            System.out.println(ee[i]);
        }
    }

}

```

```java
package com.mashibing;

public enum Gender {
    男,女
}

```

```java
package com.mashibing;

/**
 * @author: 马士兵教育
 * @create: 2019-09-07 20:47
 */
public class Test {
  	//枚举最简单的应用
    Gender gender = Gender.女;
    Gender gender2 = Gender.男;

    public static void main(String[] args) {
        EventEnum ee = EventEnum.LAUNCH;
        ee.show();
        String name = EventEnum.PAGEVIEW.name();
        System.out.println(name);
    }
}

```

![image-20210108223108972](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210108223108972.png)

枚举总结：

 枚举类型：

1. 只能够取**特定值**（男、女）中的一个 
2. 使用**enum**关键字 
3. 所有的枚举类型隐性地继承自 java.lang.Enum。（枚举实质上还是类！ 而每个被枚举的成员实质就是一个枚举类型的实例，他们默认都是**public static final**的。可以直接通过**枚举类型名**直接使用它们。） 
4.  强烈建议当你需要**定义一组常量**时，使用**枚举类型**