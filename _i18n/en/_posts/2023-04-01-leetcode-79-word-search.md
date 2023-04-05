---
title: Word Search
platform: LeetCode
number: 79
author: jose
layout: post
language: en
date: 2023-04-03 22:00 +0300
categories: [programming, bt, dfsbfs]
tags: [c/c++, leetcode, bt, dfsbfs]
difficulty: medium
source: https://leetcode.com/problems/word-search/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given an `m x n` grid of characters `board` and a string `word`, return *`true` if `word` exists in the grid*.  

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.  

## Examples
---
### **Example 1:**
<img src="https://assets.leetcode.com/uploads/2020/11/04/word2.jpg" />  

>**Input:** board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"  
>**Output:** true  

### **Example 2:**
<img src="https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg" />  

>**Input:** board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"  
>**Output:** true  

### **Example 3:**
<img src="https://assets.leetcode.com/uploads/2020/10/15/word3.jpg" />  

>**Input:** board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"  
>**Output:** false  

## Constraints
---
- `m == board.length`  
- `n = board[i].length`  
- `1 <= m, n <= 6`  
- `1 <= word.length <= 15`  
- `board` and `word` consists of only lowercase and uppercase English letters.  

**Follow up:** Could you use search pruning to make your solution faster with a larger board?

## Solution
---
This one is easily solved using **[DFS](/categories/dfsbfs/)**/**[Backtracking](/categories/bt/)**.  
- For every cell we verify if at an `index` that letter matches to the letter at `word`.  
  - If not, we return `false`.  
  - If matches, we increment `index` and look to the next character (calling recursively our method for the next character to the left, right, top, bottom) to the current one.  
- Once we matched all letters, we return `true`.

```c++
class Solution {
  vector<vector<bool>> visited;
  string word;

  bool solve(vector<vector<char>>& board, int index, int r, int c) {
    if (index == word.size())
      return true;
    if (r >= board.size() || c >= board[r].size() || r < 0 || c < 0)
      return false;
    if (visited[r][c])
      return false;

    if (board[r][c] != word[index])
      return false;
    
    visited[r][c] = true;
    bool exists = solve(board, index + 1, r + 1, c);
    exists |= solve(board, index + 1, r, c + 1);
    exists |= solve(board, index + 1, r - 1, c);
    exists |= solve(board, index + 1, r, c - 1);
    visited[r][c] = false;

    return exists;
  }

public:
  bool exist(vector<vector<char>>& board, string word) {
    visited = vector(board.size(), vector<bool>(board[0].size(), false));
    this->word = word;

    for(int r=0; r<board.size(); r++) {
      for (int c=0; c<board[0].size(); c++) {
        if (solve(board, 0, r, c))
          return true;
      }
    }

    return false;
  }
};
```
