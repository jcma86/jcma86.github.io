---
title: Sqrt(x)
platform: LeetCode
number: 69
author: jose
layout: post
language: en
date: 2023-03-30 18:30 +0300
categories: [programming, bs]
tags: [c/c++, leetcode, bs]
difficulty: easy
source: https://leetcode.com/problems/sqrtx/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given a non-negative integer `x`, return *the square root of `x` rounded down to the nearest integer*. The returned integer should be **non-negative** as well.  

You must not use any built-in exponent function or operator.  

* For example, do not use `pow(x, 0.5)` in c++ or `x ** 0.5` in python.  

## Examples
---
### **Example 1:**
>**Input:** x = 4  
>**Output:** 2  
>**Explanation:** The square root of 4 is 2, so we return 2.  

### **Example 2:**
>**Input:** x = 8  
>**Output:** 2  
>**Explanation:** The square root of 8 is 2.82842..., and since we round it down to the nearest integer, 2 is returned.  

## Constraints
---
- <code>0 <= x <= 2<sup>31</sup> - 1</code>  

## Solution
---
This can be solved with **[Binary Search](/categories/bs/)** where the `mid` value is the candidate `sqrt`.  

```c++
class Solution {
public:
  int mySqrt(int x) {
    int l=0;
    int r=x;
    int res = 0;

    while (l<=r) {
      long int m = (l+r) / 2;

      if ((m*m) == x)
        return m;
      else if ((m*m) > x)
        r = m - 1;
      else {
        l = m + 1;
        res = m;
      }
    }
    return res;
  }
};
```
