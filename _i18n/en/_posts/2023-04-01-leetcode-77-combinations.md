---
title: Combinations
platform: LeetCode
number: 77
author: jose
layout: post
language: en
date: 2023-04-01 22:00 +0300
categories: [programming, bt]
tags: [c/c++, leetcode, bt]
difficulty: medium
source: https://leetcode.com/problems/combinations/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given two integers `n` and `k`, return *all possible combinations of `k` numbers chosen from the range `[1, n]`*.  

You may return the answer in **any order**.  

## Examples
---
### **Example 1:**
>**Input:** n = 4, k = 2  
>**Output:** [[1,2],[1,3],[1,4],[2,3],[2,4],[3,4]]  
>**Explanation:** There are 4 choose 2 = 6 total combinations.  
>Note that combinations are unordered, i.e., [1,2] and [2,1] are considered to be the same combination.  

### **Example 2:**
>**Input:** n = 1, k = 1  
>**Output:** [[1]]  
>**Explanation:** There is 1 choose 1 = 1 total combination.  

## Constraints
---
- `1 <= n <= 20`  
- `1 <= k <= n`  

## Solution
---
This one is easily solved using **[Backtracking](/categories/bt/)**  

- Becasue there should not be repeated combinations, for recursive call we set the initial index to be one more than the previous call.  
- And we add `1` to the number when adding to the combination (because the range is from `1` to `n`).  

For this solution I'm pushing/poping an element to generate the combination, and alternative (a couple of milliseconds faster) is to have a vector of fixed `k` size and just handle the index of the current element to set.  

```c++
class Solution {
vector<vector<int>> result;

void generateCombinations(int n, int k, int ci, vector<int>& c) {
  if (c.size() == k) {
    result.push_back(c);
    return;
  }

  for (int i=ci; i<n; i++) {
    c.push_back(i+1);
    generateCombinations(n, k, i+1, c);
    c.pop_back();
  }
}

public:
  vector<vector<int>> combine(int n, int k) {
    result.clear();
    vector<int> sol;

    generateCombinations(n, k, 0, sol);

    return result;
  }
};
```
