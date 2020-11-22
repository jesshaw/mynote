# 微服务

## 谈谈微服务注册中心Zookeeper&Eureka

Zookeeper基于监听机制（临时节点）通知消费者服务状态。Eureka每30秒续命告知注册服务器。消费方每30秒拉取，刷本地缓存。

Zookeeper，奇数台做集群，CP(强一 致性）。Eureka，只需两台以上即可，AP（可用性）。

## 谈谈互联网常见的负载均衡

服务端负载均衡如Nginx。客户端负载均衡如Dubbo的Proxy，Spring Cloud的Ribbon。

负载均衡常见方式有轮询、权重、最小活跃数、ip_hash、一致性hash。

[引用](https://zhuanlan.zhihu.com/c_1050762683808403456)

## 分布式事务解决方案有哪些

- 全局事务(X/Open Distributed Transaction Processing Reference Model)
- 基于可靠消息服务的分布式事务
- 最大努力通知
- TCC（两阶段型，补偿型）

[引用](https://juejin.im/post/6844903573667446797)
