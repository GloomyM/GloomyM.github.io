---
title: Java多态
date: 2020-04-23 17:54:53
tags: Java
categories: 
 - 学习历程
 - Java
---

### 简介：

**多态**是继封装、继承之后，面向对象的第三大特性。

现实事物经常会体现出多种形态，如学生，学生是人的一种，则一个具体的同学张三既是**学生**也是**人**，即出现**两种形态**。            

<!-- more -->                                         

Java作为面向对象的语言，同样可以描述一个事物的多种形态。如Student类继承了Person类，一个Student的对象便既是Student，又是Person。

Java中多态的代码体现在一个子类对象(实现类对象)既可以给这个子类(实现类对象)引用变量赋值，又可以给这个子类的父类类型变量赋值。

### 多态实例：

```java
package com.多态;

/**
 * 多态
 *  只能调用父类里的成员变量
 *  可以对父类里的方法进行重写
 *  编译看左，运行看右
 *  
 *
 * instanceof 用来判断类型
 *
 */

public class demo01 {
    public static void main(String[] args) {
        Fu f = new Zi();
        System.out.println(f.num); //这里输出的是父类的num值
        f.func1();  //这里执行的是子类的方法
        if(f instanceof Fu){
            System.out.println("我是Fu类型的");
        }
        else{
            System.out.println("我是Zi类型的");
        }
    }
}


class Fu{
    int num = 0;
    public void func1(){
        System.out.println("我是父类的func1");
    }
}


class Zi extends  Fu{
    int num = 1;
    @Override
    public void func1() {
        System.out.println("我是子类的func1"); //子类对父类的func1方法重写
    }
}
```

