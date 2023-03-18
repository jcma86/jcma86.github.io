---
title: Add Two Numbers
platform: LeetCode
number: 2
author: jose
layout: post
language: en
date: 2023-02-28 21:45 +0300
categories: [programming, linkedlist]
tags: [c/c++, contests, leetcode, linked list]
difficulty: medium
source: https://leetcode.com/problems/add-two-numbers
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
You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.  

You may assume the two numbers do not contain any leading zero, except the number 0 itself.  

## Examples
---
### **Example 1:**  
<img src="https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg" width="60%" alt="example 1 linked list"/>
>**Input:** l1 = [2,4,3], l2 = [5,6,4]  
>**Output:** [7,0,8]  
>**Explanation:** 342 + 465 = 807.  

### **Example 2:**  
>**Input:** l1 = [0], l2 = [0]  
>**Output:** [0]  

### **Example 3:**  
>**Input:** l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]  
>**Output:** [8,9,9,9,0,0,0,1]  

## Constraints
---
- The number of nodes in each linked list is in the range `[1, 100]`.
- `0 <= Node.val <= 9`
- It is guaranteed that the list represents a number that does not have leading zeros.

## Solution
---
The solution is simple
- Two pointers moving at the same time.
- Create a node with value 0 and add the value of the previous two pointers (if they exist).
- As long as any of the pointers have a `next` node or the sum of the current nodes is `> 9`, create a new node with the *carrying* value of the current sum.

### Solution:
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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* result = new ListNode(0);
        ListNode* a = l1;
        ListNode* b = l2;
        ListNode* r = result;

        int carry = 0;
        while (a || b) {
          if (a) {
            r->val += a->val;
            a = a->next;
          }
          if (b) {
            r->val += b->val;
            b = b->next;
          }

          carry = r->val / 10;
          r->val = r->val - (carry * 10);
          if (carry > 0 || a || b) {
            r->next = new ListNode(carry);
            r = r->next;
          }
        }

        return result;
    }
};
```
