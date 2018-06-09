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

**汇总如下**：

![](/assets/2_2_1_pic1.png)

## 2.3 代码实例


 * c++11模板类表示基本数据类型范围


```c++

    //boolean
    cout << "bool bytes: " << sizeof(bool) << endl;

    //字符类型
    char ch_1 = 'A';
    wchar_t wch_1 = L'w';//宽字符类型：L
    char16_t ch16_1 = u'w'; //支持unicode扩展编码，u
    char32_t ch32_1 = U'w'; //支持unicode扩展编码，U

    std::cout <<"char bytes:"  << sizeof(ch_1) << " rang:" << static_cast<int>(numeric_limits<char>::min()) << "~" << static_cast<int>(numeric_limits<char>::max()) << endl;
    std::cout << "wchar_t bytes: " << sizeof(wch_1) << " rang:" << numeric_limits<wchar_t>::min() << "~" << numeric_limits<wchar_t>::max() << endl;
    std::cout << "char16_t bytes: " << sizeof(ch16_1) << " rang:" << numeric_limits<char16_t>::min() << "~" << numeric_limits<char16_t>::max() << endl;
    std::cout << "char32_t bytes: " << sizeof(ch32_1) << " rang:" << numeric_limits<char32_t>::min() << "~" << numeric_limits<char32_t>::max() << endl;

    //unsigned short、short

    cout << "unsigned int bytes: " << sizeof(unsigned int) << " rang:"<< numeric_limits<unsigned int>::min() << "~" << numeric_limits<unsigned int>::max() << endl;
    cout << "int bytes: " << sizeof(int) << " rang:"<< numeric_limits<int>::min() << "~" << numeric_limits<int>::max() << endl;


    //unsigned int、int
    cout << "unsigned int bytes: " << sizeof(unsigned int) << " rang:"<< numeric_limits<unsigned int>::min() << "~" << numeric_limits<unsigned int>::max() << endl;
    cout << "int bytes: " << sizeof(int) << " rang:"<< numeric_limits<int>::min() << "~" << numeric_limits<int>::max() << endl;

    //long
    cout << "unsigned long bytes: " << sizeof(unsigned long) << " rang:"<< numeric_limits<unsigned long>::min() << "~" << numeric_limits<unsigned long>::max() << endl;
    cout << "long bytes: " << sizeof(long) << " rang:"<< numeric_limits<long>::min() << "~" << numeric_limits<long>::max() << endl;

    //long long
    cout << "unsigned long bytes: " << sizeof(unsigned long long) << " rang:"<< numeric_limits<unsigned long long>::min() << "~" << numeric_limits<unsigned long long>::max() << endl;
    cout << "long long bytes: " << sizeof(long long) << " rang:"<< numeric_limits<long long >::min() << "~" << numeric_limits<long long>::max() << endl;

    //float,double,long double
    cout << "float bytes: " << sizeof(float) << " rang:"<< numeric_limits<float>::min() << "~" << numeric_limits<float>::max() << " epsilon: " << numeric_limits<float>::epsilon()<< " digits: " <<numeric_limits<float>::digits << endl;
    cout << "double bytes: " << sizeof(double) << " rang:"<< numeric_limits<double>::min() << "~" << numeric_limits<double>::max() << " epsilon: " << numeric_limits<double>::epsilon()<< " digits: " <<numeric_limits<double>::digits << endl;
    cout << "long double bytes: " << sizeof(long double) << " rang:"<< numeric_limits<long double>::min() << "~" << numeric_limits<long double>::max() << " epsilon: " << numeric_limits<long double>::epsilon()<< " digits: " <<numeric_limits<long double>::digits << endl;

```

* 有无符号数据类型区别代码 看：primer_2_1_2
* 基本数据类型的字面值常量及转移序列， 看：primer_2_1_3