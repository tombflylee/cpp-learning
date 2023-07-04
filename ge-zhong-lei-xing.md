# 各种类型

### 数值类型

1. 打印保留小数点

```cpp
#include<iostream>
#include<iomanip>
int main() {
    double a = 1.22323;
    cout << fixed << setprecision(3) << a << endl;
}
```

### vector

* `size()`: 返回vector中的元素数量

### stack栈

* `void push` 方法入栈；
* `void pop` 方法从**顶部**出栈；
* `reference top();` 返回顶部元素；
* `empty()` 方法判断是否为空

### queue队列

* `reference front()` : 返回对 queue 中第一个元素的引用。
* `push()` : 放到deque队列**尾部**
* **`pop():` 清除头部元素**
* **`front()`: 获取第一个元素的引用**
* `clear()`: 清除queue

```cpp
// 初始化
queue<int> p;
```

### deque双端队列

### string类型

* compare()：与指定字符串进行区分大小写的比较，以确定两个字符串是否相等或按字典顺序一个字符串是否小于另一个。相等，返回0；大于返回正；小于返回负；
  *   适合用在下面这种情况；

      > int a = 123;
      >
      > string s = to\_string(a);
      >
      > s\[0].compare("3") > 0;// 判断是否大于3


* substr() :  从字符串起始处的指定位置复制最多某个数目的字符的子字符串。
  *   > string str1 ("Heterological paradoxes are persistent.");
      >
      > basic\_string str2 = str1.substr ( 6 , 7 );  // 起始位置为6（包括6），复制7个
      >
      > cout << "The substring str1 copied is: " << str2 << endl ; // 返回logical



| isalpha() | 判断字符是否是字母（'a'-'z' 'A'-'Z'） |
| :-------: | :------------------------: |
| isdigit() |          判断字符是否是数字         |
| isspace() |    判断字符是否是空格、制表符、换行等标准空白   |
| isalnum() |        判断字符是否是字母或者数字       |
| ispunct() |          判断字符是标点符号         |
| islower() |    判断字符是否是小写字母（'a'-'z'）    |
| isupper() |    判断字符是否是大写字母（'A'-'Z'）    |

{% code title="" %}
```cpp
// 统计这句话中字母字符、数字字符、空白、标点符号和其它字符的个数
#include <iostream>
#include <string>

using namespace std;

int main() {

    string str;
    getline(cin, str);

    int whitespace = 0;
    int digits = 0;
    int chars = 0;
    int others = 0;

    // write your code here......
    for(int i =0; i < str.size(); i++) {
        if(isalpha(str[i])) {
            chars++;
        } else if(isspace(str[i])) {
            whitespace++;
        } else if(isdigit(str[i])) {
            digits++;
        } else {
            others++;
        }
    }
    

    cout << "chars : " << chars
        << " whitespace : " << whitespace
        << " digits : " << digits
        << " others : " << others << endl;

    return 0;
}
```
{% endcode %}

### unordered\_map哈希表

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



### char&#x20;

* 对于char类型，不能单独用长度循环来遍历，因为会有结束符号；

{% code title="这种方式不好" %}
```cpp
char str[100] = { 0 };
cin.getline(str, sizeof(str));
int length = strlen(str);
for(int i = 0; i < length; i++) {} // 不好
```
{% endcode %}

{% code title="这种比较好" %}
```cpp
char str[100] = { 0 };
cin.getline(str, sizeof(str));
int length = strlen(str);
for(int i = 0; str[i] != '\0'; i++) {}
```
{% endcode %}













