# Lecture2 OOP、异常、国际化、I/O流和文件

## 1. 纲要

* 计算机系统的设计和应用是复杂的
* OOP 的基本概念
* 异常与异常处理
* I/O 流和文件

## 2. 计算机系统的设计和应用是复杂的

### 常见 CS 课程的 3 个维度

* **THEORY**：概念，模型，数学，算法，原理， 机制，方法
  * 需要理解抽象的东西
* **STSTEM and TOOLS related**：HW，网络，操作系统，PLs， ide，DBMS，客户端，服务器，虚拟机，云中的容器
  * 需要正确理解、设置和使用它们
* **DESIGN related**：根据需求（问题），需要使用理论和工具来创建 / 实施 / 测试解决方案

### 软件设计

#### 软件是复杂的

**Computer System Design and Application** is **Complex**

但是 Complex（错综复杂的）≠ complicated（复杂难懂的）

* Complex = composed of many simple parts related to one another
* Complicated = not well understood, or explained

#### 软件设计是复杂且难懂的

* 软件规模增长带来要素数量增长，熵增长必然导致混乱 （热力学第三定律）
* 准确定义需求很难（用户不知道要什么，只知道不要什么），需求蔓延是软件项目失败的首要原因
* 不同的设计可以实现同样的功能(系统结构 / 行为 / 功能的关系），判断一个设计是否是好的设计很难（Conway’s law: 软件的结构倾向于与开发团队的组织架构具相似性）

### Function-Behaviour-Structure 实体

* **Function**：设计对象的目的
* **Behavior**：可以从设计对象的结构派生的属性
* **Structure**：设计对象的组件及其关系

功能与行为相联系，行为与结构相联系，功能和结构之间没有联系

### Conway 定律

> 软件组织与软件团队组织相一致的规则\
> 通常是这样说的：“如果你有四个小组致力于一个编译器，那么你将得到一个 4 种编译器。”\
> Organizations which design systems are constrained to produce designs which are copies of the communication structures of these organizations

* 它是解释为什么软件开发是困难的原因之一
* 如何判断一个设计的好坏是一个很大的挑战，这很大程度上取决于经验

### 如何将系统分解成模块？

![](<../.gitbook/assets/image (10).png>)

* High Cohesion within modules：高内聚
* Loose Coupling between modules：低耦合
* Information Hiding：信息隐藏

#### 模块化 Modularity 内聚 Cohesion 和耦合 Coupling

* 一个复杂的系统可以被分成更简单的模块
* 把系统分解成由各个模块组成的效果叫模块化
* **Separation of Concerns**（SoC，关注点分离）
  * 在处理一个模块时，我们可以忽略其他模块的细节
* 每个模块都应该是高度内聚的
  * 模块可以理解为一个有意义的单元
  * 模块的组件是紧密相关的
* 模块应该表现出低耦合
  * 模块与其他模块之间的交互很低
  * 分别可以理解

#### 结构化程序设计

* 一个复杂的系统可以被分成更简单小块，被称为模块
* 分而治之
* 逐步求精
* 将复杂问题做合理的分解，再分别仔细研究问题的不同侧面（关注点）， 最后综合各方面的结果, 合成整体的解决方案

### 软件工程管理开发过程中的变更

计算机并不关心代码是如何组织的 —— 但人类很关心

更改代码既困难又昂贵，而且因为世界在变化，这是必不可少的，我们想让它变得简单和便宜

* 最小化必须更改的代码量
* 很容易知道哪些代码必须更改
* 将必须更改的代码放在一起
  * 在一个文件中更改 6 行代码通常比在 6 个文件中分别更改 1 行代码便宜

#### 好的编程的评判标准

* **Objectives 目的**：有效地（正确地）高效地运行
* **Approaches 手段**：易于扩展和修改
* **Pre-conditions 前提**：易于理解

#### 如何让变更更加容易和便宜

* 在定义良好的代码段中**隐藏某些信息**，以便该代码段的用户不依赖于它，并且在它发生变化时也不需要更改
* **函数的调用者不知道函数是如何工作的**：只知道它接受的参数类型和它返回的类型
  * 为了使用数据类型，您不需要知道数据类型是如何实现的，阅读文档就足够了：有哪些操作，它们做什么？
* 这样，就可以编写无需更改的代码，即使实现发生更改（是否可以编写依赖于实现的代码则是另一回事，如果不是，封装的数据类型(封装)）

### 模块和对象

![模块是子程序和数据的松散分组](<../.gitbook/assets/image (12).png>)

![对象封装数据](<../.gitbook/assets/image (13).png>)

### 面向对象与面向过程

#### 面向过程

* 面向过程的更直观，因为它是以个人为中心的
  * 思考下一步该做什么，该走哪条路
* 面向流程的不能扩展到复杂的、大规模的问题
  * 大规模的问题需要人们的组织，而不是个人单独工作

#### 面向对象

* 由于分工的原因，面向对象可能更令人困惑
  * 思考如何将问题分解成任务，分配责任，协调工作
  * 这是一个管理问题
* 面向对象是以组织为中心的
  * 但是，很难设计出好的组织

#### 面向对象的哲学

* 基于软件必须要做的事情来构造软件的问题是，这会发生很大的变化
* 它工作的领域变化要小得多
* 围绕领域中的事物来组织您的软件使其更容易理解和维护

## 3. 异常与异常处理

### 异常的介绍

* 在 Java 中，异常通常用于控制指令执行流，以处理不同的情况
* 在 c++ 和 Lisp 中，它们用于异常和不可预测的错误

处理程序错误有两个方面：**检测 detection **和**处理 handling**

* 例如，Scanner 构造函数可以检测从不存在的文件中读取的尝试，但是，它不能处理这个错误
* 处理错误的一种令人满意的方法可能是终止程序，或者向用户请求另一个文件名
* Scanner 类不能在这些选项中进行选择，它需要将错误报告给程序的另一部分
* 在 Java 中，异常处理提供了一种灵活的机制，可以将控制从错误检测点传递给能够处理错误的处理程序

**异常是对象**

* Java 中的异常是由“异常事件”生成的特殊对象 (通常是一个错误)，它通过一种不同于对象间通常消息传递的机制传递回调用方法

### throw

```java
throw new MyException();
```

* 你抛出的是一个对象，不是一个类型
* 由于异常是一个对象，所以必须在需要时使用 new 实例化（从类定义为类型的模板创建）并抛出它

![](<../.gitbook/assets/image (14).png>)

### throws

由于一些异常经常发生，一些方法通过在 throws 后加上可能抛出的异常的名称来发出警告，然后让 javac 编译器知道它们

![](<../.gitbook/assets/image (15).png>)

如果你忽略了方法种 throws 的异常

![](<../.gitbook/assets/image (16).png>)

* javac 不会让你这么做的，它的信息非常明确：它希望你要么处理问题，要么让世界知道某些东西可能会失败，而另一个对象必须处理它

### 错误 Error 的类型

#### 编译时 Compile Time

* 语法错误
* 错误的类型
  * 很多事情都可能出错，所以我们有不同类型的错误，当 Javac 将 .java 文件编译为 .class java 字节码文件时，它会告诉您错误的语法，或者在分配数据或调用方法时不兼容的类型。在考虑运行程序之前，必须解决所有这些问题

#### 链接时 Link Time

* 在你可以运行你的程序之前，类加载器必须加载它，你可能已经通过编译和失败的链接，因为类加载器不能找到 .class 对应于要使用的对象

#### 运行时 Run Time

* 被应用检测到
* 被库检测到
* 被操作系统 / 硬件检测到
  * 当你运行你的程序时，你可能会遇到其他错误;，的应用程序方法之一可以检测到它获取的参数类型正确，但值范围错误，内置的 Java 方法可能会发现相同的情况(并抛出异常)，或者，事情可能真的出错了，操作系统可能会发现(例如，硬件故障)，逻辑也可能是错误的
  * 这些被称为**异常 Exceptions**

### 异常 Exception 的类型

![](<../.gitbook/assets/image (19).png>)

![](<../.gitbook/assets/image (20).png>)

### 捕获异常

```java
try{
    statement
    statement
    ...
}catch(ExceptionClass exceptionObject)
{
    statement
    statement
}
```

### 检查异常

在 Java 中，可以抛出和捕获的异常分为三类

* **系统内部的错误**：由类型 Error 的子类报告，一个例子是 OutOfMemoryError，当所有可用的计算机内存都用完时抛出该错误，这些是很少发生的致命错误，我们在本书中将不考虑它们
* **运行时错误**：RuntimeException 的子类，如 IndexOutOfBoundsException 或IllegalArgumentException 表示代码中的错误，它们被称为**未检查的异常 unchecked exceptions**
* 其他异常都是**受控异常 checked exceotions**：这些异常表明由于某些超出你控制的外部原因而出现了错误

当您面临这个选择时，您正在处理所谓的检查异常，javac 需要你选择下面两种情况之一

#### 捕获并处理异常

![](<../.gitbook/assets/image (21).png>)

![](<../.gitbook/assets/image (25).png>)

#### 抛出异常

![](<../.gitbook/assets/image (23).png>)

![](<../.gitbook/assets/image (24).png>)

### 错误与异常

![](<../.gitbook/assets/image (26).png>)

* 异常是程序或 java 中发生的异常情况，告诉您发生了错误，当异常发生时，java 强制我们处理它
* 异常处理提供了一种处理错误和从错误中恢复的方法，或者一种优雅地退出程序的方法
* 错误表示严重表示严重的不可恢复问题，例如 VirtualMachineError、OutOfMemoryError

### 自定义异常

* 不需要从头创建自己的异常，而是扩展Java Throwable，因此必须决定要扩展什么类
  * 应该继承 **Exception **类吗？那么它将是一个 checked exception，javac 将确保它是根据规则使用的
  * 或者继承 **RuntimeException**，然后 javac 将不会强制您的异常的用户遵循在方法名中声明它并使用 throw 或 try/catch 的要求
    * **unchecked Exception 是RuntimeException的子类**

```java
class MyException extends RuntimeException{
    ...
}
```

### 关闭资源

当使用一个必须关闭的资源时，例如 PrintWriter，需要小心出现异常

![](<../.gitbook/assets/image (27).png>)

#### Try-with-resources 语句

在 try 语句中声明 Printwriter 变量，如下所示

![](<../.gitbook/assets/image (29).png>)

![](<../.gitbook/assets/image (30).png>)

* 更一般地，您可以在 try-with-resources 语句中声明实现 **AutoCloseable **接口的任何类的变量

#### Try-finally 语句

try-with-resources 语句调用语句头中声明的变量的 close 方法

在**关闭资源时**，应该始终使用** try-with-resources** 语句

除了调用 close 方法之外，还可能需要进行一些清理，在这种情况下，使用 try-finally 语句

![](<../.gitbook/assets/image (31).png>)

* 很少需要 try-finally 语句，因为大多数需要清理的 Java 库类都实现了 AutoCloseable 接口

## 5. 国际化 Internationalization

* 国际化是指制作可以根据不同的地点和语言进行输入和输出的程序
* 根据所编码字符的数量，字符编码可以采用不同的形式，编码的字符数与每个表示的长度有直接关系，通常用字节数来衡量，**要编码更多的字符本质上意味着需要更长的二进制表示**

### **Base64 encoding**

![](<../.gitbook/assets/image (32).png>)

### Character Encoding

* 国际摩斯码编码了 26 英语字母A到Z，一些非英语字母，阿拉伯数字和一组小的标点符号和程序信号 ，大写字母和小写字母之间没有区别

![](<../.gitbook/assets/image (33).png>)

### ASCII 字符集

![Unicode 字符集的一小部分](<../.gitbook/assets/image (34).png>)

### Unicode

* 不同的编码方案单独开发并在当地的地理环境中实践开始变得具有挑战性
* 不难理解，虽然编码很重要，但解码对于理解表示也同样重要。只有在广泛使用一致或兼容的编码方案时，这才有可能实现
* 这一挑战催生了一种被称为 **Unicode **的单一编码标准，它可以**容纳世界上所有可能的字符**，这包括那些正在使用的字符，甚至那些已经失效的字符
* 因此，如何将这些编码点编码成位取决于 Unicode 内部的特定编码方案 &#x20;

![Unicode 字符集中的一些非西方字符](<../.gitbook/assets/image (35).png>)

#### UTF-32

UTF-32 是一种 Unicode 编码方案，使用四个字节来表示定义的每个代码点 Unicode，显然，每个字符使用 4 个字节会降低空间效率

* 例如：“UTF-32” 中的 “T” 为 00000000 00000000 00000000” 01010100 （前 3 个字节是不必要的）

#### UTF-8

可变长度编码：UTF-8 是另一种使用可变长度字节进行编码的 Unicode 编码方案。虽然它通常使用单个字节来编码字符，但如果需要，它可以使用更多的字节，从而节省空间

* 例如：“T” 在 “UTF-8” 中是 01010100
* 但 “語” 在 “UTF-8”是中是 11101000 10101010 11101000

### BOM

BOM (byte-order mark ) 文件编码头，即字节顺序标记

它是插入到以 UTF-8, UTF16 或 UTF-32 编码文件开头的特殊标记

用来标记多字节编码文件的**编码类型和字节顺序 big-endian **或** little-endian **

一般用来识别文件的编码类型

* 根据字节序的不同，UTF-32 可以被实现为 UTF-32LE 或 UTF-32BE

![](<../.gitbook/assets/image (41).png>)

## 6. I/0 流和文件

### 读入文件

首先，构造一个带有输入文件名称的 File 对象

```java
File inputFile = new File("input.txt");
```

然后使用 File 对象来构造一个 Scanner 对象

```java
Scanner in = new Scanner(inputFile);
```

* 这个 Scanner 对象从文件 input.txt 中读取文本
* 可以使用 Scanner 方法（例如 nextInt()、nextDouble() 和 next()）从输入文件读取数据

![](<../.gitbook/assets/image (37).png>)

![](<../.gitbook/assets/image (40).png>)

### 写入文件

要将输出写入文件，可以使用所需的文件名构造一个 PrintWriter 对象

```java
PrintWriter out = new PrintWriter("output.txt");
```

* 如果输出文件已经存在，则在向其写入新数据之前将其清空，如果文件不存在，则创建一个空文件
* Printwriter 类是已经知道的 PrintStream 类的增强——System.out是一个 PrintStream 对象
* 可以对任何 Printwriter 对象使用熟悉的 print()、printIn() 和printf() 方法

![](<../.gitbook/assets/image (38).png>)

### 处理完所有文件后关闭它们

![](<../.gitbook/assets/image (39).png>)

### 字符编码

字符被编码为一个字节序列

如果需要处理带有重音字符、中文字符或特殊符号的文件，应该明确请求 **UTF-8** 编码

```java
Scanner in = new Scanner(file, "UTF-8");
PrintWriter out = new PrintWriter(file, "UTF-8");
```

{% file src="../.gitbook/assets/Lab2 FileIO.pdf" %}
Lab2 FileIO
{% endfile %}

