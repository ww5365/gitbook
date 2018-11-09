# topic3 - __thread关键字

> __thread 什么作用？在sug-as项目中发现使用了此关键字修饰变量

``` c++
__thread SugAsServer *sug_as_server = NULL;
//使sug_as_server全局变量，每个线程都有一个局部值，多线程间互不影响；
//全部的文件中，分割开的函数中，都可以使用全局变量sug_as_server；

```

* __thread说明：

__thread是一个非常有用的关键子，在多线程编程中，如果使用__thread关键字修饰global变量，可以使得这个变量在每个线程都私有一份。用来修饰那些带有全局性且值可能变，但是又不值得用全局变量保护的变量；也就是：线程局部变量；使用不当容易内存泄露；

* __thread使用规则：

1. 只能修饰POD类型(类似整型指针的标量，不带自定义的构造、拷贝、赋值、析构的类型，二进制内容可以任意复制memset,memcpy,且内容可以复原)；基本数据类型都ok，指针，结构体也ok。
2. 只能初始化为编译器常量(值在编译器就可以确定const int i=5,运行期常量是运行初始化后不再改变const int i=rand()).
3. 不能修饰class类型，因为无法自动调用构造函数和析构函数.
4. 可以用于修饰全局变量，函数内的静态变量，不能修饰函数的局部变量或者class的普通成员变量;

```c++
    __thread std::string t_object_1 ("test");// 错误，因为不能调用对象的构造函数
    __thread std::string* t_object_2 = new std::string (); // 错误，初始化必须用编译期常量
    __thread std::string* t_object_3 = nullptr; // 正确，但是需要手工初始化并销毁对象

```

这样也可以解释：为什么SugAsServer类中，private成员都是指针类型。


好吧，又引入了POD的概念？plain old data

参考：
http://www.cnblogs.com/zhangzhang/archive/2013/01/06/2847570.html