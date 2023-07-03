# 笔记02-基础中的进阶

### 指针

> <mark style="background-color:purple;">数组名单独拿出来，就是一个指向数组的指针！！</mark>
>
> int指针 + 1：代表向后移动了一个int类型的大小， 4个字节；
>
> 同理，short指针 + 1 ： 那么向后移动了short类型的大小， 2个字节；
>
> 指针还可以++，--，都是向后/向前移动位置；
>
> 但是arr这个数组名指针，却不允许++ / -- 这个操作，这也是它特别的地方；

```cpp
int a = 1;
int* p = &a;
int arr[10];
int* p1 = arr; // 数组名单独拿出来就是一个指向数组的指针！！
int *p1 = &arr[0]; // 与上面等价
*p1 = 10; // 修改数组中的第一个元素
*(p + 1) = 20; // 修改数组中的第二个数组
```



指针操作结构体

```cpp
struct Student 
{
    int age;
    string name;
}
struct Student stu;
stu.age = 12;
stu.name = "amy";

struct Student* p = &stu;
p->age = 13;
p->name = "david";
```



### 函数指针

> ```
> 声明 ： int (* funcP)(int a, int b)
> ```

```cpp
int func(int a, int b) {
    return a + b;
}
int (* funcP)(int a, int b) = func;
(*funcP)(1, 2); // 函数指针的调用
```

* 函数作为入参传给另一个函数

```cpp
void doWork(int (*callback)()) {
    int result = (*callback)();
    cout << result << endl;
}
int funcA() {
    cout << "funcA" << endl;
    return 1;
}
int funcB() {
    cout << "funcB" << endl;
    return 2;
}
int funcC() {
    cout << "funcC" << endl;
    return 3;
}

int main() {
    doWork(&funcA);
    doWork(&funcB);
    doWork(&funcC);
    return 0;
}

```



### 静态变量的作用域

static 修饰的静态局部变量只执行初始化一次，而且延长了局部变量的生命周期，直到程序运行结束以后才释放。

函数内部的局部变量会在函数结束时，被释放；如果使用了static来声明，那么就不会被释放，一直到程序结束；



### 面向对象编程

> 面向过程编程: 任何程序都由：顺序、选择、循环 构成；
>
> 是按照程序执行的顺序来编写的；
>
> \
> 但这种方式忽略了**对象** 和 **动作** 之间的关系，比如打开冰箱门，是人打开？还是大象打开？
>
>



### 类

```cpp
#include <iostream>

class Staff
{
    
};

int main() {
    // 实例化
    Staff stf1;
    Staff stf2;
    // 将对象分配到堆上，使用new和delete来实现；
    Staff *st1 = new Staff();
    Staff *st2 = new Staff();
    
    // delete来释放
    delete st1;
    delete st2;
    return 0;
}
```



### public、private、protected

#### private

* `private`用来指定私有成员。一个类的私有成员，不论是成员变量还是成员函数，都只能在该类的内部才能被访问。例如

```cpp
class A
{
private:
    int a;
    int b;
}
```

私有成员是不能在外部使用的，例如，想要这样干是不行的：

```cpp
int main(int argc,char **argv)
{
    A a;
    a.a = 15; // 会报错，因为成员变量是 private 的
    return 0;
}
```

#### public

* 用来指定公有成员。一个类的公有成员在任何地方都可以被访问。例如

```cpp
class A
{
public:
    int a;
    int b;
}
```

#### protected

* 用来指定保护成员。一般是允许在子类中访问。（后续学习类的继承后你就明白了）

### 成员函数

{% code title="Staff.h" %}
```cpp
#include <string>
using namespace std;

class Staff 
{
public:
    string name;
    int age;
    int printStaff();
};
```
{% endcode %}



{% code title="Staff.cpp" %}
```cpp
#include <iostream>
#include "Staff.h"

using namespace std;

int Staff::printStaff() {
    cout << "Name is: " << name << endl;
    cout << "Age is: " << age << endl;
    return 0;
}
```
{% endcode %}



{% code title="main.cpp" %}
```cpp
#include "Staff.h"

int main() {
    Staff stf1;
    stf1.name = "tombflylee";
    stf1.age = 31;
    stf1.printStaff();
    
    return 0;
}
```
{% endcode %}

### 成员函数的重载

成员函数的重载是指在同一个类中，**函数名字相同，函数参数不同的函数**。

```cpp
#include <string>

class Staff
{
public:
    void FuncA();
    void FuncA(int a);
};
```



### 构造函数和析构函数

#### 构造函数

和类名相同，没有返回值的函数，这个函数称为构造函数。构造函数的特殊之处在于，他会在类实例化的时候被调用。构造函数是可以有参数的，我们常常用构造函数来进行初始化

```cpp
////////////////////////Staff.h/////////////////////////
#include <string>

class Staff
{
public:
    Staff(std::string _name, int _age);

public:
    std::string name;
    int age;
};
//////////////////////////Staff.cpp///////////////////////
#include "Staff.hpp"
#include <stdio.h>

Staff::Staff(std::string _name, int _age)
{
    name = _name;
    age = _age;
}
////////////////////////main.cpp/////////////////////////
#include <stdio.h>

#include "Staff.hpp"

int main(int argc,char **argv)
{
    Staff staff("mooc", 29);

    return 0;
}

```

#### 析构函数

而对象销毁的时候，就会调用析构函数。

```cpp
//////////////////////////Staff.h///////////////////////
#include <string>

class Staff
{
public:
    Staff(std::string _name, int _age);
    ~Staff();

public:
    std::string name;
    int age;
};
////////////////////////Staff.cpp/////////////////////////
#include "Staff.hpp"
#include <stdio.h>

Staff::Staff(std::string _name, int _age)
{
    name = _name;
    age = _age;
    printf("构造函数被调用\n");
}

Staff::~Staff()
{
    printf("析构函数被调用\n");
}
```

> 调用代码不改，然后再运行一下。我们发现，程序在调用了构造函数之后，又调用了析构函数。
>
> 我们之前讲过栈内存，**这个对象是分配在栈上面的，实例化的时候，调用了构造函数，而紧接着，main 函数就要结束了，这个栈对象就自动销毁了，销毁的时候，就调用了析构函数**。

### 赋值构造函数

```cpp
int main(int argc,char **argv)
{
    Staff staffA;
    Staff staffB = staffA; // C++ 会自动为我们拷贝 staffA 中的成员变量到 staffB 的成员变量中

    return 0;
}
```

> 缺点：
>
> 当我们使用这种方式实例化对象的时候，并不会调用普通构造函数，而是会调用一个特殊的构造函数，被称之为赋值构造函数或者拷贝构造函数。如果我们没有写，那么就会按照**浅拷贝的方式来进行复制。**
>
> \
> **所以，如果有一个成员变量是指针，那么这种方式就有问题：**

<figure><img src="../.gitbook/assets/Screen Shot 2023-07-03 at 11.22.59 AM.png" alt="" width="375"><figcaption></figcaption></figure>

<pre class="language-cpp"><code class="lang-cpp">////////////////////////////////Staff.h/////////////////////////////
<strong>#include &#x3C;string>
</strong>using namespace std;

class Staff 
{
public:
    Staff(string _name, int _age);
    ~Staff();
public:
    string name;
    int age;
    char* mem = nullptr;
    int printStaff();
};
////////////////////////////////Staff.cpp/////////////////////////////
#include &#x3C;iostream>
#include "Staff.h"

using namespace std;

Staff::Staff(string _name, int _age) {
    mem = (char*)malloc(20);
    name = _name;
    age = _age;
    cout &#x3C;&#x3C; "构造函数被调用！" &#x3C;&#x3C; endl;
}

Staff::~Staff() {
    if(mem != nullptr) {
        free(mem);
        mem = nullptr;
    }
    cout &#x3C;&#x3C; "析构函数被调用！" &#x3C;&#x3C; endl;
}

int Staff::printStaff() {
    cout &#x3C;&#x3C; "Name is: " &#x3C;&#x3C; name &#x3C;&#x3C; endl;
    cout &#x3C;&#x3C; "Age is: " &#x3C;&#x3C; age &#x3C;&#x3C; endl;
    return 0;
}
</code></pre>

### 运算符重载

* 重载运算符+

```cpp
/////////////////////////////////////RMB.h/////////////////////////////////
class RMB {
public:
    RMB(int _yuan, int _jiao, int _fen);
    ~RMB();
    RMB operator + (const RMB & rmb); // 运算符重载
private:
    int yuan = 0;
    int jiao = 0;
    int fen = 0;
};
/////////////////////////////////////RMB.cpp/////////////////////////////////
#include "RMB.h"

RMB::RMB(int _yuan, int _jiao, int _fen) {
    yuan = _yuan;
    jiao = _jiao;
    fen = _fen;
}
// 运算符重载
RMB RMB::operator + (const RMB &rmb) {
    RMB rmbRes(0, 0, 0);

    // fen
    int f = rmb.fen + fen;
    int f_ = f / 10;
    rmbRes.fen = f % 10;

    // jiao
    int j = rmb.jiao + jiao + f_;
    int j_ = j / 10;
    rmbRes.jiao = j % 10;

    // yuan
    int y = rmb.yuan + yuan + j_;
    int y_ = y / 10;
    rmbRes.yuan = y % 10;

    return rmbRes;
}
RMB::~RMB() {

}
/////////////////////////////////////main.cpp/////////////////////////////////
#include "Staff.h"
#include "RMB.h"

int main() {
    RMB rmbA(1, 9, 0);
    RMB rmbB(2, 5, 0);
    RMB rmbC = rmbA + rmbB;  //
    return 0;
}
```



### 类的继承

`Coder`继承自`Staff`

```cpp
class Coder : public Staff {
};
```

> 上面的public：
>
> 指明：子类中是否要保持对父类成员的权限；
>
> <img src="../.gitbook/assets/Screen Shot 2023-07-03 at 12.29.07 PM.png" alt="" data-size="original">\
> 所以上面的public Staff，代表了保持父类中函数、变量的权限保持不变，叫做“**公有继承**”

### 多态

* <mark style="background-color:orange;">C++ 多态意味着调用成员函数时，会根据调用函数的对象的类型来执行不同的函数</mark>；

```cpp
int main(int argc,char **argv)
{
    Child * obj = new Child();
    obj->func();
    
    Base * baseobj = (Base *)obj;
    baseobj->func();

    delete obj;
    return 0;
}
```



### 类的转换

类之间可以相互转换。类的转换主要是在**父类**和**子类**之间的转换;

**也存在隐式转换 、显式转换的问题；**

```cpp
#include <string>
#include <iostream>
using namespace std;
class Staff
{
public:
    string name;
    int age;
}

class Coder : public Staff
{
public:
    string language;
}

int main() {
    Coder *coder = new Coder();
    Staff *staff = coder; // 隐式转换就可以
    Coder *coder = (Coder*) staff; // 必须显式转换，但可能出问题   
}
```

### 编联

我们之前讲述了什么是多态，还用了一个例子，将一个指针的类型做成强转，然后调用 func 函数，就会发现， func 函数会随着被强转的类型的变换而变换，这种函数的关联过程称为编联。按照联编所进行的阶段不同，可分为两种不同的联编方法：静态联编和动态联编。

#### **静态编联** <a href="#undefined" id="undefined"></a>

```
Child * obj = new Child();
Base * baseobj = (Base *)obj;
baseobj->func();
delete obj;

return 0;
```

再来看看这个例子，我们通过强制转换来指定 func 执行的是哪个。这个过程是在编译阶段就将函数实现和函数调用关联起来，因此静态联编也叫早绑定，在编译阶段就必须了解所有的函数或模块执行所需要检测的信息。

#### **动态编联** <a href="#undefined" id="undefined"></a>

除了静态编联之外，C++ 还支持动态编联。动态联编是指联编在程序运行时动态地进行，根据当时的情况来确定调用哪个同名函数，实际上是在运行时虚函数的实现。当然，我们现在所学的知识还没办法完成动态编联，接下来，我们将要学习虚函数，来实现动态编联。



* 注意下面代码中，main函数中打印的内容

```cpp
////////////////////Staff.h//////////////////
#include <string>
using namespace std;

class Staff 
{
public:
    void work();
};
////////////////////Staff.cpp//////////////////
#include <iostream>
#include "Staff.h"

using namespace std;

void Staff::work() {
    cout << "staff work." << endl;
}
////////////////////Coder.h//////////////////
#include "Staff.h"

class Coder : public Staff 
{
public: 
    void code();
    void work();
};
////////////////////Coder.cpp//////////////////
#include "Coder.h"
#include <iostream>
using namespace std;

void Coder::code () {
    cout << "code." << endl;
}
void Coder::work() {
    cout << "coder work." << endl;
}
////////////////////mian.cpp///////////////////
#include "Coder.h"

int main() {
    Staff me;
    me.work(); // staff work
    Coder him;
    him.work(); // coder work.
    Staff *her = new Coder(); // 此处很神奇调用的的函数式Staff中的
    her->work(); // staff work.
    return 0;
}
```

> 上面的代码：her实际调用的不是Coder中的work函数，而是Staff中的work函数
>
> ```cpp
> Staff *her = new Coder();
> her->work();
> ```

#### virtual实现了动态编联

* 因为，函数名其实就是一个指针，它指向了函数的实现；
* <mark style="color:purple;background-color:orange;">**而使用virtual来修饰的成员函数，函数名就不再指向函数的实现，而是指向了一个虚函数表的东西。这种函数为虚函数；虚函数表中存放的东西，则指向了真正的函数实现；**</mark>

<figure><img src="../.gitbook/assets/Screen Shot 2023-07-03 at 1.28.11 PM.png" alt="" width="375"><figcaption></figcaption></figure>

对于virtual修饰的work函数，指向的是虚函数表的一个指针；虚函数表的指针，指向了具体的实现；

```cpp
virtual int work();
```

当我们声明一个Staff类的指针的时候，**我们其实只初始化了，函数名到虚函数表的指向这一部分；而此时还没有具体的实现；**

```cpp
Staff * staff
```

当我们把具体实现赋值给指针时，虚函数表的指针才会有具体的值，此时才会有具体的实现；

```cpp
Staff *staff = new Coder();
```



* 我们将Staff类中的work加入virtual来修饰：

此时，再次执行her->work()，就真正执行了Coder类中的work方法！！

```cpp
//////////////////////////////Staff.h///////////////////////////
class Staff 
{
public:
    virtual void work();
};
/////////////////////////////main.cpp//////////////////////////
int main() {
    Staff *her = new Coder();
    her->work(); // coder work.
    return 0;
}
```

### 虚函数

虚函数 是在基类中使用关键字 virtual 声明的函数。在派生类中重新定义基类中定义的虚函数时，会告诉编译器不要静态链接到该函数。

我们想要的是在程序中任意点可以根据所调用的对象类型来选择调用的函数，这种操作被称为动态链接，或后期绑定。

### 纯虚函数

您可能想要在基类中定义虚函数，以便在派生类中重新定义该函数更好地适用于对象，但是您在基类中又不能对虚函数给出有意义的实现，这个时候就会用到纯虚函数。

* <mark style="background-color:blue;">**只在.h中给出定义，且要赋值为0；**</mark>
* <mark style="background-color:blue;">**在cpp中不能给出实现！！**</mark>
* <mark style="color:green;background-color:blue;">**包括纯虚函数的类，只能被继承，不能被实例化；**</mark>

```cpp
class Staff 
{
public:
    virtual void work() = 0;
};
```



### 析构函数为纯虚函数

**对于含有纯虚函数work的父类Staff，如果父类Staff和子类Coder都有析构函数，那么再释放内存时不会调用子类Coder的析构函数；必须要把父类Staff的析构函数也声明为纯虚函数！！！**

```cpp
class Staff {
public:
    virtual ～Staff();
    virtual void work();
}
```



### 动态内存管理

遵循RAII（资源获取即初始化）的原则，

1. 仅在构造函数中，考虑资源的创建；
2. 仅在析构函数中，考虑资源的销毁；
3. 在其他函数中，只考虑资源的使用；



### C++ 中的空指针 <a href="#j_codelang" id="j_codelang"></a>

我们之前的课程中曾经讲过空指针的问题，知道在 C++ 中，有使用 NULL 和 nullptr 两种方式表示空指针的方法。

```
int * p = NULL;
int * p = nullptr;
```

这一小节来看看两者的区别。

<mark style="color:purple;background-color:orange;">**但是NULL 不等于0，因为类型就不同；**</mark>

#### **NULL** <a href="#null" id="null"></a>

首先看 NULL，在 C++ 中，NULL 其实就是 0。

例如：

```
int * p = NULL;
```

等价于：

```
int * p = 0;
```

因为在 C++ 中，0 地址通常是被保护起来的，不可访问的。因此用 0 地址来指代这个指针哪里都不指，是可以的。但是这里面却存在一些问题。因为 NULL 就是 0，所以我们可以把 NULL 用在其他地方。

例如：

```
int a = NULL;
```

我们可以将一个 int 变量赋值成 NULL，你永远无法阻止有人这么干。而在某些情况下，甚至会在不经意间酿成惨剧。

例如：

```
class A
{
public:
    void func(void * t)
    {
    }

    void func(int i)
    {
    }

}
```

这个类中，func 函数有两个重载。这个时候，我们尝试用 NULL 调用一下：

```
int main(int argc,char **argv)
{
    A a;
    a.func(NULL);

    return 0;
}
```

猜猜这个函数到底调用的哪个重载？

#### **nullptr** <a href="#nullptr" id="nullptr"></a>

正是由于 NULL 会导致这样的混乱，所以在 C++11 标准之后，C++ 标准委员会为 C++ 添加了 nullptr 关键字。我们可以将 NULL 赋值给一个普通变量，而 nullptr 却不能。

```
int a = nullptr;
```

这样是会直接报错的。

nullptr 只能赋值给指针，所以不会有 NULL 那样的问题。

所以，只要你的编译器兼容 C++11 标准，那么你应该使用 nullptr。

### 引用

引用其实和指针一样，在查看汇编过后的代码，发现引用和指针得到的汇编代码时一样的。

* **引用不可以不初始化，因为引用不是一个变量！**
* **引用不可以二次赋值；**

### 不同的const

C++ 中的 const 千变万化，之前我们已经学过使用 const 来做一个常量。const 在 C++ 中整体表示的语意是“不变的”，但是 const 申明在不同位置，却会有不一样的效果。这一小节，我们来集中学习一下 const。

#### **const 修饰普通变量**

例如：

```
const int a = 20;
```

则表示 a 是一个常量，你不可以在后续对其进行修改。因为 a 不可修改，所以在创建的时候就要对 a 进行赋值，不对其进行赋值则会报错。例如，下面的代码就会报错

```
const int a;
```

#### **const 修饰指针**

const 修饰指针可以分为多种情况：

* 只有一个 const，如果 const 位\*左侧，表示指针所指数据是常量，不能通过解引用修改该数据；指针本身是变量，可以指向其他的内存单元

```
int aaa = 20;
int bbb = 30;
const int * constPoint = &aaa;

constPoint = &bbb;
*constPoint = 80; // 这行代码会报错
```

* 只有一个 const，如果 const 位于\*右侧，表示指针本身是常量，不能指向其他内存地址；指针所指的数据可以通过解引用修改

```
int aaa = 20;
int bbb = 30;
int * const constPoint = &aaa;

constPoint = &bbb; // 这行代码会报错
*constPoint = 80;
```

* 两个 const，\*左右各一个，表示指针和指针所指数据都不能修改

```
int aaa = 20;
int bbb = 30;
const int * const constPoint = &aaa;

constPoint = &bbb; // 这行代码会报错
*constPoint = 80; // 这行代码会报错
```

#### **const 修饰函数参数**

const 修饰函数参数和修饰普通函数是一样的。但是要注意的时候 const 修饰函数参数的时候，其作用域仅仅限制在函数内部。也就是说，你可以把一个不用 const 修饰的参数传入到 const 修饰的参数中去。而只要在函数中保持其不变性就可以了。

#### **const 修饰成员函数**

* const 修饰的成员函数不能修改任何的成员变量

```
class A
{
public:
    int aaa;

    int funcA() const
    {
        aaa = 20; // 这行代码会报错
        return 0;
    }
}
```

* const 成员函数不能调用非 const 成员函数

```
class A
{
public:
    int aaa;

    int funcA() const
    {
        funcB(); // 这行代码会报错
        return 0;
    }

    int funcB()
    {
        return 0;
    }
}
```

#### &#x20;**const 修饰函数返回值**

修饰返回值要分成两种情况

* 址传递，返回指针，引用。

在 C++ 中有时我们会写这样的代码：

```
A aaa;
A & getA(){
    return aaa;
}

int main(int argc,char **argv)
{
    A bbb;
    getA() = bbb;

    return 0;
}
```

上面的代码运行之后，aaa 变量就会被 bbb 所赋值，但是有些时候这样做会造成一些混乱

例如：

```
getA() == a
```

有时候会有笔误：

```
getA() = a
```

这种情况下，就会有问题，而且不容易被找到这个错误。

所以在大多数情况下，我们可以给返回值加一个 const ，这样可以防止返回值被调用。

```
A aaa;
const A & getA(){
    return aaa;
}

int main(int argc,char **argv)
{
    A bbb;
    getA() = bbb; // 这行代码会报错

    return 0;
}
```

* 值传递。

值传递就简单多了，因为值传递的时候，返回值会被复制一份，所以加不加 const 都可以。































