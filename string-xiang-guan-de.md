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
