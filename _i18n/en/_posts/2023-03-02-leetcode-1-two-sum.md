---
title: Two Sum
platform: LeetCode
number: 1
author: jose
layout: post
language: en
date: 2023-03-02 01:30 +0300
categories: [programming, hashtable]
tags: [c/c++, contests, leetcode, hash table]
difficulty: easy
source: https://leetcode.com/problems/two-sum
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
Given an array of integers `nums` and an integer `target`, return *indices of the two numbers such that they add up to `target`.*  

You may assume that each input would have **exactly one solution**, and you may not use the same element twice.  

You can return the answer in any order.  

## Examples
---
### **Example 1:**  
>**Input:** nums = [2,7,11,15], target = 9  
>**Output:** [0,1]
>**Explanation:** Because nums[0] + nums[1] == 9, we return [0, 1].

### **Example 2:**  
>**Input:** nums = [3,2,4], target = 6  
>**Output:** [1,2]

### **Example 3:**  
>**Input:** nums = [3,3], target = 6  
>**Output:** [0,1]

## Constraints
---
- <code>2 <= nums.length <= 10<sup>4</sup></code>
- <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>
- <code>-10<sup>9</sup> <= target <= 10<sup>9</sup></code>
- **Only one valid answer exists.**

**Follow-up:** Can you come up with an algorithm that is less than `O(n2)` time complexity?

## Solution
---
Two solutions using hashmap (in reality the second one is an optimization of the first one).
- Add all values to a hash table as `key` and value a vector of the indexes where the value is located.
- Iterate through the hash table, we need to find a value `x = target - current_key`.
  - if the `x` key exist, then we get the index for that value and for the `current_key`.
  - if not, we move the the next key.

The second solution performs the search of `x`, if not found then the `current_key` it is added to the hash table.

### Solution 1:
---
```c++
class Solution {
public:
  vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, vector<int>> hasht;
    for(int i=0; i<nums.size(); i+=1)
      hasht[nums[i]].push_back(i);

    for(auto const& [key, value]: hasht) {
      int need = target - key;
      auto a = hasht.find(need);
      if(a != hasht.end()) {
        if (key == a->first) {
          if (value.size() == 1)
            continue;
          return {value[0], value[1]};
        }
        else
          return {value[0], a->second[0]};
      }
    }
    return {};
  }
};
```

### Solution 2:
---
```c++
class Solution {
public:
  vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> hasht;
      
    for(int i = 0; i < nums.size(); i++){
      if(hasht.find(target - nums[i]) == hasht.end())
        hasht[nums[i]] = i;
      else
        return {hasht[target - nums[i]], i};
    }
 
    return {};
  }
};
```
