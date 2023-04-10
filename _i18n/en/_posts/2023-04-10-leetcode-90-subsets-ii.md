---
title: Subsets II
platform: LeetCode
number: 90
author: jose
layout: post
language: en
date: 2023-04-10 20:00 +0300
categories: [programming, bt]
tags: [c/c++, leetcode, bt]
difficulty: medium
source: https://leetcode.com/problems/subsets-ii/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given an integer array `nums` that may contain duplicates, return *all possible subsets (the power set)*.  

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.  

## Examples
---
### **Example 1:**
>**Input:** nums = [1,2,2]  
>**Output:** [[],[1],[1,2],[1,2,2],[2],[2,2]]  

### **Example 2:**
>**Input:** nums = [0]  
>**Output:** [[],[0]]  

## Constraints
---
- `1 <= nums.length <= 10`  
- `-10 <= nums[i] <= 10`  

## Solution
---
This is very similar to [problem 78](../../03/leetcode-78-subsets/), we will solve it using **[backtracking](/categories/bt/)**.  

- To prevent duplicates, we first sort the array of numbers, and when adding them to the current subset, we will skip the repeated numbers.  

```c++
class Solution {
private:
  vector<vector<int>> powerset;
  void generateSets(vector<int>& nums, vector<int>& sol, int index) {
    powerset.push_back(sol);

    for (int i=index; i<nums.size(); i++) {
      if (i > index && nums[i] == nums[i-1])
        continue;
      sol.push_back(nums[i]);
      generateSets(nums, sol, i+1);
      sol.pop_back();
    }
  }

public:
  vector<vector<int>> subsetsWithDup(vector<int>& nums) {
    vector<int> sol;
    sort(nums.begin(), nums.end());
    generateSets(nums, sol, 0);
    return powerset;
  }
};
```
