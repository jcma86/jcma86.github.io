---
title: Search a 2D Matrix
platform: LeetCode
number: 74
author: jose
layout: post
language: en
date: 2023-03-01 10:00 +0300
categories: [programming, bs]
tags: [c/c++, contests, leetcode, bs]
difficulty: medium
source: https://leetcode.com/problems/search-a-2d-matrix
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
You are given an `m x n` integer matrix `matrix` with the following two properties:  

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return *`true` if `target` is in `matrix` or `false` otherwise*.

You must write a solution in `O(log(m * n))` time complexity.

## Examples
---
### **Example 1:**  
<img src="https://assets.leetcode.com/uploads/2020/10/05/mat.jpg" width="50%"/>  

>**Input:** matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3  
>**Output:** true

### **Example 2:**  
<img src="https://assets.leetcode.com/uploads/2020/10/05/mat2.jpg" width="50%"/> 

>**Input:** matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13  
>**Output:** false  

## Constraints
---
- <code>m == matrix.length</code>
- <code>n == matrix[i].length</code>
- <code>1 <= m, n <= 100</code>
- <code>-10<sup>4</sup> <= matrix[i][j], target <= 10<sup>4</sup></code>

## Solution
---
Two binary searchs (nested or not). First, we find the row where the number should be located. Then, with a second binary search we find the position of the number.  
```c++
class Solution {
public:
  bool searchMatrix(vector<vector<int>>& matrix, int target) {
    bool inRow = false;
    int l = 0;
    int h = matrix.size() - 1;
    int m;

    while (l<=h) {
      m = (l + h) / 2;
      if (matrix[m][0] == target || matrix[m][matrix[m].size() - 1] == target)
        return true;

      if (matrix[m][0] < target && matrix[m][matrix[m].size() - 1] > target) {
        inRow = true;
        break;
      }
      if (matrix[m][0] > target)
        h = m - 1;
      if (matrix[m][matrix[m].size() - 1] < target)
        l = m + 1;
    }

    if (inRow) {
      l = 0;
      h = matrix[m].size() - 1;
      int m2;
      while (l <= h) {
        m2 = (l + h) / 2;
        if (matrix[m][m2] == target)
          return true;
        if (matrix[m][m2] > target)
          h = m2 - 1;
        if (matrix[m][m2] < target)
          l = m2 + 1;
      }
    }
  
    return false;
  }
};
```
