---
title: JavaFile类
date: 2020-04-30 16:25:03
tags: Java
categories:
  - 学习历程
  - Java
---

### 引入

Java中操作一个文件或者目录，可以使用File类对象，它可以代表磁盘上的一个文件，或者目录（文件夹）的信息（文件或者目录可以不存在）

<!-- more -->

### File类的方法

#### File构造方法

![](https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/JavaFile%E7%B1%BB/Image_01.png)

#### File创建删除文件

![](https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/JavaFile%E7%B1%BB/Image_02.png)

```java
package com.File类;

import java.io.File;
import java.io.IOException;

/**
 * file.createNewFile():创建文件
 * file.mkdir():创建单一文件夹
 * file.mkdir3():创建多级文件夹
 * file.delete():删除文件/文件夹
 */

public class Demo01 {
    public static void main(String[] args) throws IOException {
        File file = new File("Test.txt");
        System.out.println("创建文件:" + file.createNewFile());
        File file2 = new File("Demo");
        System.out.println("创建文件夹:" + file2.mkdir());
        File file3 = new File("A1//A2");
        System.out.println("创建多级文件夹:" + file3.mkdirs());
        System.out.println("删除文件" + file.delete());
        System.out.println("删除文件夹" + file2.delete());
        System.out.println("删除多级文件夹" + file3.delete());
    }
}

```

#### File文件重命名

```java
package com.File类;

import java.io.File;
import java.io.IOException;

/**
 * f1.renameTo(f2)
 *  f1,f2都为File对象
 *  如果和原文件不在同目录下，重命名操作将会相当于"剪切"操作
 *  如果和原文件在同目录下，相当于"重命名"
 */


public class Demo02 {
    public static void main(String[] args) throws IOException {
        File file = new File("2.doc");
        File file2 = new File("A1//1.doc");
        file.renameTo(file2);//将2.doc剪贴到A1文件夹并改名为1.doc,如果直接写1.doc相当于将2.doc改名为1.doc
    }
}

```

#### File判断文件

![](https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/JavaFile%E7%B1%BB/Image_03.png)

```java
package com.File类;

import java.io.File;
import java.io.IOException;

public class Demo03 {
    public static void main(String[] args) throws IOException {
        File file = new File("A1//1.doc");
        System.out.println("是否为文件夹" + file.isDirectory());
        System.out.println("是否为文件" + file.isFile());
        System.out.println("是否存在" + file.exists());
        System.out.println("是否可读" + file.canRead());
        System.out.println("是否可写" + file.canWrite());
        System.out.println("是否为隐藏文件" + file.isHidden());
    }
}

```

#### File单一获取功能

![](https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/JavaFile%E7%B1%BB/Image_04.png)

```java
package com.File类;

import java.io.File;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class Demo04 {
    public static void main(String[] args) throws IOException {
        File file = new File("A1//1.doc");
        System.out.println("获取文件名" + file.getName());
        System.out.println("获取文件路径" + file.getPath());
        System.out.println("获取文件抽象路径" + file.getAbsolutePath());
        System.out.println("获取文件大小" + file.length() + "字节");
        /**
         * 复习:
         *  SimpleDateFormat格式化时间
         */
        Date date = new Date(file.lastModified());
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        System.out.println("获取文件最后一次修改时间" + sdf.format(date));
    }
}

```

#### File批量获取功能

![](https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/JavaFile%E7%B1%BB/Image_05.png)

```java
package com.File类;

import java.io.File;

public class Demo05 {
    public static void main(String[] args) {
        File file = new File("A1");
        /**
         * 返回文件名字符串
         */
        String[] s = file.list();
        for(String ss :s){
            System.out.println(ss);
        }
        /**
         * 返回File对象包含文件的抽象路径名
         */
        File[] fl = file.listFiles();
        for(File f:fl){
            System.out.println(f);
        }
    }
}

```

#### FileFilter文件过滤器

```java
package com.File类;

import java.io.File;
import java.io.FileFilter;

public class Demo06 {
    public static void main(String[] args) {
        File file = new File("A1");
        FileFilter filter = new FileFilter() {
            @Override
            public boolean accept(File pathname) {
                return pathname.isFile();//过滤非文件夹的文件
            }
        };
        File[] fl = file.listFiles(filter);
        for (File file1 : fl) {
            System.out.println(file1.getAbsolutePath());
        }
    }
}

```

### FilenameFilter文件名过滤器

```java
package com.File类;

import java.io.File;
import java.io.FilenameFilter;

public class Demo07 {
    public static void main(String[] args) {
        File file = new File("A1");
        FilenameFilter filter = new FilenameFilter() {
            @Override
            public boolean accept(File dir, String name) {
                return name.endsWith(".doc"); //过滤后缀名为.doc的文件
            }
        };
        File[] fl = file.listFiles(filter);
        for (File file1 : fl) {
            System.out.println(file1.getAbsolutePath());
        }
    }
}

```

### 实例：

查找指定目录下指定后缀名的文件

```java
package com.File类;

import java.io.File;
import java.io.FilenameFilter;
import java.io.IOException;
//查找A1目录下所有文件夹中后缀名为.txt的文件（递归）
public class Demo09 {
    public static void main(String[] args) throws IOException {
        File file = new File("A1");
        getfile(file,".txt");
    }
    public static void getfile(File file,String s2){
        File[] fl = file.listFiles();
        if(fl != null) {
            for (File file1 : fl) {
                if (file1.isFile() && file1.getName().endsWith(s2)) {
                    System.out.println(file1.getAbsolutePath());
                } else if (file1.isDirectory()) {
                    getfile(file1, s2);
                }
            }
        }
    }
}


```

