---
title: Valid Anagram
platform: LeetCode
number: 242
author: jose
layout: post
language: en
date: 2023-03-02 23:00 +0300
categories: [programming, hashtable]
tags: [c/c++, contests, leetcode, hash table]
difficulty: easy
source: https://leetcode.com/problems/valid-anagram
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
Given two strings `s` and `t`, return *`true` if `t` is an anagram of `s`, and `false` otherwise*.  

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.  

## Examples
---
### **Example 1:**  
>**Input:** s = "anagram", t = "nagaram"  
>**Output:** true

### **Example 2:**  
>**Input:** s = "rat", t = "car"  
>**Output:** false  

## Constraints
---
- <code>1 <= s.length, t.length <= 5 * 10<sup>4</sup></code>
- `s` and `t` consist of lowercase English letters.

**Follow up:** What if the inputs contain Unicode characters? How would you adapt your solution to such a case?

## Solution
---
Two solutions: For both, if words have **different lengths**, return `false.`
1. 
  - Sort/rearrange each word. compare if the rearrange words are the same.  

2. 
  - Using a hash table, count how many times appears each character in first word.  
  - For second word, is a character is not on the hash table, return `false`.
  - If character exists, then decrease the counter, if `less than 0`, return `false`.

### Solution 1:
---
```c++
class Solution {
public:
  bool isAnagram(string s, string t) {
    if (s.size() != t.size())
      return false;
      
    sort(s.begin(), s.end());
    sort(t.begin(), t.end());

    return s == t;
  }
};
```

### Solution 2:
---
```c++
class Solution {
public:
  bool isAnagram(string s, string t) {
    if (s.size() != t.size())
      return false;

    unordered_map<char, int> hashtable;
    for (int i=0; i<s.size(); i+=1)
      hashtable[s[i]] += 1;

    for (int i=0; i<t.size(); i+=1) {
      hashtable[t[i]] -= 1;
      if (hashtable[t[i]] < 0)
        return false;
    }

    return true;
  }
};
```
