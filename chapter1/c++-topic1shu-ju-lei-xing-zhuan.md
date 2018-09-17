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

## 二、 cast 显式类型转换

### 2.1 static_cast

数据转换发生阶段：编译阶段

* void指针和其它指针类型指针之间的转换；
* 不能去掉表达式中const和volatile修饰，也就是不能将上面类型的变量转换成非const/volatile类型；

```c++

    //下面是正确的用法
    int m = 100;
    Complex c(12.5, 23.8);
    long n = static_cast<long>(m);  //宽转换，没有信息丢失
    char ch = static_cast<char>(m);  //窄转换，可能会丢失信息
    int *p1 = static_cast<int*>( malloc(10 * sizeof(int)) );//将void指针转换为具体类型指针
    void *p2 = static_cast<void*>(p1);  //将具体类型指针，转换为void指针
    double real= static_cast<double>(c);  //调用类型转换函数
   
    //下面的用法是错误的
    float *p3 = static_cast<float*>(p1);  //不能在两个具体类型的指针之间进行转换
    p3 = static_cast<float*>(0X2DF9);  //不能将整数转换为指针类型

```


###2.2 const_cast


对于const/volatile变量，要转成非const/volatile怎么办？ 使用const_cast,改变变量的属性。

典型应用场景：函数重载？

```c++
const string& fun(const string& str1, const string& str2){

    return str1.size() < str2.size() ? str1: str2;
    //返回长度小的字符串；但如果传入参数是两个非const的string，返回的是const的引用
    //这种情况，如何返回非const的引用? 重载函数
}

string& fun(string&str1, string& str2){

    const string &result = fun(const_cast<const string&>(str1), const_cast<const string&>(str2));
    //这样用是安全的，string& -> const string&

    return const_cast<string&>(result);
}


```

### 2.3 reinterpret_cast

对二进制位重新解释；认为是对static_cast的补充，可以实现下面的转换：

* int -》 指针
* 具体的不同类型的指针之间的转换


```c++

    //将 char* 转换为 float*, 这样挺危险
    char str[]="http://c.biancheng.net";
    float *p1 = reinterpret_cast<float*>(str);
    cout<<*p1<<endl;
    //将 int 转换为 int*
    int *p = reinterpret_cast<int*>(100);
    //将 A* 转换为 int* ，可以访问到类A中第一个private成员，假设也是int;这样直接破坏了封装性
    p = reinterpret_cast<int*>(new A(25, 96));
    cout<<*p<<endl;


```


### 2.4 dynamic_cast

RTTI：run time type identifier

转换的时机：运行期间
只能针对：指针类型和引用类型；
要求： 同基类，继承类；基类中有虚函数；

* 向上转换 (子类-》父类)


```c++

derived *ptr = new derived();//安全
base *b_ptr = dynamic_cast<base*>(ptr);

```

* 向下转换 (父类指针 -》 子类)

是否安全，要看父类指针原本指向？父类指针就是父类对象，不安全；父类指针实际指向子类的对象，转换安全；


``` c++

    template<typename ResourceType>
    ResourceType* GetCastResource(const std::string& resource_name) {
        Resource* resource = GetResource(resource_name);//resource父类指针指向子类对象
        if (NULL == resource) {
            return NULL;
        }

        return dynamic_cast<ResourceType*>(resource);//返回想要的子类对象指针
    }
    
    
    

```



