---
title: LC-跳跃游戏1
published: 2024-07-08
description: ''
image: ''
tags: [LeetCode]
category: '算法练习'
draft: false 
---





# 题目描述

给你一个非负整数数组 `nums` ，你最初位于数组的 **第一个下标** 。数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个下标，如果可以，返回 `true` ；否则，返回 `false` 。



# 示例

**示例 1：**

```
输入：nums = [2,3,1,1,4]
输出：true
解释：可以先跳 1 步，从下标 0 到达下标 1, 然后再从下标 1 跳 3 步到达最后一个下标。
```

**示例 2：**

```
输入：nums = [3,2,1,0,4]
输出：false
解释：无论怎样，总会到达下标为 3 的位置。但该下标的最大跳跃长度是 0 ， 所以永远不可能到达最后一个下标。
```





# 数据范围

- `1 <= nums.length <= 104`
- `0 <= nums[i] <= 105`





# 思路

+ 每走一步，更新目前为止能走到的最远距离。`maxv = nums[i] + i`
+ 如果当前距离大于所记录的最远距离，则返回`false`
+ 如果最远距离大于等于数组长度，则返回`true`



# 代码

```typescript
function canJump(nums: number[]): boolean {
    let maxv = nums[0];
    for (let i = 0; i < nums.length; i++) {

        if(i > maxv) return false;
        maxv = Math.max(maxv, nums[i] + i);

        if(maxv >= nums.length - 1) return true;
    }

    return false;
};
```

