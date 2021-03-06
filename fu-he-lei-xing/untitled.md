# 1. 数组

## 1.1 数组的声明

 数组的声明应该指出以下三点

* 存储在每个元素中值的类型
* 数组名
* 数组中的元素数

```cpp
int array[10]; // 初始化一个大小为 10 的数组
int array[3] = {3,4,5}; // 初始化并对数组进行赋值
```

* 它是一个复合类型，不是“数组”类型，而是 “int 数组”类型
* 可以使用下标单独访问数组元素

### 有效下标

编译器不会检查使用的下标是否有效

如果 index 超过边界，程序运行后，这种赋值可能会引发问题

## 1.2 数组的初始化

```cpp
int cards[4] = {3, 6, 8, 10};     // okay
int hand[4];                      // okay
hand[4] = {5, 6, 7, 9};           // not allowed
hand = cards;                     // not allowed

float hotelTips[5] = {5.0, 2.5}   // 指对数组的前两个元素进行初始化
long totals[500] = {0};           // 将数组中所有元素初始化成 0
long totals[500] = {1};           // 第一个元素初始化成 1，其它为 0

short things[] = {1,5,4,8}        // C++ 编译器计算元素个数
double earnings[2] {1.2e4, 1.6e4} // 省略等号
unsigned int counts[10] = {};     // 将数组中所有元素初始化成 0
```

## 1.3 新增

* C++ 标准模板库 STL 提供了一种数组替代品 vector
* C++ 11 新增了模板类 array

