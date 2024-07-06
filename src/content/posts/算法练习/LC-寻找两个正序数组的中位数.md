---
title: LeetCode-寻找两个正序数组的中位数
published: 2024-07-05
description: ''
image: ''
tags: [LeetCode, 双指针]
category: '算法练习'
draft: false 
---



# 题目

给定两个大小分别为 `m` 和 `n` 的正序（从小到大）数组 `nums1` 和 `nums2`。请你找出并返回这两个正序数组的 **中位数** 。

算法的时间复杂度应该为 `O(log (m+n))` 。



# 示例

**示例 1：**

```
输入：nums1 = [1,3], nums2 = [2]
输出：2.00000
解释：合并数组 = [1,2,3] ，中位数 2
```

**示例 2：**

```
输入：nums1 = [1,2], nums2 = [3,4]
输出：2.50000
解释：合并数组 = [1,2,3,4] ，中位数 (2 + 3) / 2 = 2.5
```



# 提示

- `nums1.length == m`
- `nums2.length == n`
- `0 <= m <= 1000`
- `0 <= n <= 1000`
- `1 <= m + n <= 2000`
- `-106 <= nums1[i], nums2[i] <= 106`



# 思路

+ 先用双指针合并2个数组（归并排序合并）
+ 最后分情况输出即可



# 代码

```typescript
function findMedianSortedArrays(nums1: number[], nums2: number[]): number {
    let i = 0, j = 0;
    let merge: number[] = [];
    // 合并两个数组
    while(i < nums1.length && j < nums2.length)
    {
        if(nums1[i] <= nums2[j])
            merge.push(nums1[i++]);
        else
            merge.push(nums2[j++]);
    }
    // 合并剩余元素
    while(i < nums1.length)
        merge.push(nums1[i++]);
    while(j < nums2.length)
        merge.push(nums2[j++]);

    let res: number = 0;
    if(merge.length % 2 === 0){ // 偶数个数
        let n1 = merge.length / 2 - 1;
        let n2 = n1 + 1;
        res = (merge[n1] + merge[n2]) / 2;
    }else{  // 奇数个数
        res = merge[(merge.length - 1) / 2];
    }

    // 结果保留5位小数
    return Number.parseFloat(res.toFixed(5));
};
```

