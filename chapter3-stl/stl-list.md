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

#### 2.1.1 原型

```c++
entire list (1) : 整个链表
void splice (const_iterator position, list& x);
void splice (const_iterator position, list&& x);

single element (2)	: 一个元素剪接到位置position之前
void splice (const_iterator position, list& x, const_iterator i);
void splice (const_iterator position, list&& x, const_iterator i);

element range (3)	 : 某个范围的元素
void splice (const_iterator position, list& x,
             const_iterator first, const_iterator last);
void splice (const_iterator position, list&& x,
             const_iterator first, const_iterator last);

```