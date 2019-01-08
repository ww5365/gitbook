# 位图


## 基本数据结构之一？


 每个位用1或0来表示


```c++

//头文件
#include <bitset>

std::bitset<N> foo(VAL); //N位，使用VAL初始化

//构造演示
#include <iostream>       // std::cout
#include <string>         // std::string
#include <bitset>         // std::bitset

int main ()
{
  std::bitset<16> foo; //16位，默认初始化为0
  std::bitset<16> bar (0xfa2); //16bit，使用十六进制来初始化
  std::bitset<16> baz (std::string("0101111001")); //使用字符串来初始化

  std::cout << "foo: " << foo << '\n';
  std::cout << "bar: " << bar << '\n';
  std::cout << "baz: " << baz << '\n';

  return 0;
}




```






## 位图设计初衷？应用？


