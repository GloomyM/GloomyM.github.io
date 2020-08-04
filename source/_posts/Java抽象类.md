---
title: Java抽象类
date: 2020-04-23 20:50:58
tags: Java
categories:
  - 学习历程
  - Java
---

### 抽象（abstract）语法：

- 抽象方法：public abstract void 方法名(参数);
- 抽象类：abstract class 类名{}

### 注意事项：

- 一个类中有抽象方法，该类必须为抽象类
- 如果一个类继承了抽象类，那么必须实现改抽象类中的抽象方法
- 抽象类不可直接创建对象

### 关键字abstract不能和哪些关键字共存？

(1)   private：私有的方法子类是无法继承到的，也不存在覆盖，而abstract和private一起使用修饰方法，abstract既要子类去实现这个方法，而private修饰子类根本无法得到父类这个方法。互相矛盾。

(2)   final，同上final修饰的类无法被继承，无法被重写，互相矛盾

(3)   static、static修饰的方法是类方法（优先于对象存在），互相矛盾

### 什么时候用抽象类？

对于一般继承来说，子类一定是属于父类的，但这种属于相对来说是一种较大的分支，比如老师或学生是人类的子类，而抽象类往往是较小的分支，例如：语文老师，数学老师，英语老师都可以是老师的子类。这样似乎就好理解了一些，普通的继承是较大层面的分支，而抽象类的继承是较小层面的分支

### 抽象类实例：

```java
package com.抽象类;

public class Demo01 {
    public static void main(String[] args) {
        Teacher t1 = new CTeacher();
        Teacher t2 = new MTeacher();
        t1.work();
        t2.work();
    }
}


class Person{

}


abstract class Teacher extends Person{
    public abstract void work();
}

class CTeacher extends Teacher{
    @Override
    public void work(){
        System.out.println("我是语文老师");
    }
}

class MTeacher extends Teacher{
    @Override
    public void work() {
        System.out.println("我是数学老师");
    }
}
```

