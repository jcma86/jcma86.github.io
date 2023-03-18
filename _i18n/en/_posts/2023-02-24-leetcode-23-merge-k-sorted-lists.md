---
title: Merge k Sorted Lists
platform: LeetCode
number: 23
author: jose
layout: post
language: en
date: 2023-02-24 18:00 +0300
categories: [programming, linkedlist]
tags: [c/c++, contests, leetcode, linked list]
difficulty: hard
source: https://leetcode.com/problems/merge-k-sorted-lists
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
You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.  

*Merge all the linked-lists into one sorted linked-list and return it.*

## Examples
---
### **Example 1:**  
>**Input:** lists = [[1,4,5],[1,3,4],[2,6]]  
>**Output:** [1,1,2,3,4,4,5,6]  
>**Explanation:** The linked-lists are:  
>[
>  1->4->5,
>  1->3->4,
>  2->6
>]
>merging them into one sorted list:
>1->1->2->3->4->4->5->6

### **Example 2:**  
>**Input:** lists = []  
>**Output:** []  

### **Example 3:**  
>**Input:** lists = [[]]  
>**Output:** []  

## Constraints
---
- `k == lists.length`
- <code>0 <= k <= 10<sup>4</sup></code>
- `0 <= lists[i].length <= 500`
- <code>-10<sup>4</sup> <= lists[i][j] <= 10<sup>4</sup></code>
- `lists[i]` is sorted in **ascending order**.
- The sum of `lists[i].length` will not exceed <code>10<sup>4</sup></code>.

## Solution
---
I propose 3 different solutions.  
1. Using an auxiliary `vector<int>`
    - Create a vector with all the elements.
    - Sort the list.
    - Create a linked list of `ListNode` elements from the values of the sorted vector.

2. Using hashmap (`map<int, int> all`)
    - Add every `val` of the input lists (traking how many times the `val` appears).
    - For every element in the map create as many nodes as necesary, adding them to the end of the linked list.

3. Sort nodes while reading them.
    - The first list becomes out initial result.
    - For every next list:
        - For every node in list: we iterate throught the result list and once we find the place for the node we insert it there (reasigning the `next` pointers).

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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
      ListNode* result = nullptr;

      vector<int> all;
      for (int l=0; l<lists.size(); l+=1) {
        ListNode* node = lists[l];
        while(node) {
          all.push_back(node->val);
          node = (*node).next;
        }
      }

      sort(
        all.begin(),
        all.end(),
        [](int a, int b) { 
          return a < b;
        }
      );

      if (all.size()){  
        ListNode *tmp= new ListNode(all[0]);
        result = tmp;
        for (int n=1; n<all.size(); n+=1) {
          (*tmp).next = new ListNode(all[n]);;
          tmp = (*tmp).next;
        }
      }

      return result;
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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
      ListNode* result = nullptr;

      map<int, int> all;
      for (int l=0; l<lists.size(); l+=1) {
        ListNode* node = lists[l];
        while(node) {
          all[node->val] += 1;
          node = (*node).next;
        }
      }

      ListNode* tmp = nullptr;
      for (auto const& [key, val] : all) {
        int c = val;
        if (tmp == nullptr) {
          tmp = new ListNode(key);
          result = tmp;
          c -= 1;
        }
        for (int i=0; i<c; i+=1) {
          (*tmp).next = new ListNode(key);
          tmp = (*tmp).next;
        }
      }

      return result;
    }
};
```

### Solution 3:
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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
      ListNode* result = nullptr;

      for (int l=0; l<lists.size(); l+=1) {
        if (lists[l] == nullptr)
          continue;
        if (result == nullptr) {
          result = lists[l];
          continue;
        }

        ListNode *rNode = result;
        ListNode *lNode = lists[l];

        while(lNode && rNode && lNode->val < rNode->val) {
          ListNode *tmp = rNode;
          result = lNode;
          lNode = lNode->next;
          result->next = tmp;

          rNode=result;
        }

        ListNode *g = result;

        while (lNode != nullptr){
          while (rNode != nullptr && (*rNode).next) {
            if (rNode->next->val < lNode->val)
              rNode = (*rNode).next;
            else
              break;
          }

          ListNode *tmp = (*rNode).next;
          rNode->next = lNode;
          lNode = lNode->next;
          rNode = rNode->next;
          rNode->next = tmp;
        }
      }
      return result;
    }
};
```
