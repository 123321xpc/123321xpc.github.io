---
title: LC-轮转数组
published: 2024-07-07
description: ''
image: ''
tags: [LeetCode]
category: '算法练习'
draft: false 
---





# 题目描述

给定一个整数数组 `nums`，将数组中的元素向右轮转 `k` 个位置，其中 `k` 是非负数。

 

# 示例

**示例 1:**

```
输入: nums = [1,2,3,4,5,6,7], k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右轮转 1 步: [7,1,2,3,4,5,6]
向右轮转 2 步: [6,7,1,2,3,4,5]
向右轮转 3 步: [5,6,7,1,2,3,4]
```

**示例 2:**

```
输入：nums = [-1,-100,3,99], k = 2
输出：[3,99,-1,-100]
解释: 
向右轮转 1 步: [99,-1,-100,3]
向右轮转 2 步: [3,99,-1,-100]
```



# 数据范围

- `1 <= nums.length <= 105`
- `-231 <= nums[i] <= 231 - 1`
- `0 <= k <= 105`





# 思路

+ 使用3次反转。
+ 以`[1, 2, 3, 4, 5]， k = 3`为例
	+ 最终1要到4的位置，即下标为3的位置
	+ 所以第1次反转后，1要到与4对称的地方，即2的位置
	+ 故第一次反转的区间为`[0, 1]`，剩下为第二次反转
	+ 则第一次反转区间右端点`r = nums.length - k - 1`（因为下标从0开始，所以要多减1）



# 代码

```typescript
function rotate(nums: number[], k: number): void {
    // 先取模
    k %= nums.length;
    k = nums.length - k - 1;

    function reverse(l: number, r: number): void {
        let i = l, j = r;

        while(i < j) 
        {
            let t = nums[i];
            nums[i] = nums[j];
            nums[j] = t;
            i++; j--;
        }
    }

    reverse(0, k);
    reverse(k + 1, nums.length - 1);
    reverse(0, nums.length - 1);
};
```

