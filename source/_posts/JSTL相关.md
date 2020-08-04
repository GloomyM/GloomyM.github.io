---
title: EL表达式与JSTL
date: 2020-06-06 14:13:08
tags: Java
categories:
  - 学习历程
  - Java
---

## EL

### EL概述

在 JSP 开发中，为了获取 Servlet 域对象中存储的数据，经常需要书写很多 Java 代码， 这样的做法会使 SP 页面混乱，难以维护，为此，在 JSP2.0 规范中提供了 EL 表达式。EL 是 Expression Language 的缩写，它是一种简单的数据访问语言。

<!-- more -->

### EL的使用方式

EL表达式的规范是`${}`，再{}中填写内容，例如在JSP文件中，`${name}`，表示取到名字为name的变量

#### 点运算符（.）

EL 表达式中的点运算符，用于问 JSP 页面中某些对象的属性

`${user.name }` 表示访问 user 对象中的 name 属性 （要求符合JavaBean规范）

#### 方括号运算符（[]）

EL 表达式中的方括号运算符与点运算符的功能相同，都用于访问 JSP 页面中某些对象的属性，当获取的属性名中包含一些特殊符号，如“-”或“?”等并非字母或数字的符号，就 只能使用方括号运算符来访问该属性，其语法格式如下` ${user["My-name"]} `访问 user 对象中的 My-name 属性，当需要访问列表中的元素时也需要使用方括号进行访问，例如​`${list[1]}`表示访问列表list的第二个元素

## JSTL

### JSTL概述

从 JSP11 规范开始，JSP 就支持使用自定义标签，使用自定义标签大大降低了 JSP 页面的 复杂度，同时增强了代码的重用性。为此，许多 Web 应用厂商都定制了自身应用的标签库， 然而同一功能的标签由不同的 Web 应用厂商制定可能是不同的，这就导致市面上出现了很 多功能相同的标签，令网页制作者无从选择，为了解决这个问题，Sun 公司制定了一套标准 标签库（ JavaServer Pages Standard Tag Library），简称 JSTL STL 虽然被称为标准标签库，而实际上这个标签库是由 5 个不同功能的标签库共同组成的。 在 JSTL 1.1 规范中，为这 5 个标签库分别指定了不同的 UR 以及建议使用的前缀，如下所示

| 标签库     | 标签库的 URI                         | 前缀  |
| ---------- | ------------------------------------ | ----- |
| Core       | http://java.sun.com/jsp/jstl/core    | c     |
| I18N       | http://java.sun.com/jsp/jstl/fmt     | fmt   |
| SQL        | http://java.sun.com/jsp/jstl/sql     | sql   |
| XML        | http://java.sun.com/jsp/jstl/xml     | x     |
| Function s | http://java.sun.com/jsp/jstl/functio | ns fn |

### JSTL所需Jar包

- jstl-1.2.jar
- standard-1.1.2.jar

### JSTL导入标签库

<%@taglib uri="标签库的URI" prefix="标签库的前缀"%> 

例如使用Core标签库：<%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%> 

### JSTL 中的 Core 核心标签库 

#### <c:set>标签

不常用

#### <c:if>标签

```jsp
<%--
  Created by IntelliJ IDEA.
  Date: 2020/6/6
  Time: 8:26
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <c:if test="${3<4}">3小于4</c:if>

</body>
</html>

```

#### <c:choose>标签

```jsp
<%--
  Created by IntelliJ IDEA.
  Date: 2020/6/6
  Time: 8:31
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <c:set value="4" scope="session" var="day"></c:set>
    ${day}
    <c:choose>
        <c:when test="${day==1}">
            今天周一
        </c:when>
        <c:when test="${day==2}">
            今天周二
        </c:when>
        <c:when test="${day==3}">
            今天周三
        </c:when>
        <c:otherwise>
            无
        </c:otherwise>
    </c:choose>
</body>
</html>

```

#### <c:forEach>标签

​	items：类型

​	begin：开始的索引（默认为0）

​	end：结束的索引

​	step：步长

​	var：将变量存入var

```jsp
<%@ page import="java.util.ArrayList" %><%--
  Created by IntelliJ IDEA.
  User: 李之辰
  Date: 2020/6/6
  Time: 8:41
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <%
        ArrayList<String> list = new ArrayList<>();
        list.add("A1");
        list.add("A2");
        list.add("A3");
        request.setAttribute("list",list);
    %>
    <c:forEach begin="1" end="10" step="2" var="i">
        ${i}
    </c:forEach>
    <c:forEach items="${list}" var="v">
        ${v}
    </c:forEach>
</body>
</html>

```

**Tip:常用标签：if，choose，forEach**