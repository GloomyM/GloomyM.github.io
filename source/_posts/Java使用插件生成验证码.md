---
title: Java使用插件生成验证码
date: 2020-06-02 11:47:32
tags: Java
categories:
  - 学习历程
  - Java
---







#### 导入kaptcha的jar包

#### 配置文件

```xml
<servlet>
   <servlet-name>Kaptcha</servlet-name>
   <servlet-class>com.google.code.kaptcha.servlet.KaptchaServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>Kaptcha</servlet-name>
    <url-pattern>/kaptcha.jpg</url-pattern>
</servlet-mapping>
```

#### servlet



```java
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.awt.image.BufferedImage;
import java.io.IOException;

@WebServlet("/judgecode")
public class JudgeCode extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String code = (String) req.getSession().getAttribute(com.google.code.kaptcha.Constants.KAPTCHA_SESSION_KEY);
        String usercode = req.getParameter("usercode");
        System.out.println(code + "    " +usercode);
        if(code.equals(usercode)){
            System.out.println("Yes");
        }else {
            System.out.println("No");
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

    }
}

```

#### jsp

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 李之辰
  Date: 2020/6/2
  Time: 11:17
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
    <title>$Title$</title>
  </head>
  <body>
  <form action="/judgecode">
    验证码<input type="text" name = "usercode">
    <img src="/kaptcha.jpg" alt="">
    <input type="submit" value="提交">
  </form>
  </body>
</html>

```

