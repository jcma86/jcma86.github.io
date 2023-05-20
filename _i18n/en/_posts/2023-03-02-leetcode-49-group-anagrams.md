---
title: Group Anagrams
platform: LeetCode
number: 49
author: jose
layout: post
language: en
date: 2023-03-02 22:15 +0300
categories: [programming, hashtable]
tags: [c/c++, contests, leetcode, hashtable]
difficulty: medium
source: https://leetcode.com/problems/group-anagrams
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.  

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.  

## Examples
---
### **Example 1:**  
>**Input:** strs = ["eat","tea","tan","ate","nat","bat"]  
>**Output:** [["bat"],["nat","tan"],["ate","eat","tea"]]

### **Example 2:**  
>**Input:** strs = [""]  
>**Output:** [[""]]

### **Example 3:**  
>**Input:** strs = ["a"]  
>**Output:** [["a"]]

## Constraints
---
- <code>1 <= strs.length <= 10<sup>4</sup></code>
- <code>0 <= strs[i].length <= 100</code>
- `strs[i]` consists of lowercase English letters.

## Solution
---
This one is simple, using hash table:
  - For every input word:
    - Sort/rearrange the characters of the word.
    - Find that rearranged word in the hash table and add/push the original word to the value in the hash table.
We end with a hash table where every element has as a value the words that contain the same letters:
  - Iterate through the hash table and add each value (`vector<string>`) to the answer vector.

### Solution 1:
---
```c++
class Solution {
public:
  vector<vector<string>> groupAnagrams(vector<string>& strs) {
    unordered_map<string, vector<string>> hashtable;
    vector<vector<string>> result;

    for (int i=0; i<strs.size(); i+=1) {
      string s = strs[i];
      sort(s.begin(), s.end());
      hashtable[s].push_back(strs[i]);
    }

    for (auto const& [key, value]: hashtable)
      result.push_back(value);

    return result;
  }
};
```
