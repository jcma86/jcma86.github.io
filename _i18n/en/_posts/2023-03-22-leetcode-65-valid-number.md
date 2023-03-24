---
title: Valid Number
platform: LeetCode
number: 65
author: jose
layout: post
language: en
date: 2023-03-22 23:00 +0300
categories: [programming, set, fsm]
tags: [c/c++, leetcode, set, fsm]
difficulty: hard
source: https://leetcode.com/problems/valid-number/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
A **valid number** can be split up into these components (in order):  

A **decimal number** or an **integer**.  
(Optional) An `'e'` or `'E'`, followed by an **integer**.  
A **decimal number** can be split up into these components (in order):  

(Optional) A sign character (either `'+'` or `'-'`).  
One of the following formats:  
One or more digits, followed by a dot `'.'`.  
One or more digits, followed by a dot `'.'`, followed by one or more digits.  
A dot `'.'`, followed by one or more digits.  
An integer can be split up into these components (in order):  

(Optional) A sign character (either `'+'` or `'-'`).  
One or more digits.  

For example, all the following are valid numbers: ["2", "0089", "-0.1", "+3.14", "4.", "-.9", "2e10", "-90E3", "3e+7", "+6e-1", "53.5e93", "-123.456e789"], while the following are not valid numbers: ["abc", "1a", "1e", "e3", "99e2.5", "--6", "-+3", "95a54e53"].

Given a string `s`, return *`true` if `s` is a **valid number***.

## Examples
---
### **Example 1:**
>**Input:** s = "0"  
>**Output:** true  

### **Example 2:**
>**Input:** s = "e"  
>**Output:** false  

### **Example 3:**
>**Input:** s = "."  
>**Output:** false  

## Constraints
---
- `1 <= s.length <= 20`  
- `s` consists of only English letters (both uppercase and lowercase), digits (`0-9`), plus `'+'`, minus `'-'`, or dot `'.'`.  

## Solution
---
My approach to this problem is to use a ***[FSM](https://en.wikipedia.org/wiki/Finite-state_machine)*** type of solution.
  - We read the string character at a time.  
  - For every read, we should know what characters are not allowed at that moment. For example:  
    - At the start, it is not allowed to have an `'e'`.  
    - After an `'e'` is not allowed to have a dot `'.'`'  
    - After a number, is not allowed to have a sign `'+'` nor `'-'`. 
    - ...
  - If we found a not allowed character, we return `false`.  
  - Once finish, if we still need a number, return `false`.  
  - Return `true`.  

### Solution 1:
---
```c++
class Solution {
public:
  bool isNumber(string s) {
    if (s.size() == 1 && (s[0] < '0' || s[0] > '9'))
      return false;

    set<char> notValid({'e'});
    bool hasInt = false;
    bool hasDot = false;
    bool needsNum = false;
    bool hasE = false;
    char last;

    for (int i=0; i<s.size(); i++) {
      if (notValid.find(tolower(s[i])) != notValid.end())
        return false;
      
      if (s[i] >= '0' && s[i] <= '9') {
        needsNum = false;
        notValid.insert('-');
        notValid.insert('+');
        if (!hasDot && !hasE)
          hasInt = true;
        if (!hasE)
          notValid.erase('e');
        continue;
      }

      if (needsNum && last != 'e')
        return false;
      else if (s[i] == '.') {
        hasDot = true;
        if (hasInt)
          notValid.erase('e');
        else
          needsNum = true;
        notValid.insert('.');
        notValid.insert('-');
        notValid.insert('+');
      } else if (s[i] == '+' || s[i] == '-') {
        notValid.insert('+');
        notValid.insert('-');
        if (!hasE)
          notValid.erase('.');
      } else if (tolower(s[i]) == 'e') {
        needsNum = true;
        hasE = true;
        notValid.clear();
        notValid.insert('e');
        notValid.insert('.');
      } else
        return false;

      last = tolower(s[i]);
    }  

    return !needsNum;
  }
};
```
