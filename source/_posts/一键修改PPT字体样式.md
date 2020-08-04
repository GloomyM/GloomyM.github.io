---
title: 一键修改PPT字体样式
date: 2020-04-19 17:35:15
tags: 其他
categories: 其他
---

### 前言

很多人在打印PPT时会出现，部分文字出现在PPT之外而无法完整打印，当然如果PPT页数很少，一页一页的改是完全可行的，但当你面临几百页的PPT时，手动更改就不现实了，这里我们使用宏进行意见更改

### 操作方式

打开PowerPoint点击视图，点击宏出现如下界面

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/%E4%B8%80%E9%94%AE%E4%BF%AE%E6%94%B9PPT%E5%AD%97%E4%BD%93%E6%A0%B7%E5%BC%8F/Image_01.png" style="zoom: 67%;" />

自定义宏名然后点击创建，

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/%E4%B8%80%E9%94%AE%E4%BF%AE%E6%94%B9PPT%E5%AD%97%E4%BD%93%E6%A0%B7%E5%BC%8F/Image_02.png" style="zoom:67%;" />

在代码区填写如下代码

```html
Sub OED01()
Dim oShape As Shape
Dim oSlide As Slide
Dim oTxtRange As TextRange
On Error Resume Next
For Each oSlide In ActivePresentation.Slides
   For Each oShape In oSlide.Shapes
          Set oTxtRange = oShape.TextFrame.TextRange
          If Not IsNull(oTxtRange) Then
         With oTxtRange.Font
             .Name = "微软雅黑"       '更改为需要的字体
             .Size = 24       '改为所需的文字大小
             .Color.RGB = RGB(Red:=0, Green:=0, Blue:=0) '改成想要的文字颜色，用RGB参数表示。这里代表黑色
          End With
          End If
   Next
   Next
End Sub
```

保存并退出，再次点击宏，选择刚刚定义的宏，点击执行，这样PPT中所有的页面字体都已经同步了

**Logion：心甘情愿，满是遗憾**

