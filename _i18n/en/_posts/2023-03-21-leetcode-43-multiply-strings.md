---
title: Multiply Strings
platform: LeetCode
number: 43
author: jose
layout: post
language: en
date: 2023-03-21 01:27 +0300
categories: [programming, others]
tags: [c/c++, leetcode, others]
difficulty: medium
source: https://leetcode.com/problems/multiply-strings/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given two non-negative integers `num1` and `num2` represented as strings, return the product of `num1` and `num2`, also represented as a string.  

**Note**: You must not use any built-in BigInteger library or convert the inputs to integer directly.  

## Examples
---
### **Example 1:**
>**Input:** num1 = "2", num2 = "3"  
>**Output:** "6"  

### **Example 2:**
>**Input:** num1 = "123", num2 = "456"  
>**Output:** "56088"  

## Constraints
---
- `1 <= num1.length, num2.length <= 200`  
- `num1` and `num2` consist of digits only.  
- Both `num1` and `num2` do not contain any leading zero, except the number `0` itself.  

## Solution
---
The solution is simple, I just follow this steps:  
<img src="https://d138zd1ktt9iqe.cloudfront.net/media/seo_landing_files/2-digit-multiplication-01-1-1654146332.png" width="70%"/>  
<sub>*source:* [*https://www.cuemath.com/numbers/2-digit-multiplication/*](https://www.cuemath.com/numbers/2-digit-multiplication/)</sub>  

The only difference is, in the step 2 I'm adding the previous while multiplying.  

```c++
class Solution {
public:
  string multiply(string num1, string num2) {
    if (num1 == "0" || num2 == "0")
      return "0";
    if (num1 == "1" || num2 == "1")
      return num1 == "1" ? num2 : num1;

    int p0=0;
    int p1=0;
    string ans="";
    for (int b=num2.size()-1; b>=0; b--) {
      int c = 0;
      p1 = p0;
      for (int a=num1.size()-1; a>=0; a--) {
        int r = ((num2[b] - 48) * (num1[a] - 48)) + c;
        if (ans.size() > 0 && p1 < ans.size())
          r += (ans[(ans.size()-1) - p1] - 48);
        
        c = r / 10;
        r = r % 10;

        if (p0>0 and p1 < ans.size())
          ans[ans.size()-1-p1] = r + 48;
        else
          ans = to_string(r) + ans;

        if (a == 0 && c != 0)
          ans = to_string(c) + ans;

        p1++;
      }
      p0++;
    }
    return ans;
  }
};
```
