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
