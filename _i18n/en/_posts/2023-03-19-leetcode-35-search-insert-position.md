---
title: Search Insert Position
platform: LeetCode
number: 35
author: jose
layout: post
language: en
date: 2023-03-19 19:20 +0300
categories: [programming, bs]
tags: [c/c++, leetcode, bs]
difficulty: easy
source: https://leetcode.com/problems/search-insert-position/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.  

You must write an algorithm with `O(log n)` runtime complexity.  

## Examples
---
### **Example 1:**
>**Input:** nums = [1,3,5,6], target = 5  
>**Output:** 2  

### **Example 2:**
>**Input:** nums = [1,3,5,6], target = 2  
>**Output:** 1  

### **Example 3:**
>**Input:** nums = [1,3,5,6], target = 7  
>**Output:** 4  

## Constraints
---
- <code>1 <= nums.length <= 10<sup>4</sup></code>  
- <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>  
- `nums` contains **distinct** values sorted in **ascending** order.
- <code>-10<sup>4</sup> <= target <= 10<sup>4</sup></code>  

## Solution
---
Binary search,  
- If number found, return the index.  
- If number was not found, return the last value of the `left` pointer of the binary search. (Verify if the value at that index is greater than the target).  

```c++
class Solution {
public:
  int searchInsert(vector<int>& nums, int target) {
    int l = 0;
    int r = nums.size() - 1;
    
    while (l<r) {
      int m = (l + r) / 2;
      if (nums[m] == target) {
        return m;
      }
      if (nums[m] < target)
        l = m + 1;
      else
        r = m - 1;
    }

    return nums[l] >= target ? l: l+1;
  }
};
```
