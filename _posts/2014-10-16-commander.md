---
layout: post
title: node.js命令行模块commander学习笔记
category: 技术
tags: node模块
description: commander模块学习
---

commander模块可以干一件看起来很酷的事情，那就是编写自己的命令行命令，[Github地址](https://github.com/visionmedia/commander.js)。

跑一下官方的例子可以对这个模块有个基本的认识，我们在项目中利用该模块编写了很多有用的命令，其中一个就是展示游戏服务器的各项配置信息，剥离出来，就是下面的例子：

目录中有个文件config.json，记录了服务器的各项配置：
    
    {
        "app":{
            "port":3000
        },
        "gm":{
            "port":3001
        },
        "database": {
            "host": "127.0.0.1",
            "port": 27017,
            "dbname":"pk_server000"
        }
    }

当前目录下新建一个文件gm，内容如下：
    
    #!/usr/bin/env node

    var program = require('commander')
        , fs = require('fs')
        , path = require('path');

    var configFile = './config.json';

    program
    .version('0.0.1')

    program
    .command('config')
    .description('show file')
    .action(showConfig);  

    function showConfig(){
        console.log('Path:',path.resolve(configFile));
        var opt={
            encoding:'utf-8',
            flag:'r'
        };
        fs.readFile(configFile,opt,function(err,data){
            if(err){
                return console.log('Read error:',err);
            }
            console.log(JSON.parse(data));
        });
    }

    program.parse(process.argv);    

可能需要更改一下文件的权限，使之可执行
    
    chmod 777 gm

好了，现在我们可以使用gm命令了:
    
    ./gm config    

还有一个备忘的小例子

    #!/usr/bin/env node
    var program = require('commander');
    program
    .command('bye [name]')
    .description('say goodbye')
    .action(function(name){
        console.log('Bye ' + name + '. It was good to see you!');
    }); 
    program.parse(process.argv);   

