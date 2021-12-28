---
title: 循环生成图片不重复
date: 2021-12-28 14:12:35
tags: Vue
categories: Vue
---

# 关于 Vue 中循环生成图片方法

### 先上基础

- 在 Vue 中 img 图片的 src 的路径有两种索引方法：
  1. 可以直接 `<img src="路径" alt="一张图片">`
  2. 在 data 中 imgSrc: require('图片路径') 然后 `<img :src="imgSrc" alt="一张图片">`

### 提出问题

- 那么如果想循环生成不同图片该怎么办？

### 思考一会儿。。。

- 思考半天后

### 解决问题

- 可以通过生成对象的方式解决问题如下：
  1. 在循环组件中定义如下结构
  ```js
    imgSrc: {
        imgSrc1: require('路径1'),
        imgSrc2: require('路径2'),
        imgSrc3: require('路径3'),
        imgSrc4: require('路径4'),
        imgSrc5: require('路径5')
      }
  ```
  2. 循环时需要传递相对应的 变量名称(字符串类型)
  3. 循环结构写 `<img :src="imgSrc[item.imgIndex]" alt="一张图片">`
  - 这里用到了比较基础的地方，imgSrc.imgSrc1 相当于 imgSrc['imgSrc1']
