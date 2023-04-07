---
title: Longest Subarray of 1's After Deleting One Element
platform: LeetCode
number: 1493
author: jose
layout: post
language: en
date: 2023-04-04 20:00 +0300
categories: [programming, slidingwindow, others]
tags: [c/c++, leetcode, slidingwindow, others]
difficulty: medium
source: https://leetcode.com/problems/longest-subarray-of-1s-after-deleting-one-element/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given a binary array `nums`, you should delete one element from it.  

Return *the size of the longest non-empty subarray containing only `1`'s in the resulting array*. Return `0` if there is no such subarray.  

## Examples
---
### **Example 1:**
>**Input:** nums = [1,1,0,1]  
>**Output:** 3  
>**Explanation:** After deleting the number in position 2, [1,1,1] contains 3 numbers with value of 1's.  

### **Example 2:**
>**Input:** nums = [0,1,1,1,0,1,1,0,1]  
>**Output:** 5  
>**Explanation:** After deleting the number in position 4, [0,1,1,1,1,1,0,1] longest subarray with value of 1's is [1,1,1,1,1].  

### **Example 3:**
>**Input:** nums = [1,1,1]  
>**Output:** 2  
>**Explanation:** You must delete one element.  

## Constraints
---
- <code>1 <= nums.length <= 10<sup>5</sup></code>  
- `nums[i]` is either `0` or `1`.  

**Follow up:** Could you use search pruning to make your solution faster with a larger board?

## Solution
---
1. Two solutions a simple count of every group of ones.  
2. Using an sliding window.

### Solution 1
---
  - As long as we have `1`s we count them.  
  - Every step, we add the current count with the last count before a `0` was found.  
  - If a `0` is found, our current count becomes the previous count, and we reset the current count.  
    - If two `0`s are found, then the previous count will become `0`  
  - We update the max value at every step (current count + previous count).  
  - After finishing, if the max count is equal to the size of the vector, then we just decrease the count by one.  

```c++
class Solution {
public:
  int longestSubarray(vector<int>& nums) {
    int maxC = 0;
    int prev = 0;
    int c = 0;

    for (int i=0; i < nums.size(); i++) {
      if (nums[i] == 1) {
        c++;
        maxC = max(maxC, prev + c);
      }
      else {
        prev = c;
        c = 0;
      }
    }

    if (maxC == nums.size())
      maxC--;

    return maxC;
  }
};
```

### Solution 2
---
  - As long as we don't find a `0` we keep moving our `right` extreme of the window (growing).  
  - When we find a `0`, we increase a count.
  - Once the count is `2`:
    - We move the `left` extreme of the window until we find a `0` to decrease the count (shrinking window).  
  - At every step, we calculate the max with the size of the window (which contains only `1`s and maximum one `0`).  

```c++
class Solution {
public:
  int longestSubarray(vector<int>& nums) {
    int left = 0; 
    int count = 0;
    int maxC = 0;
    for (int right=0; right < nums.size(); right++) {
      count += nums[right] == 0;
      while (count > 1)
        count -= nums[left++] == 0;

      maxC = max(maxC, right - left);
    }
    return maxC;
  }
};
```
