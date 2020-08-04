---
title: BigInteger处理大数
date: 2020-04-26 21:36:15
tags: Java
categories:
  - 学习历程
  - Java
---

### 背景：

在一些特殊的场景下，我们做整数运算时，或许会碰到两个整数相加超出了int类型，或者这两个整数本身就超出了int类型，在做算法题时很容易碰到，除了自己手写大整数，在Java中，提供了BigInteger类用来处理类似问题，以及BigDecimal类处理精度损失的问题

### BigInteger：

-   public BigInteger add(BigInteger val)  加
-   public BigInteger subtract(BigInteger val) 减
-   public BigInteger multiply(BigInteger val) 乘
-   public BigInteger divide(BigInteger val)  除

```java
package com.Date类;


import java.math.BigDecimal;
import java.math.BigInteger;
import java.util.Arrays;

public class Demo03 {
    public static void main(String[] args) {
        BigInteger a1 = new BigInteger("12649879848979951897444444445");
        BigInteger a2 = new BigInteger("1555555555549788979878911245");
        BigInteger num1 = a1.add(a2);//加法
        BigInteger[] num2 = a1.divideAndRemainder(a2);//取整+取余
        BigInteger num3 = a1.subtract(a2); //减法
        BigInteger num4 = a1.divide(a2);//除法
        BigInteger num5 = a1.multiply(a2);//乘法
    }
}

```

### BigDecimal

方法与BigInteger一致不多介绍