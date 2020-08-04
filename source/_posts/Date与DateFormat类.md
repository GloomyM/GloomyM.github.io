---
title: Date与DateFormat类
date: 2020-04-26 14:33:56
tags: Java
categories:
  - 学习历程
  - Java
---

### 获取时间

```java
package com.Date类;

import java.text.DateFormat;
import java.util.Date;

public class Demo {
    public static void main(String[] args) {
        Date date = new Date();
        System.out.println(date);
        System.out.println(date.toLocaleString());//已过时
        /**
         * 由于toLocaleString()方法已经过时
         * 利用DateFormt进行替代
         */
        DateFormat dateTimeInstance = DateFormat.getDateTimeInstance();
        System.out.println(dateTimeInstance.format(date));//返回日期+时间
        DateFormat timeInstance = DateFormat.getTimeInstance();
        System.out.println(timeInstance.format(date)); //返回时间
        DateFormat dateInstance = DateFormat.getDateInstance();
        System.out.println(dateInstance.format(date)); // 返回日期
    }
}

```

### 时间格式化与解析

```java
package com.Date类;

import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class Demo02 {
    public static void main(String[] args) throws ParseException {
        Date date = new Date();
        /**
         * 以年月日输出时间
         *  使用DateFormat的子类SimpleDateFormat进行格式化
         *  yyyy:年 MM:月 DD:日 HH:小时 mm:分钟 ss:秒
         */
        DateFormat df = new SimpleDateFormat("yyyy年MM月DD日HH:mm:ss");
        String tm = df.format(date);
        System.out.println(tm);
        /**
         * 解析时间
         *  使用DateFormat的子类SimpleDateFormat进行格式化
         *  parse()方法进行解析，返回一个Date
         */
        String s = "2020年4月26日";
        DateFormat df2 = new SimpleDateFormat("yyyy年MM月dd日");
        Date date2 = df2.parse(s);
        System.out.println(date2);
    }
}

```

