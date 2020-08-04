---
title: Linux-Bash命令
date: 2020-04-04 19:43:24
tags: Linux
categories: 
  - 学习历程
  - Linux基础
---

### Linux命令：

#### echo &lt;内容>

输出内容，与C/C++中的printf类似

<!-- more -->

#### date:

显示时间

#### cal：

显示当月日历

#### pwd:

显示当前工作目录

#### ls：

- ##### ls -a:

  显示所有隐藏文件

- ##### ls -l：

  显示更加详细的文件列表

- ##### ls &lt;folder>：

  显示特定的文件夹内容

#### cd：

- ##### cd ../:

  返回父目录

- ##### cd &lt;Directory>：

  进入特定的目录下

- ##### cd:

  返回主目录

#### mkdir：

创建文件夹

#### touch：

创建文件

##### rm：

删除文件

#### rmdir：

删除文件夹

#### cat:

读取文件并输出其内容，若查看多个文件，依次在cat后输入文件名即可

#### less：

读取文件并输出其内容，与cat类似，但是当文件内容较多时，推荐使用less，less会生成一个新窗口并展示内容

- /：

  找到特定的内容

- q：

  退出less

#### Pipelinesand Filters管道和过滤器

管道运算符“|”（垂直条）是一种将一个命令的输出作为输入发送到另一个命令的方法。

command1 | command2

当命令将其输出发送到管道时，该输出的接收端是另一个命令，而不是文件

#### grep &lt;内容> <文件>:

搜索具有给定字符串的行或查找指定输入流中的模式

#### wc：

利用wc指令我们可以计算文件的Byte数、字数、或是列数，若不指定文件名称、或是所给予的文件名为"-"，则wc指令会从标准输入设备读取数据。

- ##### wc -c：

  显示Bytes数。

- ##### wc -l：

  显示行数。

- ##### wc -w：

  显示字数。

#### sort：

- sort -b：

  忽略每行前面开始出的空格字符。

- sort -c：

  检查文件是否已经按照顺序排序。

- sort -d：

  排序时，处理英文字母、数字及空格字符外，忽略其他的字符。

- sort -f：

  排序时，将小写字母视为大写字母。

- sort -i：

  排序时，除了040至176之间的ASCII字符外，忽略其他的字符。

- sort -m：

  将几个排序好的文件进行合并。

- sort -M：

  将前面3个字母依照月份的缩写进行排序。

- sort -n：

  依照数值的大小排序。

### 试验：

这里我使用Git Bash进行试验

进入d盘建立MyTest文件夹，并在该文件夹下创建Test文本文件

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Post-Linux-Bash%E5%91%BD%E4%BB%A4/%E8%AF%95%E9%AA%8C1/%E8%AF%95%E9%AA%8C1.1.PNG" style="zoom: 75%;" />

进入vim对Test.txt进行编辑，cat命令显示出编辑后的内容，利用通道对该文件进行排序，并显示排序后的内容

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Post-Linux-Bash%E5%91%BD%E4%BB%A4/%E8%AF%95%E9%AA%8C1/%E8%AF%95%E9%AA%8C1.2.PNG" style="zoom:75%;" />

在MyTest文件夹下新建Test2文本文档，进入vim编辑，并查看编辑后的文件内容

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Post-Linux-Bash%E5%91%BD%E4%BB%A4/%E8%AF%95%E9%AA%8C1/%E8%AF%95%E9%AA%8C1.3.PNG" style="zoom:75%;" />

显示Test2.txt的内容，并将Test和Test2合并为一个MainTest

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Post-Linux-Bash%E5%91%BD%E4%BB%A4/%E8%AF%95%E9%AA%8C1/%E8%AF%95%E9%AA%8C1.4.PNG" style="zoom:75%;" />

显示合并后MainTest的内容

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Post-Linux-Bash%E5%91%BD%E4%BB%A4/%E8%AF%95%E9%AA%8C1/%E8%AF%95%E9%AA%8C1.5.PNG" style="zoom:75%;" />



持续更新中...

### tar：

- tar -c:

  建立压缩档案

- tar -x:

  解压

- tar -t:

  查看内容

- tar -r:

  向压缩文档文件末尾追加文件

- tar -u:

  更新原压缩包中的文件

**Tip：以上为必选参数，无论执行什么操作都需要以上参数中的一个**

- tar -z:

  使用gzip压缩

- tar -j:

  使用bzip2压缩

- tar -Z:

  具有compress属性

- tar -v:

  再压缩过程中显示文件

- tar -O:

  将文件解开到标准输出

- tar -f:

  使用文件名，f后需立即跟文档名（可以理解为f必须写在最后）

  

### ln:

​	**ln 文件1 文件2表示文件2为文件1的链接**

- ​	ln -s:

  ​	软连接文件，符号链接文件