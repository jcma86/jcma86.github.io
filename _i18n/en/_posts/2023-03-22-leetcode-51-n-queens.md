---
title: N-Queens
platform: LeetCode
number: 51
author: jose
layout: post
language: en
date: 2023-03-22 19:00 +0300
categories: [programming, bt, recursion]
tags: [c/c++, leetcode, bt, recursion]
difficulty: hard
source: https://leetcode.com/problems/n-queens/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.  

Given an integer `n`, return *all distinct solutions to the **n-queens puzzle***. You may return the answer in **any order**.  

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.  

## Examples
---
### **Example 1:**
<img src="https://assets.leetcode.com/uploads/2020/11/13/queens.jpg" width="85%" />  

>**Input:** n = 4  
>**Output:** [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]  
>**Explanation:** There exist two distinct solutions to the 4-queens puzzle as shown above.  

### **Example 2:**
>**Input:** n = 1  
>**Output:** [["Q"]]  

## Constraints
---
- `1 <= n <= 9`  

## Solution
---
I will use the [**backtracking**](/categories/bt/) technique, I propose two solutions, same algorithm, but different implementation.  

  1. First solution, uses a `set` to keep tracking only of the `Queens` positions. The problem with this solution is that, once a solution is found, then we need to generate the strings to represent the board.  
  2. Second solution uses directly strings to represent the whole board at all times.  

### Solution 1:
---
```c++
class Solution {
private:
  vector<vector<string>> result;

  bool isValid(int n, int r, int c, set<pair<int, int>>& tmpSol) {
    for (const auto& pair: tmpSol) {
      if (pair.first == r || pair.second == c)
        return false;
      
      if (abs(pair.first - r) == abs(pair.second - c))
        return false;
    }

    return true;
  }

  void addSolution(int n, set<pair<int, int>>& tmpSol) {
    vector<string> tmp;
    for (int r=0; r<n; r++) {
      string sol = ""s;
      for (int c=0; c<n; c++) {
        if (tmpSol.find({r,c}) == tmpSol.end())
          sol = sol + ".";
        else
          sol = sol + "Q";
      }
      tmp.push_back(sol);
    }
    result.push_back(tmp);
  }

  void solve(int n, set<pair<int, int>>& tmpSol, int r) {
    if (r == n) {
      addSolution(n, tmpSol);
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
  vector<vector<string>> solveNQueens(int n) {
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
  vector<vector<string>> result;

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
      result.push_back(tmpSol);
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
  vector<vector<string>> solveNQueens(int n) {
    vector<string> tmpSol(n , string(n, '.'));
    solve(n, tmpSol, 0);
    return result;
  }
};
```
