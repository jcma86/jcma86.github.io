---
title: Longest Repeating Character Replacement
platform: LeetCode
number: 424
author: jose
layout: post
language: en
date: 2023-03-05 23:33 +0300
categories: [programming, slidingwindow]
tags: [c/c++, contests, leetcode, heap, set, multiset, sliding window]
difficulty: medium
source: https://leetcode.com/problems/longest-repeating-character-replacement
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.  

Return *the length of the longest substring containing the same letter you can get after performing the above operations*.  

## Examples
---
### **Example 1:**  
>**Input:** s = "ABAB", k = 2  
>**Output:** 4  
>**Explanation:**  Replace the two 'A's with two 'B's or vice versa.  
  
### **Example 2:**  
>**Input:** s = "AABABBA", k = 1  
>**Output:** 4  
>**Explanation:**  Replace the one 'A' in the middle with 'B' and form "AABBBBA".  
>The substring "BBBB" has the longest repeating letters, which is 4.  

## Constraints
---
- <code>1 <= s.length <= 10<sup>5</sup></code>
- `s` consists of only uppercase English letters.
- `0 <= k <= s.length`

## Solution
---
We start with a `window size = 1`, and we start growing the window.
  - Using a hash table.
  - We increase the count for the added character.
  - We track max frequency (most repeated character)
  - if the `window size - the max freq` is `>` than the allowed elements to change
    - We decrease the count of the character.
    - We increase the initial index for our final string.
  - We update the new max size of the final string.

---
```c++
class Solution {
public:
  int characterReplacement(string s, int k) {
    int j = 0;
    int maxfq = 0;
    int result = 0;
    unordered_map<char, int> mp;
    
    for (int i=0; i<s.size(); i+=1) {
      mp[s[i]] += 1;
      maxfq = max(maxfq, mp[s[i]]);
      if (i - j + 1 - maxfq > k) {
        mp[s[j]] -= 1;
        j += 1;
      }
      result = max(res, i-j+1);
    }

    return result;
  }
};
```
