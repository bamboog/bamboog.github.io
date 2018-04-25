---
layout: post
title: ZooKeeper
date: 2018-01-09
tags: 分布式
---
## ZooKeeper

- #### 简易安装
  - 官网下载 https://zookeeper.apache.org
  - 解压
  - cd /conf  mv zoo_sample.cfg zoo.cfg
  - cd  ../bin   
  - ./zkServer.sh start  (server)
  - zkCli.sh  (client)
  类似如下：
  ```Java
  ➜  bin ./zkCli.sh
  Connecting to localhost:2181
  2018-01-09 20:56:52,645 [myid:] - INFO  [main:Environment@100] - Client environment:zookeeper.version=3.4.11-37e277162d567b55a07d1755f0b31c32e93c01a0, built on 11/01/2017 18:06 GMT
  2018-01-09 20:56:52,649 [myid:] - INFO  
  ...
  ```
  就可以开始你的旅行了.....

- #### 基本命令
  - ls /
  - ls2 / (多了其它相关信息，比如时间，版本等)
  - create /test "default"
  - get /test
  - set /test "tt"
  - delete /test
  - help
  备注：
  /XXX  代表一个znode

- #### Java端

- #### 生产
- #### 场景
  - 配置中心
  - 负载均衡（mq）
  - name server (dubbo)
  - 分布式通知/协调
  - 集群管理/master选举
  - 分布式锁/队列/计数

- #### 原理
  - Paxos
    - 问题案例：
      - 在传统拍卖场景中，价高者先得，这些拍卖者都是在同一个房间，彼此能够直接看得到对方的报价，如果我们假设分布式拍卖是将这些拍卖者分离到不同的地方，这样我们可以用拍卖者之间的联系模拟分布式计算机之间的通讯。
      - 假设拍卖者各自在自己家里拍卖，通过邮局信件发出自己的拍卖信息，拍卖者之间除非等到邮局投递人告诉他们彼此之间的报价，否则是无法知道对方报价的。如果邮局信件投递这个环节出了问题，投递速度慢了甚至无法投递了，那么整个拍卖程序就无法继续进行下去。
    - 解决共识问题（consensus problem）
      - ![](https://bamboog.github.io/images/paxos.png)
      - 第一次由提交者Leader向所有其他服务器发出prepare消息请求准备，所有服务器中大多数如果回复诺言承诺就表示准备好了，可以接受写入；第二次提交者向所有服务器发出正式建议propose，所有服务器中大多数如果回复已经接收就表示成功了。
    - 。。。。

-
