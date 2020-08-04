### JDBC快速入门

<!-- more -->

```JAVA
/**
 * 1. 注册驱动
 *    驱动从哪里来？   框架开发者会将代码封装成jar包
 *    项目根目录新建lib文件夹，拷贝驱动到此目录下
 *    将驱动进行编译，驱动文件右键 -- Add As Library
 *    使用java代码加载驱动类
 * 2. 获取数据库连接对象
 * 3. 通过数据库连接对象Statement对象
 * 4. 通过Statement对象执行sql语句
 * 5. 处理结果
 * 6. 关闭资源
 */
import java.sql.Connection;
import java.sql.Driver;
import java.sql.DriverManager;
import java.sql.Statement;

public class Demo {
    public static void main(String[] args) throws Exception{
        //1.注册驱动
        Class.forName("com.mysql.cj.jdbc.Driver");
        //2.获取数据库连接对象
        Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/test1","root","sr20000316");
        //3.通过数据库连接对象获得Statement()语句对象
        Statement st = conn.createStatement();
        //4.执行SQL语句
        String sql = "insert into person value(1003,'bs')";
        st.execute(sql);
        st.close();
        conn.close();
    }
}

```



### 类介绍

jar包：使用时只需要导入到项目中

​	    将驱动进行编译，驱动文件右键 -- Add As Library

#### Driver 接口

java.sql.Driver Java提供的接口，所有的数据库厂商会实现此接口

com.mysql.jdbc.Driver 实现了java.sql.Driver接口

该接口是所有JDBC程序必须实现的接口，该接口专门提供给数据库产商使用。



#### DriverManager

registerDriver() : 注册驱动

Connection getConnection(String url,String user, String password)  获取连接对象

​	url 指定数据库连接路径

​		语法：jdbc:mysql://ip地址:端口号/数据库名称

​			jdbc:mysql://localhost:3306/test1

​		细节：如果连接的是本机数据库，数据库的默认端口号为3306

​			jdbc:mysql:///test1

​	user  数据库用户名

​	password  数据库密码



#### Connection

数据库连接对象

普通方法

```JAVA
createStatement() 获取Statement（执行sql语句）
prepareStatement() 获取PrepareStatement对象，更加安全，用来避免SQL注入带来的问题
```

管理事务的方法

开启事务

​	setAutoCommit() 

提交事务

​	commit()

回滚事务

​	rollback()

#### Statement

执行sql的对象

普通方法

```JAVA
boolean execute() 执行任意的sql
int executeUpdate() 执行DML(insert update delete) DDL(create alter drop)
ResultSet executeQuery() 执行 DQL(select)
```

### 查询数据

#### ResultSet

封装了结果集的对象

常用方法

```
ResultSet executeQuery(String sql)

ResultSet的方法we
	next()：将游标自动下移，判断是否还有数据
	getXX(int columnIndex) XX为表中属性类型
		columnIndex:代表列的编号(从1开始计数)
	getXX(String name)  XX为表中属性类型name列名
```

使用步骤：

​	获取ResultSet对象

​	调用rs.next()，判断是否有下一行，因为数据的个数不确定，所以使用while循环来操作

​	调用getXX() 获取数据

#### 查询

##### 查询所有

```JAVA
public static void selectAll(){
    Connection conn = null;
    Statement st = null;
    try {
        //1. 注册驱动
        Class.forName("com.mysql.cj.jdbc.Driver");
        //2. 获取连接对象
        conn = DriverManager.getConnection("jdbc:mysql:///test1", "root", "sr20000316");
        //3. 获取数据库执行对象
        st = conn.createStatement();
        //4. 执行sql语句
        String sql = "SELECT * FROM  user";
        ResultSet rs = st.executeQuery(sql);
        //5. 处理结果
        while (rs.next()){
            //rs.getInt(1);
            int id = rs.getInt("id");
            String name = rs.getString("name");
            System.out.println(id + " " + name);
        }
    } catch (ClassNotFoundException e) {
        e.printStackTrace();
    } catch (SQLException e) {
        e.printStackTrace();
    }finally {
        //6. 无论如何都需要关闭
        if (st != null) {
            try {
                st.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        if (conn != null) {
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

    }
}
```

##### 封装数据

**将获取到的数据封装到对象中（User），然后将所有的User对象存入List集合**

**User类**

```JAVA
public class User {

    private Integer id;
    private String username;
    private String password;
    private String email;

    public User(Integer id, String username, String password, String email) {
        this.id = id;
        this.username = username;
        this.password = password;
        this.email = email;
    }
}
```

**查询的代码**

```JAVA
public static List<User> findAllUser() throws ClassNotFoundException, SQLException {
    Class.forName("com.mysql.jdbc.Driver");
    Connection conn = DriverManager.getConnection("jdbc:mysql:///test2", "root", "root");
    Statement st = conn.createStatement();
    ResultSet rs = st.executeQuery("SELECT * FROM user");
    List<User> users = new ArrayList<>();
    while (rs.next()){
        //根据列名取值
        int id = rs.getInt("id");
        String username = rs.getString("username");
        String password = rs.getString("password");
        String email = rs.getString("email");
        //封装数据
        User user = new User(id, username, password, email);
        users.add(user);
    }
    rs.close();
    st.close();
    return users;
}
```

### SQL注入带来的安全问题

​	利用特殊的字符或关键字参与sql字符串的拼接   会造成安全问题

> 用户名密码都输入:    a' or 'a' = 'a
>
> SELECT * FROM user WHERE username = 'a' or 'a' = 'a' AND password = 'a' or 'a' = 'a'
>
> 用户名密码都输入:      a' or 'a' = 'a' -- 由于SQL中--后表示注释，所以会出现安全问题
>
> SELECT * FROM user WHERE username = 'a' or '' = '' -- ' AND password = 'a' or 'a' = 'a' -- '

问题出现的原因:

​	sql拼接问题

预编译sql

```JAVA
获取PreparedStatement
	PreparedStatement ps = conn.prepareStatement(sql);

定义sql
参数使用?作为占位符
	SELECT * FROM user WHERE username = ? AND password = ?
设置参数,给?赋值
	void setXX(int parameterIndex, XX x)
		XX表示数据库表中具体的数据类型
		参数1 : ?号的编号 从1开始
		参数2 : ? 具体的值
```



修改后的方法为

```JAVA
public static boolean login2(String username,String password) throws Exception {
    Class.forName("com.mysql.jdbc.Driver");
    Connection conn = DriverManager.getConnection("jdbc:mysql:///test2", "root", "root");
    String sql = "SELECT * FROM user WHERE username = ? AND password= ?";
    PreparedStatement ps = conn.prepareStatement(sql);
    ps.setString(1, username);
    ps.setString(2, password);
    //真正执行sql语句
    ResultSet rs = ps.executeQuery();
    return rs.next();
}
```

### JDBC工具类

提供一个工具类, 获取数据库的连接对象(Connection)

编写思路:

 	1. 将数据库连接  驱动  用户名密码都写到配置文件中   jdbc.properties
 	2. 加载配置文件,读取配置信息
 	3. 根据key取值
 	4. 创建获取连接对象的方法   关闭连接的方法

**配置文件**

```properties
driverClassName=com.mysql.cj.jdbc.Driver

url=jdbc:mysql://localhost:3306/test1

username=root

password=sr20000316
```

**JDBCTools**

```Java
package Tools;

import java.io.FileReader;
import java.io.IOException;
import java.net.URL;
import java.sql.*;
import java.util.Properties;


//driverClassName=com.mysql.jdbc.Driver
//
//url=jdbc:mysql://localhost:3306/test1
//
//username=root
//
//password=sr20000316

public class JDBCTools {
    static String driverClassName;
    static String url;
    static String username;
    static String password;
    static {
        try {
            Properties p = new Properties();
            ClassLoader classLoader = JDBCTools.class.getClassLoader();
            URL path = classLoader.getResource("jdbc.properties");
            p.load(new FileReader(path.getPath()));
            driverClassName = p.getProperty("driverClassName");
            username = p.getProperty("username");
            url = p.getProperty("url");
            password = p.getProperty("password");
            Class.forName(driverClassName);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
    public static Connection connection() throws Exception{
        return DriverManager.getConnection(url, username, password);
    }

    public static void close(Connection conn, ResultSet result, Statement st){
        if(conn != null){
            try {
                conn.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
        }

        if(result != null){
            try {
                result.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
        }

        if(st != null){
            try {
                st.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
        }
    }
}

```

**测试类（登录案例）**

```java
import Tools.JDBCTools;

import java.sql.*;
import java.util.Arrays;
import java.util.Scanner;

public class Demo {
    public static void main(String[] args) throws Exception{
        Scanner sc = new Scanner(System.in);
        int id = sc.nextInt();
        String name = sc.next();
        if(login(id,name)){
            System.out.println("登陆成功");
        }else{
            System.out.println("登录失败");
        }
    }
    public static boolean login(int id , String name) throws Exception {
        Connection conn = null;
        PreparedStatement ps = null;
        ResultSet rs = null;
        try {
            conn = JDBCTools.connection();
            String sql = "select * from person where id = ? and name = ?";
            ps = conn.prepareStatement(sql);
            ps.setInt(1,id);
            ps.setString(2,name);
            rs = ps.executeQuery();
            return rs.next();
        } finally {
            JDBCTools.close(conn,rs,ps);
        }
    }
}


```











