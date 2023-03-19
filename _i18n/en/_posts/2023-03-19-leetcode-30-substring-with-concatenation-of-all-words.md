---
title: Substring with Concatenation of All Words
platform: LeetCode
number: 30
author: jose
layout: post
language: en
date: 2023-03-19 11:00 +0300
categories: [programming, hashtable]
tags: [c/c++, leetcode, hashtable]
difficulty: hard
source: https://leetcode.com/problems/substring-with-concatenation-of-all-words/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
You are given a string `s` and an array of strings `words`. All the strings of `words` are of the **same length**.  

A **concatenated substring** in `s` is a substring that contains all the strings of any permutation of `words` concatenated.  

For example, if `words = ["ab","cd","ef"]`, then `"abcdef"`, `"abefcd"`, `"cdabef"`, `"cdefab"`, "efabcd", and "efcdab" are all concatenated strings. `"acdbef"` is not a concatenated substring because it is not the concatenation of any permutation of `words`.  

Return *the starting indices of all the concatenated substrings in `s`*. You can return the answer in **any order**.  

## Examples
---
### **Example 1:**
>**Input:** s = "barfoothefoobarman", words = ["foo","bar"]  
>**Output:** [0,9]  
>**Explanation:** Since words.length == 2 and words[i].length == 3, the concatenated substring has to be of length 6.  
>The substring starting at 0 is "barfoo". It is the concatenation of ["bar","foo"] which is a permutation of words.  
>The substring starting at 9 is "foobar". It is the concatenation of ["foo","bar"] which is a permutation of words.  
>The output order does not matter. Returning [9,0] is fine too.  

### **Example 2:**
>**Input:** s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]  
>**Output:** []  
>**Explanation:** Since words.length == 4 and words[i].length == 4, the concatenated substring has to be of length 16.  
>There is no substring of length 16 is s that is equal to the concatenation of any permutation of words.  
>We return an empty array.  

### **Example 3:**
>**Input:** s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]  
>**Output:** [6,9,12]  
>**Explanation:** Since words.length == 3 and words[i].length == 3, the concatenated substring has to be of length 9.  
>The substring starting at 6 is "foobarthe". It is the concatenation of ["foo","bar","the"] which is a permutation of words.  
>The substring starting at 9 is "barthefoo". It is the concatenation of ["bar","the","foo"] which is a permutation of words.  
>The substring starting at 12 is "thefoobar". It is the concatenation of ["the","foo","bar"] which is a permutation of words.  

## Constraints
---
- <code>1 <= s.length <= 10<sup>4</sup></code>  
- `1 <= words.length <= 5000`  
- `1 <= words[i].length <= 30`  
- `s` and `words[i]` consist of lowercase English letters.  

## Solution
---
We can generate a hast table with all the possible permutations of `words`, then compare every substring from `s` to see if found in the hash table. But this solution will be very slow.

Another solution (but still, not the optimal one), is the next one (at the moment I haven't come up with a better idea, probably using a sliding window technique).  
  - In a hash map, we store and count the `words`.
  - Iterating through the string, if a substring of size `words[0]` starting from the current position, is found, then
    - We get a substring of length equal to the length of all the words.
    - We start removing a sub-substring at the begining and looking in the map to see if found,
      - If found, then we decrease the counting.
      - If the counting is `0` we remove it from the map.
    - Once we finish with this substring, if the map is empty, then we found a match.

```c++
class Solution {
public:
  vector<int> findSubstring(string s, vector<string>& words) {
    int subLength = words[0].size() * words.size();
    if (s.size() < subLength)
      return {};

    vector<int> result;
    map <string, int> c1;

    for (int w=0; w<words.size(); w++)
      c1[words[w]]++;

    for (int i=0; i<=(s.size() - subLength); i++) {
      if (c1.find(s.substr(i, words[0].size())) == c1.end())
        continue;

      map <string, int> c2 = c1;
      string tmp = s.substr(i, subLength);
      while (tmp.size()) {
        if (c2.find(tmp.substr(0, words[0].size())) != c2.end()) {
          c2[tmp.substr(0, words[0].size())] --;
          if (c2[tmp.substr(0, words[0].size())] == 0)
           c2.erase(tmp.substr(0, words[0].size()));
        }
        tmp = tmp.substr(words[0].size());
      }
      if (c2.size() == 0)
        result.push_back(i);
    }

    return result;
  }
};
```
