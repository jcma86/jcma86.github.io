---
title: Divide Two Integers
platform: LeetCode
number: 29
author: jose
layout: post
language: en
date: 2023-03-18 14:00 +0300
categories: [programming, bw]
tags: [c/c++, leetcode, bw]
difficulty: medium
source: https://leetcode.com/problems/divide-two-integers/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given two integers `dividend` and `divisor`, divide two integers without using multiplication, division, and mod operator.  

The integer division should truncate toward zero, which means losing its fractional part. For example, `8.345` would be truncated to `8`, and `-2.7335` would be truncated to `-2`.  

Return *the **quotient** after dividing `dividend` by `divisor`*.  

Note: Assume we are dealing with an environment that could only store integers within the 32-bit signed integer range: <code>[−2<sup>31</sup>, 2<sup>31</sup> − 1]</code>. For this problem, if the quotient is strictly greater than <code>2<sup>31</sup> - 1</code>, then return <code>2<sup>31</sup> - 1</code>, and if the quotient is strictly less than <code>-2<sup>31</sup></code>, then return <code>-2<sup>31</sup></code>.  

## Examples
---
### **Example 1:**
>**Input:** dividend = 10, divisor = 3  
>**Output:** 3  
>**Explanation:** 10/3 = 3.33333.. which is truncated to 3.  

### **Example 2:**
>**Input:** dividend = 7, divisor = -3  
>**Output:** -2  
>**Explanation:** 7/-3 = -2.33333.. which is truncated to -2.  

## Constraints
---
- <code>-2<sup>31</sup> <= dividend, divisor <= 2<sup>31</sup> - 1</code>  
- `divisor != 0`  

## Solution
---
- There are three cases that we can handle directly:  
  - Division by 1.
  - Division of the minimum possible integer for a 32-bit signed integer.
  - Divident and divisor are equal.

- Once handled those cases, we can proceed with the division. I can think of two possible solutions:  
  1. As long as the `dividend >= divisor`.  
    - Substract the divisor from the dividend.  
    - Count how many times has been substracted.  
  2. Using bitwise operations, we can count, with bigger steps, how many times we can substrac the divisor from the dividend. this is the optimal solution.  
    - As long as the `dividen >= divisor`  
      - As long as the `divisor <= dividend`  
        - Perform a `left shift` (same as multiplying by 2) with the `divisor`.  
        - We do a `left shift` to a counter that started at `1`.  
      - Substract the final result of the `divisor` from the `dividend`.  
      - Add to our result the value of the counter we shifted too.  
    - Finally, we verify if the `dividend < 0 XOR divisor < 0` to know if the result will be negative.  

  We need to prevent to go outside the range of a 32-bit integer, for that, we verify at every iteration if the `INT_MAX - shifted_divisor <= shifted_divisor`. Once this condition is `true` means that for next shifting the value will be equal or greather than the max value, so, we can prevent it.  

```c++
class Solution {
public:
  int divide(int dividend, int divisor) {
    if (dividend == INT_MIN && divisor == 1) return INT_MIN;
    if (dividend == INT_MIN && divisor == -1) return INT_MAX;

    if (dividend == divisor)
      return (dividend < 0) != (divisor < 0) ? -1: 1;

    unsigned int a = abs(dividend);
    unsigned int b = abs(divisor);
    unsigned int tmp = 0;
    unsigned int quotient = 0;

    while (a >= b) {
      tmp = b;
      int i = 1;
      while(tmp << 1 <= a) {
        tmp <<= 1;
        i <<= 1;
        if (INT_MAX - tmp <= tmp)
          break;
      }
      a -= tmp;
      quotient += i;
    }

    return (dividend < 0) != (divisor < 0) ? -quotient : quotient;
  }
};
```
