---
title: JavaIO流
date: 2020-05-02 14:49:37
tags: Java
categories:
  - 学习历程
  - Java
---

### 引入

程序需要实现与设备和不同介质之间的数据传输，例如：键盘录入、读取电脑文件等，Java将这种通过不同输入输出设备（键盘，显示器，网络）等之间的数据传输抽象表述为“流”

按照操作的数据不同，可以分为：

- 字节流：字节流可以操作任何数据，因为在计算机中任何数据都是以字节的形式存储的
- 字符流：字符流只能操作纯字符数据，比较方便。

按照流向分，又可以分为：

- 输入流
- 输出流

### 字节流

![](https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/JavaIO%E6%B5%81/Image_01.png)

![](https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/JavaIO%E6%B5%81/Image_02.png)

#### 字节输入流

通过FileInputStream类来实现

```java
package com.IO;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.util.Arrays;

public class Demo03 {
    public static void main(String[] args) throws IOException {
        FileInputStream fis = new FileInputStream("test.txt");
        /**
         * read方法1:
         *  count返回数据,返回-1时表示读取结束
         */
        int conut;
        while ((conut = fis.read()) != -1){
            System.out.println(conut);
        }
        /**
         * read方法2:
         *  count返回数据的个数，数据存储在bytes中，返回-1时读取结束
         */
        byte[] bytes = new byte[2];
        while ((conut = fis.read(bytes)) != -1){
            System.out.println(Arrays.toString(bytes));
        }
    }
}

```

#### 字节输出流

通过FileOutputStream类来实现

```java
package com.IO;

import java.io.FileOutputStream;
import java.nio.file.FileVisitOption;

public class Demo01 {
    public static void main(String[] args) throws Exception {
        FileOutputStream fos = new FileOutputStream("test.txt");
        fos.write(97);//写入97的Ascii码
        byte[] bytes = new byte[]{98,99,100};
        fos.write(bytes);
    }
}

```

```java

import java.io.FileOutputStream;

public class Demo02 {
    public static void main(String[] args) throws Exception {
        FileOutputStream fos = new FileOutputStream("test.txt",true);//向该文件后追加写，不加true默认为覆盖写
        fos.write(97);//写入97的Ascii码
        fos.write("\r\n".getBytes()); //换行
        fos.write(98);
    }
}

```

#### 实例：

```java
package com.IO;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.util.Scanner;

/**
 * 输入指定文件目录，并复制该文件到自身目录下
 */
public class Demo05 {
    public static void main(String[] args) throws IOException {
        File file = getfile();
        FileInputStream fis = new FileInputStream(file);
        FileOutputStream fos = new FileOutputStream(file.getName());
        int cnt = 0;
        byte[] bytes = new byte[10];
        while ((cnt = fis.read(bytes)) != -1){
            fos.write(bytes,0,cnt);
        }
        System.out.println("文件复制成功");
    }

    public static File getfile(){
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入文件名称");
        String path = sc.next();
        File file = new File(path);
        if(!file.exists()){
            System.out.println("该文件目录不存在");
        }else if(file.isDirectory()){
            System.out.println("这不是文件");
        }
        else
            return file;
        return null;
    }
}

```

### 字符流

![](https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/JavaIO%E6%B5%81/Image_03.png)

![](https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/JavaIO%E6%B5%81/Image_04.png)

#### 字符输入流

FileWriter类实现字符流输入

```java
package com.IO;

import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

public class Demo08{
    public static void main(String[] args) throws IOException {
        FileWriter wt = new FileWriter("text.txt");
        char[] ch = new char[]{'你','好'};
        wt.write(ch);
        wt.flush();
        wt.close();
    }
}

```

#### 字符输出流

通过FileReader类实现字符流输出

```java
package com.IO;

import java.io.FileReader;
import java.io.IOException;

public class Demo09 {
    public static void main(String[] args) throws IOException {
        FileReader reader = new FileReader("text.txt");
        int count = 0;
        while ((count = reader.read()) != -1){
            System.out.println((char) count);
        }
        reader.close();
    }
}
```

### 缓冲流

#### 字节缓冲输入流

通过BufferedInputStream实现

```java
package com.IO;

import java.io.BufferedInputStream;
import java.io.FileInputStream;
import java.io.IOException;
import java.lang.reflect.Array;
import java.util.Arrays;

public class Demo10 {
    public static void main(String[] args) throws IOException {
        BufferedInputStream bis = new BufferedInputStream(new FileInputStream("text.txt"));
        byte[] bytes = new byte[1024];
        int count = bis.read(bytes);
        String st = new String(bytes,0,count);
        System.out.println(st);
    }
}

```

#### 字节缓冲输出流

通过BufferedOutputStream实现

```java
package com.IO;

import java.io.*;
import java.lang.reflect.Array;
import java.util.Arrays;

public class Demo10 {
    public static void main(String[] args) throws IOException {
        BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("text.txt"));
        bos.write("你好呀".getBytes());
        bos.close();
    }
}

```

#### 字符缓冲输入流

通过BufferedReader来实现

```java
package com.IO;

import java.io.BufferedInputStream;
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class Demo11 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new FileReader("text.txt"));
        String line = null;
        while ((line = br.readLine()) != null){ //readLine()方法读取一行元素，当为null时读取完成
            System.out.println(line);
        }
    }
}

```

#### 字符缓冲输出流

通过BufferedWriter来实现

```java
package com.IO;

import java.io.*;

public class Demo11 {
    public static void main(String[] args) throws IOException {
        BufferedWriter bw = new BufferedWriter(new FileWriter("text.txt",true));
        char[] ch = new char[]{'你','好','呀'};
        bw.write(ch);
        bw.flush();
        bw.close();
    }
}

```

### 序列化流

```java
package com.IO;

import java.io.*;

public class Demo12 {
    public static void main(String[] args) throws IOException {
        Student s = new Student("A",21);
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("st.txt"));
        oos.writeObject(s);
    }
}

class Student implements Serializable {
    String name;
    int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

```

### 反序列化流

```java
package com.IO;

import java.io.FileInputStream;
import java.io.IOException;
import java.io.ObjectInputStream;

public class Demo13 {
    public static void main(String[] args) throws Exception {
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream("st.txt"));
        Object o = ois.readObject();
        System.out.println(o);
    }
}

```

### 打印流

```java
package com.IO;

import java.io.File;
import java.io.PrintStream;

public class Demo14 {
    public static void main(String[] args) throws Exception{
        File file = new File("1.txt");
        PrintStream ps = new PrintStream(file);
        for(int i = 0 ; i < 10 ; i++){
            ps.println(i);
        }
        System.out.println("打印完成");
    }
}

```

### 实例

```java
package com.IO;

import java.io.*;
import java.util.ArrayList;
import java.util.Scanner;

public class 案例 {
    static ArrayList<user> userslist = new ArrayList<>();
    static Scanner sc = new Scanner(System.in);

    static{
        try {
            File file = new File("User");
            if(file.exists()){
                ObjectInputStream ois = new ObjectInputStream(new FileInputStream(file));
                userslist = (ArrayList<user>) ois.readObject();
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) throws Exception{
        while (true){
            System.out.println("请输入选项:(1)注册(2)输出所有用户信息(3)退出");
            int choice = sc.nextInt();
            switch (choice){
                case 1:
                    register();
                    break;
                case 2:
                    getinfo();
                    break;
            }

        }
    }
    static void register() throws Exception{
        System.out.println("请输入用户名:");
        String username = sc.next();
        System.out.println("请输入密码:");
        String password = sc.next();
        userslist.add(new user(username,password));
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("User"));
        oos.writeObject(userslist);
        System.out.println("注册成功");
    }
    static void getinfo(){
        for(int i = 0 ; i < userslist.size() ; i++){
            System.out.println(userslist.get(i).toString());
        }
    }
}

class user implements Serializable {
    private String username;
    private String password;

    public user(String username, String password) {
        this.username = username;
        this.password = password;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    @Override
    public String toString() {
        return "user{" +
                "username='" + username + '\'' +
                ", password='" + password + '\'' +
                '}';
    }
}

```

