---
title: 防抖和节流
date: 2021-05-24 10:24:23
tags: JavaScript
categories: JavaScript
---
### 认识防抖和节流
1. 什么是防抖？
    - 假设现在坐公交车，很多人不断在刷卡，那么此时司机是不能开车的，等到乘客都刷卡完毕了，司机需要等待一会儿（延迟时间）确认乘客都做好之后准备开车，此时正好又有一个乘客上车，那么司机又要重新等待刷卡上人再次坐稳之后再开车。
2. 什么是节流？
    - 保证如果电梯第一个人进来后，10秒后准时运送一次，这个时间从第一个人上电梯开始计时，不等待，如果没有人，则不运行。
### 防抖
- 具体代码如下 如果一直滚动滚动条不会运行函数，如果停止滚动一秒后就会运行一次函数
    ```xml
        function debounce(fn, delay) {
            let timer = null //借助闭包，前面讲解过闭包
            return function () {
                if (timer) {
                    clearTimeout(timer)
                }
                timer = setTimeout(fn, delay) // 简化写法
            }
        }
        function showTop() {
            var scrollTop = document.body.scrollTop || document.documentElement.scrollTop;
            console.log('滚动条位置：' + scrollTop);
        }
        window.addEventListener("scroll", debounce(showTop, 1000))
        // 为了方便观察效果我们取个大点的间断值，实际使用根据需要来配置
    ```
### 节流
- 第一种写法，没有定义函数，每隔一秒输出一次滚动条位置
```javaScript
    var lastTime = 0;
    document.addEventListener("scroll", function (event) {
        var currentTime = event.timeStamp;
        if (currentTime - lastTime > 500) {
            var scrollTop = document.body.scrollTop || document.documentElement.scrollTop;
            console.log('滚动条位置：' + scrollTop);
            lastTime = currentTime;
        }
    })
```
- 但是我们一般都会定义一个函数，不会直接写成节流，函数写法一如下
```javaScript
    function throttle(fn, delay) {
        let valid = true
        return function () {
            if (!valid) {
                //休息时间 暂不执行
                return false
            }
            // 工作时间，执行函数并且在间隔期内把状态位设为无效
            valid = false
            setTimeout(() => {
                fn()
                valid = true;
            }, delay)
        }
    }
    // 也可以直接将setTimeout的返回的标记当做判断条件-判断当前定时器是否存在，如果存在表示还在冷却，并且在执行fn之后消除定时器表示激活，原理都一样
    function showTop() {
        var scrollTop = document.body.scrollTop || document.documentElement.scrollTop;
        console.log('滚动条位置：' + scrollTop);
    }
    window.onscroll = throttle(showTop, 1000);
```
- 节流函数并不止上面这种实现方案,例如可以完全不借助setTimeout，可以把状态位换成时间戳，然后利用时间戳差值是否大于指定间隔时间来做判定。具体函数如下
```javaScript
    function throttle(fn, delay) {
        var lastTime = 0;
        return function () {
            that = this;
            arg = arguments;
            nowTime = Date.now();
            if (lastTime === 0 || nowTime - lastTime >= delay) {
                lastTime = Date.now();
                fn.apply(that, arg);
                // 有这句话就可以传递showTop的所以值，可以返回event的一些数据，和this的数据
            }
        }
    }

    function showTop() {
        var scrollTop = document.body.scrollTop || document.documentElement.scrollTop;
        console.log('滚动条位置：' + scrollTop);
    }

    window.onscroll = throttle(showTop, 1000);
```
- 好啦，关于防抖和节流就到这里了，只要动手写一写，相信你很快就会掌握