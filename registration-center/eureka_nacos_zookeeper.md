## Eureka、Nacos、Zookeeper

### CAP 理论


### Eureka

Spring Cloud Eureka，使用 Netflix Eureka 来实现服务注册与发现，既提供了服务端，也提供了客户端。

- 服务端：我们也称为注册中心，它是依托于强一致性的高可用注册中心
Eureka 如果以集群的方式进行部署，当集群中有分片出现故障时，那么 Eureka 就会转入自我保护模式。它允许在分片故障期间继续提供服务的发现和注册，当故障分片恢复时候，集群中的其他分片会把他们的状态再次同步过来。注册中心的服务是两两相护注册，实现了完全去中心化的一个设计理念。在 Eureka 的服务治理设计中，所有的节点既是提供方，又是消费方，包括注册中心。

- 客户端：主要处理服务的注册与发现
Eureka 客户端通过注解和参数配置的方式，嵌入在客户端的程序代码中。Eureka 客户端向注册中戏呢注册自己提供的服务，并周期性地发送心跳来更新它的服务租约。同时，它也能从注册中心查询当前注册中心的服务信息，并发他们缓存到本地，并周期性地刷新服务状态。

**服务治理机制：**

<image src="https://github.com/chunghwa-2018/case-interview/tree/main/registration-center/images/Eureka-Service-Governance-Mechanism.png" width="600px">

### Nacos

### Zookeeper

