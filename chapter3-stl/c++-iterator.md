# c++ STL - iterator

## 一、 基本介绍

所有标准库容器都支持迭代器\(iterator\),只有少数几个容器支持下标运算符（\[\]）;

常见的迭代器类型：

```c++
vector<int>::iterator it = vec.begin();

vector<int>::const_iterator it = vec.cbegin(); //cbegin返回常量迭代器

vector<int>::reverse_iterator rit = vec.rbegin(); //反向迭代器
```

## 二、迭代器的运算

| \*it | 解引用，访问容器中it指向的元素 |
| :--- | :--- |
| it-&gt;elem | 等价于：\(\*it\).elem |
| ++it/--it | 移向迭代器it的下一个或上一个元素 |
| it1 ！= it2 | 指向同一个元素或同时指向尾后迭代器，相等；否则不相等；必须是指向同一个容器的迭代器； |
| it1-it2 |  |



