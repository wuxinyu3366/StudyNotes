# Java集合框架-------Java容器

**面向接口编程**

为什么使用集合框架（引入）

对象的容器，实现了对对象常用的操作

数组Arrays---》一组相同类别的数组组成的----》初始化声明了长度，长度固定了------》需要一个可扩容的容器

数组---》可以存储基本类型和引用类型，集合----》只能存储引用类型

如果并不知道程序运行时会需要多少对象，或者需要 更复杂方式存储对象

——可以使用**Java集合框架**

# 一、容器的概念

Java集合框架提供了一套性能优良、使用方便的接口和类，它们位于**java.util**包中

![image-20210109061248678](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210109061248678.png)

java.util.concurrent  简称  **JUC**  的学习   ----->并发

接口：Collection 	List	 Set 	Map

子类实现：ArrayList 	LinkedList 	HashSet	 TreeSet 	HashMap 	TreeMap



区别：

▪ Collection 接口存储一组**不唯一，无序**的对象 

▪ List 接口存储一组**不唯一，有序（插入顺序）**的对象 

▪ Set 接口存储一组**唯一，无序**的对象 

▪ Map接口存储一组**键值对象**，提供key到value的**映射**

# 二、容器API

# 三、Collection接口

【1】java集合框架：

**Collection**：	存放的是单一值

​							代表一组任意类型的对象，**无序、无下标、不能重复**。

【2】创建集合:

```java
Collection collection = new ArrayList();
```



【3】特点：

1、可以存放**不同类型**的数据，而数组只能存放固定类型的数据

2、当使用Arraylist子类实现的时候，**初始化的长度是10**，当长度不够的时候会**自动进行扩容**操作 （public static final int DEFAULT_CAPACITY=10;）



## API方法：

1.增加数据的方法

| 方法                                        | 说明                                                         |
| ------------------------------------------- | ------------------------------------------------------------ |
| `boolean  add(E e)`                         | 要求必须传入的参数是**Object**对象，因此当写入**基本数据类型**的时候，包含了**自动拆箱和自动装箱**的过程 |
| `boolean addAll(Collection<? extends E> c)` | 添加**另一个集合**的**元素**到此集合中                       |

2.删除数据的方法

| 方法                                 | 说明                                                       |
| ------------------------------------ | ---------------------------------------------------------- |
| `void clear()`                       | 只是**清空集合中的元素**，但是此集合**对象并没有被回收**   |
| `boolean remove(Object o)`           | 从该集合中删除指定元素的单个实例（如果存在）（可选操作）。 |
| `boolean removeAll(Collection<?> c)` | 删除指定集合中包含的所有此集合的元素（可选操作）。         |

3.查询数据的方法

| 方法                                   | 说明                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| `boolean contains(Object o)`           | 如果此集合包含指定的元素，则返回 `true` 。                   |
| `boolean containsAll(Collection<?> c)` | 如果此集合包含指定 `集合`中的所有元素，则返回true。          |
| `boolean isEmpty()`                    | 如果此集合不包含元素，则返回 `true` 。                       |
| `boolean retainAll(Collection<?> c)`   | 仅保留此集合中包含在指定集合中的元素（可选操作）。 若集合中拥有另一个集合的所有元素，返回true，否则返回false |
| `int size()`                           | 返回此集合中的元素数。                                       |

集合转数组的操作

| 方法                 | 说明                                     |
| -------------------- | ---------------------------------------- |
| `Object[] toArray()` | 返回一个包含此集合中所有元素的**数组**。 |

【5】案例代码

```java
package com.mashibing;

import java.util.ArrayList;
import java.util.Collection;

/**
 * @author: 马士兵教育
 * @create: 2019-09-07 21:21
 */
public class CollectionDemo {
    public static void main(String[] args) {
        Collection collection = new ArrayList();
        collection.add(1);	//看似是1，实际上new Integer 自动装箱的功能
        collection.add(true);
        collection.add(1.23);
        collection.add("abc");	//可以添加不同的数据类型，这与数组是不同的
        System.out.println(collection);//[1, true, 1.23, abc]
        ((ArrayList) collection).add(0,"mashibing");
        System.out.println(collection);//[mashibing, 1, true, 1.23, abc]
        Collection collection1 = new ArrayList();
        collection1.add("a");
        collection1.add("b");
        collection1.add("c");
        collection1.add("d");
        collection.addAll(collection1);
        System.out.println(collection);//[mashibing, 1, true, 1.23, abc, a, b, c, d]
//        collection.clear();
//        System.out.println(collection);//[]
        System.out.println(collection.contains("a"));//true
        System.out.println(collection.containsAll(collection1));//true
        System.out.println(collection.isEmpty());//false
//        collection.remove("a");
//        System.out.println(collection); //[mashibing, 1, true, 1.23, abc, b, c, d]
        System.out.println(collection1.retainAll(collection));//flase
        Object[] objects = collection.toArray(); //集合转成了数组
        collection.add("a");
        System.out.println(collection);//[mashibing, 1, true, 1.23, abc, a, b, c, d, a]


    }
}

```



# 四、Iterator接口

【1】特点：
所有实现了Collection接口的容器类都有一个**iterator方法**用以返回一个实现了Iterator接口的对象，该对象拥有对集合遍历操作的能力，实际上是有了一个指向第一个头的游标。

 Iterator对象称作**迭代器**，用以方便的实现对**容器内元素**的**遍历操作**。

【2】 Iterator接口定义了如下方法：

```java
boolean hasNext(); //判断是否有元素没有被遍历
Object next(); //返回游标当前位置的元素并将游标移动到下一个位置
void remove(); //删除游标左面的元素，在执行完next之后该
								//操作只能执行一次
```

![image-20210109161404043](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210109161404043.png)

【3】可以使用Iterator遍历的本质是什么？

​			实现Iterable接口

【4】Iterator迭代器的使用案例

```java
 //Iterator迭代器
        Iterator iterator = list.iterator();
//        ListIterator iterator = list.listIterator();
        while(iterator.hasNext()){
            Object o = iterator.next();
            if(o.equals(1)){
                iterator.remove();
            }
            System.out.println(o);
        }
```

对比其他两种遍历方式

```java
//1.普通的for循环-------------------------------《《《1
        for(int i=0;i<list.size();i++){
            System.out.println(list.get(i));
        }
//2.增强的for循环-------------------------------《《《2
//        for(Object i : list){
//            System.out.println(i);
//        }
```



【5】for-each的使用

【6】为什么需要ListIterator

​		在迭代过程中，准备添加或者删除元素

```java
ArrayList al=new ArrayList();
        al.add("java1");//添加元素
        al.add("java2");
        al.add("java3");
//遍历
        Iterator it=al.iterator();
        while(it.hasNext()){
            Object obj=it.next();
            if (obj.equals("java2")) {
                al.add("java9");
            }
            sop("obj="+obj);
        }
```

​		在迭代时，不可能通过集合对象的方法(al.add(?))操作集合中的元素，会发生并发修改异常。 

 所以，在**迭代**时只能通过迭代器的方法操作元素，但是Iterator的方法是有限的，只能进行判断(hasNext)，取出(next),删除(remove)的操作，

如果想要在迭代的过程中进行向集合中添加，修改元素等就需要使用**ListIterator接口**中的方法

```java
ListIterator li=al.listIterator();
        while(li.hasNext()){
            Object obj=li.next();
            if ("java2".equals(obj)) {
                li.add("java9994");
                li.set("java002");
            }
        }
```



## Iterator接口的应用

```java
package com.mashibing;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.ListIterator;

/**
 * @author: 马士兵教育
 * @create: 2019-09-08 15:42
 */
/**
* 在java代码中包含三种循环的方式
*   do...while
*   while
*   for
* 还有一种增强for循环的方式，可以简化循环的编写
*
*
*   所有的集合类都默认实现了Iterable的接口，实现此接口意味着具备了增强for循环的能力，也就是for-each
*      增强for循环本质上使用的也是iterator（迭代器的）的功能
*      方法：
*               iterator()
*               foreach()
*   在iterator的方法中，要求返回一个Iterator的接口子类实例对象，该对象拥有遍历集合的能力
实际上实例的是在集合中定义的一个可以实例化的内部类Itr（对接口的实现），因为接口是不能实例化的
*       此接口中包含了下列方法，拥有了增强for循环的能力
*               hasNext()
*               next()
*
*   在使用iterator进行迭代的过程中如果删除其中的某个元素会报错，并发操作异常，因此
*       如果遍历的同时需要修改元素，建议使用listIterator（），
*   ListIterator迭代器提供了向前和向后两种遍历的方式
*       始终是通过cursor和lastret的指针来获取元素值及向下的遍历索引
*       当使用向前遍历的时候必须要保证指针在迭代器的结果，否则无法获取结果值
* */
public class IteratorDemo {
    public static void main(String[] args) {
        ArrayList list= new ArrayList();
        list.add(1);
        list.add(2);
        list.add(3);
        list.add(4);
      	//1.普通的for循环-------------------------------《《《1
        for(int i=0;i<list.size();i++){
            System.out.println(list.get(i));
        }

        //3.Iterator迭代器-------------------------------《《《3
        Iterator iterator = list.iterator();
//        ListIterator iterator = list.listIterator();
        while(iterator.hasNext()){
            Object o = iterator.next();
            if(o.equals(1)){
                iterator.remove();
            }
            System.out.println(o);
        }
//        System.out.println("-------------");
//        while (iterator.hasPrevious()){
//            System.out.println(iterator.previous());
//        }
      		//2.增强的for循环-------------------------------《《《2
//        for(Object i : list){
//            System.out.println(i);
//        }
    }
}
```



# 五、Iterable接口

- ```
  public interface Iterable<T>
  ```

  实现此接口允许对象成为“for-each loop”语句的目标。

![image-20210109173313557](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210109173313557.png)

# 六、Set接口

【1】Set接口：

​	 Set接口存储一组**唯一，无序**的对象（存入和取出的顺序不一定一致）

​	特点：无序、无下标、元素不可重复

​	方法：全部继承自Collection中的方法

​	增、删、遍历、判断与collection一致，Set中没有get()方法

![image-20210109172739943](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210109172739943.png)

## Set接口中的实现类

### HashSet

存储结构：哈希表（数组+链表+红黑树）（1.8）

​	–优点：添加速度快，查询速度快，删除速度快

​	–缺点：无序

问题：**HashSet是如何保证元素的唯一性的呢?**

答:是通过元素的两个方法,hashCode和equals方法来完成 

​	1.如果元素的HashCode值相同，才会判断equals是否为true 

​	 2.如果元素的hashCode值不同，不会调用equals方法

存储过程（**重复依据**，所以会重写hashCode和equals方法）

1. 根据**hashCode**计算保存的位置，如果位置为空，直接保存，若不为空，进行第二步

2. 再执行**equals方法**，如果equals为true，则认为是重复，否则形成链表

   ![image-20210109173442971](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210109173442971.png)

特点：

- 基于HashCode计算元素存放位置
  - 利用31这个质数，减少散列冲突
    - 31提高执行效率 `31 * i = (i << 5) - i` 转为移位操作
  - 当存入元素的哈希码相同时，会调用equals进行确认，如果结果为true，则拒绝后者存入

【1】新建集合 `HashSet<String> hashSet = new HashSet<String>();`

【2】添加元素 `hashSet.add( );`

```java
HashSet hs=new HashSet();//创建HashSet对象
hs.add(new Person("张三",20));
```

【3】删除元素 `hashSet.remove( );`

【4】遍历操作

1. 增强for `for( type type : hashSet)`

   ```java
   Iterator iterator = set.iterator();
   while (iterator.hasNext()){
               System.out.println(iterator.next());
           }
   ```

2. 迭代器 `Iterator<String> it = hashSet.iterator( );`

   ```java
   //将while循环改成for循环,推荐使用
           for(Iterator iter = set.iterator(); iter.hasNext();){
               System.out.println(iter.next());
           }
   ```

   

【5】判断 `hashSet.contains( );` `hashSet.isEmpty();`

【6】重写equals()方法和hashCode()方法

```java
//原有的hashCode()方法
@Override
    public int hashCode() {
        System.out.println(this.name+".....hashCode");
        return 60;
    }
}
//修改后的hashCode()方法
@Override
    public int hashCode() {
        System.out.println(this.name+".....hashCode");
        return this.name.hashCode()+age;
    }
```

### TreeSet

【1】 采用二叉树（**红黑树**）的存储结构 

![image-20210109175516453](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210109175516453.png)

– 优点：**有序**（排序后的升序）查询速度比List快 

– 缺点：查询速度没有HashSet快

【2】特点

- 基于排列顺序实现元素不重复

- 实现SortedSet接口，对集合元素**自动排序**sort

  ​						（如果是基本数据类型，自动比较，如果是引用类型的话，需要自定义比较器）

- 元素对象的类型必须实现**Comparable接口**，指定**排序规则**

- 通过**CompareTo()**方法确定是否为重复元素

【3】创建集合 `TreeSet<String> treeSet = new TreeSet<>()`

【4】添加元素 `treeSet.add();`

【5】删除元素 `treeSet.remove();`

【6】遍历 1. 增强for 			2. 迭代器

【7】判断 `treeSet.contains();`

【8】补充：TreeSet集合的使用

​		Comparator 实现定制比较（比较器）

​		Comparable 可比较的

​			返回 0 表示 this == obj
 			返回正数 表示 this > obj
​			返回负数 表示 this < obj

#### 外部比较器 compare()

```java

// 1.compare()方法
//外部比较器   定义在当前类中，通过实现comparator接口来实现，但是要将该比较器传递到集合中            
public class SetDemo implements Comparator<Person> {
    public static void main(String[] args) {
    @Override
    public int compare(Person o1, Person o2) {
        if(o1.getAge()>o2.getAge()){
            return -1;
        }else if(o1.getAge() < o2.getAge()){
            return 1;
        }else{
            return 0;
        }
    }
   }
```



#### 内部比较器comparable

```java
//2.此比较器按照name的长度来进行比较(设定)
//内部比较器 定义在元素Person的类中，通过实现comparable接口来进行实现
public class Person implements Comparable{
@Override
    public int compareTo(Object o) {
        Person p  = (Person) o;
        if (p.name.length()>this.name.length()){
            return -1;
        }else if(p.name.length()<this.name.length()){
            return 1;
        }else{
            return 0;
        }
    }
}
```

​	注意：**外部比较器**可以定义成一个工具类，此时所有需要比较的规则如果一致的话，可以复用，而
*               **内部比较器**只有在存储当前对象的时候才可以使用
*               如果两者同时存在，使用**外部比较器**
*               当**使用比较器**的时候，**不会调用equals**方法

【9】案例代码

```java
package com.mashibing;

import java.util.*;

/**
 * @author: 马士兵教育
 * @create: 2019-09-08 16:36
 */
/**
*   1、set中存放的是无序，唯一的数据
*   2、set不可以通过下标获取对应位置的元素的值，因为无序的特点
*   3、使用treeset底层的实现是treemap,利用红黑树来进行实现
*   4、设置元素的时候，如果是自定义对象，会查找对象中的equals和hashcode的方法，如果没有，比较的是地址
*   5、树中的元素是要默认进行排序操作的，如果是基本数据类型，自动比较，如果是引用类型的话，需要自定义比较器
*       比较器分类：
*         内部比较器
*               定义在元素的类中，通过实现comparable接口来进行实现
*         外部比较器
*               定义在当前类中，通过实现comparator接口来实现，但是要将该比较器传递到集合中
*         注意：外部比较器可以定义成一个工具类，此时所有需要比较的规则如果一致的话，可以复用，而
*               内部比较器只有在存储当前对象的时候才可以使用
*               如果两者同时存在，使用外部比较器
*               当使用比较器的时候，不会调用equals方法
* */
public class SetDemo implements Comparator<Person> {
    public static void main(String[] args) {
//        Set set = new HashSet();
//        set.add("123");
//        set.add(1);
//        set.add(true);
//        set.add("123");
//        System.out.println(set);
//        Iterator iterator = set.iterator();
//        while (iterator.hasNext()){
//            System.out.println(iterator.next());
//        }
//        System.out.println("---------");
//        //将while循环改成for循环,推荐使用
//        for(Iterator iter = set.iterator(); iter.hasNext();){
//            System.out.println(iter.next());
//        }

//        TreeSet treeSet = new TreeSet();
//        treeSet.add(34);
//        treeSet.add(1);
//        treeSet.add(65);
//        System.out.println(treeSet.ceiling(1));
//        System.out.println(treeSet);
//        HashSet hashSet = new HashSet();
//        hashSet.add(new Person("zhangsan",12));
//        hashSet.add(new Person("zhangsan",12));
//        hashSet.add(new Person("lisi",13));
//        System.out.println(hashSet);

        TreeSet treeSet = new TreeSet(new SetDemo());
        treeSet.add(new Person("lisi",15));
        treeSet.add(new Person("wangwu",13));
        treeSet.add(new Person("maliu",12));
        treeSet.add(new Person("zhangsan",19));
        treeSet.add(new Person("zhangsan",12));
        System.out.println(treeSet);


    }
		//外部比较器
*               定义在当前类中，通过实现comparator接口来实现，但是要将该比较器传递到集合中
    @Override
    public int compare(Person o1, Person o2) {
        if(o1.getAge()>o2.getAge()){
            return -1;
        }else if(o1.getAge() < o2.getAge()){
            return 1;
        }else{
            return 0;
        }
    }
}

```



```java
package com.mashibing;

import java.util.Objects;

/**
 * @author: 马士兵教育
 * @create: 2019-09-21 15:32
 */
public class Person implements Comparable{
    private String name;
    private int age;

    public Person(){

    }

    public Person(String name, int age) {
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

  	//HashSet中重写的equals()和hashCode()方法----------------+
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Person person = (Person) o;
        return age == person.age &&
                Objects.equals(name, person.name);
    }

    @Override
    public int hashCode() {

        return Objects.hash(name, age);
    }
		//HashSet中重写的equals()和hashCode()方法----------------+
    
  /**
  	*TreeSet中实现Comparable接口的compareTo(Object o)方法s----------------+
     * 此比较器按照name的长度来进行比较(设定)
     * @param o
     * @return
     */
    @Override
    public int compareTo(Object o) {
        Person p  = (Person) o;
        if (p.name.length()>this.name.length()){
            return -1;
        }else if(p.name.length()<this.name.length()){
            return 1;
        }else{
            return 0;
        }
    }
		//TreeSet中实现Comparable接口的compareTo(Object o)方法s----------------+
    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}

```



# 七、Comparable接口

【1】Comparable接口的引入

TreeSet中

基于排列顺序实现元素不重复实现SortedSet接口，对集合元素**自动排序**sort						

（如果是基本数据类型，自动比较，如果是引用类型的话，需要自定义比较器）

元素对象的类型必须实现**Comparable接口**，指定**排序规则**

通过**CompareTo()**方法确定是否为重复元素

【2】问题：上面的算法根据什么确定集合中对象的“大小”顺序？

 			所有可以“排序”的类都实现了java.lang.Comparable 接口

【3】特点

只有一个方法   int compareTo(T o);

```java
public int compareTo(T o);
  将此对象与指定的对象进行比较以进行排序。 返回一个负整数，零或正整数，因为该对象小于，等于或大于指定对象。 实现程序必须确保sgn(x.compareTo(y)) == -sgn(y.compareTo(x))所有x和y。 
    （这意味着x.compareTo(y)必须抛出异常iff y.compareTo(x)引发异常。） 
    返回 0 表示 this == obj
 		返回正数 表示 this > obj
		返回负数 表示 this < obj

```

【4】

# 八、List接口

![image-20210109124806267](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210109124806267.png)

【1】特点：有序、有下标、元素可重复

【2】创建集合对象:

```java
List list = new ArrayList<>( );
```

## List接口常用方法

1.添加元素 `list.add( );` 会对基本类型进行自动装箱

2.删除元素 可以用索引 `list.remove(0)`

​	当删除数字与索引矛盾时 对数字强转

```java
list.remove((Object) 10)    list.remove(new Integer(10))
```

3.遍历

- 使用for循环

```java
for(int i = 0; i < lise.size(); i++){
  sout(list.get(i)); 
}
```

- 使用增强for

```java
for(Object list: collection){ }
```

- 使用迭代器

```java
Iterator it = collection.iterator();
while(it.hasNext()){
  String object = (String)it.next(); //强转
  // 可以使用it.remove(); 进行移除元素
  // collection.remove(); 不能用collection其他方法 会报并发修改异常
}
```

4.使用列表迭代器

```java
ListIterator li = list.listIterator();
while(li.hasNext()){
  System.out.println(li.nextIndex() + ":" + li.next()); //从前往后遍历
}

while(li.hasPrevious()){
  System.out.println(li.previousIndex() + ":" + li.previous()); //从后往前遍历
}
```

5.获取

```java
list.indexOf( );
```

6.返回子集合	

```java
sublist(x, y); //左闭右开
List subList = list.subList(1, 3); //返回索引 1、2
```

【3】方法使用案例

```java
package com.mashibing;

import java.util.ArrayList;
import java.util.Collection;
import java.util.List;

/**
 * @author: 马士兵教育
 * @create: 2019-09-07 21:21
 */
/**
* java集合框架：
*   List：存放的是单一值
*       特点：
*           1、可以存放不同类型的数据，而数组只能存放固定类型的数据
*           2、当使用arraylist子类实现的时候，初始化的长度是10，当长度不够的时候会自动进行扩容操作
*       api方法：
*           增加数据的方法
*           add：要求必须传入的参数是Object对象，因此当写入基本数据类型的时候，包含了自动拆箱和自动装箱的过程
*           addAll:添加另一个集合的元素到此集合中
*
*           删除数据的方法
*           clear:只是清空集合中的元素，但是此集合对象并没有被回收
*           remove:删除指定元素
*           removeAll：删除集合元素
*
*           查询数据的方法
*           contains:判断集合中是否包含指定的元素值
*           containsAll:判断此集合中是否包含另一个集合
*           isEmpty:判断集合是否等于空
*           retainAll:若集合中拥有另一个集合的所有元素，返回true，否则返回false
*           size:返回当前集合的大小
*
*           //集合转数组的操作
*           toArray:将集合转换成数组
* */
public class ListDemo {
    public static void main(String[] args) {
        List list = new ArrayList();
        list.add("a");
        list.add(1);
        list.add("a");
        list.add(true);
        System.out.println(list);	//[a, 1, a, true]
//        System.out.println(list.get(3));
        System.out.println(list.indexOf("a"));	//0
        System.out.println(list.lastIndexOf("a"));	//2
        list.set(0,"mashibing");		//插入元素
        System.out.println(list);		//[mashibing, 1, a, true]
        List list1 = list.subList(0, 2);
        System.out.println(list1);	//[mashibing, 1] 左闭右开
//        List of = List.of(1,2,3,4);
//        System.out.println(of);   //[1, 2, 3, 4]
    }
}

```

【5】总结

List特点:有序，不唯一（可重复）的数据

|      | 方法名                                                       | 说明                                                         |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 增   | add(index,element) addAll(index,Collection) addAll(Collection) | 在指定索引的位置上插入元素        对基本类型进行自动装箱                                                                                                 在指定的引的位置上插入整个集合的元素                                                                                      在结束插入整个集合的元素 |
| 删   | remove(index)                                                | 根据索引删除指定的元素                                       |
| 改   | set(index,element)                                           | 使用element替换指定索引位置上的元素                          |
| 查   | get(index) subList(from,to) listIterator();                  | 获取元素                                                     |



## List接口的实现类

### ArrayList

实现了**长度可变的数组**，在内存中**分配连续的空间**。 

- 数组结构实现，必须要连续空间，查询快、增删慢
- jdk1.2版本，运行效率块、线程不安全

– 优点：遍历元素和随机访问元素的效率比较高 

– 缺点：添加和删除需要大量移动元素效率低，按照内容查询效率低，

![image-20210109130227909](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210109130227909.png)

【1】创建集合

```java
ArrayList arrayList = new ArrayList<>();
```

【2】添加&删除元素

```java
arrayList.add();//添加元素 
arrayList.remove(new Student("name", 10));//删除元素 

//重写equals(this == obj) 方法
public boolean equals(Object obj){
  //1 判断是不是同一个对象
  if(this == obj){
    return true;
  }
  //2 判断是否为空
  if(obj == null){
    return false;
  }
  //3 判断是否是Student类型
  if(obj instanceof Student){
    Student == (Student)obj;
    //4 比较属性
    if(this.name.equals(s.getName()) && this.age == s.getAge()){
      return true;
    }
  }
  //5 不满足条件返回false
  return false;
}
```

【3】遍历

1. 使用迭代器

   ```java
   Iterator it = arrayList.iterator();
   while(it.hasNext()){
     Student s = (Student)it.next(); //强转
   }
   ```

2. 列表迭代器

   ```java
   ListIterator li = arrayList.listIterator();
   while(li.hasNext()){
     Student s = (Student)li.next(); //从前往后遍历
   }
   
   while(li.hasPrevious()){
     Student s = (Student)li.previous();//从后往前遍历
   }
   ```

【4】判断

```java
arrayList.contains(); 和 arrayList.isEmpty();
```

【5】查找

```java
arrayList.indexof();
```

【6】案例代码

```java
public class ListDemo {
    public static void main(String[] args) {
        List list = new ArrayList();
        list.add("a");
        list.add(1);
        list.add("a");
        list.add(true);
        System.out.println(list);	//[a, 1, a, true]
//        System.out.println(list.get(3));
        System.out.println(list.indexOf("a"));	//0
        System.out.println(list.lastIndexOf("a"));	//2
        list.set(0,"mashibing");		//插入元素
        System.out.println(list);		//[mashibing, 1, a, true]
        List list1 = list.subList(0, 2);
        System.out.println(list1);	//[mashibing, 1] 左闭右开
//        List of = List.of(1,2,3,4);
//        System.out.println(of);   //[1, 2, 3, 4]
    }
}
```



【7】源码分析

```java
DEFAULT_CAPACITY = 10; //默认容量
//注意：如果没有向集合中添加任何元素时，容量0，添加一个后，容量为10
//每次扩容是原来的1.5倍
elementData存放元素的数组
size 实际元素个数
```



### LinkedList

采用**链表存储方式**，常用方法与List一致。

- 双向链表结构实现，无需连续空间，增删快，查询慢

– 优点：插入、删除元素时效率比较高 

– 缺点：遍历和随机访问元素效率低下

![image-20210109130237351](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210109130237351.png)

```java
package com.mashibing;

import java.util.LinkedList;

/**
 * @author: 马士兵教育
 * @create: 2019-09-08 15:18
 */
/*
* linkedList拥有更加丰富的方法实，需要用的时候查询api即可，不需要记忆
*
* */
public class LinkedListDemo {
    public static void main(String[] args) {
        LinkedList linkedList = new LinkedList();
        linkedList.add(123);
        linkedList.add(false);
        linkedList.add("abc");
        System.out.println(linkedList);//[123, false, abc]
        linkedList.add(2,"mashibing");
        System.out.println(linkedList);//[123, false, mashibing, abc]
        linkedList.addFirst("1111");
        System.out.println(linkedList);//[1111, 123, false, mashibing, abc]
        linkedList.addLast("2222");		//其实与add()相同，只不过add()有返回true
        System.out.println(linkedList);//[1111, 123, false, mashibing, abc, 2222]
        System.out.println(linkedList.element());//1111
        linkedList.offer("3333");				//也是add()功能
        System.out.println(linkedList);//[1111, 123, false, mashibing, abc, 2222, 3333]


    }
}

```

### Vector

【1】Vector也是List接口的一个子类实现

【2】Vector跟ArrayList一样，底层都是使用**数组**进行实现的，增加、删除、判断ArrayList

- 数组结构实现，查询快、增删慢
- jdk1.0版本，运行

【3】面试经常问区别：

（1）ArrayList是**线程不安全**的，**效率高**，Vector是**线程安全**的，**效率低**

（2）ArrayList在进行扩容的时候，是扩容**1.5倍**，Vector扩容的时候扩容原来的**2倍**
(ArrayList扩容时>>1，右移一位，1.5倍，Vector扩容时+Vector，扩容2倍)

【4】遍历

```java
Enumeration en = vector.elements();
while(en.hasMoreElements()){
  String o = (String)en.nextElement();
  sout(o);
}
```

【5】案例代码

```java
package com.mashibing;

import java.util.Vector;

/**
 * @author: 马士兵教育
 * @create: 2019-09-08 15:34
 */
public class VectorDemo {
    public static void main(String[] args) {
        Vector vector = new Vector();
        vector.add(1);
        vector.add("abc");
        System.out.println(vector);
    }
}

```



# 九、Map接口

【1】Map接口的特点：key-value的映射

1. 用于存储任意键值对（key - value）
2. 键：**无序**、**无下标**、不允许重复**（唯一）**
3. 值：**无序**、**无下标**、**允许重复**

![image-20210109193659722](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210109193659722.png)

【2】Map方法：

| 方法                   | 说明                           |
| ---------------------- | ------------------------------ |
| V put(K key, V value)  | 将对象存到集合中，关联键值     |
| Object get(Object key) | 根据键获得对应的值             |
| Set<K>                 | 返回所有的Key                  |
| Collection<V> values() | 返回包含所有值的Collection集合 |
| Set<Map.Entry<K, V>>   | 键值匹配的Set集合              |

基本api操作：

```java

*          //增加：
*              put（k,v）    //添加元素
*         // 查找：
*              isEmpty      //判断是否为空
*              size        //返回map的大小
*              containsKey
*              containsValue
*              get
*          //删除：
*              clear 清空集合中的所有元素
*              remove:删除指定元素
```

## **Map接口的使用**

```java
//创建Map集合
Map<String, String> map = new HashMap<>();
// 1. 添加元素
map.put("cn", "中国");
map.put("uk", "英国");
map.put("cn", "zhongguo"); // 会替换第一个 
// 2. 删除
map.remove("uk");
// 3. 遍历
				// 3.1 使用KeySet()
        Set<String> keys = map.keySet();		// 所有Key的set集合
        for(String key:keys){
            System.out.println(key+"="+map.get(key));
        }
        //3.2for只能获取对应的value值，不能根据value来获取key
        Collection<Integer> values = map.values();
        for (Integer i:values){
            System.out.println(i);
        }
        //3.3迭代器
        Set<String> keys2 = map.keySet();
        Iterator<String> iterator = keys2.iterator();
        while(iterator.hasNext()){
            String key = iterator.next();
            System.out.println(key+"="+map.get(key));
        }
				// 3.4 使用entrySet() 
				// Map.entry:表示的是K-V组合的一组映射关系，key和value成组出现
				//Set<Map.Entry<String, String>> entries = map.entrySet();
				for(Map.Entry<String, String> entry : map.entries){
  				sout(entry.getKey() + "---" + entry.getValue();
        }
}
```

## Map的实现类

根据底层**存储结构**的不同有所区分

### **HashMap 【重点】**

【1】存储结构：**哈希表**（**数组**+**链表**+红黑树）（1.8）

使用key可使hashcode和equals作为重复

增、删、遍历、判断与上述一致

– Key无序 唯一（Set） 

– Value无序 不唯一(Collection)

【2】**原码分析总结**：

1. HashMap刚创建时，table是null，节省空间，当添加第一个元素时，table容量调整为16

2. 当元素个数大于阈值（16*0.75 = 12）时，会进行扩容，扩容后的大小为原来的两倍，目的是减少调整元素的个数，没满就开始扩容 ，最开始16（initCapacity）*0.75（load_factor加载因子）=12   到达12时即开始扩容。

3. jdk1.8 当每个（TREEIFY_THRESHOLD）**链表长度** **>8** ，并且**数组元素**个数 **≥64**时，会调整成**红黑树**，目的是提高效率

4. jdk1.8 当链表长度 **<6** 时 调整成**链表**

5. jdk1.8 以前，链表时头插入，之后为尾插入

6. hashmap初始值initCapacity为2的N次幂，（除数散列法）

   初始值：1<<4(initCapacity)  最大初始值：1<<30(Max_initCapacity)

    * 1、方便进行&操作，提高效率，&要比取模运算效率要高

      ​				hash & (initCapacity-1)

    * 2、在扩容之后涉及到元素的迁移过程，迁移的时候只需要判断二进制的前一位是0或者是1即可

    * 如果是0，表示新数组和就数组的下标位置不变，如果是1，只需要将索引位置加上旧的数组的长度值即为新数组的下标

   7.

1.7源码知识点：  数组+链表  

1、默认初始容量  table 的最小值 threshold = Math.min{initCapacit*load_factor, Max_initCapacity}肯定是前者 16×0.75=12

2、加载因子 HashMap(){}构造方法赋予loadFactor=0.75

3、put操作  

​		1、设置值，计算hash   为减少hash碰撞的发生，采用移位的方式，（例如16位    1001 1001 和1101 		1001 放在hash中链表一个格子里，但是通过移位，使1001 和1101进行比较，减少碰撞的发生）

​		2、扩容操作  每次都是上次的2倍   16---32 ----64   oldcap<<1

​		3、数据迁移的过程

1.8源码知识点:   数组+链表+红黑树    

1.8之前链表采用头插入，1.8之后采用的是尾插入

### **Hashtable**

线程安全，运行效率慢；不允许null作为key或是value

#### 		**Properties**

​		hashtable的子类，要求key和value都是**string**，通常用于配置文件的读取**（I/O流）**

【3】hashmap跟hashtable的区别：
 *      1、**hashmap**线程不安全，效率比较高，**hashtable**线程安全，效率低
 *      2、hashmap中key和value都可以为空,hashtable不允许为空

【4】案例源码见上

### **TreeMap**

【1】存储结构：**红黑树**

– 有序 速度没有hash快

实现了SortedMap接口（是map的子接口），可以对key自动排序

#### 外部比较器 compare()

```java
// 1.compare()方法
//外部比较器   定义在当前类中，通过实现comparator接口来实现，但是要将该比较器传递到集合中            
public class SetDemo implements Comparator<Person> {
    public static void main(String[] args) {
    @Override
    public int compare(Person o1, Person o2) {
        if(o1.getAge()>o2.getAge()){
            return -1;
        }else if(o1.getAge() < o2.getAge()){
            return 1;
        }else{
            return 0;
        }
    }
   }
```



#### 内部比较器comparable

```java
//2.此比较器按照name的长度来进行比较(设定)
//内部比较器 定义在元素Person的类中，通过实现comparable接口来进行实现
public class Person implements Comparable{
@Override
    public int compareTo(Object o) {
        Person p  = (Person) o;
        if (p.name.length()>this.name.length()){
            return -1;
        }else if(p.name.length()<this.name.length()){
            return 1;
        }else{
            return 0;
        }
    }
}
```

​	注意：**外部比较器**可以定义成一个工具类，此时所有需要比较的规则如果一致的话，可以复用，而

*               **内部比较器**只有在存储当前对象的时候才可以使用
*               如果两者同时存在，使用**外部比较器**
*               当**使用比较器**的时候，**不会调用equals**方法



#### 案例代码

```java
package com.qf.chapter12;

import java.util.Map;
import java.util.TreeMap;

/**
 * @Auther: wuxy
 * @Date: 2021/1/10 - 01 - 10 - 9:24
 * @Description: com.qf.chapter12
 * TreeMap
 * @version: 1.0
 */
public class Demo3 {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
    //新建集合
        TreeMap<Student,String> treeMap=new TreeMap<Student, String>();
        
      //1添加元素
        Student s1= new Student("孙悟空",100);
        Student s2= new Student("猪八戒",101);
        Student s3= new Student("沙和尚",102);
        treeMap.put(s1,"北京");
        treeMap.put(s2,"上海");
        treeMap.put(s3,"深圳");
        treeMap.put(new Student("沙和尚",102),"深圳");
        System.out.println("元素个数"+treeMap.size());
        System.out.println(treeMap.toString());
        
      //2删除元素
        treeMap.remove(new Student("猪八戒",101) );
        System.out.println("元素个数"+treeMap.size());
        
      //3遍历
        System.out.println("----------keySet()----------");
        for (Student key:treeMap.keySet()) {
            System.out.println(key+"-----"+treeMap.get(key));
        }
        System.out.println("----------entrySet()----------");
        for(Map.Entry<Student, String> entry : treeMap.entrySet()){
            System.out.println(entry.getKey() + "---" + entry.getValue());
        }
        
      //4判断
        System.out.println(treeMap.containsKey(new Student("沙和尚",102)));
    }
}

```



### LinkedHashMap

【1】存储结构：链表

– 有序的HashMap 速度快

# 十、泛型

本质是参数化类型，把**类型**作为**参数**传递

常见形式有泛型类、泛型接口、泛型方法

语法 T成为类型占位符，表示一种引用类型，可以写多个逗号隔开

在定义对象的时候，通过<>中设置合理的类型来进行实现

好处： 

1. 提高代码重用性 

2. 防止类型转换异常，提高代码安全性
3. 获取数据时效率比较高

```java
//当做一些集合的统一操作的时候，需要保证集合的类型是统一的，此时需要泛型来进行限制     
//给集合中的元素设置相同的类型就是泛型的基本需求
List<String> list = new ArrayList<String>();
list.add("1"); 
list.add("abc");
for(String iter:list){//会报错，因为类型不统一
          System.out.println(iter);
        }
//改正
for(Object iter:list){//会报错，因为类型不统一
          System.out.println(iter);
        }
```

## 泛型的高阶应用

### **泛型类**

```java
// 写一个泛型类
public class MyGeneric<T>{
  //使用泛型T（T只起到占位的作用）
  //1 创建变量
  T t;
  //2 泛型作为方法的参数
  public void show(T t){
    sout(t);
  }
  //3 泛型作为方法的返回值
  public T getT(){
    return t;
  }
}
```



```java
// 使用泛型类
public class TestGeneric{
  public static void main(String[] args){
    //使用泛型类创建对象
    // 注意： 1. 泛型只能使用引用类型
    //			 2. 不用泛型类型对象之间不能相互赋值
    MyGeneric<String> myGeneric = new MyGeneric<String>();
    myGeneric.t = "hello";
    myGeneric.show("hello world!");
    String string = myGeneric.getT();
    
    MyGeneric<Integer> myGeneric2 = new MyGeneric<Integer>();
    myGeneric2.t = 100;
    myGeneric2.show(200);
    Integer integer = myGeneric2.getT();
    
  }
}
```



代码实现;

```java
package com.mashibing;

/**
 * @author: 马士兵教育
 * @create: 2019-09-21 16:21
 */
public class FanXingClass<A> {//FanXingClass<A>   A只是一个占位符

    private int id;
    private A a;		//A类型的变量

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public A getA() {
        return a;
    }

    public void setA(A a) {     //A类型的变量做参数
        this.a = a;
    }

    public void show(){
        System.out.println("id : "+id+" ,A : "+a);
    }

    public A get(){
        return a;
    }

    public void set(A a){
        System.out.println("执行set方法：" + a);
    }
}

```

```java
package com.mashibing;

import java.util.ArrayList;
import java.util.List;

/**
 * @author: 马士兵教育
 * @create: 2019-09-21 16:11
 */

/**
 
 *  泛型的高阶应用：
 *      1、泛型类
 *          在定义类的时候在类名的后面添加<E,K,V,A,B>,起到占位的作用，类中的方法的返回值类型和属性的类型都可以使用
 *
 */
public class FanXingDemo {
    public static void main(String[] args) {
        FanXingClass<String> fxc = new FanXingClass<String>();
        fxc.setA("mashibing");
        fxc.setId(1);
        fxc.show();

        FanXingClass<Integer> fxc2 = new FanXingClass<Integer>();
        fxc2.setA(34);
        fxc2.setId(2);
        fxc2.show();

        FanXingClass<Person> fxc3 = new FanXingClass<Person>();
        fxc3.setA(new Person("aaa",123));
        fxc3.setId(3);
        fxc3.show();
        System.out.println(fxc3.get());
        fxc3.set(new Person("hhe",123));

    }
}

```

![image-20210109185905216](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210109185905216.png)



### **泛型接口**

语法：接口名

注意：不能泛型静态常量

```java
package com.mashibing;

public interface FanXingInterface<B> {

   public B test();

   public void test2(B b);
}

```



```java
//第一种实现方式----------------------------------------------
package com.mashibing;

/**
 * @author: 马士兵教育
 * @create: 2019-09-21 16:33
 */
public  class   FanXingInterfaceSub<String> implements FanXingInterface<String> {
//实现泛型接口

    @Override
    public String test() {
        return null;
    }

    @Override
    public void test2(String string) {

    }
}
//第二种实现方式---------------------------------------------------
public  class   FanXingInterfaceSub implements FanXingInterface<String> {
//实现泛型接口

    @Override
    public String test() {
        return null;
    }

    @Override
    public void test2(String string) {

    }
}
```



```java
package com.mashibing;

import java.util.ArrayList;
import java.util.List;

/**
 * @author: 马士兵教育
 * @create: 2019-09-21 16:11
 */

/**
 *  泛型的高阶应用：
 *      
 *      2、泛型接口
 *          在定义接口的时候，在接口的名称后添加<E,K,V,A,B>,
 *          1、子类在进行实现的时候，可以不填写泛型的类型，此时在创建具体的子类对象的时候才决定使用什么类型
 *          2、子类在实现泛型接口的时候，只在实现父类的接口的时候指定父类的泛型类型即可，此时，测试方法中的泛型类型必须要跟子类保持一致
 *
 */
//第一种实现方式----------------------------------------------
public class FanXingDemo {
    public static void main(String[] args) {
        FanXingInterfaceSub<Integer> fxi = new FanXingInterfaceSub<Integer>() ;
        fxi.test2(123);

    }
//第二种实现方式--------------------------------------------------- 
  public static void main(String[] args) {
        FanXingInterfaceSub fxi = new FanXingInterfaceSub() ;
        fxi.test2("123");
    }
}

```



### **泛型方法**

语法： 返回值类型



```java
public class MyGenericMethod{
  //泛型方法
  public <T> T show(T t){
    sout("泛型方法" + t);
    return t;
  }
}

//调用
MyGenericMethod myGenericMethod = new MyGenericMethod();
myGenericMethod.show("字符串");// 自动类型为字符串
myGenericMethod.show(200);// integer类型
myGenericMethod.show(3.14);// double类型
```



```java
package com.mashibing;

/**
 * @author: 马士兵教育
 * @create: 2019-09-21 16:44
 */
public class FanXingMethod<T> {

    private T t;

    public T getT() {
        return t;
    }

    public void setT(T t) {
        this.t = t;
    }

    public <Q> void show(Q q){		//泛型方法
        System.out.println(q);
        System.out.println(t);
    }
}

```



```java
package com.mashibing;

import java.util.ArrayList;
import java.util.List;

/**
 * @author: 马士兵教育
 * @create: 2019-09-21 16:11
 */

/**
 泛型的高阶应用：
 *      
 *      3、泛型方法
 *          在定义方法的时候，指定方法的返回值和参数是自定义的占位符，可以是类名中的T,也可以是自定义的Q，只不过在使用Q的时候需要使用<Q>定义在返回值的前面
 */
public class FanXingDemo {
    public static void main(String[] args) {

        FanXingMethod<String> fxm = new FanXingMethod<>();
        fxm.setT("ttt");
        fxm.show(123);
        fxm.show(true);
    }
}

```

![image-20210109192014444](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210109192014444.png)

### **泛型集合**

概念：参数化类型、类型安全的集合，强制集合元素的类型必须一致

特点：

- 编译时即可检查，而非运行时抛出异常
- 访问时，不必类型转换（拆箱）
- 不同泛型之间应用不能相互赋值，泛型不存在多态



###  泛型的上限（工作中不用，API中使用）

​       如果父类确定了，所有的子类都可以直接使用      

###  泛型的下限（工作中不用，API中使用）

​       如果子类确定了，子类的所有父类都可以直接传递参数使用

# 十一、Collections工具类

【1】特点

概念：集合工具类，定义了**除了存取**以外的集合常用方法

【2】方法

直接二分查找`int i = Collections.binarySearch(list, x);` 成功返回索引

其他方法 ： **copy复制、reverse反转、shuffle打乱**

| 方法                                     | 说明                                      |
| ---------------------------------------- | ----------------------------------------- |
| public static void reverse(List<?> list) | 反转集合中元素的顺序                      |
| public static void shuffle(List<?> list) | 随机重置集合元素的顺序                    |
| public static void sort(List<T> list)    | 升序排序（元素类型必须实现Comparable接口) |

【3】案例源码

```java
package com.qf.chapter12;

import java.sql.SQLOutput;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;

/**
 * @Auther: wuxy
 * @Date: 2021/1/10 - 01 - 10 - 9:49
 * @Description: com.qf.chapter12
 * collections工具类的使用
 * @version: 1.0
 */
public class Demo4 {
    //这是一个main方法，是程序的入口：
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<>();
        list.add(20);
        list.add(5);
        list.add(12);
        list.add(30);
        list.add(6);

        //sort排序
        System.out.println("排序之前"+list.toString());
        Collections.sort(list);
        System.out.println("排序之后"+list.toString());

        //二分查找
        int i= Collections.binarySearch(list,13);
        System.out.println(i);

        //copy复制
        List<Integer> dest = new ArrayList<>();
        for (int k = 0; k < list.size(); k++) {
            dest.add(0);
        }
        Collections.copy(dest,list);
        System.out.println(dest.toString());

        //reverse反转
        Collections.reverse(list);
        System.out.println("反转之后"+list);

        //shuffle 打乱
        Collections.shuffle(list);
        System.out.println("打乱之后"+list);

        // list转成数组
        Integer[] arr = list.toArray(new Integer[10]);
        System.out.println((arr.length));
        System.out.println((Arrays.toString(arr)));

        // 数组转成集合
        // 此时为受限集合，不能 添加和删除！
        String[] names = {"张三","李四","王五"};
        List<String> list2 = Arrays.asList(names);

        // 把基本类型数组转为集合时，需要修改为包装类
        Integer[] nums = {100, 200, 300, 400, 500};
        List<Integer> list3 = Arrays.asList(nums);
    }
}

```



补充：

```java
// list转成数组
        Integer[] arr = list.toArray(new Integer[10]);
        System.out.println((arr.length));
        System.out.println((Arrays.toString(arr)));

        // 数组转成集合
        // 此时为受限集合，不能 添加和删除！
        String[] names = {"张三","李四","王五"};
        List<String> list2 = Arrays.asList(names);

        // 把基本类型数组转为集合时，需要修改为包装类
        Integer[] nums = {100, 200, 300, 400, 500};
        List<Integer> list3 = Arrays.asList(nums);
```

# 十二、Properties

属性集合，继承了Hashtable

特点：

1存储属性名和属性值

2属性名和属性值都是字符串类型

3 没有泛型

4和流有关

# 总结

![image-20210110101454875](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/image-20210110101454875.png)