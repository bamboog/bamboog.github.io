---
title:  object
date: 2017-03-12
tags: Java
---
####  Object类的基本方法
      - thing put before--对象

```java
public class Object {
    public boolean equals(Object obj) {
        return (this == obj);
    }
    public String toString() {
        return getClass().getName() + "@" + Integer.toHexString(hashCode());  
    }
    protected void finalize() throws Throwable { }

    public native int hashCode();

    public final native Class<?> getClass();

    private static native void registerNatives();

    protected native Object clone() throws CloneNotSupportedException;

    public final native void notify();

    public final native void notifyAll();

    public final native void wait(long timeout) throws InterruptedException;
  }

```

#### 如果是你，你会想到怎么设计抽象这个Object类么？
####  为什么这么设计呢？
      - hashCode
      - equals
      - toString
      - clone
      - notify
      - wait
