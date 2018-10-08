# 第六章 函数




## 6.1 函数基础

谈到函数，首先就想到：进程运行空间和函数调用原理，所以重新整理了《topic7 - 进程运行空间分析》；通过汇编代码，我们看到了函数调用，函数返回，所涉及的动作，也了解到了函数递归栈的使用；

记住，函数调用栈：bp,sp...



## 6.2 参数传递

由函数调用栈分析知道，超过6个参数，会把参数压栈；前6个放在寄存器；



### 6.3 可变参数

在实际的开发过程中，自己实现可变参数的函数，这种情况还是比较少。见过宏定义实现可变参数的例子；


```c++

/*
* c++11 新增加：
* 头文件：initializer_list
* 调用：
* error_msg(code,{"this", "error1"});
* error_msg(code,{"this", "error1", "error2"});
*/

void error_msg(int &err_code, std::initializer_list<std::string> para){

    //initializer_list 是模板类
    for(auto it = para.begin(); it != para.end(); it++){
        std::cout << "para: " << *it << std::endl;
    }

    //这个类支持迭代器，所以也可以用范围for
    for(auto &e: para){
        std::cout << "para2: " << e << std::endl;
    }
    err_code = 0;
}

/*
* c支持的可变参数：include<stdarg.h>
* 函数定义：
* int sum_int(const int len , ...) //省略号
* 使用


*/

可变参数的

怎么使用可变的参数？



```



