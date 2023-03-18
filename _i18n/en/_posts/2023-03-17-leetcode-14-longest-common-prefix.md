---
title: Longest Common Prefix
platform: LeetCode
number: 14
author: jose
layout: post
language: en
date: 2023-03-17 01:00 +0300
categories: [programming, others]
tags: [c/c++, leetcode, others]
difficulty: easy
source: https://leetcode.com/problems/longest-common-prefix/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Write a function to find the longest common prefix string amongst an array of strings.  

If there is no common prefix, return an empty string "".  

## Examples
---
### **Example 1:**  
>**Input:** strs = ["flower","flow","flight"]  
>**Output:** "fl"  
  
### **Example 2:**  
>**Input:** strs = ["dog","racecar","car"]  
>**Output:** ""  
>**Explanation:** There is no common prefix among the input strings.  

## Constraints
---
- `1 <= strs.length <= 200`  
- `0 <= strs[i].length <= 200`  
- `strs[i]` consists of only lowercase English letters.  

## Solution
---
- We start our longest prefix with the first word.  
- Starting from the second word:  
  - We set our prefix size to the size of the shortest word (current vs prefix --> `min(prefix.size(), currentword.size())`).  
  - Once prefix and current word have the minimun size, we start comparing every charachter, once they are different, to that point is the size of our max prefix.  
  - If the prefix size becomes `0`, then no need to process the next words.  

```c++
class Solution {
public:
  string longestCommonPrefix(vector<string>& strs) {
    string result = strs[0];

    for (int i=1; i<strs.size(); i++) {
      result = result.substr(0, min(result.size(), strs[i].size()));
      for (int p=0; p<result.size(); p++){
        if (strs[i][p] != result[p]) {
          result = result.substr(0, p);
          break;
        }
      }
      if (result.size() == 0)
        return "";
    }

    return result;
  }
};
```
