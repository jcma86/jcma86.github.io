---
title: Top K Frequent Elements
platform: LeetCode
number: 347
author: jose
layout: post
language: en
date: 2023-03-05 02:05 +0300
categories: [programming, heap]
tags: [c/c++, contests, leetcode, heap, hash table]
difficulty: medium
source: https://leetcode.com/problems/top-k-frequent-elements
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
Given an integer array `nums` and an integer `k`, return *the `k` most frequent elements*. You may return the answer in **any order**.  

## Examples
---
### **Example 1:**  
>**Input:** nums = [1,1,1,2,2,3], k = 2  
>**Output:** [1,2]  

### **Example 2:**  
>**Input:** nums = [1], k = 1  
>**Output:** [1]  

## Constraints
---
- <code>1 <= nums.length <= 10<sup>5</sup></code>
- <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
- `k` is in the range `[1, the number of unique elements in the array]`.
- It is **guaranteed** that the answer is **unique**.

**Follow-up:** Your algorithm's time complexity must be better than `O(n log n)`, where n is the array's size.

## Solution
---
To solve this problem we will use a hash table to get the frequency of each number.  
Then we will use a max heap, in this case a priority queue that simplifies the way to handle the max heap.  

We have to sort the words by frequency (highger first).  

To learn more about max heap and priority queue, see these links:
* <a href="https://en.cppreference.com/w/cpp/algorithm/make_heap" target="_blank">max heap</a>  
* <a href="https://en.wikipedia.org/wiki/Binary_heap" target="_blank">binary heap</a>  
* <a href="https://en.cppreference.com/w/cpp/container/priority_queue" target="_blank">priority queue</a>  

---
```c++
class Solution {
public:
  typedef pair<int, int> num_freq;
  struct compare {
    bool operator()(num_freq& a, num_freq& b) {
      return a.second > b.second;
    }
  };

  vector<int> topKFrequent(vector<int>& nums, int k) {
    vector<int> result;
    unordered_map<int, int> m;
    priority_queue<num_freq, vector<num_freq>, compare> pq;

    for (int i=0; i<nums.size(); i+=1)
      m[nums[i]] += 1;

    for (auto const& [key, value]: m) {
      pq.push({key, value});

      if (pq.size() > k)
        pq.pop();
    }

    while (!pq.empty()) {
      result.push_back(pq.top().first);
      pq.pop();
    }

    return result;
  }
};
```
