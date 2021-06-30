# 1. 简单文件输入 / 输出

## 1.1 写入文本文件

## 1.1 写入文本文件

注意

注意

* 必须包含头文件 fstream
* 头文件 fstream 定义了一个用于处理输出的 ofstream 类
* 需要声明一个或多个 ofstream 变量
* 必须指明命名空间 std
* 需要将 ofstream 对象于文件夹关联起来，为此，方法之一是使用 open\(\) 方法
* 使用完文件后，应该使用方法 close\(\) 关闭
* 必须包含头文件 fstream
* 头文件 fstream 定义了一个用于处理输出的 ofstream 类
* 需要声明一个或多个 ofstream 变量
* 必须指明命名空间 std
* 需要将 ofstream 对象于文件夹关联起来，为此，方法之一是使用 open\(\) 方法
* 使用完文件后，应该使用方法 close\(\) 关闭

### 示例

### 示例

```cpp
#include <iostream>
#include <fstream> // for file I/O
int main()
{
    using namespace std;
    char automobile[50];
    int year;
    double a_price;
    double d_price;

    // 从控制台获取输入
    cout << "Enter the make and model of automobile ";
    cin.getline(automobile, 50);:
    cout << "Enter the model year: ";
    cin >> year;
    cout << "Enter the original asking price: ";
    cin >> a_price;
    d_price = 0.913 * a_price;

    // 用 cout 在屏幕上显示信息
    cout << fixed;
    cout.precision(2);
    cout.setf(ios_base::showpoint);
    cout << "Make and model: " << automobile << endl;
    cout << "Year: " << year << endl;
    cout << "Was asking $" << a_price << endl;
    cout << "Now asking $" << d_price << endl;


    ofstream outFile; // create object for output
    outFile.open("carinfo.txt"); // associate with a file

    // 现在用 outFile 代替 cout 做完全相同的事情
    outFile << fixed;
    outFile.precision(2);
    outFile.setf(ios_base::showpoint);
    outFile << "Make and model: " << automobile << endl;
    outFile << "Year: " << year << endl;
    outFile << "Was asking $" << a_price << endl;
    outFile << "Now asking $" << d_price << endl;
    
    outFile.close(); // done with file
    return 0;
}
```

```cpp
#include <iostream>
#include <fstream> // for file I/O
int main()
{
    using namespace std;
    char automobile[50];
    int year;
    double a_price;
    double d_price;

    // 从控制台获取输入
    cout << "Enter the make and model of automobile ";
    cin.getline(automobile, 50);:
    cout << "Enter the model year: ";
    cin >> year;
    cout << "Enter the original asking price: ";
    cin >> a_price;
    d_price = 0.913 * a_price;

    // 用 cout 在屏幕上显示信息
    cout << fixed;
    cout.precision(2);
    cout.setf(ios_base::showpoint);
    cout << "Make and model: " << automobile << endl;
    cout << "Year: " << year << endl;
    cout << "Was asking $" << a_price << endl;
    cout << "Now asking $" << d_price << endl;


    ofstream outFile; // create object for output
    outFile.open("carinfo.txt"); // associate with a file

    // 现在用 outFile 代替 cout 做完全相同的事情
    outFile << fixed;
    outFile.precision(2);
    outFile.setf(ios_base::showpoint);
    outFile << "Make and model: " << automobile << endl;
    outFile << "Year: " << year << endl;
    outFile << "Was asking $" << a_price << endl;
    outFile << "Now asking $" << d_price << endl;
    
    outFile.close(); // done with file
    return 0;
}
```

此代码会输出一个文本文件 carinfo.txt

```aspnet
Make and model: CarModel
Year: 2021
Was asking $1000000.00
Now asking $913000.00
```

程序最后一部分与 cout 几乎完全相同

在声明了一个 ofstream 对象后，可以使用方法 open\(\) 将该对象特定文件关联起来

```cpp
ofstream outFile; // create object for output
outFile.open("carinfo.txt"); // associate with a file
```

程序使用完该文件后，应该将其关闭

```cpp
outFile.close(); // done with file
```

* **outFile 可以使用 cout 可以使用的任何方法**
* 如果在该程序运行前， carinfo.txt 并不存在，则 **open\(\) 将创建一个名为 carinfo.txt 的文件**
* 如果在该程序运行前， carinfo.txt 已经存在，则 **open\(\) 会先丢弃源文件的所有内容**，再将新的输出加入该文件中

## 1.2 读取文本文件

## 1.2 读取文本文件

注意

注意

* 必须包含头文件 fstream
* 头文件 fstream 定义了一个用于处理输出的 ifstream 类
* 需要声明一个或多个 ifstream 变量
* 必须指明命名空间 std
* 需要将 ifstream 对象于文件夹关联起来，为此，方法之一是使用 open\(\) 方法
* 使用完文件后，应该使用方法 close\(\) 关闭
* 可以使用 ifstream 对象和 get\(\) 方法来读取一个字符，getline\(\) 来读取一行字符
* 可以结合使用 ifstream 和 eof\(\)，fail\(\) 等方法来判断输入是否成功

### 示例

```cpp
// sumafile.cpp -- functions with an array argument
#include <iostream>
#include <fstream> // file I/O support
#include <cstdlib> // support for exit()
const int SIZE = 60;
int main()
{
    using namespace std;
    char filename[SIZE];

    // 输入文件名打开
    ifstream inFile; // object for handling file input
    cout << "Enter name of data file: ";
    cin.getline(filename, SIZE);
    inFile.open(filename); // associate inFile with a file
    if (!inFile.is_open()) // failed to open file
    {
        cout << "Could not open the file " << filename << endl;
        cout << "Program terminating.\n";
        exit(EXIT_FAILURE);
    }

    double value;
    double sum = 0.0;
    int count = 0; // number of items read
    inFile >> value; // get first value
    while (inFile.good()) // while input good and not at EOF
    {
        ++count; // one more item read
        sum += value; // calculate running total
        inFile >> value; // get next value
    }
    if (inFile.eof())
        cout << "End of file reached.\n";
    else if (inFile.fail())
        cout << "Input terminated by data mismatch.\n";
    else
        cout << "Input terminated for unknown reason.\n";
    if (count == 0)
        cout << "No data processed.\n";
    else
    {
        cout << "Items read: " << count << endl;
        cout << "Sum: " << sum << endl;
        cout << "Average: " << sum / count << endl;
    }
    inFile.close(); // finished with the file
    return 0;
}
```

需要特别注意的是文件读取循环的设计

* 程序读取文件时不应该超过 EOF，如果最后一次读取数据遇到 EPF
  * **方法 eof\(\) 将返回 true**
* 上述程序希望输入到 value 里的是 int 类型，如果最后一次读取操作发生了类型不匹配
  * **方法 fail\(\) 将返回 true**
* 可能出现文件受损或硬件故障的问题
  * **方法 bad\(\) 将返回 true**
* good\(\) 方法在没有发生任何错误时返回 true





