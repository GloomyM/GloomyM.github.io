---
title: String与StringBuffer类
date: 2020-04-25 14:35:38
tags: Java
categories: 
  - 学习历程
  - Java
---

### String类的几种构造方法

```java
package com.String类;

public class Demo {
    public static void main(String[] args) {
        /*
        空的构造方法
         */
        String s1 = new String();
        s1 = "abc";
        System.out.println("s1 = " + s1);
        byte[] bt = {100,99,98,97};
        /*
        将数字转换为对应的ASCII码
         */
        String s2 = new String(bt);
        System.out.println("s2 = " + s2);
        /*
        截取下标从0开始到3结束（0，1，2）的ASCII码
         */
        String s3 = new String(bt,0,3);
        System.out.println("s3 = " + s3);
        char[] ch = {'a','b','c'};
        /*
        将字符数组转换为字符串
         */
        String s4 = new String(ch);
        System.out.println("s4 = " + s4);
        /*
        将字符数组的部分转换为字符串（截取从0开始到2结束(0,1)）
         */
        String s5 = new String(ch,0,2);
        System.out.println("s5 = " + s5);
        System.out.println("s5的长度为" + s5.length());
    }
}

```

### String类的判断功能

- boolean equals(Object obj):比较字符串的内容是否相同,区分大小写
- boolean equalsIgnoreCase(String str):比较字符串的内容是否相同,忽略大小写
- boolean contains(String str):判断大字符串中是否包含小字符串
- boolean startsWith(String str):判断字符串是否以某个指定的字符串开头
- boolean endsWith(String str):判断字符串是否以某个指定的字符串结尾
- boolean isEmpty():判断字符串是否为空。

```java
package com.String类;

public class Demo02 {
    public static void main(String[] args) {
        String s1 = "abc";
        String s2 = "Abc";
        /**
         *判断是否相等（区分大小写）
         */
        System.out.println("equals:" + s1.equals(s2));
        /**
         *判断是否相等（不区分大小写）
         */
        System.out.println("equals:" + s1.equalsIgnoreCase(s2));
        /**
         *判断字符串中是否包含子串
         */
        System.out.println("equals:" + s1.contains("ab"));
        /**
         * 判断字符串是否以某固定字符串开头
         */
        System.out.println("equals:" + s1.startsWith("ab"));
        /**
         * 判断字符串是否以某固定字符串结尾
         */
        System.out.println("equals:" + s1.endsWith("bc"));
        /**
         * 判断字符串是否为空
         */
        System.out.println("isempty:" + s1.isEmpty());

    }
}

```

### String类型的获取功能

-   char charAt(int index):获取指定索引位置的字符
-   int indexOf(int ch):返回指定字符在此字符串中第一次出现处的索引
-   int indexOf(String str):返回指定字符串在此字符串中第一次出现处的索引
-   int indexOf(int ch,int fromIndex):返回指定字符在此字符串中从指定位置后第一次出现处的索引。
-   int indexOf(String str,int fromIndex):返回指定字符串在此字符串中从指定位置后第一次出现处的索引。
-   String substring(int start):从指定位置开始截取字符串,默认到末尾。
-   String substring(int start,int end):从指定位置开始到指定位置结束截取字符串。

```java
package com.String类;

public class Demo03 {
    public static void main(String[] args) {
        String s1 = "abcdea";
        /**
         * charAt(index)根据下标取元素
         */
        System.out.println(s1.charAt(1));
        /**
         * 返回指定字符在字符串中第一次出现的位置(找不到返回-1)
         */
        System.out.println(s1.indexOf(100));//100对应的ASCII为d
        /**
         * 返回指定字符串在原字符串中第一次出现的位置（找不到返回-1）
         */
        System.out.println(s1.indexOf("abc"));
        /**
         * 返回指定字符在此字符串中从指定位置后第一次出现处的索引
         */
        System.out.println(s1.indexOf(97,1));//从下标为1的字符之后寻找字符a
        /**
         * 返回指定字符串在原字符串中从指定位置后第一次出现处的索引
         */
        System.out.println(s1.indexOf("ea",1));//从下标为1的字符之后寻找字符串ea
        /**
         * 指定位置开始截取字符串的子串（默认到字符串最后）
         */
        System.out.println(s1.substring(3));
    }
}

```

### String类型的转换功能

-   byte[] getBytes():把字符串转换为字节数组。
-   char[] toCharArray():把字符串转换为字符数组。
-   static String valueOf(char[] chs):把字符数组转成字符串。
-   static String valueOf(int i):把int类型的数据转成字符串。
-   String toLowerCase():把字符串转成小写。
-   String toUpperCase():把字符串转成大写。
-   String concat(String str):把字符串拼接。

```java
package com.String类;

import java.lang.reflect.Array;
import java.util.Arrays;

public class Demo04 {
    public static void main(String[] args) {
        String s1 = "abcd";
        byte[] bt = new byte[s1.length()];
        char[] ch = new char[s1.length()];
        bt = s1.getBytes();//将字符串转换为byte类型
        System.out.println(Arrays.toString(bt));
        ch = s1.toCharArray();//将字符串转换为字符数组
        System.out.println(Arrays.toString(ch));
        char[] ch2 = {'a','b','c'};
        String val = String.valueOf(ch2);//将字符数组转换为字符串（与上面的其中一个构造方法类似）
        System.out.println(val);
        String val2 = String.valueOf(97);//将int类型的数据转换为字符串
        System.out.println(val2);
        String val3 = s1.toUpperCase();//将字符串转换为全大写
        System.out.println(val3);
        String val4 = val3.toLowerCase();//将字符串转换为全小写
        System.out.println(val4);
        String val5 = val4.concat(val3); //字符串拼接
        System.out.println(val5);
    }
}

```

### String类型的替换功能

- String replace(char old,char new):把字符串中的某个字符用新的字符所替换
- String replace(String old,String new)把字符串中的某个字符串用新的来替换
- String trim() 去除字符串两空格

```java
package com.String类;

public class Demo05 {
    public static void main(String[] args) {
        String s1 = "  aabbcce  ";
        String val = s1.replace("c","f");//将字符串中的某个字符用新字符替换(字符串一样)
        System.out.println(val);
        System.out.println(s1);
        System.out.println(s1.trim()); //去除字符串两端的空格
    }
}
```

### 大小写字母计数实例

```java
package com.String类;

import java.util.Scanner;

public class Demo06 {
    public static void main(String[] args) {
        String s;
        Scanner sc = new Scanner(System.in);
        s = sc.next();
        int bignum = 0 , smallnum = 0,num = 0;
        for(int i = 0 ; i < s.length() ; i++){
            char ch = s.charAt(i);
            if(ch >= 'A' && ch <= 'Z')
                bignum++;
            else if(ch >= 'a' && ch <= 'z')
                smallnum++;
            else
                num++;
        }
        System.out.println("大写字母有" + bignum + "个");
        System.out.println("小写字母有" + smallnum + "个");
        System.out.println("整数有" + num + "个");
    }
}

```

### 首字母大写实例

```java
package com.String类;

import java.util.Scanner;

public class Demo07 {
    public static void main(String[] args) {
        String s;
        Scanner sc = new Scanner(System.in);
        s = sc.next();
        s = s.substring(0,1).toUpperCase() + s.substring(1);
        System.out.println("首字母大写"+s);
    }
}
```

### 子串查找计数实例

```java
package com.String类;

public class Demo08 {
    public static void main(String[] args) {
        String tpl = "woaijavawoaijavawoaijava";
        System.out.println("子串的数目为" + getcount(tpl,"java"));
    }
    public static int getcount(String tpl,String s){
        int i = 0,cnt = 0;
        while (tpl.indexOf("java",i) != -1){
            cnt++;
            i = tpl.indexOf("java",i) + s.length();
        }
        return cnt;
    }
}
```

### StringBuffer类

- public StringBuffer append(boolean b)

  该方法的作用是追加内容到当前StringBuffer对象的末尾

- public StringBuffer deleteCharAt(int index)

  该方法的作用是删除指定位置的字符，然后将剩余的内容形成新的字符串。

- public StringBuffer delete(int start,int end)

  该方法的作用是删除指定区间以内的所有字符，包含start，不包含end索引值的区间。

- public StringBuffer insert(int offset, boolean b),

  该方法的作用是在StringBuffer对象中插入内容，然后形成新的字符串。例如：

- public StringBuffer reverse()

  该方法的作用是将StringBuffer对象中的内容反转，然后形成新的字符串。

- public void setCharAt(int index, char ch)

  该方法的作用是修改对象中索引值为index位置的字符为新的字符ch

```java
package com.StringBuffer类;

public class Demo {
    public static void main(String[] args) {
        StringBuffer sb = new StringBuffer("abc");
        sb.append("1234").append("fpx");
        System.out.println(sb);
        sb.deleteCharAt(0);//这里是对原字符串直接操作（直接改变了原字符串的值）
        System.out.println(sb);
        sb.delete(1,3);
        System.out.println("删除区间1-3  " + sb);
        sb.insert(3,"abs"); //在第三个处插入字符串abs(append只能在字符串尾部插入，insert可以随意插入)
        System.out.println(sb);
        sb.reverse();//字符串反转
        sb.setCharAt(0,'A');//给指定位置进行赋值
        System.out.println(sb);
    }
}

```

