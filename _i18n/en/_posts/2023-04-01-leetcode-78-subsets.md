---
title: Subsets
platform: LeetCode
number: 78
author: jose
layout: post
language: en
date: 2023-04-03 12:00 +0300
categories: [programming, bt]
tags: [c/c++, leetcode, bt]
difficulty: medium
source: https://leetcode.com/problems/subsets/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given an integer array `nums` of **unique** elements, return *all possible subsets (the power set)*.  

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.  

## Examples
---
### **Example 1:**
>**Input:** nums = [1,2,3]  
>**Output:** [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]  

### **Example 2:**
>**Input:** nums = [0]  
>**Output:** [[],[0]]  

## Constraints
---
- `1 <= nums.length <= 10`  
- `-10 <= nums[i] <= 10`  
- All the numbers of `nums` are **unique**.  

## Solution
---
This one is easily solved using **[Backtracking](/categories/bt/)** same as [problem 77](../leetcode-77-combinations/).  
- In this particular problem, we add every single combination generated at each step and not only of a particular size.  

```c++
class Solution {
  vector<vector<int>> result;

  void generateCombinations(vector<int>& nums, int ci, vector<int>& c) {
    if (ci >= nums.size()) {
      return;
    }

    for (int i=ci; i<nums.size(); i++) {
      c.push_back(nums[i]);
      result.push_back(c);
      generateCombinations(nums, i+1, c);
      c.pop_back();
    }
}

public:
  vector<vector<int>> subsets(vector<int>& nums) {
    result.clear();
    vector<int> sol;
    result.push_back({});
    generateCombinations(nums, 0, sol);
    return result;
  }
};
```
