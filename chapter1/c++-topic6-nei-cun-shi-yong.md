# c++ topic6 - 内存使用


## 内存释放？


类成员数据使用结构体，同时结构体中放在stl的map，set这些容器。如果使用delete作用于容器，能直接释放set，map里面的new的数据吗？

```c++
struct Node{
        std::set<DistrictInfo> datas;
        std::map<uint16_t, TrieNode*> next;
        bool leaf;
}

class Tree{
private:
   Node *root;
}

//释放树中节点时，Node里面的set和map中的数据释放吗？
delete root;

```


如果new数据放在map容器中，如何释放new过的数据？直接clear。。？