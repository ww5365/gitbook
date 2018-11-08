# 多线程

## 一、库和接口

`#include <pthread>`


pthread_t

pthread_create

pthread_join

pthread_detach

pthread_exit

pthread_mutex_t

pthread_mutex_lock

pthread_mutex_unlock



## pthread_exit

`void pthread_exit(void *);`

在进程主函数（main()）中调用pthread_exit()，只会使主函数所在的线程（可以说是进程的主线程）退出;而如果是return，编译器将使其调用进程退出的代码（如_exit()），从而导致进程及其所有线程结束运行。

main()中调用了pthread_exit后，导致主线程提前退出，其后的exit()无法执行了，所以要到其他线程全部执行完了，整个进程才会退出。






