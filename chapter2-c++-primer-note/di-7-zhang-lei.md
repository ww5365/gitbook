# 第7章 类




## 7.1 定义抽象数据类型


### this指针和const函数

问题：常量对象或常量对象的指针，只能访问常量成员函数，为什么？


``` c++

class  Sales_data{
private:
    std::string isbn;
    double revenue;
    unsigned int units_sold;
public:
    Sales_data():isbn(""),revenue(0.0),units_sold(0){}
    //非常量函数，不能通过常量对量或指针访问？
    void addCount(){
        units_sold ++;
    }
    //const常量函数
    unsigned int getCount() const{
        return units_sold;
    }
};

const Sales_data sa;
sa.addCount();//报错
sa.getCount();// 常量成员函数，ok

```

解答：

1、常规理解：因为是常量对象或指向常量对象的指针，那么对象本身内容是不能被改变的；如果访问非const的成员函数，是有可能改变对象本身内容的；

2、深入理解：
* 每个对象有隐含的指向自身的this指针，对象隐式的通过this来访问数据成员，类型：TYPE *const this：这是指向非常常量的常量指针；
* 如果对象自身是const的，这个隐含的指针还是指向非常量对象的，会造成类型不匹配了。
* 所以怎么把this变成：const TYPE *const this这种类型？
* 通过成员函数最后加上const，把this申明为指向const对象的指针，对象就可以通过this来访问数据成员了；
* 没有申明为const的成员函数，是不能被对象调用的；

总结：为了保持类的兼容性，能申明为const成员函数的，就尽量声明为const；保证类的const对象，尽可能多的访问成员函数；



## 构造函数


constructor function 有什么特征？
* 函数名和类名同名
* 无返回值，只有>=0个参数
* 主要的目的是初始化类中成员变量的初始值；

同是构造函数有什么不一样？
* 合成的默认构造函数： 类中并没有定义任何构造函数，编译器会自动生成一个默认的构造函数；
* 默认构造函数：输入参数=0个；



```c++

//下面是一个默认构造函数；同时使用默认值和初始化列表，进行初始化；
Sales_data():isbn(""),revenue(0.0),units_sold(0){}


```

