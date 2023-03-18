---
title: Regular Expression Matching
platform: LeetCode
number: 10
author: jose
layout: post
language: en
date: 2023-03-16 13:00 +0300
categories: [programming, dynamicp, hashtable]
tags: [c/c++, leetcode, dynamicp, hashtable]
difficulty: hard
source: https://leetcode.com/problems/regular-expression-matching/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given an input string `s` and a pattern `p`, implement regular expression matching with support for `'.'` and `'*'` where:  

* `'.'` Matches any single character.​​​​  
* `'*'` Matches zero or more of the preceding element.  

The matching should cover the entire input string (not partial).  

## Examples
---
### **Example 1:**  
>**Input:** s = "aa", p = "a"  
>**Output:** false  
>**Explanation:**  "a" does not match the entire string "aa".  
  
### **Example 2:**  
>**Input:** s = "aa", p = "a*"  
>**Output:** true  
>**Explanation:**  '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".    

### **Example 3:**  
>**Input:** s = "ab", p = ".*"  
>**Output:** true  
>**Explanation:**  ".*" means "zero or more (*) of any character (.)".  

## Constraints
---
- `1 <= s.length <= 20`  
- `1 <= p.length <= 20`  
- `s` contains only lowercase English letters.  
- `p` contains only lowercase English letters, `'.'`, and `'*'`.  
- It is guaranteed for each appearance of the character `'*'`, there will be a previous valid character to match.  

## Solution
---

We will use Dynamic Programming:  
  - We create a helper method that receives two indexes (one for the pattern, one for the string).  
  - If we find a previous result for this indexes in a hash table, we return that result (so that we don't process it again).  
  - If both indexes are outside the size of the pattern and string, then it means it fully matched (return `true`).
  - If only the index for pattern is outside the size, it means the string had extra elements that don't match (return `false`).  
  - We identify if the characters of pattern and string are equal, or if the pattern is a `'.'` (at their respective indexes).  
  - If the next character in the pattern is an `'*'` then we call recursively the method moving the indexes respectively and we compare the results (`index_pattern + 2` OR `prev_match AND index_string + 1`).  
  - Else if there is match with `'.'` or equal characters, then we call recursively moving both indexes.  
  - Else, no match.
  - We store the result in a hash table and return that result.

```c++
class Solution {
private:
  string *s;
  string *p;
  map<pair<int, int>, bool> c;

public:
  bool compare(int i, int j) {
    if (c.find({i,j}) != c.end())
      return c[{i,j}];

    if (i>=s->size() && j>=p->size())
      return true;
    if (j>=p->size())
      return false;
    
    bool m = i<s->size() && ((*s)[i] == (*p)[j] || (*p)[j] == '.');
    if (j<p->size()-1 && (*p)[j+1] == '*')
      c[{i, j}] = compare(i, j+2) || (m && compare(i+1, j));
    else if (m)
      c[{i, j}] = compare(i+1, j+1);
    else
      c[{i, j}] = false;
      
    return c[{i, j}];
  }

  bool isMatch(string s, string p) {
    this->s = &s;
    this->p = &p;
    
    return compare(0, 0);
  }
};
```
