---
layout: post
title: pomelo学习笔记（一）
category: 技术
tags: pomelo
description: 从零单排pomelo，从框架起步学习TCP编程
---
又是好久没写笔记了，当然，就是又开了个新坑：pomelo，先简要记录下来近期从各类文档、示例、官方API获取的知识点，项目初期，利用他们就可以开工啦，至于系统化，就放在以后吧，假若还有时间干这个的话。

官方文档上有所有API详细说明 [http://pomelo.netease.com/api.html](http://pomelo.netease.com/api.html)

## 获取频道

pomelo的API有一种分类，channelService，利用这类API即可获取需要的频道：
    
    var channelName = “hall”;
    var needNew = true;
    var channelService = app.get('channelService');
    var channel = channelService.getChannel(channelName, needNew);

getChannel函数即返回了名为hall的频道，needNew的解释：needNew为true，当没有名为hall的频道时，创建该频道并返回。

## 频道上的操作

当我们已经获取了一个频道channel，那么问题来了，怎么对它进行操作呢，答案很简单，请看官方API，channel类别就是干这个的。举个例子，很常见的一种就是把用户加进频道：
    
    channel.add(uid, sid);

uid参数填入用户的唯一标识，sid填入管理该用户长连接的connector服务器id。

另一种常见操作就是获取频道中的用户：

    var member = channel.getMember(uid);
    var members = channel.getMembers();  

获取到的member的默认格式为{uid: XXX, sid: XXX}

## 广播

长连接的精髓啊，终于来了，在pomelo中有三种方法可以去广播

### pushMessageByUids

使用channelService类别下的pushMessageByUids可以进行针对性的广播:
    
    var para = {
        msg: 'hello',
        from: 'zc001',
        to: 'zc002'
    };
    var targets = [{
            uid: 'XXX',
            sid: 'xxxx'
        }];
    channelService.pushMessageByUids('onChat', para, targets, callback);    

这是我比较喜欢的一种书写方式，直观明了。第一个参数标示这是一个'onChat'事件，para中是广播的dict，targets标示要广播给谁，uid就是频道中用户的唯一标识，sid就是管理该用户的前端服务器id，callback就是回调函数。对方怎么接到这个消息呢，看下面：
    
    pomelo.on('onChat', function (data) {
            console.log('data: ', data);
        })

这个data就是para。

### broadcast

位于channelService类别下的broadcast可以广播给连接到某一类前端服务器的用户上，看官方文档喽。

### pushMessage

位于channel类别下的pushMessage可以广播给连接到某一频道上的所有用户，看官方文档喽




        

