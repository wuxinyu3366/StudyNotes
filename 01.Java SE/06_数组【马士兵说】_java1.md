# 一、数组的引入

【1】习题引入：

```java
import java.util.Scanner;
public class TestArray01{
    public static void main(String[] args){
                //功能：键盘录入十个学生的成绩，求和，求平均数：
                //定义一个求和的变量：
                int sum = 0;
                Scanner sc = new Scanner(System.in);
                for(int i=1;i<=10;i++){//i:控制循环次数
                        System.out.print("请录入第"+i+"个学生的成绩：");
                        int score = sc.nextInt();
                        sum += score;
                }
                
                System.out.println("十个学生的成绩之和为："+sum);
                System.out.println("十个学生的成绩平均数为："+sum/10);
                
                //本题的缺点：
                //求第6个学生的成绩：？？？？？---》不能
                
        }
}
```

![image-20210105174108882](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105174108882.png)

缺点：就是不能求每个学生的成绩具体是多少

解决：将成绩进行存储  ----》 引入 ： 数组 

感受到数组的作用：数组用来存储数据的，在程序设计中，为了处理方便，数组用来将**相同类型的若干数据**组织起来。
这个若干数据的集合我们称之为**数组**。

# 二、数组的学习

【1】数组的定义
数组是相同类型数据的有序集合。数组描述的是相同类型的若干个数据，按照一定的先后次序排列组合而成。其中，每一个数据称作一个元素，每个元素可以通过一个索引（下标）来访问它们。
数组的四个基本特点：
1.长度是确定的。数组一旦被创建，它的大小就是不可以改变的。
2.其元素的类型必须是相同类型，不允许出现混合类型。
3.数组类型可以是任何数据类型，包括基本类型和引用类型。
4.数组有索引的：索引从0开始，到 数组.length-1 结束 
5.数组变量属于引用类型，数组也是对象。
PS:数组变量属于引用类型，数组也是对象，数组中的每个元素相当于该对象的成员变量。数组本身就是对象，Java中对象是在堆中的，因此数组无论保存原始类型还是其他对象类型，数组对象本身是在堆中存储的。

【2】数组的学习：

```java
public class TestArray02{
    public static void main(String[] args){
                //数组的作用：用来存储相同类型的数据
                //以int类型数据为案例：数组用来存储int类型数据
                //1.声明(定义数组)
                int[] arr; //定义一个int类型的数组，名字叫arr
                //int arr2[];
                //如果数组只声明，没有后续操作，那么这个数组相当于没定义
                //int[] arr3 = null;//空 辨别：数组赋值为null和什么都没有赋值  不一样的效果 
                
                //2.创建
                arr = new int[4];//给数组开辟了一个长度为4的空间
                //编译期声明和创建会被合为一句话: int[] arr = new int[4];
                
                //3.赋值
                arr[0] = 12;
                arr[3] = 47;
                arr[2] = 98;
                arr[1] = 56;
                arr[2] = 66;
                /*
                arr[4] = 93;
                出现异常：Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 4
                Array 数组
                Index 索引
                OutOf 超出
                Bounds 界限
                Exception 异常
                ---》数组索引越界异常  
                */
        
                //4.使用
                System.out.println(arr[2]);
                System.out.println(arr[0]+100);
                //通过数组一个属性来获取  length 长度
                System.out.println("数组的长度是："+arr.length);
        }
}
```

![image-20210105174059866](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105174059866.png)



## 内存分析

![image-20210105003026297](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105003026297.png)

# 三、完善引入的习题_数组的遍历

【1】代码：

```java
import java.util.Scanner;
public class TestArray03{
    public static void main(String[] args){
                //功能：键盘录入十个学生的成绩，求和，求平均数：
                //定义一个int类型的数组，长度为10 ：
                int[] scores = new int[10];
                //定义一个求和的变量：
                int sum = 0;
                Scanner sc = new Scanner(System.in);
                for(int i=1;i<=10;i++){//i:控制循环次数
                        System.out.print("请录入第"+i+"个学生的成绩：");
                        int score = sc.nextInt();
                        scores[i-1] = score;
                        sum += score;
                }
                
                System.out.println("十个学生的成绩之和为："+sum);
                System.out.println("十个学生的成绩平均数为："+sum/10);
                
                 
                //求第6个学生的成绩： 
                //System.out.println(scores[5]);
                /*
                System.out.println(scores[0]);
                System.out.println(scores[1]);
                System.out.println(scores[2]);
                System.out.println(scores[3]);
                //....
                System.out.println(scores[9]);
                */
                //将数组中的每个元素进行查看--》数组的遍历：
                //方式1：普通for循环---》正向遍历：
                for(int i=0;i<=9;i++){
                        System.out.println("第"+(i+1)+"个学生的成绩为："+scores[i]);
                }
                
                //方式2：增强for循环:
                //对scores数组进行遍历，遍历出来每个元素都用int类型的num接收：
                int count = 0;
                for(int num:scores){
                        count++;
                        //每次都将num在控制台输出
                        System.out.println("第"+count+"个学生的成绩为："+num);
                }
                
                /*
                增强for循环：
                优点：代码简单
                缺点：单纯的增强for循环不能涉及跟索引相关的操作
                */
                
                //方式3：利用普通for循环---》逆向遍历：
                for(int i=9;i>=0;i--){
                        System.out.println("第"+(i+1)+"个学生的成绩为："+scores[i]);
                }
                
        }
}
```

【2】用IDEA验证数组的确将数据进行存储了：

![image-20210105003105441](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105003105441.png)

# 四、数组的三种初始化方式

数组的初始化方式总共有三种：静态初始化、动态初始化、默认初始化。



**静态初始化**
除了用new关键字来产生数组以外，还可以直接在定义数组的同时就为数组元素分配空间并赋值。

eg:
int[] arr = {12,23,45};
int[] arr = new int[]{12,23,45};
注意：
1.new int[3]{12,23,45};-->错误
2.int[] arr ;
   arr = {12,23,45};  --->错误



**动态初始化**
数组定义与为数组元素分配空间并赋值的操作分开进行。

eg:
int[] arr ;
arr = new int[3]
arr[0] = 12;
arr[1] = 23;
arr[2] = 45;

**默认初始化**
数组是引用类型，它的元素相当于类的实例变量，因此数组一经分配空间，其中的每个元素也被按照实例变量同样的方式被隐式初始化。

int[] arr = new int[3];   ---> 数组有默认的初始化值    

![image-20210105174123763](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105174123763.png)

# 五、数组的应用题

## 1.最值问题

【1】实现一个功能：给定一个数组int[] arr = {12,3,7,4,8,125,9,45}; ，求出数组中最大的数。
思路图：

![image-20210105003143532](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105003143532.png)

```java
public class TestArray04{
    public static void main(String[] args){
                //实现一个功能：给定一个数组int[] arr = {12,3,7,4,8,125,9,45}; ，求出数组中最大的数。
                //1.给定一个数组
                int[] arr = {12,3,7,4,8,125,9,45,666,36};
                
                //2.求出数组中的最大值：
                //先找一个数上擂台，假定认为这个数最大：
                int maxNum = arr[0];
                for(int i=0;i<arr.length;i++){
                        if(arr[i]>maxNum){
                                maxNum = arr[i];
                        }
                }
                System.out.println("当前数组中最大的数为："+maxNum);
                
        }
}
```

![image-20210105175540696](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105175540696.png)

【2】将求最大值的方法提取出来：

```java
public class TestArray04{
    public static void main(String[] args){
                //实现一个功能：给定一个数组int[] arr = {12,3,7,4,8,125,9,45}; ，求出数组中最大的数。
                //1.给定一个数组
                int[] arr = {12,3,7,4,8,725,9,45,666,36};
                
                //2.求出数组中的最大值：
                //调用方法：
                int num = getMaxNum(arr);
                System.out.println("当前数组中最大的数为："+num);
        }
        
        /*
        想提取一个方法：求数组中的最大值
        求哪个数组中的最大值 ---》不确定因素：哪个数组 (形参)---》返回值：最大值
        */
        public static int getMaxNum(int[] arr){
                //先找一个数上擂台，假定认为这个数最大：
                int maxNum = arr[0];
                for(int i=0;i<arr.length;i++){
                        if(arr[i]>maxNum){
                                maxNum = arr[i];
                        }
                }
                return maxNum;
                
        }
}
```

![](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105175540696.png)

【3】画内存：
方法的实参传递给形参的时候一定要注意：一切都是值传递：
如果是**基本数据类型**，那么传递的就是**字面值**
如果是**引用数据类型**，那么传递的就是**地址值**

![image-20210105175819981](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105175819981.png)

## 2.查询问题

【1】查询指定位置的元素

```java
public class TestArray05{
    public static void main(String[] args){
                //查询指定位置的元素
                //给定一个数组：
                int[] arr = {12,34,56,7,3,10};
                //查找索引为2的位置上对应的元素是什么？
                System.out.println(arr[2]);
        }
}
```

![image-20210105203707821](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105203707821.png)

上面代码体现了数组的一个优点：
在按照位置查询的时候，直接一步到位，**效率非常高**

【2】查询指定元素的位置-----》找出元素对应的索引 

```java
public class TestArray06{
    public static void main(String[] args){
                //查询指定元素的位置--》找出元素对应的索引 
                //给定一个数组：
                int[] arr = {12,34,56,7,3,56};
                //           0  1  2  3 4  5
                
                //功能：查询元素888对应的索引：
                int index = -1; //这个初始值只要不是数组的索引即可
                for(int i=0;i<arr.length;i++){
                        if(arr[i]==12){
                                index = i;//只要找到了元素，那么index就变成为i
                                break;//只要找到这个元素，循环就停止
                        }
                }
                if(index!=-1){
                        System.out.println("元素对应的索引："+index);
                }else{//index==-1
                        System.out.println("查无次数！");
                }
        }
}
```

![image-20210105221951834](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105221951834.png)

【3】将查指定元素对应的索引的功能提取为方法：

```java
public class TestArray06{
    public static void main(String[] args){
                //查询指定元素的位置--》找出元素对应的索引 
                //给定一个数组：
                int[] arr = {12,34,56,7,3,56};
                //           0  1  2  3 4  5
                
                //功能：查询元素888对应的索引：
                //调用方法：
                int index = getIndex(arr,999);
                //后续对index的值进行判断：
                if(index!=-1){
                        System.out.println("元素对应的索引："+index);
                }else{//index==-1
                        System.out.println("查无次数！");
                }
        }
        
        /*
        定义一个方法：查询数组中指定的元素对应的索引：
        不确定因素：哪个数组，哪个指定元素  （形参）
        返回值：索引
        
        */
        public static int getIndex(int[] arr,int ele){
                int index = -1; //这个初始值只要不是数组的索引即可
                for(int i=0;i<arr.length;i++){
                        if(arr[i]==ele){
                                index = i;//只要找到了元素，那么index就变成为i
                                break;//只要找到这个元素，循环就停止
                        }
                }
                return index;
        }
}
```

![image-20210105222100675](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105222100675.png)

## 3.添加元素

【1】实现一个功能： 
添加逻辑：

![image-20210105003341066](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105003341066.png)

```java
public class TestArray07{
    public static void main(String[] args){
                //功能：给定一个数组,在数组下标为2的位置上添加一个元素91
                
                //1.给定一个数组：
                int[] arr = {12,34,56,7,3,10,55,66,77,88,999,89};
                //           0  1   2 3 4 5
                //2.输出增加元素前的数组：
                System.out.print("增加元素前的数组：");
                for(int i=0;i<arr.length;i++){
                        if(i!=arr.length-1){
                                System.out.print(arr[i]+",");
                        }else{//i==arr.length-1 最后一个元素不用加,
                                System.out.print(arr[i]);
                        }
                }
                
                //3.增加元素
                /*
                arr[5] = arr[4];
                arr[4] = arr[3];
                arr[3] = arr[2];
                */
                int index = 1;//在这个指定位置添加 元素
                for(int i=arr.length-1;i>=(index+1);i--){
                        arr[i] = arr[i-1];
                }
                arr[index] = 666;
                
                
                //4.输出增加元素后的数组：
                System.out.print("\n增加元素后的数组：");
                for(int i=0;i<arr.length;i++){
                        if(i!=arr.length-1){
                                System.out.print(arr[i]+",");
                        }else{//i==arr.length-1 最后一个元素不用加,
                                System.out.print(arr[i]);
                        }
                }
                
        }	
}
```

![image-20210105223323209](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105223323209.png)

【2】将添加功能提取为一个 方法：

```java
import java.util.Scanner;
public class TestArray07{
    public static void main(String[] args){
                //功能：给定一个数组,在数组下标为2的位置上添加一个元素91
                
                //1.给定一个数组：
                int[] arr = {12,34,56,7,3,10,55,66,77,88,999,89};
                //           0  1   2 3 4 5
                //2.输出增加元素前的数组：
                /*
                System.out.print("增加元素前的数组：");
                for(int i=0;i<arr.length;i++){
                        if(i!=arr.length-1){
                                System.out.print(arr[i]+",");
                        }else{//i==arr.length-1 最后一个元素不用加,
                                System.out.print(arr[i]);
                        }
                }
                */
                
                //从键盘接收数据：
                Scanner sc = new Scanner(System.in);
                System.out.println("请录入你要添加元素的指定下标：");
                int index = sc.nextInt();
                System.out.println("请录入你要添加的元素：");
                int ele = sc.nextInt();
                
                //3.增加元素
                //调用方法：
                insertEle(arr,index,ele);
                
                
                
                //4.输出增加元素后的数组：
                System.out.print("\n增加元素后的数组：");
                for(int i=0;i<arr.length;i++){
                        if(i!=arr.length-1){
                                System.out.print(arr[i]+",");
                        }else{//i==arr.length-1 最后一个元素不用加,
                                System.out.print(arr[i]);
                        }
                }
                
        }	
        
        
        /*
        提取一个添加元素的方法：
        在数组的指定位置上添加一个指定的元素。
        在哪个数组的哪个位置添加哪个元素！
        不确定因素：形参：哪个数组，哪个位置，哪个元素
        返回值：无
        
        */
        public static void insertEle(int[] arr,int index,int ele){
                for(int i=arr.length-1;i>=(index+1);i--){
                        arr[i] = arr[i-1];
                }
                arr[index] = ele;
        }
}
```

![](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105223323209.png)

## 4.删除元素

【1】实现一个功能：删除指定位置上的元素
逻辑：

![image-20210105003414696](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105003414696.png)

```java
import java.util.Arrays;
public class TestArray08{
    public static void main(String[] args){
                //功能：给定一个数组,删除下标为2元素
                
                //1.给定一个数组：
                int[] arr = {12,34,56,7,3,10,34,45,56,7,666};
                //           0  1   2 3 4 5
                //2.输出删除前的数组：
                System.out.println("删除元素前的数组："+Arrays.toString(arr));
                
                //3.删除
                /*
                arr[2] = arr[3];
                arr[3] = arr[4];
                arr[4] = arr[5];
                */
                int index = 0;
                for(int i=index;i<=arr.length-2;i++){
                        arr[i] = arr[i+1];
                }
                arr[arr.length-1] = 0;
                
                //4.输出删除后的数组：
                System.out.println("删除元素后的数组："+Arrays.toString(arr));
        }
}
```

![image-20210106002512438](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210106002512438.png)



【2】实现一个功能：删除指定元素

```java
import java.util.Arrays;
public class TestArray09{
    public static void main(String[] args){
                //功能：给定一个数组,删除元素3：
                
                //1.给定一个数组：
                int[] arr = {12,34,56,7,3,10,34,45,56,7,666};
                 
                //2.输出删除前的数组：
                System.out.println("删除元素前的数组："+Arrays.toString(arr));
                
                
                //找到要删除的元素对应的索引即可：
                int index = -1 ;
                for(int i=0;i<arr.length;i++){
                        if(arr[i]==1200){
                                index = i;
                                break;
                        }
                }
                
                //3.删除
                
                if(index!=-1){
                        for(int i=index;i<=arr.length-2;i++){
                                arr[i] = arr[i+1];
                        }
                        arr[arr.length-1] = 0;
                }else{//index==-1
                        System.out.println("根本没有你要删除的元素！");
                }
                
                
                //4.输出删除后的数组：
                System.out.println("删除元素后的数组："+Arrays.toString(arr));
        }
}
```



# 六、详述main方法

【1】main方法：程序的入口，在同一个类中，如果有多个方法，那么虚拟机就会识别main方法，从这个方法作为程序的**入口**
【2】main方法格式严格要求：
public static void main(String[] args){}

public static --->修饰符 ，暂时用这个 -->面向对象一章
void --->代表方法没有返回值 对应的类型void
main --->见名知意名字
String[] args  --->形参  ---》不确定因素

【3】问题：程序中是否可以有其他的方法也叫main方法？
可以，构成了**方法的重载**。

```java
public class TestArray10{
    public static void main(String[] args){
                
        }
        public static void main(String str){
                
        }
}
```

【4】形参为String[] 那么实参到底是什么？

```java
public class TestArray10{
    public static void main(String[] args){
                //从侧面验证：
                //int[] arr1; //如果对数组只声明，没有后续操作，那么相当于 白定义了。
                //int[] arr2 = null; 
                //System.out.println(arr2.length);//Exception in thread "main" java.lang.NullPointerException
                //int[] arr3 = new int[0];
                //System.out.println(arr3.length);
                //int[] arr4 = new int[4];
                //System.out.println(arr4.length);
                
                //System.out.println(args.length);//0
                //从这个结果证明，参数是String[],实参是  new String[0] 
                //默认情况下，虚拟机在调用main方法的时候就是传入了一个长度为0的数组
                
                System.out.println(args.length);
                for(String str:args){
                        System.out.println(str);
                }
        }
}
```

手动传入实参：
有特殊符号的时候可以加上“”

![image-20210106003733044](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210106003733044.png)

没有特殊符号用空格隔开即可：

![image-20210106003705040](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210106003705040.png)

# 七、可变参数

```java
public class TestArray12{
        /*
        1.可变参数：作用提供了一个方法，参数的个数是可变的 ,解决了部分方法的重载问题
        int...num
        double...num
        boolean...num
        
        
        2.可变参数在JDK1.5之后加入的新特性
        3.方法的内部对可变参数的处理跟数组是一样
        4.可变参数和其他数据一起作为形参的时候，可变参数一定要放在最后
        5.我们自己在写代码的时候，建议不要使用可变参数。
        */
    public static void main(String[] args){
                //method01(10);
                //method01();
                //method01(20,30,40);
                method01(30,40,50,60,70);
                //method01(new int[]{11,22,33,44});
        }
        public static void method01(int num2,int...num){
                System.out.println("-----1");
                for(int i:num){
                        System.out.print(i+"\t");
                }
                System.out.println();
                
                System.out.println(num2);
        }
}
```

![image-20210106004241093](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210106004241093.png)



# 八、Arrays工具类

为了方便我们对数组进行操作，系统提供一个类**Arrays**，我们将它当做工具类来使用。

```java
import java.util.Arrays;
public class TestArray13{
        public static void main(String[] args){
                //给定一个数组：
                int[] arr = {1,3,7,2,4,8};
                //toString:对数组进行遍历查看的，返回的是一个字符串，这个字符串比较好看
                System.out.println(Arrays.toString(arr));
                
                //binarySearch:二分法查找：找出指定数组中的指定元素对应的索引：
                //这个方法的使用前提：一定要查看的是一个有序的数组：
                //sort：排序 -->升序
                Arrays.sort(arr);
                System.out.println(Arrays.toString(arr));
                System.out.println(Arrays.binarySearch(arr,4));
                
                int[] arr2 = {1,3,7,2,4,8};
                //copyOf:完成数组的复制：
                int[] newArr = Arrays.copyOf(arr2,4);
                System.out.println(Arrays.toString(newArr));
                
                //copyOfRange:区间复制：
                int[] newArr2 = Arrays.copyOfRange(arr2,1,4);//[1,4)-->1,2,3位置
                System.out.println(Arrays.toString(newArr2));
                
                //equals:比较两个数组的值是否一样：
                int[] arr3 = {1,3,7,2,4,8};
                int[] arr4 = {1,3,7,2,4,8};
                System.out.println(Arrays.equals(arr3,arr4));//true
                System.out.println(arr3==arr4);//false ==比较左右两侧的值是否相等，比较的是左右的地址值，返回结果一定是false
                
                //fill：数组的填充：
                int[] arr5 = {1,3,7,2,4,8};
                Arrays.fill(arr5,10);
                System.out.println(Arrays.toString(arr5));
        }
}
```



# 九、数组的复制操作

原理：

![image-20210105003624521](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105003624521.png)

![image-20210105003633442](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105003633442.png)

![image-20210105003644034](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105003644034.png)

代码：

```java
import java.util.Arrays;
public class TestArray14{
        public static void main(String[] args){
                //给一个源数组：
                int[] srcArr = {11,22,33,44,55,66,77,88};
                //给一个目标数组：
                int[] destArr = new int[10];
                
                //复制：
                System.arraycopy(srcArr,1,destArr,3,3);
                //遍历查看目标数组：
                System.out.println(Arrays.toString(destArr));
        }
        
}
```

结果：

![image-20210105003705879](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105003705879.png)

# 十、二维数组

【1】引入：本质上全部都是一维数组：

![image-20210105003724861](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210105003724861.png)


【2】基本代码：

```java
public class TestArray15{
        public static void main(String[] args){
                //定义一个二维数组：
                int[][] arr = new int[3][];//本质上定义了一个一维数组，长度为3
                
                int[] a1 = {1,2,3};
                arr[0] = a1;
                
                arr[1] = new int[]{4,5,6,7};
                
                arr[2] = new int[]{9,10};
        }
}
```

对应内存：

![image-20210105003747204](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210105003747204.png)

【3】四种遍历方式：

```java
public class TestArray15{
        public static void main(String[] args){
                //定义一个二维数组：
                int[][] arr = new int[3][];//本质上定义了一个一维数组，长度为3
                
                int[] a1 = {1,2,3};
                arr[0] = a1;
                
                arr[1] = new int[]{4,5,6,7};
                
                arr[2] = new int[]{9,10};
                
                //读取6这个元素：
                //System.out.println(arr[1][2]);
                
                //对二维数组遍历：
                //方式1：外层普通for循环+内层普通for循环：
                for(int i=0;i<arr.length;i++){
                        for(int j=0;j<arr[i].length;j++){
                                System.out.print(arr[i][j]+"\t");
                        }
                        System.out.println();
                }
                
                //方式2：外层普通for循环+内层增强for循环：
                for(int i=0;i<arr.length;i++){
                        for(int num:arr[i]){
                                System.out.print(num+"\t");
                        }
                        System.out.println();
                }
                
                //方式3：外层增强for循环+内层增强for循环：
                for(int[] a:arr){
                        for(int num:a){
                                System.out.print(num+"\t");
                        }
                        System.out.println();
                }
                
                //方式4：外层增强for循环+内层普通for循环：
                for(int[] a:arr){
                        for(int i=0;i<a.length;i++){
                                System.out.print(a[i]+"\t");
                        }
                        System.out.println();
                }
        }
}
```

![image-20210106115113566](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210106115113566.png)



# 十一、二维数组的初始化方式

数组的初始化方式总共有三种：静态初始化、动态初始化、默认初始化。

**静态初始化**
除了用new关键字来产生数组以外，还可以直接在定义数组的同时就为数组元素分配空间并赋值。

eg:
int[][] arr = {{1,2},{4,5,6},{4,5,6,7,8,9,9}};
int[][] arr =new int[][] {{1,2},{4,5,6},{4,5,6,7,8,9,9}};
**动态初始化**
数组定义与为数组元素分配空间并赋值的操作分开进行。
eg:
int[][] arr = new int`[3][]`; //本质上定义了一维数组长度为3，每个“格子”中放入的是一个数组
arr[0] = {1,2};
arr[1] = {3,4,5,6};
arr[2] = {34,45,56};

eg:

```java
int[][] arr = new int[3][2]; 
public class TestArray16{
        public static void main(String[] args){
                int[][] arr = new int[3][2];
                //本质上：定义一维数组，长度为3，每个数组“格子”中，有一个默认的长度为2的数组：

                arr[1] = new int[]{1,2,3,4};

                //数组遍历：
                for(int[] a:arr){
                        for(int num:a){
                                        System.out.print(num+"\t");
                        }
                        System.out.println();
                }

        }
}
```

![image-20210106115300186](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210106115300186.png)

**默认初始化**
数组是引用类型，它的元素相当于类的实例变量，因此数组一经分配空间，其中的每个元素也被按照实例变量同样的方式被隐式初始化。