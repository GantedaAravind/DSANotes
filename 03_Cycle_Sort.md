# 🔁 Cycle Sort

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

# Varients

## **1. Missing Number (0 to n) using Cycle Sort**

### 🔍 Problem Statement

You're given an array `nums[]` containing **`n` distinct numbers** from the range `[0, n]` — i.e., **exactly one number is missing**.

Return the **missing number**.

📌 Constraints:

- Array has `n` elements, values from **0 to n**
- Exactly **one number is missing**
- Solve in **O(n)** time and **O(1)** space using **Cycle Sort**

---

### 🧪 Examples

#### Example 1:

```
Input:  [3, 0, 1]
Output: 2
```

#### Example 2:

```
Input:  [0, 1]
Output: 2
```

#### Example 3:

```
Input:  [9,6,4,2,3,5,7,0,1]
Output: 8
```

---

### 🧠 Intuition

We want to **place each number at its correct index**, where:

- Value `x` should be at index `x`
- But skip if the number is **`n`** (since index `n` is out of bounds)

Then:

- Traverse array: if `nums[i] !== i`, then `i` is the missing number
- If all match, missing number is `n`

---

### 🧵 Dry Run

```text
Input: [3, 0, 1]
Cycle sort:
- i = 0 → nums[0] = 3 → skip (3 == n)
- i = 1 → nums[1] = 0 → swap(1, 0) → [0, 3, 1]
- i = 1 → nums[1] = 3 → skip
- i = 2 → nums[2] = 1 → swap(2, 1) → [0, 1, 3]
Now scan:
- nums[0] = 0 ✓
- nums[1] = 1 ✓
- nums[2] = 3 ≠ 2 → return 2
```

---

### 💻 JavaScript Code

```javascript
function missingNumber(nums) {
  let i = 0;
  while (i < nums.length) {
    const correctIndex = nums[i];
    if (nums[i] < nums.length && nums[i] !== nums[correctIndex]) {
      [nums[i], nums[correctIndex]] = [nums[correctIndex], nums[i]];
    } else {
      i++;
    }
  }

  // Find the missing index
  for (let i = 0; i < nums.length; i++) {
    if (nums[i] !== i) return i;
  }

  return nums.length; // All matched, so n is missing
}
```

---

#### ✅ Usage

```javascript
console.log(missingNumber([3, 0, 1])); // Output: 2
console.log(missingNumber([0, 1])); // Output: 2
console.log(missingNumber([9, 6, 4, 2, 3, 5, 7, 0, 1])); // Output: 8
console.log(missingNumber([0])); // Output: 1
```

---

### ⏱ Time & Space Complexity

| Metric           | Value |
| ---------------- | ----- |
| Time Complexity  | O(n)  |
| Space Complexity | O(1)  |

---

### 📌 Summary

| Feature      | Description                                     |
| ------------ | ----------------------------------------------- |
| Input        | Array of `n` distinct numbers from `0 → n`      |
| Output       | The single missing number                       |
| Constraints  | No duplicates, values in range \[0, n]          |
| Core Concept | **Cyclic Sort**, skip value `n`                 |
| Use Cases    | Memory-limited systems, in-place array problems |

---

## **2. Find All Missing Numbers (from 1 to N)**

### 🔍 Problem Statement

You are given an **array `nums[]` of size N**, where:

- Numbers are in the range `[1, N]`
- Some numbers may **appear more than once**
- Some numbers are **missing**

Your task is to **return all missing numbers** in the array.

---

### 🧪 Examples

#### Example 1:

```
Input:  [4, 3, 2, 7, 8, 2, 3, 1]
Output: [5, 6]
```

#### Example 2:

```
Input:  [1, 1]
Output: [2]
```

#### Example 3:

```
Input:  [2, 2]
Output: [1]
```

---

### 🧠 Intuition

We want to place each number at its **correct index**:
For value `x`, its correct index is `x - 1`.

During cycle sort:

- If `nums[i] != nums[correctIndex]`, **swap**
- Duplicates will prevent some numbers from reaching their correct positions

After sorting:

- If `nums[i] !== i + 1` → then `(i + 1)` is **missing**

---

### 🧵 Dry Run

```text
Input: [4, 3, 2, 7, 8, 2, 3, 1]

Cycle sort places numbers in proper positions:
  → [1, 2, 3, 4, 3, 2, 7, 8]

Now scan:
  i=4 → nums[4]=3 ≠ 5 → 5 is missing
  i=5 → nums[5]=2 ≠ 6 → 6 is missing

Output: [5, 6]
```

---

### 💻 JavaScript Code

```javascript
function findDisappearedNumbers(nums) {
  let i = 0;
  while (i < nums.length) {
    const correctIndex = nums[i] - 1;
    if (nums[i] !== nums[correctIndex]) {
      [nums[i], nums[correctIndex]] = [nums[correctIndex], nums[i]];
    } else {
      i++;
    }
  }

  const result = [];
  for (let i = 0; i < nums.length; i++) {
    if (nums[i] !== i + 1) {
      result.push(i + 1);
    }
  }
  return result;
}
```

---

#### ✅ Usage

```javascript
console.log(findDisappearedNumbers([4, 3, 2, 7, 8, 2, 3, 1])); // [5, 6]
console.log(findDisappearedNumbers([1, 1])); // [2]
console.log(findDisappearedNumbers([2, 2])); // [1]
console.log(findDisappearedNumbers([1, 2, 3, 4, 5])); // []
```

---

### ⏱ Time & Space Complexity

| Metric           | Value                        |
| ---------------- | ---------------------------- |
| Time Complexity  | O(n)                         |
| Space Complexity | O(1) (ignoring output array) |

---

### 📌 Summary

| Feature      | Description                                                |
| ------------ | ---------------------------------------------------------- |
| Input        | Array of size `n` with values `1 → n`, duplicates possible |
| Output       | List of all **missing** numbers                            |
| Constraints  | No extra space allowed (except output)                     |
| Core Concept | **Cycle Sort** + Misplaced Detection                       |
| Use Cases    | Data validation, ID tracking, missing entries              |

---

## **3. Find the Duplicate Number**

### 🔍 Problem Statement

You're given an **array `nums[]` of size `n + 1`**, where:

- All elements are in the range **`1` to `n`**
- There is **exactly one duplicate** number, but it **may appear more than once**

Return the **duplicate number**, without modifying the array (if constraints require that), but here we will **solve it using Cycle Sort**, which **modifies the array**.

---

### 🧪 Examples

#### Example 1:

```
Input:  [1, 3, 4, 2, 2]
Output: 2
```

#### Example 2:

```
Input:  [3, 1, 3, 4, 2]
Output: 3
```

#### Example 3:

```
Input:  [2, 2, 2, 2, 2]
Output: 2
```

---

### 🧠 Intuition (Cycle Sort Approach)

We aim to place each number at its **correct index**:

- For value `x`, it should go to index `x - 1`

If while placing, we find that:

- `nums[i] == nums[correctIndex]` → **duplicate found**

This works because there are `n + 1` elements from `1 to n`, so **at least one must be repeated**.

---

### 🧵 Dry Run

```text
Input: [3, 1, 3, 4, 2]

Start i=0 → nums[0]=3 → correct index = 2
Swap nums[0] and nums[2] → [3, 1, 3, 4, 2] → same value → Duplicate = 3
```

---

### 💻 JavaScript Code

```javascript
function findDuplicate(nums) {
  let i = 0;
  while (i < nums.length) {
    const correctIndex = nums[i] - 1;

    // If current number is not at correct place
    if (nums[i] !== nums[correctIndex]) {
      [nums[i], nums[correctIndex]] = [nums[correctIndex], nums[i]];
    } else {
      if (i !== correctIndex) return nums[i]; // Duplicate found
      i++;
    }
  }

  return -1; // Shouldn't reach here if input is valid
}
```

---

#### ✅ Usage

```javascript
console.log(findDuplicate([1, 3, 4, 2, 2])); // Output: 2
console.log(findDuplicate([3, 1, 3, 4, 2])); // Output: 3
console.log(findDuplicate([2, 2, 2, 2, 2])); // Output: 2
```

---

### ⏱ Time & Space Complexity

| Metric           | Value |
| ---------------- | ----- |
| Time Complexity  | O(n)  |
| Space Complexity | O(1)  |

---

### 📌 Summary

| Feature      | Description                                         |
| ------------ | --------------------------------------------------- |
| Input        | Array of size `n+1` with values from `1` to `n`     |
| Output       | The **duplicate number**                            |
| Constraints  | Can modify array, exactly one duplicate             |
| Core Concept | **Cycle Sort** with index check for duplicates      |
| Use Cases    | Data validation, corruption detection, ID conflicts |

---

## **4. First Missing Positive**

### 🔍 Problem Statement

You are given an **unsorted integer array `nums[]`**.

Return the **smallest positive integer** that does **not** appear in the array.

📌 Requirements:

- Time Complexity: **O(n)**
- Space Complexity: **O(1)** (constant auxiliary space)

---

### 🧪 Examples

#### Example 1:

```
Input:  [1, 2, 0]
Output: 3
```

#### Example 2:

```
Input:  [3, 4, -1, 1]
Output: 2
```

#### Example 3:

```
Input:  [7, 8, 9, 11, 12]
Output: 1
```

---

### 🧠 Intuition

We want to **place each number `x` at index `x - 1`**, **only if**:

- `1 <= x <= n` (within bounds)
- Avoid infinite loops with duplicates

After rearranging:

- Scan through the array.
- First index `i` where `nums[i] != i + 1` → `i + 1` is the missing number

---

### 🧵 Dry Run

```text
Input: [3, 4, -1, 1]

After placing:
→ [1, -1, 3, 4]

Scan:
i = 0 → nums[0] = 1 ✓
i = 1 → nums[1] ≠ 2 → return 2
```

---

### 💻 JavaScript Code

```javascript
function firstMissingPositive(nums) {
  let n = nums.length;

  for (let i = 0; i < n; i++) {
    while (nums[i] > 0 && nums[i] <= n && nums[i] !== nums[nums[i] - 1]) {
      const correctIndex = nums[i] - 1;
      [nums[i], nums[correctIndex]] = [nums[correctIndex], nums[i]];
    }
  }

  for (let i = 0; i < n; i++) {
    if (nums[i] !== i + 1) return i + 1;
  }

  return n + 1;
}
```

---

#### ✅ Usage

```javascript
console.log(firstMissingPositive([1, 2, 0])); // Output: 3
console.log(firstMissingPositive([3, 4, -1, 1])); // Output: 2
console.log(firstMissingPositive([7, 8, 9, 11, 12])); // Output: 1
console.log(firstMissingPositive([1, 2, 3, 4])); // Output: 5
```

---

### ⏱ Time & Space Complexity

| Metric           | Value |
| ---------------- | ----- |
| Time Complexity  | O(n)  |
| Space Complexity | O(1)  |

---

### 📌 Summary

| Feature      | Description                                   |
| ------------ | --------------------------------------------- |
| Input        | Unsorted array of integers                    |
| Output       | Smallest **positive** integer not in array    |
| Constraints  | Must run in O(n) time and use O(1) space      |
| Core Concept | In-place index placing (**cycle sort style**) |
| Use Cases    | ID gaps, array integrity checks               |

---

## **5. Minimum Number of Swaps to Sort the Array**

### 🔍 Problem Statement

You are given an **array of `n` distinct integers**.
Return the **minimum number of swaps** required to **sort the array in ascending order**.

---

### 🧪 Examples

#### Example 1:

```
Input:  [4, 3, 2, 1]
Output: 2
Explanation:
Swap 4 and 1 → [1, 3, 2, 4]
Swap 3 and 2 → [1, 2, 3, 4]
```

#### Example 2:

```
Input:  [1, 5, 4, 3, 2]
Output: 2
```

---

### 🧠 Intuition

This is based on **cycle detection in graphs**:

- Sort the array → track **original indices**
- Each cycle of misplaced elements needs `cycleLength - 1` swaps
- Sum over all cycles to get total minimum swaps

---

### 🧵 Dry Run

```text
Input: [4, 3, 2, 1]
Sorted: [(1, 3), (2, 2), (3, 1), (4, 0)]

Cycle: 0 → 3 → 0 (length 2) → 1 swap
Cycle: 1 → 2 → 1 (length 2) → 1 swap
Total: 2 swaps
```

---

### 💻 JavaScript Code

```javascript
function minSwaps(nums) {
  let n = nums.length;
  let arr = nums.map((val, i) => [val, i]);

  // Sort by value
  arr.sort((a, b) => a[0] - b[0]);

  let swaps = 0;
  let i = 0;

  while (i < n) {
    let correctIndex = arr[i][1];
    if (arr[i][0] !== arr[correctIndex][0]) {
      [arr[i], arr[correctIndex]] = [arr[correctIndex], arr[i]];
      swaps++;
    } else {
      i++;
    }
  }

  return swaps;
}
```

---

### ⏱ Time & Space Complexity

| Metric           | Value                       |
| ---------------- | --------------------------- |
| Time Complexity  | O(n log n) (due to sorting) |
| Space Complexity | O(n)                        |

---

### 📌 Summary

| Feature      | Description                                         |
| ------------ | --------------------------------------------------- |
| Input        | Array of `n` distinct integers                      |
| Output       | Minimum swaps to sort array in ascending order      |
| Constraints  | No duplicates                                       |
| Core Concept | Detect **position cycles** and compute `length - 1` |
| Use Cases    | Sorting cost analysis, performance optimization     |

---
