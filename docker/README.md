# docker 
## docker 起源
2010年，旧金山成立了一家做 PaaS 平台的公司，起名为 dotCloud。dotCloud 主要是基于 PaaS 平台为开发者或开发商提供技术服务。 
- 什么是Paas ?  
任何一个在互联网上提供其服务的公司都可以叫做云计算公司。其实云计算分几层的，分别是Infrastructure（基础设施）-as-a- Service，Platform（平台）-as-a-Service，Software（软件）-as-a-Service。基础设施在最下端，平台在中间，软件在顶端。  
![](./images/laas_paas_saas.jpg)
> dotCloud 把需要花费大量时间的手工工作和重复劳动抽象成组件和服务，并放到了云端，另外，它还提供了各种监控、告警和控制功能，方便开发者管理和监控自己的产品。dotCloud 最初运行在 Amazon 的 EC2 上，不过由于 dotClout 高度的抽象层次，理论上 dotCloud 可以运行在各种各样的云服务上面。  
一切看起来都是那么的美好，如果后来的事情按照这个设想进行下去的话，软件厂商和程序员都会松好几口气。
虽然，PaaS 的概念虽好，但是由于认知、理念和技术的局限性，市场的接受度并不高，市场的规模也不够大。除此之外，还有巨头不断进场搅局，IBM 的蓝云，微软的 Azure，Amazon 的 EC2，Google 的 GAE，VMware 的 Cloud Foundry 等等，在这种情况下，虽然 dotCloud 在2011年初拿到了1000万美元的融资，但依然举步维艰。  
于是，dotCloud 的创始人 Solomon Hykes 把大伙召集到一起，说，咱们过的不舒服，也不能让别人痛快了，干脆把我们的核心引擎开源扔到市面上看看，如何？大家面面相觑，最后把拳头砸到桌面上，就这么办。  
这个基于 Linux Container 技术的核心管理引擎一经开源立刻得到了「业界」的热烈吹捧，这个容器管理引擎大大降低了容器技术的使用门槛，轻量级，可移植，虚拟化，语言无关，写了程序扔上去做成镜像可以随处部署和运行，开发、测试和生产环境彻底统一了，还能进行资源管控和虚拟化。业界几个大佬也没闲着，看看自己平台上笨重的 PaaS，纷纷表示要接入或支持这个引擎。  
这个引擎的名字叫做 Docker，以 Go 语言写成。  
从此以后，他们开始专心研发 Docker 产品和维护相关社区。  
2013年10月 dotCloud 公司更名为 Docker 股份有限公司。  
2014年8月 Docker 宣布把平台即服务的业务「dotCloud」出售给位于德国柏林的平台即服务提供商「cloudControl」。  
同年8月，Docker 内部员工 James Turnbull 发布了面向开发者、运维和系统管理员的 Docker 电子书《The Docker Book》。  
12个月过后，Docker 迅速成长为云计算相关领域最受欢迎的开源项目，Amazon、Google、IBM、Microsoft、Red Hat 和 VMware 分别表示已经支持 Docker 技术或准备支持。  
> -  [以上引用部分节选自《Docker 传奇之 dotCloud》—— 池建强-百家号](https://baijia.baidu.com/s?old_id=39451&wfr=pc&fr=app_list)
## 
### docker 加速器
1. 注册成为DaoCloud用户。
1. 登录进入DaoCould用户的控制台页面。
1. 选择"加速器",选择你Docker启动方式对应的说明进行操作。
1. [链接地址：https://www.daocloud.io/mirror#accelerator-doc](https://www.daocloud.io/mirror#accelerator-doc)  