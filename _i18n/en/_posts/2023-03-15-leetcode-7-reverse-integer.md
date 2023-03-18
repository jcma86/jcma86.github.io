---
title: Reverse Integer
platform: LeetCode
number: 7
author: jose
layout: post
language: en
date: 2023-03-15 18:00 +0300
categories: [programming, others]
tags: [c/c++, leetcode, others]
difficulty: medium
source: https://leetcode.com/problems/reverse-integer/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given a signed 32-bit integer `x`, return *`x` with its digits reversed*. If reversing `x` causes the value to go outside the signed 32-bit integer range <code>[-2<sup>31</sup>, 2<sup>31</sup> - 1]</code>, then return `0`.  

**Assume the environment does not allow you to store 64-bit integers (signed or unsigned).**  

## Examples
---
### **Example 1:**  
>**Input:** x = 123  
>**Output:** 321  
  
### **Example 2:**  
>**Input:** x = -123  
>**Output:** -321  

### **Example 3:**  
>**Input:** x = 120  
>**Output:** 21  

## Constraints
---
- <code>-2<sup>31</sup> <= x <= 2<sup>31</sup> - 1</code>

## Solution
---
- We initialize a new number (our result) to `0`.
- We just divide by 10 the number ang get the module.
- We multiply by 10 our result and then we add the module of the previous step.
- We continue until we can not get more modules.
- For each step, we calculate if the result will be outside the range once multiplied by 10, if so, we return 0.

```c++
class Solution {
public:
  int reverse(int x) {
    int tmp = x;
    int result = 0;
    int d;

    while (tmp != 0) {
      d = tmp % 10;
      if ((INT_MAX/10) - abs(result) < 0)
        return 0;

      result = (result * 10) + d;
      tmp /= 10;
    }

    return result; 
  }
};
```
