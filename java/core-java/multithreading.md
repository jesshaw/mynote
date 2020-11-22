# 多线程

## 线程中的start和run的区别

启动一个线程，线程是就绪状态(runnable)，并没获得cpu。run时获得了cpu，线程处理运行状态(running)

## sleep和 wait的区别

1. sleep属于Thread静态方法，wait属于Object实例方法。
1. sleep时让出CPU给其他线程，不会释放锁，线程进入time-waiting状态，时间一到自动恢复运行状态；wait时，线程会放弃锁，当前线程进入waiting状态，只有等待另外线程的通知或被中断才会返回，获得对象锁进行运行状态。

## synchronized 关键字和 volatile 关键字的区别

1. 两者是互补存在，不是对立关系。
1. volatile关键字是线程同步的轻量级实现，所以volatile性能更好。但volatile只能修饰变量，synchronized用来修饰方法和代码块。synchronized关键字在jdk1.6之后为了减少获取和释放锁的性能消耗引入了偏向锁和轻量级锁以及各种优化之后执行效率显著提升。
1. 多线程访问volatile不会发生阻塞，而synchronized可能会。
1. volatile主要用于解决变量在多个线程中的可见性和有序性，而synchronized是 解决多个线程访问资源的同步性（原子性）。原子性、可见性和有序性为并发编程的三个重要特性。

## ThreadLocal理解和原理

ThreadLocal可以理解为线程的私有变量。如果创建了一个ThreadLocal变量，那么访问这个变量的每个线程都会有这个变量的本地副本。

ThreadLocal为ThreadLocalMap的封装，即最终的变量是放在ThreadLocalMap中。另因为ThreadLocalMap使用的key为ThreadLocal的弱引用，而value为强引用。尽管ThreadLocalMap考虑到了这可能会存在内存泄露问题，但我们使用完之后最好手动调用一下remove方法，清理key为null的记录。

## AtomicInteger类的原理

主要利用CAS(compare and swap), volatile和native方法保证原子操作。
