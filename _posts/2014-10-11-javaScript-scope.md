---
layout: post
title: javaScript的变量作用域
category: 技术
tags: javaScript
description: javaScript令人迷惑的函数作用域
---

跟和 C、C++、Java 等常见语言不同，JavaScript的作用域不是以花括号包围的块级作用域，而是通过函数来定义的，在一个函数中定义的变量只对这个函数内部可见，称为函数作用域。在函数中引用一个变量时，JavaScript会先搜索当前函数作用域，或者称为“局部作用域”，如果没有找到则搜索其上层作用域，一直到全局作用域。

第一个例子：
    
    if(true){
        var str = 'world';
    }
    console.log('str: ', str);
    //str: world


第二个例子：

    var str = 'world';
    function testScope () {
        console.log('str: ', str);
    }
    testScope();
    //str:  world

第三个例子：
    
    var str = 'world';
    function testScope () {
        var str = 'hello';
        console.log('str: ', str);
    }
    testScope();
    //str:  hello

第四个例子：
    
    var str = 'world';
    function testScope () {
        console.log('str: ', str);
        var str = 'hello';
    }
    testScope();
    //str:  undefined

从第四个例子可以看出来，在js的函数中，变量先声明，后赋值，即声明变量的操作是提前的。

第五个例子：

    var str = 'world';
    var test_one = function () {
        console.log('str: ', str);
    }    
    var test_two = function () {
        var str = 'hello';
        test_one();
    }
    test_one();
    test_two();
    //str:  world
    //str:  world

从第五个例子可以看出，js函数作用域的嵌套关系是定义时决定的,而不是调用时决定的,也就 是说，js的作用域是静态作用域，又叫词法作用域，在词法分析时就决定了嵌套关系，不必等到执行。
