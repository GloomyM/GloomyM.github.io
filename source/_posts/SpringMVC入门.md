---
title: SpringMVC
date: 2020-07-10 15:54:24
tags: SpringMVC
categories:
 - 学习历程
 - SSM
---

## SpringMVC简介

MVC 全名是 Model View Controller，是模型(model)－视图(view)－控制器(controller)的缩写， 是一种用于设计创建 Web 应用程序表现层的模式。MVC 中每个部分各司其职：  

Model（模型）:通常指的就是我们的数据模型。作用一般情况下用于封装数据。  

View（视图）:通常指的就是我们的 jsp 或者 html。作用一般就是展示数据的。   通常视图是依据模型数据创建的。

<!--more-->

Controller（控制器）:是应用程序中处理用户交互的部分。作用一般就是处理程序逻辑的。   它相对于前两个不是很好理解，这里举个例子:我们要保存一个用户的信息，该用户信息中包含了姓名，性别，年龄等等。    这时候表单输入要求年龄必须是 1~100 之间的整数。姓名和性别不能为空。并且把数据填充 到模型之中。    此时除了 js 的校验之外，服务器端也应该有数据准确性的校验，那么校验就是控制器的该做 的。    当校验失败后，由控制器负责把错误页面展示给使用者。    如果校验成功，也是控制器负责把数据填充到模型，并且调用业务层实现完整的业务需求

## SpringMVC的配置

### SpringMVC.xml的配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/mvc
           http://www.springframework.org/schema/mvc/spring-mvc.xsd
           http://www.springframework.org/schema/context
           http://www.springframework.org/schema/context/spring-context.xsd">
    <!--开启注解扫描-->
    <context:component-scan base-package="com.Controller"/>
    <!--视图解析器对象-->
    <bean id="internalResourceViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/"/>//前缀
        <property name="suffix" value=".jsp"/>//扩展名
    </bean>
    <!--开启注解-->
    <mvc:annotation-driven/>
</beans>
```

### web.xml的配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <servlet>
        <servlet-name>dispatcher</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:/com/Resourse/myspringmvc.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>dispatcher</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```

## SpringMVC参数传递

### 一般参数传递

**前端页面的参数要和传递的参数名一致**

**JSP**

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
    <title>Demo</title>
  </head>
  <body>
        <a href="/hello?username=user&password=1234">点击跳转</a>
  </body>
</html>
```

**Controller**

```java
package com.Controller;

import com.Bean.User;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class HelloController {

    @RequestMapping(path = "/hello")
    public String hello(String username,String password){
        System.out.println("Hello SpringMVC");
        System.out.println(username + "    " + password);
        return "success";
    }
}

```

### 实体参数传递

**前端页面的name必须要和创建的实体中的成员变量名一致**

**JSP**

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
    <title>Demo</title>
  </head>
  <body>
    <form action="/login" method="post">
      用户名:<input type="text" name="username">
      密码:<input type="password" name="password">
      <button type="submit">提交</button>
    </form>
  </body>
</html>
```

**User实体**

```java
package com.Bean;

import java.io.Serializable;

public class User implements Serializable {
    private String usernama;
    private String password;

    public String getUsernama() {
        return usernama;
    }

    public void setUsernama(String usernamae) {
        this.usernama = usernamae;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    @Override
    public String toString() {
        return "User{" +
                "usernamae='" + usernama + '\'' +
                ", password='" + password + '\'' +
                '}';
    }
}

```

**Controller**

```java
package com.Controller;

import com.Bean.User;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class HelloController {
    @RequestMapping(path = "/login")
    public String Login(User u){
        System.out.println(u.toString());
        return "success";
    }
}

```

