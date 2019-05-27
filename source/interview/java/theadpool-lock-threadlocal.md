#### 线程池
  - ThreadPoolExecutor: coreSize,maxSize,queue,reject策略（丢弃抛异常，丢弃不抛异常，丢弃队列里面最前面的任务，调度线程执行）
  - 重点需要监控
  - LinkedBlockingQueue
    - l
  - 手写代码？
#### 锁__锁
  - synchronized
    - d
  - Lock
    - ReentrantLock
    -
  - AbstractQueuedSynchronizer

#### ThreadLocal
- ThreadLocalMap- 如果一个对象具有弱引用，在GC线程扫描内存区域的过程中，不管当前内存空间足够与否，都会回收内存
  - 代码
    ```java

          /**
          * The table, resized as necessary.
          * table.length MUST always be a power of two.
          */              
          private Entry[] table;    
           /**
            * The number of entries in the table.
            */
           private int size = 0;

           /**
            * The next size value at which to resize.
            */
           private int threshold; // Default to 0

    ```
  - Thread
    - code-带了一个map
    ```
    ThreadLocal.ThreadLocalMap threadLocals = null;
    ```
  - 为何内存泄漏
    -
  - set,get设计

- Thread--线程
  - 状态
    - blocked - eg: java.io.InputStream#read()  -  This method blocks until input data is available
    - runnable running
    -
  - 方法
  ```
  过期方法1—– stop 方法
  过期方法2——suspend 方法和 resume 方法
  常用方法1——线程中断方法 interrupt，isInterrupted，static interrupted
  常用方法2——等待线程结束 join 方法
  常用方法3——线程让出时间片 yield 方法
  ```
  -
