---
title: Jump Game II
platform: LeetCode
number: 45
author: jose
layout: post
language: en
date: 2023-03-22 10:00 +0300
categories: [programming, greedy]
tags: [c/c++, leetcode, greedy]
difficulty: medium
source: https://leetcode.com/problems/jump-game-ii/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
You are given a **0-indexed** array of integers `nums` of length `n`. You are initially positioned at `nums[0]`.

Each element `nums[i]` represents the maximum length of a forward jump from index `i`. In other words, if you are at `nums[i]`, you can jump to any `nums[i + j]` where:

* `0 <= j <= nums[i]` and  
* `i + j < n`  

Return *the minimum number of jumps to reach `nums[n - 1]`*. The test cases are generated such that you can reach `nums[n - 1]`.  

## Examples
---
### **Example 1:**
>**Input:** nums = [2,3,1,1,4]  
>**Output:** 2  
>**Explanation:** The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.  

### **Example 2:**
>**Input:** nums = [2,3,0,1,4]  
>**Output:** 2  

## Constraints
---
- <code>1 <= nums.length <= 10<sup>4</sup></code>  
- `0 <= nums[i] <= 1000`  
- It's guaranteed that you can reach `nums[n - 1]`.  

## Solution
---
We will use a [**Greedy Algorithm**](https://www.programiz.com/dsa/greedy-algorithm) (*see more [problems](/categories/greedy/)*)  
- For each position, we determine what is the maximum distance we can achive.  
- Everytime we are at the element of the max distance achieve, we increase the jumps counting.  
- When we can reach the last element (or more) we increase the jump count and return the value.  

```c++
class Solution {
public:
  int jump(vector<int>& nums) {
    if (nums.size() <= 1)
      return 0;
    
    int jumps = 0;
    int curPos = 0;
    int maxPos = 0;
      
    for (int i=0; i<nums.size(); i++) {
      maxPos = max(maxPos, i + nums[i]);
      
      if (maxPos >= nums.size() - 1) {
        jumps += 1;
        break;
      }
      
      if (curPos == i) {
        jumps += 1;
        curPos = maxPos;
      }
    }
    
    return jumps;
  }
};
```
