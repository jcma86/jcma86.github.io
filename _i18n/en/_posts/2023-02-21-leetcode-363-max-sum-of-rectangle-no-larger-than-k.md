---
title: Max Sum of Rectangle No Larger Than K
platform: LeetCode
number: 363
author: jose
layout: post
language: en
date: 2023-02-21 17:30:00 +0300
categories: [programming, ps]
tags: [algorithms, c/c++, contests, leetcode, prefix sum]
difficulty: hard
source: https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/
proglang: C/C++
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
Given an `m x n` matrix `matrix` and an integer `k`, return *the max sum of a rectangle in the matrix such that its sum is no larger than* `k`.  

It is **guaranteed** that there will be a rectangle with a sum no larger than `k`.  

## Examples
---
### **Example 1:**  
![Matrix example](https://assets.leetcode.com/uploads/2021/03/18/sum-grid.jpg "Example")
>**Input:** matrix = [[1,0,1],[0,-2,3]], k = 2  
>**Output:** 2  
>  
>**Explanation:** Because the sum of the blue rectangle [[0, 1], [-2, 3]] is 2, and 2 is the max number no larger than k (k = 2).  

### **Example 2:**  
>**Input:** matrix = [[2,2,-1]], k = 3  
>**Output:** 3  

## Constraints
---
- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 100`
- `-100 <= matrix[i][j] <= 100`
- <code>-10<sup>5</sup> <= k <= 10<sup>5</sup></code>  

## Solution
---
```c++
class Solution {
public:
  int maxSumSubmatrix(vector<vector<int>>& matrix, int k) {
    int rows = matrix.size();
    int cols = matrix[0].size();
    bool end = false;
    int max = -INT_MAX;
    
    for (int r = 0; r < rows; r += 1) {
      int cSum = 0;
      for (int c = 0; c < cols; c += 1) {
        cSum += matrix[r][c];
        matrix[r][c] = r == 0 ? cSum : (cSum + matrix[r - 1][c]);

        for (int r1 = r; r1 >= 0; r1 -= 1) {
          for (int c1 = c; c1 >= -1; c1 -= 1) {
            int tmp = matrix[r][c];
            if (c1 == c && r1 == r) {}
            else {
              if (r == 0 && c1 != c && c1 >= 0) {
                tmp -= matrix[r][c1];
              } else {
                if (c > 0 && c1 >= 0)
                  tmp -= matrix[r][c1];
                if (r > 0 && r1 >= 0)
                  tmp -= matrix[r1][c];
                if (c > 0 && r > 0 && r1 >= 0 && c1 >= 0)
                  tmp += matrix[r1][c1];
              }
            }
            if (tmp >= max && tmp <= k) {
              max = tmp;
            }
            if (max == k) {
              end = true;
              break;
            }
          }
          if (end)
            break;
        }

        if (max == k) {
          end = true;
          break;
        }
      }
      if (end)
        break;
    }
    
    return max;
  }
};
```
