---
title: 渲染函数 & jsx
date: 2021-06-01 09:30:41
tags: Vue
categories: Vue
---
### 介绍渲染函数（render）
- 在 vue 中我们使用模板 HTML 语法组建页面的，使用 render 函数我们可以用 js 语言来构建 DOM。
- 因为 vue 是虚拟 DOM ，所以在拿到 template 模板时也要转译成 VNode 的函数，而用 render 函数构建 DOM ， vue 就免去了转译的过程，也就是如果使用渲染函数 render 时需要将 template 部分删除，因为 render 函数，可以帮我们创建 template。
- 当使用 render 函数描述虚拟 DOM 时， vue 提供一个函数，这个函数是就构建虚拟 DOM 所需要的工具。官网上给他起了个名字叫 createElement。一般简写为 h。
### 使用渲染函数（render）
```xml
    render(createElement){
        return createElement(
        // {String | Object | Function}
        // 一个 HTML 标签字符串，组件选项对象，或者解析上述任何一种的一个 async 异步函数，必要参数。
        // 可以写成字符串拼接的标签名
        'div',

        // {Object}
        // 一个包含模板相关属性的数据对象这样，您可以在 template 中使用这些属性。可选参数。
        // 该对象内可以设置 class style 事件绑定prop插槽...
        {
            // (详情见下一节)
        },

        // {String | Array}
        // 子节点 (VNodes)，由 `createElement()` 构建而成，
        // 或使用字符串来生成“文本节点”。可选参数。
        [
            '先写一些文字',
            createElement('h1', '一则头条'),
            createElement(MyComponent, {
                props: {
                    someProp: 'foobar'
                }
            })
        ]
        )
    }
```
### 举例渲染函数（render）
- 为什么使用 render 函数？
- 什么情况下使用 render 函数？
- 创建一个等级标题组件 根据不同的 level 创建不同的 标题
    ```javaScript
        // 如果不使用 render 使用 插槽
        <template>
        <h1 v-if="Level === 1">
            <slot />
        </h1>
        <h2 v-else-if="Level === 2">
            <slot />
        </h2>
        <h3 v-else-if="Level === 3">
            <slot />
        </h3>
        </template>
        export default {
            props: ["Level"],
        };
        </script>
        // 这里用模板并不是最好的选择：不但代码冗长，而且在每一个级别的标题中重复书写了 <slot></slot>，在要插入锚点元素时还要再次重复。虽然模板在大多数组件中都非常好用，但是显然在这里它就不合适了。那么，我们来尝试使用 render 函数重写上面的例子
    ```
- 如果使用 render 函数
    ```javaScript
        export default {
            props: ["Level"],
            render() {
                const tag = "h" + this.Level;
                return <tag>{this.$slots.default}</tag>;
            },
        };
        </script>
        // 看起来简单多了！这样代码精简很多，但是需要非常熟悉 Vue 的实例 property。
    ```