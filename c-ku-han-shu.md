# c库函数

### strlen

```
#include<cstring>
size_t strlen(const char *str)
```

C 库函数 size\_t strlen(const char \*str) 计算字符串 str 的长度，直到空结束字符，但不包括空结束字符。

* 使用例子

> 编写一个函数 int mystrcmp(const char \* src, const char \* dst)，用于比较两个字符串的大小（自己实现strcmp()函数）。要求如果字符串src大于字符串dst返回 1，小于返回 -1，相等返回 0。

```cpp
#include <iostream>
#include <cstring>
using namespace std;

int mystrcmp(const char* src, const char* dst);

int main() {

    char s1[100] = { 0 };
    char s2[100] = { 0 };

    cin.getline(s1, sizeof(s1));
    cin.getline(s2, sizeof(s2));

    int ret = mystrcmp(s1, s2);

    cout << ret << endl;

    return 0;
}

int mystrcmp(const char* src, const char* dst) {
    int count = -1;
    bool flag = true;
    int result = 0;
    int lenth1 = strlen(src);
    int lenth2 = strlen(dst);
    while(count < lenth1 || count < lenth2) {
        count++;
        if(src[count] == dst[count]) {
            continue;
        }
        else if(!src[count] && !dst[count]) {
            break;
        }
        else if(src[count] > dst[count] || !dst[count]) { 
            result = 1;
            break;
        }
        else if(dst[count] > src[count] || !src[count]) {
            result = -1;
            break;
        }
        
    }
    return result;
    // write your code here......
    

}
```

