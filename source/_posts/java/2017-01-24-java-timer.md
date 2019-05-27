---
title:  java-定时器
date: 2017-01-24
tags: Java
---

## 常用定时器
  - Timer
  - ScheduledThreadPoolExecutor
  - QuartZ
  - Linux Cron
  - Spring-@Scheduled
  - BSchedule [自己造轮子](https://github.com/bamboog/BSchedule)
<!-- more -->

#### Timer
  - 定时的理解
    - 每天早上八点起床 --- 一个任务
      - 每天  -- 24小时一个轮  period
      - 早上八点 -- nextExecutionTime
    - 多个任务，怎么存多个 --- 队列(其他的数据结构对么)

  - 如果自己来抽象这样一个定时类，你会如何
    ```java
    public class BTimer {
      class BTask {
          /**
           * 轮期- eg:每天
           */
          long period;
          /**
           * 执行时间点，eg:早上八点
           */
          long nextExTime;
      }
      class BTaskQueue {
          /**
           * 队列列表
           */
          private BTask[] queue = new BTask[64];
          /**
           * 队列大小
           */
          private int size;
      }
    }
    ```
  - 它是怎么做的
    - 入口-去掉非关键代码
      ```java
      //核心代码入口 timer.schedule -> sched
      private void sched(TimerTask task, long time, long period) {
         synchronized(queue) {
             synchronized(task.lock) {//赋值
                 task.nextExecutionTime = time;
                 task.period = period;
                 task.state = TimerTask.SCHEDULED;
             }
             queue.add(task);//入队列
             if (queue.getMin() == task)
                 queue.notify();
         }
       }
       ```                
    - 主loop
      ```java
        private void mainLoop() {
          while (true) {
              try {
                  TimerTask task;boolean taskFired;
                  synchronized(queue) {
                      // Wait for queue to become non-empty
                      while (queue.isEmpty() && newTasksMayBeScheduled)queue.wait();
                      if (queue.isEmpty())break; // Queue is empty and will forever remain; die
                      // Queue nonempty; look at first evt and do the right thing
                      long currentTime, executionTime;
                      task = queue.getMin();
                      synchronized(task.lock) {
                          if (task.state == TimerTask.CANCELLED) {
                              queue.removeMin();
                              continue;  // No action required, poll queue again
                          }
                          currentTime = System.currentTimeMillis();
                          executionTime = task.nextExecutionTime;
                          if (taskFired = (executionTime<=currentTime)) {
                              if (task.period == 0) { // Non-repeating, remove
                                  queue.removeMin();
                                  task.state = TimerTask.EXECUTED;
                              } else { // Repeating task, reschedule
                                  queue.rescheduleMin(
                                 task.period<0 ? currentTime   - task.period: executionTime +task.period);
                              }
                          }
                      }
                      if (!taskFired) // Task hasn't yet fired; wait
                          queue.wait(executionTime - currentTime);
                  }
                  if (taskFired)  task.run(); // Task fired; run it, holding no locks
              }
          }
        }
      ```

    - 队列设计
      - 最小堆
      - add-task
        ```java
        private void fixUp(int k) {
        while (k > 1) {
            int j = k >> 1;
            if (queue[j].nextExecutionTime <= queue[k].nextExecutionTime)
                break;
            TimerTask tmp = queue[j];  queue[j] = queue[k]; queue[k] = tmp;
            k = j;
        }
       }
        ```
      -

- 原理
  - 主要靠wait,notify
- 存在的问题
  - 依赖系统时间
  - 单线程
  - 只处理了InterruptedException，其他异常会中断任务
- 如果是你，怎么改进
  - nanoTime 相对时间
  - 线程池
  - 异常捕获

#### ScheduledThreadPoolExecutor
  - 相比Timer,突出的是什么
    - nanoTime
    - extends ThreadPoolExecutor
    - 异常处理
      ```java
      try {
          beforeExecute(wt, task);
          Throwable thrown = null;
          try {
              task.run();
          } catch (RuntimeException x) {
              thrown = x; throw x;
          } catch (Error x) {
              thrown = x; throw x;
          } catch (Throwable x) {
              thrown = x; throw new Error(x);
          } finally {
              afterExecute(task, thrown);
          }
      } finally {
          task = null;
          w.completedTasks++;
          w.unlock();
      }
      ```
  - 所以设计

#### BSchedule
  - 为什么要做
  - 怎么做
