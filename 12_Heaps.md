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
