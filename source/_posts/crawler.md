---
title: Crawler
tags: Java
categories: Language
date: 2019-03-09 09:30:25
---

##### 基本流程
- apktool 逆向apk
- 修改
- apktool 打包apk
- jarsigner签名
- 安装
- 调试

<!-- more -->

```
逆向:apktool d  xxx.apk
打包:apktool b  xxx (逆向后的文件目录名)，生成的新apk在dist下面
签名-两步:
1. keytool -genkeypair -alias adorkable_alias -keyalg RSA -validity 400 -keystore adorkable.keystore
   -genkeypair 指定生成密钥对
   -alias 密钥对的别名
   -keyalg 密钥对用于的算法，这里用的是RSA
   -validity 密钥对的有效期，单位为天
   -keystore 密钥对存储的文件名

2.jarsigner -verbose -keystore adorkable.keystore -signedjar singed.apk unsigned.apk adorkable_alias
  -verbose 输出签名详细信息
  -keystore 指定密钥对的存储路径
  -signedjar 后面三个参数分别是 签名后的APK包 未签名的APK包 和 密钥对的别名

安装:abd install xxx.apk

调试：jeb
```
