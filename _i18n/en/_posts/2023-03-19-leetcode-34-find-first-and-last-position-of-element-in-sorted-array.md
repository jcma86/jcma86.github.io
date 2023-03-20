---
title: Find First and Last Position of Element in Sorted Array
platform: LeetCode
number: 34
author: jose
layout: post
language: en
date: 2023-03-19 19:00 +0300
categories: [programming, bs]
tags: [c/c++, leetcode, bs]
difficulty: medium
source: https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given an array of integers `nums` sorted in non-decreasing order, find the starting and ending position of a given `target` value.  

If `target` is not found in the array, return `[-1, -1]`.  

You must write an algorithm with `O(log n)` runtime complexity.  

## Examples
---
### **Example 1:**
>**Input:** nums = [5,7,7,8,8,10], target = 8  
>**Output:** [3,4]  

### **Example 2:**
>**Input:** nums = [5,7,7,8,8,10], target = 6  
>**Output:** [-1,-1]  

### **Example 3:**
>**Input:** nums = [], target = 0  
>**Output:** [-1,-1]  

## Constraints
---
- <code>0 <= nums.length <= 10<sup>5</sup></code>  
- <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>  
- `nums` is a non-decreasing array.  
- <code>-10<sup>9</sup> <= target <= 10<sup>9</sup></code>  

## Solution
---
We perform two binary searches.
  - Binary search to find the minimum index of the target value.
  - If there is a minimun index, then we perform a binary search to find the maximum index.
    - Because there is a minimum, we can initialize the `left` pointer to the first position where the target was found for the first time.

```c++
class Solution {
public:
  vector<int> searchRange(vector<int>& nums, int target) {
    int start = -1;
    int end = -1;

    int l = 0;
    int r = nums.size() - 1;
    while (l<=r) {
      int m = (l + r) / 2;
      if (nums[m] == target) {
        start = m;
        end = max(end, m);
      }
      if (nums[m] >= target)
        r = m - 1;
      else
        l = m + 1;
    }

    if (end != -1) {
      l = end;
      r = nums.size() - 1;
      while (l<=r) {
        int m = (l + r) / 2;
        if (nums[m] == target)
          end = max(end, m);
        if (nums[m] <= target)
          l = m + 1;
        else
          r = m - 1;
      }
    }

    return {start, end};
  }
};
```
