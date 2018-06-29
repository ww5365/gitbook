# c++ STL - iterator

## 一、 基本介绍

所有标准库容器都支持迭代器\(iterator\),只有少数几个容器支持下标运算符（\[\]）;

常见的迭代器类型：

```c++
vector<int>::iterator it = vec.begin();

vector<int>::const_iterator it = vec.cbegin(); //cbegin返回常量迭代器

vector<int>::reverse_iterator rit = vec.rbegin(); //反向迭代器
```

## 二、迭代器的运算

| \*it | 解引用，访问容器中it指向的元素 |
| :--- | :--- |
| it-&gt;elem | 等价于：\(\*it\).elem |
| ++it/--it | 移向迭代器it的下一个或上一个元素 |
| it1 ！= it2 | 指向同一个元素或同时指向尾后迭代器，相等；否则不相等；必须是指向同一个容器的迭代器； |
| it1 - it2 | 计算容器中元素之间的间距；返回：differece\_type, 可正，可负； |
| &gt; ,&gt;=,&lt;,&lt;= | 可以比较大小的；it1在it2之前，it1&gt;it2; |
|  |  |




## 三、迭代器的操作

```c++

next：取一下元素位置
template <class ForwardIterator>
  ForwardIterator next (ForwardIterator it,
       typename iterator_traits<ForwardIterator>::difference_type n = 1);
       //获取迭代器的下n个位置;默认n=1；

pre：取上一元素位置


distance(it1,it2)：取两个元素之间的距离 <=> (it2 - it1);返回difference_type,可正，可负；
```

图示：

![](/assets/3_1.png)


## 四、迭代器典型应用



* 二分查找迭代器版本

```c++

//查找不到，返回尾后迭代器；否则返回，查找到元素的下标迭代器；
vector<int>::iterator bin_search(vector<int> &vec, int val){

    sort(vec.begin(), vec.end(), Compare());//先排序，升序
    vector<int>::iterator start = vec.begin();
    vector<int>::iterator end = vec.end();
    while(start != end){//为空的情况也考虑进来了；
        vector<int>::iterator mid = start + (end - start)/2;//迭代器运算
        cout << "mid val: " << *mid << endl;
        if ( *mid == val){
            return mid;
        }else if(*mid > val){
            end = mid;
        }else{
            start = mid + 1;
        }
    }
    return vec.end();
}

```



