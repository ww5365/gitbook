# c++ 正则表达式

## 一、c++11 对正则表达式的支持

regex:regular expression

头文件：`#include<regex>`

### 1.1 代码


> 代码实现解决的问题：匹配以『beijing』开头的所有字符串

```c++
void string_match_way(){

    std::vector<string> test;
    test.push_back("bei hai1");
    test.push_back("beijing university");
    test.push_back("beijing人民");
    /*
    * std::regex 定义模式匹配的正则表达式；使用字符串初始化
    */
    std::regex pattern("beijing.*");//.匹配任意字符；*匹配之前出现的>=0个字符
    std::regex pattern2("[A-Za-z0-9 ]+");//字母，数字，空格
    for (auto it = test.begin();it != test.end(); it++){

        if (std::regex_match(*it, pattern)){//参数1：要匹配的字符串 参数2：通配模式
            std::cout << "match pattern: " << *it << std::endl;
        }
        if (std::regex_match(*it, pattern2)){
            std::cout << "match pattern2: " << *it << std::endl;
        }
        //模式匹配成功，将匹配成功的字符串全部替换成replace，并返回新串;未成功，直接返回待匹配的字符串；
        std::string replace_str = "good person";
        string new_str = std::regex_replace( *it, pattern, replace_str);//参数3：如果匹配成功，要替换成的字符串；
        std::cout << "repalce: " << new_str << std::endl;
    }//end for


}



```