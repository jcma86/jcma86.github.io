---
title: Add Binary
platform: LeetCode
number: 67
author: jose
layout: post
language: en
date: 2023-03-30 03:00 +0300
categories: [programming, others]
tags: [c/c++, leetcode, others]
difficulty: easy
source: https://leetcode.com/problems/add-binary/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given two binary strings `a` and `b`, return *their sum as a binary string*.  

## Examples
---
### **Example 1:**
>**Input:** a = "11", b = "1"  
>**Output:** "100"  

### **Example 2:**
>**Input:** a = "1010", b = "1011"  
>**Output:** "10101"  

## Constraints
---
- <code>1 <= a.length, b.length <= 10<sup>4</sup></code>  
- `a` and `b` consist only of `'0'` or `'1'` characters.  
- Each string does not contain leading zeros except for the zero itself.  

## Solution
---
- We take the last character of both strings.  
- Add them (`1 + 1 = 0` or `0 + 0 = 0` otherwise `1`)  
- Add the previous result with a "carried" value (initially 0).  
- If at least two (of the charatesr from string one, from string two and carried value) are `1`, then we carry `1` for next iteration.  
- Once finish, if we still carry a value, or the first charachter of result is `0`, then we add a `1` at the start of the string.  

```c++
class Solution {
public:
  string addBinary(string a, string b) {
    int i=0;
    bool c = false;
    string s = ""s;
    while (i<a.size() || i<b.size()) {
      char aa = '0';
      char bb = '0';
      s = '0' + s;

      if (i<a.size())
        aa = a[a.size() - 1 - i];
      if (i<b.size())
        bb = b[b.size() - 1 - i];

      if (!(aa == '1') != !(bb == '1'))
        s[0] = '1';
      else
        s[0] = '0';

      if (!(s[0] == '1') != !c)
        s[0] = '1';
      else
        s[0] = '0';

      c = ((aa - 48) + (bb - 48) + (int)c) > 1;
      
      i++;
    }
    if (c || (s[0] == '0' && s.size() > 1))
      s = '1' + s;

    return s;
  }
};
```
