# 第4章 表达式






## 4.1 基础

>对运算符更深入理解：
>1、运算符实际也可以看成函数：操作数是输入参数；左值或右值是返回值；
>2、右值：值内容；左值：数据在内存中位置；对象经运算符处理后，注意返回值是左值或右值



### 左值和右值

这个topic值得关注一下；因为左值和右值，使用decltype时，得到的结果不同；所以引出了对decltype使用的思考。

```

int *p;
decltype(*p);//得到什么类型？decltype作用于表达式且其求值结果是左值，得到值结果的引用
int x；
decltype(&x) : //表达式且是右值？定义的变量类型为？ int**；

```



#### 左值，右值理解

c++11引入右值引用，用&&表示，比如，int &&a = add(x,y);

左值:能取到其地址，可以通过地址稳定的存储数据；

右值:不能取到其地址，不稳定或中间值；比如，字面值常量，中间临时变量，函数返回值

#### 右值引用和move

A a;
std::move(a):将左值引用强制转换成右值引用。

为什么要出现右值引用？特定情况下，避免深拷贝，解决c++效率问题。比如，vec.push_back(a)就要先通过构造函数生成副本放入容器中，成本很昂贵；如果a是右值（也就是说用完就有可能消失的内存区域）我们把它保留住，直接利用原内存区域数据，放入容器，避免深拷贝；vec.emplace_back(std::move(a))就可以实现；






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


## 4.4 赋值运算符

int a = 3.14;

对这条语句你是怎么理解的？

1、赋值运算符：=  ，操作的对象是右面3.14这个对象；操作的结果是左侧的a对象，且是是一个左值；
2、类型不同时，右侧对象转成左侧对象类型；但不能是{3.14}这种初始化方式


## 4.8 位运算符

&： 位与    &=
|:  位或   |=
^:  位异或  ^=
~:  位取反 
`<<`: 左移
`>>`: 右移

说明几个点：
1、 如果操作数是：short，char 一般会自动提升为int，32bit进行操作。

  
```c++

    //检测该无符号长整型，第5 bit是否为0？
    unsigned long quiz = 17; 
    bool res = quiz & (1UL << 4); //先获取无符号字面值常量：1UL<<4 再进行与运算

    //交换两个整数数，不允许中间变量？如何实现,位运算：swap(a,b) ?

    uint16_t a = 3;
    uint16_t b = 2;

    a = a^b;
    b = a^b;//(a^b)^b ->a 赋给 b ；把a交换到b上
    a = b^a; // a ^(a^b) ->b 赋给a；把b交换到a上
  
```  


## 4.9 sizeof 运算符




## 4.11 类型转换






