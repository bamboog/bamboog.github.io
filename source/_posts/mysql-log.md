---
title: Mysql-log
date: 2019-01-22 20:30:15
tags: mysql
categories: DB
---

#### redo log
- redo log是InnoDB存储引擎层的日志
- 事务开始后，就会产生redo log，就会陆续存入redo log,不会等到事物提交后

- 重做日志有一个缓存区Innodb_log_buffer，当重做日志缓存可用空间 少于一半时，重做日志缓存被刷新到重做日志文件

<!-- more -->

#### undo log
- undo log 回滚日志，保存了事务发生之前的数据的一个版本，可以用于回滚，同时可以提供多版本并发控制下的读（MVCC）

- 逻辑格式的日志，在执行undo的时候，仅仅是将数据从逻辑上恢复至事务之前的状态，而不是从物理页面上操作实现的，这一点是不同于redo log的

- 为了满足事务的原子性，在操作任何数据之前，首先将数据备份到一个地方（这个存储数据备份的地方称为UndoLo）。
然后进行数据的修改。如果出现了错误或者用户执行了ROLLBACK语句，系统可以利用UndoLog中的备份将数据恢复到事务开始之前的状态。


#### binlog
- binlog是MySQL Server层记录的日志

- 逻辑格式的日志，可以简单认为就是执行过的事务中的sql语句。
　　但又不完全是sql语句这么简单，而是包括了执行的sql语句（增删改）反向的信息

- 事务提交的时候，一次性将事务中的sql语句，记录到binlog,因此如果事物提交很大，提交就会变慢

#### 为什么数据同步使用的binlog
- 我的理解，binlog是mysql的，底层引擎不一定是innodb,如果使用redo log,换了引擎还得换。。。

#### binlog日志格式
- Statement 记录：执行的sql语句,可能有些函数执行问题，比如时间函数等
- Row       记录：相关数据记录，可能量很大
- Mixed     s+r：


#### 事务案例

##### Undo+Redo-事物过程
假设有A、B两个数据，值分别为1,2.
- 事务开始.
- 记录A=1到undolog.
- 修改A=3.
- 记录A=3到redolog.
- 记录B=2到undolog.
- 修改B=4.
- 记录B=4到redolog.
- 将redolog写入磁盘。
- 事务提交


#####  Undo+Redo特性
- 为了保证持久性，必须在事务提交前将RedoLog持久化。
- 数据不需要在事务提交前写入磁盘，而是缓存在内存中。
- RedoLog保证事务的持久性。
- UndoLog保证事务的原子性。
- 有一个隐含的特点，数据必须要晚于redolog写入持久存
