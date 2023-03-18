---
title: Swap Nodes in Pairs
platform: LeetCode
number: 24
author: jose
layout: post
language: en
date: 2023-03-17 10:30 +0300
categories: [programming, linkedlist]
tags: [c/c++, leetcode, linkedlist]
difficulty: medium
source: https://leetcode.com/problems/swap-nodes-in-pairs/
proglang: C/C++
math: true
mermaid: true
pin: true
---

## {% t posts.problem %}

---
Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)  

## Examples

---
<img src="https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg" width="80%"/>  

### **Example 1:**
>
>**Input:** head = [1,2,3,4]  
>**Output:** [2,1,4,3]  
  
### **Example 2:**  
>
>**Input:** head = []  
>**Output:** []  

### **Example 3:**  
>
>**Input:** head = [1]  
>**Output:** [1]  

## Constraints

---

- The number of nodes in the list is in the range `[0, 100]`.  
- `0 <= Node.val <= 100`  

## Solution

---

- We will have two pointers to the elements to swap.  
- An extra pointer to the second element of the previous swaped nodes.  
- Once swap, we point the extra pointer to the first of the newly swaped.  
- We move all the pointers to their new position.  

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
      if (!head || !head->next)
        return head;

      ListNode *newHead = nullptr;
      ListNode *p1 = head;
      ListNode *p2 = head->next;
      ListNode* tmpSwap = nullptr;
      ListNode* tmpPrev = nullptr;
      ListNode* tmpNext = nullptr;

      while (p2) {
        tmpNext = p2->next;

        tmpSwap = p2;
        p2 = p1;
        p1 = tmpSwap;
        p1->next = p2;
        p2->next = tmpNext;
        if (tmpPrev)
          tmpPrev->next = p1;

        if(!newHead)
          newHead = p1;
        
        tmpPrev = p2;

        p1 = p2->next;
        p2 = p1 ? p1->next : nullptr;
      }

      return newHead;
    }
};
```
