---
title: Number of Islands
platform: LeetCode
number: 200
author: jose
layout: post
language: en
date: 2023-03-03 01:30 +0300
categories: [programming, dfsbfs]
tags: [c/c++, contests, leetcode, dfs]
difficulty: medium
source: https://leetcode.com/problems/number-of-islands
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return *the number of islands*.

An *island* is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

## Examples
---
### **Example 1:**  
>**Input:** grid = [  
>  ["1","1","1","1","0"],  
>  ["1","1","0","1","0"],  
>  ["1","1","0","0","0"],  
>  ["0","0","0","0","0"]  
>]  
>**Output:** 1

### **Example 2:**  
>**Input:** grid = [  
>  ["1","1","0","0","0"],  
>  ["1","1","0","0","0"],  
>  ["0","0","1","0","0"],  
>  ["0","0","0","1","1"]  
>]  
>**Output:** 3

## Constraints
---
- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 300`
- `grid[i][j]` is `'0'` or `'1'`.

## Solution
---
We will perform a Deep First Search:
  - Iterate through every point of the `map`
    - If the point is `'0'` then whe ignore it and move to the next one.
    - If the point is `'1'`:
      - We mark it as `'0'` and increase the count of islands,
      - We explore the 4 points around it in a recursive way (DFS).
        - For every adjacent point, if it is `'1'` we explore it, otherwise we ignore it.

---
```c++
class Solution {
public:
  void exploreNode(vector<vector<char>>& grid, int r, int c) {
    grid[r][c] = '0';
    if (r > 0 && grid[r-1][c] == '1')  
      exploreNode(grid, r-1, c);
    if (c > 0 && grid[r][c-1] == '1')  
      exploreNode(grid, r, c-1);
    if (r<(grid.size() - 1) && grid[r+1][c] == '1')  
      exploreNode(grid, r+1, c);
    if (c<(grid[r].size() - 1) && grid[r][c+1] == '1')  
      exploreNode(grid, r, c+1);
  }

  int numIslands(vector<vector<char>>& grid) {
    int islands = 0;

    for (int r=0; r<grid.size(); r+= 1) {
      for (int c=0; c<grid[r].size(); c+=1 ) {
        if (grid[r][c] == '0') 
          continue;

        islands += 1;
        exploreNode(grid, r, c);
      }
    }

    return islands;
  }
};
```
