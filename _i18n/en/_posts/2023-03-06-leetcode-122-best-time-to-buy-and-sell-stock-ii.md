---
title: Best Time to Buy and Sell Stock II
platform: LeetCode
number: 122
author: jose
layout: post
language: en
date: 2023-03-06 23:05 +0300
categories: [programming, greedy, dynamicp]
tags: [c/c++, contests, leetcode, greedy, dynamicp]
difficulty: medium
source: https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
You are given an integer array `prices` where `prices[i]` is the price of a given stock on the <code>i<sup>th</sup></code> day.  

On each day, you may decide to buy and/or sell the stock. You can only hold **at most one** share of the stock at any time. However, you can buy it then immediately sell it on the **same day**.  

Find and return *the **maximum** profit you can achieve*.  

## Examples
---
### **Example 1:**  
>**Input:** prices = [7,1,5,3,6,4]  
>**Output:** 7  
>**Explanation:** Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.  
>Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.  
>Total profit is 4 + 3 = 7.    
  
### **Example 2:**  
>**Input:** prices = [1,2,3,4,5]  
>**Output:** 4  
>**Explanation:** Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.  
>Total profit is 4.  
  
### **Example 3:**  
>**Input:** prices = [7,6,4,3,1]  
>**Output:** 0  
>**Explanation:** There is no way to make a positive profit, so we never buy the stock to achieve the maximum profit of 0.   
  
## Constraints
---
- <code>1 <= prices.length <= 3 * 10<sup>4</sup></code>
- <code>0 <= prices[i] <= 10<sup>4</sup></code>

## Solution
---
This is a *greedy problem*.  
First, the problem is just about buy one day, and then close that operation on another day, it doesn't consider opening a 'sell order' and close it later with a buy order, this simplifies the problem. (something that took me long to understand about this problem).  
Second, if we take the second example, with values `[1,2,3,4,5]` we can see that if we buy onde day, and close the next one, and then buy again in that closing day and close the next day... and so on... is the same that buying the first day, and closing the last day.  
So, this problem can be solved by adding up the profits for every day if we buy the previous one (if ther is no profit, then we don't add it).
    
```c++
class Solution {
public:
  int maxProfit(vector<int>& prices) {
    int maxProfit = 0;
    for (int i=1; i<prices.size(); i+=1) {
      if (prices[i] >= prices[i-1])
        maxProfit += (prices[i] - prices[i-1]);
    }

    return maxProfit;
  }
};
```
