---
title: Arrays工具类
date: 2020-04-26 13:09:00
tags: Java
categories: 
  - 学习历程
  - Java
---

### 常用方法：

- 获取集合：Arrays.asList()
- 数组排序：Arrays.sort()
- 二分查找：Arrays.binarySearch()

### 实例：

```java
package com.Array;

import java.lang.reflect.Array;
import java.util.Arrays;
import java.util.Comparator;
import java.util.List;

public class Demo {
    public static void main(String[] args) {
        List<String> ls = Arrays.asList("1","2","3","4"); //生成集合
        System.out.println(ls);
        Integer[] a = new Integer[]{1,3,2,10,4};
        /**
         * Arrays.sort()排序方法
         * 这里利用匿名内部类重写Comparator接口中的compare方法
         */
        Arrays.sort(a,new Comparator<Integer>(){
            @Override
            public int compare(Integer o1, Integer o2) {
                return o1 - o2;
            }
        });
        System.out.println(Arrays.toString(a));
        int index = Arrays.binarySearch(a,0,3,2);//二分查找，返回下标，如果fromindex和toindex不写，默认从头到尾
        System.out.println(index);
    }
}
```

