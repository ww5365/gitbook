# singlton 模式

## 什么是单例模式？

理解就是：整个程序中，即使在多线程的运行环境中，也只有一个运行的类对象实例；

这样设计的目的：多线程的情况下，可以拿到同一份数据；


## 项目中见到的单例


``` C++

class DataCenter {
public:
    int Init(const global_conf_t& g_conf);

    // Typical singlton design using double-check.
    static DataCenter& Instance() {
        if (!m_is_instance_created) {
            utility::MutexGuard mutex_guard(&m_mutex);
            if (!m_is_instance_created) {
                static DataCenter data_center;
                m_instance = &data_center;
                m_is_instance_created = true;
            }
        }
        return *m_instance;
    }
    
private:

    // Data center implementation.
    boost::scoped_ptr<DataCenterImpl> m_data_center_pimpl;
    static utility::Mutex m_mutex;
    static bool m_is_instance_created;
    static DataCenter* m_instance;

    // uncopyable
    DataCenter(const DataCenter&);
    void operator=(const DataCenter&);
};




```

