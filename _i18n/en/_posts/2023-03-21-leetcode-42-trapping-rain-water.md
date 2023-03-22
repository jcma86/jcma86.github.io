---
title: Trapping Rain Water
platform: LeetCode
number: 42
author: jose
layout: post
language: en
date: 2023-03-21 11:30 +0300
categories: [programming, twopointers]
tags: [c/c++, leetcode, twopointers]
difficulty: hard
source: https://leetcode.com/problems/trapping-rain-water/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.    

## Examples
---
### **Example 1:**
<img src="https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png" />  

>**Input:** height = [0,1,0,2,1,0,1,3,2,1,2,1]  
>**Output:** 6  
>**Explanation:** The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.  

### **Example 2:**
>**Input:** height = [4,2,0,3,2,5]  
>**Output:** 9  

## Constraints
---
- `n == height.length`  
- <code>1 <= n <= 2 * 10<sup>4</sup></code>  
- <code>0 <= height[i] <= 10<sup>5</sup></code>  

## Solution
---
To be able to trap water at the <code>i<sup>th</sup></code> position is necessary to have a higher wall to the left and to the right. To be able to do this, we will use the [**two pointers**](/categories/twopointers/) technique in order to identify a wall to the left and right.  

- We initialize our pointers `l` and `r` to the first ans last position of the array.  
- At every point, we will keep tracking of what is the `higher left` and `higher right` (`lMax` and `rMax`) bars so far "discovered".  
- If the `height[l] <= height[r]` we will update our `lMax` or add the amount of water hold at that position to our final result, and move `l`.  
- Else, we do the same but for `r` and `rMax`.  

```c++
class Solution {
public:
  int trap(vector<int>& height) {
    int res = 0;

    int l = 0;
    int r = height.size() - 1;
    int lMax = 0;
    int rMax = 0;

    while (l<=r) {
      if (height[l]<=height[r]) {
        if (height[l]>=lMax)
          lMax = height[l];
        else
          res += lMax - height[l];
        l++;
      } else {      
        if (height[r]>=rMax)
          rMax = height[r];
        else
          res += rMax-height[r];
        r--;
      }
    }
    return res;
  }
};
```
