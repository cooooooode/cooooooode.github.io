---
title: "搭建Java开发环境"
date: 2021-07-27 11:35
banner:
tags:
  - Java
  - JDK
  - Maven
---

### 1. 下载JDK并配置环境变量

去oracle官网 [https://www.oracle.com/cn/java/technologies/javase-downloads.html](https://www.oracle.com/cn/java/technologies/javase-downloads.html)
下载JDK， 选择 [Java SE 16](https://www.oracle.com/java/technologies/javase-jdk16-downloads.html), 然后选择对应的平台来下载。

这里以macOS二进制为例，安装jdk后，需要配置相关Java环境变量

```bash
export JAVA_HOME=$(/usr/libexec/java_home)
export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar
export PATH=$PATH:$JAVA_HOME/bin
```

### 2. 下载Maven并配置环境变量

去apache maven官网下载maven并解压缩 [https://maven.apache.org/download.cgi](https://maven.apache.org/download.cgi),  这里我解压缩并移动到`/usr/local`目录下。

接下来就是配置maven环境变量

```bash
export M2_HOME=/usr/local/apache-maven-3.8.1
export PATH=$PATH:$M2_HOME/bin
```

### 3. 下载编辑器IDEA

去jetbrains官网[https://www.jetbrains.com/idea/download/#section=mac](https://www.jetbrains.com/idea/download/#section=mac) 下载M1版本。

完成后可以安装无限试用插件, 点Preferences->Plugins->Manage Plugin Repositories添加仓库地址 `https://plugins.zhile.io/`， 然后搜索`IDE Eval Reset`插件进行安装。

针对IDEA不能运行单个文件的问题，选择File->Project Structure->Modules中把你代码所在文件夹选为Sources然后确定。