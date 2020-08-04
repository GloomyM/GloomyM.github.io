---
title: Tomcat
date: 2020-06-01 22:35:58
tags: Java
categories:
  - 学习历程
  - Java
---

### 简介

Tomcat 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用服务器，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP 程序的首选。对于一个初学者来说，可以这样认为，当在一台机器上配置好Apache 服务器，可利用它响应HTML（标准通用标记语言下的一个应用）页面的访问请求。实际上Tomcat是Apache 服务器的扩展，但运行时它是独立运行的，所以当你运行tomcat 时，它实际上作为一个与Apache 独立的进程单独运行的。

<!-- more -->

### 安装方式

<a href= "https://tomcat.apache.org/">下载地址</a>

选择你需要的版本，推荐下载压缩包

### 环境配置

Tomcat下载并解压后，找到bin文件夹，将该文件夹的目录加入环境变量，或者直接将%CATALINA_HOME%\bin加入环境变量，两种方法都是有效的，环境变量配置好后启动Tomcat，浏览器输入localhost:8080如果可以进入Apache-Tomcat的页面说明Tomcat安装并配置成功，可以使用。

### 问题

在安装配置完成后，可能会出现CMD中乱码的情况，这个改下注册表就行了，win+r，输入regedit，根据下面的路径，依次打开HKEY_CURRENT_USER -> Console ->TomCat，若TomCat不存在则新建一个，并新建DWORD，设置十进制为65001，然后保存，重新打开Tomcat就解决了