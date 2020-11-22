# Spring内核

## Spring bean生命周期

bean生成---销毁

bean定义（BeanDefinition）

1. scope
2. initMethod
3. byName byType
4. dependsOn
5. beanClass

实例化->填充属性->BeanNameAware绑定Name ID->BeanFactoryAware绑定Factory->ApplicationContextAware绑定上下文->
Bean后置处理器预初始化->InitializingBean的后属性设置->自定义初始化方法->Bean后置处理器的后初始化->
放到单例池待用->
DisposableBean的销毁方法->自定义销毁方法
![Spring bean生命周期](assets/ec51edca3976e7e89132c88f3c524abe1e7de7d65f192906deb5cc6e96b683c2.png)  

## Bean创建的几种方式

1. @Bean
1. 配置器创建
1. BeanFactory.registerSingleton

## ApplicationContext与BeanFactory的区别

ApplicationContext扩展了BeanFactory的功能，也扩展了其他的比如环境，国际化等等功能。

## 拦截器和过滤器什么区别

Spring的拦截器与Servlet的过滤器Filter有很多相似之处，比如两者都是AOP编程思想的体现，都能实现权限检查、日志记录等，不同的是：

1. 使用范围不同：Filter是Servlet规范规定的，只能用于Web程序中，而拦截器既可以用于Web程序，也可以用于Application、Swing程序中
2. 规范不同：Filter是Servlet规范中定义的，是Servlet容器支持的。而拦截器是在Spring容器内的，是Spring框架支持的
3. 使用的资源不同：拦截器是一个Spring的组件，归Spring管理，配置在Spring文件中，因此能使用Spring里的任何资源、对象，例如Service对象、数据源、事务管理等，通过IoC注入到拦截器即可，而Filter则不能
4. 深度不同：Filter只在Servlet前后起作用。而拦截器能够深入到方法前后、异常抛出前后等，因此拦截器的使用具有更大的弹性。所以在Spring架构的程序中，要优先使用拦截器。
5. 实现原理不同：拦截器是基于动态代理来实现的，而过滤器是基于函数回调来实现的。
6. 作用域不同：拦截器只对Action起作用，过滤器可以对所有请求起作用。
7. 调用次序不同：在action的生命周期中，拦截器可以多次被调用，而过滤器只能在容器初始化时被调用一次。

## Spring怎样解决bean循环依赖的问题

bean后置处理器(BeanPostProccess，这里的后置指的是Bean生命周期的每个节点都有执行)解决的。构造器循环依赖直接运行失败，属性和方法循环依赖不会。

[引用](https://www.bilibili.com/video/BV1tx411o77Z?p=10)

## Spring中的AOP是怎么实现的

使用代理的方式实现。若是接口则使用jdk动态代理，若是类使用cglib。

## 为什么java动态代理必须是接口

因为jdk动态代理生成的类默认继承Proxy，Java是单继承方式。

## Spring和事务的关系

Spring和事务之间是管理关系。

## Spring提供三个接口供我们使用事务

TransactionDefinition：平台事务管理器，PlatformTranscationManager：事务定义（隔离级别，传播行为，超时，只读，回滚规则）, TransactionStatus：事务运行状态。
