---
title: Search in Rotated Sorted Array
platform: LeetCode
number: 33
author: jose
layout: post
language: en
date: 2023-03-01 14:00 +0300
categories: [programming, bs]
tags: [c/c++, contests, leetcode, bs]
difficulty: medium
source: https://leetcode.com/problems/search-in-rotated-sorted-array
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
There is an integer array `nums` sorted in ascending order (with **distinct** values).

Prior to being passed to your function, `nums` is possibly rotated at an unknown pivot index `k` (`1 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` **after** the possible rotation and an integer `target`, return *the index of `target` if it is in `nums`, or `-1` if it is not in `nums`*.

You must write an algorithm with `O(log n)` runtime complexity.

## Examples
---
### **Example 1:**  
>**Input:** nums = [4,5,6,7,0,1,2], target = 0  
>**Output:** 4

### **Example 2:**  
>**Input:** nums = [4,5,6,7,0,1,2], target = 3  
>**Output:** -1

### **Example 3:**  
>**Input:** nums = [1], target = 0  
>**Output:** -1

## Constraints
---
- `1 <= nums.length <= 5000`
- <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
- All values of `nums` are **unique**.
- `nums` is an ascending array that is possibly rotated.
- <code>-10<sup>4</sup> <= target <= 10<sup>4</sup></code>

## Solution
---
The logic is as follows:
  - Binary search splits the array in two.
  - If the array is rotated, one part will be sorted, and the other not.
  - First we identify the sorted half (the sorted part has the value at the lower index `<=` that the value at the middle index).
    - If the `target` is in the sorted part, then we update our indexes to perform the next binary search in that part.
    - If not, then it means the `target` is in the unsorted part, so we update indexes to perform next search there.


```c++
class Solution {
public:
  int search(vector<int>& nums, int target) {
    int l = 0;
    int h = nums.size() - 1;
    int m;
        
    while (l <= h) {
      m = (l + h) / 2;
      if (nums[m] == target)
        return m;

      if (nums[l] <= nums[m]) {
        if (target <= nums[m] && target >= nums[l])
          h = m - 1;
        else
          l = m + 1;
      } else {
        if (target >= nums[m] && target <= nums[h])
          l = m + 1;
        else
          h = m - 1;
      }
    }
    return -1;
  }
};
```
