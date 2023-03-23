---
title: Rotate Image
platform: LeetCode
number: 48
author: jose
layout: post
language: en
date: 2023-03-22 15:00 +0300
categories: [programming, twopointers, others]
tags: [c/c++, leetcode, twopointers, others]
difficulty: medium
source: https://leetcode.com/problems/rotate-image/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
You are given an `n x n` 2D `matrix` representing an image, rotate the image by **90** degrees (clockwise).  

You have to rotate the image **in-place**, which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.  

## Examples
---
### **Example 1:**
![](https://assets.leetcode.com/uploads/2020/08/28/mat1.jpg)
>**Input:** matrix = [[1,2,3],[4,5,6],[7,8,9]]  
>**Output:** [[7,4,1],[8,5,2],[9,6,3]]  

### **Example 2:**
![](https://assets.leetcode.com/uploads/2020/08/28/mat2.jpg)
>**Input:** matrix = [[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]  
>**Output:** [[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]  

## Constraints
---
- `n == matrix.length == matrix[i].length`  
- `1 <= n <= 20`  
- `-1000 <= matrix[i][j] <= 1000`  

## Solution
---
To rotate a matrix 90 degrees, first we [**transpose**](https://en.wikipedia.org/wiki/Transpose) it  and then we reverse each row.  

To reverse the rows I wil use a [two pointers](/categories/twopointers/) technique.  

```c++
class Solution {
public:
  void rotate(vector<vector<int>>& matrix) {
    for (int r=0; r<matrix.size(); r++)
      for (int c=r; c<matrix.size(); c++)
        swap(matrix[r][c], matrix[c][r]);
    
    for (int i=0; i<matrix.size(); i++) {
      int l = 0;
      int r = matrix.size() - 1;
      while (l<r) {
        swap(matrix[i][l], matrix[i][r]);
        l++;
        r--;
      }
    }
  }
};
```
