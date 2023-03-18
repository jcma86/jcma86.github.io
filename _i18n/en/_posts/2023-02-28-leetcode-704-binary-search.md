---
title: Binary Search
platform: LeetCode
number: 704
author: jose
layout: post
language: en
date: 2023-02-28 22:45 +0300
categories: [programming, bs]
tags: [c/c++, contests, leetcode, binary search]
difficulty: easy
source: https://leetcode.com/problems/binary-search
proglang: C/C++
math: true
mermaid: true
pin: true
# image:
#   path: https://user-images.githubusercontent.com/36547915/97088991-45da5d00-1652-11eb-900f-80d106540f4f.png
#   lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
#   alt: Responsive rendering of Chirpy theme on multiple devices.
---
## Problem
---
Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.  

You must write an algorithm with `O(log n)` runtime complexity.  

## Examples
---
### **Example 1:**  
>**Input:** nums = [-1,0,3,5,9,12], target = 9  
>**Output:** 4
>**Explanation:** 9 exists in nums and its index is 4  

### **Example 2:**  
>**Input:** nums = [-1,0,3,5,9,12], target = 2  
>**Output:** -1  
>**Explanation:** 2 does not exist in nums so return -1  

## Constraints
---
- <code>1 <= nums.length <= 10<sup>4</sup></code>
- <code>-10<sup>4</sup> < nums[i], target < 10<sup>4</sup></code>
- All the integers in `nums` are **unique**.
- `nums` is sorted in ascending order.

## Solution
---
```c++
class Solution {
public:
  int search(vector<int>& nums, int target) {
    int low = 0;
    int high = nums.size() - 1;
    int mid;

    while (low <= high) {
      mid = (low + high) / 2;

      if (nums[mid] == target)
        return mid;
            
      if (nums[mid] > target)
        high = mid - 1;
      else
        low = mid + 1;
    }

    return -1;   
  }
};
```
