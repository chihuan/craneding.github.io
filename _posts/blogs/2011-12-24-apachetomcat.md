---
layout:       post
title:        Apache与Tomcat搭建集群
category:     blogs
tags:         [apache,tomcat]
description:  一起来学习怎么搭建Apache与Tomcat的集群。
---

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;早前就解了Apache和Tomcat可以搭建集群,可以负载均衡,升级就不需要停交易,真是强大。昨晚看了google reader的收藏又再次看到这篇文章,于是今天在星巴克研究了一把,发现真的很强大,负载均衡、session复制都可以做到,以后再也不用为升级系统而烦恼了。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;下面就来讲讲是搭建集群的过程，首页需要下载apahce和tomcat（当然需要安装jdk,这就不多讲了,大家应该懂得），本次实践我是在windows系统的环境下进行的，apache是2.2.21版本，tomcat是7.0.16和7.0.23两个版本。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;首先讲讲tomcat需要配置的文件，假设Tomcat 7.0.16为服务器A，Tomcat 7.0.23为服务器B。注意如果你的Tomcat都是放在同一台机子上,那你要修改端口，确保端口不要冲突。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;服务器A的server.xml配置文件中的Engine节点中新增jvmRoute属性，值可以自己定义,例如jvm1,同时新增Cluster节点的所有内容,如果tomcat是在同一台机子的就需要注意Receiver节点的port属性不能冲突，例如：4000

服务器A的server.xml配置文件 

```xml
<Connector port="8080" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" />  
  
<Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />  
  
<Engine name="Catalina" defaultHost="localhost" jvmRoute="jvm1">  
  
<Cluster className="org.apache.catalina.ha.tcp.SimpleTcpCluster" hannelSendOptions="8">  
        <Manager className="org.apache.catalina.ha.session.DeltaManager" expireSessionsOnShutdown="false" notifyListenersOnReplication="true" />  
          
        <Channel className="org.apache.catalina.tribes.group.GroupChannel">    
             <Membership className="org.apache.catalina.tribes.membership.McastService" address="228.0.0.4" port="45564" frequency="500" dropTime="3000"/>    
             <Receiver className="org.apache.catalina.tribes.transport.nio.NioReceiver" address="auto"    
                       port="4000"  
                       autoBind="100"  
                       selectorTimeout="5000"  
                       maxThreads="6" />  
    
             <Sender className="org.apache.catalina.tribes.transport.ReplicationTransmitter">  
               <Transport className="org.apache.catalina.tribes.transport.nio.PooledParallelSender"/>  
             </Sender>  
             <Interceptor className="org.apache.catalina.tribes.group.interceptors.TcpFailureDetector"/>  
             <Interceptor className="org.apache.catalina.tribes.group.interceptors.MessageDispatch15Interceptor"/>  
               
             <Valve className="org.apache.catalina.ha.tcp.ReplicationValve"  
                  filter=""/>  
           <Valve className="org.apache.catalina.ha.session.JvmRouteBinderValve"/>  
    
           <Deployer className="org.apache.catalina.ha.deploy.FarmWarDeployer"  
                     tempDir="/tmp/war-temp/"  
                     deployDir="/tmp/war-deploy/"  
                     watchDir="/tmp/war-listen/"  
                     watchEnabled="false"/>  
    
           <ClusterListener className="org.apache.catalina.ha.session.JvmRouteSessionIDBinderListener"/>  
           <ClusterListener className="org.apache.catalina.ha.session.ClusterSessionListener"/>  
           </Channel>  
      </Cluster>  
......  
  
</Engine>
```

服务器B的server.xml配置文件,其中不同的是8180、8109和4001的几个端口的修改和jvmRoute值的不同,其它都一样

```xml
<Connector port="8180" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" />  
  
<Connector port="8109" protocol="AJP/1.3" redirectPort="8443" />  
  
<Engine name="Catalina" defaultHost="localhost" jvmRoute="jvm2">  
  
<Cluster className="org.apache.catalina.ha.tcp.SimpleTcpCluster" hannelSendOptions="8">  
        <Manager className="org.apache.catalina.ha.session.DeltaManager" expireSessionsOnShutdown="false" notifyListenersOnReplication="true" />  
          
        <Channel className="org.apache.catalina.tribes.group.GroupChannel">    
             <Membership className="org.apache.catalina.tribes.membership.McastService" address="228.0.0.4" port="45564" frequency="500" dropTime="3000"/>    
             <Receiver className="org.apache.catalina.tribes.transport.nio.NioReceiver" address="auto"    
                       port="4001"  
                       autoBind="100"  
                       selectorTimeout="5000"  
                       maxThreads="6" />  
    
             <Sender className="org.apache.catalina.tribes.transport.ReplicationTransmitter">  
               <Transport className="org.apache.catalina.tribes.transport.nio.PooledParallelSender"/>  
             </Sender>  
             <Interceptor className="org.apache.catalina.tribes.group.interceptors.TcpFailureDetector"/>  
             <Interceptor className="org.apache.catalina.tribes.group.interceptors.MessageDispatch15Interceptor"/>  
               
             <Valve className="org.apache.catalina.ha.tcp.ReplicationValve"  
                  filter=""/>  
           <Valve className="org.apache.catalina.ha.session.JvmRouteBinderValve"/>  
    
           <Deployer className="org.apache.catalina.ha.deploy.FarmWarDeployer"  
                     tempDir="/tmp/war-temp/"  
                     deployDir="/tmp/war-deploy/"  
                     watchDir="/tmp/war-listen/"  
                     watchEnabled="false"/>  
    
           <ClusterListener className="org.apache.catalina.ha.session.JvmRouteSessionIDBinderListener"/>  
           <ClusterListener className="org.apache.catalina.ha.session.ClusterSessionListener"/>  
           </Channel>  
      </Cluster>  
......  
  
</Engine>
```

tomcat配置好了，为了session复制，我们还需要在应用的web.xml文件中添加<distributeable/>这个一个配置，那接下来我们就来讲讲apache的配置，需要修改apache的httpd.conf文件，将去掉一下这些的注释，使其生效 

```xml
Include conf/extra/httpd-vhosts.conf  
  
LoadModule negotiation_module modules/mod_negotiation.so  
LoadModule proxy_module modules/mod_proxy.so  
LoadModule proxy_ajp_module modules/mod_proxy_ajp.so  
LoadModule proxy_balancer_module modules/mod_proxy_balancer.so  
LoadModule proxy_connect_module modules/mod_proxy_connect.so  
LoadModule proxy_ftp_module modules/mod_proxy_ftp.so  
LoadModule proxy_http_module modules/mod_proxy_http.so 
```

在http.conf的最后面新增以下配置，使apache可以反向代理和负载均衡,注意这里的端口是tomcat的端口,同时route是刚才配置的jvmRoute的值,不能配错 

```xml
    ProxyRequests Off  
    <proxy balancer://loadbalancer>   
    BalancerMember http://127.0.0.1:8080 loadfactor=1 route=jvm1  
    BalancerMember http://127.0.0.1:8180 loadfactor=1 route=jvm2  
    </proxy>  
```

下面是httpd-vhosts.conf文件的配置,其它就不多讲了，"ProxyPass /google !"是可以配置/google地址不反向代理，那么输入地址/google就会在你apahce的根目录里面找，"/baidu" 是配置了方向代理到百度，以上这两个配置主要是看个人需求，主要是想说明怎么配置方向代理，而"ProxyPass / balancer://loadbalancer/ stickysession=jsessionid nofailover=On" 这两句才是重点，主要是配置“/”都反向代理到tomcat，并且是负载均衡的模式 

```xml
<VirtualHost *:80>  
    ServerAdmin webmaster@dummy-host.xiaoyang.com  
    DocumentRoot "D:/Program Files/Apache Software Foundation/Apache2.2/docs/dummy-host.xiaoyang.com"  
    ServerName dummy-host.xiaoyang.com  
    ServerAlias www.dummy-host.xiaoyang.com  
    ErrorLog "logs/dummy-host.xiaoyang.com-error.log"  
    CustomLog "logs/dummy-host.xiaoyang.com-access.log" common  
  
        ProxyPass /google !  
          
        ProxyPass /baidu http://www.baidu.com  
    ProxyPassReverse /baidu http://www.baidu.com  
      
    ProxyPass / balancer://loadbalancer/ stickysession=jsessionid nofailover=On  
    ProxyPassReverse / balancer://loadbalancer/  
</VirtualHost>
```

好了这就完成了，然后就可以打开你的apache的地址了，你不停的刷新页面,会被负载分配到两个tomcat服务其上面其，同时会话是相同的。