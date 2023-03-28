---
title: Spiral Matrix
platform: LeetCode
number: 54
author: jose
layout: post
language: en
date: 2023-03-28 18:55 +0300
categories: [programming, others]
tags: [c/c++, leetcode, others]
difficulty: medium
source: https://leetcode.com/problems/spiral-matrix/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given an `m x n` `matrix`, return *all elements of the `matrix` in spiral order*.  

## Examples
---
### **Example 1:**
<img src="https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg" width="90%" />  
>**Input:** matrix = [[1,2,3],[4,5,6],[7,8,9]]  
>**Output:** [1,2,3,6,9,8,7,4,5]  

### **Example 2:**
<img src="https://assets.leetcode.com/uploads/2020/11/13/spiral.jpg" width="90%" />  
>**Input:** matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]  
>**Output:** [1,2,3,4,8,12,11,10,9,5,6,7]  

## Constraints
---
- `m == matrix.length`  
- `n == matrix[i].length`  
- `1 <= m, n <= 10`  
- `-100 <= matrix[i][j] <= 100`  

## Solution
---
The algorithm is as follows:  
 - We iterate through all the cells.  
 - We use two variables for the current position (`row` and `column`).  
 - We use two variables to identify the minimun column and the maximum column.  
 - Same for minimum and maximum row.  
 - Every time the current location is at the **minimum** row and column:
   - Reduce by one the maximum column.  
   - Reduce by one the maximum row.  
 - Every time the current location is at the **maximum** row and column:
   - Increase by one the minimum column.  
   - Increase by one the minimum row.  
 - We handle the direction we move the current location by not moving or adding/substracting 1 from the column/row position base on this conditions:  
  - **Minimum row** and **minimum column**: row doesn't change, column will increase by one.  
  - **Minimum row** and **maximum column**: row increase by one, column doesn't change.  
  - **Maximum row** and **maximum column**: row doesn't change, column will decrease by one.  
  - **Maximum row** and **minimum column**: columns doesn't change, row will decrease by one.  

There are a few considerations:  
  - Initial position: row 0, column -1.  (So, first step will add one to column and start moving throgh the first row).  
  - Maximum column and row: start one place further than the size of the matrix, so, first decreasing sets them to the correct size.  
  - When only one row, or only one column (`minRow == maxRow` or `minCol == maxCol`)we don't move the row or column.  

```c++
class Solution {
public:
  vector<int> spiralOrder(vector<vector<int>>& matrix) {
    vector<int> result;
    int t = matrix.size() * matrix[0].size();

    int dr = 0;
    int dc = 1;
    int r = 0;
    int c = -1;
    int minCol = -1;
    int maxCol = matrix[0].size();
    int minRow = 0;
    int maxRow = matrix.size();

    for (int i=0; i<t; i++) {
      r += dr;
      c += dc;
      result.push_back(matrix[r][c]);
      if ((r == minRow && c == minCol) || (minCol == -1 && c==0)) {
        maxCol--;
        maxRow--;
        if (minCol < maxCol) {
          dr = 0;
          dc = 1;
        }
      } else if (r == maxRow && c == maxCol) {
        minRow++;
        minCol++;
        dr = 0;
        dc = -1;
        continue;
      }
      
      if (r == maxRow && c == minCol) {
        if (minRow < maxRow) {
          dr = -1;
          dc = 0;
        }
      } else if (r == minRow && c == maxCol) {
        dr = 1;
        dc = 0;
      }
    }

    return result;
  }
};
```
