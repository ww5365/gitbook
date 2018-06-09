# 第2章 基本数据类型和变量

## 2.1 c++内置的基本数据类型

### 2.1.1 c++11 基本数据类型

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

### 2.1.2 基本数据类型最值表示

c定义头文件：`<limits.h>` `<float.h>`  
c++升级，统一到头文件：`<limits>`   使用模板类定义实现：`numeric_limits<TYPE>`

**汇总如下**：

![](/assets/2_2_1_pic1.png)

### 2.1.3 代码实例

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

* 有无符号数据类型区别代码 看：primer\_2\_1\_2
* 基本数据类型的字面值常量及转移序列， 看：primer\_2\_1\_3

## 2.2 c++ 变量

### 2.2.1 变量定义

#### 2.2.1.1 变量命名

参考：《百度C++编码规范(C++ 11更新版).pdf》参考3.3 命名/规范
局部变量：全小写，下划线分割
全局变量：全小写，下划线分割，g_开头
静态变量：全小写，下划线分割，s_开头

不能和c++的保留字重名；比如，int double = 8;
不能和c++的标准库中的名字重名：不出现两个连续下划线：比如，int __test = 10;
不能以下划线和大写字母开头：比如，int _Test = 10;

#### 2.2.1.2 变量初始化

首先，初始化 不等于 赋值
两者有区别：初始化是定义变量时给一个初值；赋值是把变量中值擦掉，重新赋值；

c++11全面支持了{}赋初始值，常见的赋初始值形式：

```c++
    //变量初始化形式
    int t1 = 10;  //常见方式
    int t2 = (10);
    int t3{10}; //c++11中得到全面应用；与下面的括号相比，丢失精度情况下，抱错，不执行;初始化列表
    int t4(10); //类对象定义初始化，经常能看到；

```

#### 2.2.1.3 变量声明和定义

声明和定义，这两个概念进行区分的原因？
c++为了支持分离式编译，即文件a中定义的变量可以在文件b中进行使用；
区别：
* 定义要申请内存空间并初始化，建立变量和值的联系；声明仅是说明变量，类型和名称；
* 变量只能一次定义；可以多处进行声明，使用关键词：extern


```c++
extern int PI; //声明了一个变量；
int pi；//声明并定义了一个变量，但未初始化；

```
topic：?
* 不赋值的变量会进行默认初始化，结合进程运行空间；知道.data和.bss段存放初始化和未初始化的全局，静态变量。












### 2.2.2 复合数据类型 