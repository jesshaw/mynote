# 集合

## HashMap的特点有哪些？与HastTable的区别

## HashMap的扩容机制

1.7数组+链表。头插法，相同数组的链倒过来了。指定负载因子

1.8节点+链表。一次性移过去

## HashMap的容量为什么是2的幂次

方便转移到新的位置，即可能不变，也可能是老的长度+现在的位置。减少碰撞

## 有集合A和集合B，现在需要将两个集合中重复的元素放入到集合C中，请问你会怎么编程实现

这道题，简单想到的是循环遍历两个集合A和B，然后将重复的元素放入到集合C中，我们来看看怎么实现？

```java
List<String> list1 = Arrays.asList("a","b","c");
List<String> list2 = Arrays.asList("a","b");
List<String> list3 = new ArrayList<>();
for (String a : list1) {
    for (String b : list2) {
        if(a.equals(b)){
            list3.add(a);
        }
    }
}
System.out.println(list3);
```

时间复杂度为O(n²)。

一个时间复杂度为O(n)的写法

```java
Set<String> set = new HashSet<>();
for (String a : list1) {
    set.add(a);
}
for (String b : list2) {
    if(set.contains(b)){
        list3.add(b);
    }
}
System.out.println(list3);
```

## 为什么使用红黑树，不用二叉树。  红黑树实现原理

## HashMap原理，列锁的原因

## HashMap中的put是如何实现的

## 为什么不直接将key作为哈希值而是与高16位做异或运算

## ConcurrentHasmMap扩容的过程

## 扩容列循环的问题

并发情况下，扩容时在同一节点，使用头插法，当达到3个或以上的时候，开成闭环，引起死循环



## WeekHashMap与HashMap的区别

1. WeekHashMap中默认存储的是弱引用键值条目（entry）,HashMap默认存储的是强引用entry
1. 当key丢弃时，WeekHashMap中对应的entry会被垃圾回收（GC），但HashMap不会。
1. WeekHashMap未实现Cloneable接口，仅实现了Map接口。

## ArrayList、LinkedList与Vector三者有什么区别

1. 从存储数据结构分析

    ArrayList：数组
    Vector：数组
    LinkedList：双向链表

    数组：可以根据下标快速查找，所以大部分情况下，查询快。
    但是如果要进行增删操作的时候，会需要移动修改元素后面的所有元素，所以增删的开销比较大，数组的对增删操作的执行效率低。而采用数组作为数据存储结构的ArrayList、Vector也存在这些特性，查询速度快（可以根据下标直接取，比迭代查找更快），增删慢。

    链表：增加和删除元素方便，增加或删除一个元素，仅需处理结点间的引用即可。就像人手拉手连成一排，要增加或删除某个人只要附近的两个人换一个人牵手，对已经牵好手的人没影响。无论在哪里换人耗费的资源和时间都是一样的。
    但是查询不方便，需要一个个对比，无法根据下标直接查找。而采用链表结构存储的LinkedList也有这些特性，增删方便，查询慢(指的是随机查询，不是顺序查询)。

1. 从继承上分析

    它们都实现了List接口，也就是说都实现了get(int location)、remove(int location)等“根据索引值来获取、删除节点的函数”。
    数组结构根据下标取值很容易，LinkedList双向链表的实现也比较简单，通过计数索引值实现，从链表长度的1/2开始查找，下标大了就从表头开始找，小了就从表尾开始找。

1. 从并发安全上分析

    Vector：线程安全
    ArrayList：非线程安全
    LinkedList:非线程安全

1. 数据增长分析

    Vector：缺省的情况下，增长为原数组长度的一倍。说到缺省，说明他其实是可以自主设置初始化大小的。

    ArrayList：自动增长原数组的50%。
