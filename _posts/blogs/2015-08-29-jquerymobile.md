---
layout:       post
title:        JQueryMobile页面跳转与数据传递
category:     blogs
description:  JQueryMobile怎样实现页面跳转和进行页面间的数据传递呢？  
---

### 页面跳转

1. ```<a>``` 标签:

    ```html
    <a href="a/b.html" data-transition="slide">丁小样同学博客</a>
    ```

2. ```<form>``` 标签:

	```html
	<form method="get" action="a/b.html" id="form">
        <label for="name">名称:</label>
        <div class="ui-input-text ui-body-inherit ui-corner-all ui-shadow-inset">
        	<input type="text" value="" name="name" />
        </div>
        <label for="remark">备注:</label>
        <div class="ui-input-text ui-body-inherit ui-corner-all ui-shadow-inset">
        	<input type="text" value="" name="remark" />
        </div>
        <button type="submit" class="ui-btn">页面切换</button>
    </form>    
	```
    

3. ```js``` 代码:

    ```html
    <form id="form">
        <label for="name">名称:</label>
        <div class="ui-input-text ui-body-inherit ui-corner-all ui-shadow-inset">
        	<input type="text" value="" id="name" name="name" />
        </div>
        <label for="remark">备注:</label>
        <div class="ui-input-text ui-body-inherit ui-corner-all ui-shadow-inset">
        	<input type="text" value="" id="remark" name="remark" />
        </div>
        <a href="javascript:ajaxPost();" class="ui-btn">页面切换</a>
    </form>
    
    <script>
    function ajaxPost() {
            $.mobile.changePage("a/b.html", {
                type: "post",
                data: {
                	name: $("#form4").find("#name").val(),
                	remark: $("#form4").find("#remark").val()
                }
            });
     }
    </script>
    ```
    
### 获取页面数据

```html
<script>

function getUrlParam(string:string):any {
     var obj = new Object();
     if (string.indexOf("?") != -1) {
          return urlToJson(string.substr(string.indexOf("?") + 1))
     }
     return obj;
}
function urlToJson(url:string):any {
     var obj = new Object();

     var strs = url.split("&");
     for (var i = 0; i < strs.length; i++) {
         var tempArr = strs[i].split("=");
         obj[tempArr[0]] = decodeURIComponent(tempArr[1].replace(/\+/g, "%20"));
     }

     return obj;
}

$(document).unbind("pagebeforechange").bind("pagebeforechange", function(e, data) {
  if (typeof data.toPage != "string") {
    var url = $.mobile.path.parseUrl(e.target.baseURI);
      if (url.href.search(pageUrl) != -1) {
      	if (data.options.direction && data.options.direction == "back") {// 返回
      		//TODO
      	} else {// 进入
      		if (data.options.type && data.options.type == "get") {// get
    			// 获取数据 getUrlParam(url.href)  			
      		} else {// post
      			// 获取数据 data.options.data
      		}
      	}
      }
  }
}

</script>
```

> 注：上面代码通过[$(e.target).find("#子页面page ID");]

### 预加载页面

1. 在开发移动应用时，对需要链接的页面进行预加载是十分有必要的。因为当一个链接页面设置成为预加载方式时，在当前页面加载完成之后，目标页面也被自动加载到当前文档中，用户单击就可以马上打开，大大加快了页面访问的速度。

2. 设置链接页面预加载，在```<a>```标签中添加```data-prefetch```属性，并将属性值设为true。在JQuery Mobile中要实现页面的预加载，另外一种方法是调用JavaScript代码中的全局性方法```$.mobile.loadPage()```，其效果跟```data-prefetch```一样。

```html
<a href="about.html"rel="external" data-prefetch="ture">点击进入</a>
```


### 缓存页面

1. 在JQuery Mobile中，可以通过页面缓存的方式将访问过的历史内容写入页面文档的缓存中，当用户重新访问时，不需要重新加载，只要从缓存中读取就可以。

2. 保留所有访问过的页面

```html
<script>
	$.mobile.page.prototype.options.domCache = true;
</script>
```

3. 缓存特定的页面

```html
<div data-role="page" id="cacheMe" data-dom-cache="true">
```


