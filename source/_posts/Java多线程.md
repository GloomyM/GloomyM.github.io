---
title: Java多线程
date: 2020-05-08 19:35:00
tags: Java
categories:
  - 学习历程
  - Java
---

### 主线程

#### Main Thread（主线程）

主线程顾名思义就是只要执行程序就会执行的线程，可以理解为Java中的Main方法

### 多线程的构造

在Java中多线程的使用Thread进行构造

```java
package com.多线程;

public class Demo01 {
    public static void main(String[] args) {
        Thread t1 = Thread.currentThread();//主线程
        System.out.println("主线程" + t1.getName());
        Thread t2 = new Thread(){
            @Override
            public void run() {
                System.out.println("子线程" + getName());
            }
        };
        t2.start();
    }
}
```

由于Java中的继承是单继承，所以为了实现更多功能，往往结合Runnable接口进行使用

```java
package com.多线程;

//使用Runnable接口可以实现数据的共享
public class Demo03 {
    public static void main(String[] args) {
        windows w = new windows();
        Thread t1 = new Thread(w);
        t1.start();
        Thread t2 = new Thread(w);
        t2.start();
        Thread t3 = new Thread(w);
        t3.start();
    }

}


class windows implements Runnable{
    private int tickets = 100;
    Object obj = new Object();
    public void run(){
        synchronized (obj){ //同步代码块解决多线程安全问题
            while (this.tickets != 0) {
                try {
                    Thread.sleep(10);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                System.out.println("卖出第" +  this.tickets-- + "张票");
            }
        }
    }
}
```

### 模拟包子铺实例

```java
package com.模拟包子铺;
//主程序
import java.io.Serializable;

public class Demo {
    public static void main(String[] args) {
        Baozi bz = new Baozi();
        SetThread st = new SetThread(bz);
        GetThread gt = new GetThread(bz);
        st.start();
        gt.start();
    }
}

```

```java
package com.模拟包子铺;
//包子类
import java.util.ArrayList;

public class Baozi {
    private ArrayList<String> baozi = new ArrayList<>();

    public synchronized String getBaozi() {
        if(baozi.isEmpty()){
            try {
                wait(); //该线程进入睡眠
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        String b = baozi.get(0);
        baozi.remove(0);
        return b;

    }

    public synchronized void setBaozi() {
        try {
            Thread.sleep(100); //制作包子需要时间，设置0.5秒睡眠
        }catch (Exception e){
            e.printStackTrace();
        }
        this.baozi.add("a");
        notifyAll();//唤醒睡眠的线程
    }
}

```

```java
package com.模拟包子铺;
//买包子线程
public class GetThread extends Thread{

    private Baozi bz;

    public GetThread(Baozi bz) {
        this.bz = bz;
    }

    @Override
    public synchronized void run() {
        while (true){
            System.out.println("我买了包子" + bz.getBaozi());
        }
    }
}

```

```java
package com.模拟包子铺;

import java.util.ArrayList;

//做包子

public class SetThread extends Thread{

    private Baozi bz;


    public SetThread(Baozi bz) {
        this.bz = bz;
    }

    @Override
    public void run() {
        while (true){
            bz.setBaozi();
        }
    }
}

```

