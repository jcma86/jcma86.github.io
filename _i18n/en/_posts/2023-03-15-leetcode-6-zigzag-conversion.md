---
title: Zigzag Conversion
platform: LeetCode
number: 6
author: jose
layout: post
language: en
date: 2023-03-15 11:00 +0300
categories: [programming, others]
tags: [c/c++, leetcode, others]
difficulty: medium
source: https://leetcode.com/problems/zigzag-conversion/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)  

> P   A   H   N  
> A P L S I I G  
> Y   I   R  

And then read line by line: `"PAHNAPLSIIGYIR"`  

Write the code that will take a string and make this conversion given a number of rows:  

> string convert(string s, int numRows);


## Examples
---
### **Example 1:**  
>**Input:** s = "PAYPALISHIRING", numRows = 3  
>**Output:** "PAHNAPLSIIGYIR"  
  
### **Example 2:**  
>**Input:** s = "PAYPALISHIRING", numRows = 4  
>**Output:** "PINALSIGYAHRPI  
>**Explanation:**  
>P     I    N  
>A   L S  I G  
>Y A   H R  
>P     I  

### **Example 3:**  
>**Input:** s = "A", numRows = 1  
>**Output:** "A"  

## Constraints
---
- `1 <= s.length <= 1000`
- `s` consists of English letters (lower-case and upper-case), `','` and `'.'`.
- `1 <= numRows <= 1000`

## Solution
---
The approach is simple, imagine a rectified `sine wave`, for example, if we want four rows:  
> "P A Y P A L I S H I R I N G"  <- Original string  
>  1 2 3 4 3 2 1 2 3 4 3 2 1 2   <- Row for each character  
> Distance for the next character for each row.  
>  1: 6, 6, 6, 6, 6, 6....  
>  2: 4, 2, 4, 2, 4, 2....  
>  3: 2, 4, 2, 4, 2, 4....  
>  4: 6, 6, 6, 6, 6, 6....  

We can calculate the position of each letter in the original string, for the row we want.  
 - With this, then we just iterate from `0 to "size - 1"` (the size of the string).  
 - For each position, calculate the position of the next character to append to the row we are currently forming.
 - Once the calculated position for the next character is outside the size of the string, we finish with that row and we start forming the next one.

```c++
class Solution {
public:
  string convert(string s, int numRows) {
    if (numRows <= 1)
      return s;
      
    string result = ""s;

    int maxDistance = (numRows * 2) - 2;
    int maxRowDistance = maxDistance;
    int nextLetterDistance = maxDistance;
    int row = 0;
    int offset = 0;

    for (int i=0; i<s.size(); i+=1) {
      result += s[row + offset];
      offset += nextLetterDistance;

      nextLetterDistance = maxDistance - nextLetterDistance;
      if (nextLetterDistance == 0)
        nextLetterDistance = maxRowDistance;

      if (row + offset >= s.size()) {
        row += 1;
        offset = 0;
        maxRowDistance = (2 * (numRows - (row+1)));
        if (maxRowDistance == 0)
          maxRowDistance = maxDistance;
        nextLetterDistance = maxRowDistance;
      }
    }

    return result;
  }
};
```
