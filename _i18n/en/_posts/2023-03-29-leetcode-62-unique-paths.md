---
title: Unique Paths
platform: LeetCode
number: 62
author: jose
layout: post
language: en
date: 2023-03-29 09:30 +0300
categories: [programming, dynamicp, recursion]
tags: [c/c++, leetcode, dynamicp, recursion]
difficulty: medium
source: https://leetcode.com/problems/unique-paths/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
There is a robot on an `m x n` grid. The robot is initially located at the **top-left corner** (i.e., `grid[0][0]`). The robot tries to move to the bottom-right corner (i.e., `grid[m - 1][n - 1]`). The robot can only move either down or right at any point in time.  

Given the two integers `m` and `n`, return *the number of possible unique paths that the robot can take to reach the bottom-right corner*.  

The test cases are generated so that the answer will be less than or equal to <code>2 * 10<sup>9</sup></code>.  

## Examples
---
### **Example 1:**
<img src="https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png" width="90%" />  

>**Input:** m = 3, n = 7  
>**Output:** 28  

### **Example 2:**
>**Input:** m = 3, n = 2  
>**Output:** 3  
>**Explanation:** From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:  
> 1. Right -> Down -> Down  
> 2. Down -> Down -> Right  
> 3. Down -> Right -> Down  

## Constraints
---
- `1 <= m, n <= 100`  

## Solution
---
This can be solved using [**dynamic programing**](/categories/dynamicp/) (either recursive or iterative).  
- We can use a map to memoize the results, but that makes it slower, so, we will allocate a vector of vectors (representing the board).  
- The iterative version is a shorter solution.  

### Solution 1:  
---
```c++
class Solution {
vector<vector<int>> dp;

private:
  int paths(int m, int n, int r, int c) {
    if (r+1 == m && c+1 == n)
      return 1;
    if (r == m || c == n)
      return 0;
    if (dp[r][c] != 0)
      return dp[r][c];
    
    dp[r][c] = 0;
    dp[r][c] += paths(m, n, r + 1, c);
    dp[r][c] += paths(m, n, r, c + 1);

    return dp[r][c];
  }
public:
  int uniquePaths(int m, int n) {
    dp = vector(m, vector<int>(n, 0));
    int r = paths(m, n, 0, 0);

    return r;
  }
};
```

### Solution 2:  
---
```c++
class Solution {
public:
  int uniquePaths(int m, int n) {
    dp = vector(m, vector<int>(n, 1));

    for (int r=1; r<m; r++) {
      for (int c=1 ; c<n; c++)
        dp[r][c] = dp[r][c-1] + dp[r-1][c];
    }
    
    return dp[m-1][n-1];
  }
};
```
