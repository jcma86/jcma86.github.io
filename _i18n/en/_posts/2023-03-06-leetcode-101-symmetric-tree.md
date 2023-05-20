---
title: Symmetric Tree
platform: LeetCode
number: 101
author: jose
layout: post
language: en
date: 2023-03-06 02:20 +0300
categories: [programming, tree]
tags: [c/c++, contests, leetcode, hashtable, tree, dfsbfs]
difficulty: easy
source: https://leetcode.com/problems/symmetric-tree
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
Given the `root` of a binary tree, *check whether it is a mirror of itself* (i.e., symmetric around its center).  

## Examples
---
### **Example 1:**  
<img src="https://assets.leetcode.com/uploads/2021/02/19/symtree1.jpg" width="60%" />  

>**Input:** root = [1,2,2,3,4,4,3]  
>**Output:** true  
  
<br/>  

### **Example 2:**  
<img src="https://assets.leetcode.com/uploads/2021/02/19/symtree2.jpg" width="60%" />  

>**Input:** root = [1,2,2,null,3,null,3]  
>**Output:** false  
  
## Constraints
---
- The number of nodes in the tree is in the range `[1, 1000].`
- `-100 <= Node.val <= 100`

**Follow up:** Could you solve it both recursively and iteratively?

## Solution
---
  1. We have two parts for every node (left and right), we need to check if left == right. Will use a BFS (Breadth First Search) algorithm.
    - Insert the root nodes to the queue using `pair<TreeNode*, TreeNode*>`.
    - While the queue has nodes:
      - If one node exists, but the other no, return `false`.
      - If both nodes exist but their values are different, return `false`.
    
      - Insert to the queue two pairs `left and right` and `right and left`
      - Pop the first element (pair of nodes) from the queue.
    - Return `true`.
  
  2. A Depth First Search solution.
    
### Solution 1:
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
  bool isSymmetric(TreeNode* root) {
    queue<pair<TreeNode *, TreeNode *>> bfs;

    bfs.push({root->left, root->right});
    TreeNode *a;
    TreeNode *b;
    
    while (!bfs.empty()) {
      a = bfs.front().first;
      b = bfs.front().second;
      if (!a != !b)
        return false;
      if (a && b) {
        if (a->val != b->val)
          return false;

        bfs.push({a->left, b->right});
        bfs.push({a->right, b->left});
      }
      bfs.pop();
    }

    return true;
  }
};
```

### Solution 2:
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
private:
  bool exploreNode(TreeNode* nodeL, TreeNode* nodeR) {
    if (!nodeL != !nodeR)
      return false;
    if (!nodeL && !nodeR)
      return true;

    bool a = exploreNode(nodeL->left, nodeR->right);
    bool b = exploreNode(nodeL->right, nodeR->left);

    if (!a || !b) 
      return false;

    return nodeL->val == nodeR->val;
  }

public:
  bool isSymmetric(TreeNode* root) {
    return exploreNode(root->left, root->right);
  }
};
```
