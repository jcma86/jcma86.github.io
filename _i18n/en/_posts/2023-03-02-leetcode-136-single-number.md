---
title: Single Number
platform: LeetCode
number: 136
author: jose
layout: post
language: en
date: 2023-03-02 00:20 +0300
categories: [programming, hashtable]
tags: [c/c++, contests, leetcode, hashtable, xor]
difficulty: easy
source: https://leetcode.com/problems/single-number
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
Given a **non-empty** array of integers `nums`, every element appears *twice* except for one. Find that single one.  

You must implement a solution with a linear runtime complexity and use only constant extra space.    

## Examples
---
### **Example 1:**  
>**Input:** nums = [2,2,1]  
>**Output:** 1

### **Example 2:**  
>**Input:** nums = [4,1,2,1,2]  
>**Output:** 4

### **Example 3:**  
>**Input:** nums = [1]  
>**Output:** 1

## Constraints
---
- <code>1 <= nums.length <= 3 * 10<sup>4</sup></code>
- <code>-3 * 10<sup>4</sup> <= nums[i] <= 3 * 10<sup>4</sup></code>
- Each element in the array appears twice except for one element which appears only once.

## Solution
---
From electronics course at university (not a waste of time after all), I know this can be solved using the bitwise `XOR` operator.
Another solution is just to insert each element into a hash table and count how many times appears, there will be only one with counter equal to 1.

```c++
class Solution {
public:
  int singleNumber(vector<int>& nums) {
    int x = nums[0];
    for (int i=1; i<nums.size(); i+=1)
      x ^= nums[i];
      
    return x;
  }
};
```
