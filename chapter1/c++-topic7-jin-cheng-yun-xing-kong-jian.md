# topic7 - 进程运行空间分析


## 7.1 进程运行空间
程序编译链接成功后，要运行；由自己的虚地址空间，映射到物理地址空间进行运行；
可执行文件的虚地址空间，也就是进程运行空间，是怎么划分的？

linux-64bit机器为例：

![](/assets/1_7_1.jpg)


* 地址64bit,标识范围：0x0000000000000000 ~ 0xFFFFFFFFFFFFFFFF

* text segment: 代码段
二进制代码；从虚拟内存地址00400000开始，这个地址是固定的。使用pmap PID可以查看到；

* data segment:
存放已经初始化的全局变量，静态变量

* BSS segment：
未初始化的全局变量，会初始化默认值；

* heap 段：
c++动态内存分配运算符new,delete
c动态内存分配函数：malloc alloc  free


* Memeory mapping region:
**mmap系统调用可将文件**映射入进程memory map地址空间；
使用ldd命令，我们可以看到进程依赖的库文件，这些库文件编译过程中都要关联到此虚拟地址空间；

* stack 段：
函数局部变量，函数调用等都保存在stack区，地址由高到低的分配内存；

* 使用pmap PID 或 cat /proc/PID/maps 查看进程空间

![](/assets/1_7_2.png)


## 7.2 代码汇编后实例分析运行空间


## 7.3 函数调用运行进制


## 7.4 常用汇编命令及寄存器


## 7.5 代码函数debug调试
