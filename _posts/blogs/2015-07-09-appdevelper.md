---
layout:     post
title:      手机app快速开发的经验
category: blogs
description: 这是个人在手机app开发这一块的一些经验总结，希望能给大家一个好的参考。
---

### app开发模式
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;目前app平台有Android和IOS两大平台，对于一般的手机应用来说我们只需开发这两个平台的app（对于类似新浪微博、微信、QQ这样的高群体用户来说，那就必须支持所有的平台，包括：IOS，Android，Palm，Symbian，WP7，WP8，Bada和Blackberry）。目前手机app的开发模式有两大模式，分别为原生开发和混搭Web开发。对于中小团队来说我建议使用混搭Web开发的模式，因为使用原生开发需要对每个平台分不同的团队来进行开发，这样团队人员和开发进度将会是一个瓶颈。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;混搭Web开发，首选是使用PhongGap+HTML5+CSS3+JavaScript。[Phonegap](http://phonegap.com/)是一个用基于HTML，CSS和JavaScript的，创建移动跨平台移动应用程序的快速开发平台。它使开发者能够利用iPhone，Android，Palm，Symbian，WP7，WP8，Bada和Blackberry智能手机的核心功能。目前几乎所有的Android和IOS系统的手机都支持HTML5和CSS3（唯一的差别就是个别比较旧的浏览器对某些特性不支持或支持的不完美）。

### 信息推送信息
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;自己开发信息推送？不建议，除非你的团队足够大或者有比较特殊的保密信息才建议自己开发。信息推送我们先说主流的手机平台（Android和IOS），Android和IOS的推送机制完成不一样，Android是手机应用于应用后台服务之间的通讯；IOS是基于苹果公司提供的消息推送服务(APNS)，其原理就是，第三方应用将要推送给用户的信息推送到苹果服务器，苹果服务器再通过统一的系统接口将这些信息推送到用户的手机上。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;使用比较成熟的信息推送框架，会给我们的手机app开发带来不少的便利。这里推荐[极光推送](https://www.jpush.cn/common/products)，极光推送也是比较成熟的
信息推送系统，其平台整合了Android推送、iOS推送的统一推送服务。一般企业用户使用其免费版本也就足够了，想要了解免费版和收费版的区别[请看这里](https://www.jpush.cn/common/price)，其它不多少，搞的好像给它做广告是的。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;极光推送平台当然不是唯一的选择，还有[百度的云推送](http://push.baidu.com/)，推送（Push）是百度开放云向开发者提供的消息推送服务；通过利用云端与客户端之间建立稳定、可靠的长连接来为开发者提供向客户端应用推送实时消息的一种开发者服务。目前百度"云推送"服务是完全免费的，只支持 Android及iOS两个平台。也是这两年才推出的服务，相对来说是一个比较新的平台。本人还没怎么去研究其跟极光推送平台的差异和对比其优劣。不过我个人比较喜欢百度的开发服务平台，基本都是免费而且很全，如果是我选择的话，我会选择百度云推送。

### 社会化分享
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;社会化分享已经成为一个app必不可少的一个模块。新浪微博，腾讯微博，QQ空间，人人网，开心网，微信，QQ好友等平台的分享，难道我们都需要对每个平台进行对接吗，那我们的工作量和维护量得多大啊？刚刚才说百度的开发服务平台很全，现在就给你推荐它的另一个服务[百度社会化分享组件](http://developer.baidu.com/soc/share)，该组件有IOS、Android和Webapp三种模式。目前支持新浪微博、腾讯微博、QQ空间、开心网、微信好友、微信朋友圈进行分享，同时支持Android系统的邮件、短信同步分享。

### 统计分析和监控
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;统计分析这对app来说也是相当重要的一部分，它可以帮你更好的了解你的app的健康情况和用户分析等。这一方面百度的开发服务平台也提供了非常全面的服务，[百度统计-网站统计](http://tongji.baidu.com/web/welcome/login)、[百度统计-移动统计](http://mtj.baidu.com/web/welcome/login)等等。百度统计-网站统计[演示地址](http://tongji.baidu.com/web/5473605/overview/multi?siteId=1942168)，百度统计-移动统计[演示地址](http://mtj.baidu.com/web/overview?appId=19)。

### 应用测试与发布
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这么多手机型号，难道每一种手机型号都要买来测试吗？不用，咱们还是可以使用[百度移动云测试](http://mtc.baidu.com/mtc/)。对于一个app在内测阶段的app，怎么管理你的版本和快速测试呢，这[蒲公英 - 免费的应用托管平台|App应用众测分发](http://www.pgyer.com/)可以帮到你。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;发布到应用市场，对于IOS来说就相对简单，因为都是必须在早苹果的App Store进行发布。而Android就不一样，每个厂商都搞自己应用市场，五花八门，一个个发布那是相当的麻烦，你也可以使用[抓猫](https://www.zhuamob.com/)，来进行统一发布。
