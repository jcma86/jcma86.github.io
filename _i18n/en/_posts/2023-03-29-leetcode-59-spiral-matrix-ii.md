---
title: Spiral Matrix II
platform: LeetCode
number: 59
author: jose
layout: post
language: en
date: 2023-03-29 01:50 +0300
categories: [programming, others]
tags: [c/c++, leetcode, others]
difficulty: medium
source: https://leetcode.com/problems/spiral-matrix-ii/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given a positive integer `n`, generate an `n x n` `matrix` filled with elements from `1` to <code>n<sup>2</sup></code> in spiral order.  

## Examples
---
### **Example 1:**
<img src="https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg" width="90%" />  
>**Input:** n = 3  
>**Output:** [[1,2,3],[8,9,4],[7,6,5]]  

### **Example 2:**
>**Input:** n = 1  
>**Output:** [[1]]  

## Constraints
---
- `1 <= n <= 20`  

## Solution
---
Same solution that the one for [**problem 54**](../../28/leetcode-54-spiral-matrix/), but instead of reading a value, we write a value.  

```c++
class Solution {
public:
  vector<vector<int>> generateMatrix(int n) {
    vector<vector<int>> result(n, vector<int>(n));

    int dr = 0;
    int dc = 1;
    int r = 0;
    int c = -1;
    int minCol = -1;
    int maxCR = n;
    int minRow = 0;

    for (int i=1; i<=(n*n); i++) {
      r += dr;
      c += dc;
      result[r][c] = i;
      if ((r == minRow && c == minCol) || (minCol == -1 && c==0)) {
        maxCR--;
        if (minCol < maxCR) {
          dr = 0;
          dc = 1;
        }
      } else if (r == maxCR && c == maxCR) {
        minRow++;
        minCol++;
        dr = 0;
        dc = -1;
        continue;
      }
      
      if (r == maxCR && c == minCol) {
        if (minRow < maxCR) {
          dr = -1;
          dc = 0;
        }
      } else if (r == minRow && c == maxCR) {
        dr = 1;
        dc = 0;
      }
    }

    return result;
  }
};
```
