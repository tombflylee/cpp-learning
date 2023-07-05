# 笔记03--基础语法

* （一个字节）1byte = 8 bits；最小存储单元为一个字节；



### 常量的定义

1. 使用`#define`，如：`#define PI 3.1415926`；
2. 使用`const`，如：`const double PI = 3.1415926`；

> 注意：
>
> 尽量使用const定义常量，**#define不会出现在编译器期**；
>
> \#define ASPECT\_RATIO 1.653  // 在编译时出错，很难排错；早期c语言常用
>
> const double ASPECT\_RATIO = 1.653 // 在编译时出错，可以排错

* define宏定义，只是做替换的比如上面用3.1415926替换PI；那么有参宏定义：

下面的代码中，MA(a + b)被替换为a+b\*(a + b - 1) ，注意第一个a+b是没有括号的！！

所以为1 + 2 \* (1 + 2 - 1) = 1 + 2\* 2 = 5;

```cpp
#define MA(x) x*(x - 1)
int main() {
    int a = 1, b = 2;
    cout << MA(a + b) << endl; // 输出5
}
```

### 【练习】使用宏定义，实现一个MIN函数

括号不能省略，因为a或者b可能为表达式

```cpp
#define MIN(a, b) (((a) > (b)) ? (a) : (b));
```



### 字符常量

* 字符常量是在**单引号**中的。如果常量以L（仅当大写时）开头，则表示它是一个宽字符常量（例如`L'x'`），此时它必须存储在`wchar_t`类型的变量中。否则，它就是一个窄字符常量（例如'x'），此时它可以存储在`char`类型的简单变量中；
* 字符常量可以是一个普通的字符（例如'x'）、一个转义序列（'\t'），或一个通用的字符（'\u02c0'）；

### assert断言

* 是一个宏
* ASSERT ()是一个调试程序时经常使用的宏，在程序运行时它计算括号内的表达式，**如果表达式为FALSE (0), 程序将报告错误，并终止执行**。如果表达式不为0，则继续执行后面的语句。这个宏通常原来判断程序中是否出现了明显非法的数据，如果出现了终止程序以免导致严重后果，同时也便于查找错误。

```cpp
#include <assert.h>
#include <iostream>
using namespace std;
int main() {
    bool a = true;
    bool b = false;
    assert(a);
    assert(b); // false的话，会报错
// Assertion failed: (b), function main, file test3.cpp, line 8.
}
```



### 位运算

| 运算符 | 描述           | 实例 |
| --- | ------------ | -- |
| <<= | 左移且赋值运算符     |    |
| >>= | 右移且赋值运算符     |    |
| &=  | 按位与且赋值运算符    |    |
| ^=  | 按位异或且赋值运算符   |    |
| \|= | 按位huo2且赋值运算符 |    |

```cpp

int main() {
    int a = 3;
    int b = 4;
    a <<= 2;
    b >>= 2;
    cout << a << endl; // 12  a: 0011，<<= 2后变成 1100 = 8+4 = 12
    cout << b << endl; // 1   b: 0100, >>= 2后变成 0001 = 1
}

```

### sizeof

返回类型的字节数

```cpp
int E = (A, B, C); // E应该为C
```

### 逗号运算符

会顺序执行一系列运算，整个逗号表达式的值是以逗号分隔的列表中的最后一个表达式的值；



### typedef

C 语言提供了 typedef 关键字，您可以使用它来为类型取一个新的名字。下面的实例为单字节数字定义了一个术语 BYTE：

```
typedef unsigned char BYTE;
```



### 【练习】bool、int、float与“零值”比较

```cpp
// bool
if(flag)
// int
if(flag == 0)
// double 
const double EPSINON = 0.00001;
if((flag > -))
```

























