# 多线程

# 1 多线程相关概念

介绍多线程之前要介绍线程，介绍线程则离不开进程。

首先 ，

**进程** ：是一个**正在执行中的程序**，每一个进程执行都有一个执行顺序，该顺序是一个执行路径，或者叫一个控制单元；

![image-20210110110255806](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210110110255806.png)

![image-20210110110228347](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210110110228347.png)

**线程**(轻量级进程（Light Weight Process）)：就是**进程**中的一个**独立控制单元**，也是CPU的基本调度单位,进程中的一条执行路径，线程在控制着进程的执行。一个进程中至少有一个进程。

多线程：一个进程由一个或多个线程组成，彼此阀完成不同的工作，同时执行。

| 迅雷           | 一个进程，当中的多个下载任务即是多个线程。                   |
| -------------- | ------------------------------------------------------------ |
| **Java虚拟机** | **一个进程,当中默认包含主线程(main),可通过代码创建多个独立线程,与main并发执行。** |



## 1.1 进程与线程

进程是指内存中运行的应用程序，每个进程都有一个独立的内存空间。

线程是进程中的一个执行路径，共享一个内存控件线程之间可以自由切换，并发执行。一个进程最少有一个线程。线程实际上是在进程基础之上的进一步划分，一个进程启动之后，里面的若干执行路径又可以划分成若干个线程。

进程之间不能共享数据段地址，但同进程的线程之间可以

**线程**的组成：

任何一个线程都具有基本的组成部分:
CPU时间片:       操作系统（OS）会为每个线程分配执行时间。

运行数据:

​			堆空间:存储线程需使用的对象，多个线程可以共享堆中的对象。

​			栈空间:存储线程需使用的局部变量，每个线程都拥有独立的栈。

**线程**的特点：

1、线程抢占式执行

​			效率高
​			可防止单一线程长时间独占CPU
2、在单核CPU中，宏观上同时执行（切换快），微观上顺序执行（实际上同一时间只有一个）。

**线程**的6种状态：

- NEW（未启动的线程）
- RUNNABLE（执行的线程）
- BLOCKED（被阻塞的线程）
- WAITING（无限期等待的线程）
- TIMED_WAITING（有限期等待的线程）
- TERMINATED（已结束的线程）

## 1.2 同步与异步

同步:排队执行 , 效率低但是安全.

异步:同时执行 , 效率高但是数据不安全.

## 1.3 并发与并行

并发是指两个或多个事件在同一个时间段内发生。

并发是指两个或多个事件在同一时刻发生（同时性）

# 2 线程的创建与实现

## 2.1 继承Thread类

启动线程的唯一方法是通过Thread类的实例方法start（） 该方法是一个native方法，它将启动一个新线程并执行run()方法。

```java
//自定义类继承Thread类
public class MyThread extends Thread{
  //重写run()方法
	public void run(){
    for(int i = 1;i<=50;i++){
		System.out.println(“hello world”+i);
    }
	}
}

```



```java
public class test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
				//创建自定义类对象
				MyThread t = new MyThread();
				//调用start()启动线程
				t.start();
    }
}
```

【2】

### 获取线程名称或线程ID

1、在Thread的子类中调用`this.getId()`或`this.getName ()`

2、使用静态方法`Thread.currentThread().getId()`和`Thread.currentThread().getName()`

```java
public class MyThread extends Thread{
    @Override
    public void run(){
        for(int i = 1;i<10000;i++){
            //第一种方式this.getId或者this.getName
            System.out.println(this.getId()+this.getName()+"子线程执行"+i);
            //第二种方式Thread.currentThread().getName()或者Thread.currentThread().getId()
            System.out.println(Thread.currentThread().getId()+Thread.currentThread().getName()+"子线程执行"+i);
        }
    }
}
```

【3】

### 修改线程名称,不能修改ID

 1、调用线程对象的setName()方法。

2、使用线程子类的构造方法赋值。

```java
public class MyThread extends Thread{
  //第二种使用线程子类的构造方法赋值
    public MyThread() {
    }

    public MyThread(String name) {
        super(name);
    }
}

public class test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //创建自定义类对象
      	//第二种使用线程子类的构造方法赋值
        MyThread t = new MyThread("子线程1");
      	//第一种线程对象的setName()方法
        t.setName("子线程1");
        //启动线程
        t.start();
    }
}
```

【4】案例代码

![image-20210110180452205](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210110180452205.png)

```java
package com.qf.chapter14_1;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/10 - 01 - 10 - 18:05
 * @Description: com.qf.chapter14_1
 * 卖票窗口
 * @version: 1.0
 */
public class TicketWin extends Thread {
    private int ticket=100;

    public TicketWin() {
    }

    public TicketWin(String name) {
        super(name);

    }

    @Override
    public void run() {
        //卖票功能
        while(true){
            if(ticket <=0){
                break;
            }
            System.out.println(Thread.currentThread().getName()+"卖了"+ticket+"张票");
            ticket--;
        }
    }
}

```

```java
package com.qf.chapter14_1;

import com.qf.chapter14_2.Ticket;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/10 - 01 - 10 - 18:15
 * @Description: com.qf.chapter14_1
 * @version: 1.0
 */
public class TestWin {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        TicketWin w1= new TicketWin("窗口1");
        TicketWin w2= new TicketWin("窗口2");
        TicketWin w3= new TicketWin("窗口3");
        TicketWin w4= new TicketWin("窗口4");
        //
        w1.start();
        w2.start();
        w3.start();
        w4.start();
    }
}

```



## 2.2 实现Runnable接口

【1】该方法通常比继承Thread的方法更常用，主要有以下原因：
（1） 如果一个类已经继承了一个类，则无法再继承Thread，可以避免单继承带来的局限性；
（2）任务与线程是分离的，提高了程序的健壮性；
（3）线程池技术，接受Runnable类型的任务，不接受Thread类型的线程.

```java
//创建自定义类实现Runnable接口
public class MyRunnable implements Runnable{		//1.实现Runnable接口
	//2.重写run()方法
	public void run(){
    for(int i = 1;i<=50;i++){
		System.out.println(“hello world”+i);
    }
	}
}

```



```java
public class test {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
				//3.创建类对象
      	MyRunnable mr = new MyRunnable();
      	//4.创建线程对象
				Thread t = new Thread(mr);
				//5.调用start()启动线程
				t.start();
    }
}
```

或者使用**匿名内部类**的方式

```java
//创建可运行对象
public class TestRunnable {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
      //创建可运行对象
        Runnable runnable = new Runnable(){
            @Override
            public void run() {
                for (int i = 1; i <= 50; i++) {
                    System.out.println("hello world" + i);
                }
            }
        };
        //创建线程对象
        Thread t = new Thread(runnable,"线程1");
        //调用start()启动线程
        t.start();
    }
}
```

【2】案例代码

![image-20210110174746107](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210110174746107.png)

```java
package com.qf.chapter14_2;

import java.sql.SQLOutput;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/10 - 01 - 10 - 17:27
 * @Description: com.qf.chapter14_2
 * 票类（线程类）
 * @version: 1.0
 */
public class Ticket implements Runnable{
    private  int ticket = 100;

    @Override
    public void run() {
        while(true){
            if(ticket<=0){
                break;
            }
            System.out.println(Thread.currentThread().getName()+"卖了第"+ticket+"张票");
            ticket--;
        }
    }
}

```

```java
package com.qf.chapter14_2;

import com.mashibing.MyThread;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/10 - 01 - 10 - 17:30
 * @Description: com.qf.chapter14_2
 * @version: 1.0
 */
public class TestTicket {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
    //1.新建进程
    Ticket ticket = new Ticket();
    //2.创建进程
    Thread w1 = new Thread(ticket,"窗口1");
    Thread w2 = new Thread(ticket,"窗口2");
    Thread w3 = new Thread(ticket,"窗口3");
    Thread w4 = new Thread(ticket,"窗口4");
    
    //3.启动进程
    w1.start();
    w2.start();
    w3.start();
    w4.start();

    }
}

```

![image-20210110174801794](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210110174801794.png)

```java
package com.qf.chapter14_2;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/10 - 01 - 10 - 17:48
 * @Description: com.qf.chapter14_2
 * 银行卡
 * @version: 1.0
 */
public class BankCard {
    private  double money;

    public double getMoney() {
        return money;
    }

    public void setMoney(double money) {
        this.money = money;
    }
}

```

```java
package com.qf.chapter14_2;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/10 - 01 - 10 - 17:49
 * @Description: com.qf.chapter14_2
 * 存钱进程
 * @version: 1.0
 */
public class Addmoney implements Runnable{
    private BankCard card;
    public Addmoney(BankCard card){
        this.card=card;
    }
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            card.setMoney(card.getMoney()+1000);
            System.out.println(Thread.currentThread().getName()+"存了1000块，余额是"+card.getMoney()+"块钱");
        }
    }
}

```

```java
package com.qf.chapter14_2;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/10 - 01 - 10 - 17:49
 * @Description: com.qf.chapter14_2
 * 取钱进程
 * @version: 1.0
 */
public class Submoney implements Runnable{
    private BankCard card;
    public Submoney(BankCard card){
        this.card=card;
    }
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            if (card.getMoney()>=1000){card.setMoney(card.getMoney()-1000);
                System.out.println(Thread.currentThread().getName()+"取了1000块，余额是"+card.getMoney()+"块钱");
            }
            else{
                System.out.println("余额不足，请存钱");
                i--;
            }

        }
    }
}

```

```java
package com.qf.chapter14_2;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/10 - 01 - 10 - 17:55
 * @Description: com.qf.chapter14_2
 * @version: 1.0
 */
public class TestBankCard {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //1.创建一张银行卡
        BankCard card = new BankCard();
        //2.创建存钱取钱
        Addmoney add = new Addmoney(card);
        Submoney sub = new Submoney(card);
        //3创建两个进程
        Thread chenchen = new Thread(add, "晨晨");
        Thread bingbing = new Thread(sub, "冰冰");
        //启动进程
        chenchen.start();
        bingbing.start();

    }

}
```



## 2.3有返回值的线程(Callable 接口)

【1】有返回值的任务必须实现 Callable 接口，类似的，无返回值的任务必须 实现Runnable 接口。执行Callable 任务后，可以获取一个 Future 的对象，在该对象上调用 get 就可以获取到 Callable 任务返回的 Object 了，再结合线程池口 ExecutorService 就可以实现有返回结果的多线程了。
实现步骤如下：
（1） 编写类实现Callable接口，实现接口中的方法；

```java
package com.qf.chapter14_8;
public static void main(String[] args) throws Exception{
		//功能需求：使用Callable实现1-100和
		//1创建Callable对象
		Callable<Integer> callable=new Callable<Integer>() {
			@Override
			public Integer call() throws Exception {
				System.out.println(Thread.currentThread().getName()+"开始计算");
				int sum=0;
				for(int i=1;i<=100;i++) {
					sum+=i;
					Thread.sleep(100);
				}
				return sum;
			}
		};
}
```

（2） 把Callable对象转成可执行任务，创建FutureTask对象，并传入第一步编写的Callable对象；

```java
//2把Callable对象 转成可执行任务
FutureTask<Integer> task=new FutureTask<>(callable);
```

3） 通过Thread启动线程；

```java
		//3创建线程
		Thread thread=new Thread(task);
		
		//4启动线程
		thread.start();
		
		//5获取结果(等待call执行完毕，才会返回)
		Integer sum=task.get();     						//get()
		System.out.println("结果是:"+sum);
```

【2】Callable和Runnable接口的区别

- (1)Callable接口中call方法有返回值,Runnable接口中run方法没有返回值
- (2)Callable接口中call方法有声明异常，Runnable接口中run方法没有异常

【3】Callable结合线程池来使用

```java
package com.qf.chapter14_8;

import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

/**
 * 使用线程池计算1-100的和
 * @author wgy
 *
 */
public class Demo3 {
	public static void main(String[] args) throws Exception{
		//1创建线程池
		ExecutorService es=Executors.newFixedThreadPool(1);
    
		//2提交任务 Future:表示将要执行完任务的结果                    //引入future
		Future<Integer> future=es.submit(new Callable<Integer>() {

			@Override
			public Integer call() throws Exception {
				System.out.println(Thread.currentThread().getName()+"开始计算");
				int sum=0;
				for(int i=1;i<=100;i++) {
					sum+=i;
					Thread.sleep(10);
				}
				return sum;
			}
		});
		
		//3获取任务结果,等待任务执行完毕才会返回.
		System.out.println(future.get());            //引入future
		
		//4关闭线程池
		es.shutdown();
		
	}
}

```

【4】

### Future接口

表示将要执行完任务的结果,即`ExecutorService.submit()`所返回的状态结果，就是**call()的返回值**
方法:` V get()`以阻塞形式等待Future中的**异步处理结果**(call()的返回值)

```java
package com.qf.chapter14_8;

import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import java.util.concurrent.locks.Lock;

/**
 * 使用两个线程，并发计算1~50、51~100的和，再进行汇总统计。
 * @author wgy
 *
 */
public class Demo4 {
	public static void main(String[] args) throws Exception{
		//1创建线程池
		ExecutorService es=Executors.newFixedThreadPool(2);
    
		//2.1提交任务
		Future<Integer> future1=es.submit(new Callable<Integer>() {
			@Override
			public Integer call() throws Exception {
				int sum=0;
				for(int i=1;i<=50;i++) {
					sum+=i;
				}
				System.out.println("1-50计算完毕");
				return sum;
			}
		});
    //2.2提交任务
		Future<Integer> future2=es.submit(new Callable<Integer>() {

			@Override
			public Integer call() throws Exception {
				int sum=0;
				for(int i=51;i<=100;i++) {
					sum+=i;
				}
				System.out.println("51-100计算完毕");
				return sum;
			}
		});
    
		//3获取结果
		int sum=future1.get()+future2.get();
		System.out.println("结果是:"+sum);
		//4关闭线程池
    
		es.shutdown();
	
	}
}

```



## 2.4 线程池实现多线程

如果并发的线程数量很多，并且每个线程都是执行一个时间很短的任务就结束了，这样频繁创建线程就会大大降低 系统的效率，因为频繁创建线程和销毁线程需要时间. 线程池就是一个容纳多个线程的容器，池中的线程可以反复使用，省去了频繁创建线程对象的操作，节省了大量的时间和资源。线程池有以下优点：（1） 降低资源消耗（2）提高响应速度（3）方便线程管理

Java中有四种线程池。

缓存线程池。线程池长度没有限制，可以根据增加的任务数动态增加空间（类似数组动态扩容），当扩容的空间长时间不用时会缩小空间。执行的流程为1.判断线程池是否存在空闲线程；2.存在则使用；3.不存在则创建线程，并放入线程池，然后使用。

```java
//缓存线程池的使用
ExecutorService service = Executors.newCachedThreadPool();
service.execute(new Runnable() {
public void run() {
  System.out.println("该线程名字为"+Thread.currentThread().getName());
            }
    });
service.execute(new Runnable() {
public void run() {
  System.out.println("该线程名字为"+Thread.currentThread().getName());
            }
    });

12345678910111213
```

定长线程池。与缓存线程池的区别为该线程池为定长。执行过程为1.判断线程池是否存在空闲线程；2.存在则使用；3.不存在空线程，线程池未满，则创建新线程，放入线程池然后使用；4. 不存在空闲线程,且线程池已满的情况下,则等待线程池存在空闲线程。

单线程线程池。执行过程为1. 判断线程池的线程是否空闲；2. 存在则使用；3. 不空闲则等待池中的单个线程空闲后使用。

周期性任务定长线程池。创建一个线程池，它可安排在给定延迟后运行命令或者定期地执行。

# 3  线程中常用的几种方法

## 1 构造方法（常用的两种）

Thread（）；
Thread（Runnable target）；

## 2 start()方法

线程开始执行，JVM调用线程的run（）方法。

## 3 **休眠**sleep()：

`public static void sleep（long millis）`方法
sleep（long millis）；当前正在执行的线程休眠（暂时停止执行）指定的**毫秒数**
sleep（long millis， int nanos）；当前正在执行的线程休眠（暂时停止执行）指定的毫秒数加上指定的纳秒数

```java
package com.qf.chapter14_3;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/11 - 01 - 11 - 0:34
 * @Description: com.qf.chapter14_3
 * @version: 1.0
 */
public class SleepThread extends Thread{
    @Override
    public void run() {
        for (int i = 0; i < 50; i++) {
            System.out.println(Thread.currentThread().getName()+"....."+i);
            try {
                Thread.sleep(1000);	//休眠一秒
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

```



## 4**放弃**yield()

`public static void yield()`

当前方法主动放弃时间片，回到就绪状态，竞争下一次时间片

```java
package com.qf.chapter14_3;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/11 - 01 - 11 - 0:41
 * @Description: com.qf.chapter14_3
 * @version: 1.0
 */
public class YieldThread extends Thread{
    @Override
    public void run() {
        for (int i = 0; i < 50; i++) {
            System.out.println(Thread.currentThread().getName()+"....."+i);
            Thread.yield();
        }
    }
}

```



## 5**加入join()**

`public final void join()`

允许其他线程加入到当前线程中

```java
package com.qf.chapter14_3;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/11 - 01 - 11 - 0:48
 * @Description: com.qf.chapter14_3
 * @version: 1.0
 */
public class TestJoin {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args)  {
        JoinThread j1= new JoinThread();
        j1.start();

        try {
            //（j1）加入当前线程（main），并阻塞当前线程，直到加入的线程（j1）执行完毕
            j1.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        for (int i = 0; i < 30; i++) {
            System.out.println(Thread.currentThread().getName()+"....."+i);
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

}

```



## 6**设置线程优先级及守护线程**

### 优先级

`线程对象.setPriority()`

线程优先级为1-10，默认为5，优先级越高，表示获取CPU机会越多

```java
package com.qf.chapter14_3;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/11 - 01 - 11 - 8:22
 * @Description: com.qf.chapter14_3
 * @version: 1.0
 */
public class TestPriority {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        Priority p1 = new Priority();
        p1.setName("p1");
        Priority p2 = new Priority();
        p2.setName("p2");
        Priority p3 = new Priority();
        p3.setName("p3");

        p1.setPriority(1);
        p3.setPriority(10);

        p1.start();
        p2.start();
        p3.start();
    }
}

```



### 守护线程

`线程对象.setDaemon(true);`设置为守护线程或用户线程

线程有两类：用户线程（前台线程）、守护线程（后台线程）

如果程序中所有用户线程（前台线程）都执行完毕了，守护线程（后台线程）会自动结束

垃圾回收线程属于守护线程

使用**setDaemon**()方法可以将一个线程设置为守护线程或者用户线程（参数为TRUE时，是守护线程，参数为FALSE时为用户线程），一个线程被创建时默认是用户线程。

当用户线程和守护线程一起运行，当用户线程结束时，则守护线程就结束。

```java
package com.qf.chapter14_3;

/**
 * @author Administrator
 * @Auther: wuxy
 * @Date: 2021/1/11 - 01 - 11 - 8:27
 * @Description: com.qf.chapter14_3
 * @version: 1.0
 */
public class TestDeamon {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        //创建默认前台线程
        DeamonThread d1 = new DeamonThread();
        //设置守护线程
        d1.setDaemon(true);
        d1.start();

        for (int i = 0; i < 30; i++) {
            System.out.println("main----"+i);
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
//效果：
//main----49
//Thread-0------50    main用户进程完毕后将只有Thread-0进程出现了一次
```

## 7`currentThread（）`方法

静态方法，返回对当前正在执行的线程对象的引用。

## 8 interrupt()方法和stop()方法

线程在运行的过程中两种中断线程的方法，一个是**stop**()方法，一个是**interrupt**()方法。

Sun公司在JDK1.2版本的时候将**stop**()方法改为过时了，因为这种中断线程的方式是在外部强制的，这可能会导致在中断过程数据丢失，所以是不安全的。

使用**interrupt**()方法则是一种安全的方式，当在线程外部调用**interrupt**()方法时，JVM会给运行的线程传递一个异常对象，当线程接收到异常对象时，线程就会终止。

```java
public static void main(String[] args) {
        Thread t = new Thread(new MyRunnable());
        t.start();
        t.interrupt();
}
```



## 9 Thread的常用方法

```java
  		 1.String getName()                         //获取该线程的名字
       2.void setName(String name)                //设置该线程的名字
       3.void start()                             //线程开始
       4.static Thread currentThread()            //获取当前线程对象
       5.static void sleep(long millis)           //让当前线程休眠，进入阻塞状态，传入的参数单位为毫秒
       6.void setDaemon(boolean on)               //将线程设置为守护线程或者用户线程
       7.void interrupt()                         //中断此线程
       8.int getPriority()                        //返回此线程的优先级
       9.void setPriority(int newPriority)        //更改此线程的优先级
       10.Thread(Runnable target)                 //（构造方法）传入一个Runnable任务
       11.Thread(String name)                     //（构造方法）为线程取一个名字

```



# 4 线程的几种状态详解

![image-20210111000140225](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210111000140225.png)

![image-20210111084007419](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111084007419.png)

![image-20210111173803459](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111173803459.png)

线程可以处于以下状态之一`线程对象名.getState()`：

**NEW** 尚未启动的线程处于此状态。

**RUNNABLE** 在Java虚拟机中执行的线程处于此状态。（JDK1.5以后统称）

​		**READY** 等待OS选中，并分配时间片

​	    **RUNNING**运行状态

**BLOCKED** 被阻塞等待监视器锁定的线程处于此状态。

**WAITING** 无限期等待另一个线程执行特定操作的线程处于此状态。

**TIMED_WAITING** 正在等待另一个线程执行最多指定等待时间的操作的线程处于此状态。

**TERMINATED** 已退出的线程处于此状态。

线程在给定时间点只能处于一种状态。 这些状态是虚拟机状态，不反映任何操作系统线程状态。

# 5 线程安全

【1】线程安全问题

![image-20210111090437892](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111090437892.png)

- 多线程安全问题:
  当多线程并发访问**临界资源**时，如果**破坏原子操作**，可能会造成数据不一致,
  临界资源:**共享资源（同一对象）**，一次仅允许一个线程使用，才可保证其正确性。

  **原子操作**：不可分割的多步操作，被视作一个整体，其顺序和步骤不可打乱或缺省。

  ```java
  package com.qf.chapter14_4;
  
  import java.util.Arrays;
  
  /**
   * @author Administrator
   * @Auther: wuxy
   * @Date: 2021/1/11 - 01 - 11 - 9:13
   * @Description: com.qf.chapter14_4
   * @version: 1.0
   */
  public class ThreadSafe {
      private static int index = 0;
  
      //这是一个main方法，是程序的入口：
      public static void main(String[] args) throws InterruptedException {
          String[] s = new String[5];
          Runnable runnableA = new Runnable() {
              @Override
              public void run() {
                  s[index] = "hello";
                  index++;
              }
          };
          Runnable runnableB = new Runnable() {
              @Override
              public void run() {
                  s[index] = "world";  
                  index++;				//执行完world添加后还没有index++就被A抢占了线程，所以还是再s[0]处添加的数据
              }
          };
  
          Thread a= new Thread(runnableA,"A");
          Thread b= new Thread(runnableB,"B");
  
          a.start();
          b.start();
          a.join();//会将线程阻塞了
          b.join();
  
          System.out.println(Arrays.toString(s));
      }
  
  }
  
  ```

  ![image-20210111091859130](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111091859130.png)

【2】

### 1、线程的异步与同步

**线程异步**：即多条线程同时执行一个任务时，这种情况下往往是出现数据错乱的情况，例如两个人同时对一个银行账户进行取钱，账户中有10000元，两个人同时取走5000元，结果账户中还剩余5000元。所以这种**线程异步**的情况是非常不安全的。**并发执行**

![image-20210111205642039](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111205642039.png)

**线程同步**：即**多条线程同时执行一个任务**时，，当一个线程开始执行任务线程后，**为这个任务加锁**，**其他线程等待次线程执行完任务线程后再进行抢夺**执行任务的时间片。

![image-20210111205659956](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111205659956.png)

**同步规则**：只有在**调用包含同步代码块**的方法，或者同步方法时，才需要对象的锁标记。如调用不包含同步代码块的方法，或普通方法时，则不需要锁标记，可直接调用。

**线程安全的类**：StringBuffer 、Vector、 Hashtable 

### 2、实现线程安全的方法

#### 2.1、synchronized方法（显式锁）  

```java
synchronized(临界资源对象){//对临界资源对象
  //代码（原子操作）
}

//每个对象都有一个互斥锁标记，用来分配给线程的。
//只有拥有对象互斥锁标记的线程，才能进入对该对象加锁的同步代码块。
//线程退出同步代码块时,会释放相应的互斥锁标记。

```

解决上述的  `数组中添加字符`  安全问题：

```java
public class ThreadSafe {
    private static int index=0;
    public static void main(String[] args)  throws Exception{
        //创建数组
        String[] s=new String[5];
        //创建两个操作
        Runnable runnableA=new Runnable() {

            @Override
            public void run() {
                //同步代码块-----------------------------
                synchronized (s) {
                    s[index]="hello";
                    index++;
                }

            }
        };
        Runnable runnableB=new Runnable() {

            @Override
            public void run() {
               //同步代码块-----------------------------
                synchronized (s) {
                    s[index]="world";
                    index++;
                }

            }
        };

        //创建两个线程对象
        Thread a=new Thread(runnableA,"A");
        Thread b=new Thread(runnableB,"B");
        a.start();
        b.start();

        a.join();//加入线程
        b.join();//加入线程

        System.out.println(Arrays.toString(s));

    }

}

```

##### 同步代码块（案例同步解决）

1.当一个售票窗口在卖票时，其他窗口等待。

```java

class Runnable implements Runnable{
    private int count = 10;
  	//第一种方式创建锁--------
    private Object obj = new Object();
    public void run() {
        while(true){
          //第一种方式创建锁--------块中的内容需要整体实现完了，CPU时间块才能被抢占
           //第二种方式创建锁--------synchronized (this)
            synchronized (obj){
                if(count>0){
                    System.out.println(Thread.currentThread().getName()+"买票中");
                    try {
                        Thread.sleep(500);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    count--;
                    System.out.println("余票："+count);
                }else{
                    break;
                }
            }
        }
    }
}
```

2.银行卡存钱取钱案例

```java
package com.qf.chapter14_4;

public class TestBankCard {
	public static void main(String[] args) {
		//1创建银行卡
		BankCard card=new BankCard();
		//2创建两个操作
		Runnable add=new Runnable() {
			@Override
			public void run() {
				for(int i=0;i<10;i++) {
					synchronized (card) {
						card.setMoney(card.getMoney()+1000);
						System.out.println(Thread.currentThread().getName()+"存了1000,余额是:"+card.getMoney());
					}
					
				}
			}
		};
		Runnable sub=new Runnable() {
			@Override
			public void run() {
				for(int i=0;i<10;i++) {
					synchronized (card) {
						if(card.getMoney()>=1000) {
							card.setMoney(card.getMoney()-1000);
							System.out.println(Thread.currentThread().getName()+"取了1000,余额是:"+card.getMoney());
						}else {
							System.out.println("余额不足，请存取");
							i--;
						}
					}
					
				}
			}
		};
		
		//3创建两个线程对象
		Thread xiaoli=new Thread(add, "小李");
		Thread xiaoyue=new Thread(sub,"小月" );
		xiaoli.start();
		xiaoyue.start();
		
	}
}

```

![image-20210111194854466](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111194854466.png)

##### 同步方法

当时用同步方法时，当前加锁的对象默认为当前对象this

```java
synchronized 返回值类型 方法名称（形参列表0）{//对当前（this）对象加锁
  	//代码（原子操作）
  
}
```

案例解决：

```java
class Runnable implements Runnable{
    private int count = 10;
    public void run() {
        while(true){
            if(!sale()){
                break;
            }
        }
    }
  
		//卖票（同步方法）
    public synchronized boolean sale(){		//非静态方法 锁（this） 静态方法 锁（ticket.class）
    	//判断票数是否大于0，是返回true，否返回false
        if(count>0){
            System.out.println(Thread.currentThread().getName()+"买票中");
            try {
            	//此处休眠0.5秒
                Thread.sleep(500);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            //票卖出，票数减一
            count--;
            System.out.println("余票："+count);
            return true;
        }else{
            return false;
        }
    }
}
```

#### 2.2、Lock方法（隐式锁）

【1】概述

使用Lock方法需要创建`Lock`对象，并在需要加锁是**手动加锁**，在需要解锁时手动解锁，显示定义，更加**灵活**。

`Lock`实现提供比使用`synchronized`方法和语句可以获得的更广泛的锁定操作。  它们允许更灵活的结构化，可能具有完全不同的属性，并且可以支持多个相关联的对象`Condition` 。 

常用方法：

`void lock()`  //获取锁，如锁被占用，则等待。

`boolean tryLock() `//尝试获取锁（成功返回true,失败返回false，不阻塞)

`void unlock()`//释放锁

```java
 	Lock l = ...;
	l.lock(); 
	try { // access the resource protected by this lock 

	} finally {
  	l.unlock(); // 保证锁一定会被释放
} 
```

【2】详解

##### 重入锁`ReentrantLock`：

一个可重入互斥`Lock`具有与使用`synchronized`方法和语句访问的隐式监视锁相同的基本行为和语义，但具有扩展功能。 

```java
class X {
            private final ReentrantLock lock = new ReentrantLock();// ... 
             public void m() { 
                 lock.lock(); // block until condition holds 
                  try {
                      // ... method body 
                  } finally { 
                      lock.unlock(); 
                  } 
             } 
        }
```

【3】案例代码

```java
package com.qf.chapter14_9;

import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

/**
 * ReentrantLock的使用
 * @author wgy
 */
public class MyList {
	//创建锁
	private Lock lock=new ReentrantLock();
	private String[] str= {"A","B","","",""};
	private int count=2;
	
	public void add(String value) {
		lock.lock();
		try {
			str[count]=value;
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			count++;
			System.out.println(Thread.currentThread().getName()+"添加了"+value);
		} finally {
			lock.unlock();
		}
		
		
	}
	
	public String[] getStr() {
		return str;
	}
	
}

```

```java
package com.qf.chapter14_9;

import java.util.Arrays;

public class TestMyList {
	public static void main(String[] args) throws Exception {
		MyList list=new MyList();
		Runnable runnable=new Runnable() {
			
			@Override
			public void run() {
				list.add("hello");
			}
		};
		Runnable runnable2=new Runnable() {
			
			@Override
			public void run() {
				list.add("world");
			}
		};
		
		Thread t1=new Thread(runnable);
		Thread t2=new Thread(runnable2);
		
		t1.start();
		t2.start();
		
		t1.join();
		t2.join();
		System.out.println(Arrays.toString(list.getStr()));
		
			
	}
}

```

![image-20210111211656192](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111211656192.png)

##### 读写锁 `ReentrantReadWriteLock`:

【1】

一种支持**一写多读**的同步锁，读写分离，可分别分配读锁、写锁。

支持**多次分配读锁**，使多个读操作可以并发执行。

【2】互斥规则

- 写—写:互斥，阻塞。
- 读—写:互斥，读阻塞写、写阻塞读。
- 读—读:不互斥、不阻塞。
- 在读操作远远高于写操作的环境中，可在保障线程安全的情况下，提高运行效率。

【3】案例代码

```java
package com.qf.chapter14_9;
/**
 * 演示读写锁的使用
 * ReentrantReadWriteLock
 * @author wgy
 *
 */

import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.locks.ReentrantReadWriteLock;
import java.util.concurrent.locks.ReentrantReadWriteLock.ReadLock;
import java.util.concurrent.locks.ReentrantReadWriteLock.WriteLock;

public class ReadWriteDemo {
	//1.创建读写锁
	private ReentrantReadWriteLock rrl=new ReentrantReadWriteLock();
  
	//2.1获取读锁
	private ReadLock readLock=rrl.readLock();
	//2.2获取写锁
	private WriteLock writeLock=rrl.writeLock();
	
	//对比互斥锁
	//private ReentrantLock lock=new ReentrantLock();

	private String value;
	
	//读取
	public String getValue() {
		//使用读锁上锁
		readLock.lock();
		try {
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			System.out.println("读取:"+this.value);
			return this.value;
		}finally {
			readLock.unlock();
		}
	}
	//写入
	public void setValue(String value) {
		writeLock.lock();
		try {
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			System.out.println("写入:"+value);
			this.value=value;
		}finally {
			writeLock.unlock();
		}
	}
	
}

```

```java
package com.qf.chapter14_9;

import java.util.Random;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.LinkedBlockingQueue;

public class TestReadWriteLock {
	public static void main(String[] args) {
		ReadWriteDemo readWriteDemo=new ReadWriteDemo();
		//创建线程池
		ExecutorService es=Executors.newFixedThreadPool(20);
		//创建读入
		Runnable read=new Runnable() {
			@Override
			public void run() {
				readWriteDemo.getValue();
			}
		};
    //创建写入
		Runnable write=new Runnable() {
			@Override
			public void run() {
				readWriteDemo.setValue("张三:"+new Random().nextInt(100));
			}
		};
		long start=System.currentTimeMillis();
		//分配2个写的任务
		for(int i=0;i<2;i++) {
			es.submit(write);
		}

		//分配18读取任务
		for(int i=0;i<18;i++) {
			es.submit(read);
		}
		es.shutdown();//关闭
		while(!es.isTerminated()) {//空转
		}
		long end=System.currentTimeMillis();
		System.out.println("用时:"+(end-start));
		
	}
}

```

![image-20210111213413585](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111213413585.png)

#### 2.3、显式锁和隐式锁的区别

(1)Sync:Java中的关键字，是由JVM来维护的。是JVM层面的锁。
(2)Lock:是JDK5以后才出现的具体的类。使用lock是调用对应的API。是API层面的锁。

(3)在使用sync关键字的时候，我们使用者根本不用写其他的代码，然后程序就能够获取和释放锁了。那是因为当sync代码块执行完成之后，系统会自动的让程序释放占用的锁。Sync是由系统维护的，如果非逻辑问题的话话，是不会出现死锁的。
(4)在使用lock的时候，我们使用者需要手动的获取和释放锁。如果没有释放锁，就有可能导致出现死锁的现象。手动获取锁方法：lock.lock()。释放锁：unlock方法。需要配合tyr/finaly语句块来完成。

(5)Sync是不可中断的。除非抛出异常或者正常运行完成
(6)Lock可以中断的。

(7)Sync:非公平锁
(8)lock：两者都可以的。默认是非公平锁。ReentrantLock(boolean fair)，true是公平锁，false是不公平锁

# 6 死锁

![image-20210111181857196](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111181857196.png)

**概述**
A和B两人分别进入试衣间1和试衣间2，A想等B出来后去试衣间2，自己则在试衣间1中等待，B想等A出来后去试衣间1，自己则在试衣间2中等待，最终2个人都在等对方出来，但是对方都不出来，导致一直僵持。

```java
public class DeadLockTest {
    public static void main(String[] args) {
        A a = new A();
        B b = new B();
        //子线程中需要和主线程中同样的A和B对象
        R r = new R(a,b);
        Thread t = new Thread(r);
        t.start();
        b.say(a);
    }
}

class B{
    public synchronized void say(A a){
        System.out.println("BBBBB");
        a.reply();
    }
    public synchronized void reply(){
        System.out.println("bbbbb");
    }
}

class A{
    public synchronized void say(B b){
        System.out.println("AAAAA");
        b.reply();
    }
    public synchronized void reply(){
        System.out.println("aaaaa");
    }
}

class R implements Runnable{
    private A a;
    private B b;

    public R(A a, B b) {
        this.a = a;
        this.b = b;
    }
    public void run() {
        a.say(b);
    }
}
```

# 7 线程通信

## 7.1等待

`public final void wait()`

`public final void wait(long timeout)`

线程调用wait()方法，**释放**它对锁的拥有权，然后**等待另外的线程来通知它**（通知的方式是notify()或者notifyAll()方法），这样它才能重新获得锁的拥有权和恢复执行。

必须在对**obj加锁的同步代码块**中。在一个线程中，调用`obj.wait()` 时，此线程会**释放**其拥有的所有锁标记。同时此线程阻塞在o的等待队列中。释放锁，**进入等待队列**。

## 7.2通知

`public final void notify()`**方法会唤醒一个等待当前对象的锁的线程。唤醒在此对象监视器上等待的单个线程。**

`public final void notifyAll()` **方法会唤醒在此对象监视器上等待的所有线程。** 　

## 7.3案例代码：　

```java
package com.qf.chapter14_6;

public class BankCard {
	//余额
	private double money;
	//标记
	private boolean flag=false;// true 表示有钱可以取钱  false没钱 可以存
	//存钱
	
	public synchronized void save(double m) { //this
		while(flag) {//有钱
			try {
				this.wait();//进入等待队列,同时释放锁 ，和cpu
			} catch (InterruptedException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
		
		money=money+m;
		System.out.println(Thread.currentThread().getName()+"存了"+m+" 余额是"+money);
		//修改标记
		flag=true;
		//唤醒取钱线程
		this.notify();	
	}
	
	//取钱
	public synchronized void take(double m) {//this
		while(!flag) {
			try {
				this.wait();//进入等待队列,同时释放锁 ，和cpu
			} catch (InterruptedException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
		
		money=money-m;
		System.out.println(Thread.currentThread().getName()+"取了"+m+" 余额是"+money);
		//修改标记
		flag=false;
		//唤醒存钱线程
		this.notify();

	}
	
}

```



```java
package com.qf.chapter14_6;

public class AddMoney implements Runnable{

	private BankCard card;
	public AddMoney(BankCard card) {
		this.card=card;
	}
	
	@Override
	public void run() {
		
		for(int i=0;i<10;i++) {
			card.save(1000);
		}
		
	}

}

-------------------------------------------------------------------------------------
package com.qf.chapter14_6;

public class SubMoney implements Runnable{
	private BankCard card;
	public SubMoney(BankCard card) {
		this.card=card;
	}
	@Override
	public void run() {
		for(int i=0;i<10;i++) {
			card.take(1000);
		}
	}
}
-------------------------------------------------------------------------------------
package com.qf.chapter14_6;

public class TestBankCard {
	public static void main(String[] args) {
		//1创建银行卡
		BankCard card=new BankCard();
		//2创建操作
		AddMoney add=new AddMoney(card);
		SubMoney sub=new SubMoney(card);
		
		//3创建线程对象
		Thread chenchen=new Thread(add, "晨晨");
		Thread bingbing=new Thread(sub, "冰冰");
		
		//4启动
		chenchen.start();
		mingming.start();
		bingbing.start();
		lili.start();
		
	}
}

```

![image-20210111194636177](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111194636177.png)

如果**多个线程**进行上述实验将会出现问题。

```java
//3创建线程对象
		Thread chenchen=new Thread(add, "晨晨");
		Thread bingbing=new Thread(sub, "冰冰");
		
		Thread mingming=new Thread(add, "明明");
		Thread lili=new Thread(sub, "莉莉");
```

分析：

![image-20210111190212636](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111190212636.png)

解决办法：   **if**（flag）换成**while**（flag）将不会从判断出来，但是新的问题出现了：四个线程都进入等待队列

![image-20210111192646703](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111192646703.png)

解决办法：**notify();**改成**notifyAll();**

# 8 生产者与消费者

![image-20210111192851230](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111192851230.png)

生产面包、消费面包案例

```java
package com.qf.chapter14_7;
/**
 * 面包
 * @author wgy
 *
 */
public class Bread {
	private int id;		//面包id
	private String productName;		//面包生产者
	public Bread() {
		// TODO Auto-generated constructor stub
	}
	public Bread(int id, String productName) {
		super();
		this.id = id;
		this.productName = productName;
	}
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getProductName() {
		return productName;
	}
	public void setProductName(String productName) {
		this.productName = productName;
	}
	@Override
	public String toString() {
		return "Bread [id=" + id + ", productName=" + productName + "]";
	}
	
	
	
}
-------------------------------------------------------------------------------------
  package com.qf.chapter14_7;

public class BreadCon {
	//存放面包的数组
	private Bread[] cons=new Bread[6];
	//存放面包的位置
	private int index=0;
	
	//存放面包
	public synchronized void input(Bread b) { //锁this
		//判断容器有没有满
		while(index>=6) {//面包已经满了
			try {
				this.wait();
			} catch (InterruptedException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
		//先放入，再动下标
		cons[index]=b;
		System.out.println(Thread.currentThread().getName()+"生产了"+b.getId()+"");
		index++;
		//唤醒
		this.notifyAll();
		
		
		
	}
	//取出面包
	public synchronized void output() {//锁this
		while(index<=0) {
			try {
				this.wait();
			} catch (InterruptedException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
    //先动下标，再取出
		index--;
		Bread b=cons[index];
		System.out.println(Thread.currentThread().getName()+"消费了"+b.getId()+" 生产者:"+b.getProductName());
		cons[index]=null;
		//唤醒生产者
		this.notifyAll();
		
		
		
	}
}

```

```java
package com.qf.chapter14_7;

public class Prodcut implements Runnable {

	private BreadCon con;
	
	public Prodcut(BreadCon con) {
		super();
		this.con = con;
	}

	@Override
	public void run() {
		for(int i=0;i<30;i++) {
			con.input(new Bread(i, Thread.currentThread().getName()));
		}
	}
	
}

```

```java
package com.qf.chapter14_7;

public class Consume implements Runnable{

	private BreadCon con;
	
	public Consume(BreadCon con) {
		super();
		this.con = con;
	}

	@Override
	public void run() {
		for(int i=0;i<30;i++) {
			con.output();
		}
	}

}

```

```java
package com.qf.chapter14_7;

public class Test {
	public static void main(String[] args) {
		//容器
		BreadCon con=new BreadCon();
		//生产和消费
		Prodcut prodcut=new Prodcut(con);
		Consume consume=new Consume(con);
		//创建线程对象
		Thread chenchen=new Thread(prodcut, "晨晨");
		Thread bingbing=new Thread(consume, "冰冰");
		Thread mingming=new Thread(prodcut, "明明");
		Thread lili=new Thread(consume, "莉莉");
		//启动线程
		chenchen.start();
		bingbing.start();
		mingming.start();
		lili.start();
	}
}

```

![image-20210111194407696](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111194407696.png)



当厨师在做菜时，服务员休息状态，当厨师做完菜后，厨师休息，服务员端菜出去，等服务员端空盘子回来后，服务员继续休息，叫厨师继续做菜。依次循环

```java
public class Test {
    public static void main(String[] args) {
        Food f = new Food();
        Cook c = new Cook(f);
        Waiter w = new Waiter(f);
        //厨师线程
        new Thread(c).start();
        //服务员线程
        new Thread(w).start();
    }
}

class Cook implements Runnable{
    private Food f;
    public Cook(Food f) {
        this.f = f;
    }

    @Override
    public void run() {
        for(int i = 0;i<10;i++){
            f.cook(i);
            try {
            	//此处休眠0.5秒
                Thread.sleep(500);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

class Waiter implements Runnable{
    private Food f;
    private boolean flag = true;
    public Waiter(Food f) {
        this.f = f;
    }

    @Override
    public void run() {
        for(int i = 0;i<10;i++){
            f.get();
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

class Food{
    private String name;
    private String tasty;
    private boolean flag = true;

    public Food() {
    }

    public Food(String name, String tasty) {
        this.name = name;
        this.tasty = tasty;
    }

    public boolean isFlag() {
        return flag;
    }

    public void setFlag(boolean flag) {
        this.flag = flag;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getTasty() {
        return tasty;
    }

    public void setTasty(String tasty) {
        this.tasty = tasty;
    }

	//厨师做菜
    public synchronized void cook(int i){
        if(flag){
            if(i % 2 == 0){
                this.setName("番茄炒蛋");
                this.setTasty("咸");
            }else{
                this.setName("糖醋排骨");
                this.setTasty("酸甜");
            }
            System.out.println("厨师做菜："+this.getName()+"，味道："+this.getTasty());
        }
        flag = false;
        //唤醒其他线程
        this.notifyAll();
        try {
        	//厨师线程休眠
            this.wait();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

    }

	//服务员端菜
    public synchronized void get(){
        if(!flag){
            System.out.println("服务员出菜："+this.getName()+",味道："+this.getTasty());
        }
        flag = true;
        //唤醒其他线程
        this.notifyAll();
        try {
        	//服务员线程休眠
            this.wait();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

# 9 线程池（了解）

## **概述**

当程序中需要执行许多的内容很少的线程时，线程**创建所花费的时间**就会多于每次线程运行的所耗费的时间，就是导致程序的效率大大降低。使用线程池的方法就可以为程序**节省下创建线程的时间**。

【1】问题:
线程是宝贵的内存资源、单个线程约占**1MB**空间，过多分配易造成内存溢出。

**频繁的创建及销毁**线程会增加虚拟机回收频率、资源开销，造成程序性能下降。

【2】线程池:
**线程容器**，可设定线程分配的**数量上限**。

将**预先创建**的线程对象存入池中，并**重用**线程池中的线程对象。

**避免频繁的创建和销毁**。

【3】线程池原理

![image-20210111195544062](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111195544062.png)

## 创建线程池

常用的线程池接口和类（所在包`java.util.concurrent`）

`Executor`:线程池的顶级接口。

`ExecutorService`:线程池接口，可通过submit(Runnable task)提交任务代码。

`Executors工厂类`:通过此类可以获得一个线程池。

通过`newFixedThreadPool(int nThreads)`获取固定数量的线程池。参数:指定线程池中线程的数量。

通过`newCachedThreadPool()`获得动态数量的线程池，如不够则创建新的，没有上限



## 线程池的种类

```java
ExecutorService service = Executors.创建方法
void execute(Runnable command)  //指挥线程池执行任务
```

### **1.缓存线程池**

任务线程传入时自动分配线程，线程不够时自动创建新线程

```java
Executors.newCachedThreadPool()    //创建缓存线程池
```

### **2.定长线程池**

指定线程池线程的个数，任务线程传入时自动分配线程，线程不够时剩余任务线程排队等待线程池中的线程执行完毕

```
Executors.newFixedThreadPool(int nThreads) //创建定长线程池，传入线程池中线程的个数
```

### **3.单线程线程池**

线程池中只有一个线程，任务线程传入时自动分配线程，一个任务执行时剩余任务线程排队等待线程池中的线程执行完毕

```java
Executors.newSingleThreadExecutor()   //创建单线程线程池
```

### **4.调度定长线程池**

指定线程池线程的个数，任务线程传入时自动分配线程，可以设定任务线程第一次执行的延时时间和之后每次执行的间隔时间  **调度**：周期、定时

```java
Executors.newScheduledThreadPool(int corePoolSize)   
//创建周期定长线程池，传入线程池中线程的个数
  service.schedule(Runnable command, long delay, TimeUnit unit)
  //线程定时执行，传入任务、时长和时长单位
  service.scheduleAtFixedRate(Runnable command, long initialDelay, long period, TimeUnit unit)
//周期性定时执行，传入任务，初次执行延时时长，周期间隔时长和时长单位
```

## 代码案例

```java
package com.qf.chapter14_8;

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.ThreadPoolExecutor;

/**
 * 演示线程池的创建
 * Executor:线程池的根接口,execute()
 * ExecutorService:包含管理线程池的一些方法，submit shutdown
 * 	  ThreadPoolExecutor
 * 		ScheduledThreadPoolExecutor
 * Executors：创建线程池的工具类
 * 		(1)创建固定线程个数线程池
 * 		(2)创建缓存线程池，由任务的多少决定
 * 		(3)创建单线程池
 * 		(4)创建调度线程池  调度:周期、定时执行
 * 	
 * 
 * 
 * @author wgy
 *
 */
public class Demo1 {
	public static void main(String[] args) {
		//1.1创建固定线程个数的线程池
		//ExecutorService es=Executors.newFixedThreadPool(4);
		//1.2创建缓存线程池，线程个数由任务个数决定
		ExecutorService es=Executors.newCachedThreadPool();
		
		//1.3创建单线程线程池
		//Executors.newSingleThreadExecutor();
		//1.4创建调度线程池  调度:周期、定时执行
		//Executors.newScheduledThreadPool(corePoolSize)
		Executors.newScheduledThreadPool(3);
    
		//2创建任务
		Runnable runnable=new Runnable() {
			private int ticket=100;
			@Override
			public void run() {
				while(true) {
					if(ticket<=0) {
						break;
					}
					System.out.println(Thread.currentThread().getName()+"买了第"+ticket+"张票");
					ticket--;
				}
			}
		};
    
		//3提交任务
		for(int i=0;i<5;i++) {
			es.submit(runnable);   //提交任务
		}
    
		//4关闭线程池
		es.shutdown();//等待所有任务执行完毕 然后关闭线程池，不接受新任务。
    //es.shutdownNow()//不等待所有任务执行完毕 然后关闭线程池，不接受新任务。
	}
}

```

# 10 线程安全的集合

![image-20210111214437995](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111214437995.png)

![image-20210111214535916](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210111214535916.png)

## 【1】问题出现

```java
package com.qf.chapter14_10;

import java.lang.reflect.Array;
import java.util.ArrayList;
/**
 * 
 * @author wgy
 * 演示：使用多线程操作线程不安全集合
 */
public class Demo1 {
	public static void main(String[] args) {
		//1创建arraylist
		ArrayList<String> arrayList=new ArrayList<>();
    
		//2创建线程
		for(int i=0;i<20;i++) {
			int temp=i;
			new Thread(new Runnable() {
				@Override
				public void run() {
					for(int j=0;j<10;j++) {
					arrayList.add(Thread.currentThread().getName()+"===="+temp+"===="+j);
						System.out.println(arrayList.toString());
					}
				}
			}).start();
		}
	}
}

```

## 【2】collections方法解决

```java
		//1.1使用Collections中的线程安全方法转成线程安全的集合
		List<String> synList=Collections.synchronizedList(arrayList);
		//1.2使用CopyOnWriteArrayList
		//CopyOnWriteArrayList<String> arrayList=new CopyOnWriteArrayList<>(); 
		
		synList.add();
		arrayList.add();
```

## 【3】方法实现详解

### 1.CopyOnWriteArrayList

线程安全的`ArrayList`，加强版的读写分离。

写有锁，读无锁，读写之间不阻塞，优于读写锁。

源码分析：使用的lock锁，读不上锁

写入移除时，先copy一个容器副本、再添加新元素，最后替换引用。（浪费空间）

使用方式与ArrayList无异。

```java
package com.qf.chapter14_10;

import java.util.Random;
import java.util.concurrent.CopyOnWriteArrayList;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

/**
 * 使用多线程操作CopyOnWriteArrayList
 * @author wgy
 *
 */
public class Demo2 {
	public static void main(String[] args) {
		//1创建集合
		CopyOnWriteArrayList<String> list=new CopyOnWriteArrayList<>();
		
    //2使用多线程操作
		ExecutorService es=Executors.newFixedThreadPool(5);
		//3提交任务
		for(int i=0;i<5;i++) {
			es.submit(new Runnable() {
				@Override
				public void run() {
					for(int j=0;j<10;j++) {
						list.add(Thread.currentThread().getName()+"...."+new Random().nextInt(1000));
					}
				}
			});
		}
		//4关闭线程池
		es.shutdown();
		while(!es.isTerminated()) {}
		//5打印结果
		System.out.println("元素个数:"+list.size());
		for (String string : list) {
			System.out.println(string);
		}
	}
}

```

### 2.CopyOnWriteArraySet

线程安全的Set，底层使用`CopyOnWriteArrayList`实现。

唯一不同在于，使用`addIfAbsent()`添加元素，会遍历数组,

通过`indexof()及equals()`判断如存在元素，则不添加（扔掉副本）。

```java
package com.qf.chapter14_10;

import java.util.concurrent.CopyOnWriteArraySet;

/**
 * 演示CopyOnWriteArraySet
 * 重复依据：equals方法
 * @author wgy
 *
 */
public class Demo3 {
	public static void main(String[] args) {
		//1创建集合
		CopyOnWriteArraySet<String> set=new CopyOnWriteArraySet<>();
		//2添加元素
		set.add("pingguo");
		set.add("huawei");
		set.add("xiaomi");
		set.add("lianxiang");
		set.add("pingguo");
		//3打印
		System.out.println("元素个数:"+set.size());
		System.out.println(set.toString());
	}
}

```

### 3.Queue接口

#### 【1】概述与常用方法

Collection的子接口，表示队列**FIFO** (First In First Out）先进先出常用方法:
抛出异常:
 `boolean add(E e)`    //顺序添加一个元素（到达上限后，再添加则会抛出异常)。

`E remove()`                 //获得第一个元素并移除（如果队列没有元素时，则抛异常)。

`E element()`               //获得第一个元素但不移除（如果队列没有元素时，则抛异常)。

返回特殊值:   **推荐使用**

`boolean offer(E e)`//顺序添加一个元素（到达上限后，再添加则会返回false)

`E poll()`					//获得第一个元素并移除（如果队列没有元素时，则返回null)

`E peek()`					//获得第一个元素但不移除（如果队列没有元素时，则返回null)

```java
package com.qf.chapter14_10;

import java.util.LinkedList;
import java.util.Queue;

/**
 * Queue接口的使用
 * @author wgy
 *
 */
public class Demo4 {
	public static void main(String[] args) {
		//1创建队列
		Queue<String> queue=new LinkedList<>();
		//2入队
		queue.offer("苹果");
		queue.offer("橘子");
		queue.offer("葡萄");
		queue.offer("西瓜");
		queue.offer("榴莲");
		//3出队
		System.out.println(queue.peek());
		System.out.println("----------------");
		System.out.println("元素个数:"+queue.size());
		int size=queue.size();
		for(int i=0;i<size;i++) {
			System.out.println(queue.poll());
		}
		System.out.println("出队完毕:"+queue.size());
		
		
	}
}

```

#### 【2】线程安全的Queue

##### ConcurrentLinkedQueue

线程安全、可高效读写的队列，高并发下性能最好的队列。

无锁、CAS（compare and switch）比较交换算法，修改的方法包含三个核心参数(V,E,N)

V:要更新的变量、E:预期值、N:新值。

只有当V==E时，V=N;否则表示已被更新过，则取消当前操作（硬件所支持的），可扩容。

```java
package com.qf.chapter14_10;

import java.util.concurrent.ConcurrentLinkedQueue;

/**
 * ConcurrentLinkedQueue的使用
 * @author wgy
 *
 */
public class Demo5 {
	public static void main(String[] args) throws Exception {
		//1创建安全队列
		ConcurrentLinkedQueue<Integer> queue=new ConcurrentLinkedQueue<>();
		//2入队操作
		Thread t1=new Thread(new Runnable() {
			
			@Override
			public void run() {
				for(int i=1;i<=5;i++) {
					queue.offer(i);
				}
			}
		});
		Thread t2=new Thread(new Runnable() {
			
			@Override
			public void run() {
				for(int i=6;i<=10;i++) {
					queue.offer(i);
				}
			}
		});
		//3启动线程
		t1.start();
		t2.start();
		
		t1.join();
		t2.join();
		System.out.println("-------------出队-------------");
		//4出队操作
		int size=queue.size();
		for(int i=0;i<size;i++) {
			System.out.println(queue.poll());
		}
		
	}
}

```

##### BlockingQueue接口(阻塞队列)

`Queue`的子接口，阻塞的队列，增加了两个线程状态为无限期等待的方法。
方法:
`void put(E e)`		//将指定元素插入此队列中，如果没有可用空间，则等待,不可扩容（生产者与消费者面包问题）。

`E take()`			//获取并移除此队列头部元素，如果没有可用元素，则等待。

案例一

```java
package com.qf.chapter14_10;

import java.util.concurrent.ArrayBlockingQueue;

/**
 * 阻塞队列的使用
 * 案例1：创建一个有界队列，添加数据
 * @author wgy
 *
 */
public class Demo6 {
	public static void main(String[] args) throws Exception{
		//创建一个有界队列，添加数据
		ArrayBlockingQueue<String> queue=new ArrayBlockingQueue<>(5);
		//添加元素
		queue.put("aaa");
		queue.put("bbb");
		queue.put("ccc");
		queue.put("ddd");
		queue.put("eee");
		//删除元素
		queue.take();
		System.out.println("已经添加了5个元素");
		queue.put("xyz");
		System.out.println("已经添加了6个元素");
		System.out.println(queue.toString());
	}
}

```

案例二

```java
package com.qf.chapter14_10;

import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.ConcurrentHashMap;

/**
 * 案例2：使用阻塞队列实现生产者和消费者
 * @author wgy
 *
 */
public class Demo7 {
	public static void main(String[] args) {
		//1创建队列
		ArrayBlockingQueue<Integer> queue=new ArrayBlockingQueue<>(6);
		//2创建两个线程
		Thread t1=new Thread(new Runnable() {
			
			@Override
			public void run() {
				for(int i=0;i<30;i++) {
					try {
						queue.put(i);
						System.out.println(Thread.currentThread().getName()+"生产了第"+i+"号面包");
					} catch (InterruptedException e) {
						// TODO Auto-generated catch block
						e.printStackTrace();
					}
					
				}
			}
		}, "晨晨");
		
		Thread t2=new Thread(new Runnable() {
			
			@Override
			public void run() {
				for(int i=0;i<30;i++) {
					try {
						Integer num=queue.take();
						System.out.println(Thread.currentThread().getName()+"消费了第"+i+"号面包");
					} catch (InterruptedException e) {
						// TODO Auto-generated catch block
						e.printStackTrace();
					}
					
				}
			}
		}, "冰冰");
		
		//启动线程
		t1.start();
		t2.start();	
	}
}
```

### 4.ConcurrentHashMap

初始容量默认为`16段(Segment`），使用`分段锁`设计。

不对整个Map加锁，而是为每个`Segment`加锁。

当多个对象存入同一个`Segment`时，才需要互斥。

最理想状态为16个对象分别存入`16个Segment`，并行数量16。

使用方式与`HashMap`无异。

```java
package com.qf.chapter14_10;

import java.util.concurrent.ConcurrentHashMap;

/**
 * ConcurrentHashMap的使用
 * @author wgy
 *
 */
public class Demo8 {
	public static void main(String[] args) {
		//1创建集合
		ConcurrentHashMap<String, String> hashMap=new ConcurrentHashMap<String, String>();
		//2使用多线程添加数据
		for(int i=0;i<5;i++) {
			new Thread(new Runnable() {
				
				@Override
				public void run() {
					for(int k=0;k<10;k++) {
						hashMap.put(Thread.currentThread().getName()+"--"+k, k+"");
						System.out.println(hashMap);
					}
				}
			}).start();
		}
	}

}

```

