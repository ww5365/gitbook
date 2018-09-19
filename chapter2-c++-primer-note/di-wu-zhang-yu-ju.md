# 第5章 语句


## 5.4 迭代语句

while
for通用形式
do while 

这三种循环语句，以前都有接触；c++11新增加了范围for语句，可以重点了解下使用；

### 范围for语句

`for(declaration:expression)`

* expression必须是一个序列： 使用花括号初始化，数组，vector， string 等；也就说这种类型有迭代器：begin和end
* declaration: 序列中的元素类型，也可以用auto；如果需要修改expression中的内容，使用引用。 


```c++
vetor<int> v = {1,2,3,4};
for(auto &e:v){
   e = 2*e;//每个元素都乘以2
}
```


## 5.5 跳转语句

break
continue
return
goto

### goto语句

主要关注了LABLE的命名规则；它和变量不是一个体系，可以和变量重名；

```c++

goto LABLE;

LABLE:  //label独立于变量命名和其它标识符的命名；也就是说可以和变量名相同
  do something statement;

```


## 5.6 异常处理语句

常用的异常处理：

#include<>
std::runtime_error


```c++


try{
  if(ture){
     cout << "some exception" << endl;
     throw std::runtime_error("wangwei runtime error test"); //使用throw 直接抛出特定的异常
  }
}catch(){
}catch(){
}catch(...){
}


```

