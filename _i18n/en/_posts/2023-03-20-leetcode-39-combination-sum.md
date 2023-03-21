---
title: Combination Sum
platform: LeetCode
number: 39
author: jose
layout: post
language: en
date: 2023-03-20 22:30 +0300
categories: [programming, bt, recursion]
tags: [c/c++, leetcode, bt, recursion]
difficulty: medium
source: https://leetcode.com/problems/combination-sum/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given an array of **distinct** integers `candidates` and a target integer `target`, return *a list of all **unique combinations** of `candidates` where the chosen numbers sum to `target`*. You may return the combinations in **any order**.  

The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the frequency of at least one of the chosen numbers is different.  

The test cases are generated such that the number of unique combinations that sum up to target is less than 150 combinations for the given input.  

## Examples
---
### **Example 1:**
>**Input:** candidates = [2,3,6,7], target = 7  
>**Output:** [[2,2,3],[7]]  
>**Explanation:**  
>2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.  
>7 is a candidate, and 7 = 7.  
>These are the only two combinations.  

### **Example 2:**
>**Input:** candidates = [2,3,5], target = 8  
>**Output:** [[2,2,2,2],[2,3,3],[3,5]]  

### **Example 3:**
>**Input:** candidates = [2], target = 1  
>**Output:** []  

## Constraints
---
- `1 <= candidates.length <= 30`  
- `2 <= candidates[i] <= 40`  
- All elements of `candidates` are **distinct**.  
- `1 <= target <= 40`  

## Solution
---
- We will use backtracking.
- We sort the candidates vector, this way, we know that when adding a new number to a possible answer, if the sum is greater than the target, then we can stop looking into the rest of the candidates.  

```c++
class Solution {
private:
  vector<vector<int>> result;
public:
  void sum(vector<int>& candidates, int target, vector<int>& ans, int i) {
    if (target == 0) {
      result.push_back(ans);
      return;
    }
        
    for (int j=i; j<candidates.size(); j++) {
      if (target - candidates[j] < 0)
        break;

      ans.push_back(candidates[j]);
      sum(candidates, target - candidates[j], ans, j);
      ans.pop_back();
    }
  }

  vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
    vector<int> ans;
    sort(candidates.begin(), candidates.end());
    sum(candidates, target, ans, 0);
    return result;
  }
};
```
