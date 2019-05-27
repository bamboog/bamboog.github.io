### Cluster
分布式系统中，集群一般涵盖了负载均衡(LoadBalance),高可用(HA),路由(Route)等等概念

- 负载均衡可以分为服务端负载均衡和客户端负载均衡，
  - 服务端负载均衡nginx,型的软件负载均衡
  - 客服端负载均衡-- duboo负载均衡
  - 就是根据请求返回一个服务节点
  - 算法:
    - Round Robin
    - Random
    - Hash
    - ConsistentHash

- HA
  - failover
  - failfast
  - forking
  - broadcast
