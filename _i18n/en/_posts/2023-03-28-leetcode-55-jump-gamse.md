---
title: Spiral Matrix
platform: LeetCode
number: 55
author: jose
layout: post
language: en
date: 2023-03-28 19:30 +0300
categories: [programming, greedy]
tags: [c/c++, leetcode, greedy]
difficulty: medium
source: https://leetcode.com/problems/jump-game/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
You are given an integer array `nums`. You are initially positioned at the array's **first index**, and each element in the array represents your maximum jump length at that position.  

Return *`true` if you can reach the last index, or `false` otherwise*.  

## Examples
---
### **Example 1:**
>**Input:** nums = [2,3,1,1,4]  
>**Output:** true  
>**Explanation:** Jump 1 step from index 0 to 1, then 3 steps to the last index.  

### **Example 2:**
>**Input:** nums = [3,2,1,0,4]  
>**Output:** false  
>**Explanation:** You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.  

## Constraints
---
- <code>1 <= nums.length <= 10<sup>4</sup></code>  
- <code>0 <= nums[i] <= 10<sup>5</sup></code>  

## Solution
---
This problem is solved by using a **[greedy algorithm](/categories/greedy/)**.  
  - For every position we calculate what is the maximun position we can reach.  
  - If the current position is beyond the max position we can reach, `return false`.  
  - If the maximum position is equal or greater than the last index, then `return true`.  

```c++
class Solution {
public:
  bool canJump(vector<int>& nums) {
    int maxPosition = 0;
    for (int i=0; i<nums.size(); i++) {
      if (i > maxPosition)
        break;

      maxPosition = max(maxPosition, i + nums[i]);
      if (maxPosition >= (nums.size()-1))
        return true;
    }

    return false;
  }
};
```
