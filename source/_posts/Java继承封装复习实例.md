---
title: Java继承封装复习实例
date: 2020-04-23 15:01:35
tags: Java
categories: 
  - 学习历程
  - Java

---

### 继承，封装，this，super关键字，构造方法的使用实例

```java
package com.Test01;

/**
 * 继承，封装，this，super关键字，构造方法的使用
 * @author Li
 * @version demo01
 *
 */

public class demo01 {
    public static void main(String[] args) {
        System.out.println("我是com.Test01下的demo01类");
        student st = new student("li",20);
        System.out.println(st.getName() + " " + st.getAge());
        st.study();
        teacher tc = new teacher("Wang",33);
        System.out.println(tc.getName() + " " + tc.getAge());
        tc.teach();
    }
}


class Person{
    private String name;
    private int age;
    /**
     * @param name 姓名
     * @param age 年龄
     */
    public Person(String name, int age){
        this.name = name;
        this.age = age;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}

class student extends Person{
    /**
     * @param name 姓名
     * @param age  年龄
     */
    public student(String name,int age){
        super(name,age);
    }
    public void study(){
        System.out.println("我要学习");
    }
}

class  teacher extends Person{
    /**
     *
     * @param name 姓名
     * @param age 年龄
     */
    public teacher(String name,int age){
        super(name,age);
    }

    public void teach(){
        System.out.println("我要授课");
    }
}

```

