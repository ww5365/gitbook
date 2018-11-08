# topic2 - 多线程join和detach


> 主工作线程，一开始就使用:ul_pthread_detach(ul_pthread_self()),这个是为何？

先给结论：
在工作线程函数头加上 pthread_detach(pthread_self())，被创建的工作线程状态改变unjoinable，在pthread_exit线程退出时，回收被线程占用的资源(8K);


原因分析：
Linux系统中程序的线程资源是有限的，表现为能同时运行的线程数是有限的。而默认的条件下，一个线程结束后，其对应的资源不会被释放；可能造成，线程创建形式的"内存泄露";

释放线程占用资源(**堆栈和线程描述符**)的方法：

* detach

创建线程时，把子线程设置成detach属性,子线程分离于主线程,不阻塞主线程；
或者在子线程函数开始处使用pthread_detach(pthread_self())；
将子线程变为unjoinable状态，确保子线程pthread_exit或退出时，资源自动释放;

```c++

pthread_t t;
pthread_attr_t a; //线程属性
pthread_attr_init(&a);  //初始化线程属性
pthread_attr_setdetachstate(&a, PTHREAD_CREATE_DETACHED);//设置线程属性
pthread_create( &t, &a, Stub, NULL);//建立线程

```


* join

```c++

pthread_t t;
pthread_create( NULL, NULL, Stub, NULL);
pthread_join(t);//主线程等待线程t退出，并释放t线程所占用的资源

```

调用pthread_join()后，如果该线程没有运行结束，调用者会被阻塞。有些情况下我们并不希望如此，比如在Web服务器中当主线程为每个新来的链接创建一个子线程进行处理的时候，主线程并不希望因为调用pthread_join而阻塞，因为还要继续处理之后到来的链接，所以使用pthread_detach(pthread_self()) 
或者父线程调用pthread_detach(thread_id)（非阻塞，可立即返回），是较好选择；


回到sug-as源码：
子线程中使用了：detach 同时主线程中又使用:join ，怎么理解？ 会报错？但没有报错可能是因为是使用了ul库中ul_pthread_detach。但终究有功能重复；

可以考虑去掉：ul_pthread_detach(ul_pthread_self()) ？ 

再次理解： 子线程中detach是为了让主线程继续

