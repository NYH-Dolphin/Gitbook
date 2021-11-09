# Lecture3 ADT、颜色、图片和图形

## 1. 抽象数据类型 ADT

### 数据类型介绍

数据类型是一组值和对这些值的一组操作

**基本数据类型 Primitive types**

* 值直接被映射到机器码表示
* 操作符直接被映射到机器语言

![Java 内置数据类型](<../.gitbook/assets/image (42).png>)

**抽象数据类型 Abstract data types**

* 抽象数据类型是对客户端隐藏其表示的数据类型
* 颜色、图片、字符串、复杂的数字、向量、矩阵等
* 客户端可以再不知道实现细节的情况下使用 ADT
  * 如何为几个有用的 ADT 编写客户端程序
  * 如何实现自己的 ADT

![ADT](<../.gitbook/assets/image (43).png>)

### String ADT

* 字符串是以 Unicode 编码的字符序列
* Java 的 ADT 允许我们编写操作字符串的 Java 程序

![](<../.gitbook/assets/image (44).png>)

#### 封装的 String

![](<../.gitbook/assets/image (45).png>)

* s1 == s2 is false
* s1 == s3 is true
* 如果使用 new 操作符，将创建一个新对象
* 如果使用 String 初始化器，则如果已经创建了内部对象，则不会创建新对象

### Color ADT

* 颜色是电磁辐射在眼睛中的一种感觉
* ADT 允许我们编写操作颜色的 Java 程序

![](<../.gitbook/assets/image (46).png>)

#### 单色亮度 monochrome luminance

一种颜色的单色亮度量化了它的有效亮度

![](<../.gitbook/assets/image (47).png>)

示例：在屏幕上，字体和背景色以什么样的搭配最易阅读

* 单色亮度的绝对值 > 128 的时候

![](<../.gitbook/assets/image (48).png>)

#### 灰度 garyscale

目的：将有颜色的图片转换为灰白的值

* 当所有三个 R、G 和 B 值相同时，生成的颜色灰度从 0 (黑色)到 255 (白色)
* 其实，给予颜色的就是单色亮度

![](<../.gitbook/assets/image (49).png>)

### Picture ADT

* 图片是由像素组成的二维数组
* ADT 允许我们编写处理图片的 Java 程序

![](<../.gitbook/assets/image (50).png>)

#### 图片灰度转换

目的：将彩色图片转换成灰色图片

![目标](<../.gitbook/assets/image (51).png>)

![实现](<../.gitbook/assets/image (52).png>)

### 实现一个数据类型

要创建数据类型，您需要提供以下代码

* 定义一系列值（实例变量）
* 实现对于这些值的操作（方法）
* 创造和实例化新的对象（构造器）

在 Java 中，一个数据类型的实现也被称为类 class

![](<../.gitbook/assets/image (53).png>)

