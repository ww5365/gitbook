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
* c支持的可变参数：include <stdarg.h>
* 函数定义：
* int sum_int(const int len , ...) //省略号
* 利用的接口：
  va_list p;
  va_start(p,length);
  va_arg(p,参数的数据类型);
  va_end(p);
* 本质是一系列的宏定义；根据进程运行空间，参数的分布情况，计算出各个参数的地址；参数从右向左入栈，所以高地址->低地址：第n个->第1个参数；
*/
void sum_int(const int len,...){ //计算整型参数的和,长度可变

    va_list para;
    va_start(para,len); //para 指向第一可变参数的起始位置
    int para_value = va_arg(para,int);  //获取第一个int类型参数的值； 注意va_arg的第二个参数是数据类型：int

    std::cout << "param:" << 1 << ": "<<para_value <<std::endl;

    for (int i = 1 ;i < len;i++){
        para_value = va_arg(para,int);
        std::cout << "param:" << i+1 << ": "<<para_value <<std::endl;
    }
    va_end(para);
}

//vsnprintf打印va_list变量，进而能打印出可变参数,结果放在buf;

void print_msg(char *buf,const char *format,...){
    va_list va_par;
    va_start(va_par,format);
    vsnprintf(buf,256,format,va_par);  //专门格式化打印va_list这种变量类型
    va_end(va_par);
}
```

##6.4 函数返回值

定义的函数，返回值：一个指向整形数组的指针；


```c++

int (*ptr_arr)[10]; //ptr_arr是指向整形数组的指针，如何返回这种类型？

// 函数定义，返回类型特殊，让它看起来很怪
int (*fun(int len)) [10]
{
//动态分配3*10二维数组，返回第二行数组

int **ptr = new (*int)[3];

for(i=0;i<3;i++){
  ptr[i] = new int[10];
  }

return &ptr[1];  
}

//c++11 支持尾置的返回数据类型
auto fun() -> int (*) [10]
{
  ..
}


```

## 6.5 函数涉及的特殊语言特性

 > inline和宏定义，区别与联系：</br>
 > 相似点：都要执行直接替换的策略</br>
 > 不同点：</br>
 > 1、执行替换的替换阶段不同：编译 预处理</br>
 > 2、参数类型检查： 有  无
 
  
  
  
## Reference
  
1、https://github.com/ww5365/primer_v5/blob/master/src/6.cpp







