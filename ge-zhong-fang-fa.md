# 各种方法



### std::to\_string方法

将各种数字类型，变为string类型，方便遍历

|                                                                                                               |     |               |
| ------------------------------------------------------------------------------------------------------------- | --- | ------------- |
| [std::string](https://en.cppreference.com/w/cpp/string/basic\_string) to\_string( int value );                | (1) | (since C++11) |
| [std::string](https://en.cppreference.com/w/cpp/string/basic\_string) to\_string( long value );               | (2) | (since C++11) |
| [std::string](https://en.cppreference.com/w/cpp/string/basic\_string) to\_string( long long value );          | (3) | (since C++11) |
| [std::string](https://en.cppreference.com/w/cpp/string/basic\_string) to\_string( unsigned value );           | (4) | (since C++11) |
| [std::string](https://en.cppreference.com/w/cpp/string/basic\_string) to\_string( unsigned long value );      | (5) | (since C++11) |
| [std::string](https://en.cppreference.com/w/cpp/string/basic\_string) to\_string( unsigned long long value ); | (6) | (since C++11) |
| [std::string](https://en.cppreference.com/w/cpp/string/basic\_string) to\_string( float value );              | (7) | (since C++11) |
| [std::string](https://en.cppreference.com/w/cpp/string/basic\_string) to\_string( double value );             | (8) | (since C++11) |
| [std::string](https://en.cppreference.com/w/cpp/string/basic\_string) to\_string( long double value );        | (9) | (since C++11) |
|                                                                                                               |     |               |



### swap方法

可以交换两个元素；

比如：

1. 交换vector种两个元素

```cpp
vector<int> a(1,2,3,4);
swap(a[0], a[1]); // 交换前两个元素
```



### accumulate方法

累加

前两个形参必须是迭代器，第三个形参为初始值；

比如：

```cpp
#include <numeric> // accumulate在这个包下面

vector<int> nums{1,2,3,4,5,6};
int result = accumulate(nums.begin(), nums.end(), 0);
```































