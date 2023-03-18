---
title: Merge Two Sorted Lists
platform: LeetCode
number: 21
author: jose
layout: post
language: en
date: 2023-03-17 08:00 +0300
categories: [programming, linkedlist]
tags: [c/c++, leetcode, linkedlist]
difficulty: easy
source: https://leetcode.com/problems/merge-two-sorted-lists/
proglang: C/C++
math: true
mermaid: true
pin: true
---

## {% t posts.problem %}

---
You are given the heads of two sorted linked lists `list1` and `list2`.  

Merge the two lists in a one **sorted** list. The list should be made by splicing together the nodes of the first two lists.  

Return *the head of the merged linked list*.  

## Examples

---

### **Example 1:**  

<img src="https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg" width="80%"/><br/>  
  
>**Input:** list1 = [1,2,4], list2 = [1,3,4]  
>**Output:** [1,1,2,3,4,4]  
  
### **Example 2:**  

>**Input:** list1 = [], list2 = []  
>**Output:** []  

### **Example 3:**  

>**Input:** list1 = [], list2 = [0]  
>**Output:** [0]  

## Constraints

---

- The number of nodes in both lists is in the range `[0, 50]`.  
- `-100 <= Node.val <= 100`  
- Both `list1` and `list2` are sorted in **non-decreasing** order.  

## Solution

---

- We will use the list with the initial smaller node value as our head.
- We will have a `tmp` pointer to keep traking of the element that is next to the one we will sort.
- We will move two pointers, one for each list.  

  - We compare the values at the pointer position and we point the `->nexr` value to the node with the bigger value.  
  - The bigger value now will point to the value that was saved in our `tmp` pointer (the one that our smaller value was pointing before in `->next`).
  - We move the pointer of the list with the bigger value.
- Once one of the pointers reached the end, we move to the other list and just keep adding the node to the end of the already sorted list.

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
  ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
    if (!list1 || !list2)
      return list1 ? list1: list2;

    ListNode* mergedHead = nullptr;
    ListNode* p0 = nullptr;
    ListNode* p1 = list1;
    ListNode* p2 = list2;
    ListNode *tmp;

    if (p1->val < p2->val) {
      mergedHead = list1;
      p1 = p1->next;
    } else {
      mergedHead = list2;
      p2 = p2->next;
    }
    p0 = mergedHead;

    while(p1 && p2) {
      if (p1->val < p2->val) {
        tmp = p1;
        p1 = p1->next;
      } else {
        tmp = p2;
        p2 = p2->next;
      }

      p0->next = tmp;
      p0 = p0->next;
    }

    tmp = p1 ? p1 : p2;
    while(tmp) {
      p0->next = tmp;
      tmp = tmp->next;
      p0 = p0->next;
    }
    
    return mergedHead;
  }
};
```
