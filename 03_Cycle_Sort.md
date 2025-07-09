# 🔁 Cycle Sort – Full Theory

## 📘 What is Cycle Sort?

**Cycle Sort** is an **in-place, non-comparing sorting algorithm** that minimizes the number of write operations.

🔧 **Key Idea:**
Each element must be **placed at its correct position** in as few swaps as possible – ideally in **1 swap per element**.

---

## 💡 When is Cycle Sort used?

- When **writes/swaps are expensive** (e.g., EEPROM memory, flash memory).
- When you want **minimum number of memory writes**.
- Often used in **questions like:**

  - Sort an array where elements are in the range \[1, N]
  - Find missing/duplicate numbers (cyclic sort pattern)

---

## 🔍 Core Principles

### 🔄 Cycles in Array

If you trace where each element should go, it forms a **cycle**.
Cycle Sort goes through each cycle and places elements in the right spot with minimal writes.

### 🧠 Rule:

> At every index `i`, the correct element should be:
>
> - At index `i = arr[i] - 1` (for 1-based values)
> - Or `i = arr[i]` (if elements are 0 to n-1)

---

## ✅ Requirements

- Works **best** when elements are in range **\[0, N-1]** or **\[1, N]**.
- Elements should be **distinct** (basic version).

---

Sure! Here's the problem **"Cycle Sort"** explained in the exact structured format you're using — intuitive, visual, and with clean JavaScript code.

---

## **Cycle Sort**

### 🔍 Problem Statement

You are given an array `nums[]` of **`n` integers**, where:

- The array contains **distinct integers** from `1` to `n` (or `0` to `n-1` in some variations)
- Your task is to **sort the array in-place** using **Cycle Sort**, a space-optimized technique.

📌 Goal:  
Sort the array **in-place** using **O(n)** time and **O(1)** space.

---

### 🧪 Examples

#### Example 1:

```
Input:  [3, 1, 5, 4, 2]
Output: [1, 2, 3, 4, 5]
```

#### Example 2:

```
Input:  [5, 4, 3, 2, 1]
Output: [1, 2, 3, 4, 5]
```

#### Example 3 (0-based):

```
Input:  [4, 0, 2, 1, 3]
Output: [0, 1, 2, 3, 4]
```

---

### 🧠 Intuition

- If the element is at its **correct index**, skip.
- Else, **swap** it with the element at its **correct index**.
- Keep doing this until all elements are in place.

For **1-based values** → correct index = `num - 1`  
For **0-based values** → correct index = `num`

---

### 🧵 Dry Run

```text
Input: [3, 1, 5, 4, 2]
Index 0: 3 → correct index is 2 → swap(0,2)
        → [5, 1, 3, 4, 2]
Index 0: 5 → correct index is 4 → swap(0,4)
        → [2, 1, 3, 4, 5]
Index 0: 2 → correct index is 1 → swap(0,1)
        → [1, 2, 3, 4, 5]
Index 0: 1 → correct index is 0 → OK
Now array is sorted.
```

---

### 💻 JavaScript Code

```javascript
function cycleSort(nums) {
  let i = 0;
  while (i < nums.length) {
    const correctIndex = nums[i] - 1; // for 1-based values
    if (nums[i] !== nums[correctIndex]) {
      [nums[i], nums[correctIndex]] = [nums[correctIndex], nums[i]];
    } else {
      i++;
    }
  }
  return nums;
}
```

> ✅ For **0-based values**, change line:

```js
const correctIndex = nums[i]; // for 0-based values
```

---

#### ✅ Usage

```javascript
console.log(cycleSort([3, 1, 5, 4, 2])); // [1, 2, 3, 4, 5]
console.log(cycleSort([5, 4, 3, 2, 1])); // [1, 2, 3, 4, 5]
console.log(cycleSort([4, 0, 2, 1, 3])); // [0, 1, 2, 3, 4] ← (use 0-based version)
```

---

### ⏱ Time & Space Complexity

| Metric           | Value |
| ---------------- | ----- |
| Time Complexity  | O(n)  |
| Space Complexity | O(1)  |

---

### 📌 Summary

| Feature      | Description                                        |
| ------------ | -------------------------------------------------- |
| Input        | Array of size `n` with values `1 → n` or `0 → n-1` |
| Output       | Sorted array (in-place)                            |
| Constraints  | Distinct integers in a known range                 |
| Core Concept | Place each element at its correct index            |
| Use Cases    | In-place sorting with min swaps                    |

---
