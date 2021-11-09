# Lecture4 位操作符、泛型类型Lambda表达式和集合基础

## 1. 位运算符

### 运算符优先级表

操作符按照从上到下的优先级递减顺序显示，同一组中的运算符具有相同的优先级，表中显示了它们的结合性

![](<../.gitbook/assets/image (54).png>)

![](<../.gitbook/assets/image (55).png>)

![](<../.gitbook/assets/image (56).png>)

### 在内存中以位存储的任何整型

![](<../.gitbook/assets/image (57).png>)

其中 $$b_n$$是符号位

![](<../.gitbook/assets/image (58).png>)

#### 进制

* 十进制：-23 是 int，1L 或 1l 是long，123\_456 是 int
* 八进制：023 是 int，每个数字表示 3 个 bit
* 十六进制：0x2F，0XAF 是 int，以 0x 或 0X 开头，每个数字表示 4 个 bit
* 二进制：0b0011,0b1010\_1111 是 int，每个数字表示 1 个 bit

#### 整型转字符串

![](<../.gitbook/assets/image (59).png>)

### 按位运算符 Bitwise operators

![](<../.gitbook/assets/image (60).png>)

#### 按位运算示例

```java
// get b23..b16 from rgb.
int r = rgb>>16 & 0xFF; 

// set b23..b16 of rgb with b7..b0 of r,
// set b15..b8 of rgb with b7..b0 of g,
// set b7..b0 of rgb with b7..b0 of b.
rgb = r<<16 + g<<8 + b; 

// x = A and y = B Pre-condition
x = x ^ y;
y = x ^ y;
x = x ^ y;
// x = B and y = A Post-Condition
```

### 布尔运算符 Boolean related operators

![](<../.gitbook/assets/image (61).png>)

#### 布尔运算示例

```java
if(isConfirmed() == false)
if(!isConfirmed()) // elegant

if(a > b) return true; else return false;
return a > b ? true : false;
return a > b; // elegant

if(x != 0 && y/x > 5)... // 如果能得出结论，其余的子项均不计算
if(x != 0 & y/x >5)... // 所有的子项都计算
```

## 2. 泛型类型

### 泛型类

```java
class QueueOfStrings{
    private LinkedList<String> items = new LinkedList<>();
    public void enqueue(String item){
        items.addLast(item);
    }
    
    public String dequeue(){
        return items.removeFirst();
    }
    
    public boolean isEmpty(){
        return (items.size() == 0);
    }
}
```

```java
class QueueOfStrings<T>{
    private LinkedList<T> items = new LinkedList<>();
    public void enqueue(T item){
        items.addLast(item);
    }
    
    public T dequeue(){
        return items.removeFirst();
    }
    
    public boolean isEmpty(){
        return (items.size() == 0);
    }
}
```

### 泛型函数

```java
public static int countOccurrences(String[] list, String itemToCount){
    int count = 0;
    if(itemToCount == null){
        for(String listItem : list){
            if(listItem == null){
                count++;
            }
        }
    }else{
        for(String listItem : list){
            if(itemToCount.equals(listItem)){
                count++;
            }
        }
    }
    return count;
}
```

```java
// <T> 必须在返回值类型的标识符之前
public static <T> int countOccurrences(T[] list, T itemToCount){
    int count = 0;
    if(itemToCount == null){
        for(T listItem : list){
            if(listItem == null){
                count++;
            }
        }
    }else{
        for(T listItem : list){
            if(itemToCount.equals(listItem)){
                count++;
            }
        }
    }
    return count;
}
```

## 3. Lambda 表达式

Swing GUI，使用匿名内部类将行为与按钮单击关联起来

```java
button.addActionListener(new ActionListener(){
    public void actionPerformed(ActionEvent event){
            System.out.println("botton clicked");
    }
});
```

使用 lambda 表达式将行为与按钮单击关联

```java
botton.addActionListener(event -> System.out.println("botton clicked"));
```

### Lambda 表达式的使用示例

![](<../.gitbook/assets/image (62).png>)

### 一些不同的表达 Lambda 表达式的示例

```java
Runnable noArguments = () -> System.out.println("Hello World");

ActionListener oneArgument = event -> System.out.println("botton clicked");

Runnable multiStatement = () -> {
    System.out.print("Hello");
    System.out.println(" World")
}

BinaryOperator<Long> twoArguments = (x, y) -> x + y;

BinaryOperator<Long> explicitArguments = (Long x, Long y) -> x + y;
```

### 常用的函数式接口

要使用 Lambda 表达式，必须要有函数式接口（接口只有一个需要实现的方法）

![](<../.gitbook/assets/image (67).png>)

### Lambda 表达式与基本数据类型的参数

![](<../.gitbook/assets/image (63).png>)

### 静态方法 Lambda 表达式声明

![](<../.gitbook/assets/image (64).png>)

### 构造器的 Lambda 声明

![](<../.gitbook/assets/image (65).png>)

### 实例方法的 Lambda 声明

![](<../.gitbook/assets/image (66).png>)

