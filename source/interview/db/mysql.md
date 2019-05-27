####  Mysql

- 最大连接数  100000   我们线上5000
- 优化
  - explain type  full table ,full index,ref ,eq_re,还需要关注 extra属性
- 事物
  - 事物
    - ACID 四大特性：原子性（Atomicity）、一致性（Consistency）、隔离性（Isolation）和持久性（Durability）
  - 隔离性
    - 隔离级别的实现
    - 锁，时间戳（乐观锁）,多版本和快照隔离(MVCC)

  - 传播-嵌套-spring
    - 传播-PROPAGATION_REQUIRED  默认-没有就新来个
    - 嵌套，事物方法调用事物方法，try catch后抛异常，默认RuntimeEx

- 锁：
  - 粒度：表锁-页锁-行锁
  - 模式：LOCK_S（读锁，共享锁），–LOCK_X（写锁，排它锁）
  - 属性：
    - LOCK_REC_NOT_GAP（锁记录）
    - LOCK_GAP（锁记录前的GAP）
    - LOCK_ORDINARY（同时锁记录+记录前的GAP，0。传说中的Next Key锁）
    - LOCK_INSERT_INTENTION（插入意向锁）-- 表锁，意向锁不会与行级的共享 / 排他锁互斥

- 日志
  - 回滚日志  undo --(撤销)  ---  持久性
  - 重做日志  redo          ---  原子

  - binlog
    - mix
    - colum
    - row

- 索引
  - B+
  - 聚集索引（clustered index）和辅助索引（secondary index）
