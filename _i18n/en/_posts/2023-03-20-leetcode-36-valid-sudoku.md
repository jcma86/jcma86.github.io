---
title: Valid Sudoku
platform: LeetCode
number: 36
author: jose
layout: post
language: en
date: 2023-03-20 10:20 +0300
categories: [programming, others]
tags: [c/c++, leetcode, others]
difficulty: medium
source: https://leetcode.com/problems/valid-sudoku/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:  

Each row must contain the digits `1-9` without repetition.  
Each column must contain the digits `1-9` without repetition.  
Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.  

**Note:**  
* A Sudoku board (partially filled) could be valid but is not necessarily solvable.  
* Only the filled cells need to be validated according to the mentioned rules.  

## Examples
---
### **Example 1:**
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png" width="85%"/>  

>**Input:** board = 
>[["5","3",".",".","7",".",".",".","."]  
>,["6",".",".","1","9","5",".",".","."]  
>,[".","9","8",".",".",".",".","6","."]  
>,["8",".",".",".","6",".",".",".","3"]  
>,["4",".",".","8",".","3",".",".","1"]  
>,["7",".",".",".","2",".",".",".","6"]  
>,[".","6",".",".",".",".","2","8","."]  
>,[".",".",".","4","1","9",".",".","5"]  
>,[".",".",".",".","8",".",".","7","9"]]  
>**Output:** true  

### **Example 2:**
>**Input:** board = 
>[["8","3",".",".","7",".",".",".","."]  
>,["6",".",".","1","9","5",".",".","."]  
>,[".","9","8",".",".",".",".","6","."]  
>,["8",".",".",".","6",".",".",".","3"]  
>,["4",".",".","8",".","3",".",".","1"]  
>,["7",".",".",".","2",".",".",".","6"]  
>,[".","6",".",".",".",".","2","8","."]  
>,[".",".",".","4","1","9",".",".","5"]  
>,[".",".",".",".","8",".",".","7","9"]]  
>**Output:** false  
>**Explanation:** Same as Example 1, except with the **5** in the top left corner being modified to **8**. Since there are two 8's in the top left 3x3 sub-box, it is invalid.  

## Constraints
---
- `board.length == 9`  
- `board[i].length == 9`  
- `board[i][j]` is a digit `1-9` or `'.'`.

## Solution
---
- For every "cell" with a number, we explore the whole row and column to see if the number is located in any other place. If so, return `false`.  
- For every "cell" with a number, we explore the the `3x3` neighbourhood to which the number belongs.  

```c++
class Solution {
public:
  bool isValidSudoku(vector<vector<char>>& board) {
    for (int row=0; row<9; row++) {
      for (int col=0; col<9; col++) {
        if (board[row][col] == '.')
          continue;

        for (int i=0; i<9; i++) {
          if (i != row && board[i][col] == board[row][col])
            return false;
          
          if (i != col && board[row][i] == board[row][col])
            return false;
        }
        for (int y=0; y<3; y++) {
          for (int x=0; x<3; x++) {
            if ((3*(col/3)+x)==col && (3*(row/3)+y)==row)
              continue;
            if (board[3*(row/3)+y][3*(col/3)+x] == board[row][col])
              return false;
          }
        }
      }
    }
    return true;
  }
};
```
