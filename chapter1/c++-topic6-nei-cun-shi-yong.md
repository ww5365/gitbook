# c++ topic6 - 内存使用


## 内存释放？


类成员数据使用结构体，同时结构体中使用了stl的map，set这些容器。如果使用delete直接释放类成员的结构体数据，set，map里面的数据会被自动释放掉吗？

```c++
struct Node{

}



```


如果通过new之后，放到map容器中，