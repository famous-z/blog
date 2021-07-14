---
title: 水平垂直居中
date: 2021-05-25 08:21:35
tags: CSS
categories: CSS
---
### 公共代码
- body 如下
```body
    <div class="wrap">
        <div class="box"></div>
    </div>
```
- style 公共样式
```style
    .wrap {
        width: 300px;
        height: 300px;
        border: 1px solid red;
    }

    .box1 {
        width: 100px;
        height: 100px;
        background-color: pink;
    }
```
### 通过定位实现定高定宽的盒子居中
#### 通过宽度和高度
1. 方法一
    - 通过定位方式，设置绝对子元素的 margin-top: -元素高度的一半px
    - style 样式
    ```style
        .wrap {
            position: relative;
        }

        .box1 {
            position: absolute;
            top: 50%;
            left: 50%;
            margin-top: -50px;
            margin-left: -50px;
        }
    ```
2. 方法二
    - 使用 calc() 函数对数值属性执行减法运算
    - css 样式如下
    ```style
        .wrap {
            position: relative;
        }

        .box1 {
            position: absolute;
            top: calc(50% - 50px);
            left: calc(50% - 50px);
        }
    ```
#### 不通过宽度和高度
1. 方法一
    - 使用 margin 居中
    - css 样式如下
    ```style
        .wrap {
            position: relative;
        }

        .box1 {
            position: absolute;
            top: 0;
            left: 0;
            bottom: 0;
            right: 0;
            margin: auto;
        }
    ```
2. 方法二
    - 使用 translate 居中
    - css 样式如下
    ```style
        .wrap {
            position: relative;
        }

        .box1 {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }
    ```
### 通过 flex 布局方式
- css 样式如下
```style
    .wrap {
        display: flex;
        justify-content: center;
        align-items: center
    }
```