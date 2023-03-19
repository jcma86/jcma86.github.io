---
title: Find the Index of the First Occurrence in a String
platform: LeetCode
number: 28
author: jose
layout: post
language: en
date: 2023-03-18 04:30 +0300
categories: [programming, others]
tags: [c/c++, leetcode, others]
difficulty: easy
source: https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given two strings `needle` and `haystack`, return the index of the first occurrence of `needle` in `haystack`, or -`1` if `needle` is not part of `haystack`.  

## Examples
---
### **Example 1:**
>**Input:** haystack = "sadbutsad", needle = "sad"  
>**Output:** 0  
>**Explanation:** "sad" occurs at index 0 and 6.  
>The first occurrence is at index 0, so we return 0.  

### **Example 2:**
>**Input:** haystack = "leetcode", needle = "leeto"  
>**Output:** -1  
>**Explanation:** "leeto" did not occur in "leetcode", so we return -1.  

## Constraints
---
- <code>1 <= haystack.length, needle.length <= 10<sup>4</sup></code>  
- `haystack` and `needle` consist of only lowercase English characters.  

## Solution
---
Having two indexes, `h` for the haystack and `n` for the needle:  
  - We move through the haystack,
  - If  `haystack[h] == needle[n]`, then we move both indexes togheter.
  - If `n` reads the whole needle string, then we have a match, we return the index where it started.
  - We reset `n`, and we move `h` to the next position where neddle and haystack started to match.
  - `return -1`

```c++
class Solution {
public:
  int strStr(string haystack, string needle) {
    int n=0;
    int h=0;

    while (h<haystack.size()) {
      while (haystack[h] == needle[n] && n<needle.size()) {
        n++;
        h++;
      }
      if (n == needle.size())
        return h - needle.size();

      h -= n;
      n = 0;
      h++;
    }
    return -1;
  }
};
```
