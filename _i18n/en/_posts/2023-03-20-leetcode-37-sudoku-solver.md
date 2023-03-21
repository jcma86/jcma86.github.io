---
title: Sudoku Solver
platform: LeetCode
number: 37
author: jose
layout: post
language: en
date: 2023-03-20 13:30 +0300
categories: [programming, bt]
tags: [c/c++, leetcode, bt]
difficulty: hard
source: https://leetcode.com/problems/sudoku-solver/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Write a program to solve a Sudoku puzzle by filling the empty cells.  

A sudoku solution must satisfy **all of the following rules**:  

Each of the digits `1-9` must occur exactly once in each row.  
Each of the digits `1-9` must occur exactly once in each column.  
Each of the digits `1-9` must occur exactly once in each of the 9 `3x3` sub-boxes of the grid.  
The `'.'` character indicates empty cells.  

**Note:**  
* A Sudoku board (partially filled) could be valid but is not necessarily solvable.  
* Only the filled cells need to be validated according to the mentioned rules.  

## Examples
---
### **Example 1:**
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png" width="80%"/>  

>**Input:** board = [["5","3",".",".","7",".",".",".","."],  
>["6",".",".","1","9","5",".",".","."],  
>[".","9","8",".",".",".",".","6","."],  
>["8",".",".",".","6",".",".",".","3"],  
>["4",".",".","8",".","3",".",".","1"],  
>["7",".",".",".","2",".",".",".","6"],  
>[".","6",".",".",".",".","2","8","."],  
>[".",".",".","4","1","9",".",".","5"],  
>[".",".",".",".","8",".",".","7","9"]]  
>**Output:** [["5","3","4","6","7","8","9","1","2"],  
>["6","7","2","1","9","5","3","4","8"],  
>["1","9","8","3","4","2","5","6","7"],  
>["8","5","9","7","6","1","4","2","3"],  
>["4","2","6","8","5","3","7","9","1"],  
>["7","1","3","9","2","4","8","5","6"],  
>["9","6","1","5","3","7","2","8","4"],  
>["2","8","7","4","1","9","6","3","5"],  
>["3","4","5","2","8","6","1","7","9"]]  
>**Explanation:** The input board is shown above and the only valid solution is shown below:  
>  
><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png" width="80%"/>  
>  
>  

## Constraints
---
- `board.length == 9`  
- `board[i].length == 9`  
- `board[i][j]` is a digit or `'.'`.  
- It is **guaranteed** that the input board has only one solution.  

## Solution
---
This can be solved using [**backtracking algorithm**](https://www.programiz.com/dsa/backtracking-algorithm) (a "optimized" brute force method).
  - For every empty cell, we insert all the valid numbers (see [problem 36](../leetcode-36-valid-sudoku/)) using recursion until we find the correct solution.
  - If a solution is not valid we return and set back the cell to empty.
A different approach can be first generate all posible numbers for each cell, then start placing numbers to those cell with the minimum option. Problem is not efficient in memory, and also needs a good heuristic to decide what number place when a cell has more than one posible option.  
  - **Recursion will be called moving one cell to the right, if we are at the end, then we move to the start of the next row.**
  - **Once we completed all rows, we have found a correct solution.**


```c++
class Solution {
public:
  bool isValid(vector<vector<char>>& board, int row, int col, char ch) {
    for (int i=0; i<9; i++) {
      if (board[i][col] == ch) 
        return false;
 
      if (board[row][i] == ch)
        return false;
      
      if (board[3*(row/3)+i/3][3*(col/3)+i%3] == ch)
        return false;
    }
    return true;
  }

  bool solve(vector<vector<char>>& board, int r, int c) {
    if (r==9) return true;
    if (c==9) return solve(board, r+1, 0);
    if (board[r][c] != '.') return solve(board, r, c+1);

    for (char i='1'; i<='9'; i++) {
      if (isValid(board, r, c, i)) {
        board[r][c] = i;
        if (solve(board, r, c+1))
          return true;
      }
      board[r][c] = '.';
    }
    return false;
  }

public:
  void solveSudoku(vector<vector<char>>& board) {
    solve(board, 0, 0);
  }   
};
```
