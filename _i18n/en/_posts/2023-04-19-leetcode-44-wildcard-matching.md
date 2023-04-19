---
title: Wildcard Matching
platform: LeetCode
number: 44
author: jose
layout: post
language: en
date: 2023-04-19 13:00 +0300
categories: [programming, dynamicp]
tags: [c/c++, leetcode, dynamicp]
difficulty: hard
source: https://leetcode.com/problems/wildcard-matching/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given an input string (`s`) and a pattern (`p`), implement wildcard pattern matching with support for `'?'` and `'*'` where:  

* `'?'` Matches any single character.
* `'*'` Matches any sequence of characters (including the empty sequence).  

The matching should cover the **entire** input string (not partial).  

## Examples
---
### **Example 1:**
>**Input:** s = "aa", p = "a"  
>**Output:** false  
>**Explanation:** "a" does not match the entire string "aa".  

### **Example 2:**
>**Input:** s = "aa", p = "*"  
>**Output:** true  
>**Explanation:** '*' matches any sequence.  

### **Example 3:**
>**Input:** s = "cb", p = "?a"  
>**Output:** false  
>**Explanation:** '?' matches 'c', but the second letter is 'a', which does not match 'b'.  

## Constraints
---
- `0 <= s.length, p.length <= 2000`  
- `s` contains only lowercase English letters.  
- `p` contains only lowercase English letters, `'?'` or `'*'`.  

## Solution
---
This problem can be solved with **[Dynamic Programming](/categories/dynamicp/)**:  
- First we clean the pattern string (remove the extra consecutive `'*'`).  
- We use two indexes to track what character of the pattern and string we are matching.  
- If the indexes are at the end of the pattern and string, then we found a match.  
- If only the index of pattern is at the end, there was no match.  
- If the pattern at the current index has `'*'` we have three options:  
  - Move index of pattern.  
  - Move index of string.  
  - Move both indexes.  
- Else if the char at the pattern and string are equal, or the pattern has a `?`, then we can move to next position in both indexes.  
- Else, there is no match.  

### Solution
---
```c++
class Solution {
private:
  string s;
  string p;
  vector<vector<int>> dp;

  void cleanPattern() {
    int l=0;

    for (int i=0; i<p.size(); i++) {
      if (i>0 && p[i] == p[i-1] && p[i] == '*')
        continue;
      
      if (l != i)
        p[l] = p[i];
      l++;
    }
    p.resize(l);
  }

public:
  bool compare(int i, int j) {
    if (dp[i][j] != -1)
      return dp[i][j];

    if (i>=s.size() && j>=p.size())
      return true;
    if (j>=p.size())
      return false;

    bool m = i<s.size() && (s[i] == p[j] || p[j] == '?');
    if (p[j] == '*')
      dp[i][j] = compare(i, j+1) || (i<s.size() && (compare(i+1, j+1) || compare(i+1, j)));
    else if (m)
      dp[i][j] = compare(i+1, j+1);
    else
      dp[i][j] = false;
      
    return dp[i][j];
  }

  bool isMatch(string s, string p) {
    this->s = s;
    this->p = p;

    cleanPattern();
    dp = vector(this->s.size() + 1, vector(this->p.size() + 1, -1));
    return compare(0, 0);
  }
};
```