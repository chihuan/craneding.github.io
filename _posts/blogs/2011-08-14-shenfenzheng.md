---
layout:       post
title:        身份证号码验证位的计算
category:     blogs
tags:         [js]
description:  身份证上哪一位校验位呢？哪一位又是顺序码？都代表什么意思呢？
---

```html
<script>
//15位身份证号码 = 地址码(6位) + 出生日期码(6位) + 顺序码(3位)  
//18位身份证号码 = 地址码(6位) + 出生日期码(8位) + 顺序码(3位) + 校验码(1位)  
//18位身份证号码中的顺序码的最后一位奇数代表性别男,偶数代表性别女  
  
// 计算18位身份证号码校验位  
function y(notext) {  
    var len = notext.length;  
      
    if(len != 18)  
        return null;  
      
    // 加权因子  
    var ws = [7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2];  
    // 校验码  
    var ys = ['1', '0', 'X', '9', '8', '7', '6', '5', '4', '3', '2'];  
      
    // S = Sum(Ai * Wi), i = 0, ... , 16  
    var S = 0;  
    for(var i = 0; i < 17 && i < len; i++) {  
        S = S + (parseInt(notext.charAt(i)) * ws[i]);  
    }  
      
    // Y = mod(S, 11)  
    var Y = S % 11;  
      
    return ys[Y];  
}
</script>
```
