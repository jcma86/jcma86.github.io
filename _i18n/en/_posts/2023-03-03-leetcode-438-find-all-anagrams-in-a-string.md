---
title: Find All Anagrams in a String
platform: LeetCode
number: 438
author: jose
layout: post
language: en
date: 2023-03-03 01:30 +0300
categories: [programming, hashtable]
tags: [c/c++, contests, leetcode, hashtable]
difficulty: medium
source: https://leetcode.com/problems/find-all-anagrams-in-a-string
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
Given two strings `s` and `p`, return *an array of all the start indices of `p`'s anagrams in `s`*. You may return the answer in **any order**.  

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.  

## Examples
---
### **Example 1:**  
>**Input:** s = "cbaebabacd", p = "abc"  
>**Output:** [0,6]
>**Explanation:**  
>The substring with start index = 0 is "cba", which is an anagram of "abc".  
>The substring with start index = 6 is "bac", which is an anagram of "abc".  

### **Example 2:**  
>**Input:** s = "abab", p = "ab"  
>**Output:** [0,1,2]  
>**Explanation:**  
>The substring with start index = 0 is "ab", which is an anagram of "ab".  
>The substring with start index = 1 is "ba", which is an anagram of "ab".  
>The substring with start index = 2 is "ab", which is an anagram of "ab".  

## Constraints
---
- <code>1 <= s.length, p.length <= 3 * 10<sup>4</sup></code>
- `s` and `p` consist of lowercase English letters.

## Solution
---
Using two hash tables and a sliding window.
  - Create a hash table of the frequency of characters of `p`.  
  - We start from the first character of `s`.
    - We start growing a `window` from 0 to the size of `p`.
    - For every character that enters the window, we add it to the second hash table.
        - If the character to add doesn't exist in the first table, then we reset the window and second table, and we move the start of the second window to grow to the next index (the one after the character not found in the first table). And we start again the process of adding/growing our window.  
        - If the count of the character to add is `>` than the count of the first table, then we start removing the first character of the window until the counter becomes equal to the one of the first table. (the size of the window decreases)
    - If we can add a character, and the window is the same size than the size `p`, it means we found an anagram, so we add the index of the first character of the window.
    - Once the windows are same size, we remove the first character of the window, and add the next one. (sliding window), the size remains the same.

---
```c++
class Solution {
public:
  vector<int> findAnagrams(string s, string p) {
    if (s.size() < p.size())
      return {};
    
    unordered_map<char, int> hashtable;
    vector<int>result;

    for (int i=0; i<p.size(); i+=1)
      hashtable[p[i]] += 1;

    unordered_map<char, int> hashtable2;
    int i=0; int w=0;
    while(i<=(s.size() - p.size())) {
      if (hashtable.find(s[i+w]) == hashtable.end()) {
        hashtable2.clear();
        i += w+1;
        w = 0;
        continue;
      }

      hashtable2[s[i+w]] += 1;
      if (hashtable2[s[i+w]] > hashtable[s[i+w]]) {
        while (w > 0 && hashtable2[s[i+w]] > hashtable[s[i+w]]) {
          hashtable2[s[i]] -= 1;
          i += 1;
          w -= 1;
        }
        w += 1;
        continue;
      }
      w += 1;
      if (w < p.size()) {
        continue;
      }

      if (w == p.size())
        result.push_back(i);

      hashtable2[s[i]] -= 1;
      i+=1;
      w-=1;
    }

    return result;
  }
};
```
