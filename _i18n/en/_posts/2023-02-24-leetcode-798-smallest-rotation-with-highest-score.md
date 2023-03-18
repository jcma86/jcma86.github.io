---
title: Smallest Rotation with Highest Score
platform: LeetCode
number: 798
author: jose
layout: post
language: en
date: 2023-02-24 09:00 +0300
categories: [programming, ps]
tags: [algorithms, c/c++, contests, leetcode, prefix sum]
difficulty: hard
source: https://leetcode.com/problems/smallest-rotation-with-highest-score/
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
You are given an array `nums`. You can rotate it by a non-negative integer `k` so that the array becomes `[nums[k], nums[k + 1], ... nums[nums.length - 1], nums[0], nums[1], ..., nums[k-1]]`. Afterward, any entries that are less than or equal to their index are worth one point.  

- For example, if we have `nums = [2,4,1,3,0]`, and we rotate by `k = 2`, it becomes `[1,3,0,2,4]`. This is worth `3` points because `1 > 0` [no points], `3 > 1` [no points], `0 <= 2` [one point], `2 <= 3` [one point], `4 <= 4` [one point].  

Return *the rotation index* `k` *that corresponds to the highest score we can achieve if we rotated* `nums` *by it*. If there are multiple answers, return the smallest such index `k`.  

## Examples
---
### **Example 1:**  
>**Input:** nums = [2,3,1,4,0]  
>**Output:** 3  
>**Explanation:** Scores for each k are listed below:  
> k = 0,  nums = [2,3,1,4,0],    score 2  
> k = 1,  nums = [3,1,4,0,2],    score 3  
> k = 2,  nums = [1,4,0,2,3],    score 3  
> k = 3,  nums = [4,0,2,3,1],    score 4  
> k = 4,  nums = [0,2,3,1,4],    score 3  
> So we should choose k = 3, which has the highest score.  

### **Example 2:**  
>**Input:** nums = [1,3,0,2,4]  
>**Output:** 0  
>**Explanation:** nums will always have 3 points no matter how it shifts.  
> So we will choose the smallest k, which is 0.  

## Constraints
---
- <code>1 <= nums.length <= 10<sup>5</sup></code>
- `0 <= nums[i] < nums.length`

## Solution
---
```c++
class Solution {
public:
  int bestRotation(vector<int>& nums) {
    vector<int> points(2 * nums.size() + 1, 0);
    int k = 0;
    int pMax = 0;

    for (int i = 0; i < nums.size(); i += 1) {
      if (nums[i] <= i) {
        points[0] += 1;
        points[(i - nums[i]) + 1] -= 1;
      }
                
      points[i + 1] += 1;
      points[i + (nums.size() - nums[i]) + 1] -= 1;
    }

    pMax = points[0];
    for (int i = 1; i < points.size(); i += 1) {
      points[i] += points[i - 1];
        if (points[i] > pMax) {
          pMax = points[i];
          k = i;
        }
      }
    return k;
  }   
};
```
