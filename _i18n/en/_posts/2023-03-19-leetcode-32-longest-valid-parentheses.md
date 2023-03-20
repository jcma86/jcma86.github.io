---
title: Longest Valid Parentheses
platform: LeetCode
number: 32
author: jose
layout: post
language: en
date: 2023-03-19 17:00 +0300
categories: [programming, stack, others]
tags: [c/c++, leetcode, stack, others]
difficulty: hard
source: https://leetcode.com/problems/longest-valid-parentheses/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given a string containing just the characters `'('` and `')'`, return *the length of the longest valid (well-formed) parentheses substring*.  

## Examples
---
### **Example 1:**
>**Input:** s = "(()"  
>**Output:** 2  
>**Explanation:** The longest valid parentheses substring is "()".  

### **Example 2:**
>**Input:** s = ")()())"  
>**Output:** 4  
>**Explanation:** The longest valid parentheses substring is "()()".  

### **Example 3:**
>**Input:** s = ""  
>**Output:** 0  

## Constraints
---
- <code>0 <= s.length <= 3 * 10<sup>4</sup></code>  
- `s[i]` is `'('`, or `')'`.  

## Solution
---
Two solutions:

### Solution 1:
---
- This solution is <code>O(n<sup>2</sup>)</code> in time complexity, but is <code>O(1)</code> in memory.
  - For every position where the `'('` appears, we count `+1` for '`('` and `-1` for `')'`.
    - Once the number the count is negative, means we finish with a valid set of parentheses.
    - If we finish the string and `count == 0` all the substring from `start` is valid.
    - If the count ends positive, means, there are extra `'('` so:
      - We start iterating backwards to the point where `count == 0`.
    - Calculate the distance from the first `'('` to the index where the count is `0`.
```c++
class Solution {
public:
  int longestValidParentheses(string s) {
    if (s.size() == 0)
      return 0;
      
    int start=0;
    int end=0;
    int maxL=0;

    while (start<s.size()-1) {
      if (s.size() - start < maxL)
        break;
      if (s[start] == ')') {
        start++;
        continue;
      }
      int c=1;
      end = start;
      while (end<s.size()-1) {
        end++;
        c += s[end] == '(' ? 1 : -1;
        if (c<0) {
          end--;
          break;
        }
      }
      while(c>0 && end > start) {
        c += s[end] == ')' ? 1 : -1;
        end--;
      }
      if (start != end)
        maxL = max(maxL, (end-start) + 1);
      start++;
    }
    return maxL;
  }
};
```

### Solution 2:
---
- This solution is <code>O(n)</code> for time, but also for memory. This is a variation of **[problem 20 (Valid Parentheses)](../../03/leetcode-20-valid-parentheses)**
  - Every time we find a `'('` we push to the stack the index where it is located.
  - Every time we find a `')'` we pop from the stack.
  - We calculate the distance from the current `')'` with the top element from the stack and update the maximum found.

```c++
class Solution {
public:
  int longestValidParentheses(string s) {
    stack<int> st;
    int maxL=0;

    st.push(-1);
    for (int i=0; i<s.size(); i++) {
      if (s[i] == '(')
        st.push(i);
      else
        if (!st.empty())
          st.pop();
        if (st.empty())
          st.push(i);
        else
          maxL = max(maxL, i - st.top());
    }

    return maxL;
  }
};
```