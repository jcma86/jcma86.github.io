---
title: Insert Interval
platform: LeetCode
number: 57
author: jose
layout: post
language: en
date: 2023-03-28 22:30 +0300
categories: [programming, other]
tags: [c/c++, leetcode, other]
difficulty: medium
source: https://leetcode.com/problems/insert-interval/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
You are given an array of non-overlapping intervals `intervals` where <code>intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code> represent the start and the end of the <code>i<sup>th</sup></code> interval and `intervals` is sorted in ascending order by <code>start<sub>i</sub></code>. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.  

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by <code>start<sub>i</sub></code> and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).  

Return *`intervals` after the insertion*.  

## Examples
---
### **Example 1:**
>**Input:** intervals = [[1,3],[6,9]], newInterval = [2,5]  
>**Output:** [[1,5],[6,9]]  

### **Example 2:**
>**Input:** intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]  
>**Output:** [[1,2],[3,10],[12,16]]  
>**Explanation:** Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].  

## Constraints
---
- <code>0 <= intervals.length <= 10<sup>4</sup></code>  
- `intervals[i].length == 2`  
- <code>0 <= starti <= endi <= 10<sup>5</sup></code>  
- `intervals` is sorted by start<sub>i</sub> in ascending order.  
- `newInterval.length == 2`  
- <code>0 <= start <= end <= 10<sup>5</sup></code>  

## Solution
---
- For this problem, we need to know if the `newInterval` array has been merged.  
- If has not been merged, we select what is the next array to merge:  
  - `min(newInterval[0], intervals[i][0])`  
- If our result array is empty, we just add the current array to it.  
- Else:  
  - We determine if the current array fits inside the last one added to the result.  
    - If so, we do nothing with it and move to the next one.  
    - If not, we determine if the lower index fits inside the last one added.  
      - If yes, then we just set the upper index of the last one added to `max(lastAdded[1], current[1])`.  
    - If not, then we push the current array to the result.  
  - We finish once we added all the arrays and the new interval.  

```c++
class Solution {
public:
  vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
    if (intervals.size() == 0)
      return {newInterval};

    vector<vector<int>> result;
    bool newMerged = false;
    bool isNewNext = false;

    int i=0;
    while (i < intervals.size() || !newMerged) {
      isNewNext = false;
      vector<int> *next = &intervals[i];
      if ((!newMerged && i == intervals.size()) || (!newMerged && newInterval[0] <= intervals[i][0])) {
        isNewNext = true;
        next = &newInterval;
      }

      if (result.size() == 0)
        result.push_back(*next);
      else if ((*next)[0] >= result[result.size()-1][0] &&
          (*next)[0] <= result[result.size()-1][1])
            result[result.size()-1][1] = max((*next)[1], result[result.size()-1][1]);
      else
        result.push_back(*next);

      if (isNewNext)
        newMerged = true;      
      else
        i++;
    }

    return result;
  }
};
```
