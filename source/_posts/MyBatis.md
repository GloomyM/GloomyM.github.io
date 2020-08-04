---
title: MyBatis
date: 2020-07-20 13:17:41
tags: Mybatis
categories:
 - 学习历程
 - SSM
---

#### Mybatis的环境搭建：

1. 创建maven工程导入坐标
2. 创建实体类和Dao接口
3. 创建Mybatis的主配置文件（SqlMapConfig.xml）
4. 创建映射配置文件（或使用注解）

<!--more-->

**SqlMapConfig.xml基础模板**

```xml
<?xml version="1.0" encoding="utf-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
<!--    环境配置-->
    <environments default="mysql">
<!--        配置mysql环境-->
        <environment id="mysql">
<!--            配置事务类型-->
            <transactionManager type="JDBC"></transactionManager>
<!--            配置数据源-->
            <dataSource type="POOLED">
<!--            配置连接数据库的基本信息 1.驱动 2.url 3.用户名 4.密码-->
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis01"/>
                <property name="username" value="root"/>
                <property name="password" value="sr20000316"/>

            </dataSource>
        </environment>
    </environments>
<!--    指定映射配置文件-->
    <mappers>
        <!--        前面使用配置文件这里这样写-->
        <mapper resource="映射配置文件的全类名"/>
        <!--        前面使用注解这里这样写-->
      	<mapper class="dao的全类名"/>
    </mappers>
</configuration>
```

**Dao层的xml配置文件模板（使用注解则不需要xml）**

```xml
<?xml version="1.0" encoding="utf-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
```

**pom.xml配置文件模板**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>Day03</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>
    <!--导入依赖-->
    <dependencies>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.4.5</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.21</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

</project>
```

#### MyBatis动态SQL：

- if标签
- where标签
- foreach标签
- sql标签

**if标签和where的应用**

```xml
<select id="findbycondition" resultType="com.Bean.User">
    select * from userinfo
    <where>
        <if test="name != null">
            and name = #{name}
        </if>
        <if test="sex != null">
            and sex = #{sex}
        </if>
    </where>

</select>
```

**if标签和where标签以及foreach标签的应用**

**foreach标签的参数：**

- collection：遍历的集合名
- open：开始位置
- close：结束位置
- item：代表集合中的元素的变量

```xml
<select id="testin"  resultType="com.Bean.User" parameterType="QueryVO">
        select * from userinfo
        <where>
            <if test= "list != null">
                <foreach collection="list" open="and id in (" close=")" item="id" separator=",">
                    #{id}
                </foreach>
            </if>
        </where>
    </select>
```

**sql标签不常用，不再举例了**

#### MyBatis注解：

##### 基础增删查改注解：

- @Insert
- @Update
- @Delete
- @Select

##### 处理实体属性名与表字段名不一致的注解：

- @Results：使用该属性需要同时使用@Result注解用来配置属性名对应的字段名（column表示数据库字段对应property表示实体属性名）

#### MyBatis的使用步骤：

1. 读取配置文件
2. 创建SqlSessionFactory工厂
3. 使用工厂生产SqlSession对象
4. 使用SqlSession创建Dao接口的代理对象
5. 使用代理对象执行方法
6. 释放资源

```java
package com;

import com.Bean.User;
import com.Dao.IUserDao;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.InputStream;
import java.util.List;

public class Test {
    public static void main(String[] args) throws Exception{
        //读取配置文件
        InputStream inputStream = Resources.getResourceAsStream("SqlMapConfig.xml");
        //创建工厂
        SqlSessionFactory factory = new SqlSessionFactoryBuilder().build(inputStream);
        //创建SqlSession对象
        SqlSession session = factory.openSession();
        //利用SqlSession创建Dao接口代理
        IUserDao userDao = session.getMapper(IUserDao.class);
        List<User> users = userDao.findById(1);
        System.out.println(users.toString());
        session.close();
        inputStream.close();
    }
}

```

#### Mybatis基于注解实现的一对一和一对多

- 基于注解的一对一：@one
- 基于注解的一对多：@many

**Tip:下面是一个测试项目，用来测试一对一和一对多的操作，每个用户拥有多个图书（一对多），每个账户对应一个用户（一对一），这里好像正好还把一对一和一对多链接起来了= =，在一对一的过程中还涉及了一对多，算是举一反三了吧哈哈~**

**pom.xml配置**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>Mybatis基于注解的开发</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>
    <dependencies>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.4.5</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.21</version>
        </dependency>
    </dependencies>

</project>
```

**Sql配置文件**

```xml
<?xml version="1.0" encoding="utf-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--    环境配置-->
    <environments default="mysql">
        <!--        配置mysql环境-->
        <environment id="mysql">
            <!--            配置事务类型-->
            <transactionManager type="JDBC"></transactionManager>
            <!--            配置数据源-->
            <dataSource type="POOLED">
                <!--            配置连接数据库的基本信息 1.驱动 2.url 3.用户名 4.密码-->
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis01"/>
                <property name="username" value="root"/>
                <property name="password" value="sr20000316"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <mapper class="com.Dao.IUserDao"></mapper>
        <mapper class="com.Dao.IBookDao"></mapper>
        <mapper class="com.Dao.IAccountDao"></mapper>
    </mappers>
</configuration>
```

**User实体**

```java
package com.Bean;

import java.io.Serializable;
import java.util.List;

public class User implements Serializable {

    private Integer id;
    private String name;
    private String sex;
    private List<Book> books;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }

    public List<Book> getBooks() {
        return books;
    }

    public void setBooks(List<Book> books) {
        this.books = books;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", sex='" + sex + '\'' +
                ", books=" + books +
                '}';
    }
}

```

**Book实体**

```java
package com.Bean;

public class Book {
    private String bookname;
    private Integer id;

    public String getBookname() {
        return bookname;
    }

    public void setBookname(String bookname) {
        this.bookname = bookname;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    @Override
    public String toString() {
        return "Book{" +
                "bookname='" + bookname + '\'' +
                ", id=" + id +
                '}';
    }
}

```

**Account实体**

```java
package com.Bean;

import java.io.Serializable;

public class Account implements Serializable {
    private Integer id;
    private Integer money;
    private User user;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public Integer getMoney() {
        return money;
    }

    public void setMoney(Integer money) {
        this.money = money;
    }

    public User getUser() {
        return user;
    }

    public void setUser(User user) {
        this.user = user;
    }

    @Override
    public String toString() {
        return "Account{" +
                "id=" + id +
                ", money=" + money +
                ", user=" + user +
                '}';
    }
}

```

**IAccountDao**

```java
package com.Dao;

import com.Bean.Account;
import org.apache.ibatis.annotations.One;
import org.apache.ibatis.annotations.Result;
import org.apache.ibatis.annotations.Results;
import org.apache.ibatis.annotations.Select;
import org.apache.ibatis.mapping.FetchType;

import java.util.List;

public interface IAccountDao {
//一对一
    @Select("select* from account")
    @Results(id = "accountMap",value = {
            @Result(id = true,column = "id",property = "id"),
            @Result(column = "money",property = "money"),
            @Result(column = "id",property = "user",one = @One(select = "com.Dao.IUserDao.findById",fetchType = FetchType.EAGER))
    })
    public List<Account> findAll();
}

```

**IBookDao**

```java
package com.Dao;

import com.Bean.Book;
import org.apache.ibatis.annotations.Select;

import java.util.List;

public interface IBookDao {

    @Select("select* from book where id = #{id}")
    public List<Book> findbyid(int uid);

}

```

**IUserDao**

```java
package com.Dao;

import com.Bean.User;
import org.apache.ibatis.annotations.Many;
import org.apache.ibatis.annotations.Result;
import org.apache.ibatis.annotations.Results;
import org.apache.ibatis.annotations.Select;
import org.apache.ibatis.mapping.FetchType;

import java.util.List;

public interface IUserDao {
//一对多
    @Select("select* from user where id = #{id}")
    @Results(id = "userMap",value = {
            @Result(id = true,column = "id",property = "id"),
            @Result(column = "name",property = "name"),
            @Result(column = "sex",property = "sex"),
            @Result(column = "id",property = "books",many = @Many(select = "com.Dao.IBookDao.findbyid",fetchType = FetchType.EAGER))
    })
    public List<User> findById(int id);
}

```

**Test测试类**

```java
package com;

import com.Bean.Account;
import com.Bean.User;
import com.Dao.IAccountDao;
import com.Dao.IUserDao;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.InputStream;
import java.util.List;

public class Test {
    public static void main(String[] args) throws Exception{
        //读取配置文件
        InputStream inputStream = Resources.getResourceAsStream("SqlMapConfig.xml");
        //创建工厂
        SqlSessionFactory factory = new SqlSessionFactoryBuilder().build(inputStream);
        //创建SqlSession对象
        SqlSession session = factory.openSession();
        //读取配置文件
        //利用SqlSession创建Dao接口代理
        IUserDao userDao = session.getMapper(IUserDao.class);
        IAccountDao accountDao = session.getMapper(IAccountDao.class);
        //测试一对多
        List<User> users = userDao.findById(1);
        System.out.println(users.toString());
        //测试一对一
        List<Account> accounts = accountDao.findAll();
        System.out.println(accounts.toString());
        session.close();
        inputStream.close();
    }
}

```

#### 总结：

Mybatis最主要的内容都在这里了，对于Mybatis中的一级缓存和二级缓存这里没有具体介绍，等以后理解深入了，会继续增加，总的来说Mybatis在开发中简化了很多操作，再去看以前写的项目，开始以为JDBC工具类已经很方便了，现在深入学习Mybatis功能真的很强大