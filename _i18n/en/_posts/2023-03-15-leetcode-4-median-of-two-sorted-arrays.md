---
title: Median of Two Sorted Arrays
platform: LeetCode
number: 4
author: jose
layout: post
language: en
date: 2023-03-15 05:05 +0300
categories: [programming, bs]
tags: [c/c++, leetcode, bs]
difficulty: hard
source: https://leetcode.com/problems/median-of-two-sorted-arrays/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two sorted arrays.  

The overall run time complexity should be `O(log (m+n))`.  

## Examples
---
### **Example 1:**  
>**Input:** nums1 = [1,3], nums2 = [2]  
>**Output:** 2.00000  
>**Explanation:** merged array = [1,2,3] and median is 2.  
  
### **Example 2:**  
>**Input:** nums1 = [1,2], nums2 = [3,4]  
>**Output:** 2.50000  
>**Explanation:** merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.  
  
## Constraints
---
- `nums1.length == m`
- `nums2.length == n`
- `0 <= m <= 1000`
- `0 <= n <= 1000`
- `1 <= m + n <= 2000`
- <code>-10<sup>6</sup> <= nums1[i], nums2[i] <= 10<sup>6</sup></code>  

## Solution
---
This one was difficult, and I could figure out how to solve it without mergin the two arrays until I had the number of elements equal to the hald of the total number of elements (median: all elements sorted, take the value at the middle of the list of elements).

So, watch the next video, it gaves an excelent explanation of how to solve it, the basic idea is:
  - We know the total number of elements.
  - Whe know how many we need to have the first half of them.
  - Both arrays are sorted, so, for example, if we have two identical arrays, we need the first half of each one.
  - This algorithm performs a binary search to find how many elements of the first array we need, and how many of the second (partition points).
  - Knowing those partition points, we just identify the order, and we get the median.

### Algorithm explanation
{% include embed/youtube.html id='q6IEA26hvXc' %}  

```c++
class Solution {
public:
  double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
    if (nums2.size() < nums1.size())
      return findMedianSortedArrays(nums2, nums1);

    int size = nums1.size() + nums2.size();
    int medianPos = size / 2;
    
    int l = -1;
    int r = nums1.size() - 1;

    while (1) {
      int i = (l + r) >= 0 ? (l + r) / 2: -1;
      int j = medianPos - i - 2;
      
      int l1 = i >= 0 ? nums1[i] : -INT_MAX;
      int r1 = (i + 1) < nums1.size() ? nums1[i + 1] : INT_MAX;
      int l2 = j >= 0 ? nums2[j] : -INT_MAX;
      int r2 = (j + 1) < nums2.size() ? nums2[j + 1] : INT_MAX;

      if (l1 <= r2 && l2 <= r1) {
        if (size % 2 == 0)
          return (double)(((long)max(l1, l2) + (long)min(r1, r2)) / (double)2.0);
        return (double)min(r1, r2);
      } else if (l1 > r2) {
        r = i - 1;
      } else {
        l = i + 1;
      }
    }

    return 0;
  }
};
```
