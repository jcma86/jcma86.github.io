---
title: Binary Tree Inorder Traversal
platform: LeetCode
number: 94
author: jose
layout: post
language: en
date: 2023-04-11 18:00 +0300
categories: [programming, btree]
tags: [c/c++, leetcode, btree]
difficulty: easy
source: https://leetcode.com/problems/binary-tree-inorder-traversal/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given the `root` of a binary tree, return *the inorder traversal of its nodes' values*.  

## Examples
---
### **Example 1:**
<img src="https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg" width="90%" />

>**Input:** root = [1,null,2,3]  
>**Output:** [1,3,2]  

### **Example 2:**
>**Input:** root = []  
>**Output:** []  

### **Example 3:**
>**Input:** root = [1]  
>**Output:** [1]  

## Constraints
---
- The number of nodes in the tree is in the range `[0, 100]`.  
- `-100 <= Node.val <= 100`  

**Follow up:** Recursive solution is trivial, could you do it iteratively?  

## Solution
---
Two solutions:
1. Recursively:  
  - First call recursively for the left node.  
  - Add the value of the node to the result.  
  - Call recursively for the right node.  
2. Iterative:  
  - Using an stack:
  - Push the root node.  
    - While the stack is not empty:  
      - Get the top node.  
        - Push its `left` node if it hasn't been visited.  
        - Mark the node as visited (for this case, we will use a `set` to track the visited nodes).  
        - Continue until no left nodes are available.  
      - Pop the node and add its value to the result.  
      - If the node has a right node, push it to the stack.  

### Solution 1
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
  void  traverse(TreeNode* node, vector<int>& result) {
    if (node == nullptr)
      return;

    traverse(node->left, result);
    result.push_back(node->val);
    traverse(node->right, result);
  }

public:
  vector<int> inorderTraversal(TreeNode* root) {
    vector<int> result;
    traverse(root, result);
    return result;
  }
};
```

### Solution 2
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
  vector<int> inorderTraversal(TreeNode* root) {
    if (!root)
      return {};

    vector<int> result;
    stack<TreeNode*> st;
    set<TreeNode*> visited;

    st.push(root);
    while(!st.empty()) {
      TreeNode *t = st.top();

      if (visited.find(t) == visited.end() && t->left) {
        st.push(t->left);
        visited.insert(t);
        continue;
      }

      st.pop();
      result.push_back(t->val);
      if (t->right)
        st.push(t->right);
    }

    return result;
  }
};
```