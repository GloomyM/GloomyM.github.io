---
title: Java泛型
date: 2020-04-27 16:23:57
tags: Java
categories:
  - 学习历程
  - Java
---

### 泛型简介：

Java 泛型（generics）是JDK5中引入的一个新特性，泛型提供了编译时类型安全检测机制，该机制允许程序员在编译时检测到非法的类型。泛型的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数类型。

### 泛型类和泛型接口

定义泛型类在"类名"后添加一对<>，里面定义"泛型名称"

```java
package com.泛型;

public class Demo02 {
    public static void main(String[] args) {
        inter<String> inter = new inter<String>() { //匿名内部类创建
            @Override
            public void func(String num) {
                System.out.println("我是泛型接口的String类型" + num);
            }
        };
        inter.func("123");
    }
}


interface inter<T>{
    void func(T num);
}

```



### 泛型方法

定义格式：修饰符 <表示泛型方法> 返回值类型 方法名(参数){}

```java
package com.泛型;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class Demo {
    public static void main(String[] args) {
        Integer[] ints = new Integer[]{1,2,3,4};
        Double[] dbs = new Double[]{1.0,2.4,6.9,9.1};
        System.out.println(ArrayTools.getindex(2,ints));//查询目标值2在ints数组中的位置
        System.out.println(ArrayTools.getindex(6.9,dbs));//查询目标值6.9在dbs数组中的位置
    }
}

class ArrayTools{
    /**
     * 查找目标值在数组中的位置
     *  如果不使用泛型方法，那么不同数据类型要重载很多方法
     *  下面是利用泛型方法进行操作
     *
     * @param target 查找的目标值
     * @param nums 被查找的数组
     * @param <T>
     * @return  返回下标
     */
    public static <T> int getindex(T target, T[] nums){
        int index = -1;
        for(int i = 0 ; i < nums.length ; i++){
            if(nums[i].equals(target)){
                index = i;
                break;
            }
        }
        return index;
    }
}
```