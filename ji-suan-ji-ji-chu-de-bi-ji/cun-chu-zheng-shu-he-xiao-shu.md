# 存储整数和小数

### 如何存储整数

（正数 + 负数）

#### 为何要这么表示负数

假设有4个bit，存放的数字为：

那么11 + 1 = 100，溢出截断，又等于00；

**那对于减法是加法逆运算的特点，那么最小值减1应该为11；即00 - 1 = 11，那么自然的11应该表示十进制的-1；**

<figure><img src="../.gitbook/assets/Screen Shot 2023-06-28 at 7.51.46 PM.png" alt="" width="375"><figcaption></figcaption></figure>

#### 4bit表示的整数

<figure><img src="../.gitbook/assets/Screen Shot 2023-06-28 at 7.58.07 PM.png" alt="" width="90"><figcaption></figcaption></figure>

#### 如何写出负数的二进制

已知十进制4用0100表示，那么-4怎么表示？

1. 符号位取1 -> 1100；（**原码**）
2. 符号位以外的取反 -> 1011；（**反码**）
3. 最后一位加1 -> 1100；（**补码**）

所以-4用1100表示；

* <mark style="background-color:orange;">**所以负整数用补码来表示；**</mark>



### 如何存储小数





























