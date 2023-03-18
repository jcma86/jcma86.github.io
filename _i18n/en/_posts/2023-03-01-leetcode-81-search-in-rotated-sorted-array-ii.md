---
title: Search in Rotated Sorted Array II
platform: LeetCode
number: 81
author: jose
layout: post
language: en
date: 2023-03-01 22:00 +0300
categories: [programming, bs]
tags: [c/c++, contests, leetcode, binary search]
difficulty: medium
source: https://leetcode.com/problems/search-in-rotated-sorted-array
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
There is an integer array `nums` sorted in non-decreasing order (not necessarily with **distinct** values).

Before being passed to your function, `nums` is rotated at an unknown pivot index `k` (`0 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,4,4,5,6,6,7]` might be rotated at pivot index `5` and become `[4,5,6,6,7,0,1,2,4,4]`.  

Given the array `nums` **after** the rotation and an integer `target`, return *`true` if `target` is in `nums`, or `false` if it is not in `nums`.*  

You must decrease the overall operation steps as much as possible.  

## Examples
---
### **Example 1:**  
>**Input:** nums = [2,5,6,0,0,1,2], target = 0  
>**Output:** true

### **Example 2:**  
>**Input:** nums = [2,5,6,0,0,1,2], target = 3  
>**Output:** false

## Constraints
---
- `1 <= nums.length <= 5000`  
- <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
- `nums` is guaranteed to be rotated at some pivot.  
- <code>-10<sup>4</sup> <= target <= 10<sup>4</sup></code>  

## Solution
---
Solution is same as in problem [#33]({{site.url}}/posts/2023/03/01/leetcode-33-search-in-rotated-sorted-array/), the only difference is that numbers can be repeated so:
  - While lower index `<` higher index:
    - While the value at the lower index is equal to the next one, move the lower index up.
    - While the value at the higher index is equal to the previous one, move the higher index down.
  - Perform binary search as in problem [#33]({{site.url}}/posts/2023/03/01/leetcode-33-search-in-rotated-sorted-array/)


```c++
class Solution {
public:
  int search(vector<int>& nums, int target) {
    int l = 0;
    int h = nums.size() - 1;
    int m;
        
    while (l <= h) {
      while (l < h && nums[l] == nums[l+1])
        l ++;
      while (h > l && nums[h] == nums[h-1])
        h --;

      m = (l + h) / 2;
      if (nums[m] == target)
        return true;

      if (nums[l] <= nums[m]) {
        if (target <= nums[m] && target >= nums[l])
          h = m - 1;
        else
          l = m + 1;
      } else {
        if (target >= nums[m] && target <= nums[h])
          l = m + 1;
        else
          h = m - 1;
      }
    }
    return false;
  }
};
```
