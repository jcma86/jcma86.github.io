---
title: Maximum Subarray
platform: LeetCode
number: 53
author: jose
layout: post
language: en
date: 2023-03-27 10:00 +0300
categories: [programming, dynamicp, others]
tags: [c/c++, leetcode, dynamicp, others]
difficulty: medium
source: https://leetcode.com/problems/maximum-subarray/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given an integer array `nums`, find the **subarray** with the largest sum, and return *its sum*.  

## Examples
---
### **Example 1:**
>**Input:** nums = [-2,1,-3,4,-1,2,1,-5,4]  
>**Output:** 6  
>**Explanation:** The subarray [4,-1,2,1] has the largest sum 6.  

### **Example 2:**
>**Input:** nums = [1]  
>**Output:** 1  
>**Explanation:** The subarray [1] has the largest sum 1.  

### **Example 3:**
>**Input:** nums = [5,4,-1,7,8]  
>**Output:** 23  
>**Explanation:** The subarray [5,4,-1,7,8] has the largest sum 23.  

## Constraints
---
- <code>1 <= nums.length <= 10<sup>5</sup></code>  
- <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>  

## Solution
---
For this problem, we will use [*Dynamic Programming*](/categories/dynamicp/).  
 - Iterate through each number:  
  - Keep tracking of the sum of elements.  
  - If at any point the `sum < 0` it is not adding to the result, so, we can reset the `sum = 0`.  
  - Update the maximum found.  

```c++
class Solution {
public:
  int maxSubArray(vector<int>& nums) {
    int sum = 0; 
    int maxSum = INT_MIN;
    int j = 0;
    
    while (j<nums.size()) {
      if (sum < 0 && nums[j] >= sum)
        sum = 0;
      
      sum += nums[j];
      maxSum = max(maxSum, sum);
      j++;
    }
    return maxSum;
  }
};
```
