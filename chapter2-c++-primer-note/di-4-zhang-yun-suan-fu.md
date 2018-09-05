# 第4章运算符






## 4.1 基础

>对运算符更深入理解：
>1、运算符实际也可以看成函数：操作数是输入参数；左值或右值是返回值；
>2、右值：值内容；左值：数据在内存中位置；对象经运算符处理后，注意返回值是左值或右值



### 左值和右值

这个topic值得关注一下；因为左值和右值，使用decltype时，得到的结果不同；所以引出了对decltype使用的思考，如下。


#### decltype 

##### 基本说明

功能：计算一个变量的数据类型。不要值，只要数据类型；实际应用不多，代码中不常见。

关键字和运算符区别：？
1、decltype是关键字

2、运算符可以看做类内部成员函数，可以重载；关键字不可以。。

decltype 和 auto 区别：？

1、decltype与auto关键字一样，用于进行**编译时**类型推导。
2、类型推导：auto是从变量声明的初始化表达式获得变量的类型；decltype是以一个普通表达式作为参数，返回该表达式的类型,而且并不会对表达式进行求值。

##### 应用场景

* 重用匿名类型

```c++
struct{
    int a;
    double b;
} anon_s; //变量anon_s

decltype(anon_s) anon_s_other;//重新使用了没有名称结构体类型，定义变量

```

* 泛型编程结合auto，追踪函数的返回值类型

```c++
/*
  ** decltype最典型的应用场景 **
*/
template <typename _Tx, typename _Ty>
auto multiply(_Tx x, _Ty y)->decltype(x*y)
{
    return x*y;
}


/*
In C++11, there are two syntaxes for function declaration:
return-type identifier ( argument-declarations... )
and
auto identifier ( argument-declarations... ) -> return_type
这种函数定义方式也找到应用场景了，为什么这样定义？
参考：https://stackoverflow.com/questions/22514855/arrow-operator-in-function-heading
*/

```

##### 参考：
1、decltype介绍，参考：https://www.cnblogs.com/QG-whz/p/4952980.html




## 4.2 算术运算符

### 求模运算

* 如何取值？

余数的定义：a = b*q + r (q=a/b,b!=0,|r|< |a|)

`-17%10=?  10*(-1) + (-7) 或者 10*(-2) + 3`  也就说，余数可能为-7或+3

C++ 中最终取了哪个值呢？ 使用q=a/b采用truncate方式，直接不要小数点后面的值；也就是q=-1，那么最终的值是：-7

* 求模运算额外要求？

 a%b: a,b需要为整数








