---
title: Reverse Linked List II
platform: LeetCode
number: 92
author: jose
layout: post
language: en
date: 2023-04-11 18:00 +0300
categories: [programming, linkedlist]
tags: [c/c++, leetcode, linkedlist]
difficulty: medium
source: https://leetcode.com/problems/reverse-linked-list-ii/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given the `head` of a singly linked list and two integers `left` and `right` where `left <= right`, reverse the nodes of the list from position `left` to position `right`, and return *the reversed list*.  

## Examples
---
### **Example 1:**
<img src="https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg" width="90%" />

>**Input:** head = [1,2,3,4,5], left = 2, right = 4  
>**Output:** [1,4,3,2,5]  

### **Example 2:**
>**Input:** head = [5], left = 1, right = 1  
>**Output:** [5]  

## Constraints
---
- The number of nodes in the list is `n`.  
- `1 <= n <= 500`  
- `-500 <= Node.val <= 500`  
- `1 <= left <= right <= n`  

**Follow up:** Could you do it in one pass?

## Solution
---
We solve this problem this way:  
- Decrease by one the `left` and `right` indexes (to make them based `0`).  
- If the `left > 0` means that the head of the list will remain the same.  
- Move a `l` pointer to the node before the `left` node.  
- To reverse, we need to keep track of the current node, the previus node (to point to it), and the next node to keep moving and reversing node by node.  
  - Place a `r` node at the next node to the `left` index/node.  
  - Point the `r` node to the previous node, and move the next one.  
  - Repeat until the `r` node is next to the node at the `right` index.  
- Point the node before the `left` node to the node at the `rigth` index.  
- The `l` node shoul point next to the current position of `r`.  
- If the `head` is not the original node, then we pointed to the node at `right`.  

And it is solved in one pass.  

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
  ListNode* reverseBetween(ListNode* head, int left, int right) {
    if (left == right)
      return head;

    ListNode *newHead = nullptr;
    ListNode *l = head;
    ListNode *r = head;

    left--;
    right--;
    if (head && left > 0)
      newHead = head;
    
    right -= left;
    while (l && l->next && --left > 0)
      l = l->next;

    ListNode* tmp = nullptr;
    ListNode *prev = left == - 1 ? l: l->next;
    r = prev ? prev->next: nullptr;

    while (r && --right >= 0) {
      tmp = r->next;
      r->next = prev;
      prev = r;
      r = tmp;
    }

    if (!newHead)
      newHead = prev;

    if (left != -1 && l->next) {
      tmp = l->next;
      tmp->next = r;
      l->next = prev;
    } else
      l->next = r;

    return newHead;
  }
};
```
