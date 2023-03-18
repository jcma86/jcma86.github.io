---
title: Subarray Sum Equals K
platform: LeetCode
number: 560
author: jose
layout: post
language: en
date: 2023-02-23 11:00 +0300
categories: [programming, ps]
tags: [algorithms, c/c++, contests, leetcode, prefix sum]
difficulty: medium
source: https://leetcode.com/problems/subarray-sum-equals-k
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
Given an array of integers `nums` and an integer `k`, return *the total number of subarrays whose sum equals to* `k`.  

A subarray is a contiguous **non-empty** sequence of elements within an array.  

## Examples
---
### **Example 1:**  
>**Input:** nums = [1,1,1], k = 2  
>**Output:** 2  

### **Example 2:**  
>**Input:** nums = [1,2,3], k = 3  
>**Output:** 2  

## Constraints
---
- <code>1 <= nums.length <= 2 * 10<sup>4</sup></code>
- `-1000 <= nums[i] <= 1000`
- <code>-10<sup>7</sup> <= k <= 10<sup>7</sup></code>

## Solution
---
```c++
class Solution {
public:
  int subarraySum(vector<int>& nums, int k) {
    int count = 0;
    int cSum = 0;

    unordered_map<int,int>m;
    for (int i=0; i<nums.size(); i+=1) {
      cSum += nums[i];
      if (cSum == k)
        count++;

      if (m.find(cSum - k) != m.end())
        count += m[cSum - k];
      
      m[cSum]++;
    }
    return count;
  }
};
```
