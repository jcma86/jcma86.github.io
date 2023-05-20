---
title: Minimum Size Subarray Sum
platform: LeetCode
number: 209
author: jose
language: en
languages: ["en"]
date: 2023-02-20 11:33:00 +0300
categories: [programming, ps]
tags: [algorithms, c/c++, contests, leetcode, ps]
difficulty: medium
source: https://leetcode.com/problems/minimum-size-subarray-sum/
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
Given an array of positive integers `nums` and a positive integer `target`, return *the **minimal length** of a subarray whose sum is greater than or equal to* `target`. If there is no such subarray, return `0` instead.

## Examples
---
### **Example 1:**  
>**Input:** target = 7, nums = [2,3,1,2,4,3]  
>**Output:** 2  
>**Explanation:** The subarray [4,3] has the minimal length under the problem constraint.

### **Example 2:**  
>**Input:** target = 4, nums = [1,4,4]  
>**Output:** 1

### **Example 3:**  
>**Input:** target = 11, nums = [1,1,1,1,1,1,1,1]  
>**Output:** 0

## Constraints
---
- <code>1 <= target <= 10<sup>9</sup></code>  
- <code>1 <= nums.length <= 10<sup>5</sup></code>  
- <code>1 <= nums[i] <= 10<sup>4</sup></code>

## Solution
---
```c++
class Solution {
public:
  int minSubArrayLen(int target, vector<int>& nums) {
    int min = nums.size() + 1;
    int sum = 0;
    int start = 0;

    for(int i=0; i<nums.size(); i++) {
      sum += nums[i];
      while (sum >= target && start < i) {
        if (sum - nums[start] >= target) {
          sum -= nums[start];
          start += 1; 
        }
        else
          break;
      }
      int s = (i+1) - start;
      if (sum >= target && s < min)
        min = s;   
    }
      
    return min == nums.size() + 1 ? 0 : min;
  }
};
```
