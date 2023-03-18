---
title: Generate Parentheses
platform: LeetCode
number: 22
author: jose
layout: post
language: en
date: 2023-03-17 08:40 +0300
categories: [programming, dynamicp]
tags: [c/c++, leetcode, dynamicp]
difficulty: medium
source: https://leetcode.com/problems/generate-parentheses/
proglang: C/C++
math: true
mermaid: true
pin: true
---

## {% t posts.problem %}

---
Given `n` pairs of parentheses, write a function to *generate all combinations of well-formed parentheses*.

## Examples

---

### **Example 1:**  
  
>**Input:** n = 3  
>**Output:** ["((()))","(()())","(())()","()(())","()()()"]  
  
### **Example 2:**  

>**Input:** n = 1  
>**Output:** ["()"]  

## Constraints

---

- `1 <= n <= 8`

## Solution

---

- We will use Dynamic Programing.  
- We know that we need `n` open parentheses `'()'` and `n` close parentheses `')'`.  
- There cannot be (at any time) less `'('` than `')'` in our current solution.  
- The method will count how many `'('` and `')'` are still availabe to add to the current solution.  
- Once there are `0` `'('` than `')'` left, we add that solution to the final result.  

```c++
class Solution {

private:
  vector<string> result;
  void generate(string s, int o, int c) {
    if (o == 0 && c == 0)
      result.push_back(s);
    
    if (o)
      generate(s + "(", o - 1, c);
    if (o<c)
      generate(s + ")", o, c - 1);
  }

public:
  vector<string> generateParenthesis(int n) {
    generate("", n, n);
    return result;
  }
};
```
