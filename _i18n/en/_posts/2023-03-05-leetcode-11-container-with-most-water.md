---
title: Container With Most Water
platform: LeetCode
number: 11
author: jose
layout: post
language: en
date: 2023-03-05 17:25 +0300
categories: [programming, twopointers]
tags: [c/c++, contests, leetcode, two pointers]
difficulty: medium
source: https://leetcode.com/problems/container-with-most-water
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the <code>i<sup>th</sup></code> line are `(i, 0)` and `(i, height[i])`.  

Find two lines that together with the x-axis form a container, such that the container contains the most water.  

Return *the maximum amount of water a container can store*.  

**Notice** that you may not slant the container.  

## Examples
---
### **Example 1:**  
<img src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg" height="40%"/>  

>**Input:** height = [1,8,6,2,5,4,8,3,7]  
>**Output:** 49  
>**Explanation:** The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.  

### **Example 2:**  
>**Input:** height = [1,1]  
>**Output:** 1  

## Constraints
---
- `n == height.length`
- <code>2 <= n <= 10<sup>5</sup></code>
- <code>0 <= height[i] <= 10<sup>4</sup></code>

## Solution
---
We will use two pointers (indexes), `l` (left) and `r` (right):
  - `l` starts at index `0`.
  - `r` starts at the last index.
  - While `l < r`:
    - Calculate area (`shortest_bar * distance_between_bars`)
    - If the area is bigger, then we update the area.
    - Move the pointers:
      - If `l` bar shorter, then move `l` to the right.
      - Else move `r` to the left.
  - Return the max area.  

---
```c++
class Solution {
public:
  int maxArea(vector<int>& height) {
    int l = 0;
    int r = height.size() - 1;
    int max = 0;

    while (l < r) {
      int area = (r - l) * min(height[r], height[l]);
      if (area > max) max = area;

      if (height[l] < height[r])
        l += 1;
      else
        r -= 1;
    }

    return max;
  }
};
```
