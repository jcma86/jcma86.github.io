---
title: Reverse Nodes in k-Group
platform: LeetCode
number: 25
author: jose
layout: post
language: en
date: 2023-03-17 18:50 +0300
categories: [programming, linkedlist]
tags: [c/c++, leetcode, linkedlist]
difficulty: hard
source: https://leetcode.com/problems/reverse-nodes-in-k-group/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given the `head` of a linked list, reverse the nodes of the list `k` at a time, and return *the modified list*.  

`k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k` then left-out nodes, in the end, should remain as it is.  

You may not alter the values in the list's nodes, only nodes themselves may be changed.  

## Examples
---
### **Example 1:**
<img src="https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg" width="80%"/>  

>
>**Input:** head = [1,2,3,4,5], k = 2  
>**Output:** [2,1,4,3,5]  
  
### **Example 2:**  
<img src="https://assets.leetcode.com/uploads/2020/10/03/reverse_ex2.jpg" width="80%"/>  

>
>**Input:** head = [1,2,3,4,5], k = 3  
>**Output:** [3,2,1,4,5]  

## Constraints
---
- The number of nodes in the list is `n`.  
- `1 <= k <= n <= 5000`  
- `0 <= Node.val <= 1000`  

## Solution
---
Some points to consider:  

  1. We can only reverse complete sections so, first we move a pointer to know if we have enough nodes in the current section.  
  2. We need to keep track of the last element of the previous reversed section in order to point its `next` value to the first element of the next section.  

  - The first node we are looking at, it's the last element of the current section to be reversed.  
  - Once we move a pointer `k` times, it is located at what will be the first element of the current section to reverse.  
  - Having two pointers, starting from the node that will be the last of the section, we start reversing the `->next` value.  
  - We keep moving and reversing until we arrive to the node that is the new first node of the section.  
  - We point the `->next` value of the last node of the previous section, to this node (the first of the current section).  
  - Once we cannot reverse more section, we just point the `->next` value of the last node of the previous section to the current position.  
  
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
  ListNode* reverseKGroup(ListNode* head, int k) {
    if (k<=1 || !head)
      return head;

    ListNode* p = nullptr;
    ListNode* p1 = head;
    ListNode* p2 = head->next;
    ListNode* tmp = nullptr;
    ListNode* currentFirst = head;
    ListNode* currentEnd = head;
    ListNode* prevEnd = head;
    
    int c = 1;
    while (currentFirst) { 
      while (currentFirst && c<k) {
        currentFirst = currentFirst->next;
        c++;
      }
      if (!currentFirst) 
        break;
      
      while (p1 != currentFirst) {
        tmp = p2->next;
        p2->next = p1;
        p1 = p2;
        p2 = tmp;
      }
      if (p == nullptr)
        p = currentFirst;
      
      prevEnd->next = currentFirst;
      prevEnd = currentEnd;
      currentEnd = p2;
      currentFirst = p2;

      p1 = currentFirst;
      p2 = p1 ? p1->next : nullptr; 

      c = 1;
    }

    prevEnd->next = p1;
    
    return p;
  }
};
```
