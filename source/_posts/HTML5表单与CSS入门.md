---
title: HTML5表单与CSS样式
date: 2020-05-19 18:44:07
tags: HTML
categories:
  - 学习历程
  - HTML
---

### 引入

HTML 表单用于搜集不同类型的用户输入。HTML 表单包含表单元素，表单元素指的是不同类型的 input 元素、复选框、单选按钮、提交按钮等等

<!-- more -->

### 表单元素 

#### input元素

input元素有很多形态，根据不同的 type 属性，有不同的效果

##### 属性

type= "text" 文本输入域

type ="password" 密码输入域

type="checkbox" 复选框

type="radio" 单选按钮

type="file" 文件上传

type="hidden" 隐藏域

type="button" 按钮（不提交表单信息）

type="sumbit" 按钮（提交表单信息

type="reset" 按钮 （重置表单信息） 

#### select元素

HTML中使用select来定义下拉框，option用来定义每个选项

#### textarea

HTML中使用textarea定义多行文本

#### button

HTML中使用button来定义按钮，与input中的按钮类似，都存在三种不同的按钮submit，reset，button

### 表单属性

#### value

用来设置默认值

#### name

设置属性名

**Tip：属性名起到很关键的作用，后端中，通过属性名来拿到value，类似于map键值对**

#### required

设置必填

#### disable

disabled 属性规定输入字段是禁用的，被禁用的元素是不可用和不可点击的，被禁用的元素不会被提交。 

#### readonly

readonly 属性规定输入字段为只读（不能修改）

#### size

size属性设置字段长度

#### maxlength

maxlength属性设置字段最大长度

#### placeholder

placeholder设置提示信息

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title>表单</title>
	</head>
	<body>
		<!-- type设置种类 name设置属性名(最好填) value设置默认值 后台会根据name拿到value值(name对应value)-->
		<form action="" method="get">
			<!-- text文本框，显示输入的内容 -->
			<p>用户名:<input type="text" name="username" id="" value="admin" /></p>
			<!-- password密码框，显示密码（圆形）disable元素被禁用不会被提交 -->
			<p>密码:<input type="password" name= "password" id= "" value="admin" disabled="disabled"/></p>
			<!-- placeholder 输入框中显示文本 required 必填 -->
			<p>确认密码:<input type="password" name= "password" id= "" placeholder="请输入密码" required="required"/></p>
			
			<p>爱好:
				<!-- 复选框（可多选）checked为默认选择 -->
				<input type="checkbox" name="hobby" id="" value="basktball" checked="checked"/>篮球
				<input type="checkbox" name="hobby" id="" value="badminton" />羽毛球
				<input type="checkbox" name="hobby" id="" value="football" />足球
			</p>
			<!-- file添加文件 -->
			<input type="file" name="picture" id="" value="" />
			<p>性别:
			<!-- 单选框（只能选择一个，要设置name） -->
				男<input type="radio" name="sex" id="" value="male" />
				女<input type="radio" name="sex" id="" value="female" />
			</p>
			<!-- 下拉框（selected为默认选择） -->
			<select name="address">
				<option value="">请选择</option>
				<option value="JiangSu" selected="selected">江苏</option>
				<option value="GuangDong">广东</option>
				<option value="ZheJiang">浙江</option>
			</select><br>
			<!-- 可输入多行文本 -->
			自我介绍<textarea rows="10" cols="10">	
			</textarea>
			<!-- 普通按钮 -->
			<input type="button" name="" id="" value="普通按钮" />
			<!-- 提交表单按钮 -->
			<input type="submit" name="" id="" value="提交按钮" />
			<!-- 清空表单数据按钮 -->
			<input type="reset" name="" id="" value="清空按钮" />
			<button type="button" onclick="alert('你点击了我')">点击</button>
		</form>
	</body>
</html>

```

### CSS入门

#### CSS 基础语法 

CSS 语法由两个主要的部分构成：选择器，以及一条或多条声明。 

selector {declaration1;  declaration2;  ... declarationN };

#### 选择器

##### 元素选择器

最常见的 CSS 选择器是元素选择器。如果设置 HTML 的样式，选择器通常将是某个 HTML 元素，比如 p、h1、em、a，甚至可以是 html 本身

##### 属性选择器

属性选择器可以根据元素的属性及属性值来选择元素。

##### 类选择器

类选择器允许以一种独立于文档元素的方式来指定样式。

##### ID选择器

ID 选择器允许以一种独立于文档元素的方式来指定样式

##### 子代选择器

后代选择器（descendant selector）又称为包含选择器。后代选择器可以选择作为某元素后代的元素

**HTML主页面**

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title>选择器</title>
		<link rel="stylesheet" type="text/css" href="./css/demo.css"/>
	</head>
	<body>
		<input type="text" name="" id="" value="" />
		<p class="demo">123</p>
		<p id="demo02">456</p>
		<p><span>p标签中的span元素</span></p>
		<div><span>div中的span元素</span></div>
	</body>
</html>

```

**CSS**

```css
/* 类选择器 */
.demo{
	color: blueviolet;
	font-size: 20px;
	font-weight: bolder;
}
/* 元素选择器 */
html{
	background-color: cornflowerblue;
}
/* id选择器 */
#demo02{后代选择器 
	font-weight: bolder;
	font-size: 40px;
}
/* 属性选择器 元素名[属性]{} */
input[type="text"]{
	background-color: #8A2BE2;
}
/* 后代选择器  */
p span{
	color: aqua;
}
```

#### 个人信息表案例

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title>个人信息录入</title>
	</head>
	<body>
		<form action="" method="">
			<table border="1px" cellspacing="" cellpadding="">
				<tr>
					<td>
						<p>输入姓名</p>
					</td>
					<td>
						<input type="text" name="username" id="" value="" />
					</td>
				</tr>
				<tr>
					<td>
						<p>输入密码</p>
					</td>
					<td>
						<input type="password" name="password" id="" value="" placeholder="请入密码"/>
					</td>
				</tr>
				<tr>
					<td>
						<p>选择性别</p>
					</td>
					<td>
						<input type="radio" name="sex" id="" value="" />男
						<input type="radio" name="sex" id="" value="" />女
					</td>
				</tr>
				
				<tr>
					<td>
						<p>选择爱好</p>
					</td>
					<td>
						<input type="checkbox" name="hobby" id="" value="" />篮球
						<input type="checkbox" name="hobby" id="" value="" />足球
					</td>
				</tr>
			
				<tr>
					<td>
						<p>选择附件</p>
					</td>
					
					<td>
						<input type="file" name="filename" id="" value="" />
					</td>
				</tr>
				
				<tr>
					<td>
						<p>选择城市</p>
					</td>
					
					<td>
						<select name="city">
							<option value ="">请选择</option>
							<option value ="BeiJing">北京</option>
							<option value ="ShangHai">上海</option>
							<option value ="GuangZhou">广州</option>
							<option value ="HangZhou">杭州</option>
						</select>
					</td>
				</tr>
				<tr>
					<td align="center" colspan="2">
						<input type="reset" name="" id="" value="重置" />
						<input type="submit" name="" id="" value="提交" />
					</td>
				</tr>
			</table>
		</form>
	</body>
</html>

```

