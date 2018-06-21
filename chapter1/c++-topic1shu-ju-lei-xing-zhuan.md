# c++ topic1 - 数据类型转换

## 一、字符串和number之间转换

### 1.1 string to number

比如，"123.456" -&gt; 123.46，代码示例：

```c++
void string_to_number(){

    /*
     * @brief string转换成number;并保留两位小数；
     *
     * IO 方式实现：c++ c
     *
     * eg:   str1     -> value
     *     "12.3456"  -> 12.35
     */

    std::string str1 = "12.3456";
    float value = 0;

    //C++ IO: sstream
    std::stringstream ss;
    ss << str1; //将str变量的值设置进字符串输入流中；
    ss >> value; //完成字符串转换成float；

    // 处理小数点的精度
    //ss.str("");
    ss.clear();
    ss.precision(2);
    ss.setf(std::ios::fixed); //固定小数显示；2位小数；不设置的话，是2个有效数字；
    ss << value;  //value是float类型，所以按照设置的精度读入；
    ss >> value;   //把保留两位小数的字符流，再输出到float变量

    std::cout << "str to float: " << value << std::endl;

    //C IO: snprintf sscanf   ***推荐***
    value = 0;
    sscanf(str1.c_str(), "%f", &value); //将str格式化读入变量value = 12.3456
    char *buff = new char[str1.size() + 1];
    snprintf (buff, sizeof(buff), "%.2f", value); //将变量格式化读入buff
    sscanf(buff, "%f", &value); //再次读入到value=12.35
    printf("str to float: %f\n", value);
    delete []buff;
    buff = nullptr;


    /*
     * @brief 使用库函数的方式实现
     *
     * C++ 11: <string>
     *
     * float stof(const string &str, size_t *idx=0); //将str转成float，第一个不合法字符的下一个位置idx返回，同时返回float；
     * stoi
     * stol
     * stod
     * stoll
     *
     *
     * C : <stdlib.h>
     *
     * atoi，atol, atof,atod,atoll;
     *
     * long strtol(const char*, char** end, int base); //base是进制10,16,8； end返回第一个不合法字符下一个位置；
     * strtod
     * strtoll
     *
     */

    value = std::stof(str1); //建议使用c++;但c++11才支持
    std::cout << "c++ string stof: " << value << std::endl;

    value = std::atof(str1.c_str()); //c库
    std::cout << "c string atof: " << value << std::endl;

}
```

> **Tips**
>
> * 支持c++11的情况：
>   1、先使用stof得到float值；2、再使用sstringstream，设置精度读入，写出；
> * 不支持C++11： 使用C模式

### 1.2 number to string

比如将：12.345 -&gt; "12.345" ,代码示例:

```c++
void number_to_string(){
    float value = 12.3456;
    std::string str2;
    //C++ IO 方式
    std::stringstream ss;
    ss << value;
    str2 = ss.str(); //将字符流中的string赋值给str2；
    std::cout << "number to str C++ IO: " << str2 << std::endl;
    str2.clear();

    //C IO方式
    char buff[32];
    memset(buff, 0 , 32);//支持最长转换成最长31位
    snprintf(buff, sizeof(buff), "%f", value);
    str2 = buff;
    std::cout << "number to str C IO: " << str2 << std::endl;
    str2.clear();

    //C++库函数: to_string(),可以把各种类型转换成string
    str2 = std::to_string(value);
    std::cout << "number to str C++ lib: " << str2 << std::endl;
    str2.clear();

    //C库函数：itoa 不建议使用了

}
```

> **Tips**
>
> * 支持：c++11 to\_str\(\) 一个函数搞定
> * 不支持的话：使用C/C++的IO方式

### 1.3 number 和 string转换总结

#### 1.3.1 C++ 模式的转换

![](/assets/1_3_1_pic1.png)

#### 1.3.2 C 模式的转换

![](/assets/1_3_2_pic1.png)

## 二、 cast 的类型转换

### 2.1 cast 类型转换总结&区别



