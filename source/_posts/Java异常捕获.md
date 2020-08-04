---
title: Java异常捕获
date: 2020-04-30 14:39:41
tags: Java
categories:
  - 学习历程
  - Java
---

### 引入

Java程序在运行过程中出现的错误，这种错误情况，称为异常，这时就必须使用异常处理机制来编写代码

### throw抛出异常

```java
package com.异常;

public class Demo02 {
    public static void main(String[] args) {
        Stu s = new Stu();
        s.setAge(-12);
        System.out.println("程序结束");//出现异常不执行
    }
}

class Stu{
    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        if(age < 0 || age >= 120){
            AgeExcpetino ae = new AgeExcpetino("年龄不合法");
            throw ae;//抛出异常
        }
        this.age = age;
    }
}

/**
 *自定义异常
 */

class AgeExcpetino extends RuntimeException{
    public AgeExcpetino(String message) {
        super(message);
    }
}
```

### try_catch_finally异常捕获

利用try_catch_finally捕获异常，try中的语句块为运行的代码块，catch为捕获的具体异常，finally中的语句块，无论是否出现异常都要执行

```java
package com.异常;

public class Demo02 {
    public static void main(String[] args) {
        Stu s = new Stu();
        try {
            s.setAge(-12);
        } catch (AgeExcpetino e) {
            e.printStackTrace();//throwable中的常用方法，输出异常原因
        } finally {
            System.out.println("无论是否出现异常都要执行我");
        }

    }
}

class Stu{
    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        if(age < 0 || age >= 120){
            AgeExcpetino ae = new AgeExcpetino("年龄不合法");
            throw ae;
        }
        this.age = age;
    }
}


class AgeExcpetino extends RuntimeException{
    public AgeExcpetino(String message) {
        super(message);
    }
}
```

