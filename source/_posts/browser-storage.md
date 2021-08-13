---
title: 浏览器存储
date: 2021-05-15 18:54:56
tags: 浏览器
categories: 浏览器
---

## 在浏览器存储数据

> 日常开发中,难免会遇到一些要求浏览器储存一些数据的需求.目前常用的储存方法有:

1. localStorage
    - 生命周期是永久的，这意味着除非用户显示在浏览器提供的UI上清除 localStorage 数据，否则这些数据将永远存在。

2. sessionStorage
    - 生命周期为当前窗口或标签页，一旦窗口或标签页被永久关闭了，那么所有通过 sessionStorage 存储的数据也就被清空了。

### 使用


1. 存储数据
    - sessionStorage.setItem('name',value)
    - localStorage.setItem('name',value)


2. 获取数据

    - let array = sessionStorage.valueOf() //获取全部数据
    - sessionStorage.getItem('name') //获取指定name的值
    - localStorage 用法相同


3. 删除数据
    - sessionStorage.removeItem('name') //删除指定名字的数据
    - sessionStorage.clear() //清楚所有 sessionStorage 信息

    
4. 共享数据
    - 不同浏览器无法共享 localStorage 或 sessionStorage 中的信息。相同浏览器的不同页面间可以共享相同的 localStorage（页面属于相同域名和端口），但是不同页面或标签页间无法共享 sessionStorage 的信息。这里需要注意的是，页面及标 签页仅指顶级窗口，如果一个标签页包含多个 iframe 标签且他们属于同源页面，那么他们之间是可以共享 sessionStorage 的。