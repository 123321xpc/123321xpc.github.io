---
title: LC-买卖股票的最佳时机
published: 2024-07-07
description: ''
image: ''
tags: [LeetCode]
category: '算法练习'
draft: false 
---





# 题目描述

给定一个数组 `prices` ，它的第 `i` 个元素 `prices[i]` 表示一支给定股票第 `i` 天的价格。

你只能选择 **某一天** 买入这只股票，并选择在 **未来的某一个不同的日子** 卖出该股票。设计一个算法来计算你所能获取的最大利润。

返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 `0` 。





# 示例

**示例 1：**

```
输入：[7,1,5,3,6,4]
输出：5
解释：在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。
```

**示例 2：**

```
输入：prices = [7,6,4,3,1]
输出：0
解释：在这种情况下, 没有交易完成, 所以最大利润为 0。
```





# 数据范围

- `1 <= prices.length <= 105`
- `0 <= prices[i] <= 104`





# 思路

+ 等价为：数组中找出2个数，2个数的差值最大，且左侧的数小于右侧。
+ 设置一个变量`minv`储存当前以及之前所有数的最小值
+ 每遍历一个数，就与`minv`做差比较一次，并更新`minv`



# 代码

```typescript
function maxProfit(prices: number[]): number {
    let minv = 0;
    let res = 0;
    for (let i = 0; i < prices.length; i++) {
        res = Math.max(res, prices[i] - minv);
        minv = Math.min(minv, prices[i]);
    }
    
    return res;
};
```

