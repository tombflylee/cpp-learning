# 数组初始化相关问题

## c++中未初始化数组的默认问题

记住几点！！！

> 1. 全局数组，未初始化时，默认值为0；
> 2. 局部数组，未初始化时，默认值为随机的不确定值；
> 3. 局部数组，初始化一部分时，未初始化部分默认值为0；

* 验证一下，看打印的返回值

```cpp
bool arr1[10];
int main() {
    bool arr2[10];
    cout << boolalpha;
    cout << arr1[0] << "\n"; // false
    cout << arr2[0] << "\n"; // true
    cout << endl;
    return 0;
}
```
