---
title: Unique Paths II
platform: LeetCode
number: 63
author: jose
layout: post
language: en
date: 2023-03-29 10:00 +0300
categories: [programming, dynamicp, recursion]
tags: [c/c++, leetcode, dynamicp, recursion]
difficulty: medium
source: https://leetcode.com/problems/unique-paths-ii/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
You are given an `m x n` integer array `grid`. There is a robot initially located at the top-left corner (i.e., **grid[0][0]**). The robot tries to move to the **bottom-right corner** (i.e., `grid[m - 1][n - 1]`). The robot can only move either down or right at any point in time.  

An obstacle and space are marked as `1` or `0` respectively in `grid`. A path that the robot takes cannot include any square that is an obstacle.  

Return *the number of possible unique paths that the robot can take to reach the bottom-right corner*.

The test cases are generated so that the answer will be less than or equal to <code>2 * 10<sup>9</sup></code>.  

## Examples
---
### **Example 1:**
<img src="https://assets.leetcode.com/uploads/2020/11/04/robot1.jpg" width="90%" />  

>**Input:** obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]  
>**Output:** 2  
>**Explanation:** There is one obstacle in the middle of the 3x3 grid above.  
>There are two ways to reach the bottom-right corner:  
>1. Right -> Right -> Down -> Down  
>2. Down -> Down -> Right -> Right  

### **Example 2:**
<img src="https://assets.leetcode.com/uploads/2020/11/04/robot2.jpg" width="90%" />  

>**Input:** obstacleGrid = [[0,1],[0,0]]  
>**Output:** 1  

## Constraints
---
- `m == obstacleGrid.length`  
- `n == obstacleGrid[i].length`  
- `1 <= m, n <= 100`  
- `obstacleGrid[i][j] is 0 or 1.`  

## Solution
---
Same solution as for **[problem 62](../leetcode-62-unique-paths/)** with two differences:
  1. Check if the goal position has an obstacle.  
  2. Need to check if the board/grid has a `1` at the current position.  

```c++
class Solution {
private:
  vector<vector<int>> dp;

  int paths(vector<vector<int>>& grid, int r, int c) {
    if (r+1 == grid.size() && c+1 == grid[0].size())
      return 1;
    if (r == grid.size() || c == grid[0].size())
      return 0;
    if (grid[r][c] == 1)
      return 0;
    
    if (dp[r][c] != 0)
      return dp[r][c];
    
    dp[r][c] = 0;
    dp[r][c] += paths(grid, r + 1, c);
    dp[r][c] += paths(grid, r, c + 1);

    return dp[r][c];
  }

public:
  int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
    if (obstacleGrid[obstacleGrid.size() - 1][obstacleGrid[0].size() - 1] == 1)
      return 0;
        
    dp = vector(obstacleGrid.size(), vector<int>(obstacleGrid[0].size(), 0));
    return paths(obstacleGrid, 0, 0);
  }
};
```
