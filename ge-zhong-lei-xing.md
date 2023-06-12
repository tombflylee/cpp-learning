# 各种类型

#### vector

* `size()`: 返回vector中的元素数量

#### stack栈

* `void push` 方法入栈；
* `void pop` 方法从**顶部**出栈；
* `reference top();` 返回顶部元素；
* `empty()` 方法判断是否为空

#### deque队列

* `reference front()` : 返回对 `deque` 中第一个元素的引用。
* `push_back()` : 放到deque队列**尾部**
* `push_front()`: 放到deque队列的**头部**
* `pop_back()` ：清除deque队列的**尾部**
* `pop_front()` : 清除deque队列的**头部**
* `clear()`: 清除deque

#### string类型

* compare()：与指定字符串进行区分大小写的比较，以确定两个字符串是否相等或按字典顺序一个字符串是否小于另一个。相等，返回0；大于返回正；小于返回负；
  *   适合用在下面这种情况；

      > int a = 123;
      >
      > string s = to\_string(a);
      >
      > s\[0].compare("3") > 0;// 判断是否大于3
