# c++ 断言机制


## 一、c/c++ assert

### 1.1 assert 说明

头文件：`#include <cassert>`
原型： `void assert(int expersion)` ;实际是宏定义

功能：
* 如果条件为true，继续执行；
* 如果为false，向stderr打印出错信息，并调用abort终止程序；【linux 程序还会抱core】


### 1.2 为什么要用断言？

* 用错误处理代码处理预期会发生的状况，用断言来处理绝不应该发生的状况；

 > 说明了使用断言的时机；

* 避免把需要执行的代码放到断言中；因为可能不会被执行，加上NDEBUG。

 > assert(cnt++ >10);//避免

* 用断言来注解并验证前条件和后条件；
 > 所以一般用校验函数的参数的合法性；

* 对于高健壮性的代码，应该先使用断言再处理错误 ；


### 1.3 实例


```c++

//实现内存拷贝
template <class T, class U> 
int bit_copy(T& a, U& b){
assert(sizeof(a) == sizeof(b));//条件不成立，终止；报cor
e
memcpy(&a, &b, sizeof(b));
}

```
### 1.4 c++11 支持的静态断言

一般我们想在编译阶段，就能定位到哪里有问题。在编译阶段能报出错误就好了。c++11提供了static_assert实现了静态断言；

```c++
template <class T, class U> 
int bit_copy(T& a, U& b){
static_assert(sizeof(a) == sizeof(b), "the parameters of bit_copy should have same width");//不成立，抱指定的错误信息；
memcpy(&a, &b, sizeof(b));
}

```

> 注意
> static_assert 不能判定变量；必须是编译期间的常量，因为是编译期间；


### 1.5 扩展 和 abort，exit区别？


abort : 
头文件 stdlib.h
功能：异常终止一个进程;

原型：void abort(void)


exit :

头文件  stdlib.h

void exit(int status)

exit()用来**正常**终结目前进程的执行,并把参数 status 返回给父进程,而进程中所有的缓冲区数据会自动写回并关闭未关闭的文件。
它并不像abort那样不做任何清理工作就退出，而是在完成所有的清理工作后才退出程序




