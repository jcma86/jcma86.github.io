---
title: Vectors with C++
author: jose
layout: post
language: en
date: 2023-04-20 12:59 +0300
categories: [articles, datastructures]
tags: [vector, datastructures]
proglang: C/C++
math: true
mermaid: true
pin: true
---

# Vectors with C++
---
In programming, vectors are a data structure used for storing collections of values. Vectors are implemented as templates in C++, allowing them to store values of any data type. In this page, we will explore how to use vectors in C++.  

## Declaring Arrays in C++
---
To declare a vector in C++, you use the `vector` keyword followed by the data type of the elements in the vector:  

```cpp
vector<int> myVector = {1, 2, 3, 4, 5};
```

You can also declare a vector without initializing its values, like this:

```cpp
vector<int> myVector;
```

## Accessing Vector Elements
---
You can access vector elements using their index, just like with arrays:

```cpp
vector<int> myVector = {1, 2, 3, 4, 5};
cout << myVector[0] << endl; // prints 1
cout << myVector[2] << endl; // prints 3
```

You can also use a loop to iterate over the elements of a vector:
```cpp
vector<int> myVector = {1, 2, 3, 4, 5};
for (int i = 0; i < myVector.size(); i++) {
    cout << myVector[i] << endl;
}
```

## Adding Elements to a Vector
---
You can add elements to a vector using the `push_back` method:

```cpp
vector<int> myVector = {1, 2, 3, 4, 5};
myVector.push_back(6);
```

This will add the value 6 to the end of the vector.

## Removing Elements from a Vector
---
You can remove elements from a vector using the `erase` method:

```cpp
vector<int> myVector = {1, 2, 3, 4, 5};
myVector.erase(myVector.begin() + 2);
```

This will remove the element at index 2 (which has the value 3) from the vector.  

## Common Operations on Vectors
---
There are several common operations that can be performed on vectors in C++, such as sorting and searching. The algorithm library provides functions for these operations:

```cpp
vector<int> myVector = {5, 3, 1, 4, 2};

// sort the vector in ascending order
sort(myVector.begin(), myVector.end());

// search for the value 3 in the vector
auto result = find(myVector.begin(), myVector.end(), 3);
if (result != myVector.end()) {
    cout << "Found at index " << result - myVector.begin() << endl;
} else {
    cout << "Not found" << endl;
}
```

This code will sort the vector in ascending order and then search for the value 3 in the vector. If the value is found, it will print out its index.

## Conclusion
---
And that's a brief overview of vectors in C++. Vectors are a very useful data structure, as they allow you to store and access collections of values of any data type. With vectors, you can add and remove elements during runtime, making them very versatile.

