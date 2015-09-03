---
layout:       post
title:        微信分享缩略图
category:     blogs
description:  页面怎样在微信分享中显示缩略图？为什么网上很多做法都是不生效的呢？
---

### 有微信公众号

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;有微信公众号，在页面分享的时候显示缩略，只需要接入微信JS-SDK即可，其官方文档也写的很全，详情请看[官方文档](http://mp.weixin.qq.com/wiki/7/aaa137b55fb2e0456bf8dd9148dd613f.html)。

> [3 分享接口](http://mp.weixin.qq.com/wiki/7/aaa137b55fb2e0456bf8dd9148dd613f.html#.E5.88.86.E4.BA.AB.E6.8E.A5.E5.8F.A3)
> 
>    [3.1 获取“分享到朋友圈”按钮点击状态及自定义分享内容接口](http://mp.weixin.qq.com/wiki/7/aaa137b55fb2e0456bf8dd9148dd613f.html#.E8.8E.B7.E5.8F.96.E2.80.9C.E5.88.86.E4.BA.AB.E5.88.B0.E6.9C.8B.E5.8F.8B.E5.9C.88.E2.80.9D.E6.8C.89.E9.92.AE.E7.82.B9.E5.87.BB.E7.8A.B6.E6.80.81.E5.8F.8A.E8.87.AA.E5.AE.9A.E4.B9.89.E5.88.86.E4.BA.AB.E5.86.85.E5.AE.B9.E6.8E.A5.E5.8F.A3)
>    
>    [3.2 获取“分享给朋友”按钮点击状态及自定义分享内容接口](http://mp.weixin.qq.com/wiki/7/aaa137b55fb2e0456bf8dd9148dd613f.html#.E8.8E.B7.E5.8F.96.E2.80.9C.E5.88.86.E4.BA.AB.E7.BB.99.E6.9C.8B.E5.8F.8B.E2.80.9D.E6.8C.89.E9.92.AE.E7.82.B9.E5.87.BB.E7.8A.B6.E6.80.81.E5.8F.8A.E8.87.AA.E5.AE.9A.E4.B9.89.E5.88.86.E4.BA.AB.E5.86.85.E5.AE.B9.E6.8E.A5.E5.8F.A3)
>    
>    [3.3 获取“分享到QQ”按钮点击状态及自定义分享内容接口](http://mp.weixin.qq.com/wiki/7/aaa137b55fb2e0456bf8dd9148dd613f.html#.E8.8E.B7.E5.8F.96.E2.80.9C.E5.88.86.E4.BA.AB.E5.88.B0QQ.E2.80.9D.E6.8C.89.E9.92.AE.E7.82.B9.E5.87.BB.E7.8A.B6.E6.80.81.E5.8F.8A.E8.87.AA.E5.AE.9A.E4.B9.89.E5.88.86.E4.BA.AB.E5.86.85.E5.AE.B9.E6.8E.A5.E5.8F.A3)
>    
>    [3.4 获取“分享到腾讯微博”按钮点击状态及自定义分享内容接口](http://mp.weixin.qq.com/wiki/7/aaa137b55fb2e0456bf8dd9148dd613f.html#.E8.8E.B7.E5.8F.96.E2.80.9C.E5.88.86.E4.BA.AB.E5.88.B0.E8.85.BE.E8.AE.AF.E5.BE.AE.E5.8D.9A.E2.80.9D.E6.8C.89.E9.92.AE.E7.82.B9.E5.87.BB.E7.8A.B6.E6.80.81.E5.8F.8A.E8.87.AA.E5.AE.9A.E4.B9.89.E5.88.86.E4.BA.AB.E5.86.85.E5.AE.B9.E6.8E.A5.E5.8F.A3)
>    
>    [3.5 获取“分享到QQ空间”按钮点击状态及自定义分享内容接口](http://mp.weixin.qq.com/wiki/7/aaa137b55fb2e0456bf8dd9148dd613f.html#.E8.8E.B7.E5.8F.96.E2.80.9C.E5.88.86.E4.BA.AB.E5.88.B0QQ.E7.A9.BA.E9.97.B4.E2.80.9D.E6.8C.89.E9.92.AE.E7.82.B9.E5.87.BB.E7.8A.B6.E6.80.81.E5.8F.8A.E8.87.AA.E5.AE.9A.E4.B9.89.E5.88.86.E4.BA.AB.E5.86.85.E5.AE.B9.E6.8E.A5.E5.8F.A3)

    
### 无微信公众号

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;没有微信公众号，但也想在微信分享的时候显示缩略图，怎么办？网上很多都说用微信浏览器自带的```WeixinJSBridge```来处理，怎么都不生效呢？

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;从微信6起，```WeixinJSBridge```这个对象已经不再支持了，所以不能再用```WeixinJSBridge```了。目前只有按照微信默认的规则来显示，微信的规则是以当前页面的标题作为分享的标题，以页面中第一张符合300*300以上尺寸的图片作为缩略图，没有符合的图片，则不显示缩略图。同时图片最好放在body的第一元素，不然不一定会显示。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;想分享时显示缩略图，但页面又不想显示怎么办？请看一下做法：

```html
<div id="wx_share_icon" style="display: none;">
    <img src="/images/300_300.jpg" width="300px" height="300px" />
</div>
```


