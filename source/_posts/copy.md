---
title: 数据的深浅拷贝
date: 2021-05-24 14:51:32
tags: JavaScript
categories: JavaScript
---
# 数据的深浅拷贝

> 在 javascript 中有不同的方法来复制对象，如果你还不熟悉这门语言的话，复制对象时就会很容易掉进陷阱里，那么我们怎样才能正确地复制一个对象呢？


## 先熟悉一下数据的类型


- 数据类型可分为两种：
    - 基本类型：undefined,null,Boolean,String,Number,Symbol
    - 引用类型：Object,Array,Date,Function,RegExp等

- 不同类型的存储方式
    - 基本类型：基本类型值在内存中占据固定大小，保存在内存中，可以说不存在深浅拷贝问题
    - 引用类型：引用类型的值是对象，保存在内存中，而内存存储的是对象的变量标识符以及对象在内存中的存储地址，可以说引用类型给变量的是一个地址，存在深浅拷贝问题

- 引用类型的复制方式
    - 从一个变量向另一个新变量复制引用类型的值，其实复制的是指针，最终两个变量最终都指向同一个对象

## 认识深拷贝和浅拷贝


- 浅拷贝：仅仅是复制了引用地址，彼此之间的操作会互相影响

- 深拷贝：重新分配内存，不同的地址，相同的值，互不影响

## 浅拷贝


1. 使用 es6 的展开运算符实现
    ```javaScript
        let obj = { name: '小明', age: 18 }

        let obj1 = { ...obj }

        obj.age = 16
        console.log(obj) // 16
        console.log(obj1) // 18
    ```

2. 使用 assign 方法实现浅拷贝
    ```javaScript
        var obj1 = { name: '小明' };
        var obj2 = Object.assign({}, obj1);
        obj2.name = '小张';
        console.log(obj1.name); //小明
        console.log(obj2.name); //小张
    ```

3. 使用 slice 方法实现
```javaScript
    let arr1 = [
        '小明',
        {
            age: 18
        }
    ];

    let arr2 = arr1.slice(0);
    arr2[1].age = 20;
    /** 因为数组的第一层有引用类型，浅拷贝无法实现 */
    console.log(arr1); // ["小明", {age: 20}]
    console.log(arr2); // ["小明", {age: 20}]
    arr2[0] = '小张';
    console.log(arr1); // ["小明", {age: 20}]
    console.log(arr2); // ["小张", {age: 20}]
```

4. 使用 concat 方法
```javaScript
    let arr1 = [
        '小明',
        {
            age: 18
        }
    ];

    let arr2 = [].concat(arr1);
    arr2[1].age = 20;
    /** 因为数组的第一层有引用类型，浅拷贝无法实现 */
    console.log(arr1); // ["小明", {age: 20}]
    console.log(arr2); // ["小明", {age: 20}]
    arr2[0] = '小张';
    console.log(arr1); // ["小明", {age: 20}]
    console.log(arr2); // ["小张", {age: 20}]
```

- Array的slice和concat方法并不是真正的深拷贝，对于Array的第一层的元素是深拷贝，而Array的第二层 slice和concat方法是复制引用。所以，Array的slice和concat方法都是浅拷贝。

## 深拷贝


1. 通过递归实现深拷贝

```javaScript
    var post = {
        title: "vue 从入门到精通",
        data: "2020-12-20",
        author: {
            name: "wao",
            avatar_url: "http://xxx.jpg"
        },
        comment: ["666", "真棒", [1, 2, 3]]
    }

    // 值 instanceof Array 判断是否是由构造函数Array构成的   一般用于检测 Array   RegExp    Object   Function
    function deepCopy(obj) {
        var newObj = obj instanceof Array ? [] : {};
        // 也可以使用 var newObj = Array.isArray(obj) ? [] : {};
        for (var key in obj) {
            var val = obj[key];
            if (typeof val === "object") {
                newObj[key] = deepCopy(val);
            } else {
                newObj[key] = val;
            }
        }
        return newObj;
    }
    var poster = deepCopy(post);
    poster.data = "2020-12-12";
    poster.author.name = "liu";
    poster.comment[0] = "很6";
    poster.comment[2][0] = 0;
    console.log(post);
    console.log(poster);
```