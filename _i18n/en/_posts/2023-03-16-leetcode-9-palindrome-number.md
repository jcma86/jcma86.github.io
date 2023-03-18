---
title: Palindrome Number
platform: LeetCode
number: 9
author: jose
layout: post
language: en
date: 2023-03-16 09:00 +0300
categories: [programming, others]
tags: [c/c++, leetcode, others]
difficulty: easy
source: https://leetcode.com/problems/palindrome-number/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given an integer `x`, return *`true` if `x` is a **palindrome**, and `false` otherwise*.

## Examples
---
### **Example 1:**  
>**Input:** x = 121  
>**Output:** true  
>**Explanation:**  121 reads as 121 from left to right and from right to left.  
  
### **Example 2:**  
>**Input:** x = -121  
>**Output:** false  
>**Explanation:**  From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.  

### **Example 3:**  
>**Input:** x = 10  
>**Output:** false  
>**Explanation:**  Reads 01 from right to left. Therefore it is not a palindrome.  

## Constraints
---
- -2<sup>31</sup> <= x <= 2<sup>31</sup> - 1

**Follow up:** Could you solve it without converting the integer to a string?

## Solution
---

```c++
class Solution {
public:
  bool isPalindrome(int x) {
    if (x < 0 || (x != 0 && x % 10 == 0)) 
      return false;

    int tmp = x;
    long rev = 0;
    
    while (tmp > 0) {
      int mod = tmp % 10;
      tmp /= 10;
      
      rev = (rev * 10) + mod;
    }
    
    return rev == x;
  }
};
```
