---
title: 3Sum Closest
platform: LeetCode
number: 16
author: jose
layout: post
language: en
date: 2023-03-16 18:30 +0300
categories: [programming, twopointers]
tags: [c/c++, leetcode, twopointers]
difficulty: medium
source: https://leetcode.com/problems/3sum-closest/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given an integer array `nums` of length `n` and an integer `target`, find three integers in `nums` such that the sum is closest to `target`.  

Return *the sum of the three integers*.  

You may assume that each input would have exactly one solution.  

## Examples
---
### **Example 1:**  
>**Input:** nums = [-1,2,1,-4], target = 1  
>**Output:** 2  
>**Explanation:**  The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).  
  
### **Example 2:**  
>**Input:** nums = [0,0,0], target = 1  
>**Output:** 0  
>**Explanation:** The sum that is closest to the target is 0. (0 + 0 + 0 = 0).  

## Constraints
---
- `3 <= nums.length <= 500`  
- `-1000 <= nums[i] <= 1000`  
- <code>-10<sup>4</sup> <= target <= 10<sup>4</sup></code>  

## Solution
---
We will use a Two Pointers technique. See the [LeetCode Problem 15](../leetcode-15-3sum/).  
Some particular things for this problem:  
  - If the sum of the three numbers is equal to the target, we return that value.  
  - After adding the three numbers, we get the absolute difference with the `target` and update the closest value found.  

```c++
class Solution {
public:
  int threeSumClosest(vector<int>& nums, int target) {
    int sum = 0;
    int closest = INT_MAX/2;

    sort(nums.begin(), nums.end());
    for (int i=0; i<nums.size()-2; i++) {
      if (i>0 && nums[i] == nums[i-1])
        continue;
        
      int l = i + 1;
      int r = nums.size() - 1;
      while (l<r) {
        sum = nums[i] + nums[l] + nums[r];
        if (sum == target)
          return sum;
          
        if (abs(sum - target) < abs(closest - target))
          closest = sum;
          
        if (sum < target)
          l++;
        else
          r--;
      }
    }

    return closest;
  }
};
```
