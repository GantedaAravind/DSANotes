## ✅ What is a **Heap**?

A **Heap** is a **complete binary tree** that satisfies the **heap property**:

- A **complete binary tree** means all levels are filled except possibly the last, and the last level has nodes as far left as possible.
- The **heap property** depends on the type:

  - **Max-Heap**: Parent node is always **greater than or equal** to its children.
  - **Min-Heap**: Parent node is always **less than or equal** to its children.

---

## 🔁 Types of Heaps

| Heap Type    | Root Node      | Heap Property        |
| ------------ | -------------- | -------------------- |
| **Min-Heap** | Smallest value | `parent <= children` |
| **Max-Heap** | Largest value  | `parent >= children` |

---

## 🏗️ Representation of Heap

- **Heaps are usually implemented using arrays** (not using binary trees explicitly).
- For any node at index `i`:

  - **Left Child** → `2*i + 1`
  - **Right Child** → `2*i + 2`
  - **Parent** → `(i - 1) // 2`

Example of Max-Heap:

```text
        50
       /  \
     30    40
    /  \
  10   20
Array: [50, 30, 40, 10, 20]
```

---

## 🛠️ Heap Operations

### 1. **Insert** (O(log N))

- Add element at the end of the array.
- Perform **heapify-up** (bubble-up or sift-up) to restore heap property.

### 2. **Delete / Extract Root** (O(log N))

- Root is always the min (min-heap) or max (max-heap).
- Replace root with last element.
- Perform **heapify-down** (sift-down) to restore heap property.

### 3. **Peek / Get Min or Max** (O(1))

- Simply return the root element.

### 4. **Build Heap from Array** (O(N))

- Start heapifying from the last non-leaf node down to the root.
- Efficient than inserting one by one.

---

## ✅ `MinHeap` Class

```javascript
class MinHeap {
  constructor() {
    this.heap = [];
  }

  // 🔼 Insert a new value into the heap
  insert(value) {
    this.heap.push(value); // Step 1: Add at the end
    this._heapifyUp(this.heap.length - 1); // Step 2: Heapify up from the last index
  }

  // 🧹 Remove and return the minimum element (root)
  extractMin() {
    if (this.heap.length === 0) return null;
    if (this.heap.length === 1) return this.heap.pop();

    const min = this.heap[0];
    this.heap[0] = this.heap.pop(); // Move last to root
    this._heapifyDown(0); // Restore heap property

    return min;
  }

  // 👀 View the minimum element without removing
  peek() {
    return this.heap.length > 0 ? this.heap[0] : null;
  }

  // 🔄 Heapify up from a given index
  _heapifyUp(index) {
    while (index > 0) {
      const parentIndex = Math.floor((index - 1) / 2);

      if (this.heap[parentIndex] <= this.heap[index]) break;

      this._swap(index, parentIndex);
      index = parentIndex;
    }
  }

  // 🔄 Heapify down from a given index
  _heapifyDown(index) {
    const length = this.heap.length;

    while (true) {
      const left = 2 * index + 1;
      const right = 2 * index + 2;
      let smallest = index;

      if (left < length && this.heap[left] < this.heap[smallest]) {
        smallest = left;
      }

      if (right < length && this.heap[right] < this.heap[smallest]) {
        smallest = right;
      }

      if (smallest === index) break;

      this._swap(index, smallest);
      index = smallest;
    }
  }

  // 🔁 Swap helper function
  _swap(i, j) {
    [this.heap[i], this.heap[j]] = [this.heap[j], this.heap[i]];
  }

  // 📏 Return heap size
  size() {
    return this.heap.length;
  }

  // 📦 Return heap as array
  toArray() {
    return [...this.heap];
  }
}
```

---

### ✅ Sample Usage

```javascript
const minHeap = new MinHeap();

minHeap.insert(10);
minHeap.insert(5);
minHeap.insert(15);
minHeap.insert(1);

console.log(minHeap.toArray()); // [1, 5, 15, 10]
console.log(minHeap.peek()); // 1
console.log(minHeap.extractMin()); // 1
console.log(minHeap.toArray()); // [5, 10, 15]
```

---

### ✅ Time Complexity

| Operation      | Time     |
| -------------- | -------- |
| `insert()`     | O(log n) |
| `extractMin()` | O(log n) |
| `peek()`       | O(1)     |

---

## ✅ `MaxHeap` Class

```javascript
class MaxHeap {
  constructor() {
    this.heap = [];
  }

  // 🔼 Insert a new value into the heap
  insert(value) {
    this.heap.push(value); // Step 1: Add at the end
    this._heapifyUp(this.heap.length - 1); // Step 2: Heapify up from the last index
  }

  // 🧹 Remove and return the maximum element (root)
  extractMax() {
    if (this.heap.length === 0) return null;
    if (this.heap.length === 1) return this.heap.pop();

    const max = this.heap[0];
    this.heap[0] = this.heap.pop(); // Move last to root
    this._heapifyDown(0); // Restore heap property

    return max;
  }

  // 👀 View the maximum element without removing
  peek() {
    return this.heap.length > 0 ? this.heap[0] : null;
  }

  // 🔄 Heapify up from a given index
  _heapifyUp(index) {
    while (index > 0) {
      const parentIndex = Math.floor((index - 1) / 2);

      if (this.heap[parentIndex] >= this.heap[index]) break;

      this._swap(index, parentIndex);
      index = parentIndex;
    }
  }

  // 🔄 Heapify down from a given index
  _heapifyDown(index) {
    const length = this.heap.length;

    while (true) {
      const left = 2 * index + 1;
      const right = 2 * index + 2;
      let largest = index;

      if (left < length && this.heap[left] > this.heap[largest]) {
        largest = left;
      }

      if (right < length && this.heap[right] > this.heap[largest]) {
        largest = right;
      }

      if (largest === index) break;

      this._swap(index, largest);
      index = largest;
    }
  }

  // 🔁 Swap helper function
  _swap(i, j) {
    [this.heap[i], this.heap[j]] = [this.heap[j], this.heap[i]];
  }

  // 📏 Return heap size
  size() {
    return this.heap.length;
  }

  // 📦 Return heap as array
  toArray() {
    return [...this.heap];
  }
}
```

---

### ✅ Sample Usage

```javascript
const maxHeap = new MaxHeap();

maxHeap.insert(10);
maxHeap.insert(5);
maxHeap.insert(15);
maxHeap.insert(20);

console.log(maxHeap.toArray()); // [20, 15, 10, 5]
console.log(maxHeap.peek()); // 20
console.log(maxHeap.extractMax()); // 20
console.log(maxHeap.toArray()); // [15, 5, 10]
```

---

### ✅ Time Complexity

| Operation      | Time     |
| -------------- | -------- |
| `insert()`     | O(log n) |
| `extractMax()` | O(log n) |
| `peek()`       | O(1)     |

---

## ✅ **Why and When We Use Heap Instead of Sorting**

### 🧠 **The Core Idea**

When you **don’t need the full sorted array**, and you’re only interested in the **top or bottom `k` elements**, **sorting** is **wasteful**.

Instead of sorting the whole array (`O(n log n)`), we can use a **Heap** and reduce the time to `O(n log k)`.

---

### 🔄 **Sorting vs Heap Comparison**

| Method        | Use Case                   | Time Complexity |
| ------------- | -------------------------- | --------------- |
| Sorting       | Full sorted order          | `O(n log n)`    |
| Heap (size k) | Top/Bottom k elements only | `O(n log k)` ✅ |

If `k` is small and `n` is large, **heaps save a LOT of time**.

---

## 📦 Example Problem: "Find the K Largest Elements"

**Problem:**
You are given an array of `n` elements. Find the **k largest** elements in the array.

---

### ❌ Brute Force (Using Sort)

1. Sort the array → `O(n log n)`
2. Take the last `k` elements → `O(k)`

#### Total Time: `O(n log n)`

### ✅ Optimal Method (Using Min-Heap of size k)

#### 💡 Why Min-Heap?

- We maintain the **k largest** elements seen so far.
- The **smallest among those k** will be at the **top of the min-heap**.
- if size of Heap becomes the more than `k` remove the top element.

#### ⏱ Time Complexity:

- Insertion in heap: `O(log k)`
- For `n` elements: `O(n log k)`

✅ **Much faster than sorting when `k << n`**

---

## ✅ Choosing Between **Min-Heap** and **Max-Heap** for Top-K Problems

| Problem Type            | Heap Type Used | Why?                                                                                       |
| ----------------------- | -------------- | ------------------------------------------------------------------------------------------ |
| **K Smallest Elements** | **Max-Heap**   | So the **largest among the smallest k** is on top. If a new number is smaller, replace it. |
| **K Largest Elements**  | **Min-Heap**   | So the **smallest among the largest k** is on top. If a new number is larger, replace it.  |

---

> **Insert every candidate**, then:
>
> - If **heap size exceeds `k`**, we **remove the root (top)**.

## 📦 Example 1: **K Largest Elements → Min-Heap of Size k**

We want top `k` largest numbers, so we:

- Maintain the **smallest among the top k** at the root.
- Replace root if a **new number is larger**.

✅ Use **Min-Heap**

---

## 📦 Example 2: **K Smallest Elements → Max-Heap of Size k**

We want top `k` smallest numbers, so we:

- Maintain the **largest among the top k** at the root.
- Replace root if a **new number is smaller**.

✅ Use **Max-Heap**

---




## ✅ Custom `MinHeap` with Comparator Function


### 🧠 How it works under the hood:

* JavaScript’s `.sort()` accepts a **comparator** function `compare(a, b)`:

  * If it returns `< 0`, `a` comes before `b`
  * If it returns `0`, they stay unchanged
  * If it returns `> 0`, `b` comes before `a`

---
```javascript
class MinHeap {
  constructor(compareFn) {
    this.data = [];
    this.compare = compareFn || ((a, b) => a - b); // Default: min-heap for numbers
  }

  getParentIndex(i) { return Math.floor((i - 1) / 2); }
  getLeftChildIndex(i) { return 2 * i + 1; }
  getRightChildIndex(i) { return 2 * i + 2; }

  swap(i, j) {
    [this.data[i], this.data[j]] = [this.data[j], this.data[i]];
  }

  insert(val) {
    this.data.push(val);
    this.heapifyUp();
  }

  heapifyUp() {
    let index = this.data.length - 1;
    while (
      index > 0 &&
      this.compare(this.data[index], this.data[this.getParentIndex(index)]) < 0
    ) {
      this.swap(index, this.getParentIndex(index));
      index = this.getParentIndex(index);
    }
  }

  extractMin() {
    if (this.data.length === 0) return null;
    if (this.data.length === 1) return this.data.pop();

    const min = this.data[0];
    this.data[0] = this.data.pop();
    this.heapifyDown();
    return min;
  }

  heapifyDown() {
    let index = 0;
    const length = this.data.length;

    while (this.getLeftChildIndex(index) < length) {
      let smallerChildIndex = this.getLeftChildIndex(index);
      const rightIndex = this.getRightChildIndex(index);

      if (
        rightIndex < length &&
        this.compare(this.data[rightIndex], this.data[smallerChildIndex]) < 0
      ) {
        smallerChildIndex = rightIndex;
      }

      if (this.compare(this.data[index], this.data[smallerChildIndex]) <= 0) {
        break;
      }

      this.swap(index, smallerChildIndex);
      index = smallerChildIndex;
    }
  }

  peek() {
    return this.data.length > 0 ? this.data[0] : null;
  }

  size() {
    return this.data.length;
  }

  isEmpty() {
    return this.data.length === 0;
  }
}
```

---

### ✅ Example 1: Min Heap for numbers

```javascript
const heap = new MinHeap((a, b) => a - b);
heap.insert(5);
heap.insert(2);
heap.insert(8);
heap.insert(1);

while (!heap.isEmpty()) {
  console.log(heap.extractMin()); // 1, 2, 5, 8
}
```

---

### ✅ Example 2: Min Heap for objects (e.g., sort by `age`)

```javascript
const heap = new MinHeap((a, b) => a.age - b.age);

heap.insert({ name: "Alice", age: 30 });
heap.insert({ name: "Bob", age: 25 });
heap.insert({ name: "Charlie", age: 35 });

while (!heap.isEmpty()) {
  console.log(heap.extractMin());
}
// { name: "Bob", age: 25 }
// { name: "Alice", age: 30 }
// { name: "Charlie", age: 35 }
```

---

# Learning

## ✅ **1. Check if an Array Represents a Min Heap**

### 📘 Problem Statement

You're given an array of integers `nums`.
Check whether this array represents a valid **binary min-heap**.

> In a **binary min-heap**, every parent node is **less than or equal to** its children, and the tree is complete (which array representation already guarantees).

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: nums = [10, 20, 30, 21, 23]
Explanation: All parents ≤ their children → valid min-heap
Output: true
```

#### ✅ Test Case 2:

```js
Input: nums = [10, 20, 30, 25, 15]
Explanation: 20 > 15 → violates min-heap property
Output: false
```

#### ✅ Test Case 3:

```js
Input: nums = [5]
Explanation: Single element is always a min-heap
Output: true
```

---

### 💡 Intuition

In an array representing a **binary heap**:

- In a Min Heap, every node should be **greater than or equal to its parent**.
- You're checking that for **each child**, its `parent <= child`.
- You start from index `1` (first child) up to the end.

---

### 🔍 Code Review & Explanation

```javascript
class Solution {
  isHeap(nums) {
    for (let index = 1; index < nums.length; index++) {
      let parent = Math.floor((index - 1) / 2);
      if (nums[parent] > nums[index]) {
        return false;
      }
    }
    return true;
  }
}
```

---

### ⏱️ Time & Space Complexity

| Operation | Complexity |
| --------- | ---------- |
| Time      | `O(n)`     |
| Space     | `O(1)`     |

---

### 📌 Summary

| Concept       | Check                                         |
| ------------- | --------------------------------------------- |
| Min-Heap      | Parent ≤ both children for all non-leaf nodes |
| Complete Tree | Already guaranteed by array representation    |
| Index Rules   | Left: `2*i+1`, Right: `2*i+2`                 |

---

## ✅ **3. Convert Min Heap to Max Heap**

### 📘 Problem Statement

Given an array representing a **Min Heap**, convert it into a **Max Heap** in-place.

> A Min Heap has the property:
> `parent ≤ children`
> A Max Heap has the property:
> `parent ≥ children`

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: [1, 3, 5, 7, 9, 2]
Explanation:
Input is a valid Min Heap.
Convert it to a valid Max Heap.
Output: [9, 7, 5, 1, 3, 2] (One valid Max Heap)
```

#### ✅ Test Case 2:

```js
Input: [10, 20, 15, 30, 40]
Output: [40, 30, 15, 10, 20] (Max Heap)
```

---

### 💡 Intuition

To convert a **Min Heap** to a **Max Heap**, we can:

- Traverse all non-leaf nodes **in reverse level order**
- For each node, apply **heapify down** (max-heapify)

This process is also called **heapifying the array** for Max Heap.

---

### 🧑‍💻 JavaScript Code

```js
function minToMaxHeap(arr) {
  const n = arr.length;

  // Start from last non-leaf node and apply maxHeapify
  for (let i = Math.floor(n / 2) - 1; i >= 0; i--) {
    maxHeapify(arr, n, i);
  }

  return arr;
}

// Helper: Max-Heapify a subtree rooted at index i
function maxHeapify(arr, n, i) {
  let largest = i;
  let left = 2 * i + 1;
  let right = 2 * i + 2;

  if (left < n && arr[left] > arr[largest]) {
    largest = left;
  }

  if (right < n && arr[right] > arr[largest]) {
    largest = right;
  }

  if (largest !== i) {
    [arr[i], arr[largest]] = [arr[largest], arr[i]];
    maxHeapify(arr, n, largest);
  }
}
```

---

### ✅ Sample Usage

```js
let minHeap = [1, 3, 5, 7, 9, 2];
console.log("Before:", minHeap);
let maxHeap = minToMaxHeap(minHeap);
console.log("After :", maxHeap);
```

---

### 🔄 Dry Run

Given: `[1, 3, 5, 7, 9, 2]` (Min Heap)

Start from index `2 → 1 → 0` and apply `maxHeapify()`:

- At index 2 → already satisfies max-heap
- At index 1 → swap 3 with 9
- At index 0 → swap 1 with 9 → then swap 1 with 7

Final: `[9, 7, 5, 1, 3, 2]` ✅

---

### ⏱️ Time & Space Complexity

| Operation | Complexity |
| --------- | ---------- |
| Time      | O(n)       |
| Space     | O(1)       |
| In-place  | ✅ Yes     |

---

# Medium

## ✅ **1. Kth Largest Element in an Array**

### 📘 Problem Statement

You're given an integer array `nums` and an integer `k`.
Return the **kth largest element** in the array.

> 📝 Note: It’s the kth **largest** in **sorted order**, not necessarily the kth **distinct** element.

🔒 Can you solve it **without sorting**?

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: nums = [3, 2, 1, 5, 6, 4], k = 2
Explanation: Sorted => [1, 2, 3, 4, 5, 6], 2nd largest = 5
Output: 5
```

#### ✅ Test Case 2:

```js
Input: nums = [3, 2, 3, 1, 2, 4, 5, 5, 6], k = 4
Explanation: Sorted => [1, 2, 2, 3, 3, 4, 5, 5, 6], 4th largest = 4
Output: 4
```

---

### 💡 Intuition

To find the `k`th **largest** element efficiently without sorting:

- Use a **Min Heap** of size `k`
- Keep track of the `k` largest elements
- If heap grows beyond `k`, remove the smallest
- The top of the heap will be the **kth largest element**

---

### 🧑‍💻 JavaScript Code

```js
class MinHeap {
  constructor() {
    this.heap = [];
  }

  insert(num) {
    this.heap.push(num);
    this.heapifyUp();
  }

  heapifyUp() {
    let index = this.heap.length - 1;

    while (index > 0) {
      let parent = Math.floor((index - 1) / 2);

      if (this.heap[parent] > this.heap[index]) {
        this.swap(parent, index);
        index = parent;
      } else {
        break;
      }
    }
  }

  swap(i, j) {
    [this.heap[i], this.heap[j]] = [this.heap[j], this.heap[i]];
  }

  heapifyDown() {
    let index = 0;

    while (true) {
      let left = 2 * index + 1;
      let right = 2 * index + 2;

      let smallest = index;

      if (left < this.heap.length && this.heap[left] < this.heap[smallest]) {
        smallest = left;
      }

      if (right < this.heap.length && this.heap[right] < this.heap[smallest]) {
        smallest = right;
      }

      if (smallest === index) {
        break;
      }
      this.swap(smallest, index);
      index = smallest;
    }
  }

  peek() {
    if (this.heap.length === 0) {
      return null;
    }
    return this.heap[0];
  }

  extractMin() {
    if (this.heap.length === 0) {
      return null;
    }

    if (this.heap.length === 1) {
      return this.heap.pop();
    }

    let min = this.heap[0];
    this.heap[0] = this.heap.pop();
    this.heapifyDown();
    return min;
  }

  size() {
    return this.heap.length;
  }
}

/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var findKthLargest = function (nums, k) {
  const minHeap = new MinHeap();
  for (let v of nums) {
    minHeap.insert(v);
    if (minHeap.size() > k) {
      minHeap.extractMin();
    }
  }

  return minHeap.peek();
};
```

---

### 🔄 Dry Run

Let `nums = [3, 2, 1, 5, 6, 4], k = 2`

- Insert: 3 → \[3]
- Insert: 2 → \[2, 3]
- Insert: 1 → \[2, 3] → pop 1
- Insert: 5 → \[3, 5] → pop 2
- Insert: 6 → \[5, 6] → pop 3
- Insert: 4 → \[5, 6] → ignore 4 (not in top 2)

✅ Output: `5`

---

### ⏱️ Time & Space Complexity

| Operation        | Complexity   |
| ---------------- | ------------ |
| Heap Insert      | `O(log k)`   |
| Heap Extract     | `O(log k)`   |
| Total Time       | `O(n log k)` |
| Space Complexity | `O(k)`       |

---

### 📌 Summary

| Approach    | Description                           |
| ----------- | ------------------------------------- |
| Min Heap    | Maintain `k` largest elements         |
| Top of heap | Is the `k`th largest overall          |
| Avoids sort | More efficient than `O(n log n)` sort |

---

## ✅ **2. Kth Smallest Element in an Array**

### 📘 Problem Statement

Given an integer array `nums` and an integer `k`, return the **kth smallest** element in the array.

> 📌 The result is based on **sorted order**, **not distinct elements**.

> 🚫 Don’t sort the entire array if you can avoid it — use a heap!

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: nums = [7, 10, 4, 3, 20, 15], k = 3
Explanation: Sorted = [3, 4, 7, 10, 15, 20], 3rd smallest = 7
Output: 7
```

#### ✅ Test Case 2:

```js
Input: nums = [7, 10, 4, 20, 15], k = 4
Sorted = [4, 7, 10, 15, 20] → 4th smallest = 15
Output: 15
```

---

### 💡 Intuition

To get the **kth smallest** without sorting the whole array:

- Use a **Max Heap** (priority queue) of size `k`
- Push first `k` elements into it
- For each next element:

  - If smaller than top of heap → replace root

- After processing, root of max heap is the `k`th smallest

---

### 🔄 Dry Run

Let `nums = [7, 10, 4, 3, 20, 15], k = 3`

Step-by-step max heap of size `k`:

1. Insert: 7 → `[7]`
2. Insert: 10 → `[10, 7]`
3. Insert: 4 → `[10, 7, 4]` (Heap keeps largest on top)

Now check rest:

- 3 < 10 → replace 10 → heap: `[7, 3, 4]`
- 20 > 7 → ignore
- 15 > 7 → ignore

Top of heap: **7** → ✅ 3rd smallest

---

### 🧑‍💻 JavaScript Code

```js
class MaxHeap {
  constructor() {
    this.heap = [];
  }

  insert(val) {
    this.heap.push(val);
    this._heapifyUp();
  }

  extractMax() {
    if (this.heap.length === 0) return null;
    if (this.heap.length === 1) return this.heap.pop();

    const max = this.heap[0];
    this.heap[0] = this.heap.pop();
    this._heapifyDown();
    return max;
  }

  peek() {
    return this.heap[0];
  }

  size() {
    return this.heap.length;
  }

  _heapifyUp() {
    let index = this.heap.length - 1;
    while (index > 0) {
      let parent = Math.floor((index - 1) / 2);
      if (this.heap[parent] >= this.heap[index]) break;
      [this.heap[parent], this.heap[index]] = [
        this.heap[index],
        this.heap[parent],
      ];
      index = parent;
    }
  }

  _heapifyDown() {
    let index = 0;
    const length = this.heap.length;

    while (true) {
      let left = 2 * index + 1;
      let right = 2 * index + 2;
      let largest = index;

      if (left < length && this.heap[left] > this.heap[largest]) {
        largest = left;
      }
      if (right < length && this.heap[right] > this.heap[largest]) {
        largest = right;
      }

      if (largest === index) break;

      [this.heap[index], this.heap[largest]] = [
        this.heap[largest],
        this.heap[index],
      ];
      index = largest;
    }
  }
}

// 🔍 Main function
function findKthSmallest(nums, k) {
  const maxHeap = new MaxHeap();

  for (let i = 0; i < nums.length; i++) {
    maxHeap.insert(nums[i]);
    if (maxHeap.size() > k) {
      maxHeap.extractMax();
    }
  }

  return maxHeap.peek();
}
```

---

### ⏱️ Time & Space Complexity

| Operation   | Complexity |
| ----------- | ---------- |
| Heap Insert | O(log k)   |
| Total Time  | O(n log k) |
| Space       | O(k)       |

---

## ✅ **3. Merge K Sorted Linked Lists**

### 📘 Problem Statement

You are given an array of `k` linked-lists, where each list is sorted in ascending order.

Return **one sorted linked list** that merges all of them.

---

### 🧪 Test Cases

#### ✅ Test Case 1

```js
Input: lists = [
  [1, 4, 5],
  [1, 3, 4],
  [2, 6],
];
Output: [1, 1, 2, 3, 4, 4, 5, 6];
```

#### ✅ Test Case 2

```js
Input: lists = [];
Output: [];
```

#### ✅ Test Case 3

```js
Input: lists = [[]];
Output: [];
```

---

### 💡 Intuition

To merge `k` sorted lists efficiently:

- Use a **Min Heap (Priority Queue)** to keep track of the **smallest head node** from each list.
- Repeatedly extract the smallest node and attach to the result list.
- If a node has a `next`, push it into the heap.

---

### 🔄 Dry Run

**lists = \[\[1→4→5], \[1→3→4], \[2→6]]**

MinHeap stores: (1,0), (1,1), (2,2) → pop 1 → push 4 → pop 1 → push 3 → etc.

Final order: `1→1→2→3→4→4→5→6`

---

### 🧑‍💻 JavaScript Code (Using Min Heap)

```js
class ListNode {
  constructor(val, next = null) {
    this.val = val;
    this.next = next;
  }
}

class MinHeap {
  constructor() {
    this.heap = [];
  }

  insert(node) {
    this.heap.push(node);
    this._heapifyUp();
  }

  extractMin() {
    if (this.heap.length === 0) return null;
    if (this.heap.length === 1) return this.heap.pop();

    const min = this.heap[0];
    this.heap[0] = this.heap.pop();
    this._heapifyDown();
    return min;
  }

  _heapifyUp() {
    let index = this.heap.length - 1;
    while (index > 0) {
      let parent = Math.floor((index - 1) / 2);
      if (this.heap[parent].val <= this.heap[index].val) break;
      [this.heap[parent], this.heap[index]] = [
        this.heap[index],
        this.heap[parent],
      ];
      index = parent;
    }
  }

  _heapifyDown() {
    let index = 0;
    const length = this.heap.length;
    while (true) {
      let left = 2 * index + 1;
      let right = 2 * index + 2;
      let smallest = index;

      if (left < length && this.heap[left].val < this.heap[smallest].val) {
        smallest = left;
      }
      if (right < length && this.heap[right].val < this.heap[smallest].val) {
        smallest = right;
      }

      if (smallest === index) break;

      [this.heap[index], this.heap[smallest]] = [
        this.heap[smallest],
        this.heap[index],
      ];
      index = smallest;
    }
  }

  size() {
    return this.heap.length;
  }
}

// 🔧 Merge function
function mergeKLists(lists) {
  const heap = new MinHeap();

  // Initialize heap with first node of each list
  for (let node of lists) {
    if (node) heap.insert(node);
  }

  const dummy = new ListNode(0);
  let current = dummy;

  while (heap.size() > 0) {
    const minNode = heap.extractMin();
    current.next = minNode;
    current = current.next;

    if (minNode.next) heap.insert(minNode.next);
  }

  return dummy.next;
}
```

---

### ✅ Sample Usage

```js
const lists = [
  arrayToList([1, 4, 5]),
  arrayToList([1, 3, 4]),
  arrayToList([2, 6]),
];

const merged = mergeKLists(lists);
printList(merged); // [1, 1, 2, 3, 4, 4, 5, 6]
```

---

### ⏱️ Time & Space Complexity

| Metric          | Value                 |
| --------------- | --------------------- |
| Time            | `O(N log k)`          |
| Space (Heap)    | `O(k)`                |
| N = total nodes | Sum of all list sizes |

---

### 📌 Summary

| Strategy       | Details                           |
| -------------- | --------------------------------- |
| Data Structure | Min Heap (Priority Queue)         |
| Handles Edge   | Empty lists, duplicates, nulls    |
| Efficient      | Much better than merging pairwise |

---

## ✅ **4. Return the K Largest Elements from an Array**

### 📘 Problem Statement

Given an integer array `nums` and an integer `k`, return the **k largest elements** from the array **in any order** (or sorted, if required).

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (nums = [3, 2, 1, 5, 6, 4]), (k = 2);
Output: [6, 5](or[(5, 6)]);
```

#### ✅ Test Case 2:

```js
Input: (nums = [7, 10, 4, 3, 20, 15]), (k = 3);
Output: [10, 15, 20];
```

#### ✅ Test Case 3:

```js
Input: (nums = [1]), (k = 1);
Output: [1];
```

---

### 💡 Intuition

To get the **k largest elements** efficiently:

- Use a **Min Heap** of size `k`
- Iterate over the array

  - If heap size < k → push element
  - Else if element > heap top → replace the smallest

- Heap will store the **k largest** values

---

### 🔄 Dry Run

For `nums = [3, 2, 1, 5, 6, 4], k = 2`

- Insert: 3 → \[3]
- Insert: 2 → \[2, 3]
- 1 → ignore (too small)
- 5 → replace 2 → \[3, 5]
- 6 → replace 3 → \[5, 6]
- 4 → ignore

✅ Output: \[5, 6]

---

### 🧑‍💻 JavaScript Code

```js
class MinHeap {
  constructor() {
    this.heap = [];
  }

  insert(val) {
    this.heap.push(val);
    this._heapifyUp();
  }

  extractMin() {
    if (this.heap.length === 0) return null;
    if (this.heap.length === 1) return this.heap.pop();

    const min = this.heap[0];
    this.heap[0] = this.heap.pop();
    this._heapifyDown();
    return min;
  }

  peek() {
    return this.heap[0];
  }

  size() {
    return this.heap.length;
  }

  _heapifyUp() {
    let index = this.heap.length - 1;
    while (index > 0) {
      let parent = Math.floor((index - 1) / 2);
      if (this.heap[parent] <= this.heap[index]) break;
      [this.heap[parent], this.heap[index]] = [
        this.heap[index],
        this.heap[parent],
      ];
      index = parent;
    }
  }

  _heapifyDown() {
    let index = 0;
    const length = this.heap.length;
    while (true) {
      let left = 2 * index + 1;
      let right = 2 * index + 2;
      let smallest = index;

      if (left < length && this.heap[left] < this.heap[smallest]) {
        smallest = left;
      }
      if (right < length && this.heap[right] < this.heap[smallest]) {
        smallest = right;
      }

      if (smallest === index) break;

      [this.heap[index], this.heap[smallest]] = [
        this.heap[smallest],
        this.heap[index],
      ];
      index = smallest;
    }
  }
}

// Main Function
function getKLargest(nums, k) {
  const minHeap = new MinHeap();

  for (let num of nums) {
    if (minHeap.size() < k) {
      minHeap.insert(num);
    } else if (num > minHeap.peek()) {
      minHeap.extractMin();
      minHeap.insert(num);
    }
  }

  return minHeap.heap; // contains k largest elements
}
```

---

### ✅ Sample Usage

```js
console.log(getKLargest([3, 2, 1, 5, 6, 4], 2)); // [5, 6]
console.log(getKLargest([7, 10, 4, 3, 20, 15], 3)); // [10, 15, 20]
```

---

### ⏱️ Time & Space Complexity

| Operation   | Complexity   |
| ----------- | ------------ |
| Heap Insert | `O(log k)`   |
| Total Time  | `O(n log k)` |
| Space       | `O(k)`       |

---

## ✅ **5. K Closest Elements**

### 📘 Problem Statement

Given a **sorted integer array** `arr`, two integers `k` and `x`, return the `k` closest integers to `x` in the array.

> The result should also be **sorted in ascending order**.

If there's a tie in distance, return the **smaller element**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (arr = [1, 2, 3, 4, 5]), (k = 4), (x = 3);
Output: [1, 2, 3, 4];
```

#### ✅ Test Case 2:

```js
Input: (arr = [1, 2, 3, 4, 5]), (k = 4), (x = -1);
Output: [1, 2, 3, 4];
```

#### ✅ Test Case 3:

```js
Input: (arr = [1, 2, 3, 4, 5]), (k = 4), (x = 10);
Output: [2, 3, 4, 5];
```

---

### 💡 Intuition

We want to find the **k elements** with the **smallest absolute difference** from `x`.

**Approach 1 (Efficient):**
Use **Binary Search + Two Pointers** to find the best window of size `k`.

**Approach 2 (Min Heap):**
Use a Min Heap to store `(abs(arr[i] - x), arr[i])`, keep `k` closest.

---

### 🧑‍💻 JavaScript Code (Binary Search Approach — Optimal)

```js
function findClosestElements(arr, k, x) {
  let left = 0;
  let right = arr.length - k;

  while (left < right) {
    const mid = Math.floor((left + right) / 2);

    // Compare distances from x
    if (x - arr[mid] > arr[mid + k] - x) {
      left = mid + 1;
    } else {
      right = mid;
    }
  }

  return arr.slice(left, left + k);
}
```

---

### ✅ Sample Usage

```js
console.log(findClosestElements([1, 2, 3, 4, 5], 4, 3)); // [1, 2, 3, 4]
console.log(findClosestElements([1, 2, 3, 4, 5], 4, -1)); // [1, 2, 3, 4]
```

---

### 🔄 Dry Run

```js
Input: arr = [1, 2, 3, 4, 5], k = 4, x = 3
Window size = 4, search window start index

Binary search between index 0 and 1
- mid = 0 → compare x-arr[mid] vs arr[mid+k]-x:
  3-1 = 2, 5-3 = 2 → move right = mid = 0
- exit → return arr[0 to 3] = [1, 2, 3, 4]
```

---

### ⏱️ Time & Space Complexity

| Operation     | Complexity    |
| ------------- | ------------- |
| Binary Search | O(log(n - k)) |
| Final slice   | O(k)          |
| Space         | O(1)          |

---

### 🧑‍💻 Min Heap Approach (Alternative, Less Efficient)

Use a **Min Heap** to get the `k`closest elements to`x` (based on absolute difference).
The heap will store entries as:

```js
[diff, value];
```

We'll use a custom **Min Heap class**, or you can use a **priority queue** from a library like `heapify` or `collections`. For now, let's write a **vanilla Min Heap version**.

---

### ✅ Min Heap Version Using JS Class

```js
class MinHeap {
  constructor() {
    this.heap = [];
  }

  insert(diff, val) {
    this.heap.push([diff, val]);
    this._heapifyUp();
  }

  extractMin() {
    if (this.heap.length === 1) return this.heap.pop();
    const min = this.heap[0];
    this.heap[0] = this.heap.pop();
    this._heapifyDown();
    return min;
  }

  _heapifyUp() {
    let i = this.heap.length - 1;
    while (i > 0) {
      const parent = Math.floor((i - 1) / 2);
      if (this._compare(i, parent) >= 0) break;
      this._swap(i, parent);
      i = parent;
    }
  }

  _heapifyDown() {
    let i = 0;
    const n = this.heap.length;

    while (true) {
      const left = 2 * i + 1;
      const right = 2 * i + 2;
      let smallest = i;

      if (left < n && this._compare(left, smallest) < 0) smallest = left;
      if (right < n && this._compare(right, smallest) < 0) smallest = right;

      if (smallest === i) break;
      this._swap(i, smallest);
      i = smallest;
    }
  }

  _compare(i, j) {
    const [diffA, valA] = this.heap[i];
    const [diffB, valB] = this.heap[j];
    if (diffA !== diffB) return diffA - diffB;
    return valA - valB;
  }

  _swap(i, j) {
    [this.heap[i], this.heap[j]] = [this.heap[j], this.heap[i]];
  }

  size() {
    return this.heap.length;
  }
}
```

---

### ✅ Modified Function with Real Min Heap

```js
function findClosestElementsHeap(arr, k, x) {
  const heap = new MinHeap();

  for (let num of arr) {
    heap.insert(Math.abs(num - x), num);
  }

  const result = [];
  while (k-- > 0 && heap.size() > 0) {
    result.push(heap.extractMin()[1]); // get the value
  }

  return result.sort((a, b) => a - b); // sort the result as required
}
```

---

## ✅ Usage

```js
console.log(findClosestElementsHeap([1, 2, 3, 4, 5], 4, 3)); // [1, 2, 3, 4]
console.log(findClosestElementsHeap([1, 2, 3, 4, 5], 4, -1)); // [1, 2, 3, 4]
console.log(findClosestElementsHeap([10, 15, 7, 3], 2, 9)); // [10, 7]
```

---

### ⏱️ Time Complexity

| Step                  | Complexity |
| --------------------- | ---------- |
| Insert all `n` values | O(n log n) |
| Extract `k` values    | O(k log n) |
| Final sort            | O(k log k) |
| **Total**             | O(n log n) |

---

### ✅ Summary

| Strategy      | Description                            |
| ------------- | -------------------------------------- |
| Binary Search | Fastest and optimal (`O(log n + k)`)   |
| Min Heap      | Simpler to implement, but `O(n log n)` |
| Sorted Result | Always return result in sorted order   |

---

## ✅ **6. Top K Frequent Elements**

### 📘 Problem Statement

Given an integer array `nums` and an integer `k`, return the **k most frequent elements**.

You may return the answer in **any order**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (nums = [1, 1, 1, 2, 2, 3]), (k = 2);
Output: [1, 2]; // 1 appears 3 times, 2 appears 2 times
```

#### ✅ Test Case 2:

```js
Input: (nums = [1]), (k = 1);
Output: [1];
```

---

### 💡 Intuition

1. Count the frequency of each element using a hashmap.
2. Use a **Min Heap** of size `k` to store the top `k` frequent elements.
3. At the end, return the elements from the heap.

---

### 🧑‍💻 JavaScript Code (Using Min Heap)

```js
class MinHeap {
  constructor() {
    this.heap = [];
  }

  insert(freq, num) {
    this.heap.push([freq, num]);
    this._heapifyUp();
  }

  extractMin() {
    if (this.heap.length === 1) return this.heap.pop();
    const min = this.heap[0];
    this.heap[0] = this.heap.pop();
    this._heapifyDown();
    return min;
  }

  _heapifyUp() {
    let i = this.heap.length - 1;
    while (i > 0) {
      let parent = Math.floor((i - 1) / 2);
      if (this.heap[parent][0] <= this.heap[i][0]) break;
      [this.heap[parent], this.heap[i]] = [this.heap[i], this.heap[parent]];
      i = parent;
    }
  }

  _heapifyDown() {
    let i = 0;
    const n = this.heap.length;
    while (true) {
      let left = 2 * i + 1;
      let right = 2 * i + 2;
      let smallest = i;

      if (left < n && this.heap[left][0] < this.heap[smallest][0]) {
        smallest = left;
      }
      if (right < n && this.heap[right][0] < this.heap[smallest][0]) {
        smallest = right;
      }

      if (smallest === i) break;
      [this.heap[i], this.heap[smallest]] = [this.heap[smallest], this.heap[i]];
      i = smallest;
    }
  }

  peek() {
    return this.heap[0];
  }

  size() {
    return this.heap.length;
  }
}
```

---

### ✅ Main Function

```js
function topKFrequent(nums, k) {
  const freqMap = new Map();

  // Count frequency
  for (let num of nums) {
    freqMap.set(num, (freqMap.get(num) || 0) + 1);
  }

  const heap = new MinHeap();

  for (let [num, freq] of freqMap.entries()) {
    heap.insert(freq, num);
    if (heap.size() > k) {
      heap.extractMin();
    }
  }

  // Extract top-k elements
  const result = [];
  while (heap.size()) {
    result.push(heap.extractMin()[1]);
  }

  return result;
}
```

---

### ✅ Sample Usage

```js
console.log(topKFrequent([1, 1, 1, 2, 2, 3], 2)); // [1, 2]
console.log(topKFrequent([1], 1)); // [1]
```

---

### ⏱️ Time & Space Complexity

| Step               | Complexity |
| ------------------ | ---------- |
| Frequency Count    | O(n)       |
| Heap Operations    | O(n log k) |
| Space (map + heap) | O(n + k)   |

✅ Much more efficient than sorting the whole array by frequency (`O(n log n)`).

---

### 📌 Summary

| Step            | Description                       |
| --------------- | --------------------------------- |
| Count Frequency | Hash Map                          |
| Maintain Top K  | Min Heap of size `k`              |
| Output          | Elements with highest frequencies |

---

## ✅ **7. Maximum Number of Events That Can Be Attended**

### 📘 Problem Statement

You are given a 2D array `events` where each `events[i] = [startDayᵢ, endDayᵢ]`.

- You can attend **at most one event per day**.
- An event `i` can be attended **on any day `d` such that startDayᵢ ≤ d ≤ endDayᵢ\`.**

Return the **maximum number of events you can attend**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: events = [
  [1, 2],
  [2, 3],
  [3, 4],
];
Output: 3; // Attend day 1, 2, and 3
```

#### ✅ Test Case 2:

```js
Input: events = [
  [1, 2],
  [2, 3],
  [3, 4],
  [1, 2],
];
Output: 4;
```

#### ✅ Test Case 3:

```js
Input: events = [
  [1, 4],
  [4, 4],
  [2, 2],
  [3, 4],
  [1, 1],
];
Output: 4;
```

---

### 💡 Intuition

This is a **Greedy Scheduling Problem**:

- Always attend the event that ends **earliest** to leave room for more future events.
- Use a **Min Heap** to keep track of the ending days of active events.

---

### 🧱 MinHeap Class

```js
class MinHeap {
  constructor() {
    this.heap = [];
  }

  insert(val) {
    this.heap.push(val);
    this._heapifyUp();
  }

  extractMin() {
    if (this.heap.length === 1) return this.heap.pop();
    const min = this.heap[0];
    this.heap[0] = this.heap.pop();
    this._heapifyDown();
    return min;
  }

  peek() {
    return this.heap[0];
  }

  size() {
    return this.heap.length;
  }

  _heapifyUp() {
    let i = this.heap.length - 1;
    while (i > 0) {
      let parent = Math.floor((i - 1) / 2);
      if (this.heap[parent] <= this.heap[i]) break;
      [this.heap[parent], this.heap[i]] = [this.heap[i], this.heap[parent]];
      i = parent;
    }
  }

  _heapifyDown() {
    let i = 0;
    const n = this.heap.length;
    while (true) {
      let left = 2 * i + 1;
      let right = 2 * i + 2;
      let smallest = i;

      if (left < n && this.heap[left] < this.heap[smallest]) smallest = left;
      if (right < n && this.heap[right] < this.heap[smallest]) smallest = right;

      if (smallest === i) break;
      [this.heap[i], this.heap[smallest]] = [this.heap[smallest], this.heap[i]];
      i = smallest;
    }
  }
}
```

---

### ✅ Main Function

```js
function maxEvents(events) {
  events.sort((a, b) => a[0] - b[0]); // Sort by start day
  const heap = new MinHeap();
  let i = 0;
  let res = 0;
  const n = events.length;
  const lastDay = Math.max(...events.map((e) => e[1]));

  for (let day = 1; day <= lastDay; day++) {
    // Add all events that start today
    while (i < n && events[i][0] === day) {
      heap.insert(events[i][1]);
      i++;
    }

    // Remove all events that ended before today
    while (heap.size() && heap.peek() < day) {
      heap.extractMin();
    }

    // Attend the event that ends earliest
    if (heap.size()) {
      heap.extractMin();
      res++;
    }
  }

  return res;
}
```

---

### ✅ Sample Usage

```js
console.log(
  maxEvents([
    [1, 2],
    [2, 3],
    [3, 4],
  ])
); // Output: 3
console.log(
  maxEvents([
    [1, 2],
    [2, 3],
    [3, 4],
    [1, 2],
  ])
); // Output: 4
console.log(
  maxEvents([
    [1, 4],
    [4, 4],
    [2, 2],
    [3, 4],
    [1, 1],
  ])
); // Output: 4
```

---

### ⏱️ Time & Space Complexity

| Step                             | Complexity |
| -------------------------------- | ---------- |
| Sorting Events                   | O(n log n) |
| Heap Operations (insert/extract) | O(n log n) |
| Space (Heap + Sort)              | O(n)       |

---

### 📌 Summary

| Step             | Description                                |
| ---------------- | ------------------------------------------ |
| Sort             | Events by start day                        |
| MinHeap          | Tracks active events, sorted by end day    |
| Greedy Selection | Always attend the event that ends earliest |

---

## ✅ **8. Meeting Rooms II**

> "Find the **minimum number of conference rooms required** to hold all meetings without conflicts."

---

### 📘 Problem Statement

Given an array of meeting time intervals `intervals` where:

- `intervals[i] = [startᵢ, endᵢ]`
- Each meeting has a start and end time

Return the **minimum number of meeting rooms** required so that **no meetings overlap** in a room.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: [
  [0, 30],
  [5, 10],
  [15, 20],
];
Output: 2; // One meeting from 0–30, overlaps with [5,10] and [15,20]
```

#### ✅ Test Case 2:

```js
Input: [
  [7, 10],
  [2, 4],
];
Output: 1; // No overlap
```

---

### 💡 Intuition

To minimize the number of rooms:

- Sort all meetings by **start time**.
- Use a **min-heap to track current meeting end times**.
- At each new meeting:

  - If it starts **after or at** the earliest ending meeting ⇒ reuse room (pop from heap).
  - Otherwise, allocate a new room (push into heap).

- The **size of the heap** at any time represents the **number of rooms in use**.

---

### 🧱 MinHeap Class

```js
class MinHeap {
  constructor() {
    this.heap = [];
  }

  insert(val) {
    this.heap.push(val);
    this._bubbleUp();
  }

  extractMin() {
    if (this.heap.length === 1) return this.heap.pop();
    const min = this.heap[0];
    this.heap[0] = this.heap.pop();
    this._bubbleDown();
    return min;
  }

  peek() {
    return this.heap[0];
  }

  size() {
    return this.heap.length;
  }

  _bubbleUp() {
    let i = this.heap.length - 1;
    while (i > 0) {
      let parent = Math.floor((i - 1) / 2);
      if (this.heap[parent] <= this.heap[i]) break;
      [this.heap[parent], this.heap[i]] = [this.heap[i], this.heap[parent]];
      i = parent;
    }
  }

  _bubbleDown() {
    let i = 0,
      n = this.heap.length;
    while (true) {
      let left = 2 * i + 1;
      let right = 2 * i + 2;
      let smallest = i;

      if (left < n && this.heap[left] < this.heap[smallest]) smallest = left;
      if (right < n && this.heap[right] < this.heap[smallest]) smallest = right;
      if (smallest === i) break;

      [this.heap[i], this.heap[smallest]] = [this.heap[smallest], this.heap[i]];
      i = smallest;
    }
  }
}
```

---

### ✅ Main Function: `minMeetingRooms`

```js
function minMeetingRooms(intervals) {
  if (!intervals.length) return 0;

  // Step 1: Sort meetings by start time
  intervals.sort((a, b) => a[0] - b[0]);

  const heap = new MinHeap();
  heap.insert(intervals[0][1]); // First meeting's end time

  for (let i = 1; i < intervals.length; i++) {
    let currStart = intervals[i][0];
    let currEnd = intervals[i][1];

    // Step 2: If room is free (meeting has ended)
    if (currStart >= heap.peek()) {
      heap.extractMin(); // reuse room
    }

    // Step 3: Allocate (or reuse) room
    heap.insert(currEnd);
  }

  return heap.size(); // Number of rooms in use
}
```

---

### ✅ Sample Usage

```js
console.log(
  minMeetingRooms([
    [0, 30],
    [5, 10],
    [15, 20],
  ])
); // Output: 2
console.log(
  minMeetingRooms([
    [7, 10],
    [2, 4],
  ])
); // Output: 1
console.log(
  minMeetingRooms([
    [1, 5],
    [2, 6],
    [3, 7],
  ])
); // Output: 3
```

---

### ⏱️ Time & Space Complexity

| Step                | Complexity |
| ------------------- | ---------- |
| Sorting             | O(n log n) |
| Heap operations     | O(n log n) |
| Space (heap + sort) | O(n)       |

---

### 📌 Summary

| Step       | Description                             |
| ---------- | --------------------------------------- |
| Sort       | Meetings by start time                  |
| Min Heap   | Track current meeting end times         |
| Reuse Room | If current start ≥ earliest end in heap |
| Result     | Heap size = Min number of rooms needed  |

---

## ✅ **9. Minimum Number of Platforms Required**

### 📘 Problem Statement

You're given:

- An array of **arrival times**
- An array of **departure times**

Each pair represents a train's schedule. You need to find the **minimum number of platforms** needed so that **no train waits**.

---

### 🧪 Example

```js
Arrival: [900, 940, 950, 1100, 1500, 1800];
Departure: [910, 1200, 1120, 1130, 1900, 2000];

Output: 3;
```

Explanation:

- At time `950`, three trains are at the station: \[900–910], \[940–1200], \[950–1120]
- Hence, 3 platforms are needed at peak.

---

### Event-Based Sorting Approach

### 💡 Intuition

1. Treat all arrival and departure times as **events**:

   - Arrival → `+1` platform needed
   - Departure → `-1` platform freed

2. Sort all events by time.

   - If two events have the same time:

     - **Departure comes before arrival**, to **free** platform before requiring a new one.

3. Traverse events, maintaining the current count of platforms in use.

---

### ✅ Implementation

```js
function minPlatforms(arr, dep) {
  const events = [];

  // Create event tuples: [time, type]
  for (let i = 0; i < arr.length; i++) {
    events.push([arr[i], "arr"]);
    events.push([dep[i], "dep"]);
  }

  // Sort by time. For same time, dep before arr
  events.sort((a, b) => {
    if (a[0] === b[0]) {
      return a[1] === "dep" ? -1 : 1; // departure first
    }
    return a[0] - b[0];
  });

  let platforms = 0;
  let maxPlatforms = 0;

  for (let [time, type] of events) {
    if (type === "arr") {
      platforms++;
      maxPlatforms = Math.max(maxPlatforms, platforms);
    } else {
      platforms--;
    }
  }

  return maxPlatforms;
}
```

---

### ✅ Sample Usage

```js
const arr = [900, 940, 950, 1100, 1500, 1800];
const dep = [910, 1200, 1120, 1130, 1900, 2000];

console.log(minPlatforms(arr, dep)); // Output: 3
```

---

### 🔄 Sorted `events` list (for visualization)

For the above test case:

```js
events = [
  [900, "arr"],
  [910, "dep"],
  [940, "arr"],
  [950, "arr"],
  [1120, "dep"],
  [1130, "dep"],
  [1100, "arr"],
  [1200, "dep"],
  [1500, "arr"],
  [1800, "arr"],
  [1900, "dep"],
  [2000, "dep"],
];
```

(Sorted to handle dep before arr at same timestamp)

---

### ⏱️ Time & Space Complexity

| Step           | Complexity   |
| -------------- | ------------ |
| Event Creation | `O(n)`       |
| Sorting Events | `O(n log n)` |
| Traversal      | `O(n)`       |
| Space          | `O(n)`       |

---

### 📌 Summary

| Concept              | Explanation                         |
| -------------------- | ----------------------------------- |
| Event Points         | Create `[time, type]` for arr/dep   |
| Sorting Order        | Sort by time, dep before arr on tie |
| Sweep Line           | Simulate platform usage dynamically |
| Max Platforms Needed | Track max during the sweep          |

---
## ✅ **10. Frequency Sort Using Max Heap**

### 📘 Problem Statement

You're given an **array of elements** (can be numbers or characters). Your task is to return a list where elements are sorted by their **frequency in descending order**.

If two elements have the same frequency, order doesn't matter (unless otherwise specified).

---

### 🧪 Example

```js
Input: [1, 1, 1, 2, 2, 3];
Output: [1, 1, 1, 2, 2, 3];

Input: ["a", "b", "a", "c", "b", "a"];
Output: ["a", "a", "a", "b", "b", "c"];
```

---

### 💡 Intuition

1. First, count the frequency of each element using a **map**.
2. Use a **Max Heap (priority queue)** where the element with **highest frequency** is on top.
3. Extract elements from the heap and build the result by repeating each element its frequency number of times.

---

### ✅ Implementation

```js
class MaxHeap {
  constructor(compareFn) {
    this.data = [];
    this.compare = compareFn;
  }

  size() {
    return this.data.length;
  }

  isEmpty() {
    return this.size() === 0;
  }

  insert(val) {
    this.data.push(val);
    this.heapifyUp();
  }

  extractMax() {
    if (this.size() === 0) return null;
    if (this.size() === 1) return this.data.pop();

    const top = this.data[0];
    this.data[0] = this.data.pop();
    this.heapifyDown();
    return top;
  }

  swap(i, j) {
    [this.data[i], this.data[j]] = [this.data[j], this.data[i]];
  }

  heapifyUp() {
    let index = this.size() - 1;
    while (
      index > 0 &&
      this.compare(this.data[index], this.data[this.parent(index)]) > 0
    ) {
      this.swap(index, this.parent(index));
      index = this.parent(index);
    }
  }

  heapifyDown() {
    let index = 0;
    while (this.left(index) < this.size()) {
      let largest = this.left(index);
      if (
        this.right(index) < this.size() &&
        this.compare(this.data[this.right(index)], this.data[largest]) > 0
      ) {
        largest = this.right(index);
      }
      if (this.compare(this.data[index], this.data[largest]) >= 0) break;
      this.swap(index, largest);
      index = largest;
    }
  }

  parent(i) {
    return Math.floor((i - 1) / 2);
  }

  left(i) {
    return 2 * i + 1;
  }

  right(i) {
    return 2 * i + 2;
  }
}
```

---

### 🧩 Frequency Sort Function

```js
function frequencySort(arr) {
  const freqMap = new Map();

  for (let num of arr) {
    freqMap.set(num, (freqMap.get(num) || 0) + 1);
  }

  const heap = new MaxHeap((a, b) => a[1] - b[1]); // Compare by frequency

  for (let [val, freq] of freqMap.entries()) {
    heap.insert([val, freq]);
  }

  const result = [];

  while (!heap.isEmpty()) {
    const [val, freq] = heap.extractMax();
    for (let i = 0; i < freq; i++) {
      result.push(val);
    }
  }

  return result;
}
```

---

### ✅ Sample Usage

```js
console.log(frequencySort([1, 1, 1, 2, 2, 3])); 
// Output: [1, 1, 1, 2, 2, 3]

console.log(frequencySort(["a", "b", "a", "c", "b", "a"])); 
// Output: ["a", "a", "a", "b", "b", "c"]
```

---

### 🔄 Internal `freqMap` (for visualization)

For input: `[1, 1, 1, 2, 2, 3]`

```js
freqMap = {
  1: 3,
  2: 2,
  3: 1
}
```

Heap contains entries: `[1, 3]`, `[2, 2]`, `[3, 1]`
MaxHeap ensures highest frequency comes out first.

---

### ⏱️ Time & Space Complexity

| Step                 | Complexity   |
| -------------------- | ------------ |
| Frequency Counting   | `O(n)`       |
| Heap Insertions      | `O(n log n)` |
| Heap Extraction      | `O(n log n)` |
| Result Construction  | `O(n)`       |
| **Total Time**       | `O(n log n)` |
| **Space Complexity** | `O(n)`       |

---

### 📌 Summary

| Concept             | Explanation                          |
| ------------------- | ------------------------------------ |
| Frequency Map       | Track how often each element appears |
| Max Heap            | Highest freq item is always on top   |
| Comparator Function | Used to customize heap behavior      |
| Result Construction | Rebuild array by frequency order     |

---

## ✅ **11. K Closest Points to Origin**

### 📘 Problem Statement

You're given an array of points in 2D space: `[[x1, y1], [x2, y2], ...]` and an integer `k`.
Your task is to return the **`k` points closest to the origin (0, 0)\`**.

---

### 🧪 Example

```js
Input: points = [[1,3],[-2,2],[5,8],[0,1]], k = 2  
Output: [[-2,2],[0,1]]
```

Explanation:

* Distances: (1,3) → √10, (-2,2) → √8, (5,8) → √89, (0,1) → √1
* Closest two are: (0,1) and (-2,2)

---

### 💡 Intuition

1. The closer a point is to origin, the smaller its **Euclidean distance**:

   $$
   \text{distance} = \sqrt{x^2 + y^2}
   $$

   ✅ We can skip `Math.sqrt()` — since it preserves order.

2. Use a **Max Heap** of size `k`:

   * Push points with their distance.
   * If heap size > `k`, remove the **farthest** point (max distance).
   * At the end, the heap will contain the `k` closest points.

---

### ✅ MaxHeap Implementation

```js
class MaxHeap {
  constructor(compare) {
    this.data = [];
    this.compare = compare;
  }

  insert(val) {
    this.data.push(val);
    this.heapifyUp();
  }

  extractMax() {
    if (this.data.length === 0) return null;
    if (this.data.length === 1) return this.data.pop();
    const max = this.data[0];
    this.data[0] = this.data.pop();
    this.heapifyDown();
    return max;
  }

  heapifyUp() {
    let i = this.data.length - 1;
    while (i > 0) {
      let p = Math.floor((i - 1) / 2);
      if (this.compare(this.data[i], this.data[p]) <= 0) break;
      [this.data[i], this.data[p]] = [this.data[p], this.data[i]];
      i = p;
    }
  }

  heapifyDown() {
    let i = 0;
    const n = this.data.length;
    while (2 * i + 1 < n) {
      let left = 2 * i + 1;
      let right = 2 * i + 2;
      let largest = i;

      if (left < n && this.compare(this.data[left], this.data[largest]) > 0)
        largest = left;
      if (right < n && this.compare(this.data[right], this.data[largest]) > 0)
        largest = right;

      if (largest === i) break;

      [this.data[i], this.data[largest]] = [this.data[largest], this.data[i]];
      i = largest;
    }
  }

  size() {
    return this.data.length;
  }

  isEmpty() {
    return this.data.length === 0;
  }

  peek() {
    return this.data[0];
  }
}
```

---

### ✅ Main Function

```js
function kClosest(points, k) {
  const dist = ([x, y]) => x * x + y * y;

  const heap = new MaxHeap((a, b) => a[0] - b[0]); // compare by distance

  for (let point of points) {
    const d = dist(point);
    heap.insert([d, point]);

    if (heap.size() > k) {
      heap.extractMax(); // remove farthest
    }
  }

  return heap.data.map(entry => entry[1]);
}
```

---

### ✅ Sample Usage

```js
console.log(kClosest([[1, 3], [-2, 2], [5, 8], [0, 1]], 2));
// Output: [[-2,2],[0,1]]
```

---

### 🔄 Heap Trace (visual)

For input: `[[1,3],[-2,2],[5,8],[0,1]], k=2`

Distances (squared):

```
[10, [1,3]],
[8, [-2,2]],
[89, [5,8]],
[1, [0,1]]
```

Final heap contains:
→ \[\[8, \[-2,2]], \[1, \[0,1]]] (k closest)

---

### ⏱️ Time & Space Complexity

| Step          | Complexity   |
| ------------- | ------------ |
| Distance Calc | `O(n)`       |
| Heap Insert   | `O(log k)`   |
| Total Time    | `O(n log k)` |
| Space         | `O(k)`       |

---

### 📌 Summary

| Concept              | Explanation                      |
| -------------------- | -------------------------------- |
| Distance Function    | Use x² + y² to compare distances |
| Max Heap             | Keeps farthest point at top      |
| Fixed Heap Size      | Only store top k closest points  |
| Efficient Extraction | Heap ensures O(log k) ops        |

---
## ✅ **12. Connect Ropes to Minimize Cost**

### 📘 Problem Statement

You're given an array of rope lengths. You need to connect all ropes into **one single rope**.
Each time you connect two ropes of length `a` and `b`, the cost is `a + b`.

👉 Return the **minimum total cost** to connect all ropes.

---

### 🧪 Example

```js
Input: [4, 3, 2, 6]
Output: 29
```

**Explanation:**

1. Connect 2 + 3 = 5 (cost: 5) → heap: \[4, 5, 6]
2. Connect 4 + 5 = 9 (cost: 9) → heap: \[6, 9]
3. Connect 6 + 9 = 15 (cost: 15) → heap: \[15]
4. Total cost: 5 + 9 + 15 = **29**

---

### 💡 Intuition

This is a **greedy** problem.

* Always connect the **two smallest** ropes first (to minimize the current cost).
* Repeat until only one rope remains.
* Use a **Min Heap** to efficiently get the smallest two ropes at each step.

---

### ✅ MinHeap Class

```js
class MinHeap {
  constructor(compare) {
    this.data = [];
    this.compare = compare || ((a, b) => a - b);
  }

  insert(val) {
    this.data.push(val);
    this.heapifyUp();
  }

  extractMin() {
    if (this.data.length === 0) return null;
    if (this.data.length === 1) return this.data.pop();
    const min = this.data[0];
    this.data[0] = this.data.pop();
    this.heapifyDown();
    return min;
  }

  heapifyUp() {
    let i = this.data.length - 1;
    while (i > 0) {
      const p = Math.floor((i - 1) / 2);
      if (this.compare(this.data[i], this.data[p]) >= 0) break;
      [this.data[i], this.data[p]] = [this.data[p], this.data[i]];
      i = p;
    }
  }

  heapifyDown() {
    let i = 0;
    const n = this.data.length;
    while (2 * i + 1 < n) {
      let left = 2 * i + 1;
      let right = 2 * i + 2;
      let smallest = i;

      if (left < n && this.compare(this.data[left], this.data[smallest]) < 0)
        smallest = left;
      if (right < n && this.compare(this.data[right], this.data[smallest]) < 0)
        smallest = right;

      if (smallest === i) break;
      [this.data[i], this.data[smallest]] = [this.data[smallest], this.data[i]];
      i = smallest;
    }
  }

  size() {
    return this.data.length;
  }

  isEmpty() {
    return this.size() === 0;
  }
}
```

---

### ✅ Main Function

```js
function connectRopes(ropes) {
  const heap = new MinHeap();

  // Initialize heap with all ropes
  for (let rope of ropes) {
    heap.insert(rope);
  }

  let totalCost = 0;

  while (heap.size() > 1) {
    const first = heap.extractMin();
    const second = heap.extractMin();

    const cost = first + second;
    totalCost += cost;

    heap.insert(cost); // Insert combined rope back
  }

  return totalCost;
}
```

---

### ✅ Sample Usage

```js
console.log(connectRopes([4, 3, 2, 6])); // Output: 29
console.log(connectRopes([1, 2, 5, 10, 35, 89])); // Output: 224
```

---

### 🔄 Heap Trace (visual)

For input `[4, 3, 2, 6]`:

1. Heap → \[2, 3, 4, 6]
2. Connect 2 + 3 = 5 → Insert 5 → \[4, 5, 6]
3. Connect 4 + 5 = 9 → Insert 9 → \[6, 9]
4. Connect 6 + 9 = 15 → Insert 15 → \[15]
   → Total cost: 5 + 9 + 15 = **29**

---

### ⏱️ Time & Space Complexity

| Step       | Complexity   |
| ---------- | ------------ |
| Heap Build | `O(n)`       |
| N-1 Merges | `O(n log n)` |
| Space      | `O(n)`       |

---

### 📌 Summary

| Concept              | Explanation                         |
| -------------------- | ----------------------------------- |
| Greedy Strategy      | Always merge smallest ropes first   |
| Min Heap             | Efficient way to get 2 minimums     |
| Cost Tracking        | Sum of all intermediate merge costs |
| Optimal Substructure | Locally optimal → globally optimal  |

---
## ✅ **13. Sum of Two Elements from K1 and K2 Smallest Elements**

### 📘 Problem Statement

Given an array of integers and two integers `k1` and `k2`, find the **sum of all elements that lie between the `k1`-th and `k2`-th smallest elements** in the array.

> ⚠️ Elements are 1-indexed (i.e., the smallest is 1st, next is 2nd...).

---

### 🧪 Example

```js
Input: arr = [1, 3, 12, 5, 15, 11], k1 = 3, k2 = 6  
Output: 23
```

**Explanation:**

* Sorted: \[1, 3, 5, 11, 12, 15]
* 3rd smallest = 5
* 6th smallest = 15
* Elements in between: **\[11, 12]**
* Sum = 11 + 12 = **23**

---

### 💡 Intuition

* We only care about the elements that are **strictly between** the `k1`-th and `k2`-th smallest.
* Instead of sorting the full array (`O(n log n)`), we can use a **Min Heap** (`O(n + k log n)`).

---

### ✅ Implementation

```js
class MinHeap {
  constructor(compare) {
    this.data = [];
    this.compare = compare || ((a, b) => a - b);
  }

  insert(val) {
    this.data.push(val);
    this.heapifyUp();
  }

  extractMin() {
    if (this.data.length === 0) return null;
    if (this.data.length === 1) return this.data.pop();

    const min = this.data[0];
    this.data[0] = this.data.pop();
    this.heapifyDown();
    return min;
  }

  heapifyUp() {
    let i = this.data.length - 1;
    while (i > 0) {
      const p = Math.floor((i - 1) / 2);
      if (this.compare(this.data[i], this.data[p]) >= 0) break;
      [this.data[i], this.data[p]] = [this.data[p], this.data[i]];
      i = p;
    }
  }

  heapifyDown() {
    let i = 0;
    const n = this.data.length;
    while (2 * i + 1 < n) {
      let left = 2 * i + 1;
      let right = 2 * i + 2;
      let smallest = i;

      if (left < n && this.compare(this.data[left], this.data[smallest]) < 0)
        smallest = left;
      if (right < n && this.compare(this.data[right], this.data[smallest]) < 0)
        smallest = right;

      if (smallest === i) break;
      [this.data[i], this.data[smallest]] = [this.data[smallest], this.data[i]];
      i = smallest;
    }
  }

  size() {
    return this.data.length;
  }

  isEmpty() {
    return this.size() === 0;
  }
}
```

---

### ✅ Main Function

```js
function sumBetweenK1K2Smallest(arr, k1, k2) {
  const heap = new MinHeap();

  for (let num of arr) {
    heap.insert(num);
  }

  // Pop k1 smallest elements
  for (let i = 0; i < k1; i++) heap.extractMin();

  let sum = 0;

  // Sum next (k2 - k1 - 1) elements
  for (let i = 0; i < k2 - k1 - 1; i++) {
    if (!heap.isEmpty()) sum += heap.extractMin();
  }

  return sum;
}
```

---

### ✅ Sample Usage

```js
console.log(sumBetweenK1K2Smallest([1, 3, 12, 5, 15, 11], 3, 6)); // Output: 23
console.log(sumBetweenK1K2Smallest([20, 8, 22, 4, 12, 10, 14], 3, 6)); // Output: 26
```

---

### 🔄 Heap Trace (Visual)

For input: `[1, 3, 12, 5, 15, 11]`, k1 = 3, k2 = 6

1. Heap built → \[1, 3, 5, 11, 12, 15]
2. Remove first 3: 1, 3, 5
3. Next two: **11 + 12 = 23**

---

### ⏱️ Time & Space Complexity

| Step         | Complexity         |
| ------------ | ------------------ |
| Build Heap   | `O(n)`             |
| k1 Pops      | `O(k1 log n)`      |
| k2−k1−1 Pops | `O((k2-k1) log n)` |
| Total Time   | `O(n + k log n)`   |
| Space        | `O(n)`             |

---

### 📌 Summary

| Concept           | Explanation                            |
| ----------------- | -------------------------------------- |
| Min Heap          | Efficient way to get smallest elements |
| Skip k1 smallest  | Discard first k1 elements              |
| Sum middle values | Only add values between k1 and k2      |
| Avoid Full Sort   | Faster than full sorting for large `n` |

---
