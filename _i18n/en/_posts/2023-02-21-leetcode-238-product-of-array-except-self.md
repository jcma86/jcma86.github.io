---
title: Product of Array Except Self
platform: LeetCode
number: 238
author: jose
layout: post
language: en
date: 2023-02-21 11:33:00 +0300
categories: [programming, ps]
tags: [algorithms, c/c++, contests, leetcode, prefix sum]
difficulty: medium
source: https://leetcode.com/problems/product-of-array-except-self/
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
Given an integer array `nums`, return *an array* `answer` *such that* `answer[i]` *is equal to the product of all the elements of* `nums` *except* `nums[i]`.  
  
The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.  
  
You must write an algorithm that runs in `O(n)` time and without using the division operation.  

## Examples
---
### **Example 1:**  
>**Input:** nums = [1,2,3,4]  
>**Output:** [24,12,8,6]  

### **Example 2:**  
>**Input:** nums = [-1,1,0,-3,3]  
>**Output:** [0,0,9,0,0]  

## Constraints
---
- <code>2 <= nums.length <= 10<sup>5</sup></code>  
- `-30 <= nums[i] <= 30`  
- The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

## Solution
---
```c++
class Solution {
public:
  vector<int> productExceptSelf(vector<int>& nums) {
    int s = nums.size() - 1;
    vector<int> sol(nums.size(), 1);
    vector<int> tmp(nums.size(), 1);

    for(int i=1; i<nums.size(); i+=1) {
      int l = nums[i - 1];
      int r = nums[(s - i) + 1];

      sol[i] = sol[i-1]*l;
      tmp[s-i] = tmp[(s-i) + 1] * r;
    }

    for(int i=0; i<nums.size(); i+=1)
      sol[i] *= tmp[i];

    return sol;
  }
};
```
