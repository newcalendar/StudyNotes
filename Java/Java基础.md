# Java基础

参考（感谢）：黑马程序员

## 基础语法

### 1、Java概述

1、Java由美国Sun公司在1995年推出的计算机语言，Java之父James Gosling，2009年Sun公司被Oracle收购

2、Java语言的跨平台原理，每种平台都有一种Java虚拟机，所以Java可以实现跨平台

3、JRE是运行时环境，里面包括JVM（Java虚拟机），JDK是Java开发工具，里面包括了JRE和开发工具

### 2、Java基础语法

#### 一、基本语法

##### 1、注释

```java
//单行注释	
```

```java
/*
多行注释
*/
```

```java
/**
* 文档注释
*/
```

##### 2、关键字

被Java赋予了特殊含义的单词，例如public，private，class等

this关键字



##### 3、常量

在程序运行时，其值不能发生改变

##### 4、数据类型

1、基本数据类型：byte\short\int\long\float\double\char\boolean

2、引用数据类型：数组、String

3、对应基本数据类型有相应的包装类，包装类定义了操作数据的一系列方法，包装类

把基本类型转换成为对应的包装为自动装箱，将包装类转换成基本数据类型为自动拆箱

##### 5、变量

变量是程序运行时能改变的量

##### 6、标识符

标识符是开发人员编程使用的名字，命名不能使用关键字，同时命名要遵守驼峰式命名

##### 7、类型转换

类型转换分为两种，一种是自动类型转换和强制类型转换，

自动类型转换通常是将一个范围小的数值或变量赋值给另一个范围较大的变量，而强制类型转换则相反。

![image-20210706105939043](C:\Users\25753\AppData\Roaming\Typora\typora-user-images\image-20210706105939043.png)

##### 8、运算符

1、算术运算符：对常量或者变量进行操作的符号

2、算术运算符：+，-，*，/，%

3、赋值运算符：

![image-20210706110716223](C:\Users\25753\AppData\Roaming\Typora\typora-user-images\image-20210706110716223.png)

4、自增自减运算符

![image-20210706110758071](C:\Users\25753\AppData\Roaming\Typora\typora-user-images\image-20210706110758071.png)

5、关系运算符

![image-20210706110832624](C:\Users\25753\AppData\Roaming\Typora\typora-user-images\image-20210706110832624.png)

6、逻辑运算符

![image-20210706110941852](C:\Users\25753\AppData\Roaming\Typora\typora-user-images\image-20210706110941852.png)

7、短路逻辑运算符

![image-20210706111053391](C:\Users\25753\AppData\Roaming\Typora\typora-user-images\image-20210706111053391.png)

注：所谓短路，即前面的条件判断如果可以决定结果，则后面的条件不再判断，&&判断时，第一个条件为false则后面不再判断返回false,||如果前面的条件为true则后面的条件不再执行，返回true

8、三元运算符

语法：

```java
关系表达式 ？ 表达式1：表达式2;
```

实例：

```java
int a=10;
int b=20;
int c =a>b?a:b;
```

判断a>b是否为真，如果为真则返回a值，否则返回b值

#### 二、数据输入

数据输入Java可以通过Scanner类来获取用户输入

实例

```java
//创建Scanner对象
Scanner in=new Scanner（System.in）；
//取出数据
int c=in.nextInt();
```

#### 三、流程控制语句

##### 1、流程控制语句分类

顺序结构

分支结构

循环结构

##### 2、顺序结构

没有特定的语法结构，程序的执行按照代码的先后顺序进行执行

##### 3、分支结构

###### 1、if语句

1、if

```java
if（关系表达式）{

   语句；

}
```

2、if...else....

```java
if(关系表达式){
  语句；
}else{
  语句
}
```

3、if...else if...else

```java
if(表达式){
  语句；
}else if(表达式){
  语句；
}else{
  语句；
}
```

2、Switch语句

```java
switch(表达式){
case 1：
  语句；
  break；
case 2：
  语句;
  break;
case 3:
  语句3；
  break;
...
default:
  语句；
   break；
   }
```

switch语句一定要注意使用break，否则会出现错误，default语句是在case都没有与结果相匹配时执行的默认语句。

###### 4、循环

1、for

```
for(初始化语句；条件判断语句；条件控制语句){
   循环语句；
}
```

2、while循环

```java
while(条件判断语句){
  语句
  }
```

2.1 do ..while

```
do{
  循环语句；
}while(条件判断语句)
```

可用break跳出循环，结束循环；可用continue跳过本次循环，继续下次循环

#### 四、Random随机数

可使用Random类进行随机数的生成

```java
Random r =new Random();
//生成0~9的随机数
int num=r.nextInt(10);
```

## 数组

### 1、概述

数组是存储数据长度固定的容器，存储多个数据的数据类型要一致；

### 2、数组的定义格式

1、格式一

```java
int[] arr;
double[] arr;
char[] arr;	
```

2、格式二

```
int arr[];
double arr[];
char arr[]; 
```

### 3、数组动态初始化

1、数组的动态初始化是给定数组长度，由系统给出默认初始值

2、格式

```
数据类型[] 数组名=new 数据类型[数组长度]；
int [] arr =new int[3];
```

3、数组索引，数组的每个位置都有一个引索下标，一般是从0开始，可通过数组的索引访问到数组的元素

### 4、数组静态初始化

在创建数组的时候将元素存入

```
int[] arr={1,2,3};
```

### 5、可能出现的异常

1、索引越界异常

2、空指针异常

## 方法

### 1、概述

方法是将具有独立功能的代码块组织成为一个整体，使其具有特殊功能的代码集

### 2、方法的定义和调用

1、无参数方法定义和调用

格式：

```java
public static void 方法名（）{
       方法体；
}
```

调用格式：

```java
方法名（）;
```

2、带参方法定义和调用

格式：

```java
//单一参数
public static void 方法名(参数1){
  方法体；
  }


//多个参数
  public static void 方法名（参数1，参数2，参数...){
    方法体；
  }
```

### 3、形参和实参

形参：方法定义中的参数

实参：方法调用中参数

### 4、带返回值方法

1、带返回值方法定义和调用

定义格式

```java
//带返回值方法
public static 数据类型 方法名 （参数）{
  return 数据；
  }
```

### 5、方法的通用格式

```java
//方法的通用格式
public static 返回值类型 方法名（参数）{
  方法体
  return 数据；
  }
```

### 6、方法重载和重写

1、重写：

也称作子类的方法覆盖父类的方法，要求返回值、方法名和参数都需要相同

子类抛出的异常不能超过父类，子类的访问级别不能低于父类相应方法的访问级别

2、重载

方法重载是在同一个类中有两个或者两个以上方法拥有相同的方法名，但是参数不同，参数不同表现在参数类型不同或者是参数的数量不停·同

## Debug

### 1、概述

Debug是程序调试工具，用于查看程序的执行流程和数据变化，用于追踪程序执行来调试程序

### 2、Debug的操作

1、断点

断点是在Debug程序是定位停止的位置，添加断点点击鼠标左键即可，断点出现会有个红点，可以按F8进行下一步，按F7进行步入方法内部

## 面向对象

### 1、类和对象

类的理解：类是对现实生活中一类具有共同属性和行为的事物抽象

对象：万物皆对象

类和对象的关系：类是对事物的一种描述，对象则为具体存在的事物

### 2、类的定义

```java
//类的定义
public class 类名{
   //成员变量
  数据类型 变量；
  
   //成员方法
   方法体；

}
```

### 3、对象的应用

```java
class Student{
   String name;
   int age;
   
   public void study(){
      System.out.println("好好学习");
   }
 }
 
 public class StudentDemo{
    public static void main(string[] args){
        
        //创建对象
        Student s=new Student();
        s.name="李四"；
        s.age=20;
        System.out.println(s.name+","+s.age);
    }
 }
```

### 4、成员变量和局部变量

1、所在的位置不同，成员方法在类中方法外，局部变量在方法内部或方法声明上

2、内存位置不同，成员变量在堆内存，而局部变量在栈内存

3、生命周期不同，成员变量随着对象的存在而存在，而局部变量随着方法调用而存在

### 5、继承

1、继承的概念：继承是面向对象三大特征之一，可使得子类具有父类的属性和方法，还可以在子类中重新定义，以及追加属性和方法

2、继承的好处是可以让类与类之间产生关系，产生子类后，子类可以使用父类非私有成员。

继承的好处是提高了代码的复用性，和可维护性，但是增强了类的耦合

3、继承的访问特点是，子类会先在子类局部范围找->子类成员范围找->父类成员范围找

4、super关键字

this代表本类对象的引用，super可以理解是父类对象的引用

this.成员变量访问本类成员变量

super.成员变量访问父类成员变量

this.成员方法-访问本类成员方法

### 6、多态

1、概念同一对象在不同时刻表现出不同的形态，多态的前提是要继承或者实现关系，要有方法的重写，要有父类引用指向子类对象。

2、多态的好处是提高程序的扩展性。定义方法时候，使用父类型作为参数，在使用的时候，使用具体的子类型参与操作，但是不能使用子类的特有成员

### 7、抽象类

1、类中如果有抽象方法，该类必须定义为抽象类

2、抽象类不一定有抽象方法，抽象类必须使用abstract关键字修饰

### 8、接口

1、概述接口是一种公共的规范标准，Java只能单继承但是可以多实现，接口用interface关键字修饰，接口不能实例化，接口的子类需重写接口中的所有抽象方法，或者子类也是抽象类

接口和抽象类的区别

接口的设计目的，是对类的行为进行约束（更准确的说是一种“有”约束，因为接口不能规定类不可以有什么行为），也就是提供一种机制，可以强制要求不同的类具有相同的行为。它只约束了行为的有无，但不对如何实现行为进行限制。对“接口为何是约束”的理解，我觉得配合泛型食用效果更佳。

而抽象类的设计目的，是代码复用。当不同的类具有某些相同的行为(记为行为集合A)，且其中一部分行为的实现方式一致时（A的非真子集，记为B），可以让这些类都派生于一个抽象类。在这个抽象类中实现了B，避免让所有的子类来实现B，这就达到了代码复用的目的。而A减B的部分，留给各个子类自己实现。正是因为A-B在这里没有实现，所以抽象类不允许实例化出来（否则当调用到A-B时，无法执行

作者：阿法利亚
链接：https://www.zhihu.com/question/20149818/answer/150169365

## 内部类

1、概述：在一个类中定义一个类

2、特点：内部类可以直接访问外部类的成员包括私有，外部类要访问内部类的成员，必须创建对象。

### 一、成员内部类

成员内部类的定义位置是在类中方法

### 二、局部内部类

局部内部类是在方法中定义的类

### 三、匿名内部类

匿名内部类的本质是一个继承了该类或者实现了该接口的子类匿名对象

## 常用的API

### 一、String、StringBuffer、StringBuilder

#### 1、String

String代表字符串，字符串在创建后不能被更改

#### 2、StringBuilder

StringBuilder是可变类，速度更快，线程不安全，单线程操作字符串

#### 3、StringBuffer

可变类，线程安全，StringBuffer对象都有一定的缓存区容量，当字符大小没有超过容量时，不会分配新的容量，当字符串大小超过容量时，会自动增加容量

### 二、==和equals

==在作用于基本数据类型是，比较的是数值，如果作用于引用数据类型时比较的是地址。

如果不重写equals，其实==和equals是一样的效果，String重写了equals方法，可以比较内容是否一致

### 三、Math

1、Math类是运算API，执行基本数字运算的方法

2、常用方法

![image-20210707143126846](C:\Users\25753\AppData\Roaming\Typora\typora-user-images\image-20210707143126846.png)

### 四、System

1、常用方法：

exit(int staus)终止当前运行的Java虚拟机

long currentTimeMills()返回当前时间

## 异常

### 1、概述

异常指的是程序出现不正常状态

### 2、异常体系

![image-20210707144256497](C:\Users\25753\AppData\Roaming\Typora\typora-user-images\image-20210707144256497.png)

异常的分类分为严重问题和异常，而异常也通常分为，编译时异常和运行时异常。

### 3、try-catch方式处理异常

```
//try-catch异常处理方法
try{
  可能出现异常的代码；
}catch(异常类名 变量名){
  异常的处理代码；
}
```

执行的流程是，程序在try模块中运行，如果出现异常则跳转到对应的catch里进行执行

### 4、Throwable成员方法

getMessage()返回throwable的详细消息字符串

toString()返回此抛出的简短描述

printStackTrace()把异常的错误信息输出在控制台

### 5、throws方式处理异常

```java
//throws方式格式
public void 方法（） throws 异常类名{

}
```

1、throws和throw的区别

![image-20210707150452018](C:\Users\25753\AppData\Roaming\Typora\typora-user-images\image-20210707150452018.png)

## 集合

## 一、collection

collection集合是单列集合

### 1、List集合

List集合是单列集合，其元素可重复，有序集合，有索引

#### 1、ArrayList集合

1、概述

ArrayList集合是一个提供一种存储空间可变的存储模型，存储的数据容量可以发生改变，底层是数组实现，线程不安全

2、构造方法

public ArrayList（）创建一个空的集合对象

3、方法

remove（Object o）删除指定元素，返回是否成功

remove（int index）删除指定索引处的元素，返回被删除的元素

set（int index，E  element）修改指定索引处的元素，返回被修改元素

get（int index）返回指定索引处的元素

add（int index，E  element）在此集合中的指定位置插入指定元素

size（）返回集合中的元素个数



4、ArrayList的扩容机制

ArrayList的默认大小为10（JDK8）,JDK7时是0，扩容时会创建一个新的比原来大1.5倍的集合，然后将原集合元素复制到新的集合Arrays.copyof(elementData,newCapacity)方法

5、遍历方法

for循环遍历

```
//for循环遍历
for（int i=0；i<array.size();i++){
  String s=array.get(i);
  System.out.println(s);
}
```

迭代器遍历

```
//迭代器示意
ListIterator<String> lit=list.listIterator();
while(lit.hasNext()){
   String s=lit.next();
   System.out.pritln(s);
}
```

增强for循环遍历

```java
//增强for循环
for(元素数据类型 变量名：集合(数组)){
  循环体
  }
```

```
//示例
for(String s : array){
   System.out.println(s);
}
```



#### 2、LinkedList集合

1、概述：LinkedList是一个链表结构，底层实现的是双向链表，支持序列化

2、基于LinkedList集合底层是双向链表的特点，其查询相对比较慢，增删快

#### 3、Vector集合

1、Vector集合底层也是动态可变的数组，相对而言查询快、增删慢

2、Vector底层有同步代码块关键字synchronized修饰，它是线程安全的



### 2、Set集合

1、set集合的特点是元素存取无序，没有索引，只能通过迭代器和增强for循环遍历，不能存储重复的元素

2、哈希值是JDK根据对象的地址或者字符串或者数字算出来的int类型的数值

#### 1、HashSet集合

1、概述：底层是哈希表或者说是HashMap,没有索引的方法，不能使用普通的for循环遍历，不能存储重复元素

2、Hashset保持元素唯一原理

调用对象的hashcode方法，根据哈希值计算存储位置，获取位置后判断该位置是否有元素，如果没有则将该元素存储到该位置，如果有则遍历该位置的所有元素，比较哈希值是否相同，如果有相同，调用equals比较相同哈希值得对象的内容是否相同，如果相同则表明该元素重复。

#### 2、LinkedHashset

1、特点通过哈希表和链表实现set接口，可以预测的迭代次序，由链表保证元素有序，由哈希表保证元素唯一

#### 3、TreeSet

1、元素有序，可以按照一定的规则进行排序，具体排序方式取决于构造方法

2、Comparable

通过实现Comparable接口重写compareTo(T o)方法进行排序



## 二、Map集合

Map集合是双列集合，Key-Value形式，元素存取无序

常用方法：

![image-20210707162024017](C:\Users\25753\AppData\Roaming\Typora\typora-user-images\image-20210707162024017.png)





#### HashMap

参考（感谢）：敖丙 [https://github.com/JavaFamily](https://github.com/AobingJava/JavaFamily)

1、概述HashMap是集合的一种，是常用的数据结构，与collection相反，是双列的集合，底层结构由数组加链表结合。每个数组存的都是Key-Value的形式，在Java7中是叫做Entry在java8叫做node，在node进行插入时，是以链表的形式。在Java8之前是采用头插法，Java8开始采用尾查法

![image-20210702155042181](C:\Users\25753\AppData\Roaming\Typora\typora-user-images\image-20210702155042181.png)

HashMap的初始长度16，扩容因子为0.75，当用量达到总容量的75%就开始扩容，创建两倍的新数组之后，遍历数组将所有node重新hash到新数组

头插法和尾插法：头插法是每次插入都往头部插入，而尾插法每次插入往尾部进行插入。在HashMap中头插法可能导致死循环，尾插法能保持元素原本的顺序

如果想保证线程安全可使用HashTable和ConcurrentHashMap

## 三、Collections

1、概述：Collections是针对集合操作的工具类

2、常用方法

![image-20210707163512499](C:\Users\25753\AppData\Roaming\Typora\typora-user-images\image-20210707163512499.png)

## 泛型

1、概述：泛型JDK5引入的特性，它提供了编译时类型的安全检测机制，该机制允许在编译时就能检测到非法的类型，本质是参数化类型，泛型即在调用时传入规定类型，添加元素时要按规定的类型传入，否则在编译期间就会报错，在程序运行时，泛型会转换成普通类型。

2、格式

```
//泛型格式
修饰符<类型> 返回值类型 方法名（类型 变量名）{
}
```

```
//泛型实例
public class Generic{
  public<T> void show(T t){
     System.out.println(t);
  }
}
```

3、类型通配符

List<?>表示元素类型未知的List

List<?extends Number>表示类型通配符上限

List<?super  Number>表示类型通配符下限

## 线程、同步

### 一、线程

1、进程是资源分配的最小单位，线程是程序执行的最小单位，一个进程可以包含多个线程，同一进程的不同线程数据容易共享，不同进程的数据很难共享

2、Thread类

常用构造方法：

public Thread（）分配一个新的线程对象

public Thread（String name);分配一个指定名字的新的线程对象

public Thread（Runnable target)分配一个指定名字的新的线程对象

常用方法

getname()获取当前线程名称

start()执行线程，调用该线程run方法

sleep(long millis)使当前线程休眠指定的毫秒数

currentThread（）返回当前正在执行的线程对象引用

3、创建线程方式

（1）一个是继承Thread类

（2）另外一个是实现Runnable接口并重写该接口的run()方法，调用star()方法来启动线程

4、Thread和Runnable的区别

继承了Thread类不适合资源共享，而实现了Runable的话容易实现资源共享。Runable接口比继承Thread类所具有的优势：适合多个相同的程序代码的线程共享同一个资源，避免Java单继承的局限，增加程序的健壮性，实现解耦操作，线程池只能放入实现Runable

### 二、线程安全

多线程存在线程安全问题，例如在多线程不同步的情况下，可能出现火车票一共100张，其中一张卖2次的情况，出现类似脏读情况

#### 1、同步代码块

```java
synchronized（同步锁）{
  需要同步的代码
  }
```

![image-20210707171005744](C:\Users\25753\AppData\Roaming\Typora\typora-user-images\image-20210707171005744.png)

#### 2、同步方法

```
public synchronized void method(){
  可能产生线程安全问题的代码；
}
```

#### 3、Lock锁

1、Lock锁也称为同步锁

```
public void lock()加同步锁
public void unlock（）释放同步锁
```

### 三、线程状态

![Java 多线程详解二(多线程状态)](https://www.qihaoge.com/img/5182413-bec88083fb41c0f7.jpg)

1、new新建状态，线程被撞见还没启动调用start方法

2、就绪态，线程可以在虚拟机运行的状态

3、阻塞态，线程因为某些原因进入等待状态

阻塞态分为同步阻塞(synchronized)、等待阻塞（wait）、其他阻塞

(sleep,join)

4、运行状态，线程获取到CPU资源处于运行状态

5、死亡态，因为正常结束退出线程，或者异常终止了线程

#### 1、新建线程

廖雪峰https://www.liaoxuefeng.com/wiki/1252599548343744/1306580767211554

```
//Thread方式
public class Main {
    public static void main(String[] args) {
        Thread t = new MyThread();
        t.start(); // 启动新线程
    }
}

class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("start new thread!");
    }
}
```

```
//Runable方式
public class Main {
    public static void main(String[] args) {
        Thread t = new Thread(new MyRunnable());
        t.start(); // 启动新线程
    }
}

class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("start new thread!");
    }
}
```

#### 2、中断线程

```
public class Main {
    public static void main(String[] args) throws InterruptedException {
        Thread t = new MyThread();
        t.start();
        Thread.sleep(1); // 暂停1毫秒
        t.interrupt(); // 中断t线程
        t.join(); // 等待t线程结束
        System.out.println("end");
    }
}

class MyThread extends Thread {
    public void run() {
        int n = 0;
        while (! isInterrupted()) {
            n ++;
            System.out.println(n + " hello!");
        }
    }
}
```

#### 3、死锁

当两个对象分别拥有对象需求的锁，互相等待，这样就造成了死锁的情况。

#### 4、wait和notify

​           wait方法使线程进入等待，notify方法可以唤醒线程，notify,notifyAll, 唤醒等待该对象同步锁的线程,并放入该对象的锁池中.对象的锁池中线程可以去竞争得到对象锁,然后开始执行.

## 反射

1、概述：Java反射是在程序运行装填中，对任意一个类，都能指导这个类的所有属性和方法；对任意一个对象。都能够调用它的任意一个方法和属性。

2、获取class文件对象的三种方式

(1)Class.forName

(2).class

(3)getClass()方法