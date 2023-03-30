---
title: Climbing Stairs
platform: LeetCode
number: 70
author: jose
layout: post
language: en
date: 2023-03-30 10:30 +0300
categories: [programming, dynamicp, others]
tags: [c/c++, leetcode, dynamicp, others]
difficulty: easy
source: https://leetcode.com/problems/climbing-stairs/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?  

## Examples
---
### **Example 1:**
>**Input:** n = 2  
>**Output:** 2  
>**Explanation:** There are two ways to climb to the top.  
>1. 1 step + 1 step  
>2. 2 steps  

### **Example 2:**
>**Input:** n = 3  
>**Output:** 3  
>**Explanation:** There are three ways to climb to the top.  
>1. 1 step + 1 step + 1 step  
>2. 1 step + 2 steps  
>3. 2 steps + 1 step  

## Constraints
---
- `1 <= n <= 45`  

## Solution
---
This can be solved in two ways:  
1. With **[Dynamic Programing](/categories/dynamicp/)**. (This one requires space <coide>O(n)</code>).  
2. The [Fibonacci sequence](https://en.wikipedia.org/wiki/Fibonacci_sequence).  

### Solution 1 (Dynamic Programming)  
---
```c++
class Solution {
public:
  int solve(int n, vector<int> &dp){
    if (n<=2)
      return n;
        
    if (dp[n] != -1) 
      return dp[n]; 
        
    dp[n] = solve(n-1, dp) + solve(n-2, dp);
    
    return dp[n];
  }
  
  int climbStairs(int n) {
    if(n<=2)
      return n;
    
    vector<int> dp(n+1, -1);
        
    return solve(n, dp);
  }
};
```

### Solution 2 (Fibonacci Sequence)  
---
```c++
class Solution {
public:
  int climbStairs(int n) {
    int a = 0;
    int b = 1;

    while (n>0) {
      b = a+b;
      a = b-a;
      n--;
    }
    return b;
  }
};
```
