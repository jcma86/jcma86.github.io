---
title: Same Tree
platform: LeetCode
number: 100
author: jose
layout: post
language: en
date: 2023-03-06 01:40 +0300
categories: [programming, tree]
tags: [c/c++, contests, leetcode, hashtable, tree, dfsbfs]
difficulty: easy
source: https://leetcode.com/problems/same-tree
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.  

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.  

## Examples
---
### **Example 1:**  
<img src="https://assets.leetcode.com/uploads/2020/12/20/ex1.jpg" width="60%" />  

>**Input:** p = [1,2,3], q = [1,2,3]  
>**Output:** true  
  
<br/>  

### **Example 2:**  
<img src="https://assets.leetcode.com/uploads/2020/12/20/ex2.jpg" width="60%" />  

>**Input:** p = [1,2], q = [1,null,2]  
>**Output:** false  
  
<br/>  

### **Example 3:**  
<img src="https://assets.leetcode.com/uploads/2020/12/20/ex3.jpg" width="60%" />  

>**Input:** p = [1,2,1], q = [1,1,2]  
>**Output:** false  

## Constraints
---
- The number of nodes in both trees is in the range `[0, 100]`.
- <code>-10<sup>4</sup> <= Node.val <= 10<sup>4</sup></code>

## Solution
---
We will explore both trees simultaneously with a BFS (Breadth First Search) algorithm.
  - Insert the root nodes to the queue using `pair<TreeNode*, TreeNode*>`.
  - While the queue has nodes:
    - If one node exists, but the other no, return `false`.
    - If both nodes exist:
      - If their values are different, return `false`.
      - Insert to the queue the pointers to the left and right of each node.
    - Pop the first element (pair of nodes) from the queue
  - Return `true`.
    
---
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
  bool isSameTree(TreeNode* p, TreeNode* q) {
    queue<pair<TreeNode *, TreeNode *>> bfs;

    bfs.push({p, q});
    TreeNode *a;
    TreeNode *b;
    
    while (!bfs.empty()) {
      a = bfs.front().first;
      b = bfs.front().second;
      if ((!a && b) || (a && !b))
        return false;
      if (a && b) {
        if (a->val != b->val)
          return false;

        bfs.push({a->left, b->left});
        bfs.push({a->right, b->right});
      }
      
      bfs.pop();
    }

    return true;
  }
};
```
