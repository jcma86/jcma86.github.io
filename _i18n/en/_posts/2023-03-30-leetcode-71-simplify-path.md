---
title: Simplify Path
platform: LeetCode
number: 71
author: jose
layout: post
language: en
date: 2023-03-30 22:30 +0300
categories: [programming, stack, twopointers, slidingwindow]
tags: [c/c++, leetcode, stack, twopointers, slidingwindow]
difficulty: medium
source: https://leetcode.com/problems/simplify-path/
proglang: C/C++
math: true
mermaid: true
pin: true
---
## {% t posts.problem %}
---
Given a string `path`, which is an **absolute path** (starting with a slash `'/'`) to a file or directory in a Unix-style file system, convert it to the simplified **canonical path**.  

In a Unix-style file system, a period `'.'` refers to the current directory, a double period `'..'` refers to the directory up a level, and any multiple consecutive slashes (i.e. `'//'`) are treated as a single slash `'/'`. For this problem, any other format of periods such as `'...'` are treated as file/directory names.  

The canonical path should have the following format:  

* The path starts with a single slash `'/'`.  
* Any two directories are separated by a single slash `'/'`.  
* The path does not end with a trailing `'/'`.  
* The path only contains the directories on the path from the root directory to the target file or directory (i.e., no period `'.'` or double period `'..'`)  

Return *the simplified **canonical path***.  

## Examples
---
### **Example 1:**
>**Input:** path = "/home/"  
>**Output:** "/home"  
>**Explanation:** Note that there is no trailing slash after the last directory name.  

### **Example 2:**
>**Input:** path = "/../"  
>**Output:** "/"  
>**Explanation:** Going one level up from the root directory is a no-op, as the root level is the highest level you can go.  

### **Example 3:**
>**Input:** path = "/home//foo/"  
>**Output:** "/home/foo"  
>**Explanation:** In the canonical path, multiple consecutive slashes are replaced by a single one.  

## Constraints
---
- `1 <= path.length <= 3000`  
- `path` consists of English letters, digits, period `'.'`, slash `'/'` or `'_'`.  
- `path` is a valid absolute Unix path.  

## Solution
---
Using a **[stack](/categories/stack/)** and a **[window](/categories/slidingwindow/)** **[two pointers](/categories/twopointers/)** we can solve this problem.  
1. We find each subfolder in the path:  
  - For this, we identify a substring between two `'/'`.  
  - The left pointer starts at one place behind the right pointer.  
  - We move the right pointer until a `'/'` is found.  
  - This window is our subfolder/path.
2. Once we have the window:  
  - If the window is `'/..'` we remove the top element of our stack.  
  - If the window is `'/.'` we do nothing.  
  - Otherwise we push the window to the stack.
3. Once finish:  
  - If the stack is empty, return `'/'`.  
  - If stack contains elements, build the path joining the elements of the stack.  
  - If our result has a `/` at the end, we delete it.  


```c++
class Solution {
public:
  string simplifyPath(string path) {
    stack<string> cpath;

    int l=0;
    int r=1;
    
    while (r<path.size()) {
      while(r < path.size() && path[r] == '/')
        r++;
      l = r-1;
      while(r < path.size() && path[r] != '/')
        r++;
      string tmp = path.substr(l, r-l);
      if (tmp != "/.." && tmp != "/.")
        cpath.push(tmp);
      else if (tmp == "/.." && !cpath.empty())
        cpath.pop();

      r++;
    }

    if (cpath.empty())
      return "/";

    string result = ""s;
    while(!cpath.empty()) {
      result = cpath.top() + result;
      cpath.pop();
    }
    if (result.size() > 1 && result.back() == '/')
      result.pop_back();

    return result;
  }
};
```
