---
title: Linked List with C++
author: jose
layout: post
language: en
date: 2023-04-20 12:58 +0300
categories: [articles, datastructures]
tags: [linkedlist, datastructures]
proglang: C/C++
math: true
mermaid: true
pin: true
---

# Linked List with C++
---
A linked list is a data structure that consists of a sequence of nodes, where each node contains a value and a pointer to the next node in the sequence. Linked lists are commonly used in computer programming to implement dynamic data structures.

## Linked List Node
---
To implement a linked list in C++, we first define a struct to represent a node:

```cpp
struct Node {
  int data;
  Node* next;
};
```

The `Node` struct has two members: `data`, which stores the value of the node, and `next`, which stores a pointer to the next node in the sequence.

## Linked List Class
---
We can then define a class to represent a linked list:

```cpp
class LinkedList {
private:
  Node* head;
public:
  LinkedList();
  void insert(int data);
  void remove(int data);
  void display();
};
```

The `LinkedList` class has a private member `head`, which stores a pointer to the first node in the sequence. The class also has three public member functions:

* `insert(int data)`: Inserts a new node with the given data at the end of the linked list.
* `remove(int data)`: Removes the first node in the sequence with the given data.
* `display()`: Displays the values of all nodes in the sequence.

We can implement these member functions as follows:
```cpp
LinkedList::LinkedList() {
    head = nullptr;
}

void LinkedList::insert(int data) {
  Node* new_node = new Node;
  new_node->data = data;
  new_node->next = nullptr;
  if (head == nullptr) {
    head = new_node;
  } else {
    Node* curr = head;
    while (curr->next != nullptr) {
      curr = curr->next;
    }
    curr->next = new_node;
  }
}

void LinkedList::remove(int data) {
  if (head == nullptr) {
    return;
  }
  if (head->data == data) {
    Node* temp = head;
    head = head->next;
    delete temp;
    return;
  }
  Node* curr = head;
  while (curr->next != nullptr) {
    if (curr->next->data == data) {
      Node* temp = curr->next;
      curr->next = curr->next->next;
      delete temp;
      return;
    }
    curr = curr->next;
  }
}

void LinkedList::display() {
  Node* curr = head;
  while (curr != nullptr) {
    std::cout << curr->data << " ";
    curr = curr->next;
  }
  std::cout << std::endl;
}
```

In the `insert` function, we first create a new node with the given data, and set its `next` pointer to `nullptr`. If the linked list is empty, we set `head` to the new node. Otherwise, we traverse the linked list until we reach the last node, and set its `next` pointer to the new node.  

In the `remove` function, we first handle the case where the node to be removed is the first node in the sequence. If `head` contains the data, we delete `head`, set `head` to `head->next`, and return. Otherwise, we traverse the linked list until we find the node to be removed, delete it, and set the previous node's `next` pointer to the next node.  

In the `display` function, we traverse the linked list and print the value of each node.  

## Usage
---
To use the LinkedList class, we can create an instance of the class and call its member functions as needed:  

```cpp
int main() {
  LinkedList list;
  list.insert(1);
  list.insert(2);
  list.insert(3);
  list.display(); // Output: 1 2 3 
  list.remove(2);
  list.display(); // Output: 1 3 
  return 0;
}
```

In this example, we create a `LinkedList` object called `list`, and insert three nodes with values 1, 2, and 3. We then display the contents of the linked list using the `display` function, which outputs "1 2 3". We then remove the node with value 2 using the `remove` function, and display the updated contents of the linked list, which outputs "1 3".

## Conclusion
---
In this article, we learned how to implement a linked list data structure in C++. Linked lists are a powerful tool for managing dynamic data, and can be used in a variety of programming applications. By understanding the basics of linked lists and how to implement them in C++, you can improve your programming skills and build more complex and efficient programs.
