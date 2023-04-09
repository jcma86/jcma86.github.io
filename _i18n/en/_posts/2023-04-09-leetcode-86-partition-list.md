---
title: Partition List
platform: LeetCode
number: 86
author: jose
layout: post
language: en
date: 2023-04-09 10:00 +0300
categories: [programming, linkedlist]
tags: [c/c++, leetcode, linkedlist]
difficulty: medium
source: https://leetcode.com/problems/partition-list/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given the `head` of a linked list and a value `x`, partition it such that all nodes **less than** `x` come before nodes **greater than or equal** to `x`.

You should `preserve` the original relative order of the nodes in each of the two partitions.

## Examples
---
### **Example 1:**
<img src="https://assets.leetcode.com/uploads/2021/01/04/partition.jpg" />  

>**Input:** head = [1,4,3,2,5,2], x = 3  
>**Output:** [1,2,2,4,3,5]  

### **Example 2:**
>**Input:** head = [2,1], x = 2  
>**Output:** [1,2]  

## Constraints
---
- The number of nodes in the list is in the range `[0, 200]`.  
- `-100 <= Node.val <= 100`  
- `-200 <= x <= 200`  

## Solution
---
The solution is simple, we will create two list, one for numbers less than `x` and the other for the rest of the numbers.  
- Traversing the original list, we just add each node to the correspondant list.  
- At the end, we point the first list, to the head of the second list.  
- Consider cases for when:
  - Empty list.  
  - Only numbers less than `x`.  
  - Only numbers greater or equal than `x`.  

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
  ListNode* partition(ListNode* head, int x) {
    if (!head)
      return head;
    ListNode *less = nullptr;
    ListNode *greater = nullptr;
    ListNode *newHead = nullptr;
    ListNode *subHead = nullptr;

    ListNode *b = head;
    while (b) {
      if (b->val < x) {
        if (!less) {
         less = b;
         newHead = b;
        } else {
          less->next = b;
          less = less->next;
        }
      } else {
        if (!greater) {
         greater = b;
         subHead = b;
        } else {
          greater->next = b;
          greater = greater->next;
        }
      }
      b = b->next;
    }

    if (greater)
    greater->next = nullptr;
    if (!less)
      return subHead;

    less->next = subHead;

    return newHead;
  }
};
```
