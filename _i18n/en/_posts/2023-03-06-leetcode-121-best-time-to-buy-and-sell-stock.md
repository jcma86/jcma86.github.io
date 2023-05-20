---
title: Best Time to Buy and Sell Stock
platform: LeetCode
number: 121
author: jose
layout: post
language: en
date: 2023-03-06 20:30 +0300
categories: [programming, greedy, dynamicp]
tags: [c/c++, contests, leetcode, greedy, dynamicp]
difficulty: easy
source: https://leetcode.com/problems/best-time-to-buy-and-sell-stock
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
You are given an array `prices` where `prices[i]` is the price of a given stock on the <code>i<sup>th</sup></code> day.  

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.  

Return *the maximum profit you can achieve from this transaction*. If you cannot achieve any profit, return `0`.  

## Examples
---
### **Example 1:**  
>**Input:** prices = [7,1,5,3,6,4]  
>**Output:** 5  
>**Explanation:** Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.  
>Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.  
  
### **Example 2:**  
>**Input:** prices = [7,6,4,3,1]  
>**Output:** 0  
>**Explanation:** In this case, no transactions are done and the max profit = 0.  
  
## Constraints
---
- <code>1 <= prices.length <= 10<sup>5</sup></code>
- <code>0 <= prices[i] <= 10<sup>4</sup></code>

## Solution
---
This is a *greedy problem*. To solve it:
  - Iterate throught every value.
    - If current value is lower than a previous lower, then we have a new buy price (lower).
    - If the profit of selling at current value (`current - lower`) is greater than the current profit, we have a new maximum.
  - Return the max profit found.
    
```c++
class Solution {
public:
  int maxProfit(vector<int>& prices) {
    int lowestPrice = INT_MAX;
    int maxProfit = 0;
    int cProfit = 0;
    
    for (int i = 0; i < prices.size(); i++) {
      if (prices[i] < lowestPrice)
        lowestPrice = prices[i];
      
      cProfit = prices[i] - lowestPrice;
      if (cProfit > maxProfit)
        maxProfit = cProfit;
    }

    return maxProfit;
  }
};
```
