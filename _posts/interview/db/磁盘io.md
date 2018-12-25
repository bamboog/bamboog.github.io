#### 磁盘IO

##### 物理结构
  - 硬件
    - 盘片，
    - 扇区，硬盘中每个扇区的大小固定为512字节
    -
  - 性能的因素 -寻道时间-旋转延迟-数据传输时间
  - 衡量指标
    - IOPS  Input/Output Per Second
    - 7200rpm的磁盘 IOPS = 76 IOPS，10000rpm的磁盘IOPS = 111 IOPS，15000rpm的磁盘IOPS = 166 IOPS
    - 吞吐量  吞吐量（Throughput），指单位时间内可以成功传输的数据数量
    - SSD iops在几千以上

  - 操作系统层的优化
    - 虚拟文件系统层（VFS Layer）Virtual File System-- 文件系统管理者
      - 超级块（Super Block）
      - 索引结点（Inode）
      - 目录项（Dentry）
      - 文件对象（File）

    - Ext2文件系统
      - Ext2文件系统来说，硬盘分区首先被划分为一个个的Block
      - Ext2将这些Block聚集在一起分为几个大的块组（Block Group）
      - ssd block 4k,block一般是1k,4k
    - Page Cache层
      - Page Cache主要用来作为文件系统上的文件数据的缓存来用，尤其是针对当进程对文件有read/write操作的时候。Buffer Cache则主要是设计用来在系统对块设备进行读写的时候，对块进行数据缓存的系统来使用。
      - 磁盘Cache有两大功能：预读和回写
      - Page Cache层的最小单元是页（Page）
      - page->buffer->block->secter(512)
      - 目前的设计来看，pageCache里面包含的就是Buffer,linux free命令看到的cache就是PageCache,buffers（元数据信息、原始的磁盘 block IO，很小）

    - 通用块层
    - I/O调度层
      - 常见的I/O调度算法包括Noop调度算法（No Operation）、CFQ（完全公正排队I/O调度算法）、DeadLine（截止时间调度算法）、AS预测调度算法等。
  - 基于磁盘I/O特性设计的技巧--良好的读性能和写性能往往不可兼得。在许多常见的开源系统中都是优先在保证写性能的前提下来优化读性
    - 采用追加写 -- 顺序写 -- 读慢
      - 数据是被整体访问，比如HDFS--一次写多次读
      - 知道文件明确的偏移量，比如Kafka--- patition大文件又分成了多个小文件段，每个小文件段以偏移量命名，通过多个小文件段
      - 简单的方式是像Kafka那样，将文件数据有序保存，使用二分查找来优化效率；或者通过建索引的方式来进行优化；也可以采用hash的方式将数据分割为不同的桶
      - 那么有没有一种办法在保证写性能不损失的同时也提供较好的读性能呢
        - 日志结构的合并树LSM（The Log-Structured Merge-Tree）是HBase，LevelDB等NoSQL数据库的存储引擎
      - 小文件合并
        - 淘宝的TFS就采用了小文件合并存储的策略
    -
