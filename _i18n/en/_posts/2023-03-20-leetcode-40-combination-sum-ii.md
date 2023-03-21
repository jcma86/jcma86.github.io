---
title: Combination Sum II
platform: LeetCode
number: 40
author: jose
layout: post
language: en
date: 2023-03-20 23:10 +0300
categories: [programming, bt, recursion]
tags: [c/c++, leetcode, bt, recursion]
difficulty: medium
source: https://leetcode.com/problems/combination-sum-ii/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`.  

Each number in `candidates` may only be used **once** in the combination.  

**Note**: The solution set must not contain duplicate combinations.  

## Examples
---
### **Example 1:**
>**Input:** candidates = [10,1,2,7,6,1,5], target = 8  
>**Output:** [  
>[1,1,6],  
>[1,2,5],  
>[1,7],  
>[2,6]  
>]  

### **Example 2:**
>**Input:** candidates = [2,5,2,1,2], target = 5  
>**Output:** [  
>[1,2,2],  
>[5]  
>]  

## Constraints
---
- `1 <= candidates.length <= 100`  
- `1 <= candidates[i] <= 50`  
- `1 <= target <= 30`  

## Solution
---
This is a similar solution to the one for the [**problem 39**](../leetcode-39-combination-sum).  
- Everytime we call recursively:  
  - We advance the index of the next element to add to our possible solution.  
  - Once we added the element, if the next element is the same value, we keep moving our index in order to avoid duplicated solutions.  

```c++
class Solution {
private:
  vector<vector<int>> result;

  void sum(vector<int>& candidates, int target, vector<int>& ans, int i) {
    if (target == 0) {
      result.push_back(ans);
      return;
    }
        
    for (i; i<candidates.size(); i++) {
      if (target - candidates[i] < 0)
        break;
      
      ans.push_back(candidates[i]);
      sum(candidates, target - candidates[i], ans, i+1);
      ans.pop_back();

      while (i < candidates.size() - 1 && candidates[i] == candidates[i+1])
        i++;
    }
  }

public:
  vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
    vector<int> ans;
    sort(candidates.begin(), candidates.end());
    sum(candidates, target, ans, 0);
    return result;
  }
};
```
