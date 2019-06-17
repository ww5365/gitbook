#7.1 System Design overview



>> Design a photo reference counting system at fb scale


这个题是我们在《系统设计班》第一节twitter的那节课讲过的内容。

首先，你先不要曲解题目，你直接把题目翻译为：《设计distributed counting system》就已经走偏了。从这道题的题面来看，面试官只是要对每个photo有一个counter。这个counter干嘛的呢？你可以理解为某个photo被like的数目。这个和我们在《系统设计班》第一节twitter课上说的，某个post被like，是一样的。

在这道题中，面试官主要考核你以下几个层面的东西：*[这个地方是关键]*


* 第一层：

你首先要知道是用denormailze的方法，和photo 一起存在一起，这样不用去数据库里数like。所以可能考察的就是，数据库的存放方法，服务器端用memcached或者任何cache去存储，访问都是找cache，实在是太大的数据量，才会考虑分布式。+1 分


* 第二层：

你知道这玩意儿不能每次去数据库查，得cache。 +0.5分

* 第三层：

这玩意儿一直在更新，被写很多次，你知道必须一直保持这个数据在cache里，不能invalidate。+0.5 分

* 第四层：

你知道怎么让数据库和cache保持一致性 +2分

* 第五层：

你知道 cache 里如果没有了，怎么避免数据库被冲垮（memcache lease get) +2 分


* 第六层：

一个小的优化，如果这个数据很hot，可以在server内部开一个小cache，只存及其hot的数据。+2分



