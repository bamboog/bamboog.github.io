---
layout: post
title: special java
date: 2017-12-12
tags: JAVA
---
## special java--- why do like this?
```java
   public final static int COMPRESSED_FLAG = 0x1;
   public final static int MULTI_TAGS_FLAG = 0x1 << 1;
   public final static int TRANSACTION_NOT_TYPE = 0;
   public final static int TRANSACTION_PREPARED_TYPE = 0x1 << 2;
   public final static int TRANSACTION_COMMIT_TYPE = 0x2 << 2;
   public final static int TRANSACTION_ROLLBACK_TYPE = 0x3 << 2;

   public static int getTransactionValue(final int flag) {
       return flag & TRANSACTION_ROLLBACK_TYPE;
   }
   public static int resetTransactionValue(final int flag, final int type) {
       return (flag & (~TRANSACTION_ROLLBACK_TYPE)) | type;
   }
   public static int clearCompressedFlag(final int flag) {
       return flag & (~COMPRESSED_FLAG);
   }
```
## 解释
http://www.jianshu.com/p/11f331d97ec2
###### 权限
```c++
1 添加权限

增加权限使用 或（|） 运算实现。
如，为某用户增加“读取”、“写入”两种权限。
“读写”两种权限，权限码为6（110），本质是由权限码2（010）和4（100）进行或（|）运算后实现，即6 = 2 | 4，当然直观也可以视作基本的算术加 6 = 2 + 4 计算得出。

2 判断权限

在需要判断用户权限时，可使用 与（&） 运算。
如，判断权限码为6用户是否有读取权限。权限码6（110）和4（100）的与运算结果为4，即：4 = 6 & 4。
如，判断权限码为6用户是否有执行权限。权限码6（110）和1（001）的与运算结果为0，即：0 = 6 & 1。

总结下就是，当与运算结果为所要判断权限的本身值时，我们可以认为用户具有这个权限。而当运算结果为 0 时，我们可以认为用户不具有这个权限。

3 移除权限

移除用户的权限可使用 异或（^） 运算。
如，将权限码为7的用户，移除执行权限。权限码7（111）和1（001）的异或运算结果为6，即：6 = 7 ^ 1，也可以由算术减 6 = 7 - 1计算得出。


```

###### hashmap

```java

/**
    * Returns a power of two size for the given target capacity.
    */
   static final int tableSizeFor(int cap) {
       int n = cap - 1;
       n |= n >>> 1;
       n |= n >>> 2;
       n |= n >>> 4;
       n |= n >>> 8;
       n |= n >>> 16;
       return (n < 0) ? 1 : (n >= MAXIMUM_CAPACITY) ? MAXIMUM_CAPACITY : n + 1;
   }
```
###### java_Modifier
