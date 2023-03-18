---
title: Reverse Linked List
platform: LeetCode
number: 206
author: jose
layout: post
language: en
date: 2023-02-28 22:45 +0300
categories: [programming, linkedlist]
tags: [c/c++, contests, leetcode, linked list]
difficulty: easy
source: https://leetcode.com/problems/reverse-linked-list
proglang: C/C++
math: true
mermaid: true
pin: true
# image:
#   path: https://user-images.githubusercontent.com/36547915/97088991-45da5d00-1652-11eb-900f-80d106540f4f.png
#   lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
#   alt: Responsive rendering of Chirpy theme on multiple devices.
---
## Problem
---
Given the `head` of a singly linked list, reverse the list, and return *the reversed list*.  

## Examples
---
### **Example 1:**  
<img src="https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg" width="60%" alt="example 1 linked list"/>
>**Input:** [1,2,3,4,5]  
>**Output:** [5,4,3,2,1]  

### **Example 2:**  
<img src="https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg" width="60%" alt="example 2 linked list"/>
>**Input:** head = [1,2]  
>**Output:** [2,1]  

### **Example 3:**  
>**Input:** head = []  
>**Output:** []  

## Constraints
---
- The number of nodes in the list is the range `[0, 5000]`.
- `-5000 <= Node.val <= 5000`

## Solution
---
We just need to point each node to the previous node instead of the next one, and the last node becomes the head.  
Two solutions, one using a `while` loop and the other `recursive`.

### Solution 1:
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
  ListNode* reverseList(ListNode* head) {
    ListNode* p = nullptr;
    ListNode* c = head;

    while (c) {
      ListNode* n = c->next;
      c->next = p;
      p = c;
      c = n;
    }

    return p;
  }
};
```

### Solution 2:
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
  ListNode* reverseList(ListNode* head) {
    if (head == nullptr || head->next == nullptr)
      return head;

    ListNode* tmpHead = reverseList(head->next);
    head->next->next = head;
    head->next = nullptr;

    return tmpHead;
  }
};
```
