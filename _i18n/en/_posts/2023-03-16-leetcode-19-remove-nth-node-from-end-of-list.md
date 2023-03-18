---
title: Remove Nth Node From End of List
platform: LeetCode
number: 19
author: jose
layout: post
language: en
date: 2023-03-16 19:50 +0300
categories: [programming, tortoisehare, linkedlist]
tags: [c/c++, leetcode, tortoisehare, linkedlist]
difficulty: medium
source: https://leetcode.com/problems/remove-nth-node-from-end-of-list/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given the `head` of a linked list, remove the <code>n<sup>th</sup></code> node from the end of the list and return its head.  

## Examples
---
### **Example 1:**  
<img src="https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg" width="80%">  

>**Input:** head = [1,2,3,4,5], n = 2  
>**Output:** [1,2,3,4,5]  
  
### **Example 2:**  
>**Input:** head = [1], n = 1  
>**Output:** []  
  
### **Example 3:**  
>**Input:** head = [1,2], n = 1  
>**Output:** [1]  

## Constraints
---
- The number of nodes in the list is `sz`.
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`

**Follow up**: Could you do this in one pass?

## Solution
---
We will use a variation of the ["Tortoise and Hare" (Floyd's) algorithm](https://dev.to/alisabaj/floyd-s-tortoise-and-hare-algorithm-finding-a-cycle-in-a-linked-list-39af) that is used to find cycles in a list of nodes.  

- We initialize two pointer at the head node.  
- We move one of them `n` times.  
- Then we start moving both at the same time, when the firstone arrives to the end node (when `pointer_1->next == nullptr`) then we know that the second pointer is right before the node we want to delete.  
- Then we just re-assign the `pointer_2->next` to `pointer_1_node->next->next`.  

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
      ListNode* p1 = head;
      ListNode* p2 = head;

      int i=0;
      while (p1->next && i<n) {
        p1 = p1->next;
        i++;
      }
      if (i<n)
        return head->next;

      while(p1->next) {
        p1 = p1->next;
        p2 = p2->next;
      }

      p2->next = p2->next->next;

      return head;
    }
};
```
