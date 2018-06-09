# 第2章 基本数据类型和变量

## 2.1 c++11内置的基本数据类型

相比较c++98有所精简，基本数据汇总如下：

| key | 占位数 | 常量、格控 | 其它 |
| :--- | :--- | :--- | :--- |
| bool | 8bit  依赖编译器 | true; false |  |
| char | 8bit 依赖编译器转成有无符号类型； | %c                                            指定字符编码：u'a'                指定字符串编码：u''test"      转义字符：\,\',\",\?                打印%： %% | 字符串处理topic：                 1、编码转换                           2、中英文判定 |
| wchar\_t | 至少16bit; 宽字符类型；        c++11升级为基本数据类型；原来是unsigned short 的别名定义； | 宽字符：%C  L'a'                      宽字符串： %S %ls L"test"    读入打印：                             wout/wprintf                          win/wscanf | topic？为什么要增加这个基本的数据类型； |
| char16\_t | 16bit ;                                      utf-16字符类型 | utf-16的字符：u'a'                  字符串：u"test" |  |
| char32\_t | 32bit;                                       utf-32字符类型 | 字符：U'a'                                字符串： U"test" | c++11增加了对unicode编码的支持：                              可以参考：[https://blog.poxiao.me/p/unicode-character-encoding-conversion-in-cpp11/\#C++11%E5%AF%B9Unicode%E7%9A%84%E6%94%AF%E6%8C%81](https://blog.poxiao.me/p/unicode-character-encoding-conversion-in-cpp11/#C++11对Unicode的支持) |
| short | 16bit；                                  unsigned short | %d %u | uint16\_t |
| int | 32bit;                                     unsigned int | 10进制：%d %u  10, 10U       16进制：%x   0x10 | uint32\_t                                  string::size\_type                   std::size\_t |
| long | 32bit;                                      unsigned long | %l                                           %lu |  |
| long long | 64bit;                                     unsigned long long | %ll                                            %llu |  |
| float | 32bit:单精度 | %f                                           printf：%m.nf 格式控制        scanf不支持格控；              字面值常量：                         2.3e10，3.1415F |  |
| double | 64bit;双精度浮点 | %f                                           %lf | double bytes: 8                      rang:2.22507e-308~1.79769e+308                                  epsilon: 2.22045e-16           digits: 53 |
| long double | 128bit; 扩展的双精度 | %Lf |  |
|  |  |  |  |
|  |  |  |  |

## 2.2 基本数据类型最值表示

c定义头文件：`<limits.h>` `<float.h>`  
c++升级，统一到头文件：`<limits>`   使用模板类定义实现：`numeric_limits<TYPE>`

汇总如下：参考：

![](/assets/2_2_1_pic1.png)
