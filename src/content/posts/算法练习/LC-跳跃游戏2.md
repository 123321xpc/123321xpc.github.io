---
title: LC-跳跃游戏2
published: 2024-07-08
description: ''
image: ''
tags: [LeetCode, BFS]
category: '算法练习'
draft: false 
---



# 题目描述

给定一个长度为 `n` 的整数数组 `nums`。初始位置为 `nums[0]`。

每个元素 `nums[i]` 表示从索引 `i` 向前跳转的最大长度。换句话说，如果你在 `i` 处，你可以跳转到任意 `[i, i + num[i]]` 处:

返回到达 `nums[n - 1]` 的最小跳跃次数。生成的测试用例必定可以到达 `nums[n - 1]`。



# 示例

**示例 1:**

```
输入: nums = [2,3,1,1,4]
输出: 2
解释: 跳到最后一个位置的最小跳跃数是 2。
     从下标为 0 跳到下标为 1 的位置，跳 1 步，然后跳 3 步到达数组的最后一个位置。
```

**示例 2:**

```
输入: nums = [2,3,0,1,4]
输出: 2
```





# 数据范围

- `1 <= nums.length <= 104`
- `0 <= nums[i] <= 1000`
- 题目保证可以到达 `nums[n-1]`



# 思路

+ `BFS`求最短路



# 代码

```typescript
function jump(nums: number[]): number {
    let n = nums.length;    
    let st = new Array(n).fill(Infinity);   // 初始化步数数组
    st[0] = 0;  // 起点步数为0
    let q : [number, number][] = [];    // 队列
    q.push([0, nums[0]]);
    
    while (true) {
        let t = q.shift();
        if(t === undefined) break;
        for(let i = 1; i <= t[1]; i++) {
            let index = t[0] + i;
            if(index === n - 1) return st[t[0]] + 1;    // 第一次到达终点必为最短路径
            if(index > n - 1) break;    // 由于从小到大枚举，如果超出终点,之后必定继续超出范围，可以直接退出循环
            if(st[index] > st[t[0]] + 1) {    // 如果当前步数比之前的步数少，则更新步数
                st[index] = st[t[0]] + 1;
                q.push([index, nums[index]]);
            }
        }
    }

    return st[n - 1];
};
```

