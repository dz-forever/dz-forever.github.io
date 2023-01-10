---
layout: post
title: Linux和Windows解决端口号占用问题
date: 2020-9-22

tags: 端口号占用
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



