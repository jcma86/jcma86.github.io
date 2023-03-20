---
title: Next Permutation
platform: LeetCode
number: 31
author: jose
layout: post
language: en
date: 2023-03-19 14:00 +0300
categories: [programming, others]
tags: [c/c++, leetcode, others]
difficulty: medium
source: https://leetcode.com/problems/next-permutation/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
A **permutation** of an array of integers is an arrangement of its members into a sequence or linear order.  

* For example, for `arr = [1,2,3]`, the following are all the permutations of `arr`: `[1,2,3], [1,3,2], [2, 1, 3], [2, 3, 1], [3,1,2], [3,2,1]`.  

The **next permutation** of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the next permutation of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).  

* For example, the next permutation of arr = [1,2,3] is [1,3,2].  
* Similarly, the next permutation of arr = [2,3,1] is [3,1,2].  
* While the next permutation of arr = [3,2,1] is [1,2,3] because [3,2,1] does not have a lexicographical larger rearrangement.  

Given an array of integers `nums`, *find the next permutation of `nums`*.  

The replacement must be **[in place](http://en.wikipedia.org/wiki/In-place_algorithm)** and use only constant extra memory.  

## Examples
---
### **Example 1:**
>**Input:** nums = [1,2,3]  
>**Output:** [1,3,2]  

### **Example 2:**
>**Input:** nums = [3,2,1]  
>**Output:** [1,2,3]  

### **Example 3:**
>**Input:** nums = [1,1,5]  
>**Output:** [1,5,1]  

## Constraints
---
- `1 <= nums.length <= 100`  
- `0 <= nums[i] <= 100`  

## Solution
---
- First we need to identify the index were the next **lexicographically** greater permutation should occur, for this, we will iterate through the numbers starting at the last number.  
  - Once we find an `index = i` where `number[i] < number[i+1]` we have identify the place for the next permutation.  
- Starting again from the end of the array, we identify the first element that is bigger than the number where the permutation should occur (`number[i] > number[index]`).  
  - We swap those two numbers.
- Finally, we reverse the array of numbers from the next element to `index` to the end of the array `[index+1, end_array]`.
- If we didn't find an `index` it means that we have the last permutation, so, we just reverse the whole array and we are again at the first permutation.

A faster alternative, we can just call the `next_permutation` **[algortithm included in C++ 20](https://en.cppreference.com/w/cpp/algorithm/next_permutation)**
```c++
class Solution {
public:
  void nextPermutation(vector<int>& nums) {
    int n = nums.size() - 1;
    int index = -1;
    int i = 0;

    for (i=n-1; i>=0; i--) {
      if (nums[i] < nums[i+1]) {
        index = i;
        break;
      }
    }
    
    if (index != -1) {
      i = n;
      while (i >= index) {
        if (nums[i] > nums[index]) {
          swap(nums[i], nums[index]);
          break;
        }
        i--;
      }
    }
      
    reverse(nums.begin() + index + 1, nums.end());
  }
};
```
