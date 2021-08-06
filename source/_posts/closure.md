---
title: 闭包
date: 2021-05-19 18:54:56
tags: JavaScript
categories: JavaScript
---
### 闭包的产生和特点
- 简单的说函数嵌套函数，就会产生闭包
- 作用域的嵌套 而且嵌套关系永远存在
- 闭包外层定义的变量会一直存储在内存中，等待闭包内层的作用域访问
- 内存占用比较大
### 为什么使用闭包
- 这就要从变量作用域开始说了
```js
    var a=666;

　　function f1(){
　　　　alert(a);
　　}

　　f1(); // 666
```
- 我们函数外部定义的变量函数内部是可以拿到的但是，如果是函数内部定义的变量呢
```js
    function f1(){
　　　　var a=666;
　　}

　　alert(a);//a is not defined
```
- 这样就会报错，那我我们如果需要用的函数内部的变量呢？于是闭包就产生了
### 讲解闭包
- 一个小栗子
```javaScript
    function fun(){
        var num = 10;
        function fun1(){
            num++;
            console.log(num)
        }
        return fun1;
    }
    var newFun=fun();
    newfun(); // 11
    newfun(); // 12
    newfun(); // 13
    fun=null;
    newFun=null;
```
- 一个小应用
    - 当前页面有5个button，要求是点击每个button的时候弹出对应的编号
        ```xml
            <body>
                <button>Button0</button>
                <button>Button1</button>
                <button>Button2</button>
                <button>Button3</button>
                <button>Button4</button>
            </body>
            <script>
            let btnList=document.querySelectorAll('button')
            for (var i = 0; i < btnList.length; i++) {
                //使用立刻执行函数 闭包接收i的值 因为异步执行方法会在同步执行方法后执行
                (function (i) {
                    btnList[i].onclick = function () {
                        console.log(i)
                    }
                })(i);
            }
            </script>
        ```
### 使用闭包的注意点
1. 由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。
2. 闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。