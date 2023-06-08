# string相关的

### 一道string的替换问题

#### 题目

<figure><img src=".gitbook/assets/Screen Shot 2023-06-05 at 3.23.10 PM.png" alt="" width="375"><figcaption></figcaption></figure>

#### 答案1

```cpp
// 答案1
class Solution {
public: 
    string replaceSpace(string s) {
        for(int i = 0; i < s.size(); i++) {
            if(s[i] == ' ') { // 1）
                s.replace(i, 1, "%20"); // 2）
            }
        }
        return s;
    }
}
```

> 1. 1）处的对比是char的对比；
> 2. 2）处的replace函数是basic\_string的；
>
>

#### 答案2

* 如果不使用`replace`这个函数，而是用数组的方式，那么需要动态改变string的长度，因为string是个容器;

```cpp
class Solution {
public: 
    string replaceSpace(string s) {
        int origin_size = s.size();
        int current_size = origin_size;
        for(auto i: s) {
            if(i == ' ') {
                current_size += 2;
            }
        }
        s.resize(current_size); // 1）
        int i = origin_size - 1;
        int j = current_size - 1;
        while(i >= 0) {
            if(s[i] != ' ') {
                s[j] = s[i];
                i--;
                j--;
            } else {
                s[j] = '0';
                s[j - 1] = '2';
                s[j - 2] = '%';
                i--;
                j -= 3;
            }
        }
        return s;
    }
};
```

> 1. 1）使用resize函数调整string的长度；这个也是basic\_string的函数；

#### basic\_string的相关函数

1. ### `basic_string::substr` <a href="#substr" id="substr"></a>

字符串复制；

> 从字符串起始处的指定位置复制最多某个数目的字符的子字符串。
>
> C++复制
>
> ```cpp
> basic_string<CharType, Traits, Allocator> substr(
>     size_type offset = 0,
>     size_type count = npos) const;
> ```
>
> #### 参数 <a href="#parameters-25" id="parameters-25"></a>
>
> _`offset`_\
> 从进行字符串复制所在的位置查找元素的索引，默认值为 0。
>
> _`count`_\
> 要复制的字符数（如果存在）。
>
> #### 返回值 <a href="#return-value-38" id="return-value-38"></a>
>
> 子字符串对象，它是由第一个参数指定的位置开头的字符串操作数元素的副本。
