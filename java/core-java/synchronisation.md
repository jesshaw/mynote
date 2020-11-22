# 同步

## Java的锁有哪些

悲观锁，乐观锁；自旋锁，适应性自旋锁；无锁，偏向锁，轻级锁，重量级锁；公平锁，非公平锁；可重入锁，非可重入锁；共享锁，排他锁；闭锁等。
![Java主流锁](assets/eef71e35fd85563bd869be921ee80a899c4257a09eac7af2d35d9e2035baeca6.png)  

[Java主流锁原图](https://www.processon.com/mindmap/5f43286a5653bb57696cba##)  

[美团锁事](https://tech.meituan.com/2018/11/15/java-lock.html)

## 说说synchronized的底层原理

synchronized是由一对monitorenter和monitorexit指令来实现同步的，在JDK6之前，monitor的实现是依靠操作系统内部的互斥锁来实现的，所以需要进行用户态和内核态的切换，所以此时的同步操作是一个重量级的操作，性能很低。

但是，JDK6带来了新的变化，提供了三种monitor的实现方式，分别是偏向锁，轻量级锁和重量级锁，即***锁会先从偏向锁再根据情况逐步升级到轻量级锁和重量级锁。 这就是锁升级***。

在锁对象的对象头里面有一个threadid字段，默认情况下为空，当第一次有线程访问时，则将该threadid设置为当前的线程id，我们称为让其获取***偏向锁***，当线程执行结束，则重新将threadid设置为空。

之后，如果线程再次进入的时候，会先判断threadid与该线程的id是否一致，如果一致，则可以获取该对象，如果不一致，则发生锁升级，从偏向锁升级为***轻量级锁***

轻量级锁的工作模式是通过自旋循环的方式来获取锁，看对方线程是否已经释放了锁，如果执行一定次数之后，还是没有获取到锁，则发生锁升级，从轻量级锁升级为***重量级锁***。

使用锁升级的目的是为了减少锁带来的性能消耗。

通过反编译查看字节码，就可以看到相关的指令

javap -verbose Test.class

源码：就是写了synchronized同步代码块控制线程安全

    ```
    Code:
        stack=2, locals=4, args_size=1
            0: new           #2                  // class java/lang/Object
            3: dup
            4: invokespecial #1                  // Method java/lang/Object."<init>":()V
            7: astore_1
            8: aload_1
            9: dup
            10: astore_2
            11: monitorenter
            12: getstatic     #3                  // Field java/lang/System.out:Ljava/io/PrintStream;
            15: ldc           #4                  // String 获得锁
            17: invokevirtual #5                  // Method java/io/PrintStream.println:(Ljava/lang/String;)V
            20: aload_2
            21: monitorexit
            22: goto          30
            25: astore_3
            26: aload_2
            27: monitorexit
            28: aload_3
            29: athrow
            30: return
    ```

**synchronized如何保证可见性的？**

首先，我们需要知道可见性原理。

两个线程如何保证变量信息的共享可见性？需要经历以下的流程：

线程A-》本地内存A（共享变量副本）-》主内存（共享变量）

如果有变更，需要将本地内存的变量写到主内存，对方才可以获取到更新。

这个是提前知识。

那么，synchronized是如何保证可见性的

就是***当获取到锁之后，每次读取都是从主内存读取，当释放锁的时候，都会将本地内存的信息写到主内存，从而实现可见性***

## synchronized与Lock的区别

1. 原始构成
    - synchronized是关键字属于JVM层面（ monitorenter， monitorexit）
    - Lock是具体类是API层的锁
2. 使用方法
    - synchronized不需要用户去手动释放锁，当synchronized代码执行完后系统会自动让线程释放对锁的占用
    - ReentrantLock则需要用户去手动释放锁，若没有主动释放锁，就可能导致出现死锁的现象。
        需要lock()各unlock()方法配合try/finally语句块来完成。
3. 等待是否可中断
    - synchronized不可中断，除非抛出异常或者正常运行完成
    - ReentrantLock可中断，
        1. 设置超时方法trylock(long timeout,TimeUnit unit)
        2. lockInterruptibly()放代码块中，调用interrput()方法中断
4. 加锁是否公平
    - synchronized非公平锁
    - ReentrantLock两者都可以，默认为非公平锁
5. 锁绑定多个条件Condition
    - synchronized没有
    - ReentrantLock用来实现分组唤醒的线程们，可以精确唤醒，而不是synchronized要么随机唤醒一个线程要么唤醒全部线程

## 锁分段原理
