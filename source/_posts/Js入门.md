---
title: JavaScript
date: 2020-05-20 13:38:41
tags: JavaScript
categories:
  - 学习历程
  - JavaScript
---

### 引入

JavaScript简写 js，文件的后缀名也是 xxx.js，js 是基于对象和事件驱动的脚本语言，作用在客户端（浏览器）上。 

<!-- more -->

### JavaScript 变量

JavaScript中定义变量统一使用var关键字

```javascript
var x = 5;
```

### JavaScript 函数 

JavaScript中定义函数的方式：

```javascript
function 函数名(参数){
    return 返回值(可以无返回值)
}
```

###  JavaScript事件

#### onclick事件  

onclick点击事件，会在用户点击特定的内容时被触发。

#### onload和onunload事件

onload 和 onunload 事件会在用户进入或离开页面时被触发。onload 事件可用于检测访问者的浏览器类型和浏览器版本，并基于这些信息来加载网页的正确版本。 

#### onchange事件

onchange事件用来改变文本，常结合对输入字段的验证来使用。

#### onmouseover 和 onmouseout 事件 

onmouseover 和 onmouseout 事件可用于在用户的鼠标移至HTML元素上方或移出元素时触发函数。

#### onmousedown和onmouseup 以及 onclick 事件

onmousedown：鼠标按下时触发

onmouseup：鼠标释放时触发

**HTML文件**

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title>Js</title>
		
	</head>
	<script type="text/javascript" src="./js/demo.js"></script>
	<body onload="check()">
		<!-- onclick单击事件 -->	
		<input type="button" onclick="f2('Li','23')" name="" id="" value="点我" />
		<h1 onclick="this.innerHTML = '谢谢!'">点我改变</h1>
		<!-- onchange文本改变事件 -->
		<input type="text" name="" id="txt" value="" onchange="change()"/>
		<p>将文本框中的字段转换为大写</p>
		<!-- onmouseover与onmouseout事件 -->
		<div id="dv" onmouseover="togreen(this)" onmouseout="tored(this)">
			<p>鼠标移动在文字上变为绿色，移出变为红色</p>
		</div>
		<!-- onmousedown 鼠标按下事件  onmouseup 鼠标释放事件-->
		<div id="" onmousedown="changebg1(this)" onmouseup="changebg2(this)">
			<p>鼠标按下时背景色改为红，释放时背景色为绿div</p>
		</div>
	</body>
</html>

```

**Js文件**

```javascript
function f1(){
	var s = "Li";
	alert(s);
}

function f2(name,age){
	alert("我叫"+name+"我今年"+age+"岁了");
}

function change(){
	var text = document.getElementById("txt");
	text.value = text.value.toUpperCase();
}
			
function togreen(obj){
	obj.style.color = "green";
}
		
function tored(obj){
	obj.style.color = "red";
}
	
function changebg1(obj){
	obj.style.backgroundColor = "red";
}
function changebg2(obj){
	obj.style.backgroundColor = "green";
}
			
function check(){
	if(navigator.cookieEnabled == true){
		alert("cookies可用");
	}else{
		alert("cookies不可用")
	}
	
}
```

