---
title: 有关 React-hook 的用法以及“坑”
date: 2021-09-16 19:32:06
tags: React
categories: React
top: true
---

# React-hook
> 当下 React-hook 可以说非常热门，作为正牌小白还是有一些接收和不接受的，下面一 一列举。

### useState

1. State Hook 让函数组件也可以有 state 状态, 并进行状态数据的读写操作
2. 语法: const [xxx, setXxx] = React.useState(默认值)，在引入 React 的前提下 `import React from 'react'`
3. useState()说明:
    - 参数: 第一次初始化指定的值在内部作缓存
    - 返回值: 包含2个元素的数组, 第1个为内部当前状态值, 第2个为更新状态值的函数
4. setXxx()2种写法:
    - setXxx(newValue): 参数为非函数值, 直接指定新的状态值, 内部用其覆盖原来的状态值
    - setXxx(value => newValue): 参数为函数, 接收原本的状态值, 返回新的状态值, 内部用其覆盖原来的状态值
5. 一个小水坑
    - 当想执行 setXxx 的回调的时候，因为 hook 中 setXxx 不支持第二个参数， 这时我们就需要配合 useEffect 通过监听 xxx 来执行 setXxx 的回调

### useEffect

1. Effect Hook 可以让你在函数组件中执行副作用操作(用于模拟类组件中的生命周期钩子)
2. React 中的副作用操作:
    - 发ajax请求数据获取
    - 设置订阅 / 启动定时器
    - 手动更改真实DOM
3. 语法和说明: 
```js
    useEffect(() => { 
            // 在此可以执行任何带副作用操作
            return () => { // 在组件卸载前执行
            // 在此做一些收尾工作, 比如清除定时器/取消订阅等
            }
    }, [stateValue]) // 如果指定的是[], 回调函数只会在第一次render()后执行
```
    
4. 可以把 useEffect Hook 看做如下三个函数的组合
    - componentDidMount()
    - componentDidUpdate()
    - componentWillUnmount() 

### useRef

1. Ref Hook 可以在函数组件中存储/查找组件内的标签或任意其它数据
2. 语法: const refContainer = useRef()
3. 作用:保存标签对象,功能与 React.createRef() 一样

### useHistory

1. useHistory Hook可以在函数组件中存储/查找组件内的标签或任意其它数据
2. 语法: 
```js
    let history = useHistory();
    history.push('/home') // 可以是 replace('home') 或者 goBack() 等等
```
3. 作用: 可以进行路由跳转，这里用起来就比 class 组件方便了

### 后续更新中。。。