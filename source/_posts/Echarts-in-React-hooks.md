---
title: 在React-hooks中使用Echarts
date: 2021-09-19 10:20:13
tags: Echarts
categories: Echarts
top: true
---

# 在 Hook 中使用 Echart

> 在新版 Echart 也就是 5.X 中使用的时候在一次遇到了困难

### 使用方法（在艰辛的查阅资料后终于找到答案）

- 代码外壳
```js
    import { useEffect, useRef } from 'react';
    var echarts = require('echarts');

    function MyChart () {
        const chartRef = useRef()
        let myChart = null
        const option = {
            // 表格配置以及数据
        }

        function renderChart() {
            const chart = echarts.getInstanceByDom(chartRef.current)
            if (chart) {
                myChart = chart
            } else {
                myChart = echarts.init(chartRef.current)
            }
            myChart.setOption(option) 
        }

        useEffect(() => {
            renderChart()
            return () => {
                option && myChart.setOption(option);
            }
        })

        return (
            <>
                <div style={{width: "800px", height: "800px"}} ref={chartRef} />
            </>
        )
    }

    export default MyChart
```