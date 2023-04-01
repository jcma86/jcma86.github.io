---
title: Set Matrix Zeroes
platform: LeetCode
number: 73
author: jose
layout: post
language: en
date: 2023-04-01 22:00 +0300
categories: [programming, others]
tags: [c/c++, leetcode, others]
difficulty: medium
source: https://leetcode.com/problems/set-matrix-zeroes/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`'s.  

You must do it **in place**.  

## Examples
---
### **Example 1:**
<img src="https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg" width="90%"/>  

>**Input:** matrix = [[1,1,1],[1,0,1],[1,1,1]]  
>**Output:** [[1,0,1],[0,0,0],[1,0,1]]  

### **Example 2:**
<img src="https://assets.leetcode.com/uploads/2020/08/17/mat2.jpg" width="90%"/>  

>**Input:** matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]  
>**Output:** [[0,0,0,0],[0,4,5,0],[0,3,1,0]]  

## Constraints
---
- `m == matrix.length`  
- `n == matrix[0].length`  
- `1 <= m, n <= 200`  
- <code>-2<sup>31</sup> <= matrix[i][j] <= 2<sup>31</sup> - 1</code>  

## Solution
---
We will use extra space (a vetor with size of the number of columns, and a boolean variable).  
- Will iterate through the matrix:  
  - If we find a `0`, 
    - We set a `row flag` to `true` to indicate that the row needs to change to 0.  
    - We set a the element of the extra vector to `true` (at the current column) to indicate that the column needs to change to 0.  
  - Once we are at the last column, if the flag for the row is `true`, we set the whole row to `0`.  
  - Once we are at the last row, if the column index in our extra vector is `true` then we set the column to `0`.  

```c++
class Solution {
public:
  void setZeroes(vector<vector<int>>& matrix) {
    vector<bool> cols(matrix[0].size(), false);
    bool row = false;
    
    for (int r=0; r<matrix.size(); r++) {
      row = false;
      for (int c=0; c<matrix[r].size(); c++) {
        if (matrix[r][c] == 0) {
          row = true;
          cols[c] = true;
        }

        if (c == matrix[r].size()-1 && row)
          for (int i=0; i<matrix[r].size(); i++)  
            matrix[r][i] = 0;
        if (r == matrix.size()-1 && cols[c])
          for (int i=0; i<matrix.size(); i++)  
            matrix[i][c] = 0;
      }
    }
  }
};
```
