---
title: antdVue中表格操作
date: 2021-05-15 18:54:56
tags: Vue
categories: Vue
---

## table 行添加事件

### 在 table 标签部分添加 :customRow="Rowclick"

> Rowclick 为绑定的事件

### methord 部分如下

```js
  Rowclick (record, index) {
    // record 为这一行的值，index为索引值
      return {
        on: {
          click: () => {},
          dblclick: () => {}
        }
      };
    }
```
