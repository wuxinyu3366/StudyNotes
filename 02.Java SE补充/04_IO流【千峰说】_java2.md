# I/O流框架

# 一、流的概念

**内存**与**存储设备**之间传输数据的**通道**

![image-20210112111416474](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210112111416474.png)

# 二、流的分类

1. 按方向
   - 输入流：将**<存储设备>**中的内容读到**<内存>**中
   - 输出流：将**<内存>**中的内容写到**<存储设备>**中
   - ![image-20210112111519121](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210112111519121.png)
2. 按单位
   - 字节流：以**字节**为单位，可以读写所有数据
   - 字符流：以**字符**为单位，只能读写文本数据
3. 按功能
   - 节点流：具有**实际传输数据**的读写功能
   - 过滤流：在节点流的基础之上**增强功能**

# 三、字节流

字节流的父类（抽象类）

```java
//InputStream 字节输入流 
//这个抽象类是表示输入字节流的所有类的超类。
public int read(){}						//从输入流读取数据的下一个字节。 
public int read(byte[] b){}		//从输入流读取一些字节数，并将它们存储到缓冲区 b 。
public int read(byte[] b, int off, int len){} //从输入流读取最多 len字节的数据到一个字节数组。

// OutputStream 字节输出流
//这个抽象类是表示字节输出流的所有类的超类。 输出流接收输出字节并将其发送到某个接收器。 
public void write(int n){}  //将指定的字节写入此输出流。 
public void write(byte[] b){}	//将 b.length字节从指定的字节数组写入此输出流。
public void write(byte[] b, int off, int len){} //从指定的字节数组写入 len个字节，从偏移 off开始输出到此输出流。 
```

## 1.文件字节流

文件输入流 `FileInputStream`

- `FileInputStream`从文件系统中的文件获取输入字节。
- `FileInputStream`用于读取诸如图像数据的原始字节流。

```java
package com.qf.chapter15_1;

import java.io.FileInputStream;

/**
 * 演示FileInputStream的使用
 * 文件字节输入流
 * @author wgy
 *
 */
public class Demo1 {
	public static void main(String[] args) throws Exception{
		//1创建FileInputStream,并指定文件路径
		FileInputStream fis=new FileInputStream("D:\\Programming File\\TestJavaSE\\aaa.txt");

		//2读取文件
		//fis.read(); //读取完成后返回-1
		//2.1单个字节读取
//		int data=0;
//		while((data=fis.read())!=-1) { //只要返回的不是-1，说明没有读完，继续读取
//			System.out.print((char)data);
//		}
		//2.2一次读取多个字节

//		byte[] buf=new byte[3]; // 大小为3的缓存区
//		int count = fis.read(buf);// 一次读3个
//		System.out.println(new String(buf));
//		System.out.println(count);
//		int count2 = fis.read(buf); // 再读3个
//		System.out.println((new String(buf)));
//		System.out.println((count2));
		
		byte[] buf=new byte[1024];
		int count=0;
		while((count=fis.read(buf))!=-1) {
			System.out.println(new String(buf,0,count));
		}
		
		//3关闭
		fis.close();
		System.out.println();
		System.out.println("执行完毕");
	}
}

```

文件输出流 `FileOutputStream`

- 文件输出流是用于将数据写入到输出流`File`或一个`FileDescriptor` 。  文件是否可用或可能被创建取决于底层平台。  特别是某些平台允许一次只能打开一个文件来写入一个`FileOutputStream` （或其他文件写入对象）。  在这种情况下，如果所涉及的文件已经打开，则此类中的构造函数将失败。
- `FileOutputStream`用于写入诸如图像数据的原始字节流。

```java
package com.qf.chapter15_1;

import java.io.FileOutputStream;

/**
 * 演示文件字节输出流的使用
 * FileOutputStream
 * @author wgy
 *
 */
public class Demo2 {
	public static void main(String[] args) throws Exception{
		//1创建文件字节输出流对象
		FileOutputStream fos=new FileOutputStream("D:\\Programming File\\TestJavaSE\\bbb.txt",true); // true表示不覆盖 接着写 
		//2写入文件
//		fos.write(97);
//		fos.write('b');
//		fos.write('c');
		String string="helloworld";
		fos.write(string.getBytes());
		//3关闭
		fos.close();
		System.out.println("执行完毕");
	}
}

```

## 2.图片复制案例

```java
package com.qf.chapter15_1;

import java.io.FileInputStream;
import java.io.FileOutputStream;

/**
 * 使用文件字节流实现文件的复制
 * @author wgy
 *
 */
public class Demo3 {
	public static void main(String[] args) throws Exception{
		//1创建流
		//1.1文件字节输入流
		FileInputStream fis=new FileInputStream("D:\\Programming File\\TestJavaSE\\001.jpg");
		//1.2文件字节输出流
		FileOutputStream fos=new FileOutputStream("D:\\Programming File\\TestJavaSE\\002.jpg");
		//2一边读，一边写
		byte[] buf=new byte[1024];
		int count=0;
		while((count=fis.read(buf))!=-1) {
			fos.write(buf,0,count);
		}
		//3关闭
		fis.close();
		fos.close();
		System.out.println("复制完毕");	
	}
}

```

## 3.字节缓冲流

缓冲流：`BufferedInputStream`/`BufferedOutputStream`

- 提高IO效率，减少访问磁盘次数

- 数据存储在缓冲区中，flush是将缓冲区的内容写入文件中，也可以直接close

  

```java
package com.qf.chapter15_1;
public class Demo4 {
// 使用字节缓冲流 读取 文件
psvm(String[] args) throws Exception{
  // 1 创建BufferedInputStream
  FileInputStream fis = new FileInputStream("路径");
  BufferedInputStream bis = new BufferedInputStream(fis);//增强fis流
  // 2 读取
  int data = 0;
  while((data = bis.read()) != -1){
    sout((char)data);
  }
  // 用自己创建的缓冲流
  byte[] buf = new byte[1024];
  int count = 0;
  while((count = bis.read(buf)) != -1){
    sout(new String(buf, 0, count));
  }
  
  // 3 关闭
  bis.close();
}
}
```



```java
package com.qf.chapter15_1;
public class Demo5 {
// 使用字节缓冲流 写入 文件
psvm(String[] args) throws Exception{
  // 1 创建BufferedInputStream
  FileOutputStream fos = new FileOutputStream("路径");
  BufferedOutputStream bis = new BufferedOutputStream(fos);
  // 2 写入文件
  for(int i = 0; i < 10; i ++){
    bos.write("hello".getBytes());// 写入8k缓冲区
    bos.flush(); // 刷新到硬盘
  }
  // 3 关闭（内部调用flush方法）
  bos.close();
}
}
```

# 四、对象流

```
ObjectOutputStream / ObjectInputStream
```

- 增强了**缓冲区**功能
- 增强了**读写**8种基本数据类型和字符串的功能
- 增强了**读写对象**的功能
  - `readObject()` 从流中读取一个对象
  - `writeObject(Object obj)` 向流中写入一个对象

使用流传输对象的过程称为**序列化**、**反序列化**

# 五、序列化与反序列化

```java
package com.qf.chapter15_1;

import java.io.Serializable;

/**
 * 学生类
 * @author wgy
 *
 */
public class Student implements Serializable{

	/**
	 * serialVersionUID:序列化版本号ID,
	 */
	private static final long serialVersionUID = 100L;
	private String name;
	private transient int age;
	
	public static String country="中国";
	
	public Student() {
		// TODO Auto-generated constructor stub
	}
	public Student(String name, int age) {
		super();
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
		return "Student [name=" + name + ", age=" + age + "]";
	}

}
```



## 1.序列化(写)

```java
package com.qf.chapter15_1;

import java.io.FileOutputStream;
import java.io.ObjectOutputStream;
import java.util.ArrayList;

/**
 * 使用ObjectOutputStream实现对象的序列化
 * 注意事项：
 * (1)序列化类必须要实现Serializable接口
 * (2)序列化类中对象属性要求实现Serializable接口
 * (3)序列化版本号ID serialVersionUID,保证序列化的类和反序列化的类是同一个类
 * (4)使用transient（瞬间的）修饰属性，这个属性不能序列化
 * (5)静态属性不能被序列化
 * (6)序列化多个对象,可以借助集合实现
 * @author wgy
 *
 */
public class Demo6 {
	public static void main(String[] args) throws Exception{
		//1创建对象流
		FileOutputStream fos=new FileOutputStream("d:\\stu.bin");
		ObjectOutputStream oos=new ObjectOutputStream(fos);
		//2序列化(写入操作)多个对象使用集合
		Student zhangsan=new Student("张三", 20);
		Student lisi=new Student("李四", 22);
		ArrayList<Student> list=new ArrayList<>();
		list.add(zhangsan);
		list.add(lisi);
		oos.writeObject(list);
	
		//3关闭
		oos.close();
		System.out.println("序列化完毕");
	}
}

```



## 2.反序列化（读）

```java
package com.qf.chapter15_1;

import java.io.FileInputStream;
import java.io.ObjectInputStream;
import java.util.ArrayList;

/**
 * 使用ObjectInputStream实现反序列化(读取重构成对象)
 * @author wgy
 *
 */
public class Demo7 {
	public static void main(String[] args) throws Exception {
		//1创建对象流
		FileInputStream fis=new FileInputStream("d:\\stu.bin");
		ObjectInputStream ois=new ObjectInputStream(fis);
		//2读取文件(反序列化)多个对象使用集合
//		Student s=(Student)ois.readObject();
//		Student s2=(Student)ois.readObject();
		ArrayList<Student> list=(ArrayList<Student>)ois.readObject();
		//3关闭
		ois.close();
		System.out.println("执行完毕");
//		System.out.println(s.toString());
//		System.out.println(s2.toString());
		System.out.println(list.toString());
	}
}

```

## 3.注意事项

1. 某个**类**要想序列化必须实现Serializable接口

2. 序列化类中**对象属性**要求实现Serializable接口

3. 序列化版本号ID，保证**序列化的类和反序列化的类**是同一个类

4. 使用`transient（瞬间的）`修饰属性，这个属性就不能序列化

5. `static`静态属性不能序列化

6. 序列化多个对象，可以借助**集合**来实现

   

# 六、编码方式

![image-20210112180232442](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210112180232442.png)

**UTF-8**... 不赘述

# 七、字符流

```java
// 传统字节流读取
package com.qf.chapter15_2;
public class Demo1 {
psvm(String[] args){
  // 1. 创建FileInputStream对象
  FileInputSteam fis = new FileInputStream("路径");
  // 2. 读取
  int data = 0;
  while((data = fis.read()) != -1){ //好好学习（12个字节4个汉字）所以出现了下面乱码问题
    sout((char)data); 
  }
  // 3. 关闭
  fis.close();
}
}
```

![image-20210112180910301](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210112180910301.png)

## 1.字符流的父类（抽象类）

抽象类，我们使用时要使用他们的实现类

`reader` 字符输入流

- `public int read(){}`
- `public int read(char[] c){}`
- `public int read(char[] b, int off, int len){}`

`Writer` 字符输出流

- `public void write(int n){}`
- `public void write(String str){}`
- `public void write(char[] c){}`

### FileReader

- 阅读字符文件的便利课。 该类的构造函数假定**默认字符编码**和**默认字节缓冲区**大小是适当的。

` public int read(char[] c)`

从流中读取多个字符，将读到内容存入c数组，返回实际读到的字符数;如果达到文件的尾部，则返回-1。

```java
package com.qf.chapter15_2;
public class Demo2 {
	public static void main(String[] args) throws Exception{
// 1. 创建FileReader 文件字符输入流
FileReader fr = new FileReader("..");
// 2. 读取
// 2.1 单个字符读取
int data = 0;
while((data = fr.read()) != -1){
  sout((char)data);// 读取一个字符
}
// 2.2 字符缓冲区读取
char[] buf = new char[2];// 字符缓冲区2个字符2个字符读取
int count = 0;
while((count = fr.read(buf) != -1)){
  sout(new String(buf, 0, count));
}
// 3. 关闭
fr.close();
  }
}
```



### FileWriter:

 `public void write(String str)`

一次写多个字符，将b数组中所有字符，写入输出流。

```java
package com.qf.chapter15_2;
public class Demo3 {
	public static void main(String[] args) throws Exception{
// 1. 创建FileWriter对象
FileWriter fw = new FileWriter("..");
// 2. 写入
for(int i = 0; i < 10; i ++){
  fw.write("写入的内容.....、\r\n");
  fw.flush();
}
// 3. 关闭
fw.close();
sout("执行完毕");
  }
}
```

## 2.（案例)使用上述内容进行文本文件复制

使用`FileReader`和`FileWriter`复制文本文件,不能复制图片或二进制文件(因为他是有默认编码和缓冲区的，所以复制不成功)

使用`字节流`可以复制任意文件

```java
package com.qf.chapter15_2;

import java.io.FileReader;
import java.io.FileWriter;

/**
 * 使用FileReader和FileWriter复制文本文件,不能复制图片或二进制文件
 * 使用字节流复制任意文件。
 * @author wgy
 *
 */
public class Demo4 {
	public static void main(String[] args) throws Exception{
		//1创建FIleReader FileWriter
		FileReader fr=new FileReader("...");
		FileWriter fw=new FileWriter("...");
		//2读写
		int data=0;
		while((data=fr.read())!=-1) {
			fw.write(data);
			fw.flush();
		}
		//3关闭
		fr.close();
		fw.close();
		System.out.println("复制完毕");
		
	}
}

```

## 3.字符缓冲流

```java
BufferedReader / BufferedWriter
```

高效读写、支持输入换行符、可一次写一行读一行

### BufferedReader

- 从字符输入流读取文本，缓冲字符，以提供字符，数组和行的高效读取。

  可以指定缓冲区大小，或者可以使用默认大小。 默认值足够大，可用于大多数用途。 

  通常，由读取器做出的每个读取请求将引起对底层字符或字节流的相应读取请求。

```java
package com.qf.chapter15_2;

import java.io.BufferedReader;
import java.io.FileReader;

import com.sun.org.apache.bcel.internal.generic.NEW;

/**
 * 使用字符缓冲流读取文件
 * BufferedReader
 * @author wgy
 *
 */
public class Demo5 {
	public static void main(String[] args) throws Exception{
		//1创建缓冲流
		FileReader fr=new FileReader("...");
		BufferedReader br=new BufferedReader(fr);
		//2读取
		//2.1第一种方式
//		char[] buf=new char[1024];
//		int count=0;
//		while((count=br.read(buf))!=-1) {
//			System.out.print(new String(buf,0,count));
//		}
		//2.2第二种方式，一行一行的读取
		String line=null;
		while((line=br.readLine())!=null) {
			System.out.println(line);
		}
		
		//3关闭
		br.close();
	}
}

```



### BufferedWriter

- 将文本写入字符输出流，缓冲字符，以提供单个字符，数组和字符串的高效写入。

  可以指定缓冲区大小，或者可以接受默认大小。 默认值足够大，可用于大多数用途。

```java
package com.qf.chapter15_2;

import java.io.BufferedWriter;
import java.io.FileWriter;

/**
 * 演示BufferedWriter的使用
 * @author wgy
 *
 */
public class Demo6 {
	public static void main(String[] args) throws Exception{
		//1创建BufferedWriter对象
		FileWriter fw=new FileWriter("...");
		BufferedWriter bw=new BufferedWriter(fw);
		//2写入
		for(int i=0;i<10;i++) {
			bw.write("好好学习，天天向上");
			bw.newLine();//写入一个换行符 windows \r\n  linux  \n   
			bw.flush();
		}
		//3关闭
		bw.close();
		System.out.println("执行完毕");

	}
}

```

## 4.PrintWriter

封装了`print() / println()` 方法 支持写入后换行

支持数据原样打印

```java
package com.qf.chapter15_2;

import java.io.PrintWriter;

/**
 * 演示PrintWriter的使用
 * 
 */
public class Demo7 {
	public static void main(String[] args) throws Exception {
		//1创建打印流
		PrintWriter pw=new PrintWriter("d:\\print.txt");
		//2打印
		pw.println(97);     //----》97  而不是A
		pw.println(true);
		pw.println(3.14);
		pw.println('a');
		//3关闭
		pw.close();
		System.out.println("执行完毕");
	}
}

```

## 5.转换流

桥转换流 `InputStreamReader / OutputStreamWriter`

从硬盘中0/1字节流转换为内存中字符流（可以设置编码方式）

从内存中字符流转换为硬盘中0/1字节流

可将字节流转换为字符流

可设置字符的编码方式

### InputStreamReader

- InputStreamReader是从字节流到字符流的桥：它读取字节，并使用指定的`charset`将其解码为[字符](../../java/nio/charset/Charset.html)  。它使用的字符集可以由名称指定，也可以被明确指定，或者可以接受平台的默认字符集。

  每个调用InputStreamReader的read（）方法之一可能会导致从底层字节输入流读取一个或多个字节。  为了使字节有效地转换为字符，可以从底层流读取比满足当前读取操作所需的更多字节。 

```java
package com.qf.chapter15_3;

import java.io.FileInputStream;
import java.io.InputStreamReader;

/**
 * 使用InputStreamReader读取文件，指定使用的编码
 * @author wgy
 *
 */
public class Demo1 {
	public static void main(String[] args) throws Exception {
		//1创建InputStreamReader对象
		FileInputStream fis=new FileInputStream("...");
		InputStreamReader isr=new InputStreamReader(fis, "utf-8");//读取时编码一致才能正确的读出
		//2读取文件
		int data=0;
		while((data=isr.read())!=-1) {
			System.out.print((char)data);
		}
		//3关闭
		isr.close();
	}
}

```

### OutputStreamWriter

- 字符的桥梁流以字节流：向其写入的字符编码成使用指定的字节[`charset`](../../java/nio/charset/Charset.html) 。  它使用的字符集可以由名称指定，也可以被明确指定，或者可以接受平台的默认字符集。 

```java
package com.qf.chapter15_3;

import java.io.FileOutputStream;
import java.io.OutputStreamWriter;

/**
 * 使用OutputStreamWriter写入文件，使用指定的编码
 * @author wgy
 *
 */
public class Demo2 {
	public static void main(String[] args) throws Exception{
		//1创建OutputStreamWriter
		FileOutputStream fos=new FileOutputStream("...");
		OutputStreamWriter osw=new OutputStreamWriter(fos, "utf-8");
		//2写入
		for(int i=0;i<10;i++) {
			osw.write("我爱北京，我爱故乡\r\n");
			osw.flush();
		}
		//3关闭
		osw.close();
		System.out.println("执行成功");
	}
}

```

# 八、File类

概念：代表物理盘符中的一个**文件**或者**文件夹（目录）**

方法：

```java
//相关方法 
createNewFile()//创建一个新文件
mkdir()//创建一个新目录
delete()//删除文件或空目录
exists()//判断File对象所对象所代表的对象是否存在getAbsolutePath()//获取文件的绝对路径
getName()//取得名字
getParent ()//获取文件/目录所在的目录
isDirectory()//是否是目录
isFile()//是否是文件
length()//获得文件的长度
listFiles()//列出目录中的所有内容renameTo()//修改文件名为
```



```java
package com.qf.chapter15_4;

import java.io.File;
import java.io.FileFilter;
import java.sql.Date;
import java.util.Properties;

/**
 * File类的使用
 * （1）分隔符
 * （2）文件操作
 * （3）文件夹操作
 * @author wgy
 *
 */
public class Demo1 {
	public static void main(String[] args) throws Exception {
		//separator();
		//fileOpe();
		directoryOpe();
	}
	//（1）分隔符
	public static void separator() {
		System.out.println("路径分隔符"+File.pathSeparator);//;
		System.out.println("名称分隔符"+File.separator);//\
	}
	//（2）文件操作
	public static void fileOpe() throws Exception {
		//1创建文件 createNewFile()
		File file=new File("D:\\Programming File\\TestJavaSE\\file.txt");
		//System.out.println(file.toString());//文件路径名
		if(!file.exists()) {		//判断文件是否存在
			boolean b=file.createNewFile();
			System.out.println("创建结果:"+b);	//创建文件
		}
		//2删除文件
		//2.1直接删除
		//System.out.println("删除结果:"+file.delete());
		//2.2使用jvm退出时删除
//		file.deleteOnExit();
//		Thread.sleep(5000);
		
		//3获取文件信息
		System.out.println("获取文件的绝对路径:"+file.getAbsolutePath());
		System.out.println("获取路径:"+file.getPath());
		System.out.println("获取文件名称:"+file.getName());
		System.out.println("获取父目录:"+file.getParent());//D:\\
		System.out.println("获取文件长度:"+file.length());
		System.out.println("文件创建时间:"+new Date(file.lastModified()).toLocaleString());
		
		
		//4判断
		System.out.println("是否可写:"+file.canWrite());
		System.out.println("是否时文件:"+file.isFile());
		System.out.println("是否隐藏:"+file.isHidden());
		
	}
	
	//（3）文件夹操作
	public static void directoryOpe() throws Exception{
		//1 创建文件夹
		File dir=new File("D:\\Programming File\\TestJavaSE\\aaa\\bbb\\ccc");
		System.out.println(dir.toString());
		if(!dir.exists()) {		//判断文件夹是否能存在
						//dir.mkdir();//只能创建单级目录
			System.out.println("创建结果:"+dir.mkdirs());//创建多级目录
		}
		
		//2 删除文件夹
		//2.1直接删除(注意删除空目录，只删除最底层的空目录)
		//System.out.println("删除结果:"+dir.delete());
		//2.2使用jvm删除
//		dir.deleteOnExit();
//		Thread.sleep(5000);
    
		//3获取文件夹信息
		System.out.println("获取绝对路径："+dir.getAbsolutePath());
		System.out.println("获取路径:"+dir.getPath());
		System.out.println("获取文件夹名称："+dir.getName());
		System.out.println("获取父目录："+dir.getParent());
		System.out.println("获取创建时间:"+new Date(dir.lastModified()).toLocaleString());
		
		
		//4判断
		System.out.println("是否时文件夹:"+dir.isDirectory());
		System.out.println("是否时隐藏："+dir.isHidden());
		
		//5遍历文件夹
		File dir2=new File("D:\\Programming File\\TestJavaSE\\图片");
		String[] files=dir2.list();
		System.out.println("--------------------------------");
		for (String string : files) {
			System.out.println(string);
		}			//文件夹中文件的目录
		System.out.println("-----------FileFilter接口的使用-----------");
		//public interface FileFilter
    	//olean acqept(File pathname)
			//	用File类中的listFiles()方法时，支持传入FileFilter接口接口实现类，对获取文件进行过滤，只有满足条件true才可出现在listFiles()的返回值中。
    
		File[] files2=dir2.listFiles(new FileFilter() {
			@Override
			public boolean accept(File pathname) {
				if(pathname.getName().endsWith(".jpg")) {
					return true;   //以.jpg结尾的文件才可以输出
				}
				return false;
			}
		});
    
		for (File file : files2) {
			System.out.println(file.getName());
		}
	}
	
}

```

![image-20210112190958675](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210112190958675.png)

## 1.递归遍历文件夹

![image-20210112193121378](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210112193121378.png)

![image-20210112193134152](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210112193134152.png)

![image-20210112193143296](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210112193143296.png)

将myfiles文件夹中的内容全部显示出来：

```java
package com.qf.chapter15_4;

import java.io.File;

/**
 * 案例1：递归遍历文件夹
 * @author wgy
 *
 */
public class ListDemo {
	public static void main(String[] args) {
		listDir(new File("D:\Programming File\TestJavaSE\\myfiles"));
	}
	//案例1：递归遍历文件夹
	public static void listDir(File dir) {
		File[] files=dir.listFiles();
		System.out.println(dir.getAbsolutePath());
		if(files!=null&&files.length>0) {
			for (File file : files) {
				if(file.isDirectory()) {		//如果是个文件夹则进入
					listDir(file);			//递归
				}else {
					System.out.println(file.getAbsolutePath());
				}
			}
		}
	}
	
}

```

![image-20210112193355976](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210112193355976.png)

## 2.递归删除文件夹

```java
package com.qf.chapter15_4;

import java.io.File;

/**
 * 案例2：递归删除文件夹
 * @author wgy
 *
 */
public class ListDemo {
	public static void main(String[] args) {
		deleteDir(new File("D:\\Programming File\\TestJavaSE\\myfiles"));
	}

	//案例2：递归删除文件夹
	public static void deleteDir(File dir) {
		File[] files=dir.listFiles();
		if(files!=null&&files.length>0) {
			for (File file : files) {
				if(file.isDirectory()) {
					deleteDir(file);//递归
				}else {
					//删除文件
					System.out.println(file.getAbsolutePath()+"删除:"+file.delete());
				}
			}
		}
    //删除文件夹
		System.out.println(dir.getAbsolutePath()+"删除:"+dir.delete());
	}
	
}

```

# 九、Properties

```java
package com.qf.chapter15_4;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.PrintWriter;
import java.util.Properties;
import java.util.Set;

/**
 * 演示Properties集合的使用
 * @author wgy
 *
 */
public class Demo2 {
	public static void main(String[] args) throws Exception {
		//1创建集合
		Properties properties=new Properties();
		//2添加数据
		properties.setProperty("username", "zhangsan");
		properties.setProperty("age", "20");
		System.out.println(properties.toString());
		//3遍历
		//3.1-----keySet----
		//3.2-----entrySet----
		//3.3-----stringPropertyNames()---
		Set<String> pronames=properties.stringPropertyNames();
		for (String pro : pronames) {
			System.out.println(pro+"====="+properties.getProperty(pro));
		}
		//4和流有关的方法
		//----------list方法---------
//		PrintWriter pw=new PrintWriter("D:\\Programming File\\TestJavaSE\\print.txt");
//		properties.list(pw);
//		pw.close();
		
		//----------2store方法 保存-----------
//		FileOutputStream fos=new FileOutputStream("D:\\Programming File\\TestJavaSE\\store.properties");
//		properties.store(fos, "注释");
//		fos.close();
		
		//----------3load方法 加载-------------
		Properties properties2=new Properties();
		FileInputStream fis=new FileInputStream("D:\\Programming File\\TestJavaSE\\store.properties");
		properties2.load(fis);
		fis.close();
		System.out.println(properties2.toString());
		
	}
}

```

# 总结

![image-20210112194926060](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210112194926060.png)

