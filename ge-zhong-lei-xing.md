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
* `push()` : 放到deque队列**尾部**
* **`pop():` 清除头部元素**
* **`front()`: 获取第一个元素的引用**
* ~~`push_front()`: 放到deque队列的**头部**~~
* ~~`pop_back()` ：清除deque队列的**尾部**~~
* ~~`pop_front()` : 清除deque队列的**头部**~~
* `clear()`: 清除deque

```cpp
// 初始化
deque<int> p;
```

#### string类型

* compare()：与指定字符串进行区分大小写的比较，以确定两个字符串是否相等或按字典顺序一个字符串是否小于另一个。相等，返回0；大于返回正；小于返回负；
  *   适合用在下面这种情况；

      > int a = 123;
      >
      > string s = to\_string(a);
      >
      > s\[0].compare("3") > 0;// 判断是否大于3


* substr() :  从字符串起始处的指定位置复制最多某个数目的字符的子字符串。
  * > string str1 ("Heterological paradoxes are persistent.");
    >
    > basic\_string str2 = str1.substr ( 6 , 7 );  // 起始位置为6（包括6），复制7个
    >
    > cout << "The substring str1 copied is: " << str2 << endl ; // 返回logical

#### unordered\_map哈希表

> ！！注意：不是hash\_map，c++11新增了stl库中哈希表的名字为unordered\_map；！！

1. 构建一个哈希表

<pre class="language-cpp"><code class="lang-cpp">// 构建一个哈希表
unordered_map&#x3C;char,int> map;
// 设置值!!!!会覆盖；
map['c'] = 1; 
// 插入值！！！！不会覆盖
pair&#x3C;char, int> instance('c', 2);
map.insert(instance);

// 寻找某个值，返回一个迭代器！！！！first为健，这里为c；second为值，这里为1
auto j = map.find('c');
while(j != map.end()) {
<strong>    cout &#x3C;&#x3C; j->first &#x3C;&#x3C; " : " &#x3C;&#x3C; j->second &#x3C;&#x3C; endl;
</strong>    j++;
}

</code></pre>

2. 寻找一个健值

使用`find()`方法，返回一个迭代器，如果不存在这个健，则返回`unordered_map.end()`

```cpp
map.find('a') == map.end(); // 这样判断即可！！
```







