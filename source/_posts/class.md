---
title: class 类
date: 2021-06-04 09:16:40
tags: ES6
categories: ES6
---
### 声明类的基本语法
1. 正如官方所说 ES6 的类，完全可以看作构造函数的另一种写法。
2. 类的内部必须存在 constructor 函数,如果没有显式定义，一个空的 constructor 方法会被默认添加。
3. 除了 constructor 函数之外的函数都相当于共有方法
4. 类的内部默认只能写方法
5. 类的原型 __proto__ 就是他的 constructor 和他的方法
    - 当实例化对象访问一个属性的时候
        - 先找 constructor 
        - 在找类的原型对象
        - 在看有没有继承，有继承的话类的实例化对象的__proto__
        - 当找到最后一层 __proto__ 指的就是 Object 构造函数的原型 在往上就是 null
    ```xml
        class Point{
            constructor(x,y){
                this.x=x
                this.y=y
            }
            tostring(){
                return `(${this.x},${this.y})`
            }
        }
        let p =new Point(1,2)
        console.log(p)
        console.log(p.toString())
    ```
- Point 类除了构造方法，还定义了一个toString()方法。注意，定义toString()方法的时候，前面不需要加上function这个关键字，直接把函数定义放进去了就可以了。另外，方法与方法之间不需要逗号分隔，加了会报错。
6. constructor 方法默认返回实例对象（即this）也可以返回其他对象即在 constructor 内 return 一个对象
    ```javaScript
        class Foo {
            constructor() {
                return Object.create(null);
            }
        }

        const foo = new Foo()
        console.log(foo);//No properties
    ```
### class和自定义类型的区别
- class的声明不会提升，与let类似
- class的声明自动运行于严格模式之下
- class声明的方法不可枚举（显著区别）
- class的内部方法没有[[construct]]属性，无法new
- 调用class的构造函数必须new
- class内部方法不能同名
### 注意点
1. class的声明自动运行于严格模式之下
2. class的声明不会提升，与let类似
3. name属性总是返回紧跟在class关键字后面的类名
    ```javaScript
        class Point {}
        Point.name // "Point"
    ```
4. this 的指向
    - 类的方法内部如果含有this，它默认指向类的实例。但是，必须非常小心，一旦单独使用该方法，很可能报错。
### 静态方法
- 类相当于实例的原型，所有在类中定义的方法，都会被实例继承。如果在一个方法前，加上static关键字，就表示该方法不会被实例继承，但是可以被类继承，而是直接通过类来调用，这就称为“静态方法”
```javaScript
    class Foo {
    static classMethod() {
        return 'hello';
    }
    }

    console.log(Foo.classMethod()); // 'hello'

    var foo = new Foo();
    console.log(foo.classMethod());//会报错，无法调用
```
- Foo类的classMethod方法前有static关键字，表明该方法是一个静态方法，可以直接在Foo类上调用（Foo.classMethod()），而不是在Foo类的实例上调用。如果在实例上调用静态方法，会抛出一个错误，表示不存在该方法。
- 父类的静态方法，可以被子类继承。
```javaScript
    class Foo {
    static classMethod() {
        return 'hello';
    }
    }

    class Bar extends Foo {
    }

    Bar.classMethod() // 'hello'
```
### 类的继承
- 优点
    - 减少代码冗余 父类可以为子类提供通用的属性，而不必因为增加功能，而逐个修改子类的属性
    - 代码复用 同上
    - 代码易于管理和扩展 子类在父类基础上，可以实现自己的独特功能
- 缺点
    - 耦合度高 如果修改父类代码，将影响所有继承于它的子类
    - 影响性能 子类继承于父类的数据成员，有些是没有使用价值的。但是，在实例化的时候，已经分配了内存。所以，在一定程度上影响程序性能。
- 可以扩充  增加新的方法 属性等
- 子class中如果父class有constructor必须用super方法调用父class类
    ```javaScript
        class Point {
            constructor(x, y) {
                this.x = x
                this.y = y
            }
            tostring() {
                return `我的坐标为(${this.x},${this.y})`
            }
        }
        class ColorPoint extends Point {
            constructor(x, y, color) {
                super(x, y)
                this.color = color
            }
            say() {
                return `I'm ${this.color}`
            }
        }
        let colorP = new ColorPoint(1, 1, "red")
        console.log(colorP.tostring());
        console.log(colorP.say());
    ```