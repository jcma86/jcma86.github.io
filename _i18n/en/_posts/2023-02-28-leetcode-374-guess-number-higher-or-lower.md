---
title: Guess Number Higher or Lower
platform: LeetCode
number: 374
author: jose
layout: post
language: en
date: 2023-02-28 23:50 +0300
categories: [programming, bs]
tags: [c/c++, contests, leetcode, binary search]
difficulty: easy
source: https://leetcode.com/problems/guess-number-higher-or-lower
proglang: C/C++
math: true
mermaid: true
pin: true
# image:
#   path: https://user-images.githubusercontent.com/36547915/97088991-45da5d00-1652-11eb-900f-80d106540f4f.png
#   lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
#   alt: Responsive rendering of Chirpy theme on multiple devices.
---
## Problem
---
We are playing the Guess Game. The game is as follows:  

I pick a number from `1` to `n`. You have to guess which number I picked.  

Every time you guess wrong, I will tell you whether the number I picked is higher or lower than your guess.  

You call a pre-defined API `int guess(int num)`, which returns three possible results:  

- `-1`: Your guess is higher than the number I picked (i.e. `num > pick`).
- `1`: Your guess is lower than the number I picked (i.e. `num < pick`).
- `0`: your guess is equal to the number I picked (i.e. `num == pick`).

Return `the number that I picked`.

## Examples
---
### **Example 1:**  
>**Input:** n = 10, pick = 6  
>**Output:** 6

### **Example 2:**  
>**Input:** n = 1, pick = 1  
>**Output:** 1  

### **Example 3:**  
>**Input:** n = 2, pick = 1  
>**Output:** 1  

## Constraints
---
- <code>1 <= n <= 2<sup>31</sup> - 1</code>
- `1 <= pick <= n`

## Solution
---
```c++
/** 
 * Forward declaration of guess API.
 * @param  num   your guess
 * @return 	     -1 if num is higher than the picked number
 *			      1 if num is lower than the picked number
 *               otherwise return 0
 * int guess(int num);
 */

class Solution {
public:
  int guessNumber(int n) {
    long long l = 0;
    long long h = n;
    int m, g;

    while (l <= h) {
      m = (int)((l + h) / 2);
      g = guess(m);
      
      if (g == 0)
        break;
      if (g == -1)
        h = m - 1;
      if (g == 1)
        l = m + 1;
    }

    return m;
  }
};
```
