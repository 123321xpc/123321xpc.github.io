---
title: LeetCode-无重复字符的最长子串
published: 2024-07-05
description: ''
image: ''
tags: [LeetCode, 双指针]
category: '算法练习'
draft: false 
---



# 题目

给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串** 的长度



# 示例

**示例 1:**

```
输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 2:**

```
输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

**示例 3:**

```
输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```



# 提示

- `0 <= s.length <= 5 * 104`
- `s` 由英文字母、数字、符号和空格组成



# 思路

+ 双指针。
+ 用一个哈希表，右指针指向当前元素，查找哈希表中是否有该元素。若无则直接加入，若有则移动左指针并删除左指针指向的元素，直到哈希表中无当前元素为止。
+ 右指针每走一步，比较字符串长度，保存下来。



# 代码

```typescript
function lengthOfLongestSubstring(s: string): number {
    if(s.length < 2) return s.length;   // 特判0和1长度的字符串

    let i = 0, j = 1;
    let res = 1;
    let hash = new Set<string>();   // 哈希表
    hash.add(s[0]);    // 先添加第一个字符到哈希表中
    while(j < s.length)
    {
        if(!hash.has(s[j])) // 若无，则直接加入哈希表
            hash.add(s[j]);
        else{   // 有，则移动左指针
            while(hash.has(s[j])) hash.delete(s[i++]);
            hash.add(s[j]);
        }
        res = Math.max(res, j - i + 1); // 更新最大长度
        j++;
    }

    return res;
};
```

