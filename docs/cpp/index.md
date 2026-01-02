---
title: C++ STL Reference
---

## What is STL?

The Standard Template Library (STL) is a collection of generic C++ libraries that provide commonly used data structures, algorithms, iterators, and utilities.

### Core Components

1. Containers – Store data
2. Iterators – Access container elements
3. Algorithms – Operate on ranges
4. Functors (Function Objects)
5. Adapters
6. Utilities & Helpers

## Containers

### Sequence Containers

Store elements in a specific linear order.

| Container         | Description                                  |
| ----------------- | -------------------------------------------- |
| std::vector       | Dynamic array. Fast random access.           |
| std::deque        | Double-ended queue. Chunks of memory.        |
| std::list         | Doubly linked list.                          |
| std::forward_list | Singly linked list. Minimal memory overhead. |
| std::array        | Static array. Size fixed at compile time.    |

### Container Adapters

Provide a restricted interface to sequence containers.

| Adapter             | Behavior                          |
| ------------------- | --------------------------------- |
| std::stack          | LIFO. Use push(), pop(), top().   |
| std::queue          | FIFO. Use push(), pop(), front(). |
| std::priority_queue | Heap. Use push(), pop(), top().   |

### Associative Containers

Sorted collections implemented (usually) as Red-Black Trees. Keys are ordered.

| Container     | Description                                     |
| ------------- | ----------------------------------------------- |
| std::set      | Collection of sorted unique keys.               |
| std::multiset | Collection of sorted keys (duplicates allowed). |
| std::map      | Sorted Key-Value pairs.                         |
| std::multimap | Sorted Key-Value pairs (duplicates allowed).    |

### Unordered Associative Containers

Implemented as Hash Tables. Keys are not sorted.

| Container          | Description             |
| ------------------ | ----------------------- |
| std::unordered_set | Unique keys.            |
| std::unordered_map | Unique Key-Value pairs. |
