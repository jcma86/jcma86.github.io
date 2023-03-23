---
title: Permutations II
platform: LeetCode
number: 47
author: jose
layout: post
language: en
date: 2023-03-22 13:00 +0300
categories: [programming, bt, recursion]
tags: [c/c++, leetcode, bt, recursion]
difficulty: medium
source: https://leetcode.com/problems/permutations-ii/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given a collection of numbers, `nums`, that might contain duplicates, return *all possible unique permutations **in any order***.  

## Examples
---
### **Example 1:**
>**Input:** nums = [1,1,2]  
>**Output:**  
>[[1,1,2],  
>[1,2,1],  
>[2,1,1]]  

### **Example 2:**
>**Input:** nums = [1,2,3]  
>**Output:** [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]  

## Constraints
---
- `1 <= nums.length <= 8`  
- `-10 <= nums[i] <= 10`  

## Solution
---
This can be solved using [**Backtracking**](https://www.geeksforgeeks.org/introduction-to-backtracking-data-structure-and-algorithm-tutorials/) (*see more [backtracking problems](/categories/bt/)*)    

For this problem, to avoid having duplicated permutations (because we have repeated numbers):  
  - First we sort the array.  
  - We need to keep track of the numbers we add to a solution/permutation.  
  - If the number to add to a permutation is the same number than the previous one, and the previous one has not been added, then we skip it.  

```c++
class Solution {
private:
  vector<vector<int>> result;

  void permutations(vector<int>& nums, vector<int>& tmpSol, vector<bool>& proc) {
    if (tmpSol.size() == nums.size()) {
      result.push_back(tmpSol);
      return;
    }

    for (int i=0; i<nums.size(); i++) {
      if (proc[i] || (i>0 && nums[i] == nums[i-1] && !proc[i-1])) 
        continue;
      proc[i] = true;
      tmpSol.push_back(nums[i]);
      permutations(nums, tmpSol, proc);
      tmpSol.pop_back();
      proc[i] = false;
    }
  }
public:
  vector<vector<int>> permuteUnique(vector<int>& nums) {
    vector<bool> proccessed(nums.size(), false);
    vector<int> tmpSol;
    sort(nums.begin(), nums.end());
    permutations(nums, tmpSol, proccessed);

    return result;
  }
};
```
