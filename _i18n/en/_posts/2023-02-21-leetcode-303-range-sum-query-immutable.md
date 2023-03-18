---
title: Range Sum Query - Immutable
platform: LeetCode
number: 303
author: jose
layout: post
language: en
date: 2023-02-21 13:00:00 +0300
categories: [programming, ps]
tags: [algorithms, c/c++, contests, leetcode, prefix sum]
difficulty: easy
source: https://leetcode.com/problems/range-sum-query-immutable/
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
Given an integer array `nums`, handle multiple queries of the following type:

Calculate the **sum** of the elements of `nums` between indices `left` and `right` **inclusive** where `left <= right`.  
  
Implement the `NumArray` class:
- `NumArray(int[] nums)` Initializes the object with the integer array `nums`.
- `int sumRange(int left, int right)` Returns the **sum** of the elements of `nums` between indices `left` and `right` **inclusive** (i.e. `nums[left] + nums[left + 1] + ... + nums[right]`).

## Examples
---
### **Example 1:**  
>**Input**  
["NumArray", "sumRange", "sumRange", "sumRange"]  
[[[-2, 0, 3, -5, 2, -1]], [0, 2], [2, 5], [0, 5]]  
>**Output**  
[null, 1, -1, -3]  
>  
>**Explanation**  
NumArray numArray = new NumArray([-2, 0, 3, -5, 2, -1]);  
numArray.sumRange(0, 2); // return (-2) + 0 + 3 = 1  
numArray.sumRange(2, 5); // return 3 + (-5) + 2 + (-1) = -1  
numArray.sumRange(0, 5); // return (-2) + 0 + 3 + (-5) + 2 + (-1) = -3  

## Constraints
---
- <code>1 <= nums.length <= 10<sup>4</sup></code>
- <code>-10<sup>5</sup> <= nums[i] <= 10<sup>5</sup></code>
- <code>0 <= left <= right < nums.length</code>
- At most <code>10<sup>4</sup></code> calls will be made to `sumRange`.

## Solution
---
```c++
class NumArray {
private:
  vector<int> *n;
public:
  NumArray(vector<int>& nums) {
    n = &nums;
  }
    
  int sumRange(int left, int right) {
    int sum = 0;
    for(int i=left; i<=right; i+=1)
      sum += n->at(i);

    return sum;
  }
};
```
