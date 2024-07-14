---
title: LC-除自身以外数组的乘积
published: 2024-07-10
description: ''
image: ''
tags: [LeetCode]
category: '算法练习'
draft: false 
---



# 题目描述

给你一个整数数组 `nums`，返回 数组 `answer` ，其中 `answer[i]` 等于 `nums` 中除 `nums[i]` 之外其余各元素的乘积 。

题目数据 **保证** 数组 `nums`之中任意元素的全部前缀元素和后缀的乘积都在 **32 位** 整数范围内。



# 示例

**示例 1:**

```
输入: nums = [1,2,3,4]
输出: [24,12,8,6]
```

**示例 2:**

```
输入: nums = [-1,1,0,-3,3]
输出: [0,0,9,0,0]
```



# 数据范围

- `2 <= nums.length <= 105`
- `-30 <= nums[i] <= 30`
- **保证** 数组 `nums`之中任意元素的全部前缀元素和后缀的乘积都在 **32 位** 整数范围内



# 思路

+ 分类讨论：
	+ 如果没有0，则正常计算
	+ 如果有一个0，则对应位置的答案为其他数的乘积之和
	+ 如果有2个以上的0，结果全为0



# 代码

```typescript
function productExceptSelf(nums: number[]): number[] {
    let res: number[] = new Array(nums.length).fill(0);
    let mul = 1;
    let zero1 = nums.indexOf(0);
    let zero2 = nums.lastIndexOf(0);
    if(zero1 === zero2 && zero1!== -1) {    // 只有一个0
        for(let i = 0; i < nums.length; i++) {
            if(i !== zero1) mul *= nums[i];
        }

        res[zero1] = mul;
        return res;
    }else if(zero1 === -1 && zero2 === -1) {   // 没有0

        for(let i = 0; i < nums.length; i++) mul *= nums[i];

        for(let i = 0; i < nums.length; i++) {
            res[i] = mul / nums[i];
        }
        return res;
    }else{  // 2个0及以上
        return res;
    }
};
```

