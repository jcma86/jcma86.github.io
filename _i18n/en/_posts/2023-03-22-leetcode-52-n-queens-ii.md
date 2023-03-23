---
title: N-Queens II
platform: LeetCode
number: 52
author: jose
layout: post
language: en
date: 2023-03-22 19:10 +0300
categories: [programming, bt, recursion]
tags: [c/c++, leetcode, bt, recursion]
difficulty: hard
source: https://leetcode.com/problems/n-queens-ii/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.  

Given an integer `n`, return *the number of distinct solutions to the **n-queens puzzle***.  

## Examples
---
### **Example 1:**
<img src="https://assets.leetcode.com/uploads/2020/11/13/queens.jpg" width="85%" />  

>**Input:** n = 4  
>**Output:** 2  
>**Explanation:** There exist two distinct solutions to the 4-queens puzzle as shown above.  

### **Example 2:**
>**Input:** n = 1  
>**Output:** 1  

## Constraints
---
- `1 <= n <= 9`  

## Solution
---
Same solution as for ***[problem 51](../leetcode-51-n-queens/)***.  

The only difference is that, instead of saving the solution, we just increase a counter.  

### Solution 1:
---
```c++
class Solution {
private:
  int result = 0;

  bool isValid(int n, int r, int c, set<pair<int, int>>& tmpSol) {
    for (const auto& pair: tmpSol) {
      if (pair.first == r || pair.second == c)
        return false;
      
      if (abs(pair.first - r) == abs(pair.second - c))
        return false;
    }

    return true;
  }

  void solve(int n, set<pair<int, int>>& tmpSol, int r) {
    if (r == n) {
      result ++;
      return;
    }

    for (int c=0; c<n; c++) {
      if (!isValid(n, r, c, tmpSol))
        continue;

      tmpSol.insert({r, c});
      solve(n, tmpSol, r+1);
      tmpSol.erase({r, c});
    }
  }

public:
  int totalNQueens(int n) {
    set<pair<int,int>> tmpSol;
    solve(n, tmpSol, 0);

    return result;
  }
};
```

### Solution 2:
---
```c++
class Solution {
private:
  int result = 0;

  bool isValid(int n, vector<string>& tmpSol, int row, int col){
    for (int i=0; i<n; i++){
      if (tmpSol[i][col] == 'Q')
        return false;
    }
    
    for(int i=row-1, j=col-1; i>=0 && j>=0; i--, j--){
      if(tmpSol[i][j] == 'Q')
        return false;
    }

    for (int i=row-1, j=col+1; i>=0 && j<n; i--, j++) {
      if(tmpSol[i][j] == 'Q')
        return false;
    }
    return true;
  }

  void solve(int n, vector<string>& tmpSol, int r){
    if (r == n) {
      result ++;
      return;
    }

    for (int c=0; c<n; c++) {
      if (isValid(n, tmpSol, r, c)) {
        tmpSol[r][c] = 'Q';
        solve(n, tmpSol, r+1);
        tmpSol[r][c] = '.';
      }
    }
  }

public:
  int totalNQueens(int n) {
    vector<string> tmpSol(n , string(n, '.'));
    solve(n, tmpSol, 0);
    return result;
  }
};
```
