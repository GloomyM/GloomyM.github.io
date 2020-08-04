---
title: MySQL配置与命令
date: 2020-05-10 10:57:45
tags:
---



### MySQL操作：

**①安装服务：mysqld --install**

**②初始化：mysqld --initialize --console**

**③开启服务：net start mysql**

**④关闭服务：net stop mysql**

**⑤登录mysql：mysql -u root -p（在下面PASSWORD后填入自己的密码）**

**⑥修改密码：alter user 'root'@'localhost' identified by 'root';(by 接着的是密码)**

**⑦标记删除mysql服务：sc delete mysql**

