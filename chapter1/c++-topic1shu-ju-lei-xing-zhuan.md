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

> **TIPS**
>
> * 支持c++11的情况：
>   1、先使用stof得到float值；2、再使用sstringstream，设置精度读入，写出；
> * 不支持C++11： 使用C模式



