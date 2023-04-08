---
title: Remove Duplicates from Sorted List
platform: LeetCode
number: 83
author: jose
layout: post
language: en
date: 2023-04-08 20:20 +0300
categories: [programming, linkedlist]
tags: [c/c++, leetcode, linkedlist]
difficulty: easy
source: https://leetcode.com/problems/remove-duplicates-from-sorted-list/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given the `head` of a sorted linked list, *delete all duplicates such that each element appears only once. Return the linked list **sorted** as well*.

## Examples
---
### **Example 1:**
<img src="https://assets.leetcode.com/uploads/2021/01/04/list1.jpg" />  

>**Input:** head = [1,1,2]  
>**Output:** [1,2]  

### **Example 2:**
<img src="https://assets.leetcode.com/uploads/2021/01/04/list2.jpg" />  

>**Input:** head = [1,1,2,3,3]  
>**Output:** [1,2,3]  

## Constraints
---
- The number of nodes in the list is in the range `[0, 300]`.  
- `-100 <= Node.val <= 100`  
- The list is guaranteed to be **sorted** in ascending order.  

## Solution
---
We will use two pointers, one to explore each node, and one to keep tracking of the list and the element that points `next`.  
- Initialize two pointers at the head.  
- Move one pointer until the current node has a different value from the next node.  
- Move once more this pointer.  
- Point `next` of the other pointer to the pointer that moved first.  
- Move the pointer.  

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
  ListNode* deleteDuplicates(ListNode* head) {    
    ListNode *f = head;
    ListNode *b = head;

    while (f) {
      if (f->next && f->val == f->next->val) {
        f = f->next;
        continue;
      }

      f = f->next;
      b->next = f;
      b = b->next;
    }

    return head;
  }
};
```
