---
title: 构造函数
date: 2021-06-04 08:52:46
tags: JavaScript
categories: JavaScript
---
### 什么是构造函数？
- 依然是个函数，函数名首字母必须大写
- 构造函数内部使用 this 指向创建好的对象内添加属性或方法
- 必须有 new 不然 this 指向的会变成 windows
- 构造函数永远一个原型属性 prototype ，该属性是一个对象 这个对象内创建的内容是给所有创建的对象添加一个属性
- 只要是对象内部都会默认有一个__proto__属性，如果这个对象是你的某个构造函数创建出来的话，那么这个__proto__指的就是你的构造西数的原型对象,如果不是那么这个__proto__指的就是js内置的构造函数 Object 的原型对象,如果一个对象一直查找__proto__那么最终指向的是null
- 原型内的属性和方法(prototype声明的方法)会在实例化对象下的__proto__属性内显示(该属性指的是创建该实例化对象的构造函数的原型对象)；
- 如果原型对象(prototype)修改了公共的原型对象方法也改变了
- 构造函数的原型对象内默认会有一个 constructor 方法，该方法指的是构造函数本身
    ```xml
        function CreatCat(name, age) {
            this.name = name;
            this.age = age;
        }
        CreatCat.prototype.say = function () {
            console.log(this.name)
        }
        var cat1 = new CreatCat("咪咪", 1)
        console.log(cat1.constructor);
    ```
- 当实例化对象访问或者获取 公共的原型内的方法或者属性的时候  一直会在原型对象内查找  如果原型对象修改了，实例化对象的公共属性和方法也变了(上面的say方法)
### 构造函数的合并
- 普通合并，用 assign 将 user 的方法也合并给 systemuser，但不会改变 systemuser 的原型对象
    ```javaScript
        function User(name, age) {
            this.name = name;
            this.age = age;
        }
        User.prototype.say = function () {
            console.log("猫")
        }
        var user1 = new User("张三", 18)
        console.log(user1);



        function SystemUser(username, userage) {
            User.call(this, username, userage);
        }
        Object.assign(SystemUser.prototype, User.prototype);

        var systemuser1 = new SystemUser("李四", 23)
        console.log(systemuser1);


        SystemUser.prototype.sayHi = function () {
            console.log('我是管理员')
        }
        systemuser1.sayHi();
        user1.sayHi();//提示错误
    ```
- 另一种合并
    ```javaScript
        function Animal(type) {
            this.type = type;
        }

        Animal.prototype.say = function () {
            console.log("我是" + this.type + "动物");
        }

        var catAnimal = new Animal("猫科类");

        console.log(catAnimal);
        catAnimal.say();

        function Cat(name, age) {
            this.name = name
            this.age = age
        }

        Cat.prototype = catAnimal

        var mimi = new Cat('小花儿', 2)
        mimi.say()
    ```