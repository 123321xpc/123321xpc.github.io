---
title: LC-H指数
published: 2024-07-10
description: ''
image: ''
tags: [LeetCode, 二分查找]
category: '算法练习'
draft: false 
---





# 题目描述

给你一个整数数组 `citations` ，其中 `citations[i]` 表示研究者的第 `i` 篇论文被引用的次数。计算并返回该研究者的 **`h` 指数**。

h 指数的定义：`h` 代表“高引用次数” ，一名科研人员的 `h` **指数** 是指他（她）至少发表了 `h` 篇论文，并且 **至少** 有 `h` 篇论文被引用次数大于等于 `h` 。如果 `h` 有多种可能的值，**`h` 指数** 是其中最大的那个。





# 示例

**示例 1：**

```
输入：citations = [3,0,6,1,5]
输出：3 
解释：给定数组表示研究者总共有 5 篇论文，每篇论文相应的被引用了 3, 0, 6, 1, 5 次。
     由于研究者有 3 篇论文每篇 至少 被引用了 3 次，其余两篇论文每篇被引用 不多于 3 次，所以她的 h 指数是 3。
```

**示例 2：**

```
输入：citations = [1,3,1]
输出：1
```





# 提示

- `n == citations.length`
- `1 <= n <= 5000`
- `0 <= citations[i] <= 1000`





# 思路

+ 两次二分。
	+ 第一次二分答案
	+ 第二次二分区间，找出数组中第一个大于等于x的数（数组先排序）





# 代码

```typescript
function hIndex(citations: number[]): number {
    // 数组升序排序
    const nums: number[] = citations.sort((a, b) => a - b);

    // 二分查找数组中第一个大于等于x的数
    function check(x: number): boolean {
        
        let L = 0, R = nums.length - 1;
        while(L < R)
        {
            // |0 确保返回整数（向下取整）
            let M = L  +  R >> 1 | 0;
            if(nums[M] < x) L = M + 1;
            else R = M;
        }

        // 如果返回的数小于x，说明数组中没有大于等于x的数，返回false
        if(nums[L] >= x) return nums.length - 1 - L + 1 >= x;
        else return false;
    }

    let l = 0, r = 1000;
    while(l < r)
    {
        let mid = l  +  r + 1 >> 1 | 0;
        
        if(check(mid)) l = mid;
        else r = mid - 1;
    }
    
    return l;
};
```



# 注：各类取整方法

```typescript
const num = 4.7;

console.log(Math.floor(num));  // 向下取整，输出 4
console.log(Math.ceil(num));   // 向上取整，输出 5
console.log(Math.round(num));  // 四舍五入，输出 5
console.log(Math.trunc(num));  // 去除小数部分，输出 4
console.log(num | 0);          // 位运算向下取整，输出 4
```



