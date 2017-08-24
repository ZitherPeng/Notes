# MySql InnoDB memcached plugin 实践技术分享笔记
 
## 向日葵产品技术依赖
1. 通过关系型数据库管理用户主机清单；
2. 使用长连接维持被控在线状态；
3. P2P通信技术传输控制信号以及图像信号；
4. 优化的算法尽可能的降低用户带宽占用以及提高图像质量；
5. 其他周边技术，如HTML5免插件远程控制、远程开机等。

## 向日葵远程控制技术的数据需求
1. 系型数据库存贮某一个用户拥有哪些主机，以及这些主机的具体相关信息；
1. 临时存储一些关键的实时数据：主机鉴权信息、主机在线状态、如何连接主机。

## 缓存优化史

### 从memcached到ttserver  
- memcached  
第一代的主机状态数据缓存化，我们把它放在了memcached，整个客户端的登陆过程如下：
![](http://group.store.qq.com/qun/HHdZ.LJUxqz.eY3q3TgHAQ!!/V3tQmJSIPiKnlna9T8x/800?w5=710&h5=534&rf=viewer_421)
**优势**：把状态等需要频繁访问的数据放到缓存，API负责所有跟持久化DB的交互操作，长连接只负责跟memcached的通信，这样避免了DB有过多角色参与读写；另外只有一台memcached服务器，因为16G内存大约可以放上亿的主机信息。
**问题**：在经历了两次memcached崩溃后，因为memcached的数据是完全放在内存里的，所以崩溃后所有主机全部会变成不在线且只能通过重启所有服务器解决，而重启所有服务器意味着所有原先在线客户端都得全部重新登陆一次，这个过程会极其漫长，以小时计的。
- ttserver  
体系结构如下：
![](http://group.store.qq.com/qun/HHdZ.LJUxqz.eY3q3TgHAQ!!/V3tQmJSIMuMnlkugNcd/800?w5=770&h5=447&rf=viewer_421)
**优势**：tserver可以在崩溃重启后恢复数据且具备主备同步功能，而丢失那部分数据我们可以在客户端登陆时从DB里自动恢复出来，且ttserver跟memcached通信协议上完全兼容，完全堆叠式的设计，理论上也是可以无限扩容的。
**问题**：ttserver不支持key过期的，需要开启table database模式，并通过lua脚本的方式来实现，但该模式ttserver的运行性能相当差，并且在数据很大的时候会出现不稳定的现象。  

### MySQL InnoDB memcached plugin  
- 简介 
&emsp;&emsp;在传统的关系型数据库中，Oracle的Timesten，SQL Server的Hekaton，都是选择与内存数据库相集合，但实际上却少有突出的应用场景。而MySQL嵌入nosql ，在性能与管理、分析上达到互补，则是更为有意义的结合。
&emsp;&emsp;MySQL5.6.6后开始内嵌 memcached 的支持，在MySQL 5.7较新的版本性能大幅提升，有测试表明在48核只读环境下QPS可以达到百万以上。
MySQL官方的结构图:
![](http://group.store.qq.com/qun/HHdZ.LJUxqz.eY3q3TgHAQ!!/V3tQmJSINKOnllnPwkT/800?w5=554&h5=414&rf=viewer_421)
- 安装  
`wget http://cdn.mysql.com//Downloads/MySQL-5.7/mysql-community-5.7.17-1.el6.src.rpm`  

	**注意**：因为是一个插件，开启memcached plugin功能，需要在编译安装时添加：`-DWITH_INNODB_MEMCACHED=ON`
![](http://group.store.qq.com/qun/HHdZ.LJUxqz.eY3q3TgHAQ!!/V3tQmJSIPaPnlkGGKcc/800?w5=401&h5=442&rf=viewer_421)

    - 具体步骤如下：
	![](http://group.store.qq.com/qun/HHdZ.LJUxqz.eY3q3TgHAQ!!/V3tQmJSIISQnlkiUQYV/800?w5=545&h5=21&rf=viewer_421)
	![](http://group.store.qq.com/qun/HHdZ.LJUxqz.eY3q3TgHAQ!!/V3tQmJSIIeQnlltMpMr/800?w5=525&h5=67&rf=viewer_421) 
	```
	memcached plugin相关配置表：
	innodb_memcache.config_options		--配置分割符、引用符
	innodb_memcache.from cache_policies	--根据需要设置缓存策略
	innodb_memcache.containers		--设置表结构：key、value大小，过期时间等
	```

	>在mysql的配置文件my.cnf中通常需要设置以下参数（注意在启动插件后配置，否则mysqld启动报错），主要是配置分配给memcached 的内存大小以及开启写binlog，如果需要指定其他端口，如11212 在loose-daemon_memcached_option参数添加 ' -p11212'
	而daemon_memcached_r_batch_size、daemon_memcached_w_batch_size 默认为1，这里也建议设置为1

	>MySQL memcached plugin 特点：
	1.数据直接读写请求innodb存储引擎，不需要经过SQL层，不需要进行解析编译。
	2.由MySQL buffer pool 管理内存缓存数据。
	3.可以把数据存入多个表，可进行多列数据合并为一个value。
	4.可以通过SQL对数据进行查询、分析、维护。（在过期时间字段添加索引，通过mysql job进行过期数据删除）
	5.可以利用MySQL灵活的主从架构。

- 性能测试对比  
&emsp;&emsp;采用4核进行测试对比，MySQL memcached plugin 与 ttserver （hash模式）性能相当，QPS可以达到7万/秒。比 ttserver （btree模式）高出3倍以上，由于memaslap的测试存在一些缺陷，这里仅供大致参考。
对比图如下：
![](http://group.store.qq.com/qun/HHdZ.LJUxqz.eY3q3TgHAQ!!/V3tQmJSIAeTnlkNamwJ/800?w5=772&h5=312&rf=viewer_421)
&emsp;&emsp;实际上，在网络延迟上，QPS性能将大打折扣，所以要将应用部署在同个内网以降低网络延迟瓶颈，轻松应对每天上亿次的QPS请求，在接近1万/s的QPS并发访问下依旧表现稳定。

- 全新的架构  
&emsp;&emsp;在这次架构优化中，我们在应用和MySQL memcached中间加了一层magent。
![](http://group.store.qq.com/qun/HHdZ.LJUxqz.eY3q3TgHAQ!!/V3tQmJSIMGTnllHhqUs/800?w5=795&h5=382&rf=viewer_421)

**优势：**
1. 通过对magent的改造，实现HA，当ma后端cache某一台down掉后ma可以自动切换；
2. MySQL memcached plugin 不支持multi get/set （在未来的版本中会支持）。通过magent解决。
3. 由于mysql memcached plugin 存在一些bug，5.7.18做了一些修复，但不够完善。借助magent便于控制和维护。
4. 此架构优势：扩展性强,逐步提升应对高并发，采取多主架构，配合magent实现高可用。

  - 其他注意：
	MySQL 5.7.17 前的版本，不建议设置 daemon_memcached_r_batch_size 大于1，容易遭遇 bug 导致 MySQL Crashed。同时建议innodb_api_bk_commit_interval设置为稍大一点的值。默认为5。存在get会话的情况下，对 daemon_memcached 插件进行重启，也会导致MySQL crash，重启插件时要确保没有其他会话。
    禁止flush_all权限操作：`update cache_policies set flush_policy='disabled'`
 

	
>感谢张小峰老师的分享
整理：zither
