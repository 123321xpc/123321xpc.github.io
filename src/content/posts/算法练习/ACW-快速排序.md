---
title: Acwing-快速排序
published: 2024-07-05
description: ''
image: ''
tags: [LeetCode, 快速排序]
category: '算法练习'
draft: false 
---



# 快速排序要点

1. 确定分界点（基准值）：`q[l] | q[(l + r) / 2] | q[r] | 随机点`
2. 调整2个区间的数，使得一个区间的数全部小于基准值，另一个区间的数全部大于基准值。
3. 递归执行1，2



# 题目

给定你一个长度为 n𝑛 的整数数列。

请你使用快速排序对这个数列按照从小到大进行排序。

并将排好序的数列按顺序输出。



# 示例

#### 输入样例：

```
5
3 1 2 4 5
```

#### 输出样例：

```
1 2 3 4 5
```



# 数据范围

+ `1 ≤ n ≤ 100000`



# 代码

```cpp
#include<bits/stdc++.h>
using namespace std;

const int N = 100010;

int q[N];

// 快排模板，防止边界问题
void quick_sort(int q[], int l, int r)
{
    if (l >= r) return;

    int i = l - 1, j = r + 1, x = q[l + r >> 1];
    while (i < j)
    {
        do i ++ ; while (q[i] < x);
        do j -- ; while (q[j] > x);
        if (i < j) swap(q[i], q[j]);
    }

    quick_sort(q, l, j);
    quick_sort(q, j+1, r);
}

int main()
{
    int n;
    scanf("%d", &n);

    for (int i = 0; i < n; i ++ ) scanf("%d", &q[i]);

    quick_sort(q, 0, n - 1);

    for (int i = 0; i < n; i ++ ) printf("%d ", q[i]);

    return 0;
}

```

