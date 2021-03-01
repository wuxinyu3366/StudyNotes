# 网络编程

# 一、什么是网络

由点和线构成，表示诸多对象之间的相互联系。

![image-20210114182652378](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114182652378.png)

![image-20210114182635382](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114182635382.png)

# 二、计算机网络

为实现**资源共享**和**信息传递**，通过通信线路连接起来的若干**主机（Host）** 。

![image-20210114182746208](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114182746208.png)

按照地理范围网络分为:
	1.局域网

​	2.城域网

​	3.广域网
​		（1）互联网:( Internet）点与点相连

​		（2）万维网:(WWW - World Wide Web）端与端相连

​		（3）物联网:( IoT - Internet of things）物与物相连

**网络编程**: 让**计算机**与**计算机**之间建立连接、进行通信。

# 三、网络模型

## 网络模型—OSI模型

OSI (Open System Interconnection）开放式系统互联。

![image-20210114183030004](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114183030004.png)

第七层:**应用层**负责文件访问和管理、可靠运输服务、远程操作服务。(**HTTP**、**FTP**、SMTP)

第六层:**表示层**负责定义转换数据格式及加密，允许选择以二进制或**ASCII格式传输**。

第五层:**会话层**负责使应用建立和维持会话，使通信在失效时继续恢复通信。(断点续传)

第四层:**传输层**负责是否选择差错恢复协议、数据流重用、错误顺序重排。（**TCP**、UDP)

第三层:**网络层**负责定义了能够标识所有网络节点的逻辑地址。(**IP**地址)
第二层:**链路层**在物理层上，通过规程或协议（差错控制）来控制传输数据的正确性。(MAC)

第一层:**物理层**为设备之间的数据通信提供传输信号和物理介质。（双绞线、光导纤维)

![image-20210114183348987](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114183348987.png)

## 网络模型—TCP/IP模型

一组用于实现网络互连的通信协议，将协议分成四今层次。

![image-20210114183518706](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114183518706.png)

第四层:**应用层**负责传送各种最终形态的数据，是直接与用户打交道的层，典型协议是HTTP、FTP等。
第三层:**传输层**负责传送文本数据，主要协议是TCP、UDP协议。
第二层:**网络层**负责分配地址和传送二进制数据，主要协议是IP协议。
第一层:**接口层**负责建立电路连接，是整个网络的物理基础，典型的协议包括以太网、ADSL等等。

# 四、通信协议

## TCP/UDP

### TCP协议

Transmission Control Protocol **传输控制协议**

是一种**面向连接的、可靠的**、基于**字节流**的传输层通信协议。数据大小无限制。建立连接的过程需要**三次握手**，断开连接的过程需要**四次挥手**。

三次握手：A是客户端，B是服务器

![image-20210114184226056](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114184226056.png)

四次挥手：A是客户端，B是服务器

![image-20210114185123549](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114185123549.png)

### UDP协议

User Datagram Protocol**用户数据报协**


是一种**无连接**的传输层协议，提供面向事务的简单**不可靠信息**传送服务，每个包的大小64KB。

广播的、效率高的



## IP协议

IInternet Protocol **互联网协议/网际协议**

负责**数据**从一台机器**发送**到另一台机器。

给互联网每台设备分配一个**唯一标识**（IP地址）。

IP地址分为两种:
**IPV4**: **4字节32位整数**，并分成4段8位的二进制数，每8位之间用圆点隔开，每8位整数可以转换为一个0~255的**十进制整数**。
		格式:D.D.D.D		例如:255.255.255.255
**IPV6**: **16字节128位整数**，并分成8段十六进制数，每16位之间用圆点隔开，每1位整数可以转换为一个**0~65535的十进制数**。
		格式:X.X.X.X.X.X.X.X例如:FFFF.FFFF.FFFF.FFFF.FFFF.FFFF.FFFF.FFFF

# 五、IP与端口

## IPV4分类

A类:政府机构，1.0.0.1 ~ 126.255.255.254

B类:中型企业，128.0.0.1 ~ 191.255.255.254

C类:个人用户，192.0.0.1 ~ 223.255.255.254

D类:用于组播，224.0.0.1 ~ 239.255.255.254

E类:用于实验，240.0.0.1 ~ 255.255.255.254

回环地址:127.0.0.1，指本机，一般用于测试使用。

测试IP命令: ping D.D.D.D

![image-20210114185917048](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114185917048.png)

查看IP命令: ipconfig

![image-20210114185933660](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114185933660.png)

## Port

端口号:在**通信实体**上进行网络通讯程序的唯一标识。

![image-20210114190328501](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114190328501.png)

端口分类:
	公认端口: 0---1023

​	注册端口: 1024~49151

​	动态或私有端口: 49152~65535

常用端口:
	MySql: 3306

​	Oracle:1521

​	Tomcat: 8080

​	SMTP:25

​	Web服务器:80

​	FTP服务器:21

# 六、网络编程

## InetAddress类

【1】概念:

表示**互联网协议（IP）**地址对象，封装了与该IP地址相关的所有信息,并提供获取信息的常用方

法。

【2】方法：java.net

`public static InetAddress getLocalHost() `	获得本地主机地址对象

`public static InetAddress getByName(String host)`	根据主机名称获得地址对象

`public static InetAddress[] getAllByName(String host)`	获得所有相关地址对象

`public String getHostAddress()`	获取IP地址字符串

`public String getHostName()`	获得IP地址主机名

```java
package com.qf.chapter16_1;

import java.net.InetAddress;

/**
 * 演示InetAddress类的使用
 * (1)创建本机IP地址对象
 * (2)创建局域网IP地址对象
 * (3)创建外网IP地址对象
 * @author wgy
 *
 */
public class Demo1 {
	public static void main(String[] args) throws Exception{
		//1创建本机IP地址对象
		//1.1getLocalhost()方法
		InetAddress ia1=InetAddress.getLocalHost();
		System.out.println("ip地址:"+ia1.getHostAddress()+" 主机名:"+ia1.getHostName());
		//1.2getByName("ip地址");
		InetAddress ia2=InetAddress.getByName("192.168.0.103");
		System.out.println("ip地址:"+ia2.getHostAddress()+" 主机名:"+ia2.getHostName());
		//1.3getByName("127.0.0.1");
		InetAddress ia3=InetAddress.getByName("127.0.0.1");
		System.out.println("ip地址:"+ia3.getHostAddress()+" 主机名:"+ia3.getHostName());
		//1.4getByName("localhost");
		InetAddress ia4=InetAddress.getByName("localhost");
		System.out.println("ip地址:"+ia4.getHostAddress()+" 主机名:"+ia4.getHostName());
		
		//2创建局域网IP地址对象
		
//		InetAddress ia5=InetAddress.getByName("192.168.0.104");
//		System.out.println("ip地址:"+ia5.getHostAddress()+" 主机名:"+ia5.getHostName());
//		System.out.println("2秒钟是否可达:"+ia5.isReachable(2000));
		
		//3创建外网IP地址对象
		InetAddress ia6=InetAddress.getByName("www.baidu.com");
		System.out.println("ip地址:"+ia6.getHostAddress()+" 主机名:"+ia6.getHostName());
		System.out.println("2秒钟是否可达:"+ia6.isReachable(2000));
		System.out.println("--------------");
		InetAddress[] ias=InetAddress.getAllByName("www.baidu.com");
		for (InetAddress inetAddress : ias) {
			System.out.println(inetAddress.getHostAddress());
		}
		
	}
}

```

![image-20210115110720172](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210115110720172.png)

## 基于TCP的网络编程

### Socket编程：

Socket（套接字）是网络中的一个**通信节点**。

分为客户端`Socket`与服务器`ServerSocket`

通信要求:IP地址＋端口号

![image-20210115110950645](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210115110950645.png)

### 开发步骤

服务器端:

- 创建ServerSocket，指定端口号
- 调用accept等待客户端接入
  使用输入流，接收请求数据到服务器（等待)
- 使用输出流，发送响应数据给客户端
- 释放资源

客户端:

- 创建Socket，指定服务器IP＋端口号
- 使用输出流，发送请求数据给服务器
- 使用输入流，接收响应数据到客户端（等待）
- 释放资源

### 案例

#### 一、TCP编程实现客户端发送数据给服务器端

```java
package com.qf.chapter16_1;

import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.ServerSocket;
import java.net.Socket;
import java.nio.channels.NonWritableChannelException;

/**
 * 基于TCP协议的服务器端开发
 * 1 创建ServerSocket 并指定端口号
 * 2 调用accept(),接收客户端请求
 * 3 获取输入流，读取客户端发送的数据
 * 4 获取输出流，发送数据给客户端
 * 5 关闭释放资源
 * @author wgy
 *
 */
public class TcpServer {
	public static void main(String[] args) throws Exception{
//		 * 1 创建ServerSocket 并指定端口号
		ServerSocket serverSocket = new ServerSocket(8899);
//		 * 2 调用accept(),接收客户端请求,阻塞方法(如果没有客户端请求，则阻塞)
		System.out.println("服务器已启动...");
		Socket socket = serverSocket.accept();
//		 * 3 获取输入流，读取客户端发送的数据
		InputStream is = socket.getInputStream();
		BufferedReader br = new BufferedReader(new InputStreamReader(is,"utf-8"));
		String data = br.readLine();
		System.out.println("客户发送:"+data);
//		 * 4 获取输出流，发送数据给客户端[可选]
//		 * 5 关闭释放资源
		br.close();
		socket.close();
		serverSocket.close();

	}
}

```



```java
package com.qf.chapter16_1;

import java.io.BufferedWriter;
import java.io.OutputStream;
import java.io.OutputStreamWriter;
import java.net.Socket;

/**
 * 基于TCP客户端开发
 * 1 创建客户端套接字，并指定服务器的地址和端口号
 * 2 获取输出流，发送数据给服务器
 * 3 获取输入流，读取服务器回复的数据
 * 4 关闭释放资源
 * @author wgy
 *
 */
public class TcpClient {
	public static void main(String[] args) throws Exception{
//		 * 1 创建客户端套接字，并指定服务器的地址和端口号
		Socket socket=new Socket("192.168.31.156", 8899);
//		 * 2 获取输出流，发送数据给服务器
		OutputStream os=socket.getOutputStream();
		BufferedWriter bw=new BufferedWriter(new OutputStreamWriter(os,"utf-8"));
		bw.write("好久不见");
//		 * 3 获取输入流，读取服务器回复的数据[可选]
//		 * 4 关闭释放资源
		bw.close();
		socket.close();
	}
}

```

![image-20210115112246495](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210115112246495.png)

![image-20210115112401862](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210115112401862.png)

#### 二、TCP编程实现客户端上传文件给服务器端

```java
package com.qf.chapter16_2;

import java.io.FileOutputStream;
import java.io.InputStream;
import java.net.ServerSocket;
import java.net.Socket;



/**
 * TCP服务器端
 * @author wgy
 *
 */
public class TcpFileServer {
	public static void main(String[] args) throws Exception {
		//1创建ServerSocket
		ServerSocket listener=new ServerSocket(9999);
		//2侦听,接收客户端请求
		System.out.println("服务器已启动.........");
		Socket socket=listener.accept();
		//3获取输入流
		InputStream is=socket.getInputStream();
		//4边读取，边保存
		FileOutputStream fos=new FileOutputStream("D:\\Programming File\\TestJavaSE\\002.jpg");
		byte[] buf=new byte[1024*4];
		int count=0;
		while((count=is.read(buf))!=-1) {
			fos.write(buf,0,count);
		}
		//5关闭
		fos.close();
		is.close();
		socket.close();
		listener.close();
		System.out.println("接收完毕");
		
		
	}
}

```



```java
package com.qf.chapter16_2;

import java.io.FileInputStream;
import java.io.OutputStream;
import java.net.Socket;

/**
 * Tcp客户端
 * @author wgy
 *
 */
public class TcpFileClient {
	public static void main(String[] args) throws Exception {
		//1创建Socket
		Socket socket=new Socket("192.168.31.156", 9999);
		//2获取输出流
		OutputStream os=socket.getOutputStream();
		//3边读取文件，边发送
		FileInputStream fis=new FileInputStream("D:\\Programming File\\TestJavaSE\\001.jpg");
		byte[] buf=new byte[1024*4];
		int count=0;
		while((count=fis.read(buf))!=-1) {
			os.write(buf,0,count);
		}
		//4关闭
		fis.close();
		os.close();
		socket.close();
		System.out.println("发送完毕");
	}
}

```



#### 三、TCP实现多个客户端发送数据给服务器端

![image-20210115113140990](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210115113140990.png)

```java
package com.qf.chapter16_3;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.Socket;

public class SocketThread extends Thread{

	private Socket socket;
	
	public SocketThread(Socket socket) {
		this.socket=socket;
	}

	@Override
	public void run() {
		if(socket!=null) {
			BufferedReader br=null;
			try {
				InputStream is = socket.getInputStream();
				br=new BufferedReader(new InputStreamReader(is,"utf-8"));
				while(true) {
					String data=br.readLine();
					if(data==null) {//客户端已经关闭
						break;
					}
					System.out.println(socket.getInetAddress()+":"+socket.getPort()+"说:"+data);
					if(data.equals("886")||data.equals("byebye")) {
						break;
					}
				}	
				
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}finally {
				try {
					br.close();
					socket.close();
					System.out.println(socket.getInetAddress()+"退出了...");
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
				
			}
			
			
			
		}
		
	}
}

```



服务器端通过线程来不断的接收客户端的信息

```java
package com.qf.chapter16_3;

import java.net.ServerSocket;
import java.net.Socket;

/**
 * 使用TCP实现接收多个客户端请求
 * @author wgy
 *
 */
public class TcpServer {
	public static void main(String[] args) throws Exception {
		//1创建ServerSocket
		ServerSocket listener=new ServerSocket(10086);
		//2调用accept(),接收客户端请求
		System.out.println("服务器已启动..........");
		while(true) {
			Socket socket=listener.accept();
			System.out.println(socket.getInetAddress()+"进来了.........");
			//创建线程对象，负责接收数据
			new SocketThread(socket).start();
		}
	}
}

```



```java
package com.qf.chapter16_3;

import java.io.BufferedWriter;
import java.io.OutputStream;
import java.io.OutputStreamWriter;
import java.net.Socket;
import java.util.Scanner;

/**
 * TCP客户端：一直向服务器发送数据
 * @author wgy
 *
 */
public class TcpClient {
	public static void main(String[] args) throws Exception {
		//1创建Socket
		Socket socket=new Socket("192.168.31.156", 10086);
		//2获取输出流
		OutputStream os=socket.getOutputStream();
		BufferedWriter bw=new BufferedWriter(new OutputStreamWriter(os,"utf-8"));
		//3控制输入
		Scanner input=new Scanner(System.in);
		while(true) {
			String data=input.nextLine();
			bw.write(data);
			bw.newLine();//发送换行符
			bw.flush();
			if(data.equals("886")||data.equals("byebye")) {
				break;
			}
		}
		//4关闭
		bw.close();
		socket.close();
	}
}

```

#### 四、使用Socket实现注册登录

使用Scoket编程实现服务器端注册

- 注册信息保存在properties文件
- 封装格式:
- id = {id : ”1001”, name : “tom”, pwd : ”123”, age : 20 }
- 注册成功后返回字符串“注册成功”。

```java
package com.qf.chapter16_4;

public class UserServer {
	public static void main(String[] args) {
		new RegistThread().start();
		new LoginThread().start();
	}
}

```

```java
package com.qf.chapter16_4;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.Properties;

/**
 * 实现注册功能
 * @author wgy
 *
 */
public class RegistThread extends Thread{
	@Override
	public void run() {
		
		try {
			//1创建Serversocket 
			ServerSocket listener=new ServerSocket(6666);
			//2调用accept方法
			System.out.println("注册服务器已启动......");
			Socket socket=listener.accept();
			//3获取输入输出流
			BufferedReader br=new BufferedReader(new InputStreamReader(socket.getInputStream(),"utf-8"));
			BufferedWriter bw=new BufferedWriter(new OutputStreamWriter(socket.getOutputStream(),"utf-8"));
			//4接收客户端发送的数据{id : 1001, name :tom, pwd :123, age : 20 }
			String json=br.readLine();
			//id : 1001, name :tom, pwd :123, age : 20
			String[] infos=json.substring(1, json.length()-1).split(",");
			String id=infos[0].split(":")[1];
			//5加载属性文件
			Properties properties=Tools.loadProperties();
			//6判断
			if(properties.containsKey(id)) {
				//有
				bw.write("此用户已存在...");
			}else {
				//保存属性文件
				Tools.saveProperties(json);
				bw.write("注册成功");
			}
			bw.newLine();
			bw.flush();
			bw.close();
			br.close();
			socket.close();
			listener.close();			
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
	}
}

```

```java
package com.qf.chapter16_4;
/**
 * 工具类
 * @author wgy
 *
 */

import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.util.Properties;

public class Tools {
	//1加载属性文件
	public static Properties loadProperties() {
		//1创建属性集合
		Properties properties=new Properties();
		//2判断文件是否存在
		File file=new File("users.properties");
		if(file.exists()) {
			FileInputStream fis=null;
			try {
				fis = new FileInputStream(file);
				properties.load(fis);
			} catch (Exception e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}finally {
				if(fis!=null) {
					try {
						fis.close();
					} catch (IOException e) {
						// TODO Auto-generated catch block
						e.printStackTrace();
					}
				}
			}
			
		}
		
		return properties;
	}
	
	//2保存属性文件
	
	public static void saveProperties(String json) {
		String[] infos=json.substring(1, json.length()-1).split(",");
		String id=infos[0].split(":")[1];
		//保存
		FileOutputStream fos=null;
		try {
			fos=new FileOutputStream("users.properties",true);
			Properties properties=new Properties();
			properties.setProperty(id, json);
			properties.store(fos, "");
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}finally {
			if(fos!=null) {
				try {
					fos.close();
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
		}
		
	}
}

```

```java
package com.qf.chapter16_4;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.net.Socket;
import java.util.Scanner;

/**
 * 用户注册登录客户端
 * 
 * @author wgy
 *
 */
public class UserClient {
	public static void main(String[] args) throws Exception {
		System.out.println("---------请选择 1 注册 2 登录-----------");
		Scanner input = new Scanner(System.in);
		int choice = input.nextInt();
		switch (choice) {
		case 1:
			regist();
			break;
		case 2:
			login();
		default:
			break;
		}
	}

	public static void regist() throws Exception {
		// 1创建Socket
		Socket socket = new Socket("192.168.31.156", 6666);
		// 2获取流
		BufferedReader br = new BufferedReader(new InputStreamReader(socket.getInputStream(), "utf-8"));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream(), "utf-8"));
		// 3获取用户信息
		String json = getRegistInfo();
		// 4发送
		bw.write(json);
		bw.newLine();
		bw.flush();
		// 5接收
		String reply = br.readLine();
		System.out.println("服务器回复:" + reply);
		// 6关闭
		bw.close();
		br.close();
		socket.close();
	}

	public static String getRegistInfo() {
		Scanner input = new Scanner(System.in);
		System.out.println("请输入用户编号");
		int id = input.nextInt();
		System.out.println("请输入姓名");
		String name = input.next();
		System.out.println("请输入密码");
		String pwd = input.next();
		System.out.println("请输入年龄");
		int age = input.nextInt();
		// {id : 1001, name :tom, pwd :123, age : 20 }
		String json = "{id:" + id + ",name:" + name + ",pwd:" + pwd + ",age:" + pwd + "}";
		return json;
	}

	public static void login() throws Exception {
		// 1创建Socket
		Socket socket = new Socket("192.168.31.156", 7777);
		// 2获取流
		BufferedReader br = new BufferedReader(new InputStreamReader(socket.getInputStream(), "utf-8"));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream(), "utf-8"));
		// 3获取用户信息
		String json = getLoginInfo();
		// 4发送
		bw.write(json);
		bw.newLine();
		bw.flush();
		// 5接收
		String reply = br.readLine();
		System.out.println("服务器回复:" + reply);
		// 6关闭
		bw.close();
		br.close();
		socket.close();
	}
	public static String getLoginInfo() {
		Scanner input = new Scanner(System.in);
		System.out.println("请输入用户编号");
		int id = input.nextInt();
		System.out.println("请输入密码");
		String pwd = input.next();
		// {id : 1001, name :tom, pwd :123, age : 20 }
		String json = "{id:" + id+",pwd:"+ pwd+"}";
		return json;
	}
}

```

![image-20210115155728353](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210115155728353.png)

使用Scoket编程实现服务器端登录

- 获取properties文件中的用户信息，进行用户id与密码的校验
- 校验成功后返回字符串“登录成功”。

```java
package com.qf.chapter16_4;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.Properties;

public class LoginThread extends Thread {
	@Override
	public void run() {
		try {
			//1创建Serversocket 
			ServerSocket listener=new ServerSocket(7777);
			//2调用accept方法
			System.out.println("登录服务器已启动......");
			Socket socket=listener.accept();
			//3获取输入输出流
			BufferedReader br=new BufferedReader(new InputStreamReader(socket.getInputStream(),"utf-8"));
			BufferedWriter bw=new BufferedWriter(new OutputStreamWriter(socket.getOutputStream(),"utf-8"));
			//4接收客户端发送的数据{id : 1001, pwd :123}
			String json=br.readLine();
			//id : 1001 pwd :123
			String[] infos=json.substring(1, json.length()-1).split(",");
			String id=infos[0].split(":")[1];
			//5加载属性文件
			Properties properties=Tools.loadProperties();
			//6判断是否存在
			if(properties.containsKey(id)) {
				//判断密码是否正确
				String pwd=infos[1].split(":")[1];
				String value=properties.getProperty(id);
				String[] arr=value.substring(1, value.length()-1).split(",");
				String pwd2=arr[2].split(":")[1];
				if(pwd.equals(pwd2)) {
					bw.write("登录成功");
				}else {
					bw.write("密码错误");
				}
				
			}else {
				//保存属性文件
				bw.write("用户名或密码错误");
			}
			bw.newLine();
			bw.flush();
			bw.close();
			br.close();
			socket.close();
			listener.close();			
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
}

```



![image-20210115155911794](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210115155911794.png)

![image-20210115155946958](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210115155946958.png)



# JDK新特性

# 一、java8概述

Java8 (又称JKD1.8)是Java语言开发的一个主要版本。 Oracle公司于2014 年3月18日发布Java 8 。（它决

定每半年发布一版jdk，现在已经到jdk14，但是好多公司仍在使用1.8老版本稳定）

- 支持Lambda表达式
- 函数式接口
- 新的Stream API
- 新的日期API
- 其他特性

# 二、Lambada表达式

Lambda表达式:	**特殊的匿名内部类**，语法更简洁。

Lambda表达式允许把**函数**作为一个**方法**的**参数**（函数作为**方法参数**传递），将代码像**数据**一样传递。

```java
<函数式接口><变量名>=(参数1,参数2...)->{
  //方法体
};
```

Lambda引入了新的操作符`->`(箭头操作符),`->`将表达式分成两部分

- 左侧：`(参数1,参数2...)`表示参数列表
- 右侧：`{  }`内部是方法体

注意事项：

- 形参列表的数据类型会**自动推断**。
- 如果形参列表为空,只需保留`()`
- 如果形参只有1个，`()`可以省略，只需要参数的名称即可
- 如果执行语句只有一句，且无返回值，`{}`可以省略，若有返回值，则若想省去`{}`则必须同时省略`return`，且执行语句也保证只有一句.
- Lambda不会生成一个单独的内部类文件,匿名内部类会生成。

```java
package com.qf.chapter18_1;

import javax.swing.plaf.ComponentInputMapUIResource;
import java.util.Comparator;
import java.util.TreeSet;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/15 - 01 - 15 - 16:28
 * @Description: com.qf.chapter18_1
 * Lambda表达式的使用
 * @version: 1.0
 */
public class Demo1 {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //匿名内部类
        Runnable runnable01 = new Runnable() {
            @Override
            public void run() {
                System.out.println("子线程执行了");
            }
        };
        Thread thread = new Thread(runnable01);
        thread.start();

        //Lambda表达式
        Runnable runnable02 = ()-> System.out.println("子线程执行了");
        new Thread(runnable02).start();

        //---------------------------------------------
        Comparator<String> comparator01 = new Comparator<String>() {
            @Override
            public int compare(String s, String t1) {
                return s.length()-t1.length();
            }
        };
        TreeSet<String> treeSet01 = new TreeSet<>(comparator01);

        Comparator<String> comparator02 =(String s, String t1)->{
            return s.length()-t1.length();
        };
        TreeSet<String> treeSet02 = new TreeSet<>(comparator02);

        Comparator<String> comparator03 =(String s, String t1)->s.length()-t1.length();
        TreeSet<String> treeSet03 = new TreeSet<>(comparator03);
    }
}

```



# 三、函数式接口

如果**一个接口只有一个抽象方法**，则该接口称之为**函数式接口**，函数式接口可以使用Lambda表达式，

Lambda表达式会被匹配到这个**抽象方法**上。用Lambda表达式的地方。

`@FunctionalInterface`注解检测接口是否符合函数式接口。

```java
package com.qf.chapter18_1;
/**
 * 函数式接口
 * @author wgy
 *
 */
//注解来测试是否为函数式接口
@FunctionalInterface
public interface Usb {
	void service();
}

```



```java
package com.qf.chapter18_1;

public class Demo2 {
	public static void main(String[] args) {
		//匿名内部类
		Usb mouse=new Usb() {
			@Override
			public void service() {
				System.out.println("鼠标开始工作了..........");
			}
		};
		
		Usb fan=()->System.out.println("风扇开始工作了..........");
		
		run(mouse);
		run(fan);
	}
	public static void run(Usb usb) {
		usb.service();
	}
}

```



## 常见的函数式接口

| 函数式接口              | 参数类型 | 返回类型 | 说明                                                         |
| ----------------------- | -------- | -------- | ------------------------------------------------------------ |
| Consumer<T>消费型接口   | T        | void     | void accept(T t);对类型为T的对象应用操作                     |
| Supplier<T>供给型接口   | 无       | T        | T get();返回类型为T的对象                                    |
| Function<T,R>函数型接口 | T        | R        | R apply(T t);对类型为T的对象应用操作，返回类型为T的对象      |
| Predicate<T> 断言型接口 | T        | boolean  | boolean test(T t);确定类型为T的对象是否满足条件，并返回boolean类型。 |

## Consumer<T>消费型接口

```java
package com.qf.chapter18_1;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Random;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;
import java.util.function.Supplier;

public class Demo3 {
	public static void main(String[] args) {
		//匿名内部类
		Consumer<Double> consumer=new Consumer<Double>() {

			@Override
			public void accept(Double t) {
				System.out.println("聚餐消费:"+t);
			}
		};
		//Lambda表达式
		Consumer<Double> consumer= t->System.out.println("聚餐消费:"+t);
		
		happy(t->System.out.println("聚餐消费:"+t), 1000);
		happy(t->System.out.println("唱歌消费:"+t), 2000);
		happy(t->System.out.println("足疗消费:"+t), 3000);
		
	}
	//Consumer 消费型接口
	public static void happy(Consumer<Double> consumer,double money) {
		consumer.accept(money);
	}
}
```

## Supplier<T>供给型接口

```java
package com.qf.chapter18_1;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Random;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;
import java.util.function.Supplier;



public class Demo3 {
	public static void main(String[] args) {
			int[] arr=getNums(()->new Random().nextInt(100), 5);
		System.out.println(Arrays.toString(arr));
		int[] arr2=getNums(()->new Random().nextInt(1000), 10);
		System.out.println(Arrays.toString(arr2));
	}
	
	//Supplier 供给型接口
	public static int[] getNums(Supplier<Integer> supplier,int count) {
		int[] arr=new int[count];
		for(int i=0;i<count;i++) {
			arr[i]=supplier.get();
		}
		return arr;
	}

}

```

## Function<T,R>函数型接口

```java
package com.qf.chapter18_1;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Random;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;
import java.util.function.Supplier;

public class Demo3 {
	public static void main(String[] args) {		
		String result=handlerString(s->s.toUpperCase(), "hello");
		System.out.println(result);
		String result2=handlerString(s->s.trim(), "   zhangsan        ");
		System.out.println(result2);
		
	}
	
	//Function函数型接口
	public static String handlerString(Function<String, String> function,String str) {
		return function.apply(str);
	}
	
}

```

## Predicate<T> 断言型接口

```java
package com.qf.chapter18_1;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Random;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;
import java.util.function.Supplier;



public class Demo3 {
	public static void main(String[] args) {
    
		List<String> list=new ArrayList<>();
		list.add("zhangsan");
		list.add("zhangwuji");
		list.add("lisi");
		list.add("wangwu");
		list.add("zhaoliu");
    
		List<String> result=filterNames(s->s.startsWith("zhang"), list);
		System.out.println(result.toString());
    
		List<String> result2=filterNames(s->s.length()>5, list);
		System.out.println(result2);
	}
  
	//Predicate 断言型接口
	public static List<String> filterNames(Predicate<String> predicate,List<String> list){
		List<String> resultList=new ArrayList<String>();
		for (String string : list) {
			if(predicate.test(string)) {
				resultList.add(string);
			}
		}
		return resultList;
	}
}

```



# 四、方法引用

方法引用是**Lambda表达式**的一种简写形式。如果**Lambda表达式方法体**中只是调用一个**特定的已经存在**

**的方法**，则可以使用方法引用。



常见形式

```java
对象::实例方法
类::静态方法
类::实例方法
类::new
```



```java
package com.qf.chapter18_1;

import java.util.Comparator;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Supplier;

/**
 * 方法引用的使用
 * 1 对象::实例方法
 * 2 类::静态方法
 * 3 类::实例方法
 * 4 类::new
 * @author wgy
 *
 */
public class Demo4 {
	public static void main(String[] args) {
		//1 对象::实例方法
    //分析：Consumer的accept方法没有返回值，println也没有返回值，所以可以使用方法引用
		Consumer<String> consumer=s->System.out.println(s);
		consumer.accept("hello");
		Consumer<String> consumer2=System.out::println;
		consumer.accept("world");
		
		//2类::静态方法
    //分析：Comparator中的方法compare()是一个返回值两个参数，Integer中的compare()也是一个返回值两个参数，还是一个静态方法，所以可以使用方法引用
		Comparator<Integer> com=(o1,o2)->Integer.compare(o1, o2);
		Comparator<Integer> com2=Integer::compare;
			
		//3类::实例方法
    //分析：Function调用类Employee，并且返回String，getName()调用的是参数e，返回值也为String，所以可以使用方法调用
		Function<Employee, String> function=e->e.getName();
		Function<Employee, String> function2=Employee::getName;
		
		System.out.println(function2.apply(new Employee("小明", 50000)));
		
		//4类::new
    //分析：Employee()就使用构造方法，所以可以方法引用
		Supplier<Employee> supplier=()->new Employee();
		Supplier<Employee> supplier2=Employee::new;
		
		Employee employee=supplier.get();
		System.out.println(employee.toString());
		
	}
}

```

```java
package com.qf.chapter18_1;

public class Employee {
	private String name;
	private double money;
	public Employee() {
		// TODO Auto-generated constructor stub
	}
	
	public Employee(String name, double money) {
		super();
		this.name = name;
		this.money = money;
	}

	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public double getMoney() {
		return money;
	}
	public void setMoney(double money) {
		this.money = money;
	}
	@Override
	public String toString() {
		return "Employee [name=" + name + ", money=" + money + "]";
	}

	@Override
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		long temp;
		temp = Double.doubleToLongBits(money);
		result = prime * result + (int) (temp ^ (temp >>> 32));
		result = prime * result + ((name == null) ? 0 : name.hashCode());
		return result;
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		Employee other = (Employee) obj;
		if (Double.doubleToLongBits(money) != Double.doubleToLongBits(other.money))
			return false;
		if (name == null) {
			if (other.name != null)
				return false;
		} else if (!name.equals(other.name))
			return false;
		return true;
	}
	
	
	
}

```



# 五、Stream API

流 (Stream）中保存对集合或数组数据的**操作**。和集合类似，但集合中保存的是**数据**。用到了**方法引用**

![image-20210115174502556](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210115174502556.png)

Stream特点：

- Stream自己**不会存储**元素。
- Stream**不会改变**源对象。相反，他们会**返回**一个持有结果的**新Stream**
- Stream操作是**延迟执行**的。这意味着他们会等到**需要结果的时候才执行**。

Stream使用步骤：

- 创建
  - 新建一个流
- 中间操作
  - 在一个或多个步骤中，将初始Stream转化到另一个Stream的中间操作
- 终止操作
  - 使用一个终止操作来产生一个结果。该操作会强制它之前的延迟操作（中间操作）立即执行。在这之后，该Stream就不能使用了。

## 创建Stream

通过`Collection`对象的`stream()`(串行流)或`parallelStream()`(并行流)

通过`Arrays类`的`stream()`方法

通过`Stream接口`的`of()`、`iterate()`、`generate()`方法

通过`IntStream`、`IongStream`、`DoubleStream`接口中的`of、range、rangeClosed`方法



```java
package com.qf.chapter18_1;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Random;
import java.util.stream.IntStream;
import java.util.stream.Stream;

/**
 * Stream的使用
 * (1)创建流
 * @author wgy
 *
 */
public class Demo5 {
	public static void main(String[] args) {
    
		//(1)Collection对象中的stream()和parallelStream()方法
		ArrayList<String> arrayList=new ArrayList<>();
		arrayList.add("apple");
		arrayList.add("huawei");
		arrayList.add("xiaomi");
		Stream<String> stream = arrayList.parallelStream();
		//遍历
    //void forEach(Consumer<? super T> var1); 		函数需要的是一个方法引用对象
//		stream.forEach(s->System.out.println(s));
		stream.forEach(System.out::println);
    
		//(2)Arrays工具类的stream方法
		String[] arr= {"aaa","bbb","ccc"};
		Stream<String> stream2=Arrays.stream(arr);
		stream2.forEach(System.out::println);
		
		//(3)Stream接口中的of iterate 、generate 方法
		Stream<Integer> stream3 = Stream.of(10,20,30,40,50);
		stream3.forEach(System.out::println);
		//迭代流
		System.out.println("-----迭代流------");
		Stream<Integer> iterate = Stream.iterate(0, x->x+2); //从0开始，每次定增2
		iterate.limit(5).forEach(System.out::println); 		//迭代流进行限制，使只有5个数据
		System.out.println("--------生成流----------");
		//生成流
		Stream<Integer> generate = Stream.generate(()->new Random().nextInt(100));
		generate.limit(10).forEach(System.out::println);	//迭代流进行限制，使只有5个数据
		
		//(4)IntStream,LongStream,DoubleStream  的of  、range、rangeClosed
		IntStream stream4 = IntStream.of(100,200,300);
		stream4.forEach(System.out::println);
   // IntStream range = IntStream.range(0, 50); //不闭合
		IntStream range = IntStream.rangeClosed(0, 50);//闭合的
		range.forEach(System.out::println);
	}
}
```

## 中间操作

中间操作：

- `filter`、`limit`、`skip`、`distinct`、`sorted`
- `map`
- `parallel`

```java
package com.qf.chapter18_1;

import java.util.ArrayList;

/**
 * Stream的使用
 * (1)中间操作
 * @author wgy
 *
 */
public class Demo6 {
	public static void main(String[] args) {
		ArrayList<Employee> list=new ArrayList<>();
		list.add(new Employee("小王", 15000));
		list.add(new Employee("小张", 12000));
		list.add(new Employee("小李", 18000));
		list.add(new Employee("小孙", 20000));
		list.add(new Employee("小刘", 25000));
		//list.add(new Employee("小刘", 25000));
		//中间操作1 filter过滤   2 limit 限制  3 skip 跳过  4 distinct 去掉重复  5 sorted排序
		//filter过滤
		System.out.println("------filter-------");
		list.stream()
			.filter(e->e.getMoney()>15000)
			.forEach(System.out::println);
		//limit限制
		System.out.println("----limit------");
		list.stream()
			.limit(2)
			.forEach(System.out::println);
		//skip跳过
		System.out.println("-----skip------");
		list.stream()
			.skip(2)
			.forEach(System.out::println);
		System.out.println("------distinct--------");
		//distinct去重复  需要重写compara方法
		list.stream()
			.distinct()
			.forEach(System.out::println);
		
		System.out.println("---------sorted---------");
		//sorted排序
		list.stream()
			.sorted((e1,e2)->Double.compare(e1.getMoney(), e2.getMoney()))
			.forEach(System.out::println);
				
		//中间操作2 map  获取员工的所有姓名
		System.out.println("---------map--------");
		list.stream()
			.map(e->e.getName())
			.forEach(System.out::println);
    
		//中间操作3 parallel 采用多线程 效率高
		System.out.println("---------map--------");
		list.parallelStream()
			.forEach(System.out::println);
			
		
	}
}

```

## 并行流和串行流的区别

```java
package com.qf.chapter18_1;

import java.util.ArrayList;
import java.util.UUID;

public class Demo7 {
	public static void main(String[] args) {
		//串行流和并行流的区别
    //向列表中添加5000000个数据
		ArrayList<String> list=new ArrayList<>();
		for(int i=0;i<5000000;i++) {
			list.add(UUID.randomUUID().toString());
		}
		//串行 10秒  并行 7秒
		long start=System.currentTimeMillis();
		long count=list.parallelStream().sorted().count();
		System.out.println(count);
		long end=System.currentTimeMillis();
		System.out.println("用时:"+(end-start));
		
	}
}

```

## 终止操作

`forEach`、`min`、`max`、`count`

`reduce`、`collect`

```java
package com.qf.chapter18_1;

import java.util.ArrayList;
import java.util.List;
import java.util.Optional;
import java.util.stream.Collectors;

/**
 * Stream的使用 终止操作
 * 
 * @author wgy
 *
 */
public class Demo8 {
	public static void main(String[] args) {
		ArrayList<Employee> list = new ArrayList<>();
		list.add(new Employee("小王", 15000));
		list.add(new Employee("小张", 12000));
		list.add(new Employee("小李", 18000));
		list.add(new Employee("小孙", 20000));
		list.add(new Employee("小刘", 25000));
    
		//终止操作 foreach
    //证明了中间操作不立即执行，等到执行终止操作的时候才执行
		list.stream()
			.filter(e->{
					System.out.println("过滤了....");
					return e.getMoney()>15000;
				})
			.forEach(System.out::println);
    
		//终止操作 min max count
		System.out.println("-----min-----");
    //Optional可选对象，防止返回的是一个null
		Optional<Employee> min = list.stream()
			.min((e1,e2)->Double.compare(e1.getMoney(), e2.getMoney()));
		System.out.println(min.get());
    
		System.out.println("-----max-----");
		Optional<Employee> max = list.stream()
			.max((e1,e2)->Double.compare(e1.getMoney(), e2.getMoney()));
		System.out.println(max.get());
		
		long count = list.stream().count();
		System.out.println("员工个数:"+count);
		
		//终止操作 reduce 规约
		//计算所有员工的工资和
		System.out.println("--------reduce---------");
		Optional<Double> sum = list.stream()
			.map(e->e.getMoney())
			.reduce((x,y)->x+y);
		System.out.println(sum.get());
		
		//终止方法 collect收集
		//获取所有的员工姓名，封装成一个list集合
		System.out.println("------collect------");
		List<String> names = list.stream()
			.map(e->e.getName())
			.collect(Collectors.toList());
		for (String string : names) {
			System.out.println(string);
		}
	}
}

```



# 六、新时间API

线程安全问题：`SimpleDateFormat`有线程安全的问题，设计混乱

新的时间API`DateTimeFormatter`没有线程安全问题

## 线程安全

```java
package com.qf.chapter18_2;

import java.text.SimpleDateFormat;
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.util.ArrayList;
import java.util.Date;
import java.util.List;
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

/**
 * 线程安全问题
 * @author wgy
 *
 */
public class Demo1 {
	public static void main(String[] args) throws Exception{
		//SimpleDateFormat sdf=new SimpleDateFormat("yyyyMMdd");
    //新的时间API
		DateTimeFormatter dtf=DateTimeFormatter.ofPattern("yyyyMMdd");
    
    //1.
		ExecutorService pool = Executors.newFixedThreadPool(10);
    //2.
		Callable<LocalDate> callable=new Callable<LocalDate>() {
			@Override
			public LocalDate call() throws Exception {
        //sdf是线程不安全的，解决方法：一、静态synchronized静态代码块
				return LocalDate.parse("20200525",dtf);
			}
		};
    
    //3.提交事务
		List<Future<LocalDate>> list=new ArrayList<>();
		for(int i=0;i<10;i++) {
			Future<LocalDate> future=pool.submit(callable);
			list.add(future);
		}
		
		for (Future<LocalDate> future : list) {
			System.out.println(future.get());
		}
    //4.关闭线程池
		pool.shutdown();
		
	}
}

```



## 本地化日期时间API

- LocalDate
- LocalTime
- LocalDateTime

```java
package com.qf.chapter18_2;

import java.time.LocalDateTime;

/**
 * LocalDateTime的使用
 * @author wgy
 *
 */
public class Demo2 {
	public static void main(String[] args) {
		//1创建本地时间
		LocalDateTime localDateTime=LocalDateTime.now();
		//LocalDateTime localDateTime2=LocalDateTime.of(year, month, dayOfMonth, hour, minute)
		System.out.println(localDateTime);
		System.out.println(localDateTime.getYear());
		System.out.println(localDateTime.getMonthValue());
		System.out.println(localDateTime.getDayOfMonth());
		
		//2添加两天
		LocalDateTime localDateTime2 = localDateTime.plusDays(2);
		System.out.println(localDateTime2);
		
		//3减少一个月
		LocalDateTime localDateTime3 = localDateTime.minusMonths(1);
		System.out.println(localDateTime3);
	}
}

```

## Instant:时间戳及ZoneId:时区

从1970.1.1 00：00：00开始计时

```java
package com.qf.chapter18_2;

import java.time.Duration;
import java.time.Instant;
import java.time.LocalDateTime;
import java.time.ZoneId;
import java.time.ZoneOffset;
import java.util.Date;
import java.util.Set;

/**
 * Instant；时间戳
 * ZoneId:时区
 * @author wgy
 *
 */
public class Demo3 {
	public static void main(String[] args) {
		//1创建Instant：时间戳
		Instant instant=Instant.now();
		System.out.println(instant.toString());
		System.out.println(instant.toEpochMilli());
		System.out.println(System.currentTimeMillis());
		
    //2添加减少时间
		Instant instant2 = instant.plusSeconds(10);
		//打印两个时间的时间差   Duration
		System.out.println(Duration.between(instant, instant2).toMillis());
		
		//3 ZoneId 时区  打印所有时区
		Set<String> availableZoneIds = ZoneId.getAvailableZoneIds();
		for (String string : availableZoneIds) {
			System.out.println(string);
		}
		
		System.out.println(ZoneId.systemDefault().toString());
		
		//1 Date --->Instant---->LocalDateTime
		System.out.println("-------------Date --->Instant---->LocalDateTime-----------");
		Date date=new Date();
		Instant instant3 = date.toInstant();
		System.out.println(instant3);
		
		LocalDateTime localDateTime = LocalDateTime.ofInstant(instant3, ZoneId.systemDefault());
		System.out.println(localDateTime);
		
		//1 LocalDateTime --->Instant---->Date
		System.out.println("-------------LocalDateTime --->Instant---->Date-----------");
	
		Instant instant4 = localDateTime.atZone(ZoneId.systemDefault()).toInstant();
		System.out.println(instant4);
		Date from = Date.from(instant4);
		System.out.println(from);
		
	}
}

```

## Date、Instant、LocalDateTime的转换

```java
package com.qf.chapter18_2;

import java.time.Duration;
import java.time.Instant;
import java.time.LocalDateTime;
import java.time.ZoneId;
import java.time.ZoneOffset;
import java.util.Date;
import java.util.Set;

/**
 * Date、Instant、LocalDateTime的转换
 * @author wgy
 *
 */
public class Demo3 {
	public static void main(String[] args) {
		//1 Date --->Instant---->LocalDateTime
		System.out.println("-------------Date -(toInstant)-->Instant--(ofInstant)-->LocalDateTime-----------");
		Date date=new Date();
		Instant instant3 = date.toInstant();
		System.out.println(instant3);
		
		LocalDateTime localDateTime = LocalDateTime.ofInstant(instant3, ZoneId.systemDefault());
		System.out.println(localDateTime);
		
		//1 LocalDateTime --->Instant---->Date
		System.out.println("-------------LocalDateTime -(atZone.toInstant)-->Instant--(from)-->Date-----------");
	
		Instant instant4 = localDateTime.atZone(ZoneId.systemDefault()).toInstant();
		System.out.println(instant4);
		Date from = Date.from(instant4);
		System.out.println(from);
		
	}
}

```

## DateTimeFormatter:格式化类

```java
package com.qf.chapter18_2;

import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

/**
 * DateTimeFormatter类的使用
 * @author wgy
 *
 */
public class Demo4 {
	public static void main(String[] args) {
		//创建DateTimeFormatter
		DateTimeFormatter dtf=DateTimeFormatter.ofPattern("yyyy/MM/dd HH:mm:ss");
		//(1)把时间格式化成字符串
		String format = dtf.format(LocalDateTime.now());
		System.out.println(format);
		//(2)把字符串解析成时间
		LocalDateTime localDateTime = LocalDateTime.parse("2020/03/10 10:20:35", dtf);
		System.out.println(localDateTime);
	}
}

```



