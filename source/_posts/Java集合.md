---
title: Java集合
date: 2020-04-27 10:16:46
tags: Java
categories:
  - 学习历程
  - Java
---

### 引入

在我们使用某个类时，假如我们需要生成三个对象，那么可以新建一个长度为3的数组进行建立对象，但是如果我们需要生成不定量的对象，这时如果生成的对象数量超过了数组的长度，那么该对象就无法被创建，因此，Java引入了集合类型进行操作且集合中只能使用类类型。

<!-- more -->

### Collection接口

#### 集合普通方法

![](https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Java%E9%9B%86%E5%90%88%E7%B1%BB/Image_01.png)

```java
package com.集合;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collection;

public class Demo {
    public static void main(String[] args) {
        Collection list = new ArrayList();//接口多态;
        list.add("1");
        list.add("2");
        System.out.println(list.isEmpty());//false:因为里面已经存入了一个对象
        System.out.println(list.size());//2:返回的时集合元素的个数
        list.remove("1");//清除元素1
        System.out.println(list.contains("2"));//true:判断元素2是否在集合中
        list.clear();//清空操作
        System.out.println(list.size());//0:集合内元素已经被清空
    }
}

```

#### 集合批量操作方法

![](https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Java%E9%9B%86%E5%90%88%E7%B1%BB/Image_02.png)

```java
package com.集合;

import java.util.ArrayList;
import java.util.Collection;

public class Demo02 {
    public static void main(String[] args) {
        /**
         * 实现Collection接口
         *  实现该接口下的List接口
         *    实现该接口下的ArrayList()类
         */
        Collection list = new ArrayList();
        list.add("1");
        list.add("2");
        list.add("3");
        Collection list2 = new ArrayList();
        list2.add("a");
        list2.add("b");
        list2.add("c");
        list.addAll(list2); //将list2中的所有元素添加到list中,add是添加一个元素，addAll是添加一组元素
        System.out.println(list);
        //判断list中是否包含list2中的所有元素，contain是判断是否包含一个元素，containsAll是判断是否包含一组元素
        System.out.println(list.containsAll(list2));
        list.retainAll(list2); //取交集

    }
}
//Tip:可以通过toArray()方法返回一个object类型的数组
```

### Collection遍历方式

- 将集合转换为数组进行遍历
- 利用迭代器进行遍历
- foreach增强for循环进行遍历

```java
package com.集合;

import java.util.ArrayList;
import java.util.Collection;
import java.util.Iterator;

public class Demo03 {
    public static void main(String[] args) {
        Collection list = new ArrayList();
        list.add(new Student("li",19));
        list.add(new Student("zi",22));
        System.out.println(list);
        /**
         * 方法1；
         *  将集合转换为数组(toArray()方法)
         */
        Object[] ob = list.toArray();
        for(int i = 0 ; i < ob.length ; i++){
            System.out.println(ob[i]);
        }
        /**
         * 方法2：
         *  利用迭代器
         */
        Iterator it = list.iterator();
        while (it.hasNext()){//判断是否还存在下个值
            System.out.println(it.next());
        }
        /**
         * 方法3:
         *  foreach循环
         */
        for (Object o : list) {
            System.out.println(o);
        }
    }
}


class Student{
    String name;
    int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

### List接口

#### 方法

![](https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Java%E9%9B%86%E5%90%88%E7%B1%BB/Image_03.png)

```java
package com.集合;

import java.util.ArrayList;
import java.util.List;

public class Demo04 {
    public static void main(String[] args) {
        List ls = new ArrayList();
        ls.add(new Student("A",18));//第0个位置
        ls.add(new Student("B",20));//第1个位置
        ls.add(0,new Student("C",20));//插入到第0个位置
        System.out.println(ls);
        Object o = ls.get(1);//返回下标为1的元素
        System.out.println(o);
        ls.set(1,new Student("F",23)); //将第一个位置的值设置为F,23
        System.out.println(ls);
        ls.remove(0);//删除下标为0的元素
        System.out.println(ls);
    }
}


class Student{
    String name;
    int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}

```

### List遍历方式

```java
package com.集合;

import java.util.ArrayList;
import java.util.List;

public class Demo05 {
    public static void main(String[] args) {
        List ls = new ArrayList();
        ls.add(0);
        ls.add(1);
        ls.add(2);
        /**
         * 方法1：
         * 普通for循环+get()方法进行遍历(比Collection方便)
         */
        for(int i = 0 ; i < ls.size() ; i++){
            System.out.println(ls.get(i));
        }
        /**
         * 方法2：
         * foreach循环
         */
        for (Object o : ls) {
            System.out.println();
        }
        /**
         * 方法3：
         * 迭代器，和Collection类似，不多介绍
         */
    }
}
```

### ArrayList实例

#### 实例1：数据去重

```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;

public class Demo {
    public static void main(String[] args) {
        ArrayList<Integer> als = new ArrayList<>();
        for(int i = 1 ; i <= 10 ; i++){
            als.add(i);
            als.add(10-i);
        }
        for(int i = 0 ; i < als.size() ; i++){
            for(int j = i + 1 ; j < als.size() ; j++){
                if(als.get(i).equals(als.get(j))){
                    als.remove(j);
                    j--;
                }
            }
        }
        System.out.println(als);
    }
}

```

#### 实例2：用户登录注册

```java
package com.集合;

import java.util.ArrayList;
import java.util.Scanner;

public class Demo06 {
    static Scanner sc = new Scanner(System.in);
    static ArrayList<User> users = new ArrayList<>();
    public static void main(String[] args) {
        while (true){
            System.out.println("请输入以下选项");
            System.out.println("(1)注册 (2)登录 (3)查询所以用户信息 (4)退出");
            int choice = sc.nextInt();
            switch (choice){
                case 1:
                    regsiter();
                    break;
                case 2:
                    Login();
                    break;
                case 3:
                    ShowInfo();
                    break;
                case 4:
                    return;
            }
        }
    }
    public static void regsiter(){
        System.out.println("请输入用户名");
        String username = sc.next();
        String regex = "[0-9a-zA-Z]{6,12}";
        if (!username.matches(regex)){
            System.out.println("用户名格式输入错误，请输入6-12位的用户名");
            return;
        }
        System.out.println("请输入密码");
        String password = sc.next();
        users.add(new User(username,password));
        System.out.println("注册成功");
    }
    public static void Login(){
        System.out.println("请输入用户名");
        String username = sc.next();
        System.out.println("请输入密码");
        String password = sc.next();
        for(int i = 0 ; i < users.size() ; i++){
            if(users.get(i).getUsername().equals(username) && users.get(i).getPassword().equals(password)){
                System.out.println("登录成功");
                return;
            }
        }
        System.out.println("登录失败");
    }
    public static void ShowInfo(){
        System.out.println(users.toString());
    }
}

class User{
    private String username;
    private String password;

    public User(String username, String password) {
        this.username = username;
        this.password = password;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getUsername() {
        return username;
    }

    public String getPassword() {
        return password;
    }

    @Override
    public String toString() {
        return "User{" +
                "username='" + username + '\'' +
                ", password='" + password + '\'' +
                '}';
    }
}

```

### ArrayList的双重遍历

#### 背景

假如我们要录入高三年级学生信息，由于不同的学生在不同的班，假如1班有A,B,C三名学生，2班有D,E,F三名学生那么我们就可以使用ArrayList进行双重遍历，外层表示不同班级，内层为学生信息

#### 实例

```java
package com.集合;

import java.security.spec.RSAOtherPrimeInfo;
import java.util.ArrayList;

public class Demo07 {
    public static void main(String[] args) {
        ArrayList<ArrayList<ST>> stu = new ArrayList<>();
        ArrayList<ST> s1 = new ArrayList<>();
        /*
        A,B在一个班
         */
        s1.add(new ST("A",18));
        s1.add(new ST("B",22));
        ArrayList<ST> s2 = new ArrayList<>();
        /*
        C,D在一个班
         */
        s2.add(new ST("C",19));
        s2.add(new ST("D",19));
        /*
        将两个班的学生信息放入stu里
         */
        stu.add(s1);
        stu.add(s2);
        System.out.println(stu);
        for(int i = 0 ; i < stu.size() ; i++){ //stu.size()为外层的大小
            for(int j = 0 ; j < stu.get(i).size() ; j++)//stu.get(i).size()表示第i层的大小
                System.out.println(stu.get(i).get(j));
        }
    }
}

class ST{
    String name;
    int age;

    public ST(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "ST{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

### Set接口

Set 具有与 Collection 完全一样的接口，只是行为上不同，Set 不保存重复的元素，而且Set接口中元素无序(若有序可以使用LinkedHashSet)。HashSet是实现Set接口的一个类，他保证了存入元素均不重复（前提是数据类型必须为Java自带的数据类型）

### HashSet自定义对象存储

- 重写equals方法
- 重写hashcode方法

```java
package com.集合;

import java.util.HashSet;

public class Demo08 {
    public static void main(String[] args) {
        HashSet<St> set = new HashSet<>();
        set.add(new St("A",12));
        set.add(new St("A",12));
        System.out.println(set);
    }
}

class St{
    String name;
    int age;

    public St(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "St{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }

    @Override
    public int hashCode() {
        return this.name.hashCode() + age;
    }

    @Override
    public boolean equals(Object obj) {
        St s = (St) obj;
        if(this.name.equals(s.name) && this.age == age)
            return true;
        return false;
    }
}
```

### TreeSet

TreeSet因为实现了Set接口，所以其集合特点是：元素不重复。TreeSet 里面存放的元素是按照元素的自然顺序（字典序）来排列的

#### TreeSet存储自定义对象

TreeSet在存储自定义的对象时，要重写Compare方法，因为TreeSet本身是有序的存储数据，对于自定义对象，它并不知道需要按照什么顺序进行存储

```java
package com.集合;

import java.util.Comparator;
import java.util.LinkedList;
import java.util.TreeSet;

/**
 * 1.有序（字典序）
 * 2.元素无重复
 * 3.在存储自定义对象时要自定义Comparator接口
 *
 * Comparator接口的返回值：
 *  >0:顺序存储（也可以理解为0不换位置）
 *  =0:覆盖存储（覆盖）
 *  <0:倒序存储（交换位置）
 */


public class Demo09 {
    public static void main(String[] args) {
        TreeSet<stu> ts = new TreeSet<>(new Comparator<stu>() {
            @Override
            public int compare(stu o1, stu o2) {
                return o1.age - o2.age == 0  ? o1.name.compareTo(o2.name) : o1.age - o2.age;//年龄不同按照从小到大排序,相同按照姓名的字典序进行排序
            }
        });
        ts.add(new stu("A",20));
        ts.add(new stu("B",22));
        ts.add(new stu("C",19));
        System.out.println(ts.toString());
    }
}

class stu{
    String name;
    int age;

    public stu(String name, int age) {
        this.name = name;
        this.age = age;
    }


    @Override
    public String toString() {
        return "stu{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }

}

```

### Map

Map接口是双列集合，它的每个元素都包含一个键对象（key）和一个值对象（value），对象之间存在一种对应关系，称为映射。

#### Map的键值对生成

```java
package com.map;

import java.util.HashMap;
import java.util.HashSet;
import java.util.Map;

public class Demo {
    public static void main(String[] args) {
        /**
         * HashMap
         *  put()方法生成对应的键值对
         *  get()方法通过键取值
         *  remove()方法通过键删除值
         */
        Map<Integer,String> mp = new HashMap<>();
        mp.put(1,"A");
        mp.put(2,"B");
        mp.put(3,"C");
        System.out.println(mp.get(1));
        mp.remove(2);
    }
}


```

#### Map的遍历

```java
package com.map;

import java.util.*;

public class Demo02 {
    public static void main(String[] args) {
        Map<Integer,String> mp = new HashMap<>();
        mp.put(1,"A");
        mp.put(2,"B");
        mp.put(3,"C");
        mp.put(4,"D");
        mp.put(5,"E");
        /**
         * 方法1:
         *  keySet()遍历键
         */
        Set<Integer> set = mp.keySet();
        /*
        foreach循环遍历
         */
        for (Integer s:set){
            System.out.println("value " + mp.get(s));
        }
        /*
        迭代器遍历
         */
        Iterator it = set.iterator();
        while (it.hasNext()){
            System.out.println("value " + mp.get(it.next()));
        }
        /**
         * 方法2:
         *  Entry接口
         *  封装了键值对
         *
         */
        Set<Map.Entry<Integer, String>> entries = mp.entrySet();
        for (Map.Entry<Integer, String> m : entries){
            System.out.println("key:" + m.getKey() + "  value:" + m.getValue());
        }
    }
}

```

### HashMap

HashMap保证生成的键唯一，他的应用与HashSet类似，在存储自定义对象时要对equals和hashcode方法进行重写，来保证生成的键唯一

#### HashMap生成自定义对象

```java
package com.map;

import java.util.HashMap;
import java.util.Map;
import java.util.Objects;
import java.util.Set;

public class Demo03 {
    public static void main(String[] args) {
        HashMap<Student,String> map = new HashMap<>();
        map.put(new Student("A",18),"221000");
        map.put(new Student("B",19),"221001");
        map.put(new Student("C",18),"221002");
        map.put(new Student("C",18),"221003");
        Set<Map.Entry<Student, String>> entries = map.entrySet();
        for (Map.Entry<Student, String> entry : entries) {
            System.out.println("学生姓名年龄:" + entry.getKey());
            System.out.println("学生学号:" + entry.getValue());
        }
    }
}

class Student{
    String name;
    int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }

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

### TreeMap

TreeMap在实现了Map的功能的基础上保证数据不重复且根据键按照字典序排序，当类型为自定义对象时要重写compare方法

#### TreeMap生成自定义对象

```java
package com.map;

import java.util.Comparator;
import java.util.TreeMap;

public class Demo05 {
    public static void main(String[] args) {
        /**
         * 匿名内部类实现接口
         *  重写compare方法
         */
        TreeMap<Stu,String> tree = new TreeMap<>(new Comparator<Stu>() {
            @Override
            public int compare(Stu o1, Stu o2) {
                return o1.age - o2.age == 0 ? o1.name.compareTo(o2.name) : o1.age - o2.age;
            }
        });
        tree.put(new Stu("B",12),"22100");
        tree.put(new Stu("A",10),"22101");
        tree.put(new Stu("C",13),"22101");
        System.out.println(tree.toString());
    }
}


class Stu{
    String name;
    int age;

    public Stu(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Stu{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}



```

#### TreeMap实例：

```java
package com.map;

import java.util.Map;
import java.util.Set;
import java.util.TreeMap;
import java.util.TreeSet;

/**
 * TreeMap映射元素个数(同样适用于HashMap)
 */



public class Demo04 {
    public static void main(String[] args) {
        String tpl = "abcsdwasdfsasfssa";
        TreeMap<Character,Integer> map = new TreeMap<>();
        for(int i = 0 ; i < tpl.length() ; i++){
            char c = tpl.charAt(i);
            Integer val = map.get(c);
            if(val == null){//未赋值是为空
                map.put(c,1);
            }
            else {
                val++;
                map.put(c,val);
            }
        }
        /**
         * 改变输出形式
         *  复习StringBuffer类
         */
        StringBuffer sb = new StringBuffer();
        Set<Character> characters = map.keySet();
        for(Character ch:characters){
            sb.append(ch).append("(").append(map.get(ch)).append(")\n");
        }
        System.out.println(sb);
        for(int i = 0 ; i < tpl.length() ; i++){
            char c = tpl.charAt(i);
            System.out.println(c + "出现的次数:" +map.get(c));
        }
    }
}

```

### Map的嵌套

```java
package com.map;

import java.util.HashMap;
import java.util.Map;
import java.util.Set;

/**
* 这里只介绍HashMap,TreeMap与其类似
*/
public class Demo07 {
    public static void main(String[] args) {
        HashMap<String,HashMap<String,String>> map = new HashMap<>();
        HashMap<String,String> m1 = new HashMap<>();
        m1.put("张三","男");
        m1.put("李四","男");
        m1.put("王五","女");
        HashMap<String,String> m2 = new HashMap<>();
        m2.put("AA","男");
        m2.put("BB","男");
        m2.put("CC","男");
        map.put("高一",m1);
        map.put("高二",m2);
        /**
         * 嵌套遍历方法1:
         *  map.entrySet()
         */
        Set<Map.Entry<String, HashMap<String, String>>> entries = map.entrySet();
        for (Map.Entry<String, HashMap<String, String>> entry : entries) {
            HashMap<String, String> value = entry.getValue();
            Set<Map.Entry<String, String>> entries1 = value.entrySet();
            for (Map.Entry<String, String> stringStringEntry : entries1) {
                System.out.println(entry.getKey() + " " + stringStringEntry.getKey() + " " + stringStringEntry.getValue());
            }
        }
        /**
         * 嵌套遍历方法2:
         *  map.keySet()
         */
        Set<String> strings = map.keySet();
        for (String string : strings) {
            HashMap<String, String> stringStringHashMap = map.get(string);
            for (String s : stringStringHashMap.keySet()) {
                System.out.println(string + " " + s + " " + map.get(string).get(s));
            }
        }
    }
}

```

