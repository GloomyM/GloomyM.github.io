---
title: Object类
date: 2020-04-25 14:07:24
tags: Java
categories: 
  - 学习历程
  - Java
---

### Object类中的equals方法

```java
package com.Object;

import javax.swing.*;
import java.util.Objects;

public class Demo01 {
    public static void main(String[] args) {
        Student s1 = new Student("Li",18);
        Student s2 = new Student("Li",18);
        /**
         * equals与"=="对比：
         *  "=="是用来判断地址是否完全一致
         *  equals是用来判断值是否完全一致（可以在类中进行重写）
         */
        if(s1.equals(s2))
            System.out.println("Yes");
        else
            System.out.println("No");
        if(s1 == s2)
            System.out.println("Yes");
        else
            System.out.println("No");
        System.out.println(s1.toString());
        System.out.println(s2.toString());
    }
}


class Student{
    String name;
    int age;
    public Student(String name,int age){
        this.name = name;
        this.age = age;
    }

    /**
     * 对Object类中的equal方法重写，判断两个对象是否完全一致
     * (成员变量完全相等)
     */
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return age == student.age &&
                Objects.equals(name, student.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }

}

```



### Object类中的toString()方法

```java
package com.Object;

public class Demo02 {
    public static void main(String[] args) {
        Person p1 = new Person("小明",19);
        Person p2 = new Person("小红",22);
        System.out.println(p1.toString());
        System.out.println(p2.toString());
    }
}

class Person{
    String name;
    int age;

    public Person(String name,int age){
        this.age = age;
        this.name = name;
    }

    /**
     * 对Object类中的toString方法进行重写
     *  返回成员变量的值
     */
    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}

```

