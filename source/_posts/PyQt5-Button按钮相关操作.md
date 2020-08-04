---
title: PyQt5按钮控件
date: 2020-04-17 15:38:40
tags: PyQt5
categories:
  - 学习历程	
  - PyQt5
---

### 简介

**常见的按钮类包括：QPushButton、QToolButton、QRadioButton、QCheckBox、他们都继承自QAbstractButton类**

### QPushButton

| 方法        | 描述                                        |
| ----------- | ------------------------------------------- |
| isChecked() | 返回按钮的状态，被点击返回True否则返回False |
| setText()   | 设置按钮的显示文本                          |
| text()      | 返回按钮的显示文本                          |
| toggle()    | 在按钮状态之间进行切换                      |

### QRadioButton

可以切换on或者off，即checked或者unchecked；多个QRadioButton是一个按钮组合，如果多个独占的按钮组合，需要放在QGrouopBox或者QButtonGroup中；当切换on或者off时，会发送toggled信号，绑定这个信号，在按钮状态发生改变时，触发相应的行为；

| 方法           | 描述                                                         |
| -------------- | ------------------------------------------------------------ |
| isChecked()    | 返回按钮的状态，被点击返回True否则返回False                  |
| setText()      | 设置按钮的显示文本                                           |
| text()         | 返回按钮的显示文本                                           |
| setCheckable() | 设置按钮是否被选中，可以改变单按钮的选中状态True为选中False为释放 |

### QCheckBox

| 方法            | 描述                                               |
| --------------- | -------------------------------------------------- |
| isChecked()     | 返回按钮的状态，被点击返回True否则返回False        |
| setText()       | 设置复选框的显示文本                               |
| text()          | 返回复选框的显示文本                               |
| setChecked()    | 设置复选框的状态，True为选中，False为取消选中      |
| setTriState()   | 设置复选框为一个三态复选框（全选，部分选，全不选） |
| setCheckState() | 三态复选框的状态设置                               |

#### 三态复选框的三种状态

| 名称                | 值   | 含义                   |
| ------------------- | ---- | ---------------------- |
| Qt.Checked          | 2    | 组件没有被选中（默认） |
| Qt.PartiallyChecked | 1    | 组件被半选中           |
| Qt.Unchecked        | 0    | 组件被选中             |

### 简单试验

```python
# -*- coding: utf-8 -*-

# Form implementation generated from reading ui file 'untitled.ui'
#
# Created by: PyQt5 UI code generator 5.14.1
#
# WARNING! All changes made in this file will be lost!


from PyQt5 import QtCore, QtGui, QtWidgets
import sys

class Ui_MainWindow(QtWidgets.QMainWindow):
    def __init__(self):
        super(Ui_MainWindow,self).__init__()
        self.setupUi(self)
        self.retranslateUi(self)
        self.pushButton.clicked.connect(self.func_pushbutton)#与对应的槽函数连接
        self.checkBox_2.stateChanged.connect(self.func)
        self.checkBox_3.stateChanged.connect(self.func)
        self.checkBox_4.stateChanged.connect(self.func)
        self.checkBox.stateChanged.connect(self.func2)
    def setupUi(self, MainWindow):
        MainWindow.setObjectName("MainWindow")
        MainWindow.resize(800, 600)
        self.centralwidget = QtWidgets.QWidget(MainWindow)
        self.centralwidget.setObjectName("centralwidget")
        self.pushButton = QtWidgets.QPushButton(self.centralwidget)
        self.pushButton.setGeometry(QtCore.QRect(110, 150, 93, 28))
        self.pushButton.setObjectName("pushButton")
        self.lineEdit = QtWidgets.QLineEdit(self.centralwidget)
        self.lineEdit.setGeometry(QtCore.QRect(210, 150, 311, 21))
        self.lineEdit.setObjectName("lineEdit")
        self.checkBox = QtWidgets.QCheckBox(self.centralwidget)
        self.checkBox.setGeometry(QtCore.QRect(110, 220, 91, 19))
        self.checkBox.setObjectName("checkBox")
        self.checkBox_2 = QtWidgets.QCheckBox(self.centralwidget)
        self.checkBox_2.setGeometry(QtCore.QRect(130, 260, 91, 19))
        self.checkBox_2.setObjectName("checkBox_2")
        self.checkBox_3 = QtWidgets.QCheckBox(self.centralwidget)
        self.checkBox_3.setGeometry(QtCore.QRect(130, 300, 91, 19))
        self.checkBox_3.setObjectName("checkBox_3")
        self.checkBox_4 = QtWidgets.QCheckBox(self.centralwidget)
        self.checkBox_4.setGeometry(QtCore.QRect(130, 340, 91, 19))
        self.checkBox_4.setObjectName("checkBox_4")
        MainWindow.setCentralWidget(self.centralwidget)
        self.menubar = QtWidgets.QMenuBar(MainWindow)
        self.menubar.setGeometry(QtCore.QRect(0, 0, 800, 26))
        self.menubar.setObjectName("menubar")
        MainWindow.setMenuBar(self.menubar)
        self.statusbar = QtWidgets.QStatusBar(MainWindow)
        self.statusbar.setObjectName("statusbar")
        MainWindow.setStatusBar(self.statusbar)

        self.retranslateUi(MainWindow)
        QtCore.QMetaObject.connectSlotsByName(MainWindow)

    def retranslateUi(self, MainWindow):
        _translate = QtCore.QCoreApplication.translate
        MainWindow.setWindowTitle(_translate("MainWindow", "MainWindow"))
        self.pushButton.setText(_translate("MainWindow", "PushButton"))
        self.checkBox.setText(_translate("MainWindow", "全选"))
        self.checkBox_2.setText(_translate("MainWindow", "按钮1"))
        self.checkBox_3.setText(_translate("MainWindow", "按钮1"))
        self.checkBox_4.setText(_translate("MainWindow", "按钮1"))

    def func(self):#判断复选框的三种状态，全选，非全选，部分选中
        if self.checkBox_2.isChecked() and self.checkBox_3.isChecked() and self.checkBox_4.isChecked():
            self.checkBox.setCheckState(QtCore.Qt.Checked)
        elif self.checkBox_2.isChecked() or self.checkBox_3.isChecked() or self.checkBox_4.isChecked():
            self.checkBox.setTristate(True)
            self.checkBox.setCheckState(QtCore.Qt.PartiallyChecked)
        else:
            self.checkBox.setTristate(False)
            self.checkBox.setCheckState(QtCore.Qt.Unchecked)

    def func_pushbutton(self):
        self.pushButton.setText("你点击了我")
        self.lineEdit.setText("你点击了pushButton")

    def func2(self):
        if self.checkBox.checkState() == QtCore.Qt.Checked:#如果全选则将其他复选框全部勾选(True)
            self.checkBox_2.setChecked(True)
            self.checkBox_3.setChecked(True)
            self.checkBox_4.setChecked(True)
        elif self.checkBox.checkState() == QtCore.Qt.Unchecked:#非全选将其他复选框全部去掉勾选(False)
            self.checkBox_2.setChecked(False)
            self.checkBox_3.setChecked(False)
            self.checkBox_4.setChecked(False)

if __name__ == '__main__':
    app = QtWidgets.QApplication(sys.argv)
    win = Ui_MainWindow()
    win.show()
    sys.exit(app.exec_())
```

**Logion：宁愿一生孤独，也不愿随波逐流**