#c++ STL - iterator

## 一、 基本介绍

所有标准库容器都支持迭代器(iterator),只有少数几个容器支持下标运算符（[]）;

常见的迭代器类型：

```c++
vector<int>::iterator it = vec.begin();

vector<int>::const_iterator it = vec.cbegin(); //cbegin返回常量迭代器

vector<int>::reverse_iterator rit = vec.rbegin(); //反向迭代器

```

## 二、迭代器的运算

