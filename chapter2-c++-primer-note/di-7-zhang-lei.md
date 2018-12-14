# 第7章 类




## 7.1 定义抽象数据类型


### this指针和const函数

问题：常量对象或常量对象的指针，只能访问常量成员函数，为什么？

```c++
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






