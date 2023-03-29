---
title: Rotate List
platform: LeetCode
number: 61
author: jose
layout: post
language: en
date: 2023-03-29 04:00 +0300
categories: [programming, linkedlist]
tags: [c/c++, leetcode, linkedlist]
difficulty: medium
source: https://leetcode.com/problems/rotate-list/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given the `head` of a linked list, rotate the list to the right by `k` places.  

## Examples
---
### **Example 1:**
<img src="https://assets.leetcode.com/uploads/2020/11/13/rotate1.jpg" width="90%" />  

>**Input:** head = [1,2,3,4,5], k = 2  
>**Output:** [4,5,1,2,3]  

<img src="https://assets.leetcode.com/uploads/2020/11/13/roate2.jpg" width="90%" />  

### **Example 2:**
>**Input:** head = [0,1,2], k = 4  
>**Output:** [2,0,1]  

## Constraints
---
- The number of nodes in the list is in the range `[0, 500]`.  
- `-100 <= Node.val <= 100`  
- <code>0 <= k <= 2 * 10<sup>9</sup></code>  

## Solution
---
For this, we use a similar approach to the one for **[problem 19](../../16/leetcode-19-remove-nth-node-from-end-of-list/)**.
- We move a `front` pointer `k` times, and at the same time we count how many nodes we have.  
- If the pointer arrives to the end before movin `k` times:  
  - We can calculate how many times the pointer would be rotating through the list before moving `k` times.  
  - With this value, it wont be necesary to move the `front` pointer `k` times, we only need to move it `n = total_nodes % k`.  
- Once the front node is at its final position, we start a `rear` pointer at the `head`.  
- From now, we move `front` and `rear` pointers together till the `front` pointer reaches the end.  
- Exchange pointers. the `front->next` will point to the `head`.  
- The new `head` becomes `head = rear->next`.   
- Finally `rear->next` becomes the end of the list so, it will point to `nullptr`.  

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
  ListNode* rotateRight(ListNode* head, int k) {
    if (head == nullptr || head->next == nullptr)
      return head;

    ListNode *f = head;
    ListNode *r = head;
    int n=0;

    while (n<k && f->next != nullptr) {
      f = f->next;
      n++;
    }
    
    if (n <= k) {
      f = head;
      n = k % (n+1);
      if (n==0)
        return head;
        
      while (n>0) {
        f = f->next;
        n--;
      }
    }

    while (f->next != nullptr) {
      r = r->next;
      f = f->next;
    }

    f->next = head;
    head = r->next;
    r->next = nullptr;

    return head;        
  }
};
```
