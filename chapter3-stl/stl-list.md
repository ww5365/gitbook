# c++ STL --list

## 一、基本说明

头文件`#include <list>`

list:双向链表
forward_list:单向链表

比较其它线性容器优缺点：
* 缺点：不具备vector、deque随机存取的能能力
* 优点：增、删、移动元素更高效；
> sort排序算法中，建议使用list；


## 二、常用接口和实例

### 2.1 splice 剪接（移动）

delete某个元素并insert此元素到某个位置;有点像"剪接"。

> 注意数据变化：调用链表新增加数据;被剪接的链表，要删除元素或整个链表；
> 应用场景：LRU 实现中使用splice将更新元素排到头结点；

#### 2.1.1 原型

```c++
entire list (1): 整个链表
void splice (const_iterator position, list& x);
void splice (const_iterator position, list&& x);

single element (2): 一个元素，i指向的x中元素，剪接到位置position之前
void splice (const_iterator position, list& x, const_iterator i);
void splice (const_iterator position, list&& x, const_iterator i);

element range (3): 某个范围的元素
void splice (const_iterator position, list& x,
             const_iterator first, const_iterator last);
void splice (const_iterator position, list&& x,
             const_iterator first, const_iterator last);

```


#### 2.1.2 实例

```c++

#include <iostream>
#include <list>

int main ()
{
  std::list<int> mylist1, mylist2;
  std::list<int>::iterator it;

  // set some initial values:
  for (int i=1; i<=4; ++i)
     mylist1.push_back(i);      // mylist1: 1 2 3 4

  for (int i=1; i<=3; ++i)
     mylist2.push_back(i*10);   // mylist2: 10 20 30

  it = mylist1.begin();
  ++it;                         // points to 2

  mylist1.splice (it, mylist2); // mylist1: 1 10 20 30 2 3 4
                                // mylist2 (empty)
                                // "it" still points to 2 (the 5th element)
                                          
  mylist2.splice (mylist2.begin(),mylist1, it);
                                // mylist1: 1 10 20 30 3 4
                                // mylist2: 2
                                // "it" is now invalid.
  it = mylist1.begin();
  std::advance(it,3);           // "it" points now to 30
                                //advance(it,n)迭代器走n个步长的元素        

  mylist1.splice ( mylist1.begin(), mylist1, it, mylist1.end());
                                // mylist1: 30 3 4 1 10 20
                                // 自己剪自己，it还是有效的。

  return 0;
}
```


###2.2 添加、移除首位元素


* pop_front: 移除首元素 `原型： void pop_front()`
* pop_back: 移除尾元素 `原型：void pop_back();`

* push_back: 添加元素，从尾部；
* push_front: 添加元素，在头部；


```c++
//push_back 示例

void push_back( const T& value );
void push_back( T&& value );//(C++11 起)

//1) 初始化新元素为 value 的副本。
//2) 移动 value 进新元素。右值功能？新元素，是使用原来的空间构建；用完后，原来变量值消失；

#include <list>
#include <iostream>
#include <iomanip>
 
int main()
{
    std::list<std::string> numbers;
 
    numbers.push_back("abc");
    std::string s = "def";
    numbers.push_back(std::move(s)); // 函数原型2
 
    std::cout << "list holds: ";
    for (auto&& i : numbers) std::cout << std::quoted(i) << ' ';
    //list holds: "abc" "def" 
    std::cout << "\nMoved-from string holds " << std::quoted(s) << '\n';
    //Moved-from string holds ""
}
 
   

```

#### 2.3 获取首尾元素


* 返回到容器中第一/最后一个元素的引用。

```c++

//原型：
reference front();
const_reference front() const;

reference back();
const_reference back() const;

//实例：

 std::list<char> letters {'o', 'm', 'g', 'w', 't', 'f'};    
 if (!letters.empty()) {
        std::cout << "The first character is: " << letters.front() << '\n';
  }  //输出 o
```
