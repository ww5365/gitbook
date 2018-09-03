# c++ topic6 - 内存使用


## 内存释放？


类成员数据使用结构体，同时结构体中放在stl的map，set这些容器。如果使用delete作用于容器，能直接释放set，map里面的new的数据吗？

```c++
struct Node{

}

class Tree{

private:
   Node *root;
}





```


如果通过new之后，放到map容器中，