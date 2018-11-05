## Think Mysql

- 设计
  - int(1),varchar(20)
- 优化
  - explain,desc
  - type类型：ALL,Index,range,
  - 排序文件，临时文件
- 索引
  - B+
  - page(16k),内存硬盘映射缓存；
- 死锁
  - t1: start transaction;update set xxx=1 where  id=1;
  - t2: start transaction;update set xxx=1 where id = 2;
  - t1: update set xxx=2 where  id=2; 等待 t2释放lock;
  - t2: update set xxx=2 where id=1;  等待 t1释放lock
  - 这样就死锁了

锁分类：
- 表锁
- 行锁
  - 共享锁
  - 排它锁
