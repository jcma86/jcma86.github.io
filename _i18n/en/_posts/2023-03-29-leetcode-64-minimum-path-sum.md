---
title: Minimum Path Sum
platform: LeetCode
number: 64
author: jose
layout: post
language: en
date: 2023-03-29 22:00 +0300
categories: [programming, dynamicp, recursion]
tags: [c/c++, leetcode, dynamicp, recursion]
difficulty: medium
source: https://leetcode.com/problems/minimum-path-sum/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given a `m x n` grid filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.  

**Note:** You can only move either down or right at any point in time.  

## Examples
---
### **Example 1:**
<img src="https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg" width="90%" />  

>**Input:** grid = [[1,3,1],[1,5,1],[4,2,1]]  
>**Output:** 7  
>**Explanation:** Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.  

### **Example 2:**
>**Input:** grid = [[1,2,3],[4,5,6]]  
>**Output:** 12  

## Constraints
---
- `m == grid.length`  
- `n == grid[i].length`  
- `1 <= m, n <= 200`  
- `0 <= grid[i][j] <= 100`  

## Solution
---
We use **[dynamic programming](/categories/dynamicp/)**: 

```c++
class Solution {
private:
  vector<vector<int>> dp;
  int minPath(vector<vector<int>>& grid, int r, int c) {
    if (r+1 == grid.size() && c+1 == grid[0].size())
      return grid[r][c];
    if (r == grid.size() || c == grid[0].size())
      return INT_MAX;
    if (dp[r][c] != -1)
      return dp[r][c];

    dp[r][c] = grid[r][c] + min(minPath(grid, r+1, c), minPath(grid, r, c+1));

    return dp[r][c];
  }

public:
  int minPathSum(vector<vector<int>>& grid) {
    dp = vector(grid.size(), vector<int>(grid[0].size(), -1));
    return minPath(grid, 0, 0);
  }
};
```
