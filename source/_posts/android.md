---
title: Android
tags: Reverse
categories: Android
date: 2019-03-12 23:28:10
---
##### 记录总结
- adb shell
- 逆向工具



<!-- more -->
```
adb shell
- adb pull /data/data/app.greyshirts.sslcapture/databases/schedule.db  拷贝模拟器数据到下载
- adb push  hm.apk /sdcard     拷贝apk到模拟器
- adb shell am start -D -n com.wudaokou.hippo/com.wudaokou.hippo.launcher.splash.SplashActivity 调试启动app的某个activity

逆向工具
- 基础工具链接

- mumu模拟器
- mt管理器--查看修改apk源码(修改smali,转换java查看)，动态修改保存编译
- 幸运破解器--去掉签名校验
- sqllite editor
- jeb

```
