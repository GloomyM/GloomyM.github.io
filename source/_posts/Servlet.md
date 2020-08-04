---
title: Servlet
date: 2020-05-29 23:00:45
tags: Java
categories:
  - 学习历程
  - Java
---

### Servlet的实现

<!-- more -->

#### 方法1

编写类实现servlet接口，重写方法（不常用）

![](https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Servlet/Image_01.png)

#### Servlet配置文件

```xml
<servlet>
    <servlet-name>servlet类名</servlet-name>
    <servlet-class>类的地址(包名.类名)</servlet-class>
</servlet>
 
<servlet-mapping>
    <servlet-name>servlet类名</servlet-name>
    <url-pattern>该类映射地址</url-pattern>
  </servlet-mapping>
```

**Idea中已经提供了WebServlet注解用来直接配置，所以配置文件可以不写**

#### 方法2

编写类继承HttpService抽象类（常用）

```java
package Servlet;

import Dao.UserDao;
import Domain.User;
import View.UserView;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;


@WebServlet("/Login")

public class UserLoginServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html;charset=UTF-8");
        resp.setHeader("Cache-Control", "no-cache");
        resp.setCharacterEncoding("UTF-8");
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        User user = new User();
        user.setPassword(password);
        user.setUsername(username);
        UserDao dao = new UserDao();
        if(dao.JudgeLogin(user)){
            resp.getWriter().write("登录成功");

        }else{
            resp.getWriter().write("登录失败");
        }
    }
}

```

### Response对象

#### 简介

Servlet 最主要的作用就是处理客户端请求，并向客户端做出响应。为此，针对 Servlet 的每 次请求，Web 服务器在调用 service() 之前，都会创建两个对象，分别是 HttpServletRequest 和 HttpServletResponse其中

HttpServletRequest 用于封装 HTTP 请求消息，简称 request 对象

HttpServletResponse 用于封装 HTTP 响应消息，简称 response 对象

需要注意的是，在 Web 服务器运行阶段，每个 Servlet 都只会创建一个实例对象。然而，每次 HTTP 请求，Web 服务器都会调用所请求 Servlet 实例的 service(HttpServletRequest request,HttpServletResponseresponse)方法，重新创建一个 request 对象和一个 response 对象

#### getParameter(name)方法

获取浏览器中name对应的值

#### setStatus(intstatus)方法

发送状态码

#### setError(intsc,"提示信息")方法

当发送错误状态码时，Tomcat会跳转到固定的错误页面去，但可以显示错误信息。

#### 设置响应头

**setHeader(key,values)：**

​	设置键值对

**setContentType(Stringtype) ：**

​	设置 servlet 输出内容的 MIME 类型，对于 HTTP 来说，就是设置 Content-Type 响应头字 段的值

### Servlet文件下载

#### 下载的实质

文件下载的实质就是文件拷贝，将文件从服务器端拷贝到浏览器端。所以文件需要使用到 IO 流将服务器端的文件使用 InputStream 读取到，再使用 ServletOutputStream 写到 response 缓冲区中。

#### 方法1：

直接使用a标签，但是a标签不能下载所有的文件，有些文件可以直接被浏览器解析，所以该方法不推荐

#### 方法2：

通过代码使用IO流从服务器端读取数据并写入response缓存

```java
import javax.servlet.ServletException;
import javax.servlet.ServletOutputStream;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;

@WebServlet("/mydownload")
public class Download extends HttpServlet {
    /**
     * 1、获取文件名
     * 2、设置文件类型
     * 3、设置该文件以下载形式打开而不解析
     * 4、IO流输入输出
     * @param req
     * @param resp
     * @throws ServletException
     * @throws IOException
     */
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String filepath = "/download/"+req.getParameter("filename");
        String fileName = req.getParameter("filename");
        //设置文件的返回类型
        resp.setContentType(this.getServletContext().getMimeType(filepath));
        //告诉浏览器以下载的方式打开文件而不是直接解析
        resp.setHeader("Content-Disposition","attachment;filename="+fileName);
        int len = 0;
        ServletOutputStream out = resp.getOutputStream();
        //获取文件在浏览器中的地址
        String realPath = this.getServletContext().getRealPath(filepath);
        InputStream in = new FileInputStream(realPath);
        byte[] bytes = new byte[1024];//流的写入（敲黑板）
        while ((len = in.read(bytes)) != -1){
            out.write(bytes,0,len);
        }
        in.close();
        out.close();
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

    }
}

```

#### 问题

在使用response中的write方法时，前端页面会出现乱码，原因是本地的编码与浏览器上的编码出现异常，只需在write前加上如下语句即可解决

```java
resp.setContentType("text/html;charset=UTF-8");//设置浏览器编码
resp.setHeader("Cache-Control", "no-cache");
resp.setCharacterEncoding("UTF-8");//设置缓冲区编码
```

