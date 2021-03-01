# GUI编程入门到游戏实战

# GUI编程

告诉大家怎么学？

这是什么？它怎么玩？该如何去在我们平时运用？class—可阅读

组件：

窗口、弹窗、面板、文本框、列表框、按钮、图片、监听事件、鼠标、键盘事件、破解工具

# 1.简介

GUI的核心：Swing AWT

缺点：1.界面不美观	2.需要jre环境！

为什么我们要学习？

1.可以写出自己心中想要的一些小工具

2.工作的时候，也可能需要维护到swing界面，概率极小!

3.了解MVC架构，了解监听!

# 2.AWT

## 2.1Awt介绍

1.包含很多类和接口！GUI

2.元素：窗口 按钮 文本框

![image-20210113103619161](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113103619161.png)

## 2.2组件和容器

### Frame

【1】GUI的第一个界面

```java
package com.kuang.lesson01;

import java.awt.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 10:21
 * @Description: com.kuang.lesson01
 * GUI的第一个界面
 * @version: 1.0
 */
public class TestFrame {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //Frame JDK 看源码
        Frame frame = new Frame("我的第一个Java图像界面窗口");

        //需要设置可见性
        frame.setVisible(true);
        //设置窗口大小
        frame.setSize(400,400);
        //设置背景颜色 Color
        frame.setBackground(new Color(0, 253, 223));
        //弹出的初始位置
        frame.setLocation(200,200);
        //设置大小固定
        frame.setResizable(false);
    }
}

```

![image-20210113103558080](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113103558080.png)

缺点:不可关闭 

解决：停止java运行

【2】多个Frame窗口的创建

```java
package com.kuang.lesson01;

import java.awt.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 10:32
 * @Description: com.kuang.lesson01
 * @version: 1.0
 */
public class TestFrame02 {
    public static void main(String[] args) {
        MyFrame myFrame1 = new MyFrame(Color.blue, 100, 100, 200, 200);
        MyFrame myFrame2 = new MyFrame(Color.yellow, 300, 100, 200, 200);
        MyFrame myFrame3 = new MyFrame(Color.red, 100, 300, 200, 200);
        MyFrame myFrame4 = new MyFrame(Color.orange, 300, 300, 200, 200);
    }
}

class MyFrame extends Frame {
    static  int id=0;       //可能存在多个窗口，我们需要一个计数器

    public MyFrame(Color color,int x,int y,int w,int h){
        super("Myframe+"+(++id));
        setBackground(color);
        setBounds(x,y,w,h);
        setVisible(true);

    }

}
```

![image-20210113103424321](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113103424321.png)

### 面板Panel

解决了窗口关闭的问题

```java
package com.kuang.lesson01;

import jdk.management.jfr.FlightRecorderMXBean;

import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 11:58
 * @Description: com.kuang.lesson01
 * @version: 1.0
 */
public class TestPanel {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Frame frame = new Frame();
        //布局的概念
        Panel panel = new Panel();

        //设置布局
        frame.setLayout(null);

        //坐标
        frame.setBackground(new Color(0xFFB700));
        frame.setBounds(300,400,500,600);

        //panel 坐标 相对于frame
        panel.setBackground(Color.BLUE);
        panel.setBounds(100,200,300,300);

        //frame.add(panel)
        frame.add(panel);
        frame.setVisible(true);
        
        //监听事件，监听窗口关闭事件  system.exit(0)关闭
        //适配器模式：adapted
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}

```

![image-20210113120448688](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113120448688.png)

可以关闭

### 布局管理器

- 流式布局
- 东西南北中
- 表格布局

#### 流式布局FlowLayout

```java
package com.kuang.lesson01;

import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 12:10
 * @Description: com.kuang.lesson01
 * @version: 1.0
 */
public class TestFlowLayout {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Frame frame = new Frame();

        //组件 button
        Button button1 = new Button("button1");
        Button button2 = new Button("button2");
        Button button3 = new Button("button3");

        //设置流式布局
        //frame.setLayout(new FlowLayout(FlowLayout.LEFT));//靠左
        //frame.setLayout(new FlowLayout(FlowLayout.RIGHT));//靠右
        frame.setLayout(new FlowLayout());//居中
        frame.setSize(200,200);
        //添加按钮
        frame.add(button1);
        frame.add(button2);
        frame.add(button3);
        //frame可视化
        frame.setVisible(true);
        //frame关闭
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                super.windowClosing(e);
                System.exit(0);
            }
        });
    }
}

```

![image-20210113121425475](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113121425475.png)

#### 东西南北中 BorderLayout

```java
package com.kuang.lesson01;

import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 12:17
 * @Description: com.kuang.lesson01
 * @version: 1.0
 */
public class TestBorderLayout {
    public static void main(String[] args) {
        Frame frame = new Frame("TestFlowLayout");

        Button earth = new Button("earth");
        Button west = new Button("west");
        Button south = new Button("south");
        Button north= new Button("north");
        Button center = new Button("center");


        frame.add(earth,BorderLayout.EAST);
        frame.add(west,BorderLayout.WEST);
        frame.add(south,BorderLayout.SOUTH);
        frame.add(north,BorderLayout.NORTH);
        frame.add(center,BorderLayout.CENTER);

        frame.setSize(200,200);
        frame.setVisible(true);

        //监听
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                super.windowClosing(e);
                System.exit(0);
            }
        });
    }
}

```

![image-20210113121820777](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113121820777.png)

#### 表格GridLayout

```java
package com.kuang.lesson01;

import java.awt.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 12:43
 * @Description: com.kuang.lesson01
 * @version: 1.0
 */
public class TestGridLayout {
    public static void main(String[] args) {
        Frame frame = new Frame("TestGridLayout");

        Button but1 = new Button("but1");
        Button but2 = new Button("but2");
        Button but3 = new Button("but3");
        Button but4 = new Button("but4");
        Button but5 = new Button("but5");
        Button but6 = new Button("but6");

        frame.setLayout(new GridLayout(3,2));

        frame.add(but1);
        frame.add(but2);
        frame.add(but3);
        frame.add(but4);
        frame.add(but5);
        frame.add(but6);

        frame.pack();//java函数 自动寻找适合布局
        frame.setVisible(true);

    }
}
```

![image-20210113124501145](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113124501145.png)

#### 练习题

![image-20210113124629941](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113124629941.png)

构思：1个 frame 2.4个面板 border 左button 中panel 右button

```java
package com.kuang.lesson01;

import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 12:52
 * @Description: com.kuang.lesson01
 * @version: 1.0
 */
public class ExDemo {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Frame frame = new Frame("课堂练习" );

        frame.setSize(100,200);
        frame.setLocation(100,100);
        frame.setBackground(new Color(0, 253, 149));


        frame.setLayout(new GridLayout(2,3));
        Panel p1 = new Panel(new BorderLayout());
        Panel p2 = new Panel(new GridLayout(2,1));
        Panel p3 = new Panel(new BorderLayout());
        Panel p4 = new Panel(new GridLayout(2,2));

        p1.add(new Button("EAST-1"),BorderLayout.EAST);
        p1.add(new Button("WEST-1"),BorderLayout.WEST);
        p2.add(new Button("p2-btn-1"));
        p2.add(new Button("p2-btn-2"));
        p1.add(p2,BorderLayout.CENTER);
        p3.add(new Button("EAST-2"),BorderLayout.EAST);
        p3.add(new Button("WEST-2"),BorderLayout.WEST);
        p4.add(new Button("p4-btn-1"));
        p4.add(new Button("p4-btn-2"));
        p4.add(new Button("p4-btn-3"));
        p4.add(new Button("p4-btn-4"));
        p3.add(p4,BorderLayout.CENTER);
        frame.add(p1);
        frame.add(p3);




        Button button3 = new Button("button3");
        Button button4 = new Button("button4");
        Button button5 = new Button("button5");
        Button button6 = new Button("button6");
        Button button7 = new Button("button7");
        Button button8 = new Button("button8");
        Button button9 = new Button("button9");
        Button button10 = new Button("button10");



        frame.pack();
        frame.setVisible(true);

        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                super.windowClosing(e);
                System.exit(0);
            }
        });
    }
}

```

![image-20210113130129624](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113130129624.png)

#### 总结

 1.frame是一个顶级窗口

 2.panel 无法单独显示，必须添加到某个容器

 3.布局管理器

 1.流式

 2.东西南北中

 3.表格

 4.大小、定位、背景颜色、可见性，监听！

## 2.3.事件监听ActionListener

事件监听：当某件事情发生的时候，干什么？

### 窗口关闭

```java
//方式一：监听事件，监听窗口关闭事件  system.exit(0)关闭
        //适配器模式：adapted
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });

//方式二：关闭窗口内部类
    private static void windowClose(Frame frame){
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                super.windowClosing(e);
                System.exit(0);
            }
        });
    }
```

### 按钮事件监听

```java
package com.kuang.lesson02;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 19:25
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class TestActionEvent {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Frame frame = new Frame();
        Button button = new Button();

        //因为，addActionListener()需要一个ActionListener,所以我们需要构造一个ActionListener
        MyActionListener myActionListener = new MyActionListener();
        button.addActionListener(myActionListener);

        frame.add(button,BorderLayout.CENTER);
        frame.pack();

        windowClose(frame);
        frame.setVisible(true);
    }
    //关闭窗口内部类
    private static void windowClose(Frame frame){
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                super.windowClosing(e);
                System.exit(0);
            }
        });
    }
}

//自定义的事件监听，实现了ActionListener接口
class MyActionListener implements ActionListener{

    @Override
    public void actionPerformed(ActionEvent actionEvent) {
        System.out.println("aaa");
    }
}
```

### 多个按钮共享一个监听

```java
package com.kuang.lesson02;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 19:32
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class TestActionEvent2 {
    public static void main(String[] args) {
        //两个按钮实现同一个监听
        //开始 停止
        Frame frame = new Frame("开始-停止");

        Button btn1 = new Button("start");
        Button btn2 = new Button("stop");;

        //可以显示的定义触发会返回的命令，如果不显式定义，则会走默认的值
        //可以多个按钮只写一个监听器
        btn1.setActionCommand("btn1-start");
        btn2.setActionCommand("btn1-stop");

        Mymonitor mymonitor = new Mymonitor();
        btn1.addActionListener(mymonitor);
        btn2.addActionListener(mymonitor);

        frame.add(btn1,BorderLayout.EAST);
        frame.add(btn2,BorderLayout.WEST);

        close(frame);

        frame.pack();
        frame.setVisible(true);


    }
    public static void close(Frame frame){
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}

class   Mymonitor implements ActionListener {
    @Override
    public void actionPerformed(ActionEvent e) {

        //getActionCommand()获得按钮信息
        System.out.println("按钮被执行了:msg=>"+e.getActionCommand());

        //选择执行特殊的方法
        if(e.getActionCommand().equals("btn1-start")){
            System.out.println("开始按钮");
        }
        if(e.getActionCommand().equals("btn1-stop")){
            System.out.println("结束按钮");
        }
    }
}
```

## 2.4输入框TextField

```java
package com.kuang.lesson02;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 19:49
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class TestText01 {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Frame frame=new MyFrame();
    }
}
class MyFrame extends Frame{
    public MyFrame(){
        TextField textField = new TextField();
        add(textField);

        //监听文本框输入的文字
        //按下回车 就会触发这个输入框的事件
        textField.addActionListener(new MyActionListener2());

        //设置替换编码，指像密码框一样**
        textField.setEchoChar('*');

        setVisible(true);
        pack();

        addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                super.windowClosing(e);
                System.exit(0);
            }
        });
    }
}
class MyActionListener2 implements ActionListener{

    @Override
    public void actionPerformed(ActionEvent e) {
        TextField field=(TextField)e.getSource();//获得一些资源
        System.out.println(field.getText());//获得输入框的文本
        field.setText("");//null
    }
}
```

![image-20210113195640975](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113195640975.png)

![image-20210113195658168](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113195658168.png)

## 2.5简易计算器 组合+内部类回顾

【1】oop原则：组合>继承

```java
package com.kuang.lesson02;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 20:12
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class TestCal {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Frame frame = new Calculator();
    }
}
class Calculator extends Frame{
    public Calculator() {
        //3个文本框
        TextField num1 = new TextField();
        TextField num2 = new TextField();
        TextField num3 = new TextField();
        //1个按钮
        Button button = new Button("=");
        button.addActionListener(new MyCalculatorListener(num1,num2,num3));

        //1个标签
        Label label = new Label("+");
        //布局
        setLayout(new FlowLayout());

        add(num1);
        add(label);
        add(num2);
        add(button);
        add(num3);

        pack();

        setVisible(true);
    }
}

//监听器类
class MyCalculatorListener implements ActionListener{

    //获取三个变量
    private  TextField num1,num2,num3;

    public MyCalculatorListener(TextField num1,TextField num2,TextField num3){
        this.num1 = num1;
        this.num2 = num2;
        this.num3 = num3;
    }
    @Override
    public void actionPerformed(ActionEvent actionEvent) {
        //1.获得加数与被加数
        int n1= Integer.parseInt(num1.getText());
        int n2= Integer.parseInt(num2.getText());
        //2.将两个数相加 放于第三个框
        num3.setText(""+(n1+n2));
        //3.清空前两个框
        num1.setText("");
        num2.setText("");
    }
}
```

【2】完全转为面向对象

```java
package com.kuang.lesson02;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 20:12
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class TestCal {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Calculator calculator = new Calculator();
        calculator.loadFrame();
    }
}
class Calculator extends Frame{

    //属性
    public   TextField num1,num2,num3;

    //方法
    public void loadFrame(){
        //3个文本框
        num1 = new TextField(10);
        num2 = new TextField(10);
        num3 = new TextField(20);
        //1个按钮
        Button button = new Button("=");
        button.addActionListener(new MyCalculatorListener(this));

        //1个标签
        Label label = new Label("+");
        //布局
        setLayout(new FlowLayout());

        add(num1);
        add(label);
        add(num2);
        add(button);
        add(num3);

        pack();

        setVisible(true);
        addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}

//监听器类
class MyCalculatorListener implements ActionListener{

    //
    Calculator calculator = null;
    public MyCalculatorListener(Calculator calculator){
        this.calculator = calculator;
    }
    @Override
    public void actionPerformed(ActionEvent e) {
        //1.获得加数与被加数
        int n1= Integer.parseInt(calculator.num1.getText());
        int n2= Integer.parseInt(calculator.num2.getText());
        //2.将两个数相加 放于第三个框
        calculator.num3.setText(""+(n1+n2));
        //3.清空前两个框
        calculator.num1.setText("");
        calculator.num2.setText("");
    }
}
```

【3】内部类

- 更好的包装

```java
package com.kuang.lesson02;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 20:12
 * @Description: com.kuang.lesson02
 * @version: 1.0
 */
public class TestCal {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Calculator calculator = new Calculator();
        calculator.loadFrame();
    }
}
class Calculator extends Frame{

    //属性
    public   TextField num1,num2,num3;

    //方法
    public void loadFrame(){
        //3个文本框
        num1 = new TextField(10);
        num2 = new TextField(10);
        num3 = new TextField(20);
        //1个按钮
        Button button = new Button("=");
        button.addActionListener(new MyCalculatorListener());

        //1个标签
        Label label = new Label("+");
        //布局
        setLayout(new FlowLayout());

        add(num1);
        add(label);
        add(num2);
        add(button);
        add(num3);

        pack();

        setVisible(true);
        addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }

    //监听器类写成内部类
    //内部类最大的优势可以畅通无阻的访问外部类
    class MyCalculatorListener implements ActionListener{

        @Override
        public void actionPerformed(ActionEvent e) {
            //1.获得加数与被加数
            int n1= Integer.parseInt(num1.getText());
            int n2= Integer.parseInt(num2.getText());
            //2.将两个数相加 放于第三个框
            num3.setText(""+(n1+n2));
            //3.清空前两个框
            num1.setText("");
            num2.setText("");
        }
    }
}


```

![image-20210113203657270](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113203657270.png)

![image-20210113203707682](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113203707682.png)

## 2.6画笔Paint

```java
package com.kuang.lesson03;

import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 20:41
 * @Description: com.kuang.lesson03
 * @version: 1.0
 */
public class TestPaint {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        MyPaint mypaint = new MyPaint();
        mypaint.loadFrame();
    }
}
class MyPaint extends Frame{
    public void loadFrame(){
        setBounds(200,300,400,500);
        setVisible(true);

        addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                super.windowClosing(e);
                System.exit(0);
            }
        });
    }

    public void paint(Graphics g){
        //选取颜色
        //画笔可以画画
        g.setColor(Color.BLUE);
        g.drawOval(100,100,100,100);
        g.fillOval(50,50,50,50);

        g.setColor(Color.green);
        g.drawRect(100,300,150,150);

        //养成习惯，画笔用完，将他还原为原来原色
        g.setColor(Color.BLACK);
    }
}

```

![image-20210113204720636](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113204720636.png)

## 2.7鼠标监听

目的：点击鼠标 画点

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201021145812382.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMjAzMjQ2,size_16,color_FFFFFF,t_70#pic_center)

```java
package com.kuang.lesson03;

import java.awt.*;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.awt.event.MouseListener;
import java.util.ArrayList;
import java.util.Iterator;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 21:11
 * @Description: com.kuang.lesson03
 * @version: 1.0
 */
public class TestMouseListener {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new MyFrame("画图");
    }
}
class MyFrame extends Frame{
    ArrayList points;
    //画画需要画笔 需要监听鼠标的位置，需要集合来储存这个点的位置
    public MyFrame(String title){
        super(title);
        setBounds(200,200,300,400);
        //存鼠标的点
        points = new ArrayList<>();
        //鼠标监听器 在Frame
        this.addMouseListener(new MyMouselListenner());

        setVisible(true);
    }

    @Override
    public void paint(Graphics g){
        //画画监听鼠标事件
        Iterator iterator = points.iterator();
        while(iterator.hasNext()){
            Point point = (Point) iterator.next();
            g.setColor(Color.BLUE);
            g.fillOval(point.x,point.y,10,10);
        }
    }

    //添加一个点到界面上
    public  void addPoint(Point point){
        //将点存入集合中
        points.add(point);

    }

    //适配器模式
    private  class MyMouselListenner extends MouseAdapter {
        // 鼠标 按下 弹起 按住不动
        @Override
        public void mousePressed(MouseEvent e) {
            MyFrame frame=(MyFrame)e.getSource();
            //我们点击的时候会产生一个点！frame.addpoint()没有方法 自己写
            //这个点就是鼠标的点
            frame.addPoint(new Point(e.getX(),e.getY()));
            //需要重画
            frame.repaint();

        }
    }
}
```

![image-20210113211935320](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113211935320.png)

## 2.8键盘监听

```java
package com.kuang.lesson03;

import java.awt.*;
import java.awt.event.KeyAdapter;
import java.awt.event.KeyEvent;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 21:20
 * @Description: com.kuang.lesson03
 * @version: 1.0
 */
public class TestKeyListener {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new KeyFrame();
    }
}

class KeyFrame extends Frame{
    public KeyFrame(){
        setBounds(10,10,100,200);
        setVisible(true);

        this.addKeyListener(new KeyAdapter() {
            @Override
            public void keyPressed(KeyEvent e) {
                int keycode = e.getKeyCode();
                System.out.println(keycode);
                if (keycode==KeyEvent.VK_UP){
                    System.out.println("你按了上键");
                }
                //根据按下不同操作，进行不同处理
            }
        });
    }

}
```

![image-20210113213328231](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113213328231.png)

## 2.9窗口监听

```java
package com.kuang.lesson03;

import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 21:01
 * @Description: com.kuang.lesson03
 * @version: 1.0
 */
public class TestWindowListener {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new MyWindowFrame();
    }
}
class MyWindowFrame extends Frame {
    public MyWindowFrame() {
        setBounds(100, 100, 200, 300);
        setBackground(Color.blue);
        setVisible(true);

        //addWindowListener(new MyWindowListener());
        this.addWindowListener(new WindowAdapter() {
            @Override
            public void windowOpened(WindowEvent e) {
                super.windowOpened(e);
            }

            @Override
            public void windowClosed(WindowEvent e) {
                super.windowClosed(e);
            }

            //激活窗口
            @Override
            public void windowActivated(WindowEvent e) {
                MyWindowFrame source =(MyWindowFrame) e.getSource();
                source.setTitle("被激活了");
                super.windowActivated(e);
            }

            @Override
            public void windowClosing(WindowEvent e) {
                super.windowClosing(e);
                System.exit(0);
            }
        });
    }
}

/*class MyWindowListener extends WindowAdapter{
        @Override
        public void windowClosing(WindowEvent e) {
            setVisible(false);//隐藏窗口 通过按钮 隐藏当前窗口
            System.exit(0);//正常退出，非正常推出1
        }
    }
}*/
```

# 3.Swing

## 3.1 窗口JFrame 面板

### 【1】测试

```java
package com.kuang.lesson04;

import javax.swing.*;
import java.awt.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 21:39
 * @Description: com.kuang.lesson04
 * @version: 1.0
 */
public class JFrameDemo01 {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new JFrameDemo01().init();
    }
    // init()初始化
    public void init(){
        JFrame jf = new JFrame("这是一个JFrame窗口");
        jf.setVisible(true);
        jf.setBounds(100,100,200,200);
        jf.setBackground(Color.cyan);
        //设置文字JLabel
        JLabel jLabel = new JLabel("欢迎来到王者荣耀");
        jf.add(jLabel);

        //关闭事件
        jf.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
}

```

![image-20210113215137024](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113215137024.png)

问题：init()初始化中不能对背景进行修改？

### 【2】测试解决方法：

```java
package com.kuang.lesson04;

import javax.swing.*;
import java.awt.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 22:08
 * @Description: com.kuang.lesson04
 * @version: 1.0
 */
public class JFrameDemo02 {
    public static void main(String[] args) {
        new MyJframe().init();
    }
}
class MyJframe extends JFrame {
    public void init(){
        this.setVisible(true);
        this.setBounds(10,10,200,200);

        JLabel jLabel = new JLabel("欢迎");
        this.add(jLabel);

        jLabel.setHorizontalAlignment(0);

        Container contentPane = this.getContentPane();//获得容器
        contentPane.setBackground(Color.BLUE);

        //关闭事件
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
}
```

![image-20210113221138155](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113221138155.png)

### 【3】文本居中

```java
//文本居中
jLabel.setHorizontalAlignment(0);
```



## 3.2弹窗Dialog

JDialog：默认就有关闭事件

```java
package com.kuang.lesson04;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/13 - 01 - 13 - 22:19
 * @Description: com.kuang.lesson04
 * @version: 1.0
 */
public class DialogDemo extends JFrame {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new DialogDemo();
    }
    public DialogDemo(){
        this.setVisible(true);
        this.setBounds(100,100,200,300);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

        //Jframe 放东西 容器
        Container container = this.getContentPane();
        //绝对布局
        container.setLayout(null);
        //按钮
        JButton jButton = new JButton("点击弹出一个弹窗");
        jButton.setBounds(30,30,200,50);
        //点击按钮会弹出一个弹窗
        jButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent actionEvent) {
                new MyDialog();
            }
        });

        //加入容器
        container.add(jButton);


    }
}

class MyDialog extends JDialog{
    public  MyDialog(){
        this.setVisible(true);
        this.setBounds(100,100,500,500);

        Container container =this.getContentPane();
        container.setLayout(null);
        Label label = new Label("我去");
        label.setBounds(100,100,100,100);
        container.add(label);
    }
}
```

![image-20210113223140904](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210113223140904.png)

## 3.3标签

### JLabel

```java
new JLabel("xxx")
```

### 图标 Icon

```java
package com.kuang.lesson04;

import javax.swing.*;
import java.awt.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 10:23
 * @Description: com.kuang.lesson04
 * @version: 1.0
 */
public class IconDemo extends JFrame implements Icon{
    private int width;
    private int height;

    //无参构造
    public IconDemo(){
    }

    //有参构造
    public IconDemo(int width, int height) throws HeadlessException {
        this.width = width;
        this.height = height;
    }

    public void init(){
        IconDemo iconDemo = new IconDemo(30,30);
        JLabel jLabel =new JLabel("小黑点",iconDemo,SwingConstants.CENTER);
        Container container = getContentPane();
        container.add(jLabel);
        this.setVisible(true);
        this.setBounds(100,100,200,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
    @Override
    public void paintIcon(Component component, Graphics graphics, int x, int y) {
        graphics.fillOval(x,y,height,width);
    }

    @Override
    public int getIconWidth() {
        return this.width;
    }

    @Override
    public int getIconHeight() {
        return this.height;
    }

    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new IconDemo().init();
    }
}

```

![image-20210114102943700](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114102943700.png)

### 图片Icon

```java
package com.kuang.lesson04;

import javax.swing.*;
import java.awt.*;
import java.net.URL;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 10:30
 * @Description: com.kuang.lesson04
 * @version: 1.0
 */
public class ImageIconDome extends JFrame {
    public ImageIconDome(){
        JLabel jLabel = new JLabel();
        URL url = ImageIconDome.class.getResource("photo.png");

        ImageIcon imageIcon = new ImageIcon(url);
        jLabel.setIcon(imageIcon);
        jLabel.setHorizontalAlignment(SwingConstants.CENTER);

        Container container =getContentPane();
        container.add(jLabel);

        setBounds(100,100,300,300);
        setVisible(true);
        setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new ImageIconDome();
    }
}

```

![image-20210114103619759](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114103619759.png)

## 3.4面板Jpanel

### 面板Jpanel

```java
package com.kuang.lesson05;

import javax.swing.*;
import java.awt.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 10:46
 * @Description: com.kuang.lesson05
 * @version: 1.0
 */
public class JpanelDemo extends JFrame {
    public JpanelDemo() {
        Container container = getContentPane();
        container.setLayout(new GridLayout(2, 2));

        JPanel panel1 = new JPanel(new GridLayout(2, 2));
        JPanel panel2 = new JPanel(new GridLayout(2, 1));
        JPanel panel3 = new JPanel(new GridLayout(3, 1));
        JPanel panel4 = new JPanel(new GridLayout(3, 2));

        panel1.add(new JButton("1"));
        panel1.add(new JButton("1"));
        panel1.add(new JButton("1"));
        panel1.add(new JButton("1"));
        panel2.add(new JButton("2"));
        panel2.add(new JButton("2"));
        panel3.add(new JButton("3"));
        panel3.add(new JButton("3"));
        panel3.add(new JButton("3"));
        panel4.add(new JButton("4"));
        panel4.add(new JButton("4"));
        panel4.add(new JButton("4"));
        panel4.add(new JButton("4"));
        panel4.add(new JButton("4"));
        panel4.add(new JButton("4"));

        container.add(panel1);
        container.add(panel2);
        container.add(panel3);
        container.add(panel4);
        this.setVisible(true);
        this.setSize(300, 500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new JpanelDemo();
    }
}

```

![image-20210114104746748](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114104746748.png)

### 滚动条JScroll

```java
package com.kuang.lesson05;

import javax.swing.*;
import java.awt.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 10:48
 * @Description: com.kuang.lesson05
 * @version: 1.0
 */
public class JscrollDemo extends JFrame {
    public  JscrollDemo(){
        JTextArea jTextArea = new JTextArea(30,50);
        jTextArea.setText("欢迎光临");

        //Scrollpanel
        JScrollPane jScrollPane =new JScrollPane(jTextArea);
        Container container = getContentPane();

        container.add(jScrollPane);

        this.setVisible(true);
        this.setBounds(100,200,300,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new JscrollDemo();
    }
}

```

![image-20210114105747076](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114105747076.png)

## 3.5按钮

### 普通按钮Jbutton

```java
package com.kuang.lesson05;

import com.kuang.lesson04.ImageIconDome;
import com.kuang.lesson04.JFrameDemo01;

import javax.swing.*;
import java.awt.*;
import java.net.URL;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 11:53
 * @Description: com.kuang.lesson05
 * @version: 1.0
 */
public class JbuttonDemo01 extends JFrame {
    public JbuttonDemo01(){
        Container container = getContentPane();

        URL url = ImageIconDome.class.getResource("photo.png");
        ImageIcon imageIcon = new ImageIcon(url);

        JButton jButton = new JButton();
        jButton.setIcon(imageIcon);
        jButton.setToolTipText("图片按钮");

        container.add(jButton);
        this.setVisible(true);
        this.setSize(300,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new JbuttonDemo01();
    }
}

```

![image-20210114115909140](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114115909140.png)

### 单选按钮 Jradiobutton

```java
package com.kuang.lesson05;

import com.kuang.lesson04.ImageIconDome;

import javax.swing.*;
import java.awt.*;
import java.net.URL;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 11:59
 * @Description: com.kuang.lesson05
 * @version: 1.0
 */
public class JbuttonDemo02 extends JFrame{
    public JbuttonDemo02(){
        Container container = getContentPane();

        URL url = ImageIconDome.class.getResource("photo.png");
        ImageIcon imageIcon = new ImageIcon(url);

        //单选框
        JRadioButton jRadioButton01 = new JRadioButton("jRadioButton01");
        JRadioButton jRadioButton02 = new JRadioButton("jRadioButton02");
        JRadioButton jRadioButton03 = new JRadioButton("jRadioButton03");
        //单选框 每次只能选一个 分组 group
        ButtonGroup buttonGroup = new ButtonGroup();
        buttonGroup.add(jRadioButton01);
        buttonGroup.add(jRadioButton02);
        buttonGroup.add(jRadioButton03);

        container.add(jRadioButton01,BorderLayout.CENTER);
        container.add(jRadioButton02,BorderLayout.NORTH);
        container.add(jRadioButton03,BorderLayout.SOUTH);


        this.setVisible(true);
        this.setSize(300,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new JbuttonDemo02();
    }
}

```

![image-20210114120336139](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114120336139.png)

### 复选按钮JcheckBox

```java
package com.kuang.lesson05;

import com.kuang.lesson04.ImageIconDome;

import javax.swing.*;
import java.awt.*;
import java.net.URL;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 11:59
 * @Description: com.kuang.lesson05
 * @version: 1.0
 */
public class JbuttonDemo03 extends JFrame{
    public JbuttonDemo03(){
        Container container = getContentPane();
        container.setLayout(new FlowLayout());

        URL url = ImageIconDome.class.getResource("photo.png");
        ImageIcon imageIcon = new ImageIcon(url);

        //多选框
        JCheckBox checkBox01 = new JCheckBox("工资");
        JCheckBox checkBox02 = new JCheckBox("头发");
        JCheckBox checkBox03 = new JCheckBox("感情");

        container.add(checkBox01);
        container.add(checkBox02);
        container.add(checkBox03);

        this.setVisible(true);
        this.setSize(300,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new JbuttonDemo03();
    }
}

```

![image-20210114120532796](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114120532796.png)

## 3.6列表

### 下拉框JcomboBox

```java
package com.kuang.lesson06;

import javax.swing.*;
import java.awt.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 15:36
 * @Description: com.kuang.lesson06
 * @version: 1.0
 */
public class TestComboBoxDemo extends JFrame {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new TestComboBoxDemo();
    }

    public TestComboBoxDemo(){
        Container container = getContentPane();

       //下拉框
        JComboBox jComboBox = new JComboBox();

        jComboBox.addItem(null);
        jComboBox.addItem("正在热映");
        jComboBox.addItem("已下架");
        jComboBox.addItem("即将上映");

        
        container.add(jComboBox);
        this.setVisible(true);
        this.setSize(300,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
}

```

![image-20210114153854382](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114153854382.png)

### 列表框JList

```java
package com.kuang.lesson06;

import javax.swing.*;
import java.awt.*;
import java.util.Vector;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 15:39
 * @Description: com.kuang.lesson06
 * @version: 1.0
 */
public class TestComboBoxDemo02 extends JFrame {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new TestComboBoxDemo02();
    }

    public TestComboBoxDemo02(){
        Container container = getContentPane();

        //列表框
        //String[] content={"1","2","3"};
        Vector vector = new Vector();
        JList jList = new JList(vector);

        vector.add("太清");
        vector.add("上清");
        vector.add("玉清");

        container.add(jList);

        this.setVisible(true);
        this.setSize(300,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
}


```

![image-20210114154104345](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114154104345.png)

应用场景

- 选择地区，或者一些单个选项
- 列表，展示信息，一般是动态扩容

## 3.7文本框

### 文本框JTextField

```java
package com.kuang.lesson06;

import javax.swing.*;
import java.awt.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 15:41
 * @Description: com.kuang.lesson06
 * @version: 1.0
 */
public class TestTextDemo01 extends JFrame {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new TestTextDemo01();
    }
    public TestTextDemo01(){
        Container container = this.getContentPane();
        //container.setLayout(null);

        //文本框
        JTextField textField = new JTextField("hello");

        JTextField textField02 = new JTextField("world");

        container.add(textField,BorderLayout.WEST);
        container.add(textField02,BorderLayout.EAST);

        this.setVisible(true);
        this.setSize(300,300);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
}

```

![image-20210114154315390](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114154315390.png)

### 密码框Jpasswordfield

```java
package com.kuang.lesson06;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 15:47
 * @Description: com.kuang.lesson06
 * @version: 1.0
 */
public class TestTextDemo02 extends JFrame {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new TestTextDemo02();
    }
    public TestTextDemo02(){
        Container container = this.getContentPane();
        //container.setLayout(null);

        //密码框
        JPasswordField jPasswordField = new JPasswordField();

        jPasswordField.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent actionEvent) {
                System.out.println(jPasswordField.getPassword());
            }
        });
        container.add(jPasswordField);
        this.setVisible(true);
        this.setSize(300,300);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
}

```

![image-20210114155020348](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114155020348.png)

### 文本域

```java
package com.kuang.lesson06;

import javax.swing.*;
import java.awt.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 15:47
 * @Description: com.kuang.lesson06
 * @version: 1.0
 */
public class TestTextDemo03 extends JFrame {
    public TestTextDemo03(){
        Container container = getContentPane();

        //文本框JTextArea
        JTextArea jTextArea = new JTextArea(30,50);
        jTextArea.setText("欢迎光临");
        //Scrollpanel
        JScrollPane jScrollPane =new JScrollPane(jTextArea);

        container.add(jScrollPane);

        this.setVisible(true);
        this.setBounds(100,200,300,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        new TestTextDemo03();
    }
}
```

![image-20210114155314132](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114155314132.png)

# 贪吃蛇

**帧** 如果时间片足够小，就是动画，一秒30帧，一秒60帧。连起来是动画，拆开静态是图片！

【1】游戏的主启动类StartGame

```java
package com.kuang.snake;

import javax.swing.*;
import java.awt.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 16:00
 * @Description: com.kuang.snake
 * 游戏的主启动类
 * @version: 1.0
 */
public class StartGame {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        JFrame jFrame = new JFrame();

        jFrame.setBounds(10,10,900,720);
        jFrame.setResizable(false);
        jFrame.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

        //正常游戏界面都应该在面上
				jFrame.add(new GamePanel());
        
        jFrame.setVisible(true);
    }
}

```

【2】

```java
package com.kuang.snake;

import javax.swing.*;
import java.awt.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 16:07
 * @Description: com.kuang.snake
 * @version: 1.0
 */
public class GamePanel extends JPanel {
    //

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);//
        this.setBackground(Color.BLACK);
    }
}

```

【3】图片数据

路径一定要放对

![image-20210114163811478](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114163811478.png)

【4】数据中心

```java
package com.kuang.snake;

import javax.swing.*;
import java.net.URL;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 16:13
 * @Description: com.kuang.snake
 *数据中心
 * @version: 1.0
 */
public class Data {
    //相对路径    tx.jpg
    //绝对路径   /   相当于当前的项目
    public static URL headerURL=Data.class.getResource("statics/header.png");
    public static ImageIcon header= new ImageIcon(headerURL);

    public static URL bodyURL=Data.class.getResource("statics/body.png");
    public static  ImageIcon body= new ImageIcon(bodyURL);

    public static URL upURL=Data.class.getResource("statics/up.png");
    public static  ImageIcon up= new ImageIcon(upURL);

    public static URL downURL=Data.class.getResource("statics/down.png");
    public static  ImageIcon down= new ImageIcon(downURL);
    public static URL rightURL=Data.class.getResource("statics/right.png");
    public static  ImageIcon right= new ImageIcon(rightURL);
    public static URL leftURL=Data.class.getResource("statics/left.png");
    public static  ImageIcon left= new ImageIcon(leftURL);
    public static URL foodURL=Data.class.getResource("statics/food.png");
    public static  ImageIcon food= new ImageIcon(foodURL);

}

```

【5】静态页面

```java
package com.kuang.snake;

import javax.swing.*;
import java.awt.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 16:07
 * @Description: com.kuang.snake
 * 游戏的面板
 * @version: 1.0
 */
public class GamePanel extends JPanel {
    //绘制面板，我们游戏中所有的东西，都是用这个画笔来画

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);//清屏
        //绘制静态的面板
        this.setBackground(Color.WHITE);
        Data.header.paintIcon(this,g,25,11);//将头部广告栏画上去
        g.fillRect(25,75,850,600);
    }
}

```

![image-20210114164007130](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114164007130.png)

【6】

```java
package com.kuang.snake;

import javax.swing.*;
import java.awt.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 16:07
 * @Description: com.kuang.snake
 * 游戏的面板
 * @version: 1.0
 */
public class GamePanel extends JPanel {

    //定义蛇的数据结构
    int length;     //蛇的长度
    int[] snakeX = new int[600];
    int[] snakeY = new int[600];

    public GamePanel(){
        this.init();
    }

    //初始化方法
    public void init(){
        length = 3;
        snakeX[0] =100; snakeY[0] =100;//脑袋的坐标
        snakeX[1] =75; snakeY[1] =100;
        snakeX[2] =50; snakeY[2] =100;

    }

    //绘制面板，我们游戏中所有的东西，都是用这个画笔来画

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);//清屏
        //绘制静态的面板
        this.setBackground(Color.WHITE);
        Data.header.paintIcon(this,g,25,11);//将头部广告栏画上去
        g.fillRect(25,75,850,600);

        //把小蛇画上去
        Data.right.paintIcon(this,g,snakeX[0],snakeY[0]);//蛇头初始化朝右

        for (int  i = 1;  i < length;  i++) {
            Data.body.paintIcon(this,g,snakeX[i],snakeY[i]);
        }
    }
}

```



![image-20210114165417651](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114165417651.png)

【7】添加游戏状态和标日

```java
package com.kuang.snake;

import javax.swing.*;
import java.awt.*;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 16:00
 * @Description: com.kuang.snake
 * 游戏的主启动类
 * @version: 1.0
 */
public class StartGame {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        JFrame jFrame = new JFrame();

        jFrame.setBounds(10,10,900,720);
        jFrame.setResizable(false);
        jFrame.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

        //正常游戏界面都应该在面上
        jFrame.add(new GamePanel());

        jFrame.setVisible(true);
    }
}

```

![image-20210114170318299](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114170318299.png)

【8】添加键盘监听

```java
package com.kuang.snake;

import javax.swing.*;
import java.awt.*;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 16:07
 * @Description: com.kuang.snake
 * 游戏的面板
 * @version: 1.0
 */
public class GamePanel extends JPanel implements KeyListener {

    //定义蛇的数据结构
    int length;     //蛇的长度
    int[] snakeX = new int[600];
    int[] snakeY = new int[600];
    String fx;  //方向
    //游戏当前的状态  开始  停止
    boolean isStart = false;


    public GamePanel() {
        this.init();
        //获得焦点和键盘事件
        this.setFocusable(true);
        this.addKeyListener(this);
    }

    //初始化方法
    public void init() {
        length = 3;
        snakeX[0] = 100;
        snakeY[0] = 100;//脑袋的坐标
        snakeX[1] = 75;
        snakeY[1] = 100;//第一节身体的坐标
        snakeX[2] = 50;
        snakeY[2] = 100;//第二节身体的坐标
        fx = "R";//初始方向向右

    }

    //绘制面板，我们游戏中所有的东西，都是用这个画笔来画

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);//清屏
        //绘制静态的面板
        this.setBackground(Color.WHITE);
        Data.header.paintIcon(this, g, 25, 11);//将头部广告栏画上去
        g.fillRect(25, 75, 850, 600);

        //把小蛇画上去
        if ("R".equals(fx)) {
            Data.right.paintIcon(this, g, snakeX[0], snakeY[0]);//蛇头初始化朝右
        } else if ("L".equals(fx)) {
            Data.left.paintIcon(this, g, snakeX[0], snakeY[0]);
        } else if ("U".equals(fx)) {
            Data.up.paintIcon(this, g, snakeX[0], snakeY[0]);
        } else if ("D".equals(fx)) {
            Data.down.paintIcon(this, g, snakeX[0], snakeY[0]);
        }

        for (int i = 1; i < length; i++) {
            Data.body.paintIcon(this, g, snakeX[i], snakeY[i]);
        }

        //游戏状态
        if (isStart == false) {
            g.setColor(Color.white);
            g.setFont(new Font("微软雅黑", Font.BOLD, 40));
            g.drawString("按下空格开始游戏", 300, 300);
        }
    }

    //键盘监听事件
    @Override
    public void keyPressed(KeyEvent e) {
        int keyCode = e.getKeyCode();
        if (keyCode == KeyEvent.VK_SPACE){
            isStart= !isStart;
            repaint();
        }
    }

    @Override
    public void keyTyped(KeyEvent keyEvent) {
    }

    @Override
    public void keyReleased(KeyEvent keyEvent) {
    }
}

```

【9】小蛇添加了ActionListener ，它可以动起来了，

```java
package com.kuang.snake;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 16:07
 * @Description: com.kuang.snake
 * 游戏的面板
 * @version: 1.0
 */
public class GamePanel extends JPanel implements KeyListener, ActionListener {

    //定义蛇的数据结构
    int length;     //蛇的长度
    int[] snakeX = new int[600];
    int[] snakeY = new int[600];
    String fx;  //方向
    //游戏当前的状态  开始  停止
    boolean isStart = false;

    //定时器
    Timer timer = new Timer(100,this);//100ms执行一次

    public GamePanel() {
        this.init();
        //获得焦点和键盘事件
        this.setFocusable(true);
        this.addKeyListener(this);
    }

    //初始化方法
    public void init() {
        length = 3;
        snakeX[0] = 100;
        snakeY[0] = 100;//脑袋的坐标
        snakeX[1] = 75;
        snakeY[1] = 100;//第一节身体的坐标
        snakeX[2] = 50;
        snakeY[2] = 100;//第二节身体的坐标
        fx = "R";//初始方向向右

        timer.start();

    }

    //绘制面板，我们游戏中所有的东西，都是用这个画笔来画

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);//清屏
        //绘制静态的面板
        this.setBackground(Color.WHITE);
        Data.header.paintIcon(this, g, 25, 11);//将头部广告栏画上去
        g.fillRect(25, 75, 850, 600);

        //把小蛇画上去
        if ("R".equals(fx)) {
            Data.right.paintIcon(this, g, snakeX[0], snakeY[0]);//蛇头初始化朝右
        } else if ("L".equals(fx)) {
            Data.left.paintIcon(this, g, snakeX[0], snakeY[0]);
        } else if ("U".equals(fx)) {
            Data.up.paintIcon(this, g, snakeX[0], snakeY[0]);
        } else if ("D".equals(fx)) {
            Data.down.paintIcon(this, g, snakeX[0], snakeY[0]);
        }

        for (int i = 1; i < length; i++) {
            Data.body.paintIcon(this, g, snakeX[i], snakeY[i]);
        }

        //游戏状态
        if (isStart == false) {
            g.setColor(Color.white);
            g.setFont(new Font("微软雅黑", Font.BOLD, 40));
            g.drawString("按下空格开始游戏", 300, 300);
        }
    }

    //键盘监听事件
    @Override
    public void keyPressed(KeyEvent e) {
        int keyCode = e.getKeyCode();
        if (keyCode == KeyEvent.VK_SPACE){
            isStart= !isStart;
            repaint();
        }
    }

    @Override
    public void keyTyped(KeyEvent keyEvent) {
    }

    @Override
    public void keyReleased(KeyEvent keyEvent) {
    }

    //事件监听----固定的时间刷新----定时器
    @Override
    public void actionPerformed(ActionEvent actionEvent) {
        if(isStart){    //如果是开始状态，就让小蛇动起来

            //右移
            for(int i=length-1;i>0;i--){    //后一节移到前一节的位置
                snakeX[i]=snakeX[i-1];
                snakeY[i]=snakeY[i-1];
            }
            snakeX[0] = snakeX[0]+25;

            //边界判断
            if(snakeX[0]>850){
                snakeX[0]=25;
            }


            //重画页面
            repaint();
        }
        timer.start();
    }
}

```

【10】小蛇动起来了

```java
package com.kuang.snake;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 16:07
 * @Description: com.kuang.snake
 * 游戏的面板
 * @version: 1.0
 */
public class GamePanel extends JPanel implements KeyListener, ActionListener {

    //定义蛇的数据结构
    int length;     //蛇的长度
    int[] snakeX = new int[600];
    int[] snakeY = new int[600];
    String fx;  //方向
    //游戏当前的状态  开始  停止
    boolean isStart = false;

    //定时器
    Timer timer = new Timer(100,this);//100ms执行一次

    public GamePanel() {
        this.init();
        //获得焦点和键盘事件
        this.setFocusable(true);
        this.addKeyListener(this);
    }

    //初始化方法
    public void init() {
        length = 3;
        snakeX[0] = 100;
        snakeY[0] = 100;//脑袋的坐标
        snakeX[1] = 75;
        snakeY[1] = 100;//第一节身体的坐标
        snakeX[2] = 50;
        snakeY[2] = 100;//第二节身体的坐标
        fx = "R";//初始方向向右

        timer.start();

    }

    //绘制面板，我们游戏中所有的东西，都是用这个画笔来画

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);//清屏
        //绘制静态的面板
        this.setBackground(Color.WHITE);
        Data.header.paintIcon(this, g, 25, 11);//将头部广告栏画上去
        g.fillRect(25, 75, 850, 600);

        //把小蛇画上去
        if ("R".equals(fx)) {
            Data.right.paintIcon(this, g, snakeX[0], snakeY[0]);//蛇头初始化朝右
        } else if ("L".equals(fx)) {
            Data.left.paintIcon(this, g, snakeX[0], snakeY[0]);
        } else if ("U".equals(fx)) {
            Data.up.paintIcon(this, g, snakeX[0], snakeY[0]);
        } else if ("D".equals(fx)) {
            Data.down.paintIcon(this, g, snakeX[0], snakeY[0]);
        }

        for (int i = 1; i < length; i++) {
            Data.body.paintIcon(this, g, snakeX[i], snakeY[i]);
        }

        //游戏状态
        if (isStart == false) {
            g.setColor(Color.white);
            g.setFont(new Font("微软雅黑", Font.BOLD, 40));
            g.drawString("按下空格开始游戏", 300, 300);
        }
    }

    //键盘监听事件
    @Override
    public void keyPressed(KeyEvent e) {
        int keyCode = e.getKeyCode();
        if (keyCode == KeyEvent.VK_SPACE){
            isStart= !isStart;
            repaint();
        }

        if(keyCode == KeyEvent.VK_RIGHT){
            fx="R";

        }else if(keyCode == KeyEvent.VK_LEFT){
            fx="L";

        }else if(keyCode == KeyEvent.VK_UP){
            fx="U";

        }else if(keyCode == KeyEvent.VK_DOWN){
            fx="D";

        }
    }

    @Override
    public void keyTyped(KeyEvent keyEvent) {
    }

    @Override
    public void keyReleased(KeyEvent keyEvent) {
    }

    //事件监听----固定的时间刷新----定时器
    @Override
    public void actionPerformed(ActionEvent actionEvent) {
        if(isStart){    //如果是开始状态，就让小蛇动起来

            //移动
            for(int i=length-1;i>0;i--){    //后一节移到前一节的位置
                snakeX[i]=snakeX[i-1];
                snakeY[i]=snakeY[i-1];
            }
            //走向
            if("R".equals(fx)){
                snakeX[0] = snakeX[0]+25;
                //边界判断
                if(snakeX[0]>850){
                    snakeX[0]=25;
                }
            }else if ("L".equals(fx)){
                snakeX[0] = snakeX[0]-25;
                //边界判断
                if(snakeX[0]<25){
                    snakeX[0]=850;
                }
            }else if ("U".equals(fx)){
                snakeY[0] = snakeY[0]-25;
                //边界判断
                if(snakeY[0]<75){
                    snakeY[0]=650;
                }
            }else if ("D".equals(fx)){
                snakeY[0] = snakeY[0]+25;
                //边界判断
                if(snakeY[0]>650){
                    snakeY[0]=75;
                }
            }


            //重画页面
            repaint();
        }
        timer.start();
    }
}

```

【11】食物添加

```java
package com.kuang.snake;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;
import java.util.Random;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 16:07
 * @Description: com.kuang.snake
 * 游戏的面板
 * @version: 1.0
 */
public class GamePanel extends JPanel implements KeyListener, ActionListener {

    //定义蛇的数据结构
    int length;     //蛇的长度
    int[] snakeX = new int[600];
    int[] snakeY = new int[600];
    String fx;  //方向
    //食物的坐标
    int foodX; int foodY;
    Random random = new Random();

    //游戏当前的状态  开始  停止
    boolean isStart = false;

    //定时器
    Timer timer = new Timer(100,this);//100ms执行一次

    public GamePanel() {
        this.init();
        //获得焦点和键盘事件
        this.setFocusable(true);
        this.addKeyListener(this);
    }

    //初始化方法
    public void init() {
        length = 3;
        snakeX[0] = 100;
        snakeY[0] = 100;//脑袋的坐标
        snakeX[1] = 75;
        snakeY[1] = 100;//第一节身体的坐标
        snakeX[2] = 50;
        snakeY[2] = 100;//第二节身体的坐标
        fx = "R";//初始方向向右

        //把食物随机分配在界面上！
        foodX = 25+25*random.nextInt(34);
        foodY = 75+25*random.nextInt(24);
        timer.start();

    }

    //绘制面板，我们游戏中所有的东西，都是用这个画笔来画

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);//清屏
        //绘制静态的面板
        this.setBackground(Color.WHITE);
        Data.header.paintIcon(this, g, 25, 11);//将头部广告栏画上去
        g.fillRect(25, 75, 850, 600);

        //把小蛇画上去
        if ("R".equals(fx)) {
            Data.right.paintIcon(this, g, snakeX[0], snakeY[0]);//蛇头初始化朝右
        } else if ("L".equals(fx)) {
            Data.left.paintIcon(this, g, snakeX[0], snakeY[0]);
        } else if ("U".equals(fx)) {
            Data.up.paintIcon(this, g, snakeX[0], snakeY[0]);
        } else if ("D".equals(fx)) {
            Data.down.paintIcon(this, g, snakeX[0], snakeY[0]);
        }

        for (int i = 1; i < length; i++) {
            Data.body.paintIcon(this, g, snakeX[i], snakeY[i]);
        }

        //画食物上去
        Data.food.paintIcon(this,g,foodX,foodY);

        //游戏状态
        if (isStart == false) {
            g.setColor(Color.white);
            g.setFont(new Font("微软雅黑", Font.BOLD, 40));
            g.drawString("按下空格开始游戏", 300, 300);
        }
    }

    //键盘监听事件
    @Override
    public void keyPressed(KeyEvent e) {
        int keyCode = e.getKeyCode();
        if (keyCode == KeyEvent.VK_SPACE){
            isStart= !isStart;
            repaint();
        }

        if(keyCode == KeyEvent.VK_RIGHT){
            fx="R";

        }else if(keyCode == KeyEvent.VK_LEFT){
            fx="L";

        }else if(keyCode == KeyEvent.VK_UP){
            fx="U";

        }else if(keyCode == KeyEvent.VK_DOWN){
            fx="D";

        }
    }

    @Override
    public void keyTyped(KeyEvent keyEvent) {
    }

    @Override
    public void keyReleased(KeyEvent keyEvent) {
    }

    //事件监听----固定的时间刷新----定时器
    @Override
    public void actionPerformed(ActionEvent actionEvent) {
        if(isStart){    //如果是开始状态，就让小蛇动起来

            //移动
            for(int i=length-1;i>0;i--){    //后一节移到前一节的位置
                snakeX[i]=snakeX[i-1];
                snakeY[i]=snakeY[i-1];
            }
            //走向
            if("R".equals(fx)){
                snakeX[0] = snakeX[0]+25;
                //边界判断
                if(snakeX[0]>850){
                    snakeX[0]=25;
                }
            }else if ("L".equals(fx)){
                snakeX[0] = snakeX[0]-25;
                //边界判断
                if(snakeX[0]<25){
                    snakeX[0]=850;
                }
            }else if ("U".equals(fx)){
                snakeY[0] = snakeY[0]-25;
                //边界判断
                if(snakeY[0]<75){
                    snakeY[0]=650;
                }
            }else if ("D".equals(fx)){
                snakeY[0] = snakeY[0]+25;
                //边界判断
                if(snakeY[0]>650){
                    snakeY[0]=75;
                }
            }

            //吃食物
            if(snakeX[0]==foodX&&snakeY[0]==foodY){
                length++;
                //再次随机食物
                foodX = 25+25*random.nextInt(34);
                foodY = 75+25*random.nextInt(24);

            }

            //重画页面
            repaint();
        }
        timer.start();
    }
}

```

【12】加入判断失败机制

```java
package com.kuang.snake;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;
import java.util.Random;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 16:07
 * @Description: com.kuang.snake
 * 游戏的面板
 * @version: 1.0
 */
public class GamePanel extends JPanel implements KeyListener, ActionListener {

    //定义蛇的数据结构
    int length;     //蛇的长度
    int[] snakeX = new int[600];
    int[] snakeY = new int[600];
    String fx;  //方向
    //食物的坐标
    int foodX;
    int foodY;
    Random random = new Random();

    //游戏当前的状态  开始  停止
    boolean isStart = false;
    //游戏失败的状态
    boolean isFail = false;
    

    //定时器
    Timer timer = new Timer(100, this);//100ms执行一次

    public GamePanel() {
        this.init();
        //获得焦点和键盘事件
        this.setFocusable(true);
        this.addKeyListener(this);
    }

    //初始化方法
    public void init() {
        length = 3;
        snakeX[0] = 100;
        snakeY[0] = 100;//脑袋的坐标
        snakeX[1] = 75;
        snakeY[1] = 100;//第一节身体的坐标
        snakeX[2] = 50;
        snakeY[2] = 100;//第二节身体的坐标
        fx = "R";//初始方向向右

        //把食物随机分配在界面上！
        foodX = 25 + 25 * random.nextInt(34);
        foodY = 75 + 25 * random.nextInt(24);
        
        timer.start();

    }

    //绘制面板，我们游戏中所有的东西，都是用这个画笔来画

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);//清屏
        //绘制静态的面板
        this.setBackground(Color.WHITE);
        Data.header.paintIcon(this, g, 25, 11);//将头部广告栏画上去
        g.fillRect(25, 75, 850, 600);

        //画积分
        g.setColor(Color.white);
        g.setFont(new Font("微软雅黑", Font.BOLD, 18));
        g.drawString("长度"+length, 750, 25);
        g.drawString("分数"+length, 750, 50);


        //画食物上去
        Data.food.paintIcon(this, g, foodX, foodY);

        //把小蛇画上去
        if ("R".equals(fx)) {
            Data.right.paintIcon(this, g, snakeX[0], snakeY[0]);//蛇头初始化朝右
        } else if ("L".equals(fx)) {
            Data.left.paintIcon(this, g, snakeX[0], snakeY[0]);
        } else if ("U".equals(fx)) {
            Data.up.paintIcon(this, g, snakeX[0], snakeY[0]);
        } else if ("D".equals(fx)) {
            Data.down.paintIcon(this, g, snakeX[0], snakeY[0]);
        }

        for (int i = 1; i < length; i++) {
            Data.body.paintIcon(this, g, snakeX[i], snakeY[i]);
        }


        //游戏状态
        if (isStart == false) {
            g.setColor(Color.white);
            g.setFont(new Font("微软雅黑", Font.BOLD, 40));
            g.drawString("按下空格开始游戏", 300, 300);
        }

        if (isFail) {
            g.setColor(Color.red);
            g.setFont(new Font("微软雅黑", Font.BOLD, 40));
            g.drawString("失败，按下空格重新开始游戏", 300, 300);
        }
    }

    //键盘监听事件
    @Override
    public void keyPressed(KeyEvent e) {
        int keyCode = e.getKeyCode();
        if (keyCode == KeyEvent.VK_SPACE) {
            if (isFail) {
                //重新开始
                isFail = false;
                init();
            } else {
                isStart = !isStart;
            }
            repaint();
        }

        if (keyCode == KeyEvent.VK_RIGHT) {
            fx = "R";

        } else if (keyCode == KeyEvent.VK_LEFT) {
            fx = "L";

        } else if (keyCode == KeyEvent.VK_UP) {
            fx = "U";

        } else if (keyCode == KeyEvent.VK_DOWN) {
            fx = "D";

        }
    }

    @Override
    public void keyTyped(KeyEvent keyEvent) {
    }

    @Override
    public void keyReleased(KeyEvent keyEvent) {
    }

    //事件监听----固定的时间刷新----定时器
    @Override
    public void actionPerformed(ActionEvent actionEvent) {
        if (isStart && isFail == false) {    //如果是开始状态，就让小蛇动起来

            //移动
            for (int i = length - 1; i > 0; i--) {    //后一节移到前一节的位置
                snakeX[i] = snakeX[i - 1];
                snakeY[i] = snakeY[i - 1];
            }
            //走向
            if ("R".equals(fx)) {
                snakeX[0] = snakeX[0] + 25;
                //边界判断
                if (snakeX[0] > 850) {
                    snakeX[0] = 25;
                }
            } else if ("L".equals(fx)) {
                snakeX[0] = snakeX[0] - 25;
                //边界判断
                if (snakeX[0] < 25) {
                    snakeX[0] = 850;
                }
            } else if ("U".equals(fx)) {
                snakeY[0] = snakeY[0] - 25;
                //边界判断
                if (snakeY[0] < 75) {
                    snakeY[0] = 650;
                }
            } else if ("D".equals(fx)) {
                snakeY[0] = snakeY[0] + 25;
                //边界判断
                if (snakeY[0] > 650) {
                    snakeY[0] = 75;
                }
            }

            //吃食物
            if (snakeX[0] == foodX && snakeY[0] == foodY) {
                length++;
                //再次随机食物
                foodX = 25 + 25 * random.nextInt(34);
                foodY = 75 + 25 * random.nextInt(24);

            }

            //失败判断，撞到自己就算失败
            for (int i = 1; i < length; i++) {
                if (snakeX[0]==snakeX[i]&&snakeY[0]==snakeY[i]){
                    isFail=true;
                }
            }

            //重画页面
            repaint();
        }
        timer.start();
    }
}

```



【13】加入评分机制

```java
package com.kuang.snake;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;
import java.util.Random;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/14 - 01 - 14 - 16:07
 * @Description: com.kuang.snake
 * 游戏的面板
 * @version: 1.0
 */
public class GamePanel extends JPanel implements KeyListener, ActionListener {

    //定义蛇的数据结构
    int length;     //蛇的长度
    int[] snakeX = new int[600];
    int[] snakeY = new int[600];
    String fx;  //方向
    //食物的坐标
    int foodX;
    int foodY;
    Random random = new Random();

    //游戏当前的状态  开始  停止
    boolean isStart = false;
    //游戏失败的状态
    boolean isFail = false;

    //成绩
    int score;

    //定时器
    Timer timer = new Timer(100, this);//100ms执行一次

    public GamePanel() {
        this.init();
        //获得焦点和键盘事件
        this.setFocusable(true);
        this.addKeyListener(this);
    }

    //初始化方法
    public void init() {
        length = 3;
        snakeX[0] = 100;
        snakeY[0] = 100;//脑袋的坐标
        snakeX[1] = 75;
        snakeY[1] = 100;//第一节身体的坐标
        snakeX[2] = 50;
        snakeY[2] = 100;//第二节身体的坐标
        fx = "R";//初始方向向右

        //把食物随机分配在界面上！
        foodX = 25 + 25 * random.nextInt(34);
        foodY = 75 + 25 * random.nextInt(24);

        score=0;
        timer.start();

    }

    //绘制面板，我们游戏中所有的东西，都是用这个画笔来画

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);//清屏
        //绘制静态的面板
        this.setBackground(Color.WHITE);
        Data.header.paintIcon(this, g, 25, 11);//将头部广告栏画上去
        g.fillRect(25, 75, 850, 600);

        //画积分
        g.setColor(Color.white);
        g.setFont(new Font("微软雅黑", Font.BOLD, 18));
        g.drawString("长度"+length, 750, 25);
        g.drawString("分数"+length, 750, 50);


        //画食物上去
        Data.food.paintIcon(this, g, foodX, foodY);

        //把小蛇画上去
        if ("R".equals(fx)) {
            Data.right.paintIcon(this, g, snakeX[0], snakeY[0]);//蛇头初始化朝右
        } else if ("L".equals(fx)) {
            Data.left.paintIcon(this, g, snakeX[0], snakeY[0]);
        } else if ("U".equals(fx)) {
            Data.up.paintIcon(this, g, snakeX[0], snakeY[0]);
        } else if ("D".equals(fx)) {
            Data.down.paintIcon(this, g, snakeX[0], snakeY[0]);
        }

        for (int i = 1; i < length; i++) {
            Data.body.paintIcon(this, g, snakeX[i], snakeY[i]);
        }


        //游戏状态
        if (isStart == false) {
            g.setColor(Color.white);
            g.setFont(new Font("微软雅黑", Font.BOLD, 40));
            g.drawString("按下空格开始游戏", 300, 300);
        }

        if (isFail) {
            g.setColor(Color.red);
            g.setFont(new Font("微软雅黑", Font.BOLD, 40));
            g.drawString("失败，按下空格重新开始游戏", 300, 300);
        }
    }

    //键盘监听事件
    @Override
    public void keyPressed(KeyEvent e) {
        int keyCode = e.getKeyCode();
        if (keyCode == KeyEvent.VK_SPACE) {
            if (isFail) {
                //重新开始
                isFail = false;
                init();
            } else {
                isStart = !isStart;
            }
            repaint();
        }

        if (keyCode == KeyEvent.VK_RIGHT) {
            fx = "R";

        } else if (keyCode == KeyEvent.VK_LEFT) {
            fx = "L";

        } else if (keyCode == KeyEvent.VK_UP) {
            fx = "U";

        } else if (keyCode == KeyEvent.VK_DOWN) {
            fx = "D";

        }
    }

    @Override
    public void keyTyped(KeyEvent keyEvent) {
    }

    @Override
    public void keyReleased(KeyEvent keyEvent) {
    }

    //事件监听----固定的时间刷新----定时器
    @Override
    public void actionPerformed(ActionEvent actionEvent) {
        if (isStart && isFail == false) {    //如果是开始状态，就让小蛇动起来

            //移动
            for (int i = length - 1; i > 0; i--) {    //后一节移到前一节的位置
                snakeX[i] = snakeX[i - 1];
                snakeY[i] = snakeY[i - 1];
            }
            //走向
            if ("R".equals(fx)) {
                snakeX[0] = snakeX[0] + 25;
                //边界判断
                if (snakeX[0] > 850) {
                    snakeX[0] = 25;
                }
            } else if ("L".equals(fx)) {
                snakeX[0] = snakeX[0] - 25;
                //边界判断
                if (snakeX[0] < 25) {
                    snakeX[0] = 850;
                }
            } else if ("U".equals(fx)) {
                snakeY[0] = snakeY[0] - 25;
                //边界判断
                if (snakeY[0] < 75) {
                    snakeY[0] = 650;
                }
            } else if ("D".equals(fx)) {
                snakeY[0] = snakeY[0] + 25;
                //边界判断
                if (snakeY[0] > 650) {
                    snakeY[0] = 75;
                }
            }

            //吃食物
            if (snakeX[0] == foodX && snakeY[0] == foodY) {
                length++;
               score=score+10;
                //再次随机食物
                foodX = 25 + 25 * random.nextInt(34);
                foodY = 75 + 25 * random.nextInt(24);

            }

            //失败判断，撞到自己就算失败
            for (int i = 1; i < length; i++) {
                if (snakeX[0]==snakeX[i]&&snakeY[0]==snakeY[i]){
                    isFail=true;
                }
            }

            //重画页面
            repaint();
        }
        timer.start();
    }
}

```

![image-20210114175858124](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210114175858124.png)

