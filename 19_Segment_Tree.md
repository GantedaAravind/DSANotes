# 🌳 What is a Segment Tree?

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

## 🌳 Segment Tree Node Structure

Each **node** in a Segment Tree represents an **interval (segment)** of the array.
So a node typically contains:

1. **Range (start, end):**

   - The indices of the subarray this node represents (e.g., `[L, R]`).
   - Example: root = `[0, n-1]`, left child = `[0, mid]`, right child = `[mid+1, R]`.

2. **Value (aggregated result):**

   - The information about this segment (depends on the problem).
   - Examples:

     - Range **sum** → node stores sum of elements in `[L, R]`.
     - Range **min** → node stores minimum element in `[L, R]`.
     - Range **max** → node stores maximum element in `[L, R]`.
     - Range **gcd** → node stores gcd of `[L, R]`.

3. **Pointers to children (optional depending on implementation):**

   - Left child → represents `[L, mid]`
   - Right child → represents `[mid+1, R]`
   - In array-based representation (common in competitive programming), children are just indices in an array (like a heap).

---

### 🧩 Example (Range Sum Segment Tree)

Say `arr = [2, 5, 1, 4]`.

- Root node:

  - Interval = `[0, 3]`
  - Value = `2 + 5 + 1 + 4 = 12`

- Left child:

  - Interval = `[0, 1]`
  - Value = `2 + 5 = 7`

- Right child:

  - Interval = `[2, 3]`
  - Value = `1 + 4 = 5`

- Leaf nodes:

  - `[0,0] → 2`, `[1,1] → 5`, `[2,2] → 1`, `[3,3] → 4`

---

### 📦 So, a Node Can Be Defined As:

```js
class SegmentTreeNode {
  constructor(start, end, value) {
    this.start = start; // left index of range
    this.end = end; // right index of range
    this.value = value; // aggregated info (sum, min, max, etc.)
    this.left = null; // left child
    this.right = null; // right child
  }
}
```

---

👉 In practice:

- If you use an **object-oriented style** → each node has `start`, `end`, `value`, `left`, `right`.
- If you use an **array representation** (like in competitive programming) → node at index `i` stores `value`, and its children are `2*i` and `2*i+1`.

---

### 📊 Time Complexity

| Operation   | Complexity   |
| ----------- | ------------ |
| Build Tree  | **O(n)**     |
| Query Range | **O(log n)** |
| Update      | **O(log n)** |

---

## 📘 Segment Tree for Range Sum Queries

### 1. Problem Definition

We have an array `arr[0..n-1]`, and we want to:

1. **Query the sum** of elements between indices `[L, R]`.
2. **Update an element** at index `i` to a new value.

We want both operations to be efficient (`O(log n)`).

---

### 2. Key Concepts

- **Each node in the tree represents a segment of the array.**
- The root node covers `[0, n-1]`.
- Left child covers `[l, mid]`, right child covers `[mid+1, r]`.
- Each node stores the **sum of its segment**.

---

### 3. Node Structure

If using an object-based tree:

```js
class SegmentTreeNode {
  constructor(start, end, value) {
    this.start = start; // left index of segment
    this.end = end; // right index of segment
    this.value = value; // sum of this segment
    this.left = null; // left child
    this.right = null; // right child
  }
}
```

If using an array-based representation (more common):

- `tree[1]` → root = sum of whole array
- `tree[2*i]` → left child
- `tree[2*i + 1]` → right child

---

### 4. Building the Tree (O(n))

Recursive logic:

1. If `l == r`, it’s a leaf → store `arr[l]`.
2. Otherwise:

   - Build left child `[l, mid]`.
   - Build right child `[mid+1, r]`.
   - Node value = `left.value + right.value`.

---

### 5. Querying the Sum (O(log n))

To query sum in `[L, R]`:

1. If segment `[l, r]` is completely inside `[L, R]`, return `tree[node]`.
2. If segment `[l, r]` is completely outside `[L, R]`, return `0`.
3. Otherwise, split into children and combine results.

### 🌳 Overlap Conditions in Segment Tree

#### ✅ 1. **Complete Overlap**

👉 When the query range `[ql, qr]` completely covers the node’s segment `[l, r]`.

- Condition:

  ```
  ql <= l && r <= qr
  ```

- Meaning: The entire segment `[l, r]` lies inside the query `[ql, qr]`.
- Action:

  - Directly return the value stored at this node (no need to go deeper).

- Example:
  Query `[1, 4]`, Node `[2, 3]` → completely inside.

---

#### ❌ 2. **No Overlap**

👉 When the query range `[ql, qr]` and the node’s segment `[l, r]` do not intersect at all.

- Condition:

  ```
  qr < l || ql > r
  ```

- Meaning: The segment is completely outside the query range.
- Action:

  - Return the **neutral value** for the operation.
  - For sum = `0`, for min = `+∞`, for max = `-∞`.

- Example:
  Query `[1, 4]`, Node `[5, 7]` → no overlap.

---

#### ⚡ 3. **Partial Overlap**

👉 When the query range `[ql, qr]` partially overlaps with the node’s segment `[l, r]`.

- Condition:

  ```
  !(qr < l || ql > r) && !(ql <= l && r <= qr)
  ```

  (i.e., not complete overlap and not no overlap).

- Meaning: Some part of the segment overlaps with query.
- Action:

  - Split into left and right children.
  - Query both sides and combine the results.

- Example:
  Query `[1, 4]`, Node `[0, 2]` → partial overlap (index 0 is outside, but 1–2 is inside).

---

#### 🧩 Example Walkthrough

Array: `[2, 5, 1, 4, 9, 3]`
Query: sum `[1, 3]`
Root covers `[0, 5]`.

- Root `[0,5]` → **partial overlap** → go left `[0,2]`, right `[3,5]`.
- Left `[0,2]` → **partial overlap** (0 is outside) → split.

  - `[0,1]` → partial again.

    - `[0,0]` → no overlap (outside query). Return 0.
    - `[1,1]` → complete overlap. Return `5`.

  - `[2,2]` → complete overlap. Return `1`.
    → Left sum = 5 + 1 = 6.

- Right `[3,5]` → partial.

  - `[3,3]` → complete overlap. Return `4`.
  - `[4,5]` → no overlap. Return `0`.
    → Right sum = 4.

Final Answer = 6 + 4 = **10** ✅

---

---

### 6. Updating an Element (O(log n))

To update index `i` to `newVal`:

1. Traverse down to leaf representing `i`.
2. Update leaf’s value.
3. Recompute sums on the way back up.

---

### 7. **Implementations**

1. **Array-based representation** (efficient, used in contests).
2. **Tree node representation** (intuitive, like a real tree).

### 🌳 1. Array-Based Segment Tree (Efficient)

This is the **version you already have**. It stores the tree in an array, where:

- Root = `tree[1]`.
- Left child = `tree[2*i]`.
- Right child = `tree[2*i+1]`.

✅ Efficient in memory and speed.

```js
class SegmentTreeArray {
  constructor(arr) {
    this.n = arr.length;
    this.tree = new Array(4 * this.n).fill(0);
    this.build(arr, 1, 0, this.n - 1);
  }

  build(arr, node, l, r) {
    if (l === r) {
      this.tree[node] = arr[l];
      return;
    }
    let mid = Math.floor((l + r) / 2);
    this.build(arr, 2 * node, l, mid);
    this.build(arr, 2 * node + 1, mid + 1, r);
    this.tree[node] = this.tree[2 * node] + this.tree[2 * node + 1];
  }

  query(node, l, r, ql, qr) {
    if (qr < l || ql > r) return 0; // completely outside
    if (ql <= l && r <= qr) return this.tree[node]; // completely inside
    let mid = Math.floor((l + r) / 2);
    let leftSum = this.query(2 * node, l, mid, ql, qr);
    let rightSum = this.query(2 * node + 1, mid + 1, r, ql, qr);
    return leftSum + rightSum;
  }

  rangeSum(ql, qr) {
    return this.query(1, 0, this.n - 1, ql, qr);
  }

  update(node, l, r, idx, newVal) {
    if (l === r) {
      this.tree[node] = newVal;
      return;
    }
    let mid = Math.floor((l + r) / 2);
    if (idx <= mid) {
      this.update(2 * node, l, mid, idx, newVal);
    } else {
      this.update(2 * node + 1, mid + 1, r, idx, newVal);
    }
    this.tree[node] = this.tree[2 * node] + this.tree[2 * node + 1];
  }

  pointUpdate(idx, newVal) {
    this.update(1, 0, this.n - 1, idx, newVal);
  }
}
```

---

### 🌲 2. Tree Node-Based Segment Tree (Intuitive)

Here, we explicitly build a **binary tree of nodes**, where each node stores:

- `start` and `end` → the range it covers
- `sum` → sum of that segment
- `left` and `right` → pointers to children

✅ Easier to visualize, great for learning.

```js
class SegmentTreeNode {
  constructor(start, end, sum = 0) {
    this.start = start;
    this.end = end;
    this.sum = sum;
    this.left = null;
    this.right = null;
  }
}

class SegmentTreeTree {
  constructor(arr) {
    this.root = this.build(arr, 0, arr.length - 1);
  }

  // Build tree recursively
  build(arr, l, r) {
    if (l > r) return null;
    if (l === r) return new SegmentTreeNode(l, r, arr[l]);

    let mid = Math.floor((l + r) / 2);
    let node = new SegmentTreeNode(l, r);

    node.left = this.build(arr, l, mid);
    node.right = this.build(arr, mid + 1, r);

    node.sum = node.left.sum + node.right.sum;
    return node;
  }

  // Query sum in range [ql, qr]
  query(node, ql, qr) {
    if (!node || qr < node.start || ql > node.end) return 0; // outside
    if (ql <= node.start && node.end <= qr) return node.sum; // inside
    return this.query(node.left, ql, qr) + this.query(node.right, ql, qr);
  }

  rangeSum(ql, qr) {
    return this.query(this.root, ql, qr);
  }

  // Update value at index
  update(node, idx, newVal) {
    if (!node || idx < node.start || idx > node.end) return;

    if (node.start === node.end) {
      node.sum = newVal;
      return;
    }

    this.update(node.left, idx, newVal);
    this.update(node.right, idx, newVal);

    node.sum = node.left.sum + node.right.sum;
  }

  pointUpdate(idx, newVal) {
    this.update(this.root, idx, newVal);
  }
}
```

---

### 📊 Example Usage for Both

```js
let arr = [2, 5, 1, 4, 9, 3];

// Array-based
let stArray = new SegmentTreeArray(arr);
console.log(stArray.rangeSum(1, 3)); // 5+1+4 = 10
stArray.pointUpdate(2, 7);
console.log(stArray.rangeSum(1, 3)); // 5+7+4 = 16

// Tree-based
let stTree = new SegmentTreeTree(arr);
console.log(stTree.rangeSum(1, 3)); // 10
stTree.pointUpdate(2, 7);
console.log(stTree.rangeSum(1, 3)); // 16
```

---

### 8. Example Usage

```js
let arr = [2, 5, 1, 4, 9, 3];
let st = new SegmentTree(arr);

console.log(st.rangeSum(1, 3)); // sum of arr[1..3] = 5+1+4 = 10
st.pointUpdate(2, 7); // update arr[2] = 7
console.log(st.rangeSum(1, 3)); // sum of arr[1..3] = 5+7+4 = 16
```

---

### 9. Time & Space Complexity

| Operation  | Complexity                       |
| ---------- | -------------------------------- |
| Build Tree | **O(n)**                         |
| Query Sum  | **O(log n)**                     |
| Update     | **O(log n)**                     |
| Space      | **O(4n)** (array representation) |

---

# Problems

## 1. 📘 Segment Tree for Range Minimum Query (RMQ)

### 1. Problem Statement

Given an array `arr[0..n-1]`, support two operations efficiently:

1. **Range Minimum Query (RMQ):** Find the minimum element in subarray `[L, R]`.
2. **Update:** Change an element `arr[i]` to a new value.

---

### 2. Test Cases

#### Test Case 1:

```
Input: arr = [2, 5, 1, 4, 9, 3]
Query: min(1, 4) → min(5,1,4,9) = 1
```

#### Test Case 2:

```
Update: arr[2] = 7  → arr = [2, 5, 7, 4, 9, 3]
Query: min(1, 4) → min(5,7,4,9) = 4
```

#### Test Case 3:

```
Query: min(0, 5) → min(2,5,7,4,9,3) = 2
```

---

### 3. Key Insights

- Segment Tree structure is the same as for sum queries, but instead of storing **sum**, each node stores the **minimum** in its segment.
- Building → `O(n)`
- Query → `O(log n)`
- Update → `O(log n)`

---

### 4. Implementation (JavaScript, Array-Based)

```js
class SegmentTreeMin {
  constructor(arr) {
    this.n = arr.length;
    this.tree = new Array(4 * this.n).fill(Infinity);
    this.build(arr, 1, 0, this.n - 1);
  }

  // Build the tree
  build(arr, node, l, r) {
    if (l === r) {
      this.tree[node] = arr[l];
      return;
    }
    let mid = Math.floor((l + r) / 2);
    this.build(arr, 2 * node, l, mid);
    this.build(arr, 2 * node + 1, mid + 1, r);
    this.tree[node] = Math.min(this.tree[2 * node], this.tree[2 * node + 1]);
  }

  // Query min in range [ql, qr]
  query(node, l, r, ql, qr) {
    if (qr < l || ql > r) return Infinity; // completely outside
    if (ql <= l && r <= qr) return this.tree[node]; // completely inside
    let mid = Math.floor((l + r) / 2);
    let leftMin = this.query(2 * node, l, mid, ql, qr);
    let rightMin = this.query(2 * node + 1, mid + 1, r, ql, qr);
    return Math.min(leftMin, rightMin);
  }

  rangeMin(ql, qr) {
    return this.query(1, 0, this.n - 1, ql, qr);
  }

  // Update a value at index
  update(node, l, r, idx, newVal) {
    if (l === r) {
      this.tree[node] = newVal;
      return;
    }
    let mid = Math.floor((l + r) / 2);
    if (idx <= mid) {
      this.update(2 * node, l, mid, idx, newVal);
    } else {
      this.update(2 * node + 1, mid + 1, r, idx, newVal);
    }
    this.tree[node] = Math.min(this.tree[2 * node], this.tree[2 * node + 1]);
  }

  pointUpdate(idx, newVal) {
    this.update(1, 0, this.n - 1, idx, newVal);
  }
}
```

---

### 5. Example Usage

```js
let arr = [2, 5, 1, 4, 9, 3];
let st = new SegmentTreeMin(arr);

console.log(st.rangeMin(1, 4)); // min(5,1,4,9) = 1
st.pointUpdate(2, 7); // arr[2] = 7
console.log(st.rangeMin(1, 4)); // min(5,7,4,9) = 4
console.log(st.rangeMin(0, 5)); // min(2,5,7,4,9,3) = 2
```

---

### 6. Time & Space Complexity

| Operation  | Complexity                       |
| ---------- | -------------------------------- |
| Build Tree | **O(n)**                         |
| Query Min  | **O(log n)**                     |
| Update     | **O(log n)**                     |
| Space      | **O(4n)** (array representation) |

---
