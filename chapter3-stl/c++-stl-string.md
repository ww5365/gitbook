# c++ STL - string

## 一、基本说明

字符串string，c++/c不是基本数据类型，c++通过标准库实现了string。

头文件：`#include <string>`

## 二、定义、初始化、赋值


```c++

string str1；//定义一个空串；默认构造

string str2 = str1；//拷贝构造
string str3（str1); //直接构造
string str4(10,'c'); //调用构造函数，内容是10个c
string str5(arr,arr+3);//使用数组的前3个字符构造[begin,end)？是的

string str6.assign(str1.begin(), str1.end());//赋值

```

## 三、处理字符串中每个字符

字符处理函数：`#include <cctype>`


```c++
for(auto &e:str){
   
   e = to_upper(e); //字符变大写
   
   e = to_lower(e); //字符变小写
   
   isalnum(e);//是否是字符或数字字符
   

     

}

```