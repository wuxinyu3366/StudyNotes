# 文件的上传和下载

## 1.准备工作

![image-20210129165730976](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129165731.png)

![image-20210129170226600](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129170226.png)

![image-20210129171252210](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129171252.png)

![image-20210129172213660](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129172213.png)

## 2.思路分析

### 2.1下载文件思路步骤

1.要获取下载文件的路径

2.下载的文件名是啥?

3.设置浏览器能够支持(Content-Disposition) 下载我们需要的东西

4.获取下载文件的输入流

5.创建缓冲区

6.获取0utputStream对象

7.将FileOutputStream流写入到buffer缓中区，使用Outputstream将缓冲区中的数据输出到客户端!

### 2.2文件上传注意事项

1.为保证服务器安全，上传文件应该放在外界无法直接访问的目录下， 比如放于WEB-INF目录下。

2.为防止文件覆盖的现象发生,要为上传文件产生一个唯一 的文件名

3.要限制上传文件的最大值。

4.可以限制上传文件的类型,在收到上传文件名时,判断后缀名是否合法。

![image-20210129171217327](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129171217.png)

## 3.上传文件实现

### 1. 导入依赖包

https://mvnrepository.com/artifact/commons-fileupload/commons-fileupload/1.4

https://mvnrepository.com/artifact/commons-io/commons-io/2.8.0

![image-20210129172859208](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129172859.png)

![image-20210129172850007](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129172850.png)

![image-20210129172931822](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129172931.png)

记得必须全部导入！！！！！

![image-20210129172948975](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129172949.png)

### 2.使用类介绍

【文件上传的注意事项】

1.为保证服务器安全，上传文件应该放在外界无法直接访问的目录下，比如放于`WEB-INF`目录下。

2.为防止文件覆盖的现象发生，要为上传文件产生一个唯一的文件名

3.要限制上传文件的最大值。

4.可以限制上传文件的类型，在收到上传文件名时，判断后缀名是否合法。

【需要用到的类详解】

`ServletFileUpload`负责处理上传的文件数据,并将表单中每个输入项封装成一个`FileItem`对象，在使用`SevletFileupload`对象解析请求时需要`DiskFileltemFactory`对象。所以，我们需要在进行解析工作前构造好`DiskFileItemFactory`对象，通过`ServletFileUpload`对象的构造方法或`setFiletemFactory()`方法设置`ServletFileUpload`对象的`fileItemFactory`属性。



#### Fileltem类

在HTML页面input必须有name <input type="file" name="filename">

表单如果包含一个文件上传输入项的话，这个表单的`enctyp`属性就必须设置为`multipart/form-dat
a`

```jsp
<form action="${pageContext.request.contextPath}/upload.do" enctype="multipart/form-data" method="post">
上传用户:<input type="text" name="username"><br/>
上传文件1: <input type="file" name="file1"><br/>
上传文件2:<input type="file" name="file2"><br/>
 <input type="submit" value="提交">
</form>
```

浏览器表单的类型如果为multipart/form-data ,在服务器端想获取数据就要通过流。

常用方法

```java
//isFormField方法用于判断FileItem类对象封装的数据是一个普通文本表单
//还是一个文件表单，如果是普通表单字段则返回true，否则返回false
boolean isFormField();

//getFieldName方法用于返回表单标签name属性的值。string getFieldName();
//getstring方法用于将FileItem对象中保存的数据流内容以一个字符串返回
string getstring();

//getName方法用于获得文件上传字段中的文件名。
string getName();

//以流的形式返回上传文件的数据内容。
Inputstream getInputstream()
  
//delete方法用来清空FileItem类对象中存放的主体内容
//如果主体内容被保存在临时文件中，delete方法将删除该临时文件。
void delete();

```

#### ServletFileUpload类

`ServletFileUpload`负责处理上传的文件数据,并将表单中每个输入项封装成一个`FileItem`对象中.使用其`parseRequest(HttpServletRequest)`方法可以将通过表单中每一个HTML标签提交的数据封装成—个`FileItem`对象，然后以`List`列表的形式返回。使用该方法处理上传文件简单易用。



### 3.代码编写

未出现先导包  Servlet

https://mvnrepository.com/artifact/javax.servlet/jsp-api/2.0

https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api/4.0.1



![image-20210129175757779](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129175757.png)

```java
package com.kuang.servlet; /**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/29 - 01 - 29 - 17:59
 * @Description: ${PACKAGE_NAME}
 * @version: 1.0
 */

import org.apache.commons.fileupload.FileItem;
import org.apache.commons.fileupload.FileUploadException;
import org.apache.commons.fileupload.ProgressListener;
import org.apache.commons.fileupload.disk.DiskFileItemFactory;
import org.apache.commons.fileupload.servlet.ServletFileUpload;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.List;
import java.util.UUID;

@WebServlet(name = "FileServlet", value = "/upload.do")
public class FileServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //判断上传的文件是普通表非还是带文件的表单
        if (!ServletFileUpload.isMultipartContent(request)) {
            return; //终止方法运行说明这是一个普远的表单，直接返回
        }

        //创建上传文件的保存路径，建议在WEB-INF路径下，安全，用户无法直接访问上传的文件;
        String uploadPath = this.getServletContext().getRealPath("/WEB-INF/upload");//文件夹
        File uploadFile = new File(uploadPath);
        if (!uploadFile.exists()) {
            uploadFile.mkdir(); //创建这个目录
        }

        //缓存，临时文件
        //临时路径，假如文件超过J预期的大小，我们就把他放到一一个临时文件中，过几天自动删除，或者提醒用户转存为永久
        String tmpPath = this.getServletContext().getRealPath("/WEB-INF/tmp");
        File file = new File(tmpPath);
        if (!file.exists()) {
            file.mkdir(); //创建这个临时目录
        }
        //处理上传的文件，一般都需要通过流来获取，我们可以使request. getInputstream(),原生态的文件上传流获取，十分麻烦
        //但是我们都建议使用Apache的文件上:传组件米实现，common-fileupload, 它需要依赖于commons-io组件:
        /*
        ServletFileUpload负责处理上传的文件数据并将表单中每个输入项封装成- - 个FileItem对象。
        在使用ServletFileUpload对象解析请求时需要DiskFileItemFactory对象。
        所以，我们需要在进行解析工作前构造好DiskFileItemFactory对象。
        通过ServletFileUpload对象的构造方法或setFileItemFactory()方法设置ServletFileUpload对象的fileItemFactory属性。
        */
        try {
            //1.创建DiskFileItemFactory对象，处理文件上传路径或者大小限制的;
            DiskFileItemFactory factory = getDiskFileItemFactory(file);
            //2.获取ServletFileUpload
            ServletFileUpload upload = getServletFileUpload(factory);
            //3.处理上传的文件
            String msg = uploadParseRequest(upload, request, uploadPath);
            //servlet请求转发消息
            request.setAttribute("msg", msg);
            request.getRequestDispatcher("info.jsp").forward(request, response);

        } catch (FileUploadException e) {
            e.printStackTrace();
        }
    }

    public static DiskFileItemFactory getDiskFileItemFactory(File file) {
        DiskFileItemFactory factory = new DiskFileItemFactory();
        //通过这个工厂设置一个缓冲区，当上传的文件大于这个缓冲区的时候，将他放到临时文件中;
        factory.setSizeThreshold(1024 * 1024); //缓存区大小为1M
        factory.setRepository(file);//临时目录的保存目录，需要一个File
        return factory;
    }

    public static ServletFileUpload getServletFileUpload(DiskFileItemFactory factory) {
        ServletFileUpload upload = new ServletFileUpload(factory);
        //监听文件上传进度;
        upload.setProgressListener(new ProgressListener() {
            @Override
            //pBytesRead:已经读取到的文件大小
            //pContentlength :文件大小
            public void update(long pBytesRead, long pContentLength, int pItems) {
                System.out.println("总大小:" + pContentLength + "已上传:" + pBytesRead);
            }
        });
        //处理乱码问题
        upload.setHeaderEncoding("UTF-8");
        //设置单个文件的最大值
        upload.setFileSizeMax(1024 * 1024 * 10);
        //设置总共能够上传文件的大小
        //1024=1kb*1024=1M*10=10M
        upload.setSizeMax(1024 * 1024 * 10);
        return upload;
    }

    /**
     * ServletFileUpload负责处理上传的文件数据并将表单中每个输入项封装成- - 个FileItem对象。
     * 在使用ServletFileUpload对象解析请求时需要DiskFileItemFactory对象。
     * 所以，我们需要在进行解析工作前构造好DiskFileItemFactory对象。
     * 通过ServletFileUpload对象的构造方法或setFileItemFactory()方法设置ServletFileUpload对象的fileItemFactory属性。
     */
    public static String uploadParseRequest(ServletFileUpload upload, HttpServletRequest request, String uploadPath)
            throws FileUploadException, IOException {
        String msg = "";
        //3.把前端请求解析，封装成一个FileItem对象
        List<FileItem> fileItems = upload.parseRequest(request);
        for (FileItem fileItem : fileItems) {
            if (fileItem.isFormField()) { //判断上传的文件是普通的表单还是带文件的表单
                //getFieldName指的是前端表单控件的name;
                String name = fileItem.getFieldName();
                String value = fileItem.getString("UTF-8"); //处理乱码
                System.out.println(name + ":" + value);
            } else { //判断它是上传的文件
                /*====================处理文件========================*/
                //拿到文件名字
                String uploadFileName = fileItem.getName();
                System.out.println("上传的文件名: " + uploadFileName);
//                可能出现文件名不合法的情况
                if (uploadFileName.trim().equals("") || uploadFileName == null) {
                    continue;
                }
                //获得上传的文件名/images/girl/paojie.png      ------》paojie.png
                String fileName = uploadFileName.substring(uploadFileName.lastIndexOf("/") + 1);
                //获得文件的后缀名   ------》png
                String fileExtName = uploadFileName.substring(uploadFileName.lastIndexOf(".") + 1);
                /*
                如果文件后缀名fileExtName 不是我们所需要的
                就直接return,不处理，告诉用户文件类型不对。
                */
                System.out.println("文件信息[件名: " + fileName + "---文件类型" + fileExtName + "]");
                //可以使用UUID (序列化：唯一识别的通用码)，保证文件名唯一;
                //UUID. randomUUID()，implements Serializable（啥也没有 标记式接口），随机生一个唯一识别的通 用码;
                String uuidPath = UUID.randomUUID().toString();
                /*==================处理文件完-=======================*/
                //存到哪? uploadPath
                //文件真实存在的路径realPath
                String realPath = uploadPath + "/" + uuidPath;
                //给每个文件创建一个对应的文件夹
                File realPathFile = new File(realPath);
                if (!realPathFile.exists()) {
                    realPathFile.mkdir();
                }
                /*====================存放地址完毕-========================*/
                //获得文件上传的流
                InputStream inputStream = fileItem.getInputStream();
                //创建一个文件输出流
                //realPath =真实的文件夹;
                //差了一个文件;加上输出文件的名字+"/"+uuidFileName
                FileOutputStream fos = new FileOutputStream(realPath + "/" + fileName);
                //创建一个缓冲区
                byte[] buffer = new byte[1024 * 1024];
                //判断是否读取完毕
                int len = 0;
                //如果大于0说明还存在数据;
                while ((len = inputStream.read(buffer)) > 0) {
                    fos.write(buffer, 0, len);
                }
                //关闭流
                fos.close();
                inputStream.close();
                msg = "文件上传成功!";
                fileItem.delete(); //上传成功，清除临时文件
                /*====================文件传输完==========================*/
            }
        }
        return msg;
    }

}

```

```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/29
  Time: 17:22
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
    <title>$Title$</title>
  </head>
  <body>
  <form action="${pageContext.request.contextPath}/upload.do" enctype="multipart/form-data" method="post">
    上传用户:<input type="text" name="username"><br/>
    上传文件1: <input type="file" name="file1"><br/>
    上传文件2:<input type="file" name="file2"><br/>
    <input type="submit" value="提交">
  </form>
  </body>
</html>

```

```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/29
  Time: 18:28
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    ${msg}
</body>
</html>

```



缓存，临时文件
临时路径，假如文件超过预期的大小，我们就把他放到一一个临时文件中，过几天自动删除，或者提醒用户转存为永久

![image-20210129181024055](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129181024.png)

## 4.下载文件实现

### 1.配置xml

### 2.注册FileServlet

```java
public class FileServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 1.获取下载文件的路径
        //String realPath = this.getServletContext().getRealPath("/dali.jpg");
        String realPath = "E:\\CodePlace\\Java\\idea\\狂神说Java\\Maven\\javawebMaven\\javaweb\\servlet-03-response\\target\\classes\\dali.jpg";
        System.out.println("下载文件的路径为：" + realPath);
        // 2.下载的文件名
        String filename = realPath.substring(realPath.lastIndexOf("\\") + 1);
        // 3.设置想办法让浏览器能够支持下载我们需要的东西
        resp.setHeader("Content-Disposition", "attachment; filename=" + URLEncoder.encode(filename,"UTF-8"));
        // 4.获取下载文件的输入流
        FileInputStream in = new FileInputStream(realPath);
        // 5.创建缓冲区
        int len = 0;
        byte[] buffer = new byte[1024];
        // 6.获取OutputStream对象
        ServletOutputStream out = resp.getOutputStream();
        // 7.将FileOutputStream流写入到buffer缓冲区,使用OutputStream将缓冲区中的数据输出到客户端
        while((len=in.read(buffer))!=-1){
            out.write(buffer,0,len);
        }
        in.close();
        out.close();
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

# 网页注册发送邮件功能实现

## 1.基础知识铺垫

### 电子邮件

```
  要在网络上实现邮件功能，必须要有专门的邮件服务器。
  这些邮件服务器类似于现实生活中的邮局，它主要负责接收用户投递过来的邮件，并把邮件投递到邮件接收者的电子邮箱中。

  SMTP服务器地址：一般是 smtp.xxx.com，比如163邮箱是smtp.163.com，qq邮箱是smtp.qq.com。

  电子邮箱(E-Mail地址)的获得需要在邮件服务器上进行申请。比如我们要使用QQ邮箱，就需要开通邮箱功能；
```

![img](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129192946.png)
![img](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129192949.png)
![img](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129192951.png)

### 传输协议

- SMTP协议
  发送邮件：
  我们通常把处理用户smtp请求(邮件发送请求)的服务器称之为SMTP服务器(邮件发送服务器)。
- POP3协议
  接收邮件：
  我们通常把处理用户pop3请求(邮件接收请求)的服务器称之为POP3服务器(邮件接收服务器)。

### 邮件收发原理

![image-20210129192747523](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129194957.png)

![img](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129192955.png)
1、邮件服务器

 ①SMTP邮件服务器：替用户发送邮件和接收外面发送给本地用户的邮件（发送邮件）

 ②POP3/IMAP邮件服务器：帮助用户读取SMTP邮件服务器接收进来的邮件（接受邮件）

2、邮件传输协议

 ①电子邮件需要在邮件客户端和邮件服务器之间，以及两个邮件服务器之间进行邮件传递，那就必须要遵守一定的规则，这个规则就是邮件传输协议

 ②SMTP协议：全称为 Simple Mail Transfer Protocol，简单邮件传输协议。它定义了邮件客户端软件和SMTP邮件服务器之间，以及两台SMTP邮件服务器之间的通信规则

 ③POP3协议：全称为 Post Office Protocol，邮局协议。它定义了邮件客户端软件和POP3邮件服务器的通信规则

 ④IMAP协议：全称为 Internet Message Access Protocol,Internet消息访问协议，它是对POP3协议的一种扩展，也是定义了邮件客户端软件和IMAP邮件服务器的通信规则

 我们说所有的邮件服务器和邮件客户端软件程序都是基于上面的协议编写的

引自：https://www.jb51.net/article/125852.htm

### 邮件分类

-  简单邮件：没有除了文字以外的其他所有文件(包括附件和图片、视频等)，即纯文本邮件
-  复杂邮件：除了传统的文字信息外，还包括了一些非文字数据的邮件

### 使用Java实现邮件发送需要使用到的类

#### 概述

```
  我们将用代码完成邮件的发送。这在实际项目中应用的非常广泛，比如注册需要发送邮件进行账号激活，再比如OA项目中利用邮件进行任务提醒等等。

  使用Java发送 E-mail 十分简单，但是首先你应该准备 JavaMail API 和Java Activation Framework。
  
  得到两个jar包：
  1.mail.jar
  https://mvnrepository.com/artifact/javax.mail/mail/1.4.7
  2.activation.jar
  https://mvnrepository.com/artifact/javax.activation/activation/1.1.1

  JavaMail 是sun公司（现以被甲骨文收购）为方便Java开发人员在应用程序中实现邮件发送和接收功能而提供的一套标准开发包，它支持一些常用的邮件协议，如前面所讲的SMTP，POP3，IMAP,还有MIME等。我们在使用JavaMail API 编写邮件时，无须考虑邮件的底层实现细节，只要调用JavaMail 开发包中相应的API类就可以了。

  我们可以先尝试发送一封简单的邮件，确保电脑可以连接网络。
  - 创建包含邮件服务器的网络连接信息的Session对象。
  - 创建代表邮件内容的Message对象
  - 创建Transport对象，连接服务器，发送Message，关闭连接
  主要有四个核心类，我们在编写程序时，记住这四个核心类，就很容易编写出Java邮件处理程序。
```



## 2.授权码的获取

![在这里插入图片描述](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129194911.png)

![image-20210129195702322](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129195702.png)

![image-20210129195742036](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129195742.png)

```java
lfapwgjonpfubeaa
```



## 3.发送一封邮件

![img](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129194948.png)

**由上图我们可以确定几个必须步骤**

**1.创建session对象**

**2.创建Transport对象**

**3.使用邮箱的用户名和授权码连上邮件服务器**

**4.创建一个Message对象（需要传递session）**

- **message需要指明发件人、收件人以及文件内容**

**5.发送邮件**

**6.关闭连接**

```java
package com.kuang.mail;

import com.sun.mail.util.MailSSLSocketFactory;

import javax.mail.*;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;
import java.util.Properties;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/29 - 01 - 29 - 19:51
 * @Description: com.kuang.mail
 * @version: 1.0
 */
public class MailDemo01 {
    public static void main(String[] args) throws Exception {
        Properties prop = new Properties();
        prop.setProperty("mail.host", "smtp.qq.com");  //设置QQ邮件服务器
        prop.setProperty("mail.transport.protocol", "smtp"); // 邮件发送协议
        prop.setProperty("mail.smtp.auth", "true"); // 需要验证用户名密码

        // 关于QQ邮箱，还要设置SSL加密，加上以下代码即可,大厂，其他不需要！
        MailSSLSocketFactory sf = new MailSSLSocketFactory();
        sf.setTrustAllHosts(true);
        prop.put("mail.smtp.ssl.enable", "true");
        prop.put("mail.smtp.ssl.socketFactory", sf);

        //使用JavaMail发送邮件的5个步骤

        //1、创建定义整个应用程序所需的环境信息的 Session对象
//        创建定义整个应用程序所需要的环境信息的Session对象

        //使用QQ邮箱的时候才需要，其他邮箱不需要这一段代码
        Session session = Session.getDefaultInstance(prop, new Authenticator() {//获取和SMTP服务器的连接对象
            @Override
            public PasswordAuthentication getPasswordAuthentication() {
                //发件人邮件用户名、授权码
                return new PasswordAuthentication("957904804@qq.com", "lfapwgjonpfubeaa");
            }
        });

        //开启Session的debug模式，这样就可以查看到程序发送Email的运行状态，不加为空
        session.setDebug(true);

        //2、通过session得到transport对象
        Transport ts = session.getTransport();//通过这一次和SMTP服务器的连接对象获取发送邮件的传输对象

        //3、使用邮箱的用户名和授权码连上SMTP邮件服务器，即登陆
        ts.connect("smtp.qq.com", "957904804@qq.com", "lfapwgjonpfubeaa");

        //4、创建邮件对象MimeMessage——点击网页上的写信
        //创建一个邮件对象
        MimeMessage message = new MimeMessage(session);
        //指明邮件的发件人——在网页上填写发件人
        message.setFrom(new InternetAddress("957904804@qq.com"));//设置发件人
        //指明邮件的收件人，现在发件人和收件人是一样的，那就是自己给自己发——在网页上填写收件人
        message.setRecipient(Message.RecipientType.TO, new InternetAddress("957904804@qq.com"));//设置收件人
        //邮件的标题——在网页上填写邮件标题
        message.setSubject("简单邮件发送实现");//设置邮件主题
        //邮件的文本内容——在网页上填写邮件内容
        message.setContent("<h2 style='color:red'>你好啊！</h2>", "text/html;charset=UTF-8");//设置邮件的具体内容

        //5、发送邮件——在网页上点击发送按钮
        ts.sendMessage(message, message.getAllRecipients());

        //6、关闭连接对象，即关闭服务器上的连接资源
        ts.close();
    }
}

```

![image-20210129200518245](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129200518.png)

## 4.发送一封复杂的邮件

**复杂邮件就是非纯文本的邮件，可能还包含了图片和附件等资源**

先认识两个类一个名词：

 **MIME（多用途互联网邮件扩展类型）**

- **MimeBodyPart类**

 javax.mail.internet.MimeBodyPart类**表示的是一个MIME消息**，它和MimeMessage类一样都是从Part接口继承过来。即一个MIME消息对应一个MimeBodyPart对象，而MimeBodyPart对象就是我们写的邮件内容中的元素
![img](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129200818.png)

- **MimeMultipart类**

 javax.mail.internet.MimeMultipart是抽象类 Multipart的实现子类，它**用来组合多个MIME消息**。一个MimeMultipart对象可以包含多个代表MIME消息的MimeBodyPart对象。即一个MimeMultipart对象表示多个MimeBodyPart的集合，而一个MimeMultipart表示的就是我们一封邮件的内容
![img](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129200822.png)

MimeMultipart对象的使用的时候需要设置setSubType()的属性值，一共就下面3种取值

- alternative：表明这个MimeMultipart对象中的MimeMessage对象的数据是纯文本文件
- related：表明这个MimeMultipart对象中的MimeMessage对象的数据包含非纯文本文件
- mixed：表明这个MimeMultipart对象中的MimeMessage对象的数据包含附件

我们在使得的时候如果不知道使用哪一个，直接使用mixed即可，使用这个属性值一定不会报错
![img](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129200825.png)

 相较于简单邮件，复杂邮件变化的地方只是在于邮件内容本身会发送变化，而其他的步骤都是一样的

 1、准备一些参数

 2、获取session对象

 3、获取传输对象

 4、登陆授权

 5、**写邮件 (和简单邮件相区别)**

 6、发送邮件

 7、关闭服务器资源

### 发送含图片的复杂邮件

```java
package com.kuang.mail;

import com.sun.mail.util.MailSSLSocketFactory;


import javax.activation.DataHandler;
import javax.activation.FileDataSource;
import javax.mail.*;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeBodyPart;
import javax.mail.internet.MimeMessage;
import javax.mail.internet.MimeMultipart;
import java.util.Properties;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/29 - 01 - 29 - 20:10
 * @Description: com.kuang.mail
 * @version: 1.0
 */
public class MailDemo02 {
    public static void main(String[] args) throws Exception {
        Properties prop = new Properties();
        prop.setProperty("mail.host", "smtp.qq.com");  //设置QQ邮件服务器
        prop.setProperty("mail.transport.protocol", "smtp"); // 邮件发送协议
        prop.setProperty("mail.smtp.auth", "true"); // 需要验证用户名密码

        // 关于QQ邮箱，还要设置SSL加密，加上以下代码即可,大厂，其他不需要！
        MailSSLSocketFactory sf = new MailSSLSocketFactory();
        sf.setTrustAllHosts(true);
        prop.put("mail.smtp.ssl.enable", "true");
        prop.put("mail.smtp.ssl.socketFactory", sf);

        //使用JavaMail发送邮件的5个步骤

        //1、创建定义整个应用程序所需的环境信息的 Session对象
//        创建定义整个应用程序所需要的环境信息的Session对象

        //使用QQ邮箱的时候才需要，其他邮箱不需要这一段代码
        Session session = Session.getDefaultInstance(prop, new Authenticator() {//获取和SMTP服务器的连接对象
            @Override
            public PasswordAuthentication getPasswordAuthentication() {
                //发件人邮件用户名、授权码
                return new PasswordAuthentication("957904804@qq.com", "lfapwgjonpfubeaa");
            }
        });

        //开启Session的debug模式，这样就可以查看到程序发送Email的运行状态，不加为空
        session.setDebug(true);

        //2、通过session得到transport对象
        Transport ts = session.getTransport();//通过这一次和SMTP服务器的连接对象获取发送邮件的传输对象

        //3、使用邮箱的用户名和授权码连上SMTP邮件服务器，即登陆
        ts.connect("smtp.qq.com", "957904804@qq.com", "lfapwgjonpfubeaa");

        //4、创建邮件对象MimeMessage——点击网页上的写信
        //创建一个邮件对象
        MimeMessage message = new MimeMessage(session);
        //指明邮件的发件人——在网页上填写发件人
        message.setFrom(new InternetAddress("957904804@qq.com"));//设置发件人
        //指明邮件的收件人，现在发件人和收件人是一样的，那就是自己给自己发——在网页上填写收件人
        message.setRecipient(Message.RecipientType.TO, new InternetAddress("957904804@qq.com"));//设置收件人
        //邮件的标题——在网页上填写邮件标题
        message.setSubject("简单邮件发送实现");//设置邮件主题


        System.out.println("=============================复杂邮件的邮件内容设置==================================");
        // 准备邮件数据

        // 准备图片数据
        MimeBodyPart image = new MimeBodyPart();//获取一个图片的MimeBodyPart对象
//        图片需要经过数据处理.....  DataHandler
        DataHandler dh = new DataHandler(new FileDataSource("D:\\WorkingSpace\\Idea_workingspace\\JavaWeb\\javaweb-07-功能扩展\\mail-java\\src\\1.png"));//由于图片需要字符化才能传输，所以需要获取一个DataHandler对象
        image.setDataHandler(dh);//将图片序列化
        image.setContentID("bz.jpg");//为图片的MimeBodyPart对象设置一个ID，我们在文字中就可以使用它了

        // 准备正文数据
        MimeBodyPart text = new MimeBodyPart();//获取一个文本的MimeBodyPart对象
        text.setContent("这是一封邮件正文带图片<img src='cid:bz.jpg'>的邮件", "text/html;charset=UTF-8");//设置文本内容，注意在里面嵌入了<img src='cid:bz.jpg'>

        // 描述数据关系
        MimeMultipart mm = new MimeMultipart();//获取MimeMultipart
        mm.addBodyPart(text);//将文本MimeBodyPart对象加入MimeMultipart中
        mm.addBodyPart(image);//将图片MimeBodyPart对象加入MimeMultipart中
        mm.setSubType("related");//设置MimeMultipart对象的相对熟悉为related，即发送的数据为文本+非附件资源  或者mixed（默认的）

        //设置到消息中，保存修改
        message.setContent(mm);//将最后编辑好的MimeMultipart放入消息对象中
        message.saveChanges();//保存上面的修改

        System.out.println("===============================================================");


        //5、发送邮件——在网页上点击发送按钮
        ts.sendMessage(message, message.getAllRecipients());

        //6、关闭连接对象，即关闭服务器上的连接资源
        ts.close();
    }
}

```

![image-20210129202941591](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129202941.png)

### 包含附件的发送

```java
package com.kuang.mail;

import com.sun.mail.util.MailSSLSocketFactory;

import javax.activation.DataHandler;
import javax.activation.FileDataSource;
import javax.mail.*;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeBodyPart;
import javax.mail.internet.MimeMessage;
import javax.mail.internet.MimeMultipart;
import java.util.Properties;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/29 - 01 - 29 - 20:30
 * @Description: com.kuang.mail
 * @version: 1.0
 */
public class MailDemo03 {
    public static void main(String[] args) throws Exception {
        Properties prop = new Properties();
        prop.setProperty("mail.host", "smtp.qq.com");  //设置QQ邮件服务器
        prop.setProperty("mail.transport.protocol", "smtp"); // 邮件发送协议
        prop.setProperty("mail.smtp.auth", "true"); // 需要验证用户名密码

        // 关于QQ邮箱，还要设置SSL加密，加上以下代码即可,大厂，其他不需要！
        MailSSLSocketFactory sf = new MailSSLSocketFactory();
        sf.setTrustAllHosts(true);
        prop.put("mail.smtp.ssl.enable", "true");
        prop.put("mail.smtp.ssl.socketFactory", sf);

        //使用JavaMail发送邮件的5个步骤

        //1、创建定义整个应用程序所需的环境信息的 Session对象
//        创建定义整个应用程序所需要的环境信息的Session对象

        //使用QQ邮箱的时候才需要，其他邮箱不需要这一段代码
        Session session = Session.getDefaultInstance(prop, new Authenticator() {//获取和SMTP服务器的连接对象
            @Override
            public PasswordAuthentication getPasswordAuthentication() {
                //发件人邮件用户名、授权码
                return new PasswordAuthentication("957904804@qq.com", "lfapwgjonpfubeaa");
            }
        });

        //开启Session的debug模式，这样就可以查看到程序发送Email的运行状态，不加为空
        session.setDebug(true);

        //2、通过session得到transport对象
        Transport ts = session.getTransport();//通过这一次和SMTP服务器的连接对象获取发送邮件的传输对象

        //3、使用邮箱的用户名和授权码连上SMTP邮件服务器，即登陆
        ts.connect("smtp.qq.com", "957904804@qq.com", "lfapwgjonpfubeaa");

        //4、创建邮件对象MimeMessage——点击网页上的写信
        //创建一个邮件对象
        MimeMessage message = new MimeMessage(session);
        //指明邮件的发件人——在网页上填写发件人
        message.setFrom(new InternetAddress("957904804@qq.com"));//设置发件人
        //指明邮件的收件人，现在发件人和收件人是一样的，那就是自己给自己发——在网页上填写收件人
        message.setRecipient(Message.RecipientType.TO, new InternetAddress("957904804@qq.com"));//设置收件人
        //邮件的标题——在网页上填写邮件标题
        message.setSubject("附件图片邮件发送实现");//设置邮件主题

        //邮件的文本内容
        //=================================准备图片数据
        MimeBodyPart image=new MimeBodyPart();
        //图片需要经过数据化的处理
        DataHandler dh=new DataHandler(new FileDataSource("D:\\WorkingSpace\\Idea_workingspace\\JavaWeb\\javaweb-07-功能扩展\\mail-java\\src\\1.png"));
        //在part中放入这个处理过图片的数据
        image.setDataHandler(dh);
        //给这个part设置一个ID名字
        image.setContentID("bz.jpg");

        //=================================准备正文数据
        MimeBodyPart text=new MimeBodyPart();
        text.setContent("这是一张正文<img src='cid:bz.jpg'>","text/html;charset=UTF-8");

        //=================================准备附件数据
        MimeBodyPart body1= new MimeBodyPart();
        body1.setDataHandler(new DataHandler(new FileDataSource("D:\\WorkingSpace\\Idea_workingspace\\JavaWeb\\javaweb-07-功能扩展\\mail-java\\src\\1.txt")));
        body1.setFileName("1.txt");

        //描述数据关系
        MimeMultipart mm=new MimeMultipart();
        mm.addBodyPart(body1);
        mm.addBodyPart(text);
        mm.addBodyPart(image);
        mm.setSubType("mixed");

        //设置到消息中，保存修改
        message.setContent(mm);
        message.saveChanges();


        //5、发送邮件——在网页上点击发送按钮
        ts.sendMessage(message, message.getAllRecipients());

        //6、关闭连接对象，即关闭服务器上的连接资源
        ts.close();
    }
}

```

![image-20210129203404704](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129203404.png)

## 5.网站注册发送邮件功能实现

分析：在我们注册的时候，前端我们填写的就是一个表单，这个表单提交给后端的servlet，这个servlet就向我们填写的那个邮箱中发送一封邮件

```
  所以我们需要创建一个javaweb项目，因为要使用到前端页面+servlet
```

![img](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129203605.png)
![img](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129203609.png)
![img](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129203612.png)
**拷贝两个前端素材**

 注册页面

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%--注册填写邮箱的前端页面--%>
<html>
<head>
  <title>注册</title>
</head>
<body>

<form action="${pageContext.request.contextPath}/RegisterServlet.do" method="post">
  用户名：<input type="text" name="username"><br/>
  密码：<input type="password" name="password"><br/>
  邮箱：<input type="text" name="email"><br/>
  <input type="submit" value="注册">
</form>

</body>
</html>
```

 提示成功页面

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>提示信息</title>
</head>
<body>
<h2>thhh提醒您</h2>
    ${message}
</body>
</html>
```

**编写servlet**

```java
package com.kuang.servlet;

import com.kuang.pojo.User;
import com.kuang.utils.Sendmail;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/29 - 01 - 29 - 20:45
 * @Description: com.kuang.servlet
 * @version: 1.0
 */
public class RegisterServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1、接收用户填写的表单数据
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        String email = req.getParameter("email");
//        System.out.println(username+password+email);

        //2、向用户邮箱发送邮件，注意发送邮件很耗时，所以我们启动一个子线程去做这件事，而用户则是直接跳转注册成功页面，以免降低用户体验
        User user = new User(username,password,email);
//        我们使用线程来专门发送邮件，防止出现耗时、网站注册人数过多的情况
        Sendmail sendmail = new Sendmail(user);//获取子线程对象
        new Thread(sendmail).start();//启动子线程

        //3、视图跳转 注册用户
        req.setAttribute("message","注册成功！我们已经向您的邮箱发送了邮件，请您及时进行查收。由于网络原因，您收到邮件的时间存在延迟，敬请谅解~");
        req.getRequestDispatcher("info.jsp").forward(req,resp);

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

**Web.xml**

```xml
<servlet>
    <servlet-name>RegisterServlet</servlet-name>
    <servlet-class>com.kuang.servlet.RegisterServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>RegisterServlet</servlet-name>
    <url-pattern>/RegisterServlet.do</url-pattern>
</servlet-mapping>
```

**实体类**

```java
package com.kuang.pojo;

import java.io.Serializable;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/29 - 01 - 29 - 20:51
 * @Description: com.kuang.pojo
 * @version: 1.0
 */
public class User implements Serializable {
    private String username;
    private String password;
    private String email;

    public User() {
    }

    public User(String username, String password, String email) {
        this.username = username;
        this.password = password;
        this.email = email;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    @Override
    public String toString() {
        return "User{" +
                "username='" + username + '\'' +
                ", password='" + password + '\'' +
                ", email='" + email + '\'' +
                '}';
    }
}

```

可以通过注解的方式简化实体类

**多线程工具类**

```java
package com.kuang.utils;

import com.kuang.pojo.User;
import com.sun.mail.util.MailSSLSocketFactory;

import javax.mail.*;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;
import java.util.Properties;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/29 - 01 - 29 - 20:54
 * @Description: com.kuang.utils
 * @version: 1.0
 */
//网站三秒原则：用户体验
//    多线程实现用户体验（异步处理）
public class Sendmail extends Thread {

    private String from="957904804@qq.com";

    private String host="smtp.qq.com";

    private User user;

    public Sendmail(User user){
        this.user=user;
    }
    @Override
    public void run() {
        try {
            Properties prop=new Properties();
            prop.setProperty("mail.host",host);///设置QQ邮件服务器
            prop.setProperty("mail.transport.protocol","smtp");///邮件发送协议
            prop.setProperty("mail.smtp.auth","true");//需要验证用户密码
            //QQ邮箱需要设置SSL加密
            MailSSLSocketFactory sf=new MailSSLSocketFactory();
            sf.setTrustAllHosts(true);
            prop.put("mail.smtp.ssl.enable","true");
            prop.put("mail.smtp.ssl.socketFactory",sf);

            //使用javaMail发送邮件的5个步骤
            //1.创建定义整个应用程序所需要的环境信息的session对象
            Session session= Session.getDefaultInstance(prop, new Authenticator() {
                @Override
                protected PasswordAuthentication getPasswordAuthentication() {
                    return new PasswordAuthentication(from,"lfapwgjonpfubeaa");
                }
            });
            //开启session的debug模式，这样可以查看到程序发送Email的运行状态
            session.setDebug(true);
            //2.通过session得到transport对象
            Transport ts=session.getTransport();
            //3.使用邮箱的用户名和授权码连上邮件服务器
            ts.connect(host,from,"lfapwgjonpfubeaa");
            //4.创建邮件：写文件
            //注意需要传递session
            MimeMessage message=new MimeMessage(session);
            //指明邮件的发件人
            message.setFrom(new InternetAddress(from));
            //指明邮件的收件人
            message.setRecipient(Message.RecipientType.TO,new InternetAddress(user.getEmail()));
            //邮件标题
            message.setSubject("注册通知");
            //邮件的文本内容
            message.setContent("恭喜你("+user.getUsername()+")成功注册！"+"密码："+user.getPassword()
                    ,"text/html;charset=UTF-8");
            //5.发送邮件
            ts.sendMessage(message,message.getAllRecipients());

            //6.关闭连接
            ts.close();
        }catch (Exception e){
            System.out.println(e);
        }

    }
}

```

**测试**
![img](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129203619.png)
![image-20210129210438586](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129210438.png)
![image-20210129210423814](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129210423.png)

测试成功！

再就是将我们手动下载的两个mail的jar包粘贴一份到tomcat安装目录/lib中，以免tomcat运行时找不到jar包报错

## 6.项目感悟

整个邮件发送的实现我们都是依赖的两个jar包：mail.jar、activation.jar

1.这两个jar包导入之后我们就在按照固定的调用这两个jar包中的功能进行代码编写，其实代码+步骤都是写死的，我们只需要复制粘贴，然后修改一下参数就可以在我们自己的项目上跑起来了，所以对于这个例子，我们只需要掌握使用Java发送邮件的原理/需要哪些步骤，而不用去记住代码怎么实现的，如果真的到了要用的时候，我们可以直接在网上搜索一下，这种例子一大堆，所以重点还是要学习实现原理，在理解原理的基础上那这个项目锻炼一下自己的编码+排错能力+提升对IDE的熟悉度
2.通过这个例子我们也更进一步的理解了为什么说在Java中万物皆对象：我们对邮件的操作中，获取客户端与SMTP服务器的连接需要一个session对象、进行客户端和SMTP服务器之间的数据传输需要使用Transport 对象、发送纯文本邮件需要使用MimeMessage 对象、发送非纯文本邮件需要使用MimeMultipart对象...

**收获**
​ 1.在这个项目中我们还可以加深对一个javaweb项目文件结构的熟悉

 2.加深我们在IDEA中创建WEB项目的3种方法：直接创建javaweb项目、创建一个干净的maven项目再添加web文件夹和直接使用maven创建一个javaweb项目

 3.实践了"小黄鸭调试法"

 4.见识了使用注解+框架开发的简便

 5.实现了期待的功能