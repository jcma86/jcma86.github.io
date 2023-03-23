---
title: Pow(x, n)
platform: LeetCode
number: 50
author: jose
layout: post
language: en
date: 2023-03-22 16:00 +0300
categories: [programming, bw]
tags: [c/c++, leetcode, bw]
difficulty: medium
source: https://leetcode.com/problems/powx-n/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Implement `pow(x, n)`, which calculates `x` raised to the power `n` (i.e., <code>x<sup>n</sup></code>).  

## Examples
---
### **Example 1:**
>**Input:** x = 2.00000, n = 10  
>**Output:** 1024.00000  

### **Example 2:**
>**Input:** x = 2.10000, n = 3  
>**Output:** 9.26100  

### **Example 3:**
>**Input:** x = 2.00000, n = -2  
>**Output:** 0.25000  
>**Explanation:** 2<sup>-2</sup> = 1/2<sup>2</sup> = 1/4 = 0.25  

## Constraints
---
- `-100.0 < x < 100.0`  
- <code>-2<sup>31</sup> <= n <= 2<sup>31</sup>-1</code>  
- `n` is an integer.  
- <code>-10<sup>4</sup> <= x<sup>n</sup> <= 10<sup>4</sup></code>  

## Solution
---
Instead of multiplying by `x`  `n-times` we will optimize (reduce the amount of times we multiply) using the [*right-shift*](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/) [**bitwise**](/categories/bw/) operation.  

- We initialize our `result = 1`.  
- While `n > 0` (we use the absolute value of n).  
- If the last (LSB) of `n` is `1` we multiply `result * x`.  
- We multiply `x` by itself (`x * x`).  
- And `right-shift` `n` (`n >> 1`).
- Finally, if the original `n<0`, then the result will be `1/result` otherwise `result`.  

```c++
class Solution {
public:
  double myPow(double x, int n) {
    double ans = 1.0;
    bool neg = n < 0;
    n = abs(n);
    while (n > 0) {
      if (n & 1)
        ans = ans * x;
 
      x = x * x;
      n = n >> 1;
    }

    return neg ? 1 / ans: ans;
  }
};
```
