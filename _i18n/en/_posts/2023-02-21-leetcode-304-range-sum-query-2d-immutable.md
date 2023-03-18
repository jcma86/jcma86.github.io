---
date: 2023-02-21 15:00:00 +0300
title: Range Sum Query 2D - Immutable
author: jose
platform: LeetCode
number: 304
difficulty: medium
source: https://leetcode.com/problems/range-sum-query-2d-immutable/
proglang: C/C++
categories: [programming, ps]
tags: [algorithms, c/c++, contests, leetcode, prefix sum]
layout: post
language: en
math: true
mermaid: true
pin: true
# image:
#   path: https://user-images.githubusercontent.com/36547915/97088991-45da5d00-1652-11eb-900f-80d106540f4f.png
#   lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
#   alt: Responsive rendering of Chirpy theme on multiple devices.
--- 
## Problem
---
Given a 2D matrix `matrix`, handle multiple queries of the following type:

> Calculate the **sum** of the elements of `matrix` inside the rectangle defined by its **upper left corner** `(row1, col1)` and **lower right corner** `(row2, col2)`.
  
Implement the `NumMatrix` class:  
- `NumMatrix(int[][] matrix)` Initializes the object with the integer matrix `matrix`.
- `int sumRegion(int row1, int col1, int row2, int col2)` Returns the **sum** of the elements of `matrix` inside the rectangle defined by its **upper left corner** `(row1, col1)` and **lower right corner** `(row2, col2)`.  

You must design an algorithm where sumRegion works on O(1) time complexity.

## Examples
---
### **Example 1:**  
![Matrix example](https://assets.leetcode.com/uploads/2021/03/14/sum-grid.jpg "Example 1")
>**Input**  
["NumMatrix", "sumRegion", "sumRegion", "sumRegion"]  
[[[[3, 0, 1, 4, 2], [5, 6, 3, 2, 1], [1, 2, 0, 1, 5], [4, 1, 0, 1, 7], [1, 0, 3, 0, 5]]], [2, 1, 4, 3], [1, 1, 2, 2], [1, 2, 2, 4]]  
>**Output**  
[null, 8, 11, 12]  
>  
>**Explanation**  
NumMatrix numMatrix = new NumMatrix([[3, 0, 1, 4, 2], [5, 6, 3, 2, 1], [1, 2, 0, 1, 5], [4, 1, 0, 1, 7], [1, 0, 3, 0, 5]]);  
numMatrix.sumRegion(2, 1, 4, 3); // return 8 (i.e sum of the red rectangle)  
numMatrix.sumRegion(1, 1, 2, 2); // return 11 (i.e sum of the green rectangle)  
numMatrix.sumRegion(1, 2, 2, 4); // return 12 (i.e sum of the blue rectangle)  

## Constraints
---
- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 200`
- <code>-10<sup>4</sup> <= matrix[i][j] <= 10<sup>4</sup></code>
- `0 <= row1 <= row2 < m`
- `0 <= col1 <= col2 < n`
- At most <code>10<sup>4</sup></code> calls will be made to `sumRegion`.

## Solution
---
```c++
/**
 * Your NumMatrix object will be instantiated and called as such:
 * NumMatrix* obj = new NumMatrix(matrix);
 * int param_1 = obj->sumRegion(row1,col1,row2,col2);
 */

class NumMatrix {
private:
  vector<vector<int>> *m;
public:
  NumMatrix(vector<vector<int>>& matrix) {
    m = &matrix;
        
    for(int r = 0; r < m->size(); r += 1) {
      int crow = 0;
      for(int c = 0; c < m->at(r).size(); c += 1) {
        crow += m->at(r)[c];
        m->at(r)[c] = r == 0 ? crow : (crow + m->at(r - 1)[c]);
      }
    }
  }
    
  int sumRegion(int row1, int col1, int row2, int col2) {
    int sum = m->at(row2)[col2];

    if (row1 > 0)
      sum -= m->at(row1-1)[col2];
    if (col1 > 0)
      sum -= m->at(row2)[col1-1];
    if (col1 > 0 && row1 > 0)
      sum += m->at(row1-1)[col1-1];

    return sum;
  }
};
```
