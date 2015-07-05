---
layout:     post
title:      Memcached分布式
category: blogs
description: Mecached一个高性能的分布式内存对象缓存系统，让我们一起来了解它的特性。
---

&nbsp;&nbsp;&nbsp;&nbsp;大多数小公司的Web服务器都只有一台，然后就部署了很多Web程序，完全没有什么负载均衡的概念。一但要做个升级，就得停服务，升级完成后，用户还得重新登录，这给用户是相当不好的体验。

&nbsp;&nbsp;&nbsp;&nbsp;Web负载均衡，这首选肯定是Nginx了，这就不在这里多说了。而使用了负载均衡，那多个Web实例的用户会话怎么保持一致呢？这个时候Memcached就可以闪亮登场了（其实Memcached的不仅仅是用于用户会话缓存的），最近学习了Memcached，在自己边学习，边实验的过程当中，看了许多资料。这里就简单说一下Memcached，具体会给大家分享一些比较好的文章。

&nbsp;&nbsp;&nbsp;&nbsp;Memcached 是一个高性能的分布式内存对象缓存系统，用于动态Web应用以减轻数据库负载。介绍可以看官网，如果觉得英文看不大懂，那就看看[百度百科](http://baike.baidu.com/link?url=5s_KtQnwf9DohOzjy3rBtUpBMX21lLHE9ZjB6DibbAyXmyE2juRn5hCUt9cdTnoS)的介绍，同时也有对Memcached做了全面剖析，详情请看[memcached全面剖析--PDF总结篇](http://blog.charlee.li/memcached-pdf/)。 

> memcached全面剖析的连载已经结束，翻译工作也已经全部完成了。
> 
> 为了方便阅读，现将原来的翻译结果打包成PDF文档。可在本文末尾处下载。
> 
> 原来的各篇翻译的地址如下：
> 
>    第1章：
>
>    第2章：http://tech.idv2.com/2008/07/11/memcached-002/
>
>    第3章：http://tech.idv2.com/2008/07/16/memcached-003/
>
>    第4章：http://tech.idv2.com/2008/07/24/memcached-004/
>
>    第5章：http://tech.idv2.com/2008/07/31/memcached-005/ 

&nbsp;&nbsp;&nbsp;&nbsp;Memcached是需要安装的，具体的安装就不在这里将来，安装方面可以看官网的介绍或[这篇文章](http://www.cnblogs.com/czh-liyu/archive/2010/04/27/1722084.html)。那有了服务器端，那其客户端支持什么语言呢？有C / C++、PHP、Java、Python等等，基本的语言都支持，对于客户端的介绍和下载，请看[Clients](http://code.google.com/p/memcached/wiki/Clients)。

&nbsp;&nbsp;&nbsp;&nbsp;那至于怎么跟Tomcat进行结合呢？需要用到哪些包呢？请看[memcached-session-manager](http://code.google.com/p/memcached-session-manager/wiki/SetupAndConfiguration)，这篇文章写的非常详细，不过就是全英文的。想看中文的翻译版的，那请看这篇文章[memcached-session-manager中文翻译](http://chenzhou123520.iteye.com/blog/1650212)

> [Introduction](http://code.google.com/p/memcached-session-manager/wiki/SetupAndConfiguration#Introduction)
> 
>    [Decide which serialization strategy to use](http://code.google.com/p/memcached-session-manager/wiki/SetupAndConfiguration#Decide_which_serialization_strategy_to_use)
>
>    [Configure tomcat](http://code.google.com/p/memcached-session-manager/wiki/SetupAndConfiguration#Configure_tomcat)
>
>    &nbsp;&nbsp;&nbsp;&nbsp;[Add memcached-session-manager jars to tomcat](http://code.google.com/p/memcached-session-manager/wiki/SetupAndConfiguration#Add_memcached-session-manager_jars_to_tomcat)
>
>    &nbsp;&nbsp;&nbsp;&nbsp;[Add custom serializers to your webapp (optional)](http://code.google.com/p/memcached-session-manager/wiki/SetupAndConfiguration#Add_custom_serializers_to_your_webapp_(optional))
> 
>   &nbsp;&nbsp;&nbsp;&nbsp;[Configure memcached-session-manager as <Context> Manager](http://code.google.com/p/memcached-session-manager/wiki/SetupAndConfiguration#Configure_memcached-session-manager_as_%3CContext%3E_Manager)
>
>    &nbsp;&nbsp;&nbsp;&nbsp;[Overview over memcached-session-manager configuration attributes](http://code.google.com/p/memcached-session-manager/wiki/SetupAndConfiguration#Overview_over_memcached-session-manager_configuration_attributes)
>
>    &nbsp;&nbsp;&nbsp;&nbsp;[Overview over available system properties (all optional)](http://code.google.com/p/memcached-session-manager/wiki/SetupAndConfiguration#Overview_over_available_system_properties_(all_optional))
>
>    [Configure logging](http://code.google.com/p/memcached-session-manager/wiki/SetupAndConfiguration#Configure_logging)
