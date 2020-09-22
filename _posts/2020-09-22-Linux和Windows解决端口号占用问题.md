---
layout: post
title: Linux和Windows解决端口号占用问题
data: 2020-9-22

tags: Linux和Windows解决端口号占用问题
description: Linux和Windows解决端口号占用问题
---

# **1.Linux**

```
netstat -tunlp|grep 端口号
得到pid
kill pid
```

# **2.Windows**

```
netstat -ano|findstr 端口号
taskkill /F /PID pid
```



