# c++ STL - set


> 1、set是一个容器
> 2、set是集合，具备去重功能；结构体多个元素相同才算重复的判断，如何实现？重载`operator<`,如何理解？


## 代码赏析

``` c++

struct DistrictInfo
{
    uint32_t cid;
    uint32_t level;
    DistrictInfo(uint32_t cid_, uint32_t level_):
        cid(cid_), level(level_){}

    bool operator< (const DistrictInfo &right) const{
        if ((this->cid == right.cid) && (this->level == right.level)){
            return false; //让比较函数对相同元素返回false
        }else{
            return true;
        }
    }
};

```