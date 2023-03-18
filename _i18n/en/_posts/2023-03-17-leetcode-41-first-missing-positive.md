---
title: First Missing Positive
platform: LeetCode
number: 41
author: jose
layout: post
language: en
date: 2023-03-17 20:50 +0300
categories: [programming, others]
tags: [c/c++, leetcode, others]
difficulty: hard
source: https://leetcode.com/problems/first-missing-positive/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given an unsorted integer array `nums`, return the smallest missing positive integer.  

You must implement an algorithm that runs in `O(n)` time and uses constant extra space.  

## Examples
---
### **Example 1:**
>**Input:** nums = [1,2,0]  
>**Output:** 3  
>**Explanation:** The numbers in the range [1,2] are all in the array.  

### **Example 2:**
>**Input:** nums = [3,4,-1,1]  
>**Output:** 2  
>**Explanation:** 1 is in the array but 2 is missing.  

### **Example 3:**
>**Input:** nums = [7,8,9,11,12]  
>**Output:** 1  
>**Explanation:** The smallest positive integer 1 is missing.  

## Constraints
---
- <code>1 <= nums.length <= 10<sup>5</sup></code>  
- <code>-2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1</code>  

## Solution
---
  - Because we are looking for a positive integer, we can "remove" all the negative numbers (We set them to `0`).  
  - If we have an array of size `n` with numbers `from 2 to n+1` we know that the value missing is `1`; if the array has all the values `[1,n]`, then the first missing integer is `n+1`. So, we are looking for an integer in the range `[1, n+1]`.  
  - For each number, we verify if its absolute is a number in the range `[1,n]`.  
  - If so, we can verify the value present at the index that should be for that number if the array was sorted (with values from `1 to n`).  
    - If the value at that position is `> 0`, we mark them as negative.  
    - If the value is `0` we set it to `-(n+1)`.  

  - Once completed, we iterate through the array, and the first element with value `>0` that's the missing integer (`index+1`).  
  
```c++
class Solution {
public:
  int firstMissingPositive(vector<int>& nums) {
    int n=nums.size();
    
    for (int i=0;i<n;++i)
      if (nums[i]<0) nums[i] = 0;
        
    for (int i=0;i<n;++i){
      int absv = abs(nums[i]);
      if (absv >= 1 && absv <= n) {
        if (nums[absv-1] > 0)
          nums[absv-1] *= -1;
        else if (nums[absv-1] == 0)
          nums[absv-1] = -1*(n+1);
      }
    }
        
    for (int i=1;i<n+1;++i)
      if (nums[i-1]>=0) return i;
        
    return n+1;
  }
};
```
