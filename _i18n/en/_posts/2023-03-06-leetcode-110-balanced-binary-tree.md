---
title: Balanced Binary Tree
platform: LeetCode
number: 110
author: jose
layout: post
language: en
date: 2023-03-06 17:20 +0300
categories: [programming, tree]
tags: [c/c++, contests, leetcode, tree, dfsbfs]
difficulty: easy
source: https://leetcode.com/problems/balanced-binary-tree
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
Given a binary tree, determine if it is **height-balanced**.  

A **height-balanced** binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.  

## Examples
---
### **Example 1:**  
<img src="https://assets.leetcode.com/uploads/2020/10/06/balance_1.jpg" width="60%" />  

>**Input:** root = [3,9,20,null,null,15,7]  
>**Output:** true  
  
<br/>  

### **Example 2:**  
<img src="https://assets.leetcode.com/uploads/2020/10/06/balance_2.jpg" width="60%" />  

>**Input:** root = [1,2,2,3,3,null,null,4,4]  
>**Output:** false  

### **Example 3:**  
>**Input:** root = []  
>**Output:** true  
  
## Constraints
---
- The number of nodes in the tree is in the range `[0, 5000]`.
- <code>-10<sup>4</sup> <= Node.val <= 10<sup>4</sup></code>

## Solution
---
We will use recursion to perform a DFS (Depth First Search) in order to determine the heigh of each subtree.
  - We call the recursive method with the root node.
    - If the current node doesn't exist, `return 0`.
    - Explore the left and right nodes.
    - If the absolute difference of nodes' depth is higher than 1, we return -1.
    - If the the depth of the left or right node is -1, we return -1 for the current node.
    - Otherwise, we return the max hight of the nodes (left vs right) plus 1.  
  - If the final `result == -1` then the tree is unbalanced.  
    
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
private:
  int exploreNode(TreeNode* node) {
    if (node == nullptr)  return 0;

    int lH = exploreNode(node->left);
    int rH = exploreNode(node->right);
  
    if (lH == -1 || rH == -1 || abs(lH - rH) > 1) 
      return -1;

    return max(lH, rH) + 1;
 }

public:
  bool isBalanced(TreeNode* root) {
    int r =  exploreNode(root); 
    return  r != -1;
  }
};
```
