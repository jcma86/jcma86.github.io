---
title: Decode Ways
platform: LeetCode
number: 91
author: jose
layout: post
language: en
date: 2023-04-10 21:00 +0300
categories: [programming, dynamicp]
tags: [c/c++, leetcode, dynamicp]
difficulty: medium
source: https://leetcode.com/problems/decode-ways/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
A message containing letters from `A-Z` can be **encoded** into numbers using the following mapping:  

>'A' -> "1"  
>'B' -> "2"  
>...  
>'Z' -> "26"  

To **decode** an encoded message, all the digits must be grouped then mapped back into letters using the reverse of the mapping above (there may be multiple ways). For example, `"11106"` can be mapped into:  

* `"AAJF"` with the grouping `(1 1 10 6)`  
* `"KJF"` with the grouping `(11 10 6)`  

Note that the grouping `(1 11 06)` is invalid because `"06"` cannot be mapped into `'F'` since `"6"` is different from `"06"`.  

Given a string `s` containing only digits, return *the **number** of ways to **decode** it*.  

The test cases are generated so that the answer fits in a **32-bit** integer.  

## Examples
---
### **Example 1:**
>**Input:** s = "12"  
>**Output:** 2  
>**Explanation:** "12" could be decoded as "AB" (1 2) or "L" (12).  

### **Example 2:**
>**Input:** s = "226"  
>**Output:** 3  
>**Explanation:** "226" could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).  

### **Example 3:**
>**Input:** s = "06"  
>**Output:** 0  
>**Explanation:** "06" cannot be mapped to "F" because of the leading zero ("6" is different from "06").  

## Constraints
---
- `1 <= s.length <= 100`  
- `s` contains only digits and may contain leading zero(s).  

## Solution
---
To solve this, we will use **[dynamic programming](/categories/dynamicp/)**.  

- Each group can consist of 1 or 2 digits (ranges: `[A, Z]` -> `[1, 26]`).  
- If the group starts with `0`, it can't be decoded.  
- If the group in its integer value is greater than `26` it can't be decoded.  

With this constraints, we will call recursivelly our `decode` method by moving `1` or `2` positions in the original string.  
Once we are at the end of the string, it was successfully decoded, so, we return `1`.  

```c++
class Solution {
private:
  int decode(string s, int index, vector<int>& dp) {
    if (index >= s.size())
      return 1;
    if (s[index] == '0')
      return 0;
    if (dp[index] != -1)
      return dp[index];

    dp[index] = 0;
    dp[index] += decode(s, index + 1, dp);
    if ((index < s.size() - 1) && stoi(s.substr(index, 2)) < 27)
      dp[index] += decode(s, index + 2, dp);

    return dp[index];
  }

public:
  int numDecodings(string s) {
    vector<int> dp(s.size(), -1);
    int waysToDecode = decode(s, 0, dp);

    return waysToDecode;
  }
};
```
