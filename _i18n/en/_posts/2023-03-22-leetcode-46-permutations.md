---
title: Permutations
platform: LeetCode
number: 46
author: jose
layout: post
language: en
date: 2023-03-22 11:00 +0300
categories: [programming, bt, recursion]
tags: [c/c++, leetcode, bt, recursion]
difficulty: medium
source: https://leetcode.com/problems/permutations/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given an array `nums` of distinct integers, return *all the possible permutations*. You can return the answer in **any order**.  

## Examples
---
### **Example 1:**
>**Input:** nums = [1,2,3]  
>**Output:** [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]  

### **Example 2:**
>**Input:** nums = [0,1]  
>**Output:** [[0,1],[1,0]]  

### **Example 3:**
>**Input:** nums = [1]  
>**Output:** [[1]]  

## Constraints
---
- `1 <= nums.length <= 6`
- `-10 <= nums[i] <= 10`
- All the integers of `nums` are **unique**.

## Solution
---
This can be solved using [**Backtracking**](https://www.geeksforgeeks.org/introduction-to-backtracking-data-structure-and-algorithm-tutorials/) (*see more [backtracking problems](/categories/bt/)*)    

```c++
class Solution {
private:
  vector<vector<int>> result;

  void permutations(vector<int>& nums, int index) {
    if (index == nums.size()) {
      result.push_back(nums);
      return;
    }

    for (int i=index; i<nums.size(); i++) {
      swap(nums[index], nums[i]);
      permutations(nums, index+1);
      swap(nums[index], nums[i]);
    }
  }
public:
  vector<vector<int>> permute(vector<int>& nums) {
    permutations(nums, 0);

    return result;
  }
};
```
