---
title: Letter Combinations of a Phone Number
platform: LeetCode
number: 17
author: jose
layout: post
language: en
date: 2023-03-16 19:00 +0300
categories: [programming, dynamicp]
tags: [c/c++, leetcode, dynamicp, hashtable]
difficulty: medium
source: https://leetcode.com/problems/letter-combinations-of-a-phone-number/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.  

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.  

<img src="https://assets.leetcode.com/uploads/2022/03/15/1200px-telephone-keypad2svg.png" width="70%"/>  

## Examples
---
### **Example 1:**  
>**Input:** digits = "23"  
>**Output:** ["ad","ae","af","bd","be","bf","cd","ce","cf"]  
  
### **Example 2:**  
>**Input:** digits = ""  
>**Output:** []  

### **Example 3:**  
>**Input:** digits = "2"  
>**Output:** ["a","b","c"]  

## Constraints
---
- `0 <= digits.length <= 4`  
- `digits[i]` is a digit in the range `['2', '9']`.  

## Solution
---
Using Dynamic Programming,  
  - We will grow a string starting with the first letter of the first digit of the phone number,
  - For every letter available for the digit, we recursively call our helper method, growing the string.
  - Once the string has the same length than the phone number, we add that string to the result.

```c++
class Solution {
private:
  unordered_map<char, string> letters;
  vector<string> result;
  string *num;

  void generateStrings(string currentStr, int index) {
    if (currentStr.size() == num->size())
      result.push_back(currentStr);
    
    for (int i=0; i<letters[(*num)[index]].size(); i++)
      generateStrings(currentStr + letters[(*num)[index]][i], index + 1);
  }

public:
    vector<string> letterCombinations(string digits) {
      if (digits.size() == 0)
        return {};
      num = &digits;

      letters['2'] = "abc";
      letters['3'] = "def";
      letters['4'] = "ghi";
      letters['5'] = "jkl";
      letters['6'] = "mno";
      letters['7'] = "pqrs";
      letters['8'] = "tuv";
      letters['9'] = "wxyz";

      generateStrings("", 0);

      return result;
    }
};
```
