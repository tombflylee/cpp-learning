# 笔记01-基础中的基础-小笔记

### 收入输出

* c style

```cpp
#include <stdio.h>
int main() {
    printf("hello world!\n");
    return 0;
}
```

* c++ style

```cpp
#include <iostream>
int main() {
    std::cout << "hello world!\n" << std::endl;
    return 0;
}
```



### printf & scanf

* scanf 要用**引用**给变量赋值

```cpp
#include<stdio.h>
#include<iostream>

int main(int argc, char ** argv) {
    int a = 99;
    int b = 98;
    printf("a:%d\n", a);
    printf("a: %d, b: %d", a, b);
    scanf("%d, %d", &a, &b);// 由于"%d, %d"中间写的是逗号，所以输入的两个值要用逗号隔开。
    std::cin >> a >> b;
    return 0;
}
```

### 类型介绍

* 8 bit = 1byte（字节）

| 有符号       | 无符号                | 数据长度（字节） |
| --------- | ------------------ | -------- |
| char      | unsigned char      | 1        |
| short     | unsigned short     | 2        |
| int       | unsigned int       | 4        |
| long      | unsigned long      | 4        |
| long long | unsigned long long | 8        |
| float     |                    | 4        |
| double    |                    | 8        |

* 其实上面的表中的数据长度，只是一个常见的默认值，不同的机器会有不同的情况，C++ 标准中并没有定义某一个数据类型必须占用多少个字节的长度，C++只定义了每种数据类型长度的一个范围。
  * short 要大于等于 char
  * int 要大于等于 short
  * long 要大于等于 int
  * long long 要大于等于 long

{% code title="查询类型大小" %}
```cpp
#include <stdio.h>

int main(int argc,char **argv)
{
    printf("int: %d\n", sizeof(int));
    
    return 0;
}
```
{% endcode %}



### 类型转换

隐式转换会遵守一个推演表，依照这个顺序进行转换，就不需要显式得指明类型；（就是要保证不会溢出）

<figure><img src="../.gitbook/assets/Screen Shot 2023-06-28 at 11.14.01 AM.png" alt=""><figcaption></figcaption></figure>

### 数组

* **初始化注意语法，是花括号{}，不是\[];**

```cpp
int main() {
    int a[50]; // 声明一个数组
    int b[4] = {1, 2, 3, 4}; // 初始化
    int c[] = {1, 2, 3, 4}; // 也可以不指定数组长度
    int d[4] = {1, 2}; // 也可以部分赋值
}
```

* 注意全初始化为0的时候，不能空着

```cpp
int a[20]; // 这样，不能保证所有都为0；！！！！
int b[20] = {0}; // 这才是对的
```

### 结构体

声明一个结构体：

```cpp
struct Student 
{
    int math;
    int english;
};
```

初始化一个结构体：

```cpp
int main() {
    struct Student stu;
    stu.math = 99;
    stu.english = 98;
    
    struct Student amy = {95, 95};
    return 0;
}
```



### 枚举类型

```cpp
#include <iostream>

enum Week
{
    Mon, 
    Tue,
    Wed,
    Thu,
    Fri,
    Sat,
    Sun
};

int main() {
    Week week = Week::Fri;
    std::cout << week << std::endl; // 输出4
    return 0;
}
```

### 指针

```cpp
#include <stdio.h>
#include <iostream>
using namespace std;
int main() {
    int a = 1;
    int b = 2;
    int* pa = &a;
    int* pb = &b;
    cout << *pa << endl; // 1
    cout << pa << endl; // 地址
    pa = pb; // pb存放的地址复制给pb，那就是pa和pb都指向了b
    cout << *pa << endl; // 2
    *pa += 3;
    cout << b << endl; // 5
    return 0;
}
```

* 空指针

不指向任意地址; 如果不确定该指向哪里，就赋值nullptr;

```cpp
int *p = nullptr;
int *p = NULL; // 历史遗留，不建议
int *p = 0; // 历史遗留，不建议
```

* 野指针

一个指针声明后，但未初始化，那么这个指针就是一个野指针；**野指针可能存放的是任意的地址**；

```cpp
int* p; // 一个野指针
```



### 自动变量（栈内存）

<mark style="background-color:orange;">变量在内存中的分配和销毁是自动的；</mark>

* 正常变量，会在变量的作用域结束后，自动销毁；
* c++中，**自动变量使用**<mark style="background-color:purple;">**“栈”**</mark>**来管理的**；

```cpp
int main() {
    {
        int b = 0;
    }
    b = 2; // 报错，因为变量b在上面已经被销毁了
}
```

### 堆内存 (malloc & free)

**堆内存中的变量，不会随着作用域的结束，而被自动回收，所以要手动释放；**

```cpp
#include <stdio.h>
#include <iostream>
#include <stdlib.h>
using namespace std;
int main() {
    int a = 1;
    int* p;
    {
        // 分配4个字节的空间；malloc返回一个指针，指向分配出的内存的首地址
        // 栈内存中分配了一个指针，然后在堆内存分配了4个字节的空间，然后把堆内存中分配的空间的首地址赋值给栈内存中的int指针；
        p = (int*) malloc(4); // 这段内存不会在这个作用域结束后被自动销毁
    }
    *p = 2;
    cout << *p << endl;
    free(p); // 释放这段内存
    return 0;
}
```

### 数组与指针

* 数组名是一个指向数组首地址的指针；

```cpp
#include<iostream>

int main() {
    int arr[5];
    std::cout << arr << std::endl; // 0x7ffd37a157b0
    std::cout << &arr[0] << std::endl; // 0x7ffd37a157b0
    
    *(arr + 2) = 3; // 等价于 arr[2] = 3
    return 0;
}
```

* 使用malloc构造

下面1和2是等价的

```cpp
#include<iostream>

int main() {
    int *p = (int*)malloc(5 * sizeof(int)); // 创建5个int大小的存储空间
    *(p + 2) = 3; // 1
    p[2] = 4; // 2.同样可以使用这种形式来访问；
}
```



### 函数

* c++中，函数声明必须在函数调用之后；
* c++会给每个函数分配一个独立的栈空间；



* 值传递

```cpp
void change (int a) { // change中的a，和main传给它的a，不是一样的；
    a--;
}
int main() {
    int a = 3;
    cout << a; // 3
    change(a);
    cout << a; // 依然为 3
}
```

* 引用传递（址传递）

```cpp
void change(int* a) {
    (*a)--;
}
int main() {
    int a = 3;
    cout << a; // 3
    change(&a);
    cout << a; // 2
}
```



> 本质上，传递指针变量，和传递普通变量都是一样的；都是拷贝！！
>
> \
> 在引用传递中，参数依然会拷贝给函数的入参，**不过此时拷贝的是一个地址；**\
> \
> 址传递和值传递，其实对于c++来说并没有任何区别，这两个概念完全是人为定义便于理解的；





