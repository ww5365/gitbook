# 编译链接阶段 

##case1: duplicate symbol for architecture x86_64

一、问题原因
ld: 1 duplicate symbol for architecture x86_64 
出现错误的原因是：**重复定义**。

完整的报错信息： 
ld: 1 duplicate symbol for architecture x86_64 
clang: error: linker command failed with exit code 1 (use -v to see invocation) 
即：在链接阶段，发现“重复定义”。

问题原因： 
在.h文件中定义实现了“非内联的”“独立函数”。

这种情况下，该.h文件每被include一次，其中的“非内联的”“独立函数”都会被定义实现一次，所以就“重复定义”。 
这也是解释了：“重复定义”为什么没有在“编译阶段”报错，而是等到“链接阶段”才报错。

如果这个独立函数是内联的，由于是在被调用处直接展开，所以不会有“重复定义”的问题。

对了，所谓“独立函数”是指“不是某个类的成员方法的那些‘游离’函数”

二、解决方式
将“非内联的”“独立函数”的定义实现从.h文件挪到.cpp文件，然后在.h文件中对该函数进行声明。
--------------------- 
作者：图形跟班 
来源：CSDN 
原文：https://blog.csdn.net/libing_zeng/article/details/78362000 
版权声明：本文为博主原创文章，转载请附上博文链接！