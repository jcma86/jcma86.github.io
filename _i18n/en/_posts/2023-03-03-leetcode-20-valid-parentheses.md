---
title: Valid Parentheses
platform: LeetCode
number: 20
author: jose
layout: post
language: en
date: 2023-03-03 02:30 +0300
categories: [programming, stack]
tags: [c/c++, contests, leetcode, stack]
difficulty: easy
source: https://leetcode.com/problems/valid-parentheses
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.  

An input string is valid if:  

Open brackets must be closed by the same type of brackets.  
Open brackets must be closed in the correct order.  
Every close bracket has a corresponding open bracket of the same type.  

## Examples
---
### **Example 1:**  
>**Input:** s = "()"  
>**Output:** true

### **Example 2:**  
>**Input:** s = "()[]{}"  
>**Output:** true  

### **Example 3:**  
>**Input:** s = "(]"  
>**Output:** false  

## Constraints
---
- <code>1 <= s.length <= 10<sup>4</sup></code>
- `s` consists of parentheses only `'()[]{}'`.

## Solution
---
Using stack:
  - If the string length is odd, return `false`.
  - For every character:
    - If is an open parentheses, push to the stack.
    - If is a close parentheses:
      - If stack is empty, return `false`.
      - Pop from stack and verify if the close parentheses corresponds to the open one (the one poped).
        - If not, return `false`.
  - Once finish, if the stack is empty, return `true`, otherwise `false`.

---
```c++
class Solution {
public:
  bool isValid(string s) {
    if (s.size() % 2 != 0)
      return false;

    unordered_map<char, char> m;
    stack<char> st;

    m[')'] = '(';
    m['}'] = '{';
    m[']'] = '[';

    for (int i=0; i<s.size(); i+=1) {
      if (s[i] == '(' || s[i] == '{' || s[i] == '[') {
        st.push(s[i]);
      } else {
        if (st.empty() || st.top() != m[s[i]]) 
          return false;
        st.pop();
      }
    }

    return st.empty();
  }
};
```
