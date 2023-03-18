---
title: Longest Substring Without Repeating Characters
platform: LeetCode
number: 3
author: jose
layout: post
language: en
date: 2023-03-15 03:05 +0300
categories: [programming, slidingwindow]
tags: [c/c++, leetcode, slidingwindow]
difficulty: medium
source: https://leetcode.com/problems/longest-substring-without-repeating-characters
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given a string `s`, find the length of the **longest substring** without repeating characters.  

A **substring** is a contiguous non-empty sequence of characters within a string.  

## Examples
---
### **Example 1:**  
>**Input:** s = "abcabcbb"  
>**Output:** 3  
>**Explanation:** The answer is "abc", with the length of 3.  
  
### **Example 2:**  
>**Input:** s = "bbbbb"  
>**Output:** 1  
>**Explanation:** The answer is "b", with the length of 1.  
  
### **Example 3:**  
>**Input:** s = "pwwkew"  
>**Output:** 3  
>**Explanation:** The answer is "wke", with the length of 3.  
>Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
  
## Constraints
---
- <code>0 <= s.length <= 5 * 10<sup>4</sup></code>  
- `s` consists of English letters, digits, symbols and spaces.  

## Solution
---
- We oterate through all the characters:
  - We set the first character as the start of our substring.
  - For every character: If found in a hash table (our "window"), then we remove from the hash table all the characters that appear before the current one, and we set the start of our substring to be the next character after all the deleted ones.
  - If not found, then we add the character to our hash table/window.
  - We calculate the size of the window (`current_position - position_of_first_character`) and we update our value for the longest substring.

```c++
class Solution {
public:
  int lengthOfLongestSubstring(string s) {
    if (s.size() <= 1)
      return s.size();

    int result=0;
    int start = 0;
    unordered_map<char, int> window;

    for (int i=0; i<s.size(); i+= 1) {
      if (window.find(s[i]) != window.end()) {
        int foundAt = window[s[i]];
        for (int rem=start; rem < foundAt; rem += 1) {
          window.erase(s[rem]);
        }
        start = foundAt + 1;
      }
      
      window[s[i]] = i;
      result = max(result, i-(start-1));
    }

    return result;
  }
};
```
