---
title: Sliding Window Maximum
platform: LeetCode
number: 239
author: jose
layout: post
language: en
date: 2023-03-05 22:38 +0300
categories: [programming, ps]
tags: [c/c++, contests, leetcode, ps]
difficulty: hard
source: https://leetcode.com/problems/sliding-window-maximum
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.  

Return *the max sliding window*.  

## Examples
---
### **Example 1:**  
>**Input:** nums = [1,3,-1,-3,5,3,6,7], k = 3  
>**Output:** [3,3,5,5,6,7]  
>**Explanation:**  
>```
>Window position                Max
>---------------               -----
>[1  3  -1] -3  5  3  6  7       3
>  1 [3  -1  -3] 5  3  6  7       3
>  1  3 [-1  -3  5] 3  6  7       5
>  1  3  -1 [-3  5  3] 6  7       5
>  1  3  -1  -3 [5  3  6] 7       6
>  1  3  -1  -3  5 [3  6  7]      7
>```

### **Example 2:**  
>**Input:** nums = [1], k = 1  
>**Output:** [1]  

## Constraints
---
- <code>1 <= nums.length <= 10<sup>5</sup></code>
- <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
- `1 <= k <= nums.length`

## Solution
---
Two solutions:
  1. **Fast**. Using deque. **We will track the index of the max value for each window**.
    -  Iterate through the numbers
      - If the first element (index) is outside the window, then we remove it (`pop_front`)
      - We remove all the indexes that have nums `<` thant the one at the current index.
      - We add the new index to the window/deque (`push_back`).
      - Once the index is corresponds to the last element of the window
        - We can add the num at the index of first element (`front`) of the deque to the results, as it holds the max value for the window.

  2. **Slow**. Using multiset (using the `greater` function object) to sort the elements from greater to lower.
    - Iterate through the numbers.
      - We add the number to the window.
      - Once the multiset has the size of the window we take the first element, as it will be the greater one in the window.
      - We remove the element that corresponds to the first element of the window.
    
### Solution 1:
---
```c++
class Solution {
public:
  vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    deque<int> dq;
    vector<int> result;
    
    for (int i=0;i<nums.size();i++){
      if (!dq.empty() && dq.front()== i-k)
        dq.pop_front();
      
      while (!dq.empty() && nums[dq.back()] < nums[i])
        dq.pop_back();
      
      dq.push_back(i);     
      if (i >= k-1)
        result.push_back(nums[dq.front()]);
    }
    
    return result;
  }
};
```

### Solution 2:
```c++
class Solution {
public:
  vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    vector<int> result;
    multiset<int> w;
    int i = 0;

    for (i=0; i<k-1; i+=1)
      w.insert(nums[i]);

    while (i<nums.size()) {
      w.insert(nums[i]);

      auto n = w.rbegin();
      result.push_back(*n);
      
      w.erase(w.lower_bound(nums[i-k+1]));
      i += 1;
    }

    return result;
  }
};
```
---