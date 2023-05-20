---
title: Length of Last Word
platform: LeetCode
number: 58
author: jose
layout: post
language: en
date: 2023-03-28 23:50 +0300
categories: [programming, others]
tags: [c/c++, leetcode, others]
difficulty: easy
source: https://leetcode.com/problems/length-of-last-word/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given a string `s` consisting of words and spaces, return *the length of the **last** word in the string*.  

A `word` is a maximal substring consisting of non-space characters only.  

## Examples
---
### **Example 1:**
>**Input:** s = "Hello World"  
>**Output:** 5  
>**Explanation:** The last word is "World" with length 5.  

### **Example 2:**
>**Input:** s = "&nbsp;&nbsp;&nbsp;fly me&nbsp;&nbsp;&nbsp;to&nbsp;&nbsp;&nbsp;the moon&nbsp;&nbsp;"</pre>  
>**Output:** 4  
>**Explanation:** The last word is "moon" with length 4.  

### **Example 3:**
>**Input:** s = "luffy is still joyboy"  
>**Output:** 6  
>**Explanation:** The last word is "joyboy" with length 6.  

## Constraints
---
- <code>1 <= s.length <= 10<sup>4</sup></code>  
- `s` consists of only English letters and spaces `' '`.  
- There will be at least one word in `s`.  

## Solution
---
This one is easy: 
- We start from the end of the string.  
- Move to prev character while there are spaces.  
- Move to prev character while there are NOT spaces and count.  

```c++
class Solution {
public:
  int lengthOfLastWord(string s) {
    int i = s.size() - 1;
    int c = 0;
    while(i >= 0 && s[i] == ' ')
      i--;
    
    while(i>=0 && s[i] != ' ') {
      c++;
      i--;
    }

    return c;    
  }
};
```
