---
title: Shortest Subarray with Sum at Least K
platform: LeetCode
number: 862
author: jose
layout: post
language: en
date: 2023-02-24 12:00 +0300
categories: [programming, ps]
tags: [algorithms, c/c++, contests, leetcode, prefix sum, deque]
difficulty: hard
source: https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k/
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
Given an integer array `nums` and an integer `k`, return *the length of the shortest non-empty **subarray** of `nums` with a sum of at least `k`*. If there is no such **subarray**, return `-1`.  

A **subarray** is a **contiguous** part of an array.  

## Examples
---
### **Example 1:**  
>**Input:** nums = [1], k = 1  
>**Output:** 1  

### **Example 2:**  
>**Input:** nums = [1,2], k = 4  
>**Output:** -1  

### **Example 3:**  
>**Input:** nums = [2,-1,2], k = 3  
>**Output:** 3  

## Constraints
---
- <code>1 <= nums.length <= 10<sup>5</sup></code>
- <code>-10<sup>5</sup> <= nums[i] <= 10<sup>5</sup></code>
- <code>1 <= k <= 10<sup>9</sup></code>

## Solution
---
```c++
class Solution {
public:
  int shortestSubarray(vector<int>& nums, int k) {
    deque<int> dq;
    vector<long long> pSum(nums.size(), 0);
    long long sum = 0;

    int minSize = nums.size() + 1;
    for(int i=0; i<nums.size(); i+=1) {
      sum += nums[i];
      pSum[i] = sum;

      if (pSum[i] >= k)
        minSize = min(minSize, i + 1);

      while(!dq.empty() && pSum[i] - pSum[dq.front()] >= k) {
        minSize = min(minSize, i - dq.front());
        dq.pop_front();
      }

      while(!dq.empty() && pSum[dq.back()] >= pSum[i])
        dq.pop_back();

      dq.push_back(i);
    }

    return minSize == nums.size() + 1 ? -1 : minSize;
  }
};
```
