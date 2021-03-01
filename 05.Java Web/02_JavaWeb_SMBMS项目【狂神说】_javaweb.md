SMBMS(超市管理项目)

![image-20210127103123340](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127103130.png)

数据库：
![image-20210127103209402](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127103209.png)
**项目如何搭建？**
考虑是不是用maven？ jar包，依赖

## 搭建项目准备工作

1. 搭建一个maven web 项目

   ![image-20210127103524828](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127103524.png)

2. 配置Tomcat

3. 测试项目是否能够跑起来

   ![image-20210127105530911](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127105531.png)

4. 导入项目中需要的jar包;
   jsp，Servlet，mysql驱动jstl，stand…

   ```xml
   <dependencies>
       <dependency>
         <groupId>junit</groupId>
         <artifactId>junit</artifactId>
         <version>4.11</version>
       </dependency>
   
       <dependency>
         <groupId>javax.servlet</groupId>
         <artifactId>servlet-api</artifactId>
         <version>2.5</version>
       </dependency>
   
       <dependency>
         <groupId>javax.servlet.jsp</groupId>
         <artifactId>javax.servlet.jsp-api</artifactId>
         <version>2.3.3</version>
       </dependency>
   
       <dependency>
         <groupId>javax.servlet.jsp.jstl</groupId>
         <artifactId>jstl-api</artifactId>
         <version>1.2</version>
       </dependency>
   
       <dependency>
         <groupId>taglibs</groupId>
         <artifactId>standard</artifactId>
         <version>1.1.2</version>
       </dependency>
   
       <dependency>
         <groupId>mysql</groupId>
         <artifactId>mysql-connector-java</artifactId>
         <version>5.1.49</version>
       </dependency>
     </dependencies>
   ```

   

5. 构建项目包结构
   ![image-20210127110127067](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127110127.png)

6. 编写实体类
   ROM映射:表-类映射

   ```sql
   详情sql见项目文档
   ```

   ![image-20210127111959738](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127111959.png)

![image-20210127112144478](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127112144.png)





1. 编写基础公共类
   1、数据库配置文件（mysql5.xx和8.xx的编写有差异）

   ```properties
   driver=com.mysql.jdbc.Driver
   #在和mysql传递数据的过程中，使用unicode编码格式，并且字符集设置为utf-8
   url=jdbc:mysql://127.0.0.1:3306/smbms?useSSL=false&useUnicode=true&characterEncoding=utf-8
   username=root
   password=123456
   ```

   2、编写数据库的公共类

```java
package com.wxy.dao;

import java.io.IOException;
import java.io.InputStream;
import java.nio.file.attribute.UserPrincipalNotFoundException;
import java.sql.*;
import java.util.Properties;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/27 - 01 - 27 - 11:30
 * @Description: com.wxy.dao
 * 操作数据库的基类--静态类
 * @version: 1.0
 */
public class BaseDao {
    //静态代码块,在类加载的时候执行
    static {
        init();
    }

    private static String driver;
    private static String url;
    private static String username;
    private static String password;

    //初始化连接参数,从配置文件里获得
    public static void init(){
        Properties properties = new Properties();
        String configFile = "db.properties";
        InputStream inputStream = BaseDao.class.getClassLoader().getResourceAsStream(configFile);

        try {
            properties.load(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }

        driver=properties.getProperty("driver");
        url=properties.getProperty("url");
        username=properties.getProperty("username");
        password=properties.getProperty("password");
    }

    /**
     * 获取数据库连接
     * @return
     */
    public static Connection getConnection() {
        Connection connection =null;
        try {
            Class.forName(driver);
            connection=DriverManager.getConnection(url,username,password);
        }catch (Exception e){
            e.printStackTrace();
        }

        return connection;
    }


    /**
     * 编写查询公共类
     * @param connection
     * @param pstm
     * @param rs
     * @param sql
     * @param params
     * @return
     */
    public static ResultSet execute(Connection connection,PreparedStatement pstm,ResultSet rs,String sql,Object[] params)throws Exception{
        pstm = connection.prepareStatement(sql);
        for (int i = 0; i < params.length; i++) {
            pstm.setObject(i+1,params[i]);
        }
        rs=pstm.executeQuery();
        return rs;
    }

    /**
     * 编写增删改公共类
     * @param connection
     * @param pstm
     * @param sql
     * @param params
     * @return
     * @throws Exception
     */
    public static int execute(Connection connection,PreparedStatement pstm,
                              String sql,Object[] params) throws Exception{
        int updateRows = 0;
        pstm = connection.prepareStatement(sql);
        for(int i = 0; i < params.length; i++){
            pstm.setObject(i+1, params[i]);
        }
        updateRows = pstm.executeUpdate();
        return updateRows;
    }

    /**
     * 释放资源
     * @param connection
     * @param pstm
     * @param rs
     * @return
     */
    public static boolean closeResource(Connection connection,PreparedStatement pstm,ResultSet rs){
        boolean flag = true;
        if(rs != null){
            try {
                rs.close();
                rs = null;//GC回收
            } catch (SQLException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
                flag = false;
            }
        }
        if(pstm != null){
            try {
                pstm.close();
                pstm = null;//GC回收
            } catch (SQLException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
                flag = false;
            }
        }
        if(connection != null){
            try {
                connection.close();
                connection = null;//GC回收
            } catch (SQLException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
                flag = false;
            }
        }

        return flag;
    }
}

```

. 3、编写字符编码过滤器

```xml
 <!--字符编码过滤器    -->
    <filter>
        <filter-name>CharacterEncodingFilter</filter-name>
        <filter-class>com.wxy.filter.CharacterEncodingFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>CharacterEncodingFilter</filter-name>
        <!--只要是 /的任何请求，会经过这个过滤器-->
        <url-pattern>/*</url-pattern>
    </filter-mapping>
```

```java
package com.wxy.filter;

import javax.servlet.*;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/27 - 01 - 27 - 11:56
 * @Description: com.wxy.filter
 * @version: 1.0
 */
public class CharacterEncodingFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        servletRequest.setCharacterEncoding("utf-8");
        servletResponse.setCharacterEncoding("utf-8");
        servletResponse.setContentType("text/html;charset=UTF-8");

        //让我们的请求继续走，如果不写，程序到这里就被拦截停止！
        filterChain.doFilter(servletRequest,servletResponse);
    }

    @Override
    public void destroy() {

    }
}

```

2.导入静态资源

![image-20210127121800428](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127121800.png)

## 登录功能实现

![image-20210127122951458](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127122951.png)

### 前端

1. 编写前端页面

   

2. 设置首页
   1.设置欢迎首页

   `login.jsp`

   ```jsp
   <%--
     Created by IntelliJ IDEA.
     User: Administrator
     Date: 2021/1/27
     Time: 12:31
     To change this template use File | Settings | File Templates.
   --%>
   <%@ page contentType="text/html;charset=UTF-8" language="java" %>
   <html>
   <head lang="en">
       <meta charset="UTF-8">
       <title>系统登录-超市订单管理系统</title>
       <link type="text/css" rel="stylesheet" href="${pageContext.request.contextPath}/css/style.css">
       <script>
   
       </script>
   </head>
   <body class="login_bg">
       <section class="loginBox">
           <header class="loginHeader">
               <h1>超市订单管理系统</h1>
           </header>
           <section class="loginCont">
               <form class="loginForm" action="${pageContext.request.contextPath}/login.do" name="actionForm" id="actionForm" method="post">
                   <div class="info">${error}</div>
                   <div class="inputbox">
                       <label>用户名：</label>
                       <input type="text" class="input-text" id="userCode" name="userCode" placeholder="请输入用户名" required/>
                   </div>
                   <div class="inputbox">
                       <label>密码：</label>
                       <input type="password" id="userPassword" name="userPassword" placeholder="请输入密码" required/>
                   </div>
                   <div class="subBtn">
                       <input type="submit" value="登录"/>
                       <input type="reset" value="重置"/>
                   </div>
               </form>
           </section>
       </section>
   </body>
   </html>
   
   ```

```xml
<!--设置首页-->
    <welcome-file-list>
        <welcome-file>login.jsp</welcome-file>
    </welcome-file-list>
```

主页：`head.jsp `

```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/27
  Time: 19:57
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<%@ taglib prefix="fmt" uri="http://java.sun.com/jstl/fmt" %>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title>超市订单管理系统</title>
    <link type="text/css" rel="stylesheet" href="${pageContext.request.contextPath}/statics/css/style.css" />
    <link type="text/css" rel="stylesheet" href="${pageContext.request.contextPath}/statics/css/public.css" />
</head>
<body>
<!--头部-->
<header class="publicHeader">
    <h1>超市订单管理系统</h1>
    <div class="publicHeaderR">
        <p><span>下午好！</span><span style="color: #fff21b">${userSession.userName}</span> , 欢迎你！</p>
        <a href="${pageContext.request.contextPath }/logout.do">退出</a>
    </div>
</header>
<!--时间-->
<section class="publicTime">
    <span id="time">2015年1月1日 11:11  星期一</span>
    <a href="#">温馨提示：为了能正常浏览，请使用高版本浏览器！（IE10+）</a>
</section>
<!--主体内容-->
<section class="publicMian ">
    <div class="left">
        <h2 class="leftH2"><span class="span1"></span>功能列表 <span></span></h2>
        <nav>
            <ul class="list">
                <li ><a href="${pageContext.request.contextPath }/bill/billlist.html">订单管理</a></li>
                <li><a href="${pageContext.request.contextPath }/provider/providerlist.html">供应商管理</a></li>
                <li><a href="${pageContext.request.contextPath }/user/userlist.html">用户管理</a></li>
                <li><a href="${pageContext.request.contextPath }/jsp/pwdmodify.jsp">密码修改</a></li>
                <li><a href="${pageContext.request.contextPath }/role/rolelist.html">角色管理</a></li>
                <li><a href="${pageContext.request.contextPath }/logout.do">退出系统</a></li>
            </ul>
        </nav>
    </div>
    <input type="hidden" id="path" name="path" value="${pageContext.request.contextPath }"/>
    <input type="hidden" id="referer" name="referer" value="<%=request.getHeader("Referer")%>"/>


```

`frame.jsp`

```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/27
  Time: 19:57
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ include file="/jsp/common/head.jsp"%>
<div class="right">
    <img class="wColck" src="${pageContext.request.contextPath}/statics/images/clock.jpg" alt=""/>
    <div class="wFont">
        <h2>${userSession.userName}</h2>
        <p> 欢迎来到超市订单管理系统！</p>
    </div>
</div>
</section>
<%@ include file="/jsp/common/foot.jsp"%>

```

这里处理了一个大问题：</section>的位置是有特殊要求的！！！！

`foot.jsp`

```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/27
  Time: 19:57
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<footer class="footer">
    超市订单管理系统
</footer>
<script type="text/javascript" src="${pageContext.request.contextPath }/statics/js/time.js"></script>
<script type="text/javascript" src="${pageContext.request.contextPath }/statics/js/jquery-1.8.3.min.js"></script>
<script type="text/javascript" src="${pageContext.request.contextPath }/statics/js/common.js"></script>
<script type="text/javascript" src="${pageContext.request.contextPath }/statics/calendar/WdatePicker.js"></script>
</body>
</html>

```



### DAO层

1. 编写dao层登录用户登录的接口

```java
package com.wxy.dao.user;

import com.wxy.pojo.User;

import java.sql.Connection;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/27 - 01 - 27 - 12:45
 * @Description: com.wxy.dao.user
 * @version: 1.0
 */
public interface UserDao {
    //冲数据库中获取数据成员
    public User getLoginUser(Connection connection,String userCode);
}

```

2.编写dao层接口的实现类

```java
package com.wxy.dao.user;

import com.wxy.dao.BaseDao;
import com.wxy.pojo.User;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/27 - 01 - 27 - 12:48
 * @Description: com.wxy.dao.user
 * @version: 1.0
 */
public class UserDaoImpl implements UserDao {
    @Override
    public User getLoginUser(Connection connection, String userCode) {
        //准备三个对象
        PreparedStatement pstm = null;
        ResultSet rs = null;
        User user = null;
        //判断是否连接成功
        if(null != connection){
            String sql = "select * from smbms_user where userCode=?";
            Object[] params = {userCode};
            try {
                rs = BaseDao.execute(connection, pstm, rs, sql, params);
                if(rs.next()){
                    user = new User();
                    user.setId(rs.getInt("id"));
                    user.setUserCode(rs.getString("userCode"));
                    user.setUserName(rs.getString("userName"));
                    user.setUserPassword(rs.getString("userPassword"));
                    user.setGender(rs.getInt("gender"));
                    user.setBirthday(rs.getDate("birthday"));
                    user.setPhone(rs.getString("phone"));
                    user.setAddress(rs.getString("address"));
                    user.setUserRole(rs.getInt("userRole"));
                    user.setCreatedBy(rs.getInt("createdBy"));
                    user.setCreationDate(rs.getTimestamp("creationDate"));
                    user.setModifyBy(rs.getInt("modifyBy"));
                    user.setModifyDate(rs.getTimestamp("modifyDate"));
                }
                BaseDao.closeResource(null, pstm, rs);
            } catch (Exception e) {
                e.printStackTrace();
            }

        }
        return user;
    }
}

```

### Service层

1. Service业务层接口

```java
package com.wxy.service.user;

import com.wxy.pojo.User;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/27 - 01 - 27 - 12:59
 * @Description: com.wxy.service.user
 * @version: 1.0
 */
public interface UserService {
    //用户登录
    public User login(String userCode,String password);
}

```

2.Service业务层实现类

```java
package com.wxy.service.user;

import com.wxy.dao.BaseDao;
import com.wxy.dao.user.UserDao;
import com.wxy.dao.user.UserDaoImpl;
import com.wxy.pojo.User;
import org.junit.Test;

import java.sql.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/27 - 01 - 27 - 13:00
 * @Description: com.wxy.service.user
 * @version: 1.0
 */
public class UserServiceImpl implements UserService{

    //业务层会调用dao层，所以我们要引入Dao层
    private UserDao userDao;

    public UserServiceImpl(){
        userDao =new UserDaoImpl();
    }
    @Override
    public User login(String userCode,String userPassword) {
        // TODO Auto-generated method stub
        Connection connection = null;
        //通过业务层调用对应的具体数据库操作
        User user = null;
        try {
            connection = BaseDao.getConnection();
            user = userDao.getLoginUser(connection, userCode);
        } catch (Exception e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }finally{
            BaseDao.closeResource(connection, null, null);
        }

        //匹配密码
        if(null != user) {
            if (!user.getUserPassword().equals(userPassword)) {
                user = null;
            }
        }
        return user;
    }

    /*@Test
	public void test() {
		UserServiceImpl userService = new UserServiceImpl();
		String userCode = "admin";
		String userPassword = "12345678";
		User admin = userService.login(userCode, userPassword);
		System.out.println(admin.getUserPassword());

	}*/

}

```

### Servlet层

1. 编写Servlet

```java
package com.wxy.servlet.user;


import com.wxy.pojo.User;
import com.wxy.service.user.UserService;
import com.wxy.service.user.UserServiceImpl;
import com.wxy.util.Constants;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/27 - 01 - 27 - 15:42
 * @Description: com.wxy.servlet.user
 * @version: 1.0
 */
public class LoginServlet extends HttpServlet {
    //Servlet控制层，调用业务层代码

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("LoginServlet start!!============ " );
        //获取用户名和密码
        String userCode = req.getParameter("userCode");
        String userPassword = req.getParameter("userPassword");

        //调用service方法，进行用户匹配
        UserService userService = new UserServiceImpl();
        User user = userService.login(userCode,userPassword);

        if(null != user){//登录成功
            //放入session
            req.getSession().setAttribute(Constants.USER_SESSION,user);
            //页面跳转（frame.jsp）
            resp.sendRedirect("jsp/frame.jsp");
        }else{
            //页面跳转（login.jsp）带出提示信息--转发
            req.setAttribute("error", "用户名或密码不正确");
            req.getRequestDispatcher("login.jsp").forward(req,resp);
        }
    }

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doGet(req, resp);
    }
}
```

1. 注册Servlet

```xml
		<!--Servlet-->
    <servlet>
        <servlet-name>LoginServlet</servlet-name>
        <servlet-class>com.wxy.servlet.user.LoginServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>LoginServlet</servlet-name>
        <url-pattern>/login.do</url-pattern>
    </servlet-mapping>
```

1. 测试访问,保证以上功能可以成功

![image-20210127201448215](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127201448.png)

![image-20210127201500022](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127201500.png)

## 登录功能优化

注销功能
思路：移除session，返回登录页面

```java
package com.wxy.servlet.user;

import com.wxy.util.Constants;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/27 - 01 - 27 - 20:09
 * @Description: com.wxy.servlet.user
 * @version: 1.0
 */
public class LogoutServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //清除session
        req.getSession().removeAttribute(Constants.USER_SESSION);
        resp.sendRedirect(req.getContextPath()+"/login.jsp");//返回登录页面
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```

注册xml

```xml
<servlet>
    <servlet-name>LogoutServlet</servlet-name>
    <servlet-class>com.wxy.servlet.user.LogoutServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>LogoutServlet</servlet-name>
    <url-pattern>/logout.do</url-pattern>
  </servlet-mapping>
```

## 登录拦截优化

编写一个过滤器，并注册

```java
package com.wxy.filter;

import com.wxy.pojo.User;
import com.wxy.util.Constants;

import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/27 - 01 - 27 - 20:15
 * @Description: com.wxy.filter
 * @version: 1.0
 */
public class SysFilter implements Filter {

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        HttpServletRequest request =  (HttpServletRequest)servletRequest;
        HttpServletResponse response = (HttpServletResponse)servletResponse;

        //过滤器，从session中获取用户
        User user = (User)request.getSession().getAttribute(Constants.USER_SESSION);
        if(user == null) {//已经被移除或者注销了，或者未登录
            response.sendRedirect(request.getContextPath()+"/error.jsp");
        }else {
            filterChain.doFilter(servletRequest, servletResponse);
        }
    }

    @Override
    public void destroy() {

    }
}

```

注册xml

```xml
 <!-- 用户登录过滤器 -->
  <filter>
    <filter-name>SysFilter</filter-name>
    <filter-class>com.wxy.filter.SysFilter</filter-class>
  </filter>
  <filter-mapping>
    <filter-name>SysFilter</filter-name>
    <url-pattern>/jsp/*</url-pattern>
  </filter-mapping>

```

测试，登录，注销，权限，都要保证OK

## 密码修改

### 前端

1. 导入前端素材

`pwdmodify.jsp`

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@include file="/jsp/common/head.jsp" %>
<div class="right">
    <div class="location">
        <strong>你现在所在的位置是:</strong>
        <span>密码修改页面</span>
    </div>
    <div class="providerAdd">
        <form id="userForm" name="userForm" method="post" action="${pageContext.request.contextPath }/jsp/user.do">
            <input type="hidden" name="method" value="savepwd"/>
            <!--div的class 为error是验证错误，ok是验证成功-->
            <div class="info">${message}</div>
            <div class="">
                <label for="oldPassword">旧密码：</label>
                <input type="password" name="oldpassword" id="oldpassword" value="">
                <font color="red"></font>
            </div>
            <div>
                <label for="newPassword">新密码：</label>
                <input type="password" name="newpassword" id="newpassword" value="">
                <font color="red"></font>
            </div>
            <div>
                <label for="newPassword">确认新密码：</label>
                <input type="password" name="rnewpassword" id="rnewpassword" value="">
                <font color="red"></font>
            </div>
            <div class="providerAddBtn">
                <!--<a href="#">保存</a>-->
                <input type="button" name="save" id="save" value="保存" class="input-button">
            </div>
        </form>
    </div>
</div>
</section>
<%@include file="/jsp/common/foot.jsp" %>
<script type="text/javascript" src="${pageContext.request.contextPath }/statics/js/pwdmodify.js"></script>
```



```html
<li><a href="${pageContext.request.contextPath }/jsp/pwdmodify.jsp">密码修改</a></li>
```

1. 写项目，建议从底层向上写
   ![image-20210127204342186](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210127204342.png)

### Dao层

1. UserDao接口

```java
package com.wxy.dao.user;

import com.wxy.pojo.User;

import java.sql.Connection;
import java.sql.SQLException;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/27 - 01 - 27 - 12:45
 * @Description: com.wxy.dao.user
 * @version: 1.0
 */
public interface UserDao {
    /**
     * 修改当前用户密码
     * @param connection
     * @param id
     * @param pwd
     * @return
     * @throws Exception
     */
    public int updatePwd(Connection connection, int id, String pwd)throws Exception;
}

```

3.UserDao接口实现类

```java
@Override
    public int updatePwd(Connection connection, int id, String pwd)
            throws Exception {
        // TODO Auto-generated method stub
        int flag = 0;
        PreparedStatement pstm = null;
        if(connection != null){
            String sql = "update smbms_user set userPassword= ? where id = ?";
            Object[] params = {pwd,id};
            flag = BaseDao.execute(connection, pstm, sql, params);
            BaseDao.closeResource(null, pstm, null);
        }
        return flag;
    }

```

### Service层

1. UserService层

```java
public interface UserService {

     /**
     * 根据userId修改密码
     * @param id
     * @param pwd
     * @return
     */
    public boolean updatePwd(int id, String pwd);
}
```

1. UserService实现类

```java
 @Override
    public boolean updatePwd(int id, String pwd) {
        boolean flag = false;
        Connection connection = null;
        try {
            connection = BaseDao.getConnection();
            if (userDao.updatePwd(connection, id, pwd) > 0) {
                flag = true;
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            BaseDao.closeResource(connection, null, null);
        }
        return flag;
    }
```

### Servlet层

servlet记得实现复用，要提取出方法！
在 **dao层** 和 **service层** 自己写映射类和实现类
下面是 **servlet层** 的主体

```java
package com.wxy.servlet.user;

import com.alibaba.fastjson.JSONArray;
import com.mysql.jdbc.StringUtils;
import com.sun.javaws.HtmlOptions;
import com.wxy.pojo.User;
import com.wxy.service.user.UserService;
import com.wxy.service.user.UserServiceImpl;
import com.wxy.util.Constants;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import java.sql.SQLException;
import java.util.HashMap;
import java.util.Map;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/28 - 01 - 28 - 0:17
 * @Description: com.wxy.servlet.user
 * @version: 1.0
 */
public class UserServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // TODO 自动生成的方法存根
        String method = req.getParameter("method");
        System.out.println("method----> " + method);

        if(method != null && method.equals("savepwd")) {
            this.updatePwd(req, resp);
        }
        //实现复用~~~~~~
        // 想添加新的增删改查，直接用if(method != "savepwd" && method != null);
    }

    private void updatePwd(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {

        Object o = request.getSession().getAttribute(Constants.USER_SESSION);
        String newpassword = request.getParameter("newpassword");
        boolean flag = false;
        if(o != null && !StringUtils.isNullOrEmpty(newpassword)){
            UserService userService = new UserServiceImpl();
            flag = userService.updatePwd(((User)o).getId(),newpassword);
            if(flag){
                request.setAttribute(Constants.SYS_MESSAGE, "修改密码成功,请退出并使用新密码重新登录！");
                request.getSession().removeAttribute(Constants.USER_SESSION);//session注销
            }else{
                request.setAttribute(Constants.SYS_MESSAGE, "修改密码失败！");
            }
        }else{
            request.setAttribute(Constants.SYS_MESSAGE, "修改密码失败！");
        }
        request.getRequestDispatcher("pwdmodify.jsp").forward(request, response);
    }

  
}

```



注册xml

```xml
<servlet>
    <servlet-name>UserServlet</servlet-name>
    <servlet-class>com.wxy.servlet.user.UserServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>UserServlet</servlet-name>
    <url-pattern>/jsp/user.do</url-pattern>
  </servlet-mapping>
```



```xml
<!--  默认Session过期时间-->
  <session-config>
    <session-timeout>30</session-timeout>
  </session-config>
```



### 优化密码修改使用Ajax

1. 阿里巴巴的fastjson

```xml
<!-- https://mvnrepository.com/artifact/com.alibaba/fastjson -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.68</version>
</dependency>

```

1. 后台代码修改

导入阿里的包

```java
package com.wxy.servlet.user;

import com.alibaba.fastjson.JSONArray;
import com.mysql.jdbc.StringUtils;
import com.sun.javaws.HtmlOptions;
import com.wxy.pojo.User;
import com.wxy.service.user.UserService;
import com.wxy.service.user.UserServiceImpl;
import com.wxy.util.Constants;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import java.sql.SQLException;
import java.util.HashMap;
import java.util.Map;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/28 - 01 - 28 - 0:17
 * @Description: com.wxy.servlet.user
 * @version: 1.0
 */
public class UserServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // TODO 自动生成的方法存根
        String method = req.getParameter("method");
        System.out.println("method----> " + method);

        if(method != null && method.equals("savepwd")) {
            this.updatePwd(req, resp);
        }else if(method != null && method.equals("pwdmodify")){
            this.getPwdByUserId(req,resp);
        }
        //实现复用~~~~~~
        // 想添加新的增删改查，直接用if(method != "savepwd" && method != null);
    }

    private void updatePwd(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {

        Object o = request.getSession().getAttribute(Constants.USER_SESSION);
        String newpassword = request.getParameter("newpassword");
        boolean flag = false;
        if(o != null && !StringUtils.isNullOrEmpty(newpassword)){
            UserService userService = new UserServiceImpl();
            flag = userService.updatePwd(((User)o).getId(),newpassword);
            if(flag){
                request.setAttribute(Constants.SYS_MESSAGE, "修改密码成功,请退出并使用新密码重新登录！");
                request.getSession().removeAttribute(Constants.USER_SESSION);//session注销
            }else{
                request.setAttribute(Constants.SYS_MESSAGE, "修改密码失败！");
            }
        }else{
            request.setAttribute(Constants.SYS_MESSAGE, "修改密码失败！");
        }
        request.getRequestDispatcher("pwdmodify.jsp").forward(request, response);
    }

    private void getPwdByUserId(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        Object o = request.getSession().getAttribute(Constants.USER_SESSION);
        String oldpassword = request.getParameter("oldpassword");
        //万能的Map，一切东西都可以存放
        Map<String, String> resultMap = new HashMap<String, String>();

        if(null == o ){ //session过期了
            resultMap.put("result", "sessionerror");
        }else if(StringUtils.isNullOrEmpty(oldpassword)){//旧密码输入为空
            resultMap.put("result", "error");
        }else{
            String sessionPwd = ((User)o).getUserPassword();
            if(oldpassword.equals(sessionPwd)){
                resultMap.put("result", "true");
            }else{//旧密码输入不正确
                resultMap.put("result", "false");
            }
        }
        //想办法返回一个json值
        response.setContentType("application/json");
        PrintWriter outPrintWriter = response.getWriter();
        //alibab的JSONArray工具类，转换格式使用
//        ={key，value}  然后传递给前端  result
        outPrintWriter.write(JSONArray.toJSONString(resultMap));
        outPrintWriter.flush();
        outPrintWriter.close();
    }
}

```



## 用户管理实现

![image-20210128194259654](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210128194307.png)

1. 导入分页的工具类-PageSupport

```java
package com.wxy.util;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/28 - 01 - 28 - 19:43
 * @Description: com.wxy.util
 * @version: 1.0
 */
public class PageSupport {
    //当前页码-来自于用户输入
    private int currentPageNo = 1;

    //总数量（表）
    private int totalCount = 0;

    //页面容量
    private int pageSize = 0;

    //总页数-totalCount/pageSize（+1）
    private int totalPageCount = 1;

    public int getCurrentPageNo() {
        return currentPageNo;
    }
		//封装的特性：set中可以做一些安全性的判断！
    public void setCurrentPageNo(int currentPageNo) {
        if(currentPageNo > 0){
            this.currentPageNo = currentPageNo;
        }
    }

    public int getTotalCount() {
        return totalCount;
    }

    public void setTotalCount(int totalCount) {
        if(totalCount > 0){
            this.totalCount = totalCount;
            //设置总页数
            this.setTotalPageCountByRs();
        }
    }
    public int getPageSize() {
        return pageSize;
    }

    public void setPageSize(int pageSize) {
        if(pageSize > 0){
            this.pageSize = pageSize;
        }
    }

    public int getTotalPageCount() {
        return totalPageCount;
    }

    public void setTotalPageCount(int totalPageCount) {
        this.totalPageCount = totalPageCount;
    }

    public void setTotalPageCountByRs(){
        if(this.totalCount % this.pageSize == 0){
            this.totalPageCount = this.totalCount / this.pageSize;
        }else if(this.totalCount % this.pageSize > 0){
            this.totalPageCount = this.totalCount / this.pageSize + 1;
        }else{
            this.totalPageCount = 0;
        }
    }

}

```



2.用户列表页面导入-userlist.jsp

```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/28
  Time: 19:48
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@include file="/jsp/common/head.jsp"%>
<div class="right">
    <div class="location">
        <strong>你现在所在的位置是:</strong>
        <span>用户管理页面</span>
    </div>
    <div class="search">
        <form method="get" action="${pageContext.request.contextPath }/jsp/user.do">
            <input name="method" value="query" class="input-text" type="hidden">
            <span>用户名：</span>
            <input name="queryname" class="input-text"	type="text" value="${queryUserName }">

            <span>用户角色：</span>
            <select name="queryUserRole">
                <c:if test="${roleList != null }">
                    <option value="0">--请选择--</option>
                    <c:forEach var="role" items="${roleList}">
                        <option <c:if test="${role.id == queryUserRole }">selected="selected"</c:if>
                                value="${role.id}">${role.roleName}</option>
                    </c:forEach>
                </c:if>
            </select>

            <input type="hidden" name="pageIndex" value="1"/>
            <input	value="查 询" type="submit" id="searchbutton">
            <a href="${pageContext.request.contextPath}/jsp/useradd.jsp" >添加用户</a>
        </form>
    </div>
    <!--用户-->
    <table class="providerTable" cellpadding="0" cellspacing="0">
        <tr class="firstTr">
            <th width="10%">用户编码</th>
            <th width="20%">用户名称</th>
            <th width="10%">性别</th>
            <th width="10%">年龄</th>
            <th width="10%">电话</th>
            <th width="10%">用户角色</th>
            <th width="30%">操作</th>
        </tr>
        <c:forEach var="user" items="${userList }" varStatus="status">
            <tr>
                <td>
                    <span>${user.userCode }</span>
                </td>
                <td>
                    <span>${user.userName }</span>
                </td>
                <td>
							<span>
								<c:if test="${user.gender==1}">男</c:if>
								<c:if test="${user.gender==2}">女</c:if>
							</span>
                </td>
                <td>
                    <span>${user.age}</span>
                </td>
                <td>
                    <span>${user.phone}</span>
                </td>
                <td>
                    <span>${user.userRoleName}</span>
                </td>
                <td>
                    <span><a class="viewUser" href="javascript:;" userid=${user.id } username=${user.userName }><img src="${pageContext.request.contextPath }/statics/images/read.png" alt="查看" title="查看"/></a></span>
                    <span><a class="modifyUser" href="javascript:;" userid=${user.id } username=${user.userName }><img src="${pageContext.request.contextPath }/statics/images/xiugai.png" alt="修改" title="修改"/></a></span>
                    <span><a class="deleteUser" href="javascript:;" userid=${user.id } username=${user.userName }><img src="${pageContext.request.contextPath }/statics/images/schu.png" alt="删除" title="删除"/></a></span>
                </td>
            </tr>
        </c:forEach>
    </table>
    <input type="hidden" id="totalPageCount" value="${totalPageCount}"/>
    <c:import url="rollpage.jsp">
        <c:param name="totalCount" value="${totalCount}"/>
        <c:param name="currentPageNo" value="${currentPageNo}"/>
        <c:param name="totalPageCount" value="${totalPageCount}"/>
    </c:import>
</div>
</section>

<!--点击删除按钮后弹出的页面-->
<div class="zhezhao"></div>
<div class="remove" id="removeUse">
    <div class="removerChid">
        <h2>提示</h2>
        <div class="removeMain">
            <p>你确定要删除该用户吗？</p>
            <a href="#" id="yes">确定</a>
            <a href="#" id="no">取消</a>
        </div>
    </div>
</div>

<%@include file="/jsp/common/foot.jsp" %>
<script type="text/javascript" src="${pageContext.request.contextPath }/statics/js/userlist.js"></script>

```

3.页码jsp

```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/28
  Time: 19:52
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
    <script type="text/javascript">

    </script>
</head>
<body>
<div class="page-bar">
    <ul class="page-num-ul clearfix">
        <li>共${param.totalCount }条记录&nbsp;&nbsp; ${param.currentPageNo }/${param.totalPageCount }页</li>
        <c:if test="${param.currentPageNo > 1}">
            <a href="javascript:page_nav(document.forms[0],1);">首页</a>
            <a href="javascript:page_nav(document.forms[0],${param.currentPageNo-1});">上一页</a>
        </c:if>
        <c:if test="${param.currentPageNo < param.totalPageCount }">
            <a href="javascript:page_nav(document.forms[0],${param.currentPageNo+1 });">下一页</a>
            <a href="javascript:page_nav(document.forms[0],${param.totalPageCount });">最后一页</a>
        </c:if>
        &nbsp;&nbsp;
    </ul>
    <span class="page-go-form"><label>跳转至</label>
	     <input type="text" name="inputPage" id="inputPage" class="page-key" />页
	     <button type="button" class="page-btn" onClick='jump_to(document.forms[0],document.getElementById("inputPage").value)'>GO</button>
		</span>
</div>
</body>
<script type="text/javascript" src="${pageContext.request.contextPath }/statics/js/rollpage.js"></script>
</html>

```

![image-20210128195632448](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210128195632.png)

### 1、获取用户数量

#### Dao层

1. UserDao

```java
//根据用户名或者角色查询用户总数
/**
     * 通过条件查询-用户表记录数
     * @param connection
     * @param userName
     * @param userRole
     * @return
     * @throws Exception
     */
    public int getUserCount(Connection connection, String userName, int userRole)throws Exception;
```

1. UserDaoImpl

```java
//根据用户名或者角色来查询用户总数（最难理解的sql）
    @Override
    public int getUserCount(Connection connection, String userName, int userRole)
            throws Exception {
        // TODO Auto-generated method stub
        PreparedStatement pstm = null;
        ResultSet rs = null;
        int count = 0;
        if(connection != null){
            StringBuffer sql = new StringBuffer();
            sql.append("select count(1) as count from smbms_user u,smbms_role r where u.userRole = r.id");
//            存放sql参数
            List<Object> list = new ArrayList<Object>();
            if(!StringUtils.isNullOrEmpty(userName)){
                sql.append(" and u.userName like ?");
                list.add("%"+userName+"%");  //index：0
            }
            if(userRole > 0){
                sql.append(" and u.userRole = ?");
                list.add(userRole);            //index：1
            }
            //List转换为数组
            Object[] params = list.toArray();
            System.out.println("sql ----> " + sql.toString());
            rs = BaseDao.execute(connection, pstm, rs, sql.toString(), params);
            if(rs.next()){
                //从结果集中获得的最终的数量
                count = rs.getInt("count");
            }
            BaseDao.closeResource(null, pstm, rs);
        }
        return count;
    }
```

#### Service层

1. UserService

```java
/**
	 * 根据条件查询用户表记录数
	 * @param queryUserName
	 * @param queryUserRole
	 * @return
	 */
	public int getUserCount(String queryUserName, int queryUserRole);
```

1. UserServiceImpl

```java
//查询记录数
	@Override
	public int getUserCount(String queryUserName, int queryUserRole) {
		// TODO Auto-generated method stub
		Connection connection = null;
		int count = 0;
		System.out.println("queryUserName ---- > " + queryUserName);
		System.out.println("queryUserRole ---- > " + queryUserRole);
		try {
			connection = BaseDao.getConnection();
			count = userDao.getUserCount(connection, queryUserName,queryUserRole);
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}finally{
			BaseDao.closeResource(connection, null, null);
		}
		return count;
	}
```

![image-20210128202822511](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210128202822.png)

### 2、获取用户列表

#### Dao层

1.UserDao

```java
/**
	 * 通过条件查询-userList
	 * @param connection
	 * @param userName
	 * @param userRole
	 * @return
	 * @throws Exception
	 */
	public List<User> getUserList(Connection connection, String userName, int userRole, int currentPageNo, int pageSize)throws Exception;

```

1. UserDaoImpl

```java
@Override
    public List<User> getUserList(Connection connection, String userName, int userRole, int currentPageNo, int pageSize)
            throws Exception {
        // TODO Auto-generated method stub
        PreparedStatement pstm = null;
        ResultSet rs = null;
        List<User> userList = new ArrayList<User>();
        if(connection != null){
            StringBuffer sql = new StringBuffer();
            sql.append("select u.*,r.roleName as userRoleName from smbms_user u,smbms_role r where u.userRole = r.id");
            List<Object> list = new ArrayList<Object>();
            if(!StringUtils.isNullOrEmpty(userName)){
                sql.append(" and u.userName like ?");
                list.add("%"+userName+"%");
            }
            if(userRole > 0){
                sql.append(" and u.userRole = ?");
                list.add(userRole);
            }

            //在数据库中，分页使用 limit startIndex pageSize
            //当前页  （当前页-1）*页面大小
            //0,5    1   0    012345
            //6,5    2   5    26789
            //11,5   3   10
            sql.append(" order by creationDate DESC limit ?,?");
            currentPageNo = (currentPageNo-1)*pageSize;
            list.add(currentPageNo);
            list.add(pageSize);

            Object[] params = list.toArray();
            System.out.println("sql ----> " + sql.toString());
            rs = BaseDao.execute(connection, pstm, rs, sql.toString(), params);
            while(rs.next()){
                User _user = new User();
                _user.setId(rs.getInt("id"));
                _user.setUserCode(rs.getString("userCode"));
                _user.setUserName(rs.getString("userName"));
                _user.setGender(rs.getInt("gender"));
                _user.setBirthday(rs.getDate("birthday"));
                _user.setPhone(rs.getString("phone"));
                _user.setUserRole(rs.getInt("userRole"));
                _user.setUserRoleName(rs.getString("userRoleName"));
                userList.add(_user);
            }
            BaseDao.closeResource(null, pstm, rs);
        }
        return userList;
    }
```

#### Service层

1. UserService

```java
/**
	 * 根据条件查询用户列表
	 * @param queryUserName
	 * @param queryUserRole
	 * @return
	 */
	public List<User> getUserList(String queryUserName, int queryUserRole, int currentPageNo, int pageSize);
```

1. UserServiceImpl

```java
@Override
    public List<User> getUserList(String queryUserName, int queryUserRole, int currentPageNo, int pageSize) {
        // TODO Auto-generated method stub
        Connection connection = null;
        List<User> userList = null;
        System.out.println("queryUserName ---- > " + queryUserName);
        System.out.println("queryUserRole ---- > " + queryUserRole);
        System.out.println("currentPageNo ---- > " + currentPageNo);
        System.out.println("pageSize ---- > " + pageSize);
        try {
            connection = BaseDao.getConnection();
            userList = userDao.getUserList(connection, queryUserName,queryUserRole,currentPageNo,pageSize);
        } catch (Exception e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }finally{
            BaseDao.closeResource(connection, null, null);
        }
        return userList;
    }
```

### 3、获取角色列表

为了我们的职责统一，我们可以把**角色的操作**单独放在一个包中，和pojo类对应。。。

#### Dao层

1.RoleDao

```java
package com.wxy.dao.role;

import com.wxy.pojo.Role;

import java.sql.Connection;
import java.util.List;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/28 - 01 - 28 - 20:43
 * @Description: com.wxy.dao.role
 * @version: 1.0
 */
public interface RoleDao {
    public List<Role> getRoleList(Connection connection)throws Exception;
}

```

1. RoleDaoImpl

```java
package com.wxy.dao.role;

import com.wxy.dao.BaseDao;
import com.wxy.pojo.Role;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.util.ArrayList;
import java.util.List;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/28 - 01 - 28 - 20:44
 * @Description: com.wxy.dao.role
 * @version: 1.0
 */
public class RoleDaoImpl implements RoleDao{

    @Override
    public List<Role> getRoleList(Connection connection) throws Exception {
        PreparedStatement pstm = null;
        ResultSet rs = null;
        List<Role> roleList = new ArrayList<Role>();
        if(connection != null){
            String sql = "select * from smbms_role";
            Object[] params = {};
            rs = BaseDao.execute(connection, pstm, rs, sql, params);
            while(rs.next()){
                Role _role = new Role();
                _role.setId(rs.getInt("id"));
                _role.setRoleCode(rs.getString("roleCode"));
                _role.setRoleName(rs.getString("roleName"));
                roleList.add(_role);
            }
            BaseDao.closeResource(null, pstm, rs);
        }

        return roleList;
    }

}
```

#### Service层

1. RoleService

```java
package com.wxy.service.role;

import com.wxy.pojo.Role;

import java.util.List;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/28 - 01 - 28 - 20:45
 * @Description: com.wxy.service.role
 * @version: 1.0
 */
public interface RoleService {
    public List<Role> getRoleList();
}

```

1. RoleServiceImpl

```java
package com.wxy.service.role;

import com.wxy.dao.BaseDao;
import com.wxy.dao.role.RoleDao;
import com.wxy.dao.role.RoleDaoImpl;
import com.wxy.pojo.Role;

import java.sql.Connection;
import java.util.List;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/28 - 01 - 28 - 20:46
 * @Description: com.wxy.service.role
 * @version: 1.0
 */
public class RoleServiceImpl implements RoleService {

    private RoleDao roleDao;

    public RoleServiceImpl(){
        roleDao = new RoleDaoImpl();
    }

    @Override
    public List<Role> getRoleList() {
        Connection connection = null;
        List<Role> roleList = null;
        try {
            connection = BaseDao.getConnection();
            roleList = roleDao.getRoleList(connection);
        } catch (Exception e) {
            e.printStackTrace();
        }finally{
            BaseDao.closeResource(connection, null, null);
        }
        return roleList;
    }

}
```

![image-20210128205355198](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210128205355.png)



### 4、用户显示的Servlet

1. 获取用户前端的数据（查询）
2. 判断请求是否需要执行，看参数的值判断
3. 为了实现分页，需要计算出当前页面和总页面，页面大小…
4. 用户列表展示
5. 返回前端

```java
@Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // TODO 自动生成的方法存根
        String method = req.getParameter("method");
        System.out.println("method----> " + method);

        if(method != null && method.equals("savepwd")) {
            this.updatePwd(req, resp);
        }else if(method != null && method.equals("pwdmodify")){
            this.getPwdByUserId(req,resp);
        }else if(method != null && method.equals("query")){
            this.query(req, resp);
        }
        //实现复用~~~~~~
        // 想添加新的增删改查，直接用if(method != "savepwd" && method != null);
    }


private void query(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        //查询用户列表

        //从前端获取数据
        String queryUserName = request.getParameter("queryname");
        String temp = request.getParameter("queryUserRole");
        String pageIndex = request.getParameter("pageIndex");
        int queryUserRole = 0;

        //获取用户列表
        UserService userService = new UserServiceImpl();

        //第一次走页面一定是第一页,页面大小固定的
        //设置页面容量
        int pageSize = Constants.pageSize;
        //当前页码
        int currentPageNo = 1;
        /**
         * http://localhost:8090/SMBMS/userlist.do
         * ----queryUserName --NULL
         * http://localhost:8090/SMBMS/userlist.do?queryname=
         * --queryUserName ---""
         */
        System.out.println("queryUserName servlet--------"+queryUserName);
        System.out.println("queryUserRole servlet--------"+queryUserRole);
        System.out.println("query pageIndex--------- > " + pageIndex);
        if(queryUserName == null){
            queryUserName = "";
        }
        if(temp != null && !temp.equals("")){
            queryUserRole = Integer.parseInt(temp);//给查询赋值! 默认为0
        }
        if(pageIndex != null){
            try{
                currentPageNo = Integer.valueOf(pageIndex);
            }catch(NumberFormatException e){
                response.sendRedirect("error.jsp");
            }
        }

        //获取用户总数量（分页：上一页 下一页的情况）
        int totalCount	= userService.getUserCount(queryUserName,queryUserRole);
        //总页数支持
        PageSupport pages=new PageSupport();
        //设置当前页码
        pages.setCurrentPageNo(currentPageNo);
        //设置页总大小
        pages.setPageSize(pageSize);
        //设置页总数量
        pages.setTotalCount(totalCount);

        //控制首页和尾页
        int totalPageCount = pages.getTotalPageCount();

        if(currentPageNo < 1){  //显示第一页的东西
            currentPageNo = 1;
        }else if(currentPageNo > totalPageCount){//当前页面大于最后一页，让它为最后一页就行
            currentPageNo = totalPageCount;
        }

        List<User> userList = null;
        userList = userService.getUserList(queryUserName,queryUserRole,currentPageNo, pageSize);
        request.setAttribute("userList", userList);

        List<Role> roleList = null;
        RoleService roleService = new RoleServiceImpl();
        roleList = roleService.getRoleList();
        request.setAttribute("roleList", roleList);

        request.setAttribute("queryUserName", queryUserName);
        request.setAttribute("queryUserRole", queryUserRole);
        request.setAttribute("totalPageCount", totalPageCount);
        request.setAttribute("totalCount", totalCount);
        request.setAttribute("currentPageNo", currentPageNo);
        request.getRequestDispatcher("userlist.jsp").forward(request, response);
    }
```

![image-20210128211923092](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210128211923.png)



小黄鸭调试法：自言自语

**项目原理流程图：**
![项目原理流程图](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210129101856.png)

### 5.用户的增删改详的实现

#### 前端

useradd.jsp

```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/29
  Time: 10:55
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@include file="/jsp/common/head.jsp"%>

<div class="right">
    <div class="location">
        <strong>你现在所在的位置是:</strong>
        <span>用户管理页面 >> 用户添加页面</span>
    </div>
    <div class="providerAdd">
        <form id="userForm" name="userForm" method="post" action="${pageContext.request.contextPath }/jsp/user.do">
            <input type="hidden" name="method" value="add">
            <!--div的class 为error是验证错误，ok是验证成功-->
            <div>
                <label for="userCode">用户编码：</label>
                <input type="text" name="userCode" id="userCode" value="">
                <!-- 放置提示信息 -->
                <font color="red"></font>
            </div>
            <div>
                <label for="userName">用户名称：</label>
                <input type="text" name="userName" id="userName" value="">
                <font color="red"></font>
            </div>
            <div>
                <label for="userPassword">用户密码：</label>
                <input type="password" name="userPassword" id="userPassword" value="">
                <font color="red"></font>
            </div>
            <div>
                <label for="ruserPassword">确认密码：</label>
                <input type="password" name="ruserPassword" id="ruserPassword" value="">
                <font color="red"></font>
            </div>
            <div>
                <label >用户性别：</label>
                <select name="gender" id="gender">
                    <option value="1" selected="selected">男</option>
                    <option value="2">女</option>
                </select>
            </div>
            <div>
                <label for="birthday">出生日期：</label>
                <input type="text" Class="Wdate" id="birthday" name="birthday"
                       readonly="readonly" onclick="WdatePicker();">
                <font color="red"></font>
            </div>
            <div>
                <label for="phone">用户电话：</label>
                <input type="text" name="phone" id="phone" value="">
                <font color="red"></font>
            </div>
            <div>
                <label for="address">用户地址：</label>
                <input name="address" id="address"  value="">
            </div>
            <div>
                <label >用户角色：</label>
                <!-- 列出所有的角色分类 -->
                <select name="userRole" id="userRole"></select>
                <font color="red"></font>
            </div>
            <div class="providerAddBtn">
                <input type="button" name="add" id="add" value="保存" >
                <input type="button" id="back" name="back" value="返回" >
            </div>
        </form>
    </div>
</div>
</section>
<%@include file="/jsp/common/foot.jsp" %>
<script type="text/javascript" src="${pageContext.request.contextPath }/statics/js/useradd.js"></script>

```



```jsp

```

usermodify.jsp

```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/29
  Time: 11:01
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@include file="/jsp/common/head.jsp"%>
<div class="right">
    <div class="location">
        <strong>你现在所在的位置是:</strong>
        <span>用户管理页面 >> 用户修改页面</span>
    </div>
    <div class="providerAdd">
        <form id="userForm" name="userForm" method="post" action="${pageContext.request.contextPath }/jsp/user.do">
            <input type="hidden" name="method" value="modifyexe">
            <input type="hidden" name="uid" value="${user.id }"/>
            <div>
                <label for="userName">用户名称：</label>
                <input type="text" name="userName" id="userName" value="${user.userName }">
                <font color="red"></font>
            </div>
            <div>
                <label >用户性别：</label>
                <select name="gender" id="gender">
                    <c:choose>
                        <c:when test="${user.gender == 1 }">
                            <option value="1" selected="selected">男</option>
                            <option value="2">女</option>
                        </c:when>
                        <c:otherwise>
                            <option value="1">男</option>
                            <option value="2" selected="selected">女</option>
                        </c:otherwise>
                    </c:choose>
                </select>
            </div>
            <div>
                <label >出生日期：</label>
                <input type="text" Class="Wdate" id="birthday" name="birthday" value="${user.birthday }"
                       readonly="readonly" onclick="WdatePicker();">
                <font color="red"></font>
            </div>

            <div>
                <label >用户电话：</label>
                <input type="text" name="phone" id="phone" value="${user.phone }">
                <font color="red"></font>
            </div>
            <div>
                <label >用户地址：</label>
                <input type="text" name="address" id="address" value="${user.address }">
            </div>
            <div>
                <label >用户角色：</label>
                <!-- 列出所有的角色分类 -->
                <input type="hidden" value="${user.userRole }" id="rid" />
                <select name="userRole" id="userRole"></select>
                <font color="red"></font>
            </div>
            <div class="providerAddBtn">
                <input type="button" name="save" id="save" value="保存" />
                <input type="button" id="back" name="back" value="返回"/>
            </div>
        </form>
    </div>
</div>
</section>
<%@include file="/jsp/common/foot.jsp" %>
<script type="text/javascript" src="${pageContext.request.contextPath }/statics/js/usermodify.js"></script>
```

详情userview.jsp

```jsp
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/1/29
  Time: 11:03
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@include file="/jsp/common/head.jsp"%>
<div class="right">
    <div class="location">
        <strong>你现在所在的位置是:</strong>
        <span>用户管理页面 >> 用户信息查看页面</span>
    </div>
    <div class="providerView">
        <p><strong>用户编号：</strong><span>${user.userCode }</span></p>
        <p><strong>用户名称：</strong><span>${user.userName }</span></p>
        <p><strong>用户性别：</strong>
            <span>
            		<c:if test="${user.gender == 1 }">男</c:if>
					<c:if test="${user.gender == 2 }">女</c:if>
				</span>
        </p>
        <p><strong>出生日期：</strong><span>${user.birthday }</span></p>
        <p><strong>用户电话：</strong><span>${user.phone }</span></p>
        <p><strong>用户地址：</strong><span>${user.address }</span></p>
        <p><strong>用户角色：</strong><span>${user.userRoleName}</span></p>
        <div class="providerAddBtn">
            <input type="button" id="back" name="back" value="返回" >
        </div>
    </div>
</div>
</section>
<%@include file="/jsp/common/foot.jsp" %>
<script type="text/javascript" src="${pageContext.request.contextPath }/statics/js/userview.js"></script>

```



#### Dao层

1.UserDao

```java
/**
     * 增加用户信息
     * @param connection
     * @param user
     * @return
     * @throws Exception
     */
    public int add(Connection connection, User user)throws Exception;

    /**
     * 通过userId删除user
     * @param delId
     * @return
     * @throws Exception
     */
    public int deleteUserById(Connection connection, Integer delId)throws Exception;

    /**
     * 修改用户信息
     * @param connection
     * @param user
     * @return
     * @throws Exception
     */
    public int modify(Connection connection, User user)throws Exception;

    /**
     * 通过userId获取user
     * @param connection
     * @param id
     * @return
     * @throws Exception
     */
    public User getUserById(Connection connection, String id)throws Exception;
```



2.UserDaoImpl

```java
@Override
    public int add(Connection connection, User user) throws Exception {
        // TODO Auto-generated method stub
        PreparedStatement pstm = null;
        int updateRows = 0;
        if(null != connection){
            String sql = "insert into smbms_user (userCode,userName,userPassword," +
                    "userRole,gender,birthday,phone,address,creationDate,createdBy) " +
                    "values(?,?,?,?,?,?,?,?,?,?)";
            Object[] params = {user.getUserCode(),user.getUserName(),user.getUserPassword(),
                    user.getUserRole(),user.getGender(),user.getBirthday(),
                    user.getPhone(),user.getAddress(),user.getCreationDate(),user.getCreatedBy()};
            updateRows = BaseDao.execute(connection, pstm, sql, params);
            BaseDao.closeResource(null, pstm, null);
        }
        return updateRows;
    }

    @Override
    public int deleteUserById(Connection connection,Integer delId) throws Exception {
        // TODO Auto-generated method stub
        PreparedStatement pstm = null;
        int flag = 0;
        if(null != connection){
            String sql = "delete from smbms_user where id=?";
            Object[] params = {delId};
            flag = BaseDao.execute(connection, pstm, sql, params);
            BaseDao.closeResource(null, pstm, null);
        }
        return flag;
    }

    @Override
    public int modify(Connection connection, User user) throws Exception {
        // TODO Auto-generated method stub
        int flag = 0;
        PreparedStatement pstm = null;
        if(null != connection){
            String sql = "update smbms_user set userName=?,"+
                    "gender=?,birthday=?,phone=?,address=?,userRole=?,modifyBy=?,modifyDate=? where id = ? ";
            Object[] params = {user.getUserName(),user.getGender(),user.getBirthday(),
                    user.getPhone(),user.getAddress(),user.getUserRole(),user.getModifyBy(),
                    user.getModifyDate(),user.getId()};
            flag = BaseDao.execute(connection, pstm, sql, params);
            BaseDao.closeResource(null, pstm, null);
        }
        return flag;
    }

    @Override
    public User getUserById(Connection connection, String id) throws Exception {
        // TODO Auto-generated method stub
        User user = null;
        PreparedStatement pstm = null;
        ResultSet rs = null;
        if(null != connection){
            String sql = "select u.*,r.roleName as userRoleName from smbms_user u,smbms_role r where u.id=? and u.userRole = r.id";
            Object[] params = {id};
            rs = BaseDao.execute(connection, pstm, rs, sql, params);
            if(rs.next()){
                user = new User();
                user.setId(rs.getInt("id"));
                user.setUserCode(rs.getString("userCode"));
                user.setUserName(rs.getString("userName"));
                user.setUserPassword(rs.getString("userPassword"));
                user.setGender(rs.getInt("gender"));
                user.setBirthday(rs.getDate("birthday"));
                user.setPhone(rs.getString("phone"));
                user.setAddress(rs.getString("address"));
                user.setUserRole(rs.getInt("userRole"));
                user.setCreatedBy(rs.getInt("createdBy"));
                user.setCreationDate(rs.getTimestamp("creationDate"));
                user.setModifyBy(rs.getInt("modifyBy"));
                user.setModifyDate(rs.getTimestamp("modifyDate"));
                user.setUserRoleName(rs.getString("userRoleName"));
            }
            BaseDao.closeResource(null, pstm, rs);
        }
        return user;
    }
```



#### Service层

1.UserService

```java
 /**
     * 增加用户信息
     *
     * @param user
     * @return
     */
    public boolean add(User user);

    /**
     * 根据ID删除user
     *
     * @param delId
     * @return
     */
    public boolean deleteUserById(Integer delId);

    /**
     * 修改用户信息
     *
     * @param user
     * @return
     */
    public boolean modify(User user);

    /**
     * 根据userCode查询出User
     *
     * @param userCode
     * @return
     */
    public User selectUserCodeExist(String userCode);

    /**
     * 根据ID查找user
     *
     * @param id
     * @return
     */
    public User getUserById(String id);
```



2.UserServiceImpl

```java

@Override
    public boolean add(User user) {
        // TODO Auto-generated method stub

        boolean flag = false;
        Connection connection = null;
        try {
            connection = BaseDao.getConnection();
            connection.setAutoCommit(false);//开启JDBC事务管理
            int updateRows = userDao.add(connection,user);
            connection.commit();
            if(updateRows > 0){
                flag = true;
                System.out.println("add success!");
            }else{
                System.out.println("add failed!");
            }

        } catch (Exception e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
            try {
                System.out.println("rollback==================");
                connection.rollback();
            } catch (SQLException e1) {
                // TODO Auto-generated catch block
                e1.printStackTrace();
            }
        }finally{
            //在service层进行connection连接的关闭
            BaseDao.closeResource(connection, null, null);
        }
        return flag;
    }

    @Override
    public boolean deleteUserById(Integer delId) {
        // TODO Auto-generated method stub
        Connection connection = null;
        boolean flag = false;
        try {
            connection = BaseDao.getConnection();
            if(userDao.deleteUserById(connection,delId) > 0)
                flag = true;
        } catch (Exception e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }finally{
            BaseDao.closeResource(connection, null, null);
        }
        return flag;
    }

    @Override
    public boolean modify(User user) {
        // TODO Auto-generated method stub
        Connection connection = null;
        boolean flag = false;
        try {
            connection = BaseDao.getConnection();
            if(userDao.modify(connection,user) > 0)
                flag = true;
        } catch (Exception e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }finally{
            BaseDao.closeResource(connection, null, null);
        }
        return flag;
    }

    @Override
    public User getUserById(String id) {
        // TODO Auto-generated method stub
        User user = null;
        Connection connection = null;
        try{
            connection = BaseDao.getConnection();
            user = userDao.getUserById(connection,id);
        }catch (Exception e) {
            // TODO: handle exception
            e.printStackTrace();
            user = null;
        }finally{
            BaseDao.closeResource(connection, null, null);
        }
        return user;
    }

    @Override
    public User selectUserCodeExist(String userCode) {
        // TODO Auto-generated method stub
        Connection connection = null;
        User user = null;
        try {
            connection = BaseDao.getConnection();
            user = userDao.getLoginUser(connection, userCode);
        } catch (Exception e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }finally{
            BaseDao.closeResource(connection, null, null);
        }
        return user;
    }
```



#### Servlet层

```java
@Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // TODO 自动生成的方法存根
        String method = req.getParameter("method");
        System.out.println("method----> " + method);

        if (method != null && method.equals("add")) {
            //增加操作
            this.add(req, resp);
        } else if (method != null && method.equals("query")) {
            this.query(req, resp);
        } else if (method != null && method.equals("getrolelist")) {
            //this.getRoleList(req, resp);
        } else if (method != null && method.equals("ucexist")) {
            this.userCodeExist(req, resp);
        } else if (method != null && method.equals("deluser")) {
            this.delUser(req, resp);
        } else if (method != null && method.equals("view")) {
            this.getUserById(req, resp, "userview.jsp");
        } else if (method != null && method.equals("modify")) {
            this.getUserById(req, resp, "usermodify.jsp");
        } else if (method != null && method.equals("modifyexe")) {
            this.modify(req, resp);
        } else if (method != null && method.equals("pwdmodify")) {
            this.getPwdByUserId(req, resp);
        } else if (method != null && method.equals("savepwd")) {
            this.updatePwd(req, resp);
        }
        //实现复用~~~~~~
        // 想添加新的增删改查，直接用if(method != "savepwd" && method != null);
    }




private void add(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        System.out.println("add()================");
        String userCode = request.getParameter("userCode");
        String userName = request.getParameter("userName");
        String userPassword = request.getParameter("userPassword");
        String gender = request.getParameter("gender");
        String birthday = request.getParameter("birthday");
        String phone = request.getParameter("phone");
        String address = request.getParameter("address");
        String userRole = request.getParameter("userRole");

        User user = new User();
        user.setUserCode(userCode);
        user.setUserName(userName);
        user.setUserPassword(userPassword);
        user.setAddress(address);
        try {
            user.setBirthday(new SimpleDateFormat("yyyy-MM-dd").parse(birthday));
        } catch (ParseException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        user.setGender(Integer.valueOf(gender));
        user.setPhone(phone);
        user.setUserRole(Integer.valueOf(userRole));
        user.setCreationDate(new Date());
        user.setCreatedBy(((User) request.getSession().getAttribute(Constants.USER_SESSION)).getId());

        UserService userService = new UserServiceImpl();
        if (userService.add(user)) {
            response.sendRedirect(request.getContextPath() + "/jsp/user.do?method=query");
        } else {
            request.getRequestDispatcher("useradd.jsp").forward(request, response);
        }

    }

    private void delUser(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        String id = request.getParameter("uid");
        Integer delId = 0;
        try {
            delId = Integer.parseInt(id);
        } catch (Exception e) {
            // TODO: handle exception
            delId = 0;
        }
        HashMap<String, String> resultMap = new HashMap<String, String>();
        if (delId <= 0) {
            resultMap.put("delResult", "notexist");
        } else {
            UserService userService = new UserServiceImpl();
            if (userService.deleteUserById(delId)) {
                resultMap.put("delResult", "true");
            } else {
                resultMap.put("delResult", "false");
            }
        }

        //把resultMap转换成json对象输出
        response.setContentType("application/json");
        PrintWriter outPrintWriter = response.getWriter();
        outPrintWriter.write(JSONArray.toJSONString(resultMap));
        outPrintWriter.flush();
        outPrintWriter.close();
    }

    private void modify(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        String id = request.getParameter("uid");
        String userName = request.getParameter("userName");
        String gender = request.getParameter("gender");
        String birthday = request.getParameter("birthday");
        String phone = request.getParameter("phone");
        String address = request.getParameter("address");
        String userRole = request.getParameter("userRole");

        User user = new User();
        user.setId(Integer.valueOf(id));
        user.setUserName(userName);
        user.setGender(Integer.valueOf(gender));
        try {
            user.setBirthday(new SimpleDateFormat("yyyy-MM-dd").parse(birthday));
        } catch (ParseException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        user.setPhone(phone);
        user.setAddress(address);
        user.setUserRole(Integer.valueOf(userRole));
        user.setModifyBy(((User) request.getSession().getAttribute(Constants.USER_SESSION)).getId());
        user.setModifyDate(new Date());

        UserService userService = new UserServiceImpl();
        if (userService.modify(user)) {
            response.sendRedirect(request.getContextPath() + "/jsp/user.do?method=query");
        } else {
            request.getRequestDispatcher("usermodify.jsp").forward(request, response);
        }

    }

    private void getUserById(HttpServletRequest request, HttpServletResponse response, String url)
            throws ServletException, IOException {
        String id = request.getParameter("uid");
        if (!StringUtils.isNullOrEmpty(id)) {
            //调用后台方法得到user对象
            UserService userService = new UserServiceImpl();
            User user = userService.getUserById(id);
            request.setAttribute("user", user);
            request.getRequestDispatcher(url).forward(request, response);
        }

    }

    private void userCodeExist(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		//判断用户账号是否可用
		String userCode = request.getParameter("userCode");
		
		HashMap<String, String> resultMap = new HashMap<String, String>();
		if(StringUtils.isNullOrEmpty(userCode)){
			//userCode == null || userCode.equals("")
			resultMap.put("userCode", "exist");
		}else{
			UserService userService = new UserServiceImpl();
			User user = userService.selectUserCodeExist(userCode);
			if(null != user){
				resultMap.put("userCode","exist");
			}else{
				resultMap.put("userCode", "notexist");
			}
		}
		
		//把resultMap转为json字符串以json的形式输出
		//配置上下文的输出类型
		response.setContentType("application/json");
		//从response对象中获取往外输出的writer对象
		PrintWriter outPrintWriter = response.getWriter();
		//把resultMap转为json字符串 输出
		outPrintWriter.write(JSONArray.toJSONString(resultMap));
		outPrintWriter.flush();//刷新
		outPrintWriter.close();//关闭流
	}
	
		private void getRoleList(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
				List<Role> roleList = null;
				RoleService roleService = new RoleServiceImpl();
				roleList = roleService.getRoleList();
				//把roleList转换成json对象输出
				response.setContentType("application/json");
				PrintWriter outPrintWriter = response.getWriter();
				outPrintWriter.write(JSONArray.toJSONString(roleList));
				outPrintWriter.flush();
				outPrintWriter.close();
	}
```

