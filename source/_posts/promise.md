---
title: promise
date: 2021-06-21 10:32:15
tags: JavaScript
categories: JavaScript
---
### 什么是Promise
- 他是一个对象，是用来处理异步操作的，可以让我们写异步调用的时候写起来更加优雅，更加美观便于阅读。顾名思义为承诺、许诺的意思，意思是使用了Promise之后他肯定会给我们答复，无论成功或者失败都会给我们一个答复。Promise有三种状态：pending（进行中），resolved（完成），rejected（失败）。
### 怎么使用Promise
- promise 对象和 es6 配合使用，es6中构造函数原型上有一个比较常用的 then 方法，用来执行回调函数，then 方法接受两个参数，第一个是成功的 resolved 的回调，另一个是失败 rejected 的回调，第二个失败的回调参数可选。并且 then 方法里也可以返回 promise 对象
- 理论已经到位，下面上代码
```js
    const promise = new Promise((resolve, reject) => {
    console.log(1)
    resolve()
    console.log(2)
    })
    promise.then(() => {
    console.log(3)
    })
    console.log(4)
    // 运行结果
    1
    2
    4
    3
```
- 为什么是这个结果呢？Promise 内部是顺序执行的，resolve 是异步执行的
- 另外 Promise.all() 也是比较常见的，什么时候使用呢？适合用于所有的结果都成功了才去执行 then（）成功的操作，废话不多说，上代码
```js
    let p1 = new Promise(function (resolve, reject) {
        resolve();
    });
    let p2 = new Promise(function (resolve, reject) {
        resolve();
    });
    let p3 = new Promise(function (resolve, reject) {
        resolve();
    });
    Promise.all([p1, p2, p3]).then(function (results) {
        console.log('我们都成功了');
    }).catch(function (err) {
        console.log(err);
    });
```
- 上面执行结果为 我们都成功了，那么如果有失败的呢？下面请看代码
```js
    let p1 = new Promise(function (resolve, reject) {
        resolve();
    });
    let p2 = new Promise(function (resolve, reject) {
        reject('我是p2我失败了');
    });
    let p3 = new Promise(function (resolve, reject) {
        resolve();
    });
    Promise.all([p1, p2, p3]).then(function (results) {
        console.log('我们都成功了');
    }).catch(function (err) {
        console.log(err);
    });
```
- 就会返回 我是 p2 我失败了
- 接下来我们使用 promise 对象和 es6 中构造函数原型上的 finally() 配合使用，请看代码
```js
    const achievement = Math.floor(Math.random()*99)
    const promise = new Promise((resolve, reject) => {
        if (achievement > 60) {
            resolve('我及格了')
        } else {
            reject('我没及格')
        }
    })
    promise.then(pass => {
        console.log(pass);
    }).catch(fail => {
        console.log(fail);
    }).finally(()=>{
        console.log('我考试了');
    })
```
- 不管考试是否及格，都会返回'我考试了'
- 下面讲解一下 Promise.race() 的作用也是同时执行多个实例，只要有一个实例改变状态，Promise就改为那个实例所改变的状态，通俗的说呢，就是赛跑，有一个完成，就结束了，下面直接上代码讲解
```js
    function rabbit() {
        var p = new Promise((resolve, reject) => {
            //延时函数，用于给请求计时
            setTimeout(() => {
                reject('我是兔子，我跑完了');
            }, 1000);
        });
        return p;
    }
    function tortoise() {
        var p = new Promise((resolve, reject) => {
            setTimeout(() => {
                reject('我是乌龟，我居然输了');
            }, 3000);
        });
        return p;
    }
    Promise.race([rabbit(), tortoise()]).then((data) => {
        console.log(data);
    }).catch((err) => {
        console.log(err);
    });
```
- 结果很明显这次兔子赢了，嘿嘿。 