# Java基础

## 集合

## HashMap

参考：敖丙 [https://github.com/JavaFamily](https://github.com/AobingJava/JavaFamily)

1、概述HashMap是集合的一种，是常用的数据结构，与collection相反，是双列的集合，底层结构由数组加链表结合。每个数组存的都是Key-Value的形式，在Java7中是叫做Entry在java8叫做node，在node进行插入时，是以链表的形式。在Java8之前是采用头插法，Java8开始采用尾查法

![image-20210702155042181](C:\Users\25753\AppData\Roaming\Typora\typora-user-images\image-20210702155042181.png)

HashMap的初始长度16，扩容因子为0.75，当用量达到总容量的75%就开始扩容，创建两倍的新数组之后，遍历数组将所有node重新hash到新数组

头插法和尾插法：头插法是每次插入都往头部插入，而尾插法每次插入往尾部进行插入。在HashMap中头插法可能导致死循环，尾插法能保持元素原本的顺序

如果想保证线程安全可使用HashTable和ConcurrentHashMap