---
title: String to Integer (atoi)
platform: LeetCode
number: 8
author: jose
layout: post
language: en
date: 2023-03-16 08:00 +0300
categories: [programming, others]
tags: [c/c++, leetcode, others]
difficulty: medium
source: https://leetcode.com/problems/string-to-integer-atoi/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
mplement the `myAtoi(string s)` function, which converts a string to a 32-bit signed integer (similar to C/C++'s `atoi` function).  

The algorithm for `myAtoi(string s)` is as follows:  

Read in and ignore any leading whitespace.  

Check if the next character (if not already at the end of the string) is `'-'` or `'+'`. Read this character in if it is either. This determines if the final result is negative or positive respectively. Assume the result is positive if neither is present.  

Read in next the characters until the next non-digit character or the end of the input is reached. The rest of the string is ignored.
Convert these digits into an integer (i.e. `"123" -> 123`, `"0032" -> 32`). If no digits were read, then the integer is `0`. Change the sign as necessary (from step 2).  

If the integer is out of the 32-bit signed integer range [<code>-2<sup>31</sup></code>, <code>2<sup>31</sup> - 1</code>], then clamp the integer so that it remains in the range. Specifically, integers less than <code>-2<sup>31</sup></code> should be clamped to <code>-2<sup>31</sup></code>, and integers greater than <code>2<sup>31</sup> - 1</code> should be clamped to <code>2<sup>31</sup> - 1</code>.  

Return the integer as the final result.  

**Note:**  
* Only the space character `' '` is considered a whitespace character.  
* **Do not ignore** any characters other than the leading whitespace or the rest of the string after the digits.  

## Examples
---
### **Example 1:**  
>**Input:** s = "42"  
>**Output:** 42  
>**Explanation:** The underlined characters are what is read in, the caret is the current reader position.  
>Step 1: "42" (no characters read because there is no leading whitespace)  
>Step 2: "42" (no characters read because there is neither a '-' nor '+')  
>Step 3: "42" ("42" is read in)  
>The parsed integer is 42.  
>Since 42 is in the range [-231, 231 - 1], the final result is 42.  
  
### **Example 2:**  
>**Input:** s = "   -42"  
>**Output:** -42  
>**Explanation:**  
>Step 1: "___-42" (leading whitespace is read and ignored)  
>Step 2: "   <u>-</u>42" ('-' is read, so the result should be negative)  
>Step 3: "   -<u>42</u>" ("42" is read in)  
>The parsed integer is -42.  
>Since -42 is in the range [-2<sup>31</sup>, 2<sup>31</sup> - 1], the final result is -42.  

### **Example 3:**  
>**Input:** s = "4193 with words"  
>**Output:** 4193  
>**Explanation:**  
>Step 1: "4193 with words" (no characters read because there is no leading whitespace)  
>Step 2: "4193 with words" (no characters read because there is neither a '-' nor '+')  
>Step 3: "<u>4193</u> with words" ("4193" is read in; reading stops because the next character is a non-digit)  
>The parsed integer is 4193.  
>Since 4193 is in the range [-231, 231 - 1], the final result is 4193.  

## Constraints
---
- `0 <= s.length <= 200`
- `s` consists of English letters (lower-case and upper-case), digits (`0-9`), `' '`, `'+'`, `'-'`, and `'.'`.

## Solution
---
The problem description and examples detail the algorithm.

```c++
class Solution {
public:
  int myAtoi(string s) {
    int i = 0;
    bool negative = false;
    int r = 0;

    while (i < s.size() && s[i] == ' ')
      i++;
    
    if (i < s.size() && s[i] == '+') {
      i++;
      if (i < s.size() && s[i] == '-')
        return 0;
    }

    if (i < s.size() && s[i] == '-') {
      negative = true;
      i++;
    }

    while (i < s.size() && (s[i] >= 48 && s[i] <= 57)) {
      if ((INT_MAX/10) - abs(r) < (s[i] - 55))
        return negative ? -INT_MAX - 1: INT_MAX;

      r *= 10;
      r += s[i] - 48;
      i++;
    }
    
    if (negative)
      r *= -1;

    return r;
  }
};
```
