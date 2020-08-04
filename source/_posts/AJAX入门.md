---
title: AJAX
date: 2020-06-08 20:20:29
tags: Java
categories:
  - 学习历程
  - Java
---

### 概述 

AJAX 是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。 

<!-- more -->

### AJAX 应用场景 

搜索框输入关键字时，JavaScript 会把这些字符发送到服务器，然后服务器会返回一个搜索 建议的列表。 实时翻译，在翻译框输入内容,会实时显示翻译结果，网站注册账号 

### AJAX实现

1、创建 XMLHttpRequest 对象（JS 对象）

2、注册请求的监听事件  

**readyState** 

- 0 请求未初始化 
- 1 服务器连接已建立 
- 2 请求已接收 
- 3 请求处理中 
- 4 请求已完成,且响应已就绪 

**status**  

- 200 请求成功
- 404 未找到界面 

3、打开和服务器的连接

4、发送请求

```jsp
<%--
  Created by IntelliJ IDEA.
  Date: 2020/6/8
  Time: 16:47
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
    <title>$Title$</title>
  </head>
  <body>
  <button type="submit" onclick="ajax()">提交</button>
  </body>
  <script type="text/javascript">
    function ajax() {
      //创建XMLHttpRequest对象
      var x = new XMLHttpRequest();
      x.onreadystatechange = function(){
        //注册请求的监听事件
        if(x.status == 200 && x.readyState == 4){
          alert(x.responseText);
        }
      }
      /**
       打开和服务器的连接open(method,url,async)
       method:请求的类型
       url:请求的url
       async:true（异步）或 false（同步）
       **/
      x.open("post","/ajax1");
      //请求为post类型时需要设置setRequestHeader，且位置必须在打开服务器连接之后
      x.setRequestHeader("Content-type","application/x-www-form-urlencoded");
      /**
       * send(String) 将请求发送到服务器
       * string:设置 POST 请求携带的参数
       */
      x.send("username=lisi");
    }
  </script>
</html>

```

```java
package Servlet;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/ajax1")
public class AJAX1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String username = req.getParameter("username");
        System.out.println(username);
        resp.getWriter().write("1111111");
    }
}

```

### AJAX（jQuery）

jQuery 对 JS 原生的 AJAX 进行了封装

#### `$.get和$.post`

参数：

1. url：表示请求的服务器端地址 
2. ata：表示请求服务器端的数据（可以是 key=value 形式也可以是 JSON 格式）
3. callback：表示服务器端成功响应所触发的函数（只有正常成功返回才执行） 

4. type：表示服务器端返回的数据类型（jQuery 会根据指定的类型自动类型转换） 常用的返回类型：text、json、html 等 

#### `$.ajax`

参数： 

​	1.async：是否异步，默认是 true 代表异步 

​	2.data：发送到服务器的参数，建议使用 json 格式 

​	3.dataType：服务器端返回的数据类型，常用 text 和 json

​	4.success：成功响应执行的函数，对应的类型是 function 类型

​	5.type：请求方式，POST/GET 6. url：请求服务器端地址 