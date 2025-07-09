# 🧠 **Time and Space Complexity**

## 📘 **What is Time and Space Complexity?**

- **Time Complexity** measures how **execution time** grows with **input size**.
- **Space Complexity** measures how much **extra memory** (excluding input) an algorithm needs as input size grows.

---

## 📈 **Time Complexity**

### 📌 **How to Analyze Time Complexity?**

#### 💡 Rule 1: Count Loops

```js
for (let i = 0; i < n; i++) {
  // O(1) operation
}
// ➤ O(n)
```

#### 💡 Rule 2: Nested Loops Multiply

```js
for (let i = 0; i < n; i++) {
  for (let j = 0; j < n; j++) {
    // O(1)
  }
}
// ➤ O(n²)
```

#### 💡 Rule 3: Consecutive loops ADD

```js
for (let i = 0; i < n; i++) {} // O(n)
for (let j = 0; j < m; j++) {} // O(m)
// ➤ O(n + m)
```

#### 💡 Rule 4: Recursive Calls

```js
function fib(n) {
  if (n <= 1) return 1;
  return fib(n - 1) + fib(n - 2);
}
// ➤ O(2^n)
```

Use **recursion trees** or **Master Theorem** for more complex ones.

---

## 🧮 **Space Complexity**

### ✅ What It Measures:

- **Extra memory** used by the algorithm (not counting input).
- Includes **variables, data structures, recursive call stacks**.

---

### 📌 **How to Analyze Space Complexity?**

#### ✅ Variables

```js
let a = 10; // O(1)
let arr = new Array(n); // O(n)
```

#### ✅ Recursive Stack

```js
function binarySearch(start, end) {
  if (start > end) return;
  let mid = Math.floor((start + end) / 2);
  binarySearch(start, mid - 1);
  binarySearch(mid + 1, end);
}
// ➤ O(log n) stack space
```

---

### 👀 Space Complexity in Recursion

If a function calls itself `n` times and each call is independent:

- Stack builds up to depth `n`: O(n)

Example:

```js
function countdown(n) {
  if (n === 0) return;
  countdown(n - 1);
}
// ➤ O(n) space due to call stack
```

---

## 🛠️ Real Example Walkthrough

### 🧮 Example: Two Sum Problem

```js
function twoSum(nums, target) {
  let map = new Map(); // O(n) space

  for (let i = 0; i < nums.length; i++) {
    let complement = target - nums[i];
    if (map.has(complement)) {
      return [map.get(complement), i];
    }
    map.set(nums[i], i);
  }
}
```

- **Time Complexity**: O(n)
- **Space Complexity**: O(n)

Why?

- One pass through `n` elements = O(n)
- Map stores up to `n` elements = O(n)

---
