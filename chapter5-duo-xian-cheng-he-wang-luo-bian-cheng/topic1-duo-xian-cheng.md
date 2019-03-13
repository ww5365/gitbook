# 多线程

## 一、库和接口

`#include <pthread>`


pthread_t

pthread_create

pthread_join

pthread_detach

pthread_exit

pthread_self

pthread_mutex_t

pthread_mutex_lock

pthread_mutex_unlock



## pthread_t

定义线程数据类型：主要是线程id

pthread_t tids[10];

一般作为参数传入pthread_create;


## pthread_create

原型：`int pthread_create(pthread_t * restrict t, const pthread_attr_t *a, void*(*f)(void *), void * restrict fun_pram) `

返回值： 0 成功，否则出错

参数说明：
第一个参数为指向线程标识符的指针。
>pthread_t 类型的指针

第二个参数用来设置线程属性。

>pthread_attr_t a; //线程属性
>pthread_attr_init(&a);  //初始化线程属性
>pthread_attr_setdetachstate(&a, >PTHREAD_CREATE_DETACHED);//设置线程属性


第三个参数是线程运行函数的地址。

  >void* fun(void *)` : 使用桩函数的指针

最后一个参数是运行函数的参数。




实例：


``` c++
if (pthread_create(&m_threadid, NULL, ThreadRun, m_handle.get()) != 0) {
    m_started = false;
    fprintf(stderr, "Fail to %s thread", m_name.c_str());
}

这个线程创建的手法，有什么不一样？ 
把回调函数的指针作为参数，传递给桩函数；
好处？实际运行是回调函数，同时，回调函数还能在类中进行设置；因为一般桩函数都是static的独立的函数：static void* fun(void *)

```


## pthread_exit

`void pthread_exit(void *);`

在进程主函数（main()）中调用pthread_exit()，只会使主函数所在的线程（可以说是进程的主线程）退出;而如果是return，编译器将使其调用进程退出的代码（如_exit()），从而导致进程及其所有线程结束运行。

main()中调用了pthread_exit后，导致主线程提前退出，其后的exit()无法执行了，所以要到其他线程全部执行完了，整个进程才会退出。



## 





