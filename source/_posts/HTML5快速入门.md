---
title: HTML5基本标签
date: 2020-05-18 17:38:07
tags: HTML5
categories:
  - 学习历程
  - HTML
---

### 引入

HTML 是用来描述网页的一种语言。HTML 指的是超文本标记语言：HyperText Markup Language HTML 不是一种编程语言，而是一种标记语言标记语言是一套标记标签 (markup tag)HTML 使用标记标签来描述网页HTML文档包含了 HTML 标签及文本内容HTML 文档也叫做 web 页面 

<!-- more -->

### HTML标签

#### 标题标签 

HTML 标题（Heading）是通过 h1 - h6 等标签进行定义的。 

#### 段落标签 

HTML 段落是通过 p 标签进行定义的。 

#### 水平线标签

HTML水平线通过hr标签进行定义

#### 换行标签

HTML换行标签通过br标签进行定义

#### 字体标签

HTML字体标签通过font进行定义，

##### 属性：

size：字体大小

face：字体种类

color：字体颜色

#### 图片标签

HTML图片标签通过img进行定义

##### 属性：

src：URL

width：设置图片的宽度 

height：设置图片的高度 

alt：当图片无法正常显示时的提示文字

#### 列表标签

HTML有序列表通过ol标签进行定义，无序列表通过ul标签进行定义，列表里的每行元素通过li进行定义

##### 属性

disc：实心 

circle：空心

square：方块

#### 链接标签

HTML链接标签通过a标签进行定义

#### 属性

href：创建指向另一个文档的URL

name：创建文档内的书签 

target：设置显示位置

#### 表格标签

HTML表格标签通过table定义，表格中的每一行通过tr定义，每行中的每列通过td定义，标题通过th定义

##### 属性：

border：表格边框属性（默认无边框）

width：表格的宽

height：表格的高

align：控制表格位置，center，left，right

bgcolor：背景色

cellpadding：内边距

cellspacing：外边距

rowspan=？：合并？行 

colspan=？：合并？列 

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title>我是标题</title>
	</head>
	<body>
		<b>加粗的内容</b>
		<p><font color="red",face = "arial",size= 60>123</font></p>
		<img src="./img/img.png",alt="">
		<!-- 链接(target 为_blank表示在新窗口打开链接) -->
		<a href="http://www.baidu.com" target="_blank">百度一下</a>
		<!-- 无序列表 -->
		<ul type="disc">
			<li>1</li>
			<li>2</li>
			<li>3</li>
		</ul>
		<!-- 有序列表（前面有序号） -->
		<ol>
			<li>1</li>
			<li>2</li>
			<li>3</li>
		</ol>
		<!-- cellpadding 内边距 cellspacing 外边距 align 设置位置（中左右）-->
		<!-- tr表示行 th表示标题（自动加粗自动居中） td表示列 -->
		<table  border="1px" width = 500px height= 50px cellpadding="20" cellspacing="20" align="center">
			<tr>
				<th rowspan="2">标题1</th>
				<th>标题2</th>
				<th>标题3</th>
			</tr>
			<tr>
				<td>1.1</td>
				<td>1.2</td>
				<td>1.3</td>
			</tr>
			
			<tr>
				<td>2.1</td>
				<td>2.2</td>
				<td>2.3</td>
			</tr>
		</table>
		
	</body>
</html>

```

#### 框架标签

HTML框架标签用frameset来定义框架中的每一部分使用frame定义

##### 属性：

rows：将页面按行分割（百分比或像素）

cols：将页面按列分割（百分比或像素）

```html
<!-- 主页面 -->
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
	</head>
	<frameset rows="30%,60%,*">
		<frame src="top.html" >
		<frameset cols="30%,*">			
			<frame src="left.html">
			<frame src="right.html" name="right">
		</frameset>
		<frame src="bottom.html" >
	</frameset>
</html>

```

```html
<!-- 左侧页面 -->
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<!-- 让百度在右侧页面显示 -->
		<a href="http://www.baidu.com" target="right">百度</a>
	</body>
</html>

```

```html
<!-- 右侧页面 -->
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<p>Right Page</p>
	</body>
</html>

```

```html
<!-- 顶部页面 -->
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<p2>Top页面</p2>
	</body>
</html>

```

```html
<!-- 底部页面 -->
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<p1>Bottom</p1>
	</body>
</html>

```

