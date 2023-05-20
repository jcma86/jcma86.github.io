---
title: Remove Invalid Parentheses
platform: LeetCode
number: 301
author: jose
layout: post
language: en
date: 2023-03-04 23:58 +0300
categories: [programming, dfsbfs]
tags: [c/c++, contests, leetcode, dfsbfs]
difficulty: hard
source: https://leetcode.com/problems/remove-invalid-parentheses
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
Given a string `s` that contains parentheses and letters, remove the minimum number of invalid parentheses to make the input string valid.  

Return *a list of **unique strings** that are valid with the minimum number of removals*. You may return the answer in **any order**.  

## Examples
---
### **Example 1:**  
>**Input:** s = "()())()"  
>**Output:** ["(())()","()()()"]  

### **Example 2:**  
>**Input:** s = "(a)())()"  
>**Output:** ["(a())()","(a)()()"]  

### **Example 3:**  
>**Input:** s = ")("  
>**Output:** [""]  

## Constraints
---
- `1 <= s.length <= 25`
- `s` consists of lowercase English letters and parentheses `'('` and `')'`.
- There will be at most `20` parentheses in `s`.

## Solution
---
We will use recursion (Deep First Search).
  - To know is the string is invalid, we start iterating through every character.
    - If the character `== '('` we count `+ 1`.
    - If the character `== ')'` we count `- 1`.
    (We know that, the moment the count becomes negative, then we have an extra closing parentheses)
    - We call recursively but passing the string with the first closing parentheses eliminated **if the previous character is different**, and with the current indexes of where was found the extra parentheses and of the current character. Otherwhise we continue iterating till the position where our original counting became 0.

  We also have to identify extra opening parentheses... we can iterate backwards or just simply reverse the string once the count remained `>= 0`, once we explore the reversed string, then we can add the final string to the results.

---
```c++
class Solution {
public:
  vector<string> result;

  void sanitize(string s, int li, int lj, bool reversed) {
    char a = reversed ? ')' : '(';
    char b = reversed ? '(' : ')';
    
    int count = 0;
    int i;
    for (i=li; i<s.size(); i+=1) {
      if (s[i] == a) count += 1;
      else if (s[i] == b) count -= 1;

      if (count >= 0) continue;

      for (int j = lj; j <= i; j+=1) {
        if (s[j] == b && (j == lj || s[j - 1] != b))
          sanitize(s.substr(0, j) + s.substr(j + 1), i, j, reversed);
      }
      return;
    }

    if (!reversed) {
      reverse(s.begin(), s.end());
      sanitize(s, 0, 0, true);
    } else{
      string r = s;
      reverse(r.begin(), r.end());
      result.push_back(r);
    }
  }

  vector<string> removeInvalidParentheses(string s) {
    sanitize(s, 0, 0, false);
    return result;
  }
};
```
