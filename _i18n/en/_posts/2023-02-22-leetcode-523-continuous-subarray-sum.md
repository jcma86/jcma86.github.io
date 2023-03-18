---
title: Continuous Subarray Sum
platform: LeetCode
number: 523
author: jose
layout: post
language: en
date: 2023-02-22 11:00 +0300
categories: [programming, ps]
tags: [algorithms, c/c++, contests, prefix sum, leetcode]
difficulty: medium
source: https://leetcode.com/problems/continuous-subarray-sum/
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
Given an integer array `nums` and an integer `k`, return `true` *if* `nums` *has a **good subarray** or* `false` *otherwise*.  

A **good subarray** is a subarray where:  

- its length is **at least two**, and  
- the sum of the elements of the subarray is a multiple of `k`.  

Note that:  

- A **subarray** is a contiguous part of the array.  
- An integer `x` is a multiple of `k` if there exists an integer `n` such that `x = n * k`. `0` is **always** a multiple of `k`.  

## Examples
---
### **Example 1:**  
>**Input:** nums = [23,2,4,6,7], k = 6  
>**Output:** true  
>  
>**Explanation:** [2, 4] is a continuous subarray of size 2 whose elements sum up to 6.  

### **Example 2:**  
>**Input:** nums = [23,2,6,4,7], k = 6  
>**Output:** true  
>  
>**Explanation:** [23, 2, 6, 4, 7] is an continuous subarray of size 5 whose elements sum up to 42.  
>42 is a multiple of 6 because 42 = 7 * 6 and 7 is an integer.  

### **Example 3:**  
>**Input:** nums = [23,2,6,4,7], k = 13  
>**Output:** false  

## Constraints
---
- <code>1 <= nums.length <= 10<sup>5</sup></code>
- <code>0 <= nums[i] <= 10<sup>9</sup></code>
- <code>0 <= sum(nums[i]) <= 2<sup>31</sup> - 1</code>
- <code>1 <= k <= 2<sup>31</sup> - 1</code>

## Solution
---
```c++
class Solution {
public:
  bool checkSubarraySum(vector<int>& nums, int k) {
    int sum = 0;
    unordered_map<int, int> hashmods{{0, 0}};
    for (int i = 0; i < nums.size(); i+= 1) {
      sum += nums[i];
      int mod = sum % k;
      if (!hashmods.count(mod))
        hashmods[mod] = i + 1;
      else if (hashmods[mod] < i)
        return true;
    }

    return false;
  }
};
```