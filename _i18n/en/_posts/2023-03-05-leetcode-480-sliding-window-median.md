---
title: Sliding Window Median
platform: LeetCode
number: 480
author: jose
layout: post
language: en
date: 2023-03-05 21:05 +0300
categories: [programming, slidingwindow]
tags: [c/c++, contests, leetcode, heap, set, multiset, sliding window]
difficulty: hard
source: https://leetcode.com/problems/sliding-window-median
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
The **median** is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle values.  

* For examples, if <code>arr = [2,<u>3</u>,4]</code>, the median is `3`.  
* For examples, if <code>arr = [1,<u>2</u>,<u>3</u>,4]</code>, the median is `(2 + 3) / 2 = 2.5`.  

You are given an integer array `nums` and an integer `k`. There is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.  

Return t*he median array for each window in the original array*. Answers within <code>10<sup>-5</sup></code> of the actual value will be accepted.  

## Examples
---
### **Example 1:**  
>**Input:** nums = [1,3,-1,-3,5,3,6,7], k = 3  
>**Output:** [1.00000,-1.00000,-1.00000,3.00000,5.00000,6.00000]  
>**Explanation:**  
>```
>Window position                Median  
>---------------                -----  
>[1  3  -1] -3  5  3  6  7        1  
>  1 [3  -1  -3] 5  3  6  7       -1  
>  1  3 [-1  -3  5] 3  6  7       -1  
>  1  3  -1 [-3  5  3] 6  7        3  
>  1  3  -1  -3 [5  3  6] 7        5  
>  1  3  -1  -3  5 [3  6  7]       6 
>```
  
### **Example 2:**  
>**Input:** nums = [1,2,3,4,2,3,1,4,2], k = 3  
>**Output:** [2.00000,3.00000,3.00000,3.00000,2.00000,3.00000,2.00000]  

## Constraints
---
- <code>1 <= k <= nums.length <= 10<sup>5</sup></code>
- <code>-2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1</code>

## Solution
---
We will slide a window through all the data, to know the median we need the values in the window to be in order, then we know that the element in the middle (or the mean of the two central elements) is our median.  

We can handle ourselves the list of elements in the window, sort them, and then when we move the window we have to remove the element with the lower value, and insert a new one in its corresponding sorted position... but, to do it much more simple, we can use multiset, it allows us to have multiple repeated values and it will be sort, when we insert a new element, it will be placed in the correct position.  

Then we just need to look to the central elemente(s) and we know the median.

To learn more about multisets see these link:
* <a href="https://cplusplus.com/reference/set/multiset/" target="_blank">Multiset C++</a>  

---
```c++
class Solution {
public:
  vector<double> medianSlidingWindow(vector<int>& nums, int k) {
    vector<double> result;
    int mid = (k / 2);
    bool even = k % 2 == 0;

    multiset<int> w;
    int i = 0;

    for (i=0; i<k-1; i+=1)
      w.insert(nums[i]);

    while (i<nums.size()) {
      w.insert(nums[i]);
      long long sum = 0;

      auto n = w.begin();
      advance(n, mid);
      sum += (long long)*n;
        
      if (even) {
        n = w.begin();
        advance(n, mid - 1);
        sum += (long long)*n;
      }
          
      result.push_back(even ? (double)sum / (double)2.0: (double)sum);
      w.erase(w.lower_bound(nums[i-k+1]));

      i += 1;
    }

    return result;
  }
};
```
