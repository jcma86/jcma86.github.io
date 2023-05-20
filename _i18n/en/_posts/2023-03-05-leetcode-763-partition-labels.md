---
title: Partition Labes
platform: LeetCode
number: 763
author: jose
layout: post
language: en
date: 2023-03-05 18:25 +0300
categories: [programming, twopointers]
tags: [c/c++, contests, leetcode, hashtable, twopointers]
difficulty: medium
source: https://leetcode.com/problems/partition-labels
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Note that the partition is done so that after concatenating all the parts in order, the resultant string should be `s`.

Return *a list of integers representing the size of these parts*.  

## Examples
---
### **Example 1:**  
>**Input:** s = "ababcbacadefegdehijhklij"  
>**Output:** [9,7,8]  
>**Explanation:**  
> The partition is "ababcbaca", "defegde", "hijhklij".  
> This is a partition so that each letter appears in at most one part.  
> A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts.  

### **Example 2:**  
>**Input:** s = "eccbbbbdec"  
>**Output:** 10  

## Constraints
---
- `1 <= s.length <= 500`
- `s` consists of lowercase English letters.

## Solution
---
Using Hash Table to track last index of each character, and two pointers to determine where a new partition starts and where it ends.
  - We track the last location of each character using the hash table.
  - We iterate again through the  string, and we determine if we are in the last position for this character.
    - If so, then we determine its size (position of the char minus last position for previous label)
    - We add that size to the result and we set this as the new last position.  
    
---
```c++
class Solution {
public:
  vector<int> partitionLabels(string s) {
    vector<int> result;
    unordered_map<char, int> positions;

    for (int i = 0; i < s.size(); i += 1)
      positions[s[i]] = i;

    int maxP = 0;
    int lastP = -1;

    for (int i = 0; i < s.size(); i += 1) {
      maxP = max(maxP, positions[s[i]]);
      if (maxP == i) {
        result.push_back(maxP - lastP);
        lastP = maxP;
      }
    }

    return result;
  }
};
```
