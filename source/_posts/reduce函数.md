---
title: reduce函数
date: 2025-08-14 15:16:39
tags:
categories:
- [前端基础知识,JavaScript]
---
在 JavaScript 中，`Array.prototype.reduce()` 是一个强大的数组方法，用于将数组元素**“缩减”为单个值**。它通过遍历数组元素并执行一个回调函数来实现累积计算。

### 基础语法

```javascript
array.reduce(callback(accumulator, currentValue, index, array), initialValue)
```

| 参数           | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| `accumulator`  | 累积值（上一次回调的返回值或初始值）                         |
| `currentValue` | 当前处理的数组元素                                           |
| `index`        | (可选) 当前元素的索引                                        |
| `array`        | (可选) 调用 `reduce` 的原始数组                              |
| `initialValue` | (可选) 作为第一次调用回调时的初始值。**如果省略，默认使用数组第一个元素** |

例子：// 无初始值 → 第一次迭代 acc=1, cur=2 

​     [1, 2, 3].reduce((acc, cur) => acc + cur); // 6 (数字)

​     // 有初始值 → 第一次迭代 acc=[], cur=1 

​    [1, 2, 3].reduce((acc, cur) => [...acc, cur * 2], []); // [2, 4, 6] (数组)

------

### 核心特点

1. **从左到右**遍历数组（`reduceRight()` 从右向左）
2. 返回值可以是任意类型（数字、字符串、对象、数组等）
3. 不改变原数组（纯函数）