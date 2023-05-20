---
title: Top K Frequent Words
platform: LeetCode
number: 692
author: jose
layout: post
language: en
date: 2023-03-05 02:30 +0300
categories: [programming, heap]
tags: [c/c++, contests, leetcode, heap, hashtable]
difficulty: medium
source: https://leetcode.com/problems/top-k-frequent-words
proglang: C/C++
math: true
mermaid: true
pin: true
---
## Problem
---
Given an array of strings `words` and an integer `k`, return *the `k` most frequent strings*.  

Return the answer **sorted** by **the frequency** from highest to lowest. Sort the words with the same frequency by their **lexicographical order**.  

## Examples
---
### **Example 1:**  
>**Input:** words = ["i","love","leetcode","i","love","coding"], k = 2  
>**Output:** ["i","love"]  
>**Explanation:** "i" and "love" are the two most frequent words.  
>Note that "i" comes before "love" due to a lower alphabetical order.  

### **Example 2:**  
>**Input:** words = ["the","day","is","sunny","the","the","the","sunny","is","is"], k = 4  
>**Output:** ["the","is","sunny","day"]  
>**Explanation:** "the", "is", "sunny" and "day" are the four most frequent words, with the number of occurrence being 4, 3, 2 and 1 respectively.  

## Constraints
---
- `1 <= words.length <= 500`
- `1 <= words[i].length <= 10`
- `words[i]` consists of lowercase English letters.
- `k` is in the range `[1, The number of unique words[i]]`

**Follow-up:** Could you solve it in O(n log(k)) time and O(n) extra space?

## Solution
---
<b>See first the solution to problem [#347]({{site.url}}/posts/2023/03/05/leetcode-347-top-k-frequent-elements).</b>  
To solve this problem we will use a hash table to get the frequency of each word.  
Then we will use a max heap, in this case a priority queue that simplifies the way to handle the max heap.  

We have to sort the words by frequency (highger first), and then by *lexicographical order* for those with same freq.  

To learn more about max heap and priority queue, see these links:
* <a href="https://en.cppreference.com/w/cpp/algorithm/make_heap" target="_blank">max heap</a>  
* <a href="https://en.wikipedia.org/wiki/Binary_heap" target="_blank">binary heap</a>  
* <a href="https://en.cppreference.com/w/cpp/container/priority_queue">priority queue</a>  

---
```c++
class Solution {
public:
  typedef pair<string, int> word_freq;
  struct compare {
    bool operator()(word_freq& a, word_freq& b) {
      return a.second > b.second || (a.second == b.second && a.first < b.first);
    }
  };

  vector<string> topKFrequent(vector<string>& words, int k) {
    vector<string> result(k);
    unordered_map<string, int> m;
    priority_queue<word_freq, vector<word_freq>, compare> pq;

    for (int i=0; i<words.size(); i+=1)
      m[words[i]] += 1;

    for (auto const& [key, value]: m) {
      pq.push({key, value});

      if (pq.size() > k)
        pq.pop();
    }

    int i = k - 1;
    while (!pq.empty()) {
      result[i] = pq.top().first;
      pq.pop();
      i-=1;
    }

    return result;
  }
};
```
