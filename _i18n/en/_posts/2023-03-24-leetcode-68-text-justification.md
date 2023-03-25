---
title: Text Justification
platform: LeetCode
number: 68
author: jose
layout: post
language: en
date: 2023-03-24 01:00 +0300
categories: [programming, greedy]
tags: [c/c++, leetcode, greedy]
difficulty: hard
source: https://leetcode.com/problems/text-justification/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given an array of strings `words` and a width `maxWidth`, format the text such that each line has exactly `maxWidth` characters and is fully (left and right) justified.  

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces `' '` when necessary so that each line has exactly `maxWidth` characters.  

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line does not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.  

For the last line of text, it should be left-justified, and no extra space is inserted between words.  

**Note:**  

* A word is defined as a character sequence consisting of non-space characters only.  
* Each word's length is guaranteed to be greater than `0` and not exceed `maxWidth`.  
* The input array `words` contains at least one word.  

## Examples
---
### **Example 1:**
>**Input:** words = ["This", "is", "an", "example", "of", "text", "justification."], maxWidth = 16  
>**Output:**  
>[  
>   "This    is    an",  
>   "example  of text",  
>   "justification.  "  
>]  

### **Example 2:**
>**Input:** words = ["What","must","be","acknowledgment","shall","be"], maxWidth = 16  
>**Output:**  
>[  
>  "What   must   be",  
>  "acknowledgment  ",  
>  "shall be        "  
>]  
>**Explanation:** Note that the last line is "shall be    " instead of "shall     be", because the last line must be left-justified instead of fully-justified.
Note that the second line is also left-justified because it contains only one word.  

### **Example 3:**
>**Input:** words = ["Science","is","what","we","understand","well","enough","to","explain","to","a","computer.","Art","is","everything","else","we","do"], maxWidth = 20  
>**Output:**  
>[  
>  "Science  is  what we",  
>  "understand      well",  
>  "enough to explain to",  
>  "a  computer.  Art is",  
>  "everything  else  we",  
>  "do                  "  
>]  

## Constraints
---
- `1 <= words.length <= 300`  
- `1 <= words[i].length <= 20`  
- `words[i]` consists of only English letters and symbols.  
- `1 <= maxWidth <= 100`  
- `words[i].length <= maxWidth`  

## Solution
---
The approach is easy using [**greedy algorithm**](/categories/greedy/).  
- Knowing the `maxWidth` for a line, we start adding words until we run out of space.  
  - For each added word, we add an exrea space.  
- Once we finish with the line, when there is no more space for other word:  
  - We calculate the number of spaces abailable for a line (`maxWidth - length_of_joint_words`).  
  - The spaces will be divided by the `number of words in the line - 1` (for three words, there are two spaces... and so on).  
  - If the previous step gives a fraction of space, we will add an extra espace.
  - After adding a word and the spaces, we reduce the amount of spaces abailable for the line.  
  - We calculate again the espaces for the next word.  
- If we are in the last line (when already iterate through all words), then there is just one space between words, and at the end we add as many spaces as needed to complete the line `maxWidth`.  

```c++
class Solution {
public:
  vector<string> fullJustify(vector<string>& words, int maxWidth) {
    vector<string> sol;
    int w=0;
    int c=0;
    while (w<words.size()) {
      int s = 0;
      while (w < words.size() && (s + 1 + words[w].size()) <= maxWidth + 1) {
        s += (words[w].size() + 1);
        w++;
      }
      string line = ""s;
      int maxSpace = maxWidth - (s - (w-c));
      while (c < w) {
        line += words[c];
        int nSpaces = 1;
        bool extra = false;
        if (w - c == 1)
          nSpaces = maxWidth - line.size();
        else if (w < words.size()) {
          nSpaces = maxSpace / (w-c-1);
          extra  = (maxSpace % (w-c-1)) != 0;
        }
        for (int i=0; i<nSpaces; i++)
          line += " "s;
        if (extra) {
          line += " "s;
          nSpaces++;
        }

        c++;
        maxSpace -= nSpaces;
      }
      sol.push_back(line);
    }
    return sol;
  }
};
```
