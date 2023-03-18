---
title: Longest Palindromic Substring
platform: LeetCode
number: 5
author: jose
layout: post
language: en
date: 2023-03-15 08:05 +0300
categories: [programming, twopointers]
tags: [c/c++, leetcode, twopointers]
difficulty: medium
source: https://leetcode.com/problems/longest-palindromic-substring/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given a string `s`, return **the longest palindromic substring** in `s`.  

## Examples
---
### **Example 1:**  
>**Input:** s = "babad"  
>**Output:** "bab"  
>**Explanation:** "aba" is also a valid answer.  
  
### **Example 2:**  
>**Input:** s = "cbbd"  
>**Output:** "bb"  
  
## Constraints
---
- `1 <= s.length <= 1000`
- `s` consist of only digits and English letters.

## Solution
---
We will use two pointers.
  - We will iterate through every character.
  - For each character, one pointer will be to the left and the other to the right.
    - Using the character as the center: As long as the character at the pointers position are equal, we calculate the size and update the longest palindomic string found to this point, and we "expand" the pointers (move one place to the left and right)
    - For palindromic string of even size, we start with the pointers one next to the other, and we do the same process of comparing and expanding.

```c++
class Solution {
public:
  string longestPalindrome(string s) {
    string result = ""s + s[0];

    int l = 0;
    int r = 0;
    int m = 1;
    for (int i=1; i<s.size(); i+=1) {
      l = i-1;
      r = i+1;
      while (l>=0 && r<s.size() && s[l] == s[r]) {
        if ((r-l) + 1 > m) {
          m = (r-l) + 1;
          result = s.substr(l, m);
        }
        l--;
        r++;
      }
      l = i-1;
      r = i;
      while (l>=0 && r<s.size() && s[l] == s[r]) {
        if ((r-l) + 1 > m) {
          m = (r-l) + 1;
          result = s.substr(l, m);
        }
        l--;
        r++;
      }
    }

    return result;
  }
};
```
