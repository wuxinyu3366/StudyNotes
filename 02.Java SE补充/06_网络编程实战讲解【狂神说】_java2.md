# 网络编程

# 1.1概述

地球村：你在西安，你朋友在美国！

信件：

![image-20210116101009744](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116101009744.png)

**计算机网络：**

计算机网络是指将==地理位置不同==的具有独立功能的==多台计算机及其外部设备，通过通信线路连接起来==，在网络操作系统，网络管理软件及==网络通信协议==的管理和协调下，==实现资源共享和信息传递==的计算机系统。



**网络编程的目的：**

无限电台。。。。传播交流信息，数据交换。通信



**想要达到这个效果需要什么：**

1.如何准确的定位网络上的一台主机192.168.31.156 ：端口，定位到这个计算机上的某个资源

2.找到了这个珠玑，如何传输数据



Javaweb： 网页编程 		B/S

网络编程：TCP/IP 		C/S

![image-20210116103025009](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116103025009.png)

# 1.2网络通信的要素

如何实现网络的通信？

通信双方地址：

- IP

- 端口号

- 192.168.16.124：:5900

- 规则：网络通信的协议

  ![image-20210116103517308](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116103517308.png)

  TCP/IP

  ![image-20210116103601904](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116103601904.png)
  
  小结：
  
  1. 网络编程中有两个主要的问题
     - 如何准确的定位到网络上的一台或多台主机
     - 找到主机之后如何进行通信

1. 网络编程中高端要素

   - IP和端口号 IP
   - 网络通信协议 UDP /TCP

2. 万物皆对象



# 1.3IP

   ip地址：InteAddress 					查看本地cmd ipconfig

   - 唯一定位一台网络上计算机
   - 127.0.0.1：本机localhost
   - ip地址的分类
     - ipv4/Ipv6
       - ==ipv4== 127.0.0.1 4个字节组成。 0~255 		42亿个   2011年用尽了
       
       - ==ipv6== fe80::60f8:dddd:6bea:17a7%5 ，128位。8个无符号整数！
       
         - ```java
           伪造的ipv6地址
             2001:0bb2:aaaa:0015:0000:0000:1aaa:1312 
           ```

    ```
    -公网（互联网）/私网（局域网）
    	ABCD类地址
    	192.168.xx.xx专门给组织内部使用的
   - 域名：记忆IP问题！
        - 	IP：www.vip.com
                
               

```java
package com.kuang.lesson01;

import java.net.InetAddress;
import java.net.UnknownHostException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 10:49
 * @Description: com.kuang.lesson01
 * @version: 1.0
 */
public class TestInteAddress {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        try {
            //查询本机地址
            InetAddress inetAddress1=InetAddress.getByName("127.0.0.1");
            System.out.println(inetAddress1);
            InetAddress inetAddress3 = InetAddress.getByName("localhost");
            System.out.println(inetAddress3);
            InetAddress inetAddress4 = InetAddress.getLocalHost();
            System.out.println(inetAddress4);
            //查询网站地址
            InetAddress inetAddress2 = InetAddress.getByName("www.baidu.com");
            System.out.println(inetAddress2);
            //常用方法
            System.out.println(inetAddress2.getAddress());
            System.out.println(inetAddress2.getCanonicalHostName());//规范的名字
            System.out.println(inetAddress2.getHostAddress());//ip
            System.out.println(inetAddress2.getHostName());//域名，或自己电脑的名字
        }catch (UnknownHostException e){
            e.printStackTrace();
        }

    }
}

```

 ![image-20210116105554386](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116105554386.png)



# 1.4端口

端口表示计算机上的一个程序的进程;

- 不同的进程有不同的端口号!用来区分软件!
- 被规定0~65535
- TCPUDP :65535* 2 	tcp: 80，udp: 80吗，单个协议下，端口号不能冲突
- 端口分类
  - 公有端口0~1023
    - HTTP:80
    - HTTPS: 443
    - FTP:21
    - Telent : 23
  - 程序注册端口:1024~49151,分配用户或者程序
    - Tomcat : 8080
    - MySQL : 3306
    - Oracle : 1521
  - 动态、私有:49152~65535



```bash
netstat -ano 									#查看所有的窗口
netstat -ano|findstr"5900" 		#查看指定的端口
taskList|findstr "8696" 			#查看指定端口的进程
ctrl+shift+Esc     
```

 

```java
package com.kuang.lesson01;

import java.net.InetSocketAddress;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 11:03
 * @Description: com.kuang.lesson01
 * @version: 1.0
 */
public class TestInetSocketAddress {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        InetSocketAddress inetSocketAddress = new InetSocketAddress("127.0.0.1",8080);
        InetSocketAddress inetSocketAddress2= new InetSocketAddress("localhost",8080);
        System.out.println(inetSocketAddress);
        System.out.println(inetSocketAddress2);

        System.out.println(inetSocketAddress.getAddress());
        System.out.println(inetSocketAddress.getHostName());
        System.out.println(inetSocketAddress.getPort());

    }
}

```

![image-20210116110559941](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116110559941.png)

![image-20210116110716732](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116110716732.png)



# 1.5通信协议

协议：约定，就好比我们现在说的普通话

**网络通信协议**：速率，传输码率，代码结构，传输控制....

**问题**：非常复杂

大事化小：分层！

**TCP/IP协议簇：实际上是一组协议**

重要：

- TCP：**用户传输协议**
- UDP：**用户数据报协议**

出名的协议：

- TCP：
- IP：网络互连协议
- ![image-20210116110949215](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116110949215.png)

**TCP、UDP对比**

TCP:打电话

- 连接，稳定

- `三次握手`和`四次挥手`

  ```java
  最少需要三次,保证稳定连接!
    
  A:你瞅啥?
  B:瞅你咋地?
  A:干一场!
    
    
  A:我要走了!
  B:我真的要走了吗?
  B:你真的真的要走了吗?
  A:我的真的要走了!
  
  ```

  ![image-20210116111506746](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116111506746.png)

  ![image-20210116111524362](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116111524362.png)

- 客户端、服务端

- 传输完成，释放连接，效率低

UDP∶发短信

- 不连接，不稳定

- 客户端、服务端:没有明确的界限

- 不管有没有准备好，都可以发给你..

- 导弹

- DDOS:洪水攻击!(饱和攻击)

  



# 1.6TCP

![image-20210116113918269](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210116113918269.png)

## TCP实现客户端向服务器发送消息

服务端

```java
package com.kuang.lesson01;

import com.sun.source.tree.TryTree;

import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.net.ServerSocket;
import java.net.Socket;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 11:22
 * @Description: com.kuang.lesson01
 * @version: 1.0
 */
public class TestTcpServer {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        ServerSocket serverSocket = null;
        Socket socket= null;
        InputStream is = null;
        ByteArrayOutputStream baos = null;

        try {
            //1.我得有一个地址
            serverSocket = new ServerSocket(9999);
            //2.等待客户端连接过来
            socket = serverSocket.accept();
            //3.读取客户端的消息
            is = socket.getInputStream();
            //管道流
            baos = new ByteArrayOutputStream();
            byte[] buffer = new byte[1024];
            int len=0;
            while((len=is.read(buffer))!=-1){
                baos.write(buffer,0,len);
            }
            System.out.println(baos.toString());
        }catch (IOException e){
            e.printStackTrace();
        }finally {

            try {
                baos.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                is.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                socket.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                serverSocket.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}

```

 

客户端

```java
package com.kuang.lesson01;

import java.io.IOException;
import java.io.OutputStream;
import java.net.InetAddress;
import java.net.Socket;
import java.nio.charset.StandardCharsets;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 11:21
 * @Description: com.kuang.lesson01
 * @version: 1.0
 */
public class TestTcpClient {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Socket socket= null;
        OutputStream os = null;

        try {
            //1.要知道服务器地址，端口号
            InetAddress serverIP = InetAddress.getByName("127.0.0.1");
            int port = 9999;
            //2.创建一个socket连接
            socket = new Socket(serverIP, port);
            //3.发送消息IO流
            os = socket.getOutputStream();
            os.write("你好，欢迎学习Java".getBytes(StandardCharsets.UTF_8));

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            if (os != null) {
                try {
                    os.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }

            if (socket != null) {
                try {
                    socket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

    }
}

```

## 文件上传



服务端

```java
package com.kuang.lesson02;

import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;
import java.nio.charset.StandardCharsets;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 11:44
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class TestFileServer {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) throws Exception {
        //1.创建服务
        ServerSocket serverSocket = new ServerSocket(9999);
        //2.监听客户端的连接
        Socket socket = serverSocket.accept();
        //3.获取输入流
        InputStream is = socket.getInputStream();
        //4.文件输出
        FileOutputStream fos = new FileOutputStream(new File("..."));
        byte[] buffer = new byte[1024];
        int len;
        while((len=is.read())!=-1){
            fos.write(buffer,0,len);
        }

        //通知服务器段我接受完毕了
        OutputStream os=socket.getOutputStream();
        os.write("我接受完毕了，你可以断开".getBytes(StandardCharsets.UTF_8));

        //5.关闭资源
        fos.close();
        is.close();
        socket.close();
        serverSocket.close();
    }
}

```

 

```java
package com.kuang.lesson02;

import java.io.*;
import java.net.InetAddress;
import java.net.Socket;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 11:44
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class TestFileClient {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) throws IOException {
        //1.创建一个Socket连接
        Socket socket = new Socket(InetAddress.getByName("127.0.0.1"),9999);
        //2.创建一个输出流
        OutputStream os = socket.getOutputStream();
        //3.读取文件
        FileInputStream fis = new FileInputStream(new File("..."));
        //4.写出文件
        byte[] buffer = new byte[1024];
        int len;
        while((len=fis.read())!=-1){
            os.write(buffer,0,len);
        }

        //通知服务器我已经结束了
        socket.shutdownOutput();

        //确定服务器接受完毕，才能断开连接
        InputStream is = socket.getInputStream();
        //String byte[]
        ByteArrayOutputStream baos = new ByteArrayOutputStream();
        byte[] buffer2 = new byte[1024];
        int len2;
        while((len2 = is.read())!=-1){
            baos.write(buffer2,0,len2);
        }

        System.out.println(baos.toString());

        //5.关闭资源
        baos.close();
        is.close();
        fis.close();
        os.close();
        socket.close();

    }
}

```



# 1.7Tomcat

服务端

- 自定义 S
- Tomcat服务器 S

客户端

- 自定义 C
- 浏览器 B

# 1.8UDP

## 发短信

客户端

```java
package com.kuang.lesson03;

import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 12:10
 * @Description: com.kuang.lesson03
 * @version: 1.0
 */
//不需要连接服务器
public class TestUDPClient {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) throws IOException {
        //1.建立Socket
        DatagramSocket socket=new DatagramSocket();

        //2.打包数据包
        String msg="hello，server";
        new DatagramPacket(msg.getBytes(),0,msg.getBytes().length);
        //发送
        InetAddress address=InetAddress.getByName("127.0.0.1");
        int post=9090;
        //数据，数据的长度起始，要发送给谁
        DatagramPacket packet=new DatagramPacket(msg.getBytes(),0,msg.getBytes().length,address,post);

        //3.发送包
        socket.send(packet);
        //4.关闭流
        socket.close();
    }
}

```



服务器端

```java
package com.kuang.lesson03;

import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 12:10
 * @Description: com.kuang.lesson03
 * @version: 1.0
 */
//服务器端,等待客户端的数据包
public class TestUDPServer {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) throws IOException {
        //开放端口
        DatagramSocket socket=new DatagramSocket(9090);
        //接受数据包
        byte[] buffer=new byte[1024];
        DatagramPacket packet=new DatagramPacket(buffer,0,buffer.length);

        socket.receive(packet);//阻塞接受

        System.out.println(packet.getAddress().getHostName());
        System.out.println(new String(packet.getData()));

        //关闭连接
        socket.close();
    }
}

```

## 咨询

### **循环发送消息**

发送方

```java
package com.kuang.chat;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;
import java.nio.charset.StandardCharsets;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 12:21
 * @Description: com.kuang.chat
 * @version: 1.0
 */
public class UDPSend {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) throws Exception {
        DatagramSocket datagramSocket = new DatagramSocket(8888);

        while (true) {
            //准备数据，控制台读取System.in
            BufferedReader buf = new BufferedReader(new InputStreamReader(System.in));
            // 读取控制台输入的一行并把它转化为字符
            String Buf = buf.readLine();

            InetAddress inetAddress = InetAddress.getByName("127.0.0.1");
            DatagramPacket datagramPacket = new DatagramPacket(Buf.getBytes(StandardCharsets.UTF_8), 0, Buf.length(), inetAddress, 9999);

            datagramSocket.send(datagramPacket);

            if (Buf.equals("bye"))
                break;
        }
        datagramSocket.close();
    }

}


```



接收方

```java
package com.kuang.chat;

import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 12:22
 * @Description: com.kuang.chat
 * @version: 1.0
 */
public class UDPRecive {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) throws Exception {
        //建立链接
        DatagramSocket datagramSocket = new DatagramSocket(9999);
        byte[] bufin = new byte[1024];
        while (true) {

            //准备接收包裹
            DatagramPacket datagramPacket = new DatagramPacket(bufin, 0, bufin.length);

            datagramSocket.receive(datagramPacket);//阻塞时接收包裹

            byte[] data = datagramPacket.getData();
            String msg = new String(data, 0, data.length);
            System.out.println(msg);

            if (msg.equals("bye")) {
                break;
            }

            datagramSocket.close();
        }
    }

}


```

### 在线咨询：两个人都可以发送

发送端线程：

```java
package com.kuang.ChatWith;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetSocketAddress;
import java.net.SocketException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 12:59
 * @Description: com.kuang.ChatWith
 * @version: 1.0
 */
public class Send implements Runnable{
    DatagramSocket datagramSocket;
    DatagramPacket datagramPacket;
    private int fromPort;
    private String toIP;
    private int Toport;
    BufferedReader bufferedReader;
    String buf;

    public Send(int fromPort,String toIP,int toport){
        this.fromPort = fromPort;
        this.toIP = toIP;
        this.Toport = toport;
        try {
            this.datagramSocket=new DatagramSocket(fromPort);
        } catch (SocketException e) {
            e.printStackTrace();
        }
    }
    @Override
    public void run() {
        while(true){
            try {
                bufferedReader=new BufferedReader(new InputStreamReader(System.in));
                buf=bufferedReader.readLine();
                byte[] buff=buf.getBytes();
                datagramPacket= new DatagramPacket(buff,0,buff.length,new InetSocketAddress(this.toIP,this.Toport));

                datagramSocket.send(datagramPacket);

                if (buf.equals("bye")){
                    break;
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        datagramSocket.close();

    }
}

```



接收端线程：

```java
package com.kuang.ChatWith;

import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.SocketException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 12:59
 * @Description: com.kuang.ChatWith
 * @version: 1.0
 */
public class Receive implements Runnable{
    DatagramSocket datagramSocket;
    DatagramPacket datagramPacket;
    private String FromID;
    private int Port;

    public Receive(String fromID,int port) {
        this.FromID = fromID;
        this.Port=port;
        try {
            datagramSocket = new DatagramSocket(port);
        }catch (SocketException e){
            e.printStackTrace();
        }
    }

    @Override
    public void run() {
        while (true) {
            try {
                byte[] buff = new byte[1024];
                datagramPacket = new DatagramPacket(buff, 0, buff.length);
                datagramSocket.receive(datagramPacket);

                byte[] data=datagramPacket.getData();
                String msg=new String(data,0,data.length);

                System.out.println(FromID + ":" +msg);

                if (datagramPacket.equals("bye")) {
                    break;
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        datagramSocket.close();
    }
}

```



老师：

```java
package com.kuang.ChatWith;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 12:58
 * @Description: com.kuang.ChatWith
 * @version: 1.0
 */
public class Teacher {
    public static void main(String[] args) {
        new Thread(new Send(7755,"localhost",7787)).start();
        new Thread(new Receive("学生：",9999)).start();
    }
}

```



学生：

```java
package com.kuang.ChatWith;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 12:58
 * @Description: com.kuang.ChatWith
 * @version: 1.0
 */
public class Student {
    public static void main(String[] args) {
        new Thread(new Send(7754,"localhost",9999)).start();
        new Thread(new Receive("老师：",7787)).start();
    }
}

```

两人既可以是发送端，也可以是接收端

# 1.9URL

https://www.baidu.com/

统一资源定位符：定位资源，定位互联网上某一个资源

DNS域名解析  https://www.baidu.com/  zzz.zzzz.zzzz

```java
协议://ip地址:端口/项目名/资源
```

### URL下载资源

```java
URL url=new URL("...");
HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection();
```



```java
package com.kuang.lesson04;

import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.net.HttpURLConnection;
import java.net.URL;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/16 - 01 - 16 - 13:29
 * @Description: com.kuang.lesson04
 * @version: 1.0
 */
public class Url {
    public static void main(String[] args) throws IOException {
        
      URL url=new URL("https://m801.music.126.net/20201123231609/7a60a829f966abbdfc75ee0756ed0ff9/jdyyaac/obj/w5rDlsOJwrLDjj7CmsOj/4916388353/e2fe/8be5/e1e6/c7614d21f4afc33120723d86e09d330d.m4a");
        HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection();

        InputStream in=urlConnection.getInputStream();
        FileOutputStream Fout=new FileOutputStream("d.m4a");

        byte[] buff=new byte[1024];
        int len;
        while ((len=in.read(buff))!=-1){
            Fout.write(buff,0,len);
        }

        Fout.close();
        in.close();
        urlConnection.disconnect();
    }


}
```