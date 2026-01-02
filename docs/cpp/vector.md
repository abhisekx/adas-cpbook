---
title: std::vector
---

## Overview

-   **Header:** `#include <vector>`
-   **Definition:** A dynamic array that manages its own memory. Elements are stored contiguously, allowing efficient random access.
-   **Key Characteristic:** Fast access and insertion at the end; slower insertion/deletion in the middle.

---

## 1. Initialization

Different ways to create and populate a vector.

```cpp
#include <vector>
#include <string>

// 1. Empty vector
std::vector<int> v1;

// 2. Fill constructor: 5 integers, all initialized to 10
std::vector<int> v2(5, 10); // {10, 10, 10, 10, 10}

// 3. Initializer list (C++11)
std::vector<int> v3 = {1, 2, 3, 4, 5};

// 4. Copy constructor (from another vector)
std::vector<int> v4(v3);

// 5. Range constructor (from another container or array)
int arr[] = {10, 20, 30};
std::vector<int> v5(arr, arr + 3); // {10, 20, 30}

```

---

## 2. Element Access

Methods to read or modify elements.

| Method      | Description                                    | Safety check                                 |
| ----------- | ---------------------------------------------- | -------------------------------------------- |
| `v[i]`      | Access element at index `i`.                   | **No** (Undefined behavior if out of bounds) |
| `v.at(i)`   | Access element at index `i`.                   | **Yes** (Throws `std::out_of_range`)         |
| `v.front()` | Access the first element.                      | Undefined if empty                           |
| `v.back()`  | Access the last element.                       | Undefined if empty                           |
| `v.data()`  | Returns a raw pointer to the underlying array. | Useful for C-style APIs                      |

**Example:**

```cpp
std::vector<int> v = {10, 20, 30};

int a = v[0];      // 10
int b = v.at(1);   // 20
v.back() = 100;    // v is now {10, 20, 100}
int* ptr = v.data(); // Pointer to 10

```

---

## 3. Iterators & Traversal

Standard ways to loop through a vector.

```cpp
std::vector<int> v = {1, 2, 3};

// 1. Range-based for loop (Best for simple traversal)
for (int x : v) {
    // Read x
}
for (int& x : v) {
    x *= 2; // Modify elements
}

// 2. Iterator loop
for (auto it = v.begin(); it != v.end(); ++it) {
    std::cout << *it << " ";
}

// 3. Reverse Iterator loop
for (auto it = v.rbegin(); it != v.rend(); ++it) {
    std::cout << *it << " "; // Prints 3 2 1
}

```

---

## 4. Modifiers (Adding/Removing)

| Method               | Description                                           | Complexity |
| -------------------- | ----------------------------------------------------- | ---------- |
| `push_back(val)`     | Adds `val` to the end.                                | Amortized  |
| `emplace_back(args)` | Constructs element in-place at the end (avoids copy). | Amortized  |
| `pop_back()`         | Removes the last element.                             |            |
| `insert(it, val)`    | Inserts `val` before iterator `it`.                   |            |
| `erase(it)`          | Removes element at iterator `it`.                     |            |
| `erase(it1, it2)`    | Removes elements in range `[it1, it2)`.               |            |
| `clear()`            | Removes all elements.                                 |            |
| `resize(n)`          | Resizes vector to contain `n` elements.               | or         |
| `swap(v2)`           | Swaps contents with vector `v2`.                      |            |

**Example:**

```cpp
struct Point { int x, y; Point(int x, int y) : x(x), y(y) {} };

std::vector<Point> points;

// push_back copies the object
points.push_back(Point(1, 2));

// emplace_back constructs it directly in the vector memory (More efficient)
points.emplace_back(3, 4);

std::vector<int> v = {1, 2, 3, 4, 5};
v.erase(v.begin() + 1); // Removes 2. v is now {1, 3, 4, 5}

```

> **Note on `std::erase` vs `std::erase_if` (C++20):**
> You can now remove elements matching a criteria easily:
> `std::erase_if(v, [](int x) { return x % 2 == 0; });` // Removes all even numbers.

---

## 5. Capacity & Memory Management

Understanding the difference between `size` and `capacity` is crucial for performance.

-   **Size:** How many elements are currently in the vector.
-   **Capacity:** How many elements can be held in the currently allocated memory block before a reallocation is needed.

| Method            | Description                                                                               |
| ----------------- | ----------------------------------------------------------------------------------------- |
| `empty()`         | Checks if the vector has no elements (returns `true`/`false`).                            |
| `size()`          | Returns the number of elements.                                                           |
| `capacity()`      | Returns the size of the storage space currently allocated.                                |
| `reserve(n)`      | Requests that the vector capacity be at least `n`. **Use this to prevent reallocations.** |
| `shrink_to_fit()` | Requests the removal of unused capacity (C++11).                                          |

**Performance Tip:**
If you know you are going to push 1000 elements, use `reserve` first. This prevents the vector from reallocating memory and copying elements multiple times as it grows.

```cpp
std::vector<int> v;
v.reserve(1000); // Allocates memory for 1000 ints immediately
for(int i=0; i<1000; ++i) {
    v.push_back(i); // No reallocation occurs here
}

```

---

## 6. Time Complexity Summary

| Operation                    | Complexity       | Note                                          |
| ---------------------------- | ---------------- | --------------------------------------------- |
| Random Access                | $O(1)$           | Direct memory addressing.                     |
| Insertion/Deletion at End    | Amortized $O(1)$ | Fast, but occasionally triggers reallocation. |
| Insertion/Deletion in Middle | $O(n)$           | Requires shifting subsequent elements.        |
| Search (Unsorted)            | $O(n)$           | Linear scan.                                  |
| Search (Sorted)              | $O(log n)$       | Using `std::binary_search`.                   |

---

## 7. Common Algorithms with Vector

Vectors work seamlessly with `<algorithm>`.

```cpp
#include <algorithm>
#include <vector>

std::vector<int> v = {4, 1, 3, 5, 2};

// Sort
std::sort(v.begin(), v.end()); // {1, 2, 3, 4, 5}

// Find
auto it = std::find(v.begin(), v.end(), 3);
if (it != v.end()) {
    // Found it
}

// Binary Search (Must be sorted first)
bool found = std::binary_search(v.begin(), v.end(), 3); // true

// Min/Max Element
auto max_it = std::max_element(v.begin(), v.end());
int max_val = *max_it; // 5

```
