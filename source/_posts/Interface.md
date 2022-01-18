---
title: 关于接口的一些问题
date: 2022-01-18 17:46:00
tags: JavaScript
categories: JavaScript
---

### 后端返回数据直接渲染时，遇到了如下问题

> 数据需要循环渲染，而且返回的是一个对象

```js
// 这是后台返回的数据
const res = { type: 'TEXT', key: '222222', value: '213123' }
```

#### 那么要怎么循环呢？

> 经过思考发现了如下方法

```js
const keyList = Object.keys(res)
```

#### 具体渲染方法如下

- 循环的数组为 keyList
- 展示的 key 直接用 item 显示
- 展示的 value 需要用 res[item] 的方式显示
