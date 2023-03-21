---
title: Count And Say
platform: LeetCode
number: 38
author: jose
layout: post
language: en
date: 2023-03-20 15:30 +0300
categories: [programming, recursion]
tags: [c/c++, leetcode, recursion]
difficulty: medium
source: https://leetcode.com/problems/count-and-say/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
The **count-and-say** sequence is a sequence of digit strings defined by the recursive formula:  

* `countAndSay(1) = "1"`  
* `countAndSay(n)` is the way you would "say" the digit string from `countAndSay(n-1)`, which is then converted into a different digit string.  

To determine how you "say" a digit string, split it into the minimal number of substrings such that each substring contains exactly **one** unique digit. Then for each substring, say the number of digits, then say the digit. Finally, concatenate every said digit.  

For example, the saying and conversion for digit string `"3322251"`:  

<img src="https://assets.leetcode.com/uploads/2020/10/23/countandsay.jpg" width="85%"/>  

Given a positive integer `n`, return *the <code>n<sup>th</sup></code> term of the **count-and-say** sequence*.

## Examples
---
### **Example 1:**
>**Input:** n = 1,  
>**Output:** "1"  
>**Explanation:** This is the base case.  

### **Example 2:**
>**Input:** n = 4,  
>**Output:** "1211"  
>**Explanation:**  
>countAndSay(1) = "1"  
>countAndSay(2) = say "1" = one 1 = "11"  
>countAndSay(3) = say "11" = two 1's = "21"  
>countAndSay(4) = say "21" = one 2 + one 1 = "12" + "11" = "1211"  

## Constraints
---
- `1 <= n <= 30`  

## Solution
---
- We iterate through the string, if `size == 0` then the string will be `"1"`.  
- We count how many times a character is repeated.  
- Append to the final string the `counter + the character`.  
- Call recursively the method, passing our last generated string.  

```c++
class Solution {
private:
  string cAndS(int n, string cStr) {
    if (n==0)
      return cStr;
    
    string tmp = cStr.size() == 0 ? "1"s : ""s;
    
    for (int i=0; i<cStr.size(); i++) {
      int j=i+1;
      while(j<cStr.size() && cStr[j] == cStr[i])
        j++;

      tmp += to_string(j-i) + cStr[i];
      i = j-1;
    }
    
    return cAndS(n-1, tmp);
  }

public:
  string countAndSay(int n) {
    return cAndS(n, "");
  }
};
```
