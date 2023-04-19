---
title: Permutation Sequence
platform: LeetCode
number: 60
author: jose
layout: post
language: en
date: 2023-04-19 13:00 +0300
categories: [programming, others]
tags: [c/c++, leetcode, others]
difficulty: hard
source: https://leetcode.com/problems/permutation-sequence/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
The set `[1, 2, 3, ..., n]` contains a total of `n!` unique permutations.

By listing and labeling all of the permutations in order, we get the following sequence for `n = 3`:

`"123"`  
`"132"`  
`"213"`  
`"231"`  
`"312"`  
`"321"`  

Given n and k, return the kth permutation sequence.  

## Examples
---
### **Example 1:**
>**Input:** n = 3, k = 3  
>**Output:** "213"  

### **Example 2:**
>**Input:** n = 4, k = 9  
>**Output:** "2314"  

### **Example 3:**
>**Input:** n = 3, k = 1  
>**Output:** "123"  

## Constraints
---
- `1 <= n <= 9`  
- `1 <= k <= n!`  

## Solution
---
We can generate `k!` permutations, but this is not an optimal solution, so:  
- Let's consider the case for `n = 4` and `k = 14`.  
  - We know there are `24` permutations (`n!`).  
  - Because the numbers are in sequence from `1` to `n`, we have the next permutations:  
    - 1 + permutations of {2, 3, 4} -> (3! = 6) -> (**1**234, **1**243, **1**324, **1**342, **1**423, **1**432) -> Permutations `1` to `6`
    - 2 + permutations of {1, 3, 4} -> (3! = 6) -> (**2**134, **2**143, **2**314, **2**341, **2**413, **2**431) -> Permutations `7` to `12`
    - 3 + permutations of {1, 2, 4} -> (3! = 6) -> (**3**124, **3**142, **3**214, **3**241, **3**412, **3**421) -> Permutations `13` to `18`
    - 4 + permutations of {1, 2, 3} -> (3! = 6) -> (**4**123, **4**132, **4**213, **4**231, **4**312, **4**321) -> Permutations `19` to `24`
  - From the previous, we know that the <code>14<sup>th</sup></code> permutation (`k = 14`) starts with `3`, so we are at the <code>13<sup>th</sup></code> permutation.  
  - Then to calculate the next number we repeat the process with the rest of the numbers:  
    - 1 + permutations of {2, 4} -> (2! = 2) -> (**1**24, **1**42) -> Permutations `13` to `14`  
    - 2 + permutations of {1, 4} -> (2! = 2) -> (**2**14, **2**41) -> Permutations `15` to `16`  
    - 4 + permutations of {1, 2} -> (2! = 2) -> (**4**12, **4**21) -> Permutations `17` to `18`  
  - From the previous, we know the next number is `1`, so, we repeat the process:  
    - 2 + permutation of {4} -> (1! = 1) -> (**2**4) -> Permutations `13`.  
    - 4 + permutation of {2} -> (1! = 1) -> (**4**2) -> Permutations `14`.  
  - From the previous, we know the next number is `4`, so, we repeat the process:  
    - 2 + permutation of {} -> (0! = 1) -> (**2**) -> Permutations `14`.  
  - From the previous, we know the next number is `2`.  There are no more numbers left, so, the algorithm ends.  
  
The <code>14<sup>th</sup></code> permutation is: `3142`.  

### Solution
---
```c++
class Solution {
public:
  string getPermutation(int n, int k) {
    string permutation = "";
    vector<bool> v(n+1,false);
    vector<int> f(n+1, 1);
    
    for (int i = 2; i <= n; i++)
      f[i] = f[i-1] * i;
    
    k--;
    for(int i = 1; i <= n; i++){
      int x = k/f[n-i];
      int j;
      k -= x * f[n-i];
      for(j = 1; j <= n; j++) {
        if (!v[j] && x==0)
          break;
        if (!v[j])
          x--;
      }
      if (j<=n)
        v[j] = true;
      permutation += to_string(j);
    }
    return permutation;
  }
};
```