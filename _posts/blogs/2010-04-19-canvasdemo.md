---
layout:     post
title:      HTML5 Canvas 的初试
category: blogs
tags:         [web, js]
description: 学习HTML5 Canvas，利用其画板来实现类似ps软件中的某些模块功能。
---

### Canvas的简单实习
HTML5 真的很强大，目前大多数的浏览器都支持了，就差IE了，前两个星期开始了解Canvas，真的很好很强大，HTML5在WEB开发方面真的是越来越快速了和方便了。 

```html
<html>  
 <head>  
  <script type="application/x-javascript">  
    function draw() {  
      var canvas = document.getElementById("canvas");  
      if (canvas.getContext) {  
        var ctx = canvas.getContext("2d");  
  
        ctx.fillStyle = "rgb(200,0,0)";  
        ctx.fillRect (10, 10, 55, 50);  
  
        ctx.fillStyle = "rgba(0, 0, 200, 0.5)";  
        ctx.fillRect (30, 30, 55, 50);  
      }  
    }  
  </script>  
 </head>  
 <body onload="draw();">  
   <canvas id="canvas" width="150" height="150"></canvas>  
 </body>  
</html>
```
效果图如下:

![canvas效果](https://developer.mozilla.org/@api/deki/files/602/=Canvas_ex1.png)

简单的几行代码就可以实现在界面画两个矩形，还支持透明；突然就想起弄个Demo来练练手，于是就自己用GWT做了一个简单的画图页面，[展示地址(国内可能打不开)](http://canvasdemo.appspot.com/)，有兴趣的朋友可以看看，本来想做多几个功能的，可没什么时间做，所有等以后有时间再慢慢完善。 
界面如下图：

![canvas效果](http://dl.iteye.com/upload/attachment/236815/ec876b1d-14f9-32a8-8c52-b3472b89d377.gif)
