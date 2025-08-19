## 🌳 What is a Segment Tree?

A **Segment Tree** is a **binary tree data structure** used for storing information about intervals (segments) of an array.

- It allows us to **efficiently answer range queries** (like sum, min, max, gcd, etc.) over an array.
- It also supports **updating elements** in the array efficiently.
- It’s essentially a divide-and-conquer structure where:

  - The root represents the entire array.
  - Each node represents a segment (subrange).
  - The leaves represent single elements of the array.

---

### ⚡ Operations Supported

1. **Range Query** – Get information about a subarray `[L, R]`.
   Examples:

   - Range sum
   - Range minimum / maximum
   - Range greatest common divisor (GCD)

2. **Update** – Change the value of an element in the array and reflect it in the tree.

---

### 📊 Time Complexity

| Operation   | Complexity   |
| ----------- | ------------ |
| Build Tree  | **O(n)**     |
| Query Range | **O(log n)** |
| Update      | **O(log n)** |

---

### 🧩 Example

Say we have an array:
`arr = [2, 5, 1, 4, 9, 3]`

- Root = sum(0..5) = 24
- Left child = sum(0..2) = 8
- Right child = sum(3..5) = 16
- Further splitting until leaves represent single elements.

Now, if we want **sum of range \[1, 4]**:

- Instead of iterating, the tree breaks it into a few segments → query in O(log n).

If we **update arr\[2] = 7**, we update the leaf and propagate changes up the tree.

---
