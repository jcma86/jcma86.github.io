---
title: Find Minimum in Rotated Sorted Array
platform: LeetCode
number: 153
author: jose
layout: post
language: en
date: 2023-03-01 18:00 +0300
categories: [programming, bs]
tags: [c/c++, contests, leetcode, bs]
difficulty: medium
source: https://leetcode.com/problems/find-minimum-in-rotated-sorted-array
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
Suppose an array of length `n` sorted in ascending order is **rotated** between `1` and `n` times. For example, the array `nums = [0,1,2,4,5,6,7]` might become:

- `[4,5,6,7,0,1,2]` if it was rotated `4` times.
- `[0,1,2,4,5,6,7]` if it was rotated `7` times.  

Notice that **rotating** an array `[a[0], a[1], a[2], ..., a[n-1]]` 1 time results in the array `[a[n-1], a[0], a[1], a[2], ..., a[n-2]]`.  

Given the sorted rotated array `nums` of **unique** elements, return *the minimum element of this array*.  

You must write an algorithm that runs in `O(log n)` time.  

## Examples
---
### **Example 1:**  
>**Input:** nums = [3,4,5,1,2]  
>**Output:** 1  
>**Explanation:** The original array was [1,2,3,4,5] rotated 3 times.

### **Example 2:**  
>**Input:** nums = [4,5,6,7,0,1,2]  
>**Output:** 0
>**Explanation:** The original array was [0,1,2,4,5,6,7] and it was rotated 4 times.

### **Example 3:**  
>**Input:** nums = [11,13,15,17]  
>**Output:** 11
>**Explanation:** The original array was [11,13,15,17] and it was rotated 4 times. 

## Constraints
---
- `n == nums.length`
- `1 <= n <= 5000`
- `-5000 <= nums[i] <= 5000`
- All the integers of `nums` are **unique**.
- `nums` is sorted and rotated between `1` and `n` times.

## Solution
---
The logic is pretty similar to the problem [#33]({{site.url}}/posts/2023/03/01/leetcode-33-search-in-rotated-sorted-array/):
  - We identify the sorted part of the array:
    - If the value at the lower index `<` current min value:
      - Update minimum value.
      - Next search will be in this part of the array.
    - If not, then the minimum value is on the unsorted part.

```c++
class Solution {
public:
  int findMin(vector<int>& nums) {
    int min = nums[0];
    int l = 0;
    int h = nums.size() - 1;
    int m;

    while (l <= h) {
      m = (l + h) / 2;
      if (nums[m] < min)
        min = nums[m];

      if (nums[l] <= nums[m]) {
        if (nums[l] < min)
          h = m - 1;
        else
          l = m + 1;
      } else {
        if (nums[l] < min)
          l = m + 1;
        else
          h = m - 1;
      }
    }
    return min;
  }
};
```
