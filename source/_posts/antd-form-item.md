---
title: AntD 表单无数据问题
date: 2021-09-16 19:07:12
tags: AntD
categories: AntD
---

# 提出问题（问题怎么那么多）

> 有时 form.item 的初始值和我们理想的不尽相同

### 真实场景

- 有时 form.item 绑定的数据的值需要从后台接口获取，这时 from.item 的 initialValue 就成了对应数据的初始值，可能是空串、数值0、空数组……
- 这时显示出来的数据就会是空串、数值0、空数组……

# 解决问题（查了很多资料后终于解决）

### 设定场景

- 当在 react-hook 环境中，我们可以这样
    ```js
        React.useEffect(() => {
            form.resetFields()
        }, [form.item 的某个 value 绑定的变量])
    ```
- 通过监听变量值的变化，值发送改变后清除原来的值，把新的值重新渲染上去，就解决了。