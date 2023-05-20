---
title: Best Time to Buy and Sell Stock With Transaction Fee
platform: LeetCode
number: 714
author: jose
layout: post
language: en
date: 2023-03-07 03:05 +0300
categories: [programming, greedy, dynamicp]
tags: [c/c++, contests, leetcode, greedy, dynamicp]
difficulty: medium
source: https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
You are given an integer array `prices` where `prices[i]` is the price of a given stock on the <code>i<sup>th</sup></code> day, and an integer `fee` representing a transaction fee.   

Find the maximum profit you can achieve. You may complete as many transactions as you like, but you need to pay the transaction fee for each transaction.

**Note**: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

## Examples
---
### **Example 1:**  
>**Input:** prices = [1,3,2,8,4,9], fee = 2  
>**Output:** 8  
>**Explanation:** The maximum profit can be achieved by:  
>- Buying at prices[0] = 1  
>- Selling at prices[3] = 8  
>- Buying at prices[4] = 4  
>- Selling at prices[5] = 9  
>The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.  
  
### **Example 2:**  
>**Input:** prices = [1,2,3,4,5]  
>**Output:** 4  
>**Explanation:** Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.  
>Total profit is 4.  
  
### **Example 3:**  
>**Input:** prices = [1,3,7,5,10,3], fee = 3  
>**Output:** 6  
  
## Constraints
---
- <code>1 <= prices.length <= 5 * 10<sup>4</sup></code>  
- <code>1 <= prices[i] < 5 * 10<sup>4</sup></code>  
- <code>0 <= fee < 5 * 10<sup>4</sup></code>  

## Solution
---
This is a *greedy problem*.  
The profit for every transactions is the `curren_price - open_price - fee`, we will keep track of two states, If we have a transaction opened, and if not. If we start with an open transaction, then our profit is negative (the `open_price + fee`). Then, we will just accumulate the profits (if closing transaction, or if opening).  

If we have an opened transaction, then we verify if closing gives us more profit (we update the profit of not openend).  
If we don't have an opened transaction, then we verify if opening gives us more profit (we update the profit of openend).  

At the end, transaction should be closed, so, the not opened accumulator will hold the maximum profit we can make.  
```c++
class Solution {
public:
  int maxProfit(vector<int>& prices, int fee) {
    int opened = -prices[0];
    int notOpened = 0;
    int tmpProfit = 0;

    for (int i=1; i<prices.size(); i+=1) {     
      int tmpProfit = opened + prices[i] - fee;
      if (notOpened < tmpProfit)
        notOpened = tmpProfit;

      tmpProfit = notOpened - prices[i];
      if (opened < tmpProfit)
        opened = tmpProfit;
    }

    return notOpened;
  }
};
```
