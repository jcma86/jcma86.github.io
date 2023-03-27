---
title: Edit Distance
platform: LeetCode
number: 72
author: jose
layout: post
language: en
date: 2023-03-25 20:00 +0300
categories: [programming, dynamicp, recursion]
tags: [c/c++, leetcode, dynamicp, recursion]
difficulty: hard
source: https://leetcode.com/problems/edit-distance/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given two strings `word1` and `word2`, return *the minimum number of operations required to convert `word1` to `word2`*.

You have the following three operations permitted on a word:

* Insert a character  
* Delete a character  
* Replace a character  

## Examples
---
### **Example 1:**
>**Input:** word1 = "horse", word2 = "ros"  
>**Output:** 3  
>**Explanation:**  
>horse -> rorse (replace 'h' with 'r')  
>rorse -> rose (remove 'r')  
>rose -> ros (remove 'e')  

### **Example 2:**
>**Input:** word1 = "intention", word2 = "execution"  
>**Output:** 5  
>**Explanation:**  
>intention -> inention (remove 't')  
>inention -> enention (replace 'i' with 'e')  
>enention -> exention (replace 'n' with 'x')  
>exention -> exection (replace 'n' with 'c')  
>exection -> execution (insert 'u')  

## Constraints
---
- `0 <= word1.length, word2.length <= 500`  
- `word1` and `word2` consist of lowercase English letters.  

## Solution
---
For this problem, we will use [*Dynamic Programming*](/categories/dynamicp/).  
  - We need a map/vector to store the computed values.  
  - We actually don't need to modify the words to find a solution.  
  - Using two pointers (one for each word), we will move them according to this:  
    - Move first pointer: it means we deleted the character. 
    - Move the second pointer: it means that we inserted that character in the first word, so we move to the next one.  
    - Move both characters: it means we replace the character (or it was the same a no need to do anything).  
  - When a pointer arrives to the end, we return the size of the other word minus the pointer of the current word.  
  - If we computed the solution before (found in the map/vector) then we return that value and no need to explore more.  

```c++
class Solution {
private:
  vector<vector<int>> dp;
  int solve(int i, int j, string &w1, string &w2){
    if (i >= w1.size())
      return w2.size() - j;
    if (j >= w2.size())
      return w1.size() - i;

    if (dp[i][j] != -1)
      return dp[i][j];

    if (w1[i] == w2[j])
      dp[i][j] = solve(i+1, j+1, w1, w2);
    else {
      int min1 = solve(i+1, j, w1, w2);
      int min2 = solve(i, j+1, w1, w2);
      int min3 = solve(i+1, j+1, w1, w2);
      dp[i][j] = 1 + min(min(min1, min2), min3);
    }

    return dp[i][j];
  }

public:
  int minDistance(string word1, string word2) {
    dp = vector(word1.size(),vector<int>(word2.size(),-1));

    return solve(0, 0, word1, word2);
  }
};
```
