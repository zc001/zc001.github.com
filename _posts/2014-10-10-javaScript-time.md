---
layout: post
title: javaScript中的Date对象
category: 技术
tags: javaScript
description: javaScript中常用的时间操作
---

## Date对象
javaScript中获取当前时间以及对时间的各种操作都是通过Date对象完成的。
### 基本用法

获取本地时间

    var now = new Date();
    console.log('now: ', now);
    //now: Fri Oct 10 2014 17:41:05 GMT+0800 (CST)

返回1970年1月1日与当前时间之间的毫秒数

    var now = Date.now();
    console.log('now: ', now);
    //now: 1412934199954

各种函数操作new Date()获取的对象

    var now = new Date();
    var data = now.getDate(); //data是一个介于1和31的整数，表示一个月的第几天
    var day = now.getDay(); //day是一个介于0和6之间的整数，该整数表示星期数（0 表示周日，6表示周六）

对时间对象的操作方法还有很多，可以详查微软的 [Developer Network](http://msdn.microsoft.com/zh-cn/library/cd9w2te4%28v=vs.94%29.aspx)。

## 项目中Date对象的实际应用

### 获取某天0时时间

    function resetTime (date) {
        date.setHours(0);
        date.setMinutes(0);
        date.setSeconds(0);
        date.setMilliseconds(0);
        return date;
    }
    var now = new Date();
    console.log('origin now: ', now);
    console.log('after been changed now: ', resetTime(now));
    //origin now:  Fri Oct 10 2014 18:13:13 GMT+0800 (CST)
    //after been changed now:  Fri Oct 10 2014 00:00:00 GMT+0800 (CST)



### 判断相差几天
在做游戏的时候，常常会用到判断两个时间之间相差几天这样的逻辑。用到了上面的resetTime函数。

    function getDaysDiff (firstData, secondDate) {
        var diff = resetTime(firstData).getTime() - resetTime(secondDate).getTime();
        return diff / 24 * 60 * 60 * 1000;
    }





