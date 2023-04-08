---
title: Remove Duplicates from Sorted List II
platform: LeetCode
number: 82
author: jose
layout: post
language: en
date: 2023-04-08 20:00 +0300
categories: [programming, linkedlist]
tags: [c/c++, leetcode, linkedlist]
difficulty: medium
source: https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given the `head` of a sorted linked list, *delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list sorted as well*.

## Examples
---
### **Example 1:**
<img src="https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg" />  

>**Input:** head = [1,2,3,3,4,4,5]  
>**Output:** [1,2,5]  

### **Example 2:**
<img src="https://assets.leetcode.com/uploads/2021/01/04/linkedlist2.jpg" />  

>**Input:** head = [1,1,1,2,3]  
>**Output:** [2,3]  

## Constraints
---
- The number of nodes in the list is in the range `[0, 300]`.  
- `-100 <= Node.val <= 100`  
- The list is guaranteed to be **sorted** in ascending order.  

## Solution
---
We will use two pointers, one to explore each node, and one to keep tracking of the list and the element that points `next`.  
- If the current node has the same value than the next node.  
  - Move until the current node has a different value.  
  - Repeat to see if there is a new repeated value.  
- If our pointer to track the list is not initialized yet, we set it to the current position of the other pointer, and at the same time, this node will be the head of the final list.  
- Else, the pointer to track list will point its next node to the current explored node (the other pointer).  
- We move both pointers.  
- After traversing the list, if the pointer to track list is still null, then the list is empty, we return null or simply assign the head to the current position (null).  
- Else, our pointer to track list, the `next` should be pointed to the final position of the other pointer.  

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
    if (head == nullptr || head->next == nullptr)
      return head;
    
    ListNode *f = head;
    ListNode *b = nullptr;
    int val;

    while (f) {
      if (f->next && f->val == f->next->val) {
        val = f->val;
        while (f && f->val == val)
          f = f->next;
        continue;
      }

      if (b == nullptr) {
        head = f;
        b = f;
      } else {
        b->next = f;
        b = b->next;
      }

      f = f->next;
    }

    if (b == nullptr)
      head = f;
    else
      b->next = f;

    return head;
  }
};
```
