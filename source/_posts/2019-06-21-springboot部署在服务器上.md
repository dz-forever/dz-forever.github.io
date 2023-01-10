---
layout: post
title: springboot项目部署在服务器上
date: 2019-6-21


tags: 
- springboot
- deploy

categories:
- [springboot, deploy]
---

# **springboot项目部署在服务器上**
## **准备工作**
### 1.在服务器上安装git,java,maven


安装java和maven配置的环境变量：


``` bash
entexport MAVEN_HOME=/usr/local/maven/apache-maven-3.6.1
export JAVA_HOME=/usr/local/java/jdk1.8.0_152
export JRE_HOME=/usr/local/java/jdk1.8.0_152/jre
export CLASSPATH=$CLASSPATH:$JAVA_HOME/lib:$JAVA_HOME/jre/lib
export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$MAVEN_HOME/bin:$PATH:$HOME/bin
```

### 2.git克隆代码

``` bash
git clone
```


将代码打成jar包

``` bash
mvn clean package -Dmaven.test.skip=true
```

### 3.构建镜像

创建一个image文件夹，创建Dockerfile文件：

``` bash
FROM openjdk:8-jre
MAINTAINER dz-forever <1871301001@qq.com>

RUN mkdir /app
COPY baidu-image-1.0-SNAPSHOT.jar /app/app.jar

ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "-jar", "/app/app.jar"]

EXPOSE 6002

```

将target下生成的jar包复制到image文件夹下，然后执行：

``` bash
docker build -t baiduimage .     
注意最后有一个点
```

### 4.使用docker-compose.yml文件运行镜像

在image文件夹下创建docker-compose.yml文件：

``` bash
version: '3.1'
services:
  baidu-image:
    image: baiduimage
    container_name: baidu-image
    ports:
      - 6002:6002
```

运行docker-compose.yml文件：

``` bash
docker-compose up -d 后台运行


查看项目启动日志：

docker -f logs   容器id
```

