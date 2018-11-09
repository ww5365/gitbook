# c++ - topic5 - 智能指针

## 一、c++ 11支持的智能指针

```
头文件:
#include <memeory>
```

| STD库 | 说明 | boost库 |
| :--- | :--- | :--- |
| auto\_ptr | c++11废弃 |  |
| shared\_ptr | 共享指针 | shared\_ptr |
| unique\_ptr | 独占指针 | scoped\_ptr |
| weak\_ptr |  |  |


也就是说，boost库中早就有智能指针；c++11引入进来；

```c++
//使用

shared_ptr<string> sp(new string("test")); //必须显示初始化智能指针



```

## 二、智能指针的设计思想

2.1 为什么要有智能指针？

用户通过malloc/free，new/delete 进行动态的内存分配和回收；但是，避免不了的会发生new完之后，没有delete，造成内存泄露的情况，比如，函数出异常提前return，或者就是忘记delete了，或者容器中装了new出来的数据只用clear是不行的，等等；实际项目中，也出现过类似情况：实现实时库，使用buff设计，加载最新的索引文件时，出现异常，函数提前返回，未释放内存，造成大量的内存泄露；

所以希望，动态分配完一片内存后，自动回收指针指向的那片内存；避免造成内存泄露；所以库提供了智能指针模板类，来帮助实现这一功能；

注意：智能指针管理的范畴，必须是heap区，动态内存分配，如下情况是不能使用的:

```c++

string vacation("I wandered lonely as a cloud.");
shared_ptr<string> pvac(&vacation);   //not allowed ,why? stack memory

```

2.2 为什么设计不同类型的智能指针？

主要使用的两种类型的智能指针：shared_ptr,unique_ptr;为什么有不同类型？多个指针可以指向同一个对象，但对象只能delete一次;怎么控制被多次释放，就形成不同的类型智能指针；

shared_ptr:是通过计数器来实现delete；当引用计数器为0时，才释放内存；

unique_ptr:是通过转移控制权来实现只能"主"指针才能释放内存；比如，ptr2 = ptr1，那么控制权就由ptr1转移到ptr2上，ptr1消失(函数返回的临时值，这样是好的，编译不报错)，或者悬空(不好的，编译报错)；只有ptr2才能释放；





## 参考

1、[http://www.cnblogs.com/lanxuezaipiao/p/4132096.html](http://www.cnblogs.com/lanxuezaipiao/p/4132096.html)

