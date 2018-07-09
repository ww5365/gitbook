# c++ - topic4 -const constexpr 区别


> 个人总结：
>


## 一、constexpr



* c++11增加的关键字，常量表达式,强约束
* 编译期其值就必须确认; 目的：**效率**，因为代码在编译器就进行优化；

* 使用对象： 基本数据类型、指针、引用，类构造函数(产出常量表达式对象)
* 应用场合：数组长度，enum，switch 等




##二、const 


### 2.1 const 语义

 const保证的是对象的常量性，是：物理常量性，不是逻辑常量性


``` c++
//代码说明，物理、逻辑常量

class CTextBlock { 
public: 
    ... 
    std::size_t length() const{//调用完后，lengthIsValid是有可能发生变化的，但const不是保证逻辑常量性，只保证物理常量行，各数据位不能变化，所以lengthIsValid是无法更改的；使用mutable来打破一些成员变量的常量性，即使是const函数，也可以修改成员变量；
    
     lengthIsValid = true; //没有mutable 
    }
private: 
    char *pText; 
    std::size_t textLength;            // last calculated length of textblock 
    mutable bool lengthIsValid;                // whether length is currently valid ，增加mutable来打破const限制 
};


```


### 2.2 修饰变量，指针，引用

* 修饰的变量：必须初始化时赋初值
* 初始值，可以编译阶段确定也可以运行阶段确定；（和constexpr不一样）


```c++
//

const int *ptr[10]; //ptr是数组，保存10个指针，指向整型常量
int * const ptr[10]; //ptr是数组名，保存10个常量指针，指向非常量整型
const int (*ptr)[10];//ptr是指针，指向含有10个整型常量的数组

const int &ref；//const引用则是const Type * const指针

//去掉const性质？ 非const函数调用const函数；

int &A::operator[](int i) {
    return const_cast<int &>(static_cast<const A &>(*this).operator[](i)); //先加上const，使其能调用到const函数；再去掉const特性；
}


```


### 2.3 类中const



const 成员变量：static 和 非static

* 非static： 初始化列表中进行初始化
* static：类内生命；类外初始化；


const 成员函数：
* this指针是双const的；
* 对成员变量赋值，调用非const函数，调用非const方法，都是不允许的；

```c++
class B {

private:
const string name;
static const int grade;

public:

B():name("yizhong"){
  name = "yizhong";//error
  }
string getName() const{
   return this->name;//this name的值不能修改
  }  
  
}

const int B::grade = 5;


```














## 参考

1、 https://www.cnblogs.com/fuzhe1989/p/3554345.html

