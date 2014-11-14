---
layout: post
title: 我对javascript对象和原型的理解 
category: 技术
tags: javaScript
description: 对象和原型
---

## 对象

    function Student (name, age) {
        this.name = name;
        this.age = age;
    }

    var zhangsan = new Student("zhangsan", 10);
    var lisi = {};
    Student.call(lisi, "lisi", 11);
    console.log('zhangsan: ', zhangsan);
    console.log('lisi: ', lisi);

    //zhangsan:  { name: 'zhangsan', age: 10 }
    //lisi:  { name: 'lisi', age: 11 }

上面的例子恰巧还涉及到了js中的this指针的概念：

> this在js中指的就是调用函数的上下文

我的理解就是： **this** 指向调用函数的对象。

在上面的例子中，**zhangsan** 是通过关键字 **new**利用构造函数创建，js选手对于这种方式再熟悉不过了。在学习和使用**call** 以及 **this**的过程中，我偶然想到是不是可以通过 **Student.call(lisi, "lisi", 11)** 创建一个对象实例，实验之果然可行，这个例子也加深了我对js的对象的理解。

Student是一个构造函数，lisi就是调用Student的对象（上下文），这样通过执行该函数，把name和age属性都添加到list对象上。

## 原型链

    function Shape (x, y) {
        this.x = x || 0;
        this.y = y || 0;
    }

    Shape.prototype.getPosition = function () {
        return [this.x, this.y];
    }   

    var s = new Shape(10, 20);
    s.getPosition();

js中，当你创建一个构造函数的时候，例如上例中的Shape，该构造函数会自动获得一个属性prototype，当你用构造函数创建一个实例时，例如上例中得s，该实例会获得一个属性 __proto __，这个属性指向该实例的构造函数的prototype，你可以通过下列代码证实：

    console.log(s.__proto__ === Shape.prototype);
    //true

然后，Shape.prototype作为一个实例，它也有__proto __属性，指向的是 Object.prototype，然后这就是所谓的原型链，当然这也只是我个人的理解。

s调用getPosition函数，外层（我胡比想的一个词，意会吧），找不到getPosition的定义，就会进入到__proto __中查找定义，也就是在Shape.prototype中查找，本例中就找到了，假若没有找到，就会到Object.prototype中查找，而到了这里，js的原型链就到头了。

    console.log(Object.prototype.__proto__);
    //null

## 使用原型链实现继承

    function Shape() {
        this.x = 0;
        this.y = 0;
    }

    Shape.prototype.getPosition = function () {
        return [this.x, this.y];
    };

    function Circle() {
        this.radius = 0;
        Shape.call(this);
        this.x = 5;
        this.y = 10;
    }

    Circle.prototype = Object.create(Shape.prototype);

    var c = new Circle();

看一下Object.create的定义可以帮助理解上面的例子：

    Object.create = (function(){
        function F(){};
        return function(o){
                F.prototype = o;
                return new F();
        };
    })();   

不做讲解了，原型链继承的这个经典例子抄自[谈谈JavaScript中的原型继承](http://www.html-js.com/article/A-day-to-learn-to-talk-to-JavaScript-JavaScript-prototype-inheritance)这篇博文，内容很详尽。     







 
