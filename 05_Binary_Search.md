# 📘 **Binary Search Notes**

### 🔍 What is Binary Search?

Binary Search is an efficient algorithm used to find the position of a target value in a **sorted** array.

It works by repeatedly dividing the search interval in half.

---

### ✅ **Prerequisites**

- The array **must be sorted** (either ascending or descending).
- You should know the **start** and **end** indices of the array.

---

### 🧠 **Intuition**

Instead of checking every element one by one (like in linear search), binary search compares the middle element of the array with the target:

- If it matches, you return the index.
- If the target is less than mid, search the **left half**.
- If the target is greater than mid, search the **right half**.

---

### 🔄 **Algorithm Steps**

1. Set `low = 0`, `high = n - 1`.
2. While `low <= high`:

   - Compute `mid = low + (high - low) // 2`
   - If `arr[mid] == target`, return `mid`
   - If `arr[mid] < target`, set `low = mid + 1`
   - If `arr[mid] > target`, set `high = mid - 1`

3. If not found, return `-1`

---

### 💻 **Code (Iterative - Ascending Order)**

```javascript
function binarySearch(arr, target) {
  let low = 0;
  let high = arr.length - 1;

  while (low <= high) {
    let mid = Math.floor(low + (high - low) / 2);

    if (arr[mid] === target) return mid;
    else if (arr[mid] < target) low = mid + 1;
    else high = mid - 1;
  }

  return -1; // not found
}
```

---

### 🧪 **Dry Run**

For `arr = [2, 4, 7, 10, 15], target = 10`:

- Step 1: `low = 0, high = 4 → mid = 2`, arr\[2] = 7 → 7 < 10 → search right
- Step 2: `low = 3, high = 4 → mid = 3`, arr\[3] = 10 → Found!

---

### 🔁 Recursive Version

```javascript
function binarySearchRecursive(arr, target, low = 0, high = arr.length - 1) {
  if (low > high) return -1;

  let mid = Math.floor((low + high) / 2);

  if (arr[mid] === target) return mid;
  else if (arr[mid] < target)
    return binarySearchRecursive(arr, target, mid + 1, high);
  else return binarySearchRecursive(arr, target, low, mid - 1);
}
```

---

### 🧩 **Binary Search Variations**

1. **Lower Bound** – First index where element ≥ target
2. **Upper Bound** – First index where element > target
3. **First Occurrence** in duplicates
4. **Last Occurrence** in duplicates
5. **Binary Search on Answers** – Used in problems like "Minimum Days to Make Bouquets", "Capacity to Ship Packages", etc.

---

### ⏱️ **Time Complexity**

| Case    | Time     |
| ------- | -------- |
| Best    | O(1)     |
| Average | O(log n) |
| Worst   | O(log n) |

### 📦 **Space Complexity**

- **O(1)** for iterative
- **O(log n)** for recursive (stack space)

---

### 🧠 Tips

- Always ensure the array is **sorted**.
- Use `Math.floor` or equivalent to avoid floating mid-values.
- Watch out for integer overflow in some languages: use `mid = low + (high - low) // 2` instead of `(low + high) // 2`.

---

## 🔍 What is Order-Agnostic Binary Search?

**Order-Agnostic Binary Search** is a binary search algorithm that works **whether the array is sorted in ascending or descending order**.

> It first detects the sort order and then applies the correct comparison logic.

---

### 📦 Use Case

You're given a **sorted array** (either ascending or descending) and a **target value**. Your goal is to find the **index** of the target or return `-1` if not found.

---

### ✅ Steps

1. **Detect sort order**: Compare `arr[0]` and `arr[end]`
2. **Perform binary search**:

   - Adjust comparison based on the order:

     - Ascending → `target < arr[mid]`
     - Descending → `target > arr[mid]`

---

### 💡 JavaScript Implementation

```js
function orderAgnosticBinarySearch(arr, target) {
  let start = 0;
  let end = arr.length - 1;

  // Step 1: Check if ascending or descending
  let isAscending = arr[start] < arr[end];

  while (start <= end) {
    let mid = Math.floor(start + (end - start) / 2);

    if (arr[mid] === target) {
      return mid;
    }

    if (isAscending) {
      // Ascending order
      if (target < arr[mid]) {
        end = mid - 1;
      } else {
        start = mid + 1;
      }
    } else {
      // Descending order
      if (target > arr[mid]) {
        end = mid - 1;
      } else {
        start = mid + 1;
      }
    }
  }

  return -1; // not found
}
```

---

### 📦 Example 1 – Ascending

```js
orderAgnosticBinarySearch([1, 3, 5, 7, 9, 11], 7);
// ➤ Output: 3
```

### 📦 Example 2 – Descending

```js
orderAgnosticBinarySearch([100, 80, 60, 40, 20], 60);
// ➤ Output: 2
```

---

### ⏱️ Time and Space Complexity

- **Time Complexity**: `O(log n)` – Same as standard binary search.
- **Space Complexity**: `O(1)` – Iterative, constant space.

---

# **Binary Search on 1D Arrays**

## 1. **Lower Bound using Binary Search**

### 🔍 What is Lower Bound?

Given a **sorted array**, and a **target**, the **lower bound** is the index of the **first element that is not less than the target** (i.e., `>= target`).

If no such element exists, return the length of the array.

---

**Pre-requisite**: Binary Search

---

### 🧪 Examples

#### Example 1:

```
Input:  N = 4, arr = [1, 2, 2, 3], x = 2
Output: 1
Explanation: arr[1] = 2 is the first element >= 2
```

#### Example 2:

```
Input:  N = 5, arr = [3, 5, 8, 15, 19], x = 9
Output: 3
Explanation: arr[3] = 15 is the first element >= 9
```

---

### 🧠 Intuition

- The array is **sorted**, so we can use **Binary Search** to find the **first position** where the element is **not less than `x`**.
- Use binary search to shrink the range.

  - If `arr[mid] >= x`, store `mid` as a potential answer, and search on the **left half**.
  - Else, search on the **right half**.

---

### 🧵 Dry Run

```text
arr = [1, 2, 2, 3], x = 2

low = 0, high = 3, ans = 4 (default)

mid = 1 → arr[1] = 2 ≥ 2 → ans = 1, high = 0
mid = 0 → arr[0] = 1 < 2 → low = 1

Loop ends → final ans = 1
```

---

### 💻 JavaScript Code

```javascript
function lowerBound(arr, x) {
  let low = 0;
  let high = arr.length - 1;
  let ans = arr.length; // default: not found

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);

    if (arr[mid] >= x) {
      ans = mid;
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }

  return ans;
}
```

---

#### ✅ Usage

```javascript
console.log(lowerBound([1, 2, 2, 3], 2)); // Output: 1
console.log(lowerBound([3, 5, 8, 15, 19], 9)); // Output: 3
console.log(lowerBound([3, 5, 8, 15, 19], 20)); // Output: 5 (not found)
console.log(lowerBound([], 5)); // Output: 0 (edge case)
```

---

### ⏱ Time & Space Complexity

| Metric           | Value    |
| ---------------- | -------- |
| Time Complexity  | O(log N) |
| Space Complexity | O(1)     |

---

### 📌 Summary

| Feature        | Description                           |
| -------------- | ------------------------------------- |
| Input          | Sorted array `arr[]`, value `x`       |
| Output         | First index where `arr[i] >= x`       |
| Return Value   | Index `i` or `N` if not found         |
| Algorithm Used | Binary Search                         |
| Application    | Floor/Ceil, Insert position in arrays |

---

## 2. **Upper Bound using Binary Search**

### 🔍 What is Upper Bound?

Given a **sorted array** and a **target** `x`, the **upper bound** is the index of the **first element strictly greater than `x`** (i.e., `> x`).

If no such element exists, return the length of the array.

---

**Pre-requisite**: Binary Search

---

### 🧪 Examples

#### Example 1:

```
Input:  N = 4, arr = [1, 2, 2, 3], x = 2
Output: 3
Explanation: arr[3] = 3 is the first element > 2
```

#### Example 2:

```
Input:  N = 6, arr = [3, 5, 8, 9, 15, 19], x = 9
Output: 4
Explanation: arr[4] = 15 is the first element > 9
```

---

### 🧠 Intuition

- The array is **sorted**, so we can use **Binary Search** to find the **first position** where the element is **strictly greater than `x`**.
- Binary search helps narrow down the range:

  - If `arr[mid] > x`, store `mid` as a potential answer and search the **left half**.
  - Else, search the **right half**.

---

### 🧵 Dry Run

```text
arr = [1, 2, 2, 3], x = 2

low = 0, high = 3, ans = 4 (default)

mid = 1 → arr[1] = 2 ≤ 2 → low = 2
mid = 2 → arr[2] = 2 ≤ 2 → low = 3
mid = 3 → arr[3] = 3 > 2 → ans = 3, high = 2

Loop ends → final ans = 3
```

---

### 💻 JavaScript Code

```javascript
function upperBound(arr, x) {
  let low = 0;
  let high = arr.length - 1;
  let ans = arr.length; // default: not found

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);

    if (arr[mid] > x) {
      ans = mid;
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }

  return ans;
}
```

---

#### ✅ Usage

```javascript
console.log(upperBound([1, 2, 2, 3], 2)); // Output: 3
console.log(upperBound([3, 5, 8, 9, 15, 19], 9)); // Output: 4
console.log(upperBound([3, 5, 8, 15, 19], 20)); // Output: 5 (not found)
console.log(upperBound([], 5)); // Output: 0 (edge case)
```

---

### ⏱ Time & Space Complexity

| Metric           | Value    |
| ---------------- | -------- |
| Time Complexity  | O(log N) |
| Space Complexity | O(1)     |

---

### 📌 Summary

| Feature        | Description                       |
| -------------- | --------------------------------- |
| Input          | Sorted array `arr[]`, value `x`   |
| Output         | First index where `arr[i] > x`    |
| Return Value   | Index `i` or `N` if not found     |
| Algorithm Used | Binary Search                     |
| Application    | Range queries, insert upper bound |

---

## 3. **Search Insert Position using Binary Search**

### 🔍 What is Search Insert Position?

Given a **sorted array of distinct integers** and a **target** value `x`, return the **index** if the target is found. If not, return the index where it would be **inserted to maintain the sorted order**.

---

**Pre-requisite**: Lower Bound, Binary Search

---

### 🧪 Examples

#### Example 1:

```
Input:  arr = [1, 2, 4, 7], x = 6
Output: 3
Explanation: 6 is not in the array. It should be inserted at index 3 to maintain the sorted order.
```

#### Example 2:

```
Input:  arr = [1, 2, 4, 7], x = 2
Output: 1
Explanation: 2 is already present at index 1.
```

---

### 🧠 Intuition

- This is essentially a **lower bound** problem:

  - If the target is found → return its index.
  - If not found → return the index of the **first element greater than `x`**, which is where `x` should be inserted.

- Since the array is sorted, we can use **binary search** to do this efficiently in O(log N) time.

---

### 🧵 Dry Run

```text
arr = [1, 2, 4, 7], x = 6

low = 0, high = 3, ans = 4 (default)

mid = 1 → arr[1] = 2 < 6 → low = 2
mid = 2 → arr[2] = 4 < 6 → low = 3
mid = 3 → arr[3] = 7 > 6 → ans = 3, high = 2

Loop ends → final ans = 3
```

---

### 💻 JavaScript Code

```javascript
function searchInsertPosition(arr, x) {
  let low = 0;
  let high = arr.length - 1;
  let ans = arr.length;

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);

    if (arr[mid] >= x) {
      ans = mid;
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }

  return ans;
}
```

---

#### ✅ Usage

```javascript
console.log(searchInsertPosition([1, 2, 4, 7], 6)); // Output: 3
console.log(searchInsertPosition([1, 2, 4, 7], 2)); // Output: 1
console.log(searchInsertPosition([1, 3, 5, 6], 7)); // Output: 4
console.log(searchInsertPosition([], 10)); // Output: 0
```

---

### ⏱ Time & Space Complexity

| Metric           | Value    |
| ---------------- | -------- |
| Time Complexity  | O(log N) |
| Space Complexity | O(1)     |

---

### 📌 Summary

| Feature        | Description                                        |
| -------------- | -------------------------------------------------- |
| Input          | Sorted array `arr[]`, value `x`                    |
| Output         | Index of `x` or index where `x` should be inserted |
| Return Value   | Valid index (0 to N)                               |
| Algorithm Used | Binary Search / Lower Bound                        |
| Application    | Insert/search in ordered arrays                    |

---

## 4. **Floor and Ceiling in a Sorted Array**

### 🔍 What are Floor and Ceiling?

Given a **sorted array** and a **target** value `x`:

- The **floor** of `x` is the **largest element** in the array **≤ x**.
- The **ceiling** of `x` is the **smallest element** in the array **≥ x**.

If the floor or ceiling doesn't exist, return `-1` for that value.

---

**Pre-requisite**: Lower Bound, Binary Search

---

### 🧪 Examples

#### Example 1:

```
Input:  arr = [3, 4, 4, 7, 8, 10], x = 5
Output: 4 7
Explanation: Floor is 4 (≤ 5), Ceiling is 7 (≥ 5)
```

#### Example 2:

```
Input:  arr = [3, 4, 4, 7, 8, 10], x = 8
Output: 8 8
Explanation: Both floor and ceiling are 8
```

#### Example 3:

```
Input:  arr = [3, 4, 4, 7, 8, 10], x = 2
Output: -1 3
Explanation: No floor exists, ceiling is 3
```

#### Example 4:

```
Input:  arr = [3, 4, 4, 7, 8, 10], x = 15
Output: 10 -1
Explanation: Floor is 10, no ceiling exists
```

---

### 🧠 Intuition

- Use **binary search** to find:

  - Floor: **last element ≤ x**
  - Ceiling: **first element ≥ x**

- These are standard binary search variations, similar to lower bound and upper bound concepts.

---

### 🧵 Dry Run

```text
arr = [3, 4, 4, 7, 8, 10], x = 5

Find floor:
low = 0, high = 5, floor = -1
mid = 2 → arr[2] = 4 ≤ 5 → floor = 4, low = 3
mid = 4 → arr[4] = 8 > 5 → high = 3
mid = 3 → arr[3] = 7 > 5 → high = 2
→ Final floor = 4

Find ceiling:
low = 0, high = 5, ceil = -1
mid = 2 → arr[2] = 4 < 5 → low = 3
mid = 4 → arr[4] = 8 > 5 → ceil = 8, high = 3
mid = 3 → arr[3] = 7 > 5 → ceil = 7, high = 2
→ Final ceil = 7
```

---

### 💻 JavaScript Code

```javascript
function findFloorAndCeil(arr, x) {
  let floor = -1,
    ceil = -1;

  // Find floor (last element ≤ x)
  let low = 0,
    high = arr.length - 1;
  while (low <= high) {
    let mid = Math.floor((low + high) / 2);
    if (arr[mid] <= x) {
      floor = arr[mid];
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  // Find ceil (first element ≥ x)
  (low = 0), (high = arr.length - 1);
  while (low <= high) {
    let mid = Math.floor((low + high) / 2);
    if (arr[mid] >= x) {
      ceil = arr[mid];
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }

  return [floor, ceil];
}
```

---

#### ✅ Usage

```javascript
console.log(findFloorAndCeil([3, 4, 4, 7, 8, 10], 5)); // Output: [4, 7]
console.log(findFloorAndCeil([3, 4, 4, 7, 8, 10], 8)); // Output: [8, 8]
console.log(findFloorAndCeil([3, 4, 4, 7, 8, 10], 2)); // Output: [-1, 3]
console.log(findFloorAndCeil([3, 4, 4, 7, 8, 10], 15)); // Output: [10, -1]
```

---

### ⏱ Time & Space Complexity

| Metric           | Value    |
| ---------------- | -------- |
| Time Complexity  | O(log N) |
| Space Complexity | O(1)     |

---

### 📌 Summary

| Feature        | Description                                   |
| -------------- | --------------------------------------------- |
| Input          | Sorted array `arr[]`, value `x`               |
| Output         | Floor and Ceiling values                      |
| Return Value   | Pair \[floor, ceil], -1 if not found          |
| Algorithm Used | Binary Search (Floor & Lower Bound logic)     |
| Application    | Range searching, interval mapping, thresholds |

---

## 5. **Last Occurrence of Element in Sorted Array**

### 🔍 Problem Statement

Given a **sorted array** of `N` integers, and a **target value**, return the **index of the last occurrence** of the target. If the target does not exist, return `-1`.

**Note**: Use **0-based indexing**.

---

**Pre-requisite**: Binary Search

---

### 🧪 Examples

#### Example 1:

```
Input:  N = 7, target = 13, arr = [3, 4, 13, 13, 13, 20, 40]
Output: 4
Explanation: The last occurrence of 13 is at index 4.
```

#### Example 2:

```
Input:  N = 7, target = 60, arr = [3, 4, 13, 13, 13, 20, 40]
Output: -1
Explanation: 60 is not present in the array.
```

#### Example 3:

```
Input:  N = 6, target = 10, arr = [1, 2, 5, 5, 10, 10]
Output: 5
```

#### Example 4:

```
Input:  N = 6, target = 1, arr = [1, 2, 5, 5, 10, 10]
Output: 0
```

---

### 🧠 Intuition

Since the array is **sorted**, we can use **binary search** to avoid a linear scan. We'll modify the binary search to:

- Move **right** if the target is found, because there may be more occurrences later.
- Move **left** if the current element is greater than the target.
- Move **right** if current element is less than the target.

---

### ✅ Approach 1: Modified Binary Search (Optimal)

#### 💻 JavaScript Code

```javascript
function lastOccurrence(arr, target) {
  let low = 0,
    high = arr.length - 1;
  let result = -1;

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);

    if (arr[mid] === target) {
      result = mid; // Store index
      low = mid + 1; // Move right to find last occurrence
    } else if (arr[mid] < target) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  return result;
}
```

---

### ✅ Approach 2: Linear Scan (Brute Force)

> 🚫 Not recommended for large arrays but good as a basic starting point.

```javascript
function lastOccurrenceBrute(arr, target) {
  for (let i = arr.length - 1; i >= 0; i--) {
    if (arr[i] === target) return i;
  }
  return -1;
}
```

---

##### ✅ Usage

```javascript
console.log(lastOccurrence([3, 4, 13, 13, 13, 20, 40], 13)); // Output: 4
console.log(lastOccurrence([3, 4, 13, 13, 13, 20, 40], 60)); // Output: -1
console.log(lastOccurrence([1, 2, 5, 5, 10, 10], 10)); // Output: 5
console.log(lastOccurrence([1, 2, 5, 5, 10, 10], 1)); // Output: 0
```

---

### ⏱ Time & Space Complexity

| Approach      | Time Complexity | Space Complexity |
| ------------- | --------------- | ---------------- |
| Binary Search | O(log N)        | O(1)             |
| Linear Scan   | O(N)            | O(1)             |

---

### 📌 Summary

| Feature       | Description                              |
| ------------- | ---------------------------------------- |
| Input         | Sorted array `arr[]`, integer `target`   |
| Output        | Index of **last occurrence** of target   |
| Return Value  | Integer index or `-1` if not found       |
| Best Approach | Modified Binary Search                   |
| Alternatives  | Linear scan (brute force)                |
| Use Cases     | Frequency count, range indexing problems |

---

## 6. **Count Occurrences in a Sorted Array**

### 🔍 Problem Statement

You're given a **sorted array** of `N` integers and a target `X`. Your task is to **count how many times `X` occurs** in the array.

---

**Pre-requisite**: Binary Search, Lower Bound, Upper Bound

---

### 🧪 Examples

#### Example 1:

```
Input:  N = 7, X = 3, arr = [2, 2, 3, 3, 3, 3, 4]
Output: 4
Explanation: 3 appears from index 2 to 5 → total = 4
```

#### Example 2:

```
Input:  N = 8, X = 2, arr = [1, 1, 2, 2, 2, 2, 2, 3]
Output: 5
Explanation: 2 appears from index 2 to 6 → total = 5
```

#### Example 3:

```
Input:  N = 6, X = 1, arr = [1, 1, 1, 1, 1, 1]
Output: 6
Explanation: All elements are 1 → count = 6
```

#### Example 4:

```
Input:  N = 5, X = 10, arr = [2, 4, 6, 8, 9]
Output: 0
Explanation: 10 is not present → count = 0
```

---

### 🧠 Intuition

- Since the array is **sorted**, we can use **Binary Search** to find the:

  - First occurrence of `X` (`lowerBound`)
  - Last occurrence of `X` (`upperBound - 1`)

- Count = `lastIndex - firstIndex + 1`

---

### ✅ Approach 1: Binary Search for First & Last Occurrence

#### 💻 JavaScript Code

```javascript
function countOccurrences(arr, x) {
  function lowerBound(arr, x) {
    let low = 0,
      high = arr.length - 1,
      ans = arr.length;
    while (low <= high) {
      let mid = Math.floor((low + high) / 2);
      if (arr[mid] >= x) {
        ans = mid;
        high = mid - 1;
      } else {
        low = mid + 1;
      }
    }
    return ans;
  }

  function upperBound(arr, x) {
    let low = 0,
      high = arr.length - 1,
      ans = arr.length;
    while (low <= high) {
      let mid = Math.floor((low + high) / 2);
      if (arr[mid] > x) {
        ans = mid;
        high = mid - 1;
      } else {
        low = mid + 1;
      }
    }
    return ans;
  }

  let lb = lowerBound(arr, x);
  let ub = upperBound(arr, x);

  let count = ub - lb;
  return count > 0 ? count : 0;
}
```

---

### ✅ Approach 2: Linear Scan (Brute Force)

```javascript
function countOccurrencesBrute(arr, x) {
  let count = 0;
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === x) count++;
  }
  return count;
}
```

---

#### ✅ Usage

```javascript
console.log(countOccurrences([2, 2, 3, 3, 3, 3, 4], 3)); // Output: 4
console.log(countOccurrences([1, 1, 2, 2, 2, 2, 2, 3], 2)); // Output: 5
console.log(countOccurrences([1, 1, 1, 1, 1, 1], 1)); // Output: 6
console.log(countOccurrences([2, 4, 6, 8, 9], 10)); // Output: 0
```

---

### ⏱ Time & Space Complexity

| Approach      | Time Complexity | Space Complexity |
| ------------- | --------------- | ---------------- |
| Binary Search | O(log N)        | O(1)             |
| Linear Scan   | O(N)            | O(1)             |

---

### 📌 Summary

| Feature       | Description                             |
| ------------- | --------------------------------------- |
| Input         | Sorted array `arr[]`, integer `x`       |
| Output        | Number of times `x` occurs in the array |
| Return Value  | Integer count                           |
| Best Approach | Lower and Upper Bound via Binary Search |
| Alternate     | Linear scan                             |
| Application   | Frequency count in sorted datasets      |

---

Let me know your next problem to format or solve! 💻📘

## 7. **Search in Rotated Sorted Array**

### 🔍 Problem Statement

You're given a **sorted array** (ascending, with **distinct values**) that has been **rotated at an unknown pivot**. Given a **target value**, return its **index** if it exists, or **-1** if it does not.

🔧 You must solve this in **O(log N)** time.

---

**Pre-requisite**: Binary Search, Rotated Array Concept

---

### 🧪 Examples

#### Example 1:

```
Input:  nums = [4, 5, 6, 7, 0, 1, 2], target = 0
Output: 4
```

#### Example 2:

```
Input:  nums = [4, 5, 6, 7, 0, 1, 2], target = 3
Output: -1
```

#### Example 3:

```
Input:  nums = [1], target = 0
Output: -1
```

#### Example 4:

```
Input:  nums = [6, 7, 1, 2, 3, 4, 5], target = 3
Output: 4
```

---

### 🧠 Intuition

The array is **partially sorted**, i.e., one half (left or right) is always **sorted**.

**Binary Search Strategy**:

- Find the middle element.
- Check which part is sorted:

  - **Left part is sorted** → check if `target` lies in that part.
  - **Right part is sorted** → check if `target` lies in that part.

- Narrow down the search range accordingly.

---

### 🧵 Dry Run

```text
nums = [4,5,6,7,0,1,2], target = 0

low = 0, high = 6

mid = 3 → nums[3] = 7
Right half [4...6] is sorted
Target 0 lies in [4...6] → low = 4

mid = 5 → nums[5] = 1
Right half is sorted, target 0 lies in [4...4] → high = 4

mid = 4 → nums[4] = 0 → FOUND → return 4
```

---

### 💻 JavaScript Code

```javascript
function searchInRotatedArray(nums, target) {
  let low = 0,
    high = nums.length - 1;

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);

    if (nums[mid] === target) return mid;

    // Check which half is sorted
    if (nums[low] <= nums[mid]) {
      // Left half is sorted
      if (nums[low] <= target && target < nums[mid]) {
        high = mid - 1;
      } else {
        low = mid + 1;
      }
    } else {
      // Right half is sorted
      if (nums[mid] < target && target <= nums[high]) {
        low = mid + 1;
      } else {
        high = mid - 1;
      }
    }
  }

  return -1;
}
```

---

#### ✅ Usage

```javascript
console.log(searchInRotatedArray([4, 5, 6, 7, 0, 1, 2], 0)); // Output: 4
console.log(searchInRotatedArray([4, 5, 6, 7, 0, 1, 2], 3)); // Output: -1
console.log(searchInRotatedArray([1], 0)); // Output: -1
console.log(searchInRotatedArray([6, 7, 1, 2, 3, 4, 5], 3)); // Output: 4
```

---

### ⏱ Time & Space Complexity

| Metric           | Value    |
| ---------------- | -------- |
| Time Complexity  | O(log N) |
| Space Complexity | O(1)     |

---

### 📌 Summary

| Feature       | Description                                   |
| ------------- | --------------------------------------------- |
| Input         | Rotated sorted array `nums[]`, value `target` |
| Output        | Index of `target` or `-1`                     |
| Return Value  | Integer index                                 |
| Best Approach | Modified Binary Search                        |
| Application   | Search in rotated search spaces, OS/memory    |

---

## 8. **Search in Rotated Sorted Array II (with Duplicates)**

### 🔍 Problem Statement

You're given a **rotated sorted array** `nums` that may contain **duplicates**. Determine whether a **target value** exists in the array.

You must **minimize the number of operations** as much as possible.

---

**Pre-requisite**: Binary Search with Duplicate Handling, Rotated Array Logic

---

### 🧪 Examples

#### Example 1:

```
Input:  nums = [2,5,6,0,0,1,2], target = 0
Output: true
```

#### Example 2:

```
Input:  nums = [2,5,6,0,0,1,2], target = 3
Output: false
```

#### Example 3:

```
Input:  nums = [1,0,1,1,1], target = 0
Output: true
```

#### Example 4:

```
Input:  nums = [1,1,1,1,1], target = 2
Output: false
```

---

### 🧠 Intuition

This problem is similar to the standard rotated sorted array search, **but now includes duplicates**, which breaks normal binary search rules in some cases.

**Challenge**: When duplicates are present, `nums[low] == nums[mid] == nums[high]` gives us no information. In this case, we must **shrink the search space** by `low++` and `high--`.

---

### 🧵 Dry Run

```text
nums = [2,5,6,0,0,1,2], target = 0

low = 0, high = 6

mid = 3 → nums[3] = 0 → target found → return true
```

---

### 💻 JavaScript Code

```javascript
function searchInRotatedArrayII(nums, target) {
  let low = 0,
    high = nums.length - 1;

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);

    if (nums[mid] === target) return true;

    // If duplicates at edges, skip them
    if (nums[low] === nums[mid] && nums[mid] === nums[high]) {
      low++;
      high--;
    }
    // Left part is sorted
    else if (nums[low] <= nums[mid]) {
      if (nums[low] <= target && target < nums[mid]) {
        high = mid - 1;
      } else {
        low = mid + 1;
      }
    }
    // Right part is sorted
    else {
      if (nums[mid] < target && target <= nums[high]) {
        low = mid + 1;
      } else {
        high = mid - 1;
      }
    }
  }

  return false;
}
```

---

#### ✅ Usage

```javascript
console.log(searchInRotatedArrayII([2, 5, 6, 0, 0, 1, 2], 0)); // true
console.log(searchInRotatedArrayII([2, 5, 6, 0, 0, 1, 2], 3)); // false
console.log(searchInRotatedArrayII([1, 0, 1, 1, 1], 0)); // true
console.log(searchInRotatedArrayII([1, 1, 1, 1, 1], 2)); // false
```

---

### ⏱ Time & Space Complexity

| Metric           | Worst Case             | Best Case |
| ---------------- | ---------------------- | --------- |
| Time Complexity  | O(N) (when duplicates) | O(log N)  |
| Space Complexity | O(1)                   | O(1)      |

---

### 📌 Summary

| Feature        | Description                                          |
| -------------- | ---------------------------------------------------- |
| Input          | Rotated sorted array `nums[]`, target `x`            |
| Output         | `true` if `target` exists, otherwise `false`         |
| Edge Cases     | Duplicates at edges reduce efficiency to O(N)        |
| Algorithm Used | Modified Binary Search with Duplicate Handling       |
| Application    | Search in uncertain rotated lists with repeated data |

---

Here's your Java solution for **"Find Minimum in Rotated Sorted Array"** presented in the same structured format as before — this version follows the **"detect and eliminate the sorted half"** approach explicitly used in your code.

---

## 9. **Find Minimum in Rotated Sorted Array (Java Version)**

### 🔍 Problem Statement

Given a **rotated sorted array** `arr` of **unique elements**, return the **minimum element** in the array.

You must solve this in **O(log N)** time.

---

### 🧪 Examples

#### Example 1:

```
Input:  arr = [3,4,5,1,2]
Output: 1
```

#### Example 2:

```
Input:  arr = [4,5,6,7,0,1,2]
Output: 0
```

#### Example 3:

```
Input:  arr = [11,13,15,17]
Output: 11
```

#### Example 4:

```
Input:  arr = [2,3,4,5,6,7,1]
Output: 1
```

---

### 🧠 Intuition

This approach uses **binary search** and explicitly checks if the **current subarray is sorted**.

#### Key Idea:

- If `arr[low] <= arr[high]` → current segment is sorted → minimum is `arr[low]`.
- Otherwise:

  - If left half is sorted → min could be `arr[low]` → eliminate left.
  - If right half is sorted → min could be `arr[mid]` → eliminate right.

> 🔁 Keep track of minimum using `Math.min()`.

---

### 🧵 Dry Run

```text
arr = [4, 5, 6, 7, 0, 1, 2, 3]

low = 0, high = 7 → mid = 3 → arr[3]=7

→ arr[low]=4 ≤ arr[mid]=7 → left half is sorted
→ min = min(∞, 4) = 4 → eliminate left → low = 4

low = 4, high = 7 → mid = 5 → arr[5]=1
→ arr[mid]=1 ≤ arr[high]=3 → right half is sorted
→ min = min(4, 1) = 1 → eliminate right → high = 4

low = 4, high = 4 → arr[low]=0
→ search space sorted → min = min(1, 0) = 0 → done
```

---

### 💻 Java Code

```js
function findMin(arr) {
  let low = 0,
    high = arr.length - 1;
  let ans = Infinity;
  while (low <= high) {
    let mid = Math.floor((low + high) / 2);

    //search space is already sorted
    //then arr[low] will always be
    //the minimum in that search space:
    if (arr[low] <= arr[high]) {
      ans = Math.min(ans, arr[low]);
      break;
    }

    // If left part is sorted:
    if (arr[low] <= arr[mid]) {
      // Keep the minimum:
      ans = Math.min(ans, arr[low]);

      // Eliminate left half:
      low = mid + 1;
    } else {
      // If right part is sorted:
      // Keep the minimum:
      ans = Math.min(ans, arr[mid]);

      // Eliminate right half:
      high = mid - 1;
    }
  }
  return ans;
}

let arr = [4, 5, 6, 7, 0, 1, 2, 3];
let ans = findMin(arr);
console.log("The minimum element is: " + ans);
```

---

#### ✅ Usage

```java
int[] arr1 = {3, 4, 5, 1, 2}; // Output: 1
int[] arr2 = {4, 5, 6, 7, 0, 1, 2}; // Output: 0
int[] arr3 = {11, 13, 15, 17}; // Output: 11
int[] arr4 = {2, 3, 4, 5, 6, 7, 1}; // Output: 1
```

---

### ⏱ Time & Space Complexity

| Metric           | Value    |
| ---------------- | -------- |
| Time Complexity  | O(log N) |
| Space Complexity | O(1)     |

---

## 10. **Count Rotations in a Rotated Sorted Array**

### 🔍 Problem Statement

You are given a sorted array `arr[]` (distinct elements) that has been **rotated between 1 to N times**. Your task is to **find the number of times it has been rotated**.

The number of rotations equals the **index of the smallest element** in the rotated array.

---

**Pre-requisites**:

- 🔹 Binary Search
- 🔹 Find Minimum in Rotated Sorted Array
- 🔹 Rotated Array Concepts

---

### 🧪 Examples

#### Example 1:

```
Input:  arr = [4, 5, 6, 7, 0, 1, 2, 3]
Output: 4
Explanation: Minimum element is 0, which is at index 4 → rotated 4 times.
```

#### Example 2:

```
Input:  arr = [3, 4, 5, 1, 2]
Output: 3
Explanation: Minimum element is 1, which is at index 3 → rotated 3 times.
```

#### Example 3:

```
Input:  arr = [1, 2, 3, 4, 5]
Output: 0
Explanation: No rotation → smallest at index 0.
```

#### Example 4:

```
Input:  arr = [5, 1, 2, 3, 4]
Output: 1
Explanation: Smallest is at index 1 → rotated once.
```

---

### 🧠 Intuition

- The **minimum element** is the **pivot point** where rotation occurred.
- In a rotated sorted array without duplicates, we can use **Binary Search** to find the **minimum element’s index**.
- The **index of the smallest element = number of rotations**.

---

### 🧵 Dry Run

```text
arr = [4, 5, 6, 7, 0, 1, 2, 3]

low = 0, high = 7
mid = 3 → arr[3] = 7 > arr[7] = 3 → min is on right → low = 4

mid = 5 → arr[5] = 1 > arr[7] → low = 6

mid = 6 → arr[6] = 2 > arr[7] → low = 7

low = high = 7 → return index 4
```

---

### 💻 JavaScript Code

```javascript
function countRotations(arr) {
  let low = 0,
    high = arr.length - 1;

  while (low < high) {
    let mid = Math.floor((low + high) / 2);

    // If mid element is greater than high, pivot must be on right
    if (arr[mid] > arr[high]) {
      low = mid + 1;
    } else {
      high = mid; // pivot might be mid or to the left
    }
  }

  return low; // index of the smallest element
}
```

---

#### ✅ Usage

```javascript
console.log(countRotations([4, 5, 6, 7, 0, 1, 2, 3])); // Output: 4
console.log(countRotations([3, 4, 5, 1, 2])); // Output: 3
console.log(countRotations([1, 2, 3, 4, 5])); // Output: 0
console.log(countRotations([5, 1, 2, 3, 4])); // Output: 1
```

---

### ⏱ Time & Space Complexity

| Metric           | Value    |
| ---------------- | -------- |
| Time Complexity  | O(log N) |
| Space Complexity | O(1)     |

---

### 📌 Summary

| Feature     | Description                                       |
| ----------- | ------------------------------------------------- |
| Input       | Rotated sorted array `arr[]` (distinct values)    |
| Output      | Integer (number of rotations)                     |
| Idea        | Find the index of the smallest element            |
| Approach    | Binary Search to find pivot                       |
| Application | Circular arrays, OS job queues, rotated data logs |

---

## 11. **Single Element in a Sorted Array**

### 🔍 Problem Statement

You're given a **sorted array** where every element appears **exactly twice**, **except for one element** which appears **only once**. Find and return that single element.

Your algorithm must run in **O(log n)** time and use **O(1)** space.

---

**Pre-requisite**: Binary Search on Indexed Pairs

---

### 🧪 Examples

#### Example 1:

```
Input:  nums = [1, 1, 2, 3, 3, 4, 4, 8, 8]
Output: 2
Explanation: 2 appears once; all others appear twice.
```

#### Example 2:

```
Input:  nums = [3, 3, 7, 7, 10, 11, 11]
Output: 10
Explanation: 10 is the only element appearing once.
```

#### Example 3:

```
Input:  nums = [0, 1, 1, 2, 2, 3, 3]
Output: 0
```

#### Example 4:

```
Input:  nums = [1, 1, 2, 2, 3]
Output: 3
```

---

### 🧠 Intuition

In a sorted array:

- All **pairs appear consecutively**.
- The **first index of a pair is even**, and the **second is odd**.
- But **after the single element**, this pairing breaks (shifted).

👉 Use binary search to find the **first unmatched index** where `nums[mid] !== nums[mid ^ 1]`.

- `mid ^ 1` trick:

  - If `mid` is even, `mid ^ 1 = mid + 1`
  - If `mid` is odd, `mid ^ 1 = mid - 1`

---

### 🧵 Dry Run

```text
nums = [1, 1, 2, 3, 3, 4, 4, 8, 8]

low = 0, high = 8

mid = 4 → nums[4] = 3, nums[3] = 3 → pair matched → search right → low = 5

mid = 6 → nums[6] = 4, nums[7] = 8 → not matched → move left → high = 6

mid = 5 → nums[5] = 4, nums[4] = 3 → not matched → high = 5

mid = 5 → nums[5] = 4, nums[4] = 3 → not matched → high = 5

low == high → return nums[low] = 2
```

---

### 💻 JavaScript Code

```javascript
function singleNonDuplicate(nums) {
  let low = 0,
    high = nums.length - 1;

  while (low < high) {
    let mid = Math.floor((low + high) / 2);

    if (nums[mid] === nums[mid ^ 1]) {
      low = mid + 1;
    } else {
      high = mid;
    }
  }

  return nums[low];
}
```

---

#### ✅ Usage

```javascript
console.log(singleNonDuplicate([1, 1, 2, 3, 3, 4, 4, 8, 8])); // Output: 2
console.log(singleNonDuplicate([3, 3, 7, 7, 10, 11, 11])); // Output: 10
console.log(singleNonDuplicate([0, 1, 1, 2, 2, 3, 3])); // Output: 0
console.log(singleNonDuplicate([1, 1, 2, 2, 3])); // Output: 3
```

---

### ⏱ Time & Space Complexity

| Metric           | Value    |
| ---------------- | -------- |
| Time Complexity  | O(log N) |
| Space Complexity | O(1)     |

---

### 📌 Summary

| Feature     | Description                                         |
| ----------- | --------------------------------------------------- |
| Input       | Sorted array with one unique element                |
| Output      | The single non-duplicate element                    |
| Core Idea   | Use `mid ^ 1` to binary search through valid pairs  |
| Efficiency  | Logarithmic search using pair-matching index trick  |
| Application | Array compression, frequency deduplication, hashing |

---

## 12. **Find Peak Element**

### 🔍 Problem Statement

You are given a **0-indexed array** `nums[]`. A **peak element** is one that is **strictly greater than its neighbors**.

Return the **index of any peak element**.

📌 Assumptions:

- `nums[-1] = nums[n] = -∞`
- There is always **at least one peak**.
- Solve in **O(log N)** time.

---

**Pre-requisite**: Binary Search & Neighbor Comparison

---

### 🧪 Examples

#### Example 1:

```
Input:  nums = [1, 2, 3, 1]
Output: 2
Explanation: 3 is greater than both 2 and 1 → Peak at index 2
```

#### Example 2:

```
Input:  nums = [1, 2, 1, 3, 5, 6, 4]
Output: 5
Explanation: 6 > 5 and 6 > 4 → Peak at index 5 (also 2 is a peak at index 1)
```

#### Example 3:

```
Input:  nums = [1]
Output: 0
Explanation: Single element is always a peak
```

#### Example 4:

```
Input:  nums = [5, 10, 20, 15]
Output: 2
Explanation: 20 is the peak → index 2
```

---

### 🧠 Intuition

We can use **Binary Search** even if the array is not sorted:

- At any index `mid`, check `nums[mid]` vs `nums[mid+1]`
- If `nums[mid] > nums[mid+1]` → we are **in the decreasing slope** → peak on the **left** (including `mid`)
- Else → we are **in the increasing slope** → peak on the **right**

This binary narrowing guarantees convergence to a peak.

---

### 🧵 Dry Run

```text
nums = [1, 2, 1, 3, 5, 6, 4]

low = 0, high = 6
mid = 3 → nums[3] = 3 < nums[4] = 5 → move right → low = 4

mid = 5 → nums[5] = 6 > nums[6] = 4 → peak found on left → high = 5

mid = 4 → nums[4] = 5 < nums[5] = 6 → move right → low = 5

low = high → return 5
```

---

### 💻 JavaScript Code

```javascript
function findPeakElement(nums) {
  let low = 0,
    high = nums.length - 1;

  while (low < high) {
    let mid = Math.floor((low + high) / 2);

    if (nums[mid] > nums[mid + 1]) {
      high = mid; // Peak is on left
    } else {
      low = mid + 1; // Peak is on right
    }
  }

  return low; // or high, both are equal
}
```

---

#### ✅ Usage

```javascript
console.log(findPeakElement([1, 2, 3, 1])); // Output: 2
console.log(findPeakElement([1, 2, 1, 3, 5, 6, 4])); // Output: 5 (or 1)
console.log(findPeakElement([1])); // Output: 0
console.log(findPeakElement([5, 10, 20, 15])); // Output: 2
```

---

### ⏱ Time & Space Complexity

| Metric           | Value    |
| ---------------- | -------- |
| Time Complexity  | O(log N) |
| Space Complexity | O(1)     |

---

### 📌 Summary

| Feature      | Description                               |
| ------------ | ----------------------------------------- |
| Input        | Array `nums[]`                            |
| Output       | Index of any **peak element**             |
| Constraints  | `nums[i] ≠ nums[i+1]`, edge = -∞          |
| Core Concept | Binary Search using slope direction       |
| Use Cases    | Local optima detection, signal processing |

---

# **Binary Search on Answers**

### 📘 What is Binary Search on Answers?

**Binary Search on Answers** is a **problem-solving strategy** where:

- You are not binary searching through the **array elements**, but through a **range of possible answers**.
- The original problem is **reframed as a yes/no (decision)** problem: _“Is this value a valid solution?”_
- Then, binary search is applied to find the **minimum or maximum value** that satisfies the given condition.

---

### 🧠 When to Use It?

Use **Binary Search on Answers** when:

- You're asked to **minimize** or **maximize** something.
- The answer lies in a **range** (say \[low, high]).
- You can write a **helper function** like `isValid(mid)` or `canPlace(mid)` that returns a boolean.

---

### 🛠️ General Approach

1. Define the **search space** `[low, high]`.
2. While `low <= high`:

   - Find `mid = Math.floor((low + high) / 2)`
   - If `isValid(mid)`:

     - Save `mid` as a potential answer.
     - Move `high = mid - 1` (for minimization)

   - Else:

     - Move `low = mid + 1`

---

## 1. **Square Root of a Number (Floor of √n)**

---

### 🔍 Problem Statement

Given a **positive integer `n`**, return the **floor value of its square root**.

- If `n` is a perfect square, return `sqrt(n)`
- If `n` is not a perfect square, return the **largest integer `x` such that `x*x <= n`**

---

### 🔗 Pre-requisite

- Binary Search
- Integer Math

---

### 🧪 Examples

#### Example 1:

```
Input:  n = 36
Output: 6
Explanation: 6 * 6 = 36 → exact square root
```

#### Example 2:

```
Input:  n = 28
Output: 5
Explanation: sqrt(28) ≈ 5.29 → floor(sqrt(28)) = 5
```

#### Example 3:

```
Input:  n = 1
Output: 1
Explanation: sqrt(1) = 1
```

#### Example 4:

```
Input:  n = 10
Output: 3
Explanation: sqrt(10) ≈ 3.16 → floor = 3
```

---

### 🧠 Intuition

- The square root of a number lies between `1` and `n` (or `0` and `n`, if including 0).
- You can **use binary search** to check for midpoints `mid` such that `mid * mid <= n`, and track the highest valid `mid`.

---

### 🧵 Dry Run

```text
n = 28
low = 1, high = 28

mid = 14 → 14*14 = 196 > 28 → high = 13
mid = 7  → 7*7  = 49  > 28 → high = 6
mid = 4  → 16   <= 28 → ans = 4, low = 5
mid = 5  → 25   <= 28 → ans = 5, low = 6
mid = 6  → 36   > 28  → high = 5

Loop ends → answer = 5
```

---

### 💻 JavaScript Code

```javascript
function floorSqrt(n) {
  if (n === 0 || n === 1) return n;

  let low = 1,
    high = n;
  let ans = 1;

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);

    if (mid * mid === n) {
      return mid;
    }

    if (mid * mid < n) {
      ans = mid;
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  return ans;
}
```

---

#### ✅ Usage

```javascript
console.log(floorSqrt(36)); // Output: 6
console.log(floorSqrt(28)); // Output: 5
console.log(floorSqrt(1)); // Output: 1
console.log(floorSqrt(10)); // Output: 3
```

---

### ⏱ Time & Space Complexity

| Metric           | Value    |
| ---------------- | -------- |
| Time Complexity  | O(log N) |
| Space Complexity | O(1)     |

---

### 📌 Summary

| Feature      | Description                                    |
| ------------ | ---------------------------------------------- |
| Input        | Integer `n` (n ≥ 0)                            |
| Output       | Floor of √n                                    |
| Technique    | Binary Search on range \[0...n]                |
| Edge Cases   | n = 0, 1                                       |
| Applications | Math problems, integer approximation, geometry |

---

## 2. **N-th Root of a Number**

### 🔍 Problem Statement

You are given two positive integers `N` and `M`. Your task is to **find the N-th root of M** (i.e., a number `X` such that `X^N = M`).

- If such an integer `X` exists, return it.
- Otherwise, return `-1`.

---

### 🔗 Pre-requisite

- Binary Search on Answers
- Power calculation

---

### 🧪 Examples

#### Example 1:

```
Input:  N = 3, M = 27
Output: 3
Explanation: 3^3 = 27 → valid integer root
```

#### Example 2:

```
Input:  N = 4, M = 69
Output: -1
Explanation: No integer X such that X^4 = 69
```

#### Example 3:

```
Input:  N = 2, M = 81
Output: 9
```

#### Example 4:

```
Input:  N = 5, M = 243
Output: 3
```

---

### 🧠 Intuition

- The N-th root of M lies in the range `[1, M]`.
- We perform **binary search** on this range.
- At each step, compute `mid^N` and:

  - If `mid^N === M`, return `mid`
  - If `mid^N < M`, move right
  - If `mid^N > M`, move left

---

### 🧵 Dry Run

```text
N = 3, M = 27

low = 1, high = 27

mid = 14 → 14^3 = 2744 > 27 → high = 13
mid = 7 → 343 > 27 → high = 6
mid = 4 → 64 > 27 → high = 3
mid = 2 → 8 < 27 → low = 3
mid = 3 → 27 = 27 → return 3 ✅
```

---

### ⚙️ Helper Function: `power(mid, n, m)`

- Avoid using `Math.pow()` directly due to floating-point precision issues.
- Instead, implement safe integer power check.

---

### 💻 JavaScript Code

```javascript
function nthRoot(N, M) {
  let low = 1,
    high = M;

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);
    let result = power(mid, N, M);

    if (result === 1) return mid;
    else if (result === 2) high = mid - 1;
    else low = mid + 1;
  }

  return -1;
}

function power(x, n, m) {
  let res = 1;
  for (let i = 1; i <= n; i++) {
    res *= x;
    if (res > m) return 2; // too big
  }
  if (res === m) return 1; // exact
  return 0; // too small
}
```

---

#### ✅ Usage

```javascript
console.log(nthRoot(3, 27)); // Output: 3
console.log(nthRoot(4, 69)); // Output: -1
console.log(nthRoot(2, 81)); // Output: 9
console.log(nthRoot(5, 243)); // Output: 3
```

---

### ⏱ Time & Space Complexity

| Metric           | Value         |
| ---------------- | ------------- |
| Time Complexity  | O(log M \* N) |
| Space Complexity | O(1)          |

---

### 📌 Summary

| Feature   | Description                                   |
| --------- | --------------------------------------------- |
| Input     | Two integers `N` and `M`                      |
| Output    | Integer X such that `X^N = M` or -1           |
| Technique | Binary Search on Answers                      |
| Used in   | Math libraries, root approximation algorithms |

---

## 3. **Koko Eating Bananas 🍌 (Minimum Eating Speed)**

### 🔍 Problem Statement

Koko has `n` banana piles and `h` hours before the guards return.

- She eats at a speed of **k bananas per hour**.
- Each hour, she can choose **one pile** and eat up to `k` bananas.
- If the pile has **less than k bananas**, she eats them all and waits for the next hour.

🧠 **Goal**: Find the **minimum value of `k`** such that Koko can finish **all the bananas** in **`h` hours**.

---

### 🔗 Pre-requisite

- Binary Search on Answers
- Ceil division logic

---

### 🧪 Examples

#### Example 1:

```
Input:  piles = [3,6,7,11], h = 8
Output: 4
Explanation: With k = 4 → hours = 1+2+2+3 = 8 ✅
```

#### Example 2:

```
Input:  piles = [30,11,23,4,20], h = 5
Output: 30
```

#### Example 3:

```
Input:  piles = [30,11,23,4,20], h = 6
Output: 23
```

---

### 🧠 Intuition

- We want to **minimize k**, such that Koko can finish eating in `≤ h` hours.
- Valid `k` values lie between:

  - `low = 1` (slowest speed)
  - `high = max(piles)` (fastest possible speed)

- Use Binary Search:

  - If she **can eat all bananas in h hours** at speed `k`, try smaller `k`.
  - Otherwise, try higher speeds.

---

### 🧵 Dry Run

```text
piles = [3, 6, 7, 11], h = 8

low = 1, high = 11
mid = 6 → total hours = ceil(3/6) + ceil(6/6) + ceil(7/6) + ceil(11/6)
         = 1 + 1 + 2 + 2 = 6 → ✅ try smaller → high = 5

mid = 3 → hours = 1 + 2 + 3 + 4 = 10 → too long → low = 4

mid = 4 → hours = 1 + 2 + 2 + 3 = 8 ✅ → answer = 4
```

---

### 💻 JavaScript Code

```javascript
function minEatingSpeed(piles, h) {
  let low = 1,
    high = Math.max(...piles);
  let answer = high;

  const canEatAll = (speed) => {
    let hours = 0;
    for (let pile of piles) {
      hours += Math.ceil(pile / speed);
    }
    return hours <= h;
  };

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);
    if (canEatAll(mid)) {
      answer = mid;
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }

  return answer;
}
```

---

#### ✅ Usage

```javascript
console.log(minEatingSpeed([3, 6, 7, 11], 8)); // Output: 4
console.log(minEatingSpeed([30, 11, 23, 4, 20], 5)); // Output: 30
console.log(minEatingSpeed([30, 11, 23, 4, 20], 6)); // Output: 23
```

---

### ⏱ Time & Space Complexity

| Metric           | Value         |
| ---------------- | ------------- |
| Time Complexity  | O(N \* log M) |
| Space Complexity | O(1)          |

Where:

- `N` = number of piles
- `M` = max number of bananas in any pile

---

### 📌 Summary

| Feature      | Description                                        |
| ------------ | -------------------------------------------------- |
| Input        | `piles[]` and total hours `h`                      |
| Output       | Minimum `k` such that all bananas are eaten in `h` |
| Technique    | Binary Search on possible speeds (answers)         |
| Core Idea    | Minimize the valid speed `k`                       |
| Applications | Load balancing, scheduling, time-constrained tasks |

---

## 4. **Minimum Days to Make M Bouquets**

### 🔍 Problem Statement

You're given:

- `bloomDay[]`: array where `bloomDay[i]` is the day the `i-th` flower blooms
- `m`: number of bouquets needed
- `k`: number of **adjacent** flowers required per bouquet

🌸 **Goal**: Return the **minimum number of days** to make `m` bouquets, or `-1` if it's **impossible**.

---

### 🔗 Pre-requisites

- Binary Search on Answers
- Array processing with sliding logic

---

### 🧪 Examples

#### Example 1:

```
Input: bloomDay = [1,10,3,10,2], m = 3, k = 1
Output: 3
Explanation: After 3 days → bloom status: [x, _, x, _, x] → Can make 3 bouquets ✅
```

#### Example 2:

```
Input: bloomDay = [1,10,3,10,2], m = 3, k = 2
Output: -1
Explanation: Need 6 flowers but only have 5 → ❌
```

#### Example 3:

```
Input: bloomDay = [7,7,7,7,12,7,7], m = 2, k = 3
Output: 12
```

#### Example 4:

```
Input: bloomDay = [5, 5, 5, 5, 5], m = 1, k = 5
Output: 5
```

---

### 🧠 Intuition

- The earliest possible day is `min(bloomDay)`, the latest is `max(bloomDay)`
- We perform a **Binary Search on days**
- For each candidate day `d`, check:

  - Can we make **at least `m` bouquets** using **only flowers bloomed by day `d`**?

✅ If yes → try smaller days
❌ If no → try larger days

---

### ⚙️ Helper: Can We Make Bouquets?

- Traverse the `bloomDay[]`
- Count **consecutive bloomed flowers** (i.e., `bloomDay[i] ≤ mid`)
- If count reaches `k`, increment bouquet count, and reset

---

### 🧵 Dry Run

```text
bloomDay = [1,10,3,10,2], m = 3, k = 1
Search range: 1 to 10

mid = 5 → flowers bloomed = [x, _, x, _, x]
Bouquets = 3 ✅ → try smaller → high = 4

mid = 3 → bloomed = [x, _, x, _, x] → bouquets = 3 ✅ → high = 2

mid = 2 → bloomed = [x, _, _, _, x] → bouquets = 2 ❌ → low = 3

Answer = 3
```

---

### 💻 JavaScript Code

```javascript
function minDays(bloomDay, m, k) {
  const n = bloomDay.length;

  if (m * k > n) return -1; // Not enough flowers

  let low = Math.min(...bloomDay);
  let high = Math.max(...bloomDay);
  let ans = -1;

  const canMake = (day) => {
    let count = 0,
      consecutive = 0;

    for (let bloom of bloomDay) {
      if (bloom <= day) {
        consecutive++;
        if (consecutive === k) {
          count++;
          consecutive = 0;
        }
      } else {
        consecutive = 0;
      }
    }

    return count >= m;
  };

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);

    if (canMake(mid)) {
      ans = mid;
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }

  return ans;
}
```

---

#### ✅ Usage

```javascript
console.log(minDays([1, 10, 3, 10, 2], 3, 1)); // Output: 3
console.log(minDays([1, 10, 3, 10, 2], 3, 2)); // Output: -1
console.log(minDays([7, 7, 7, 7, 12, 7, 7], 2, 3)); // Output: 12
console.log(minDays([5, 5, 5, 5, 5], 1, 5)); // Output: 5
```

---

### ⏱ Time & Space Complexity

| Metric           | Value            |
| ---------------- | ---------------- |
| Time Complexity  | O(N \* log(max)) |
| Space Complexity | O(1)             |

Where:

- `N` = size of `bloomDay`
- `max` = maximum bloom value

---

### 📌 Summary

| Feature   | Description                                         |
| --------- | --------------------------------------------------- |
| Input     | `bloomDay[]`, bouquets `m`, flowers per bouquet `k` |
| Output    | Minimum number of days or `-1` if not possible      |
| Technique | Binary Search on Answer + Greedy check              |
| Used in   | Scheduling, sliding window + greedy optimization    |

---

## 5. **Smallest Divisor Given a Threshold**

### 🔍 Problem Statement

You're given an integer array `nums[]` and an integer `threshold`.

Choose a **positive integer divisor**, divide all elements of `nums[]` by it using **ceil division**, and take the sum.

🧠 **Goal**: Find the **smallest divisor** such that the **sum is less than or equal to `threshold`**.

> Use `Math.ceil(nums[i] / divisor)` for each element.

---

### 🔗 Pre-requisite

- Binary Search on Answers
- Ceiling division and sum computation

---

### 🧪 Examples

#### Example 1:

```
Input: nums = [1,2,5,9], threshold = 6
Output: 5

Explanation:
Try divisor = 5 → [1,1,1,2] → sum = 5 ✅
```

#### Example 2:

```
Input: nums = [44,22,33,11,1], threshold = 5
Output: 44

Explanation:
Only when divisor = 44 we get [1,1,1,1,1] → sum = 5 ✅
```

#### Example 3:

```
Input: nums = [8,4,2], threshold = 3
Output: 8
```

#### Example 4:

```
Input: nums = [1,2,3], threshold = 10
Output: 1
```

---

### 🧠 Intuition

- The divisor must lie between:

  - `low = 1` (smallest possible)
  - `high = max(nums)` (largest divisor will reduce all values to 1)

- Perform **Binary Search on this range**.
- For a given divisor:

  - If total sum after division ≤ threshold → try smaller divisor
  - Else → increase the divisor

---

### 🧵 Dry Run

```text
nums = [1,2,5,9], threshold = 6

Try divisor = 5 → [1,1,1,2] → sum = 5 ✅
Try divisor = 4 → [1,1,2,3] → sum = 7 ❌
Try divisor = 6 → [1,1,1,2] → sum = 5 ✅
Keep trying smaller to find minimum valid divisor
Final answer = 5
```

---

### 💻 JavaScript Code

```javascript
function smallestDivisor(nums, threshold) {
  let low = 1;
  let high = Math.max(...nums);
  let answer = high;

  const getSum = (divisor) => {
    let sum = 0;
    for (let num of nums) {
      sum += Math.ceil(num / divisor);
    }
    return sum;
  };

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);
    let sum = getSum(mid);

    if (sum <= threshold) {
      answer = mid;
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }

  return answer;
}
```

---

#### ✅ Usage

```javascript
console.log(smallestDivisor([1, 2, 5, 9], 6)); // Output: 5
console.log(smallestDivisor([44, 22, 33, 11, 1], 5)); // Output: 44
console.log(smallestDivisor([1, 2, 3], 10)); // Output: 1
console.log(smallestDivisor([8, 4, 2], 3)); // Output: 8
```

---

### ⏱ Time & Space Complexity

| Metric           | Value         |
| ---------------- | ------------- |
| Time Complexity  | O(N \* log M) |
| Space Complexity | O(1)          |

Where:

- `N` = number of elements in `nums`
- `M` = maximum value in `nums`

---

### 📌 Summary

| Feature   | Description                                                 |
| --------- | ----------------------------------------------------------- |
| Input     | Array of integers `nums[]` and integer `threshold`          |
| Output    | Smallest integer divisor such that division sum ≤ threshold |
| Technique | Binary Search on Answer                                     |
| Use Case  | Minimizing rate to stay within constraints                  |

---

## 6. **Ship Packages Within D Days 🚢**

### 🔍 Problem Statement

You are given an array `weights[]` representing the weights of packages, and an integer `days`.

📦 You must **ship all the packages** in the **given order**, using a ship that has a maximum weight capacity per day.

🧠 **Goal**: Return the **minimum weight capacity** of the ship so that all packages are shipped in `≤ days`.

---

### 🔗 Pre-requisite

- Binary Search on Answer
- Greedy grouping of weights by ship capacity

---

### 🧪 Examples

#### Example 1:

```
Input: weights = [1,2,3,4,5,6,7,8,9,10], days = 5
Output: 15

Explanation:
Day 1: 1,2,3,4,5
Day 2: 6,7
Day 3: 8
Day 4: 9
Day 5: 10
```

#### Example 2:

```
Input: weights = [3,2,2,4,1,4], days = 3
Output: 6
```

#### Example 3:

```
Input: weights = [1,2,3,1,1], days = 4
Output: 3
```

---

### 🧠 Intuition

- The ship must carry at least `max(weights)` on any day.
- The worst-case capacity is `sum(weights)` (carry everything in one day).
- **Search range**:

  - `low = max(weights)`
  - `high = sum(weights)`

Use **Binary Search** to find the **minimum capacity** that allows shipping all packages in `≤ days`.

---

### 🧵 Dry Run

```text
weights = [1,2,3,4,5,6,7,8,9,10], days = 5

Try mid = 15:
  - Day 1: 1+2+3+4+5 = 15
  - Day 2: 6+7 = 13
  - Day 3: 8
  - Day 4: 9
  - Day 5: 10 ✅
Try lower values until it's not valid
```

---

### 💻 JavaScript Code

```javascript
function shipWithinDays(weights, days) {
  let low = Math.max(...weights);
  let high = weights.reduce((a, b) => a + b, 0);
  let answer = high;

  const canShip = (capacity) => {
    let requiredDays = 1;
    let currentLoad = 0;

    for (let weight of weights) {
      if (currentLoad + weight <= capacity) {
        currentLoad += weight;
      } else {
        requiredDays++;
        currentLoad = weight;
      }
    }

    return requiredDays <= days;
  };

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);

    if (canShip(mid)) {
      answer = mid;
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }

  return answer;
}
```

---

#### ✅ Usage

```javascript
console.log(shipWithinDays([1, 2, 3, 4, 5, 6, 7, 8, 9, 10], 5)); // Output: 15
console.log(shipWithinDays([3, 2, 2, 4, 1, 4], 3)); // Output: 6
console.log(shipWithinDays([1, 2, 3, 1, 1], 4)); // Output: 3
```

---

### ⏱ Time & Space Complexity

| Metric           | Value         |
| ---------------- | ------------- |
| Time Complexity  | O(N \* log S) |
| Space Complexity | O(1)          |

Where:

- `N` = number of weights
- `S` = sum of all weights

---

### 📌 Summary

| Feature        | Description                                   |
| -------------- | --------------------------------------------- |
| Input          | weights\[], number of days                    |
| Output         | Minimum weight capacity to ship within `days` |
| Algorithm Used | Binary Search on Answer                       |
| Use Case       | Scheduling, capacity planning                 |

---

## 7. **Kth Missing Positive Number**

### 🔍 Problem Statement

You are given a strictly increasing sorted array `arr[]` of positive integers and an integer `k`.

👉 **Goal**: Return the `k-th` positive integer that is **missing** from this array.

---

### 🔗 Pre-requisite

- Binary Search (for optimized version)
- Basic arithmetic reasoning

---

### 🧪 Examples

#### Example 1:

```
Input: arr = [2,3,4,7,11], k = 5
Output: 9

Explanation: Missing = [1,5,6,8,9,...] → 5th missing = 9
```

#### Example 2:

```
Input: arr = [1,2,3,4], k = 2
Output: 6

Explanation: Missing = [5,6,...] → 2nd missing = 6
```

#### Example 3:

```
Input: arr = [5,6,8,9], k = 4
Output: 7
```

#### Example 4:

```
Input: arr = [2], k = 1
Output: 1
```

---

### 🧠 Intuition

Let’s define:

- `arr[i]` should be the `(i + 1)`-th natural number if **no numbers were missing**
- But the actual value is more, so:

  ```
  missing = arr[i] - (i + 1)
  ```

Example:

```text
arr = [2,3,4,7,11]
missing before arr[0] = 2 - 1 = 1 → [1]
missing before arr[1] = 3 - 2 = 1 → [1,5]
...
```

---

### 🔸 Approach 1: Brute Force (Linear Scan)

#### 💻 JavaScript Code

```javascript
function findKthPositive(arr, k) {
  let i = 0,
    num = 1;

  while (k > 0) {
    if (i < arr.length && arr[i] === num) {
      i++;
    } else {
      k--;
      if (k === 0) return num;
    }
    num++;
  }
}
```

---

#### ⏱ Time & Space Complexity (Brute Force)

| Metric           | Value    |
| ---------------- | -------- |
| Time Complexity  | O(k + n) |
| Space Complexity | O(1)     |

---

### 🔸 Approach 2: Binary Search (Optimized)

We binary search the **first position** where `missing count >= k`.

```text
missing = arr[mid] - (mid + 1)
```

If `missing < k` → move right
Else → move left

---

#### 💻 JavaScript Code (Binary Search)

```javascript
function findKthPositive(arr, k) {
  let left = 0,
    right = arr.length - 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    const missing = arr[mid] - (mid + 1);

    if (missing < k) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return left + k;
}
```

---

#### 🧵 Dry Run

```text
arr = [2,3,4,7,11], k = 5

Binary Search:
mid = 2 → missing = 4 - 3 = 1 < 5 → move right
mid = 3 → missing = 7 - 4 = 3 < 5 → move right
mid = 4 → missing = 11 - 5 = 6 ≥ 5 → move left

left = 4, right = 3 → done
return left + k = 4 + 5 = 9 ✅
```

---

#### ⏱ Time & Space Complexity (Binary Search)

| Metric           | Value    |
| ---------------- | -------- |
| Time Complexity  | O(log N) |
| Space Complexity | O(1)     |

---

#### 📌 Summary

| Feature       | Description                                 |
| ------------- | ------------------------------------------- |
| Input         | Sorted positive integer array, integer `k`  |
| Output        | k-th missing positive number                |
| Brute Force   | Check each number, skip if present in array |
| Binary Search | Search using missing count formula          |
| Optimized     | Yes (Binary Search: O(log N))               |

---

## 8. **Aggressive Cows Problem 🐄**

### 🔍 Problem Statement

You are given:

- `arr[]` of size `n`: positions of `n` stalls.
- An integer `k`: number of **aggressive cows**.

👉 **Goal**: Assign stalls to `k` cows so that **minimum distance between any two cows is maximized**.

---

### 🔗 Pre-requisite

- **Binary Search on Answers**
- **Greedy Placement**

---

### 🧪 Examples

#### Example 1:

```
Input: N = 6, k = 4, arr = [0,3,4,7,10,9]
Output: 3

Explanation:
Place cows at positions: [0, 3, 7, 10]
Distances: [3, 4, 3] → min = 3 → this is the maximum possible minimum distance.
```

#### Example 2:

```
Input: N = 5, k = 2, arr = [4,2,1,3,6]
Output: 5

Explanation:
Sorted: [1, 2, 3, 4, 6]
Place cows at: 1 and 6 → distance = 5 (maximized)
```

#### Example 3:

```
Input: N = 5, k = 3, arr = [1, 2, 8, 4, 9]
Output: 3

Explanation:
Place cows at: 1, 4, 8 → distances: [3, 4] → min = 3
```

#### Example 4:

```
Input: N = 4, k = 2, arr = [10, 20, 30, 40]
Output: 30
```

---

### 🧠 Intuition

We need to **maximize the minimum distance** → this means **Binary Search on Answer**.

- ✅ Range of answers → between `1` and `max(arr) - min(arr)`
- For each guess `mid`, check: **Can we place all cows with at least `mid` distance?**
- Use a **greedy approach** to check feasibility.

---

### 🧵 Dry Run

```text
arr = [0,3,4,7,10,9], k = 4
Sorted arr = [0,3,4,7,9,10]
Try distance = 3:
  Place first cow at 0
  Next: 3 (yes), 7 (yes), 10 (yes) → 4 cows placed ✅
Try 4:
  Place at 0 → next 4 (no), 7 (yes), 10 (no) → only 3 cows ❌
→ So max minimum distance = 3
```

---

### 💻 JavaScript Code

```javascript
function aggressiveCows(stalls, k) {
  stalls.sort((a, b) => a - b);

  const canPlaceCows = (minDist) => {
    let count = 1;
    let lastPos = stalls[0];

    for (let i = 1; i < stalls.length; i++) {
      if (stalls[i] - lastPos >= minDist) {
        count++;
        lastPos = stalls[i];
        if (count === k) return true;
      }
    }

    return false;
  };

  let low = 1;
  let high = stalls[stalls.length - 1] - stalls[0];
  let answer = 0;

  while (low <= high) {
    const mid = Math.floor((low + high) / 2);

    if (canPlaceCows(mid)) {
      answer = mid;
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  return answer;
}
```

---

#### ✅ Usage

```javascript
console.log(aggressiveCows([0, 3, 4, 7, 10, 9], 4)); // Output: 3
console.log(aggressiveCows([4, 2, 1, 3, 6], 2)); // Output: 5
console.log(aggressiveCows([1, 2, 8, 4, 9], 3)); // Output: 3
console.log(aggressiveCows([10, 20, 30, 40], 2)); // Output: 30
```

---

### ⏱ Time & Space Complexity

| Metric           | Value                |
| ---------------- | -------------------- |
| Time Complexity  | O(N \* log(maxDist)) |
| Space Complexity | O(1)                 |

---

### 📌 Summary

| Feature        | Description                                    |
| -------------- | ---------------------------------------------- |
| Input          | Stall positions `arr[]`, cows `k`              |
| Output         | Max possible min distance between any two cows |
| Algorithm Used | Binary Search on Answer + Greedy Feasibility   |
| Important Note | Must **sort stalls\[]** before applying logic  |

---

## 9. **Book Allocation Problem 📚**

### 🔍 Problem Statement

You are given an array `arr[]` where `arr[i]` denotes the **number of pages** in the `i-th` book. You are also given an integer `m`, the **number of students**.

👉 **Objective**: Allocate books to `m` students such that:

- Each student gets at least **one book**.
- Each book is given to **only one student**.
- Books are allocated in **contiguous** manner.
- Minimize the **maximum number of pages** a student has to read.

---

### ⚠️ Edge Condition

If `m > n` (more students than books), return `-1`.

---

### 🔗 Pre-requisite

- Binary Search on Answer
- Greedy partition logic

---

### 🧪 Examples

#### Example 1:

```
Input: n = 4, m = 2, arr = [12, 34, 67, 90]
Output: 113

Explanation:
Allocate: [12, 34, 67] | [90] → max pages = 113
```

#### Example 2:

```
Input: n = 5, m = 4, arr = [25, 46, 28, 49, 24]
Output: 71

Explanation:
Allocate: [25,46] | [28] | [49] | [24] → max pages = 71
```

#### Example 3:

```
Input: n = 3, m = 4, arr = [10, 20, 30]
Output: -1

Explanation:
Not enough books to allocate.
```

#### Example 4:

```
Input: n = 5, m = 2, arr = [10, 20, 30, 40, 50]
Output: 90

Explanation:
Allocate: [10,20,30] | [40,50] → max pages = 90
```

---

### 🧠 Intuition

- **Lower Bound**: max(arr), since at least one student must take the book with max pages.
- **Upper Bound**: sum(arr), if one student takes all the books.

✅ Apply **Binary Search** on the possible answer between `max(arr)` and `sum(arr)`, and check whether a configuration is **valid**.

---

### 💡 Greedy Function: Is allocation possible?

```javascript
function isValid(arr, maxPages, m) {
  let students = 1,
    pages = 0;

  for (let i = 0; i < arr.length; i++) {
    if (arr[i] > maxPages) return false;

    if (pages + arr[i] > maxPages) {
      students++;
      pages = arr[i];

      if (students > m) return false;
    } else {
      pages += arr[i];
    }
  }

  return true;
}
```

---

### 💻 JavaScript Code

```javascript
function allocateBooks(arr, m) {
  const n = arr.length;
  if (m > n) return -1;

  let low = Math.max(...arr);
  let high = arr.reduce((sum, val) => sum + val, 0);
  let result = -1;

  while (low <= high) {
    const mid = Math.floor((low + high) / 2);

    if (isValid(arr, mid, m)) {
      result = mid;
      high = mid - 1; // try smaller max
    } else {
      low = mid + 1;
    }
  }

  return result;
}
```

---

### 🧵 Dry Run

```text
arr = [12, 34, 67, 90], m = 2

low = 90, high = 203
mid = 146 → valid
mid = 118 → valid
mid = 104 → invalid
mid = 111 → invalid
mid = 114 → invalid
mid = 116 → invalid
mid = 117 → invalid
mid = 118 → valid → final result = 113 ✅
```

---

### ⏱ Time & Space Complexity

| Metric           | Value                  |
| ---------------- | ---------------------- |
| Time Complexity  | O(N \* log(Sum - Max)) |
| Space Complexity | O(1)                   |

---

### 📌 Summary

| Feature        | Description                                   |
| -------------- | --------------------------------------------- |
| Input          | Array of books and student count `m`          |
| Output         | Minimum of max pages any student has to read  |
| Edge Case      | If `m > n` return `-1`                        |
| Algorithm Used | Binary Search on Answers + Greedy Feasibility |

---

## 10. **Split Array to Minimize Largest Sum**

### 🔍 Problem Statement

You're given an array `nums` of integers and a number `k`.
Split `nums` into `k` **non-empty, contiguous subarrays** such that the **maximum sum of any subarray is minimized**.

👉 **Goal**: Minimize the **maximum subarray sum**.

---

### 🔗 Pre-requisite

- **Binary Search on Answers**
- **Greedy partitioning**

---

### 🧪 Examples

#### Example 1:

```
Input: nums = [7,2,5,10,8], k = 2
Output: 18

Explanation:
Split into: [7,2,5] and [10,8]
Sums: 14 and 18 → max = 18 (minimized)
```

#### Example 2:

```
Input: nums = [1,2,3,4,5], k = 2
Output: 9

Explanation:
Split into: [1,2,3] and [4,5]
Sums: 6 and 9 → max = 9
```

#### Example 3:

```
Input: nums = [1,4,4], k = 3
Output: 4

Explanation:
Each subarray will be a single element, so max sum is 4.
```

#### Example 4:

```
Input: nums = [10, 20, 30, 40], k = 2
Output: 60

Explanation:
Split: [10, 20, 30] and [40] → max = 60
```

---

### 🧠 Intuition

This is a **Binary Search on the Answer** problem.

- **Lower Bound**: `max(nums)` – one element is the minimum max we must allow.
- **Upper Bound**: `sum(nums)` – everything in one subarray.

We **binary search** between `max(nums)` and `sum(nums)` for the smallest value of max sum such that we can split into `k` or fewer subarrays.

---

### ✅ Greedy Check Function

```javascript
function isValid(nums, k, maxSum) {
  let subarrays = 1;
  let currentSum = 0;

  for (const num of nums) {
    if (currentSum + num > maxSum) {
      subarrays++;
      currentSum = num;
      if (subarrays > k) return false;
    } else {
      currentSum += num;
    }
  }

  return true;
}
```

---

### 💻 JavaScript Code

```javascript
function splitArray(nums, k) {
  let low = Math.max(...nums);
  let high = nums.reduce((sum, num) => sum + num, 0);
  let result = high;

  while (low <= high) {
    const mid = Math.floor((low + high) / 2);

    if (isValid(nums, k, mid)) {
      result = mid;
      high = mid - 1; // try to minimize
    } else {
      low = mid + 1;
    }
  }

  return result;
}
```

---

### 🧵 Dry Run

```text
nums = [7,2,5,10,8], k = 2
low = 10, high = 32

Try mid = 21 → valid
Try mid = 15 → not valid
Try mid = 18 → valid
Try mid = 16 → not valid
Try mid = 17 → not valid
Try mid = 18 → valid ✅
Final answer = 18
```

---

### ⏱ Time & Space Complexity

| Metric                     | Value          |
| -------------------------- | -------------- |
| Time Complexity            | O(N \* log(S)) |
| Where N = length of array, |                |
| S = sum of all elements.   |                |
| Space Complexity           | O(1)           |

---

### 📌 Summary

| Feature        | Description                              |
| -------------- | ---------------------------------------- |
| Input          | `nums[]`, `k` → split into `k` subarrays |
| Output         | Minimize the **max subarray sum**        |
| Algorithm Used | Binary Search on Answers + Greedy        |
| Edge Case      | All elements same → return that value    |

---

## 11. **Painter’s Partition Problem**

### 🔍 Problem Statement

You are given:

- An array `boards[]` of size `N` where each element represents the length of a board.
- An integer `K` denoting the number of painters.

🖌️ Each painter can **only paint a contiguous section** of boards.
⏱️ Painting 1 unit of board takes 1 unit of time.

**Return:** Minimum time required to paint all the boards using exactly `K` painters.

---

### 🔗 Pre-requisite

- **Binary Search on Answer**
- **Book Allocation Problem** (BS-18)

---

### 🧪 Examples

#### Example 1:

```
Input: N = 4, boards = [5, 5, 5, 5], K = 2
Output: 10

Explanation:
Partition: [5,5] and [5,5]
Time taken = max(10, 10) = 10
```

#### Example 2:

```
Input: N = 4, boards = [10, 20, 30, 40], K = 2
Output: 60

Explanation:
Partition: [10, 20, 30] and [40]
Time taken = max(60, 40) = 60
```

#### Example 3:

```
Input: N = 5, boards = [10, 30, 40, 20, 15], K = 3
Output: 55

Explanation: [10,30], [40], [20,15]
```

#### Example 4:

```
Input: N = 3, boards = [10, 10, 10], K = 1
Output: 30

Explanation: Only 1 painter → all boards assigned to him.
```

---

### 🧠 Intuition

- Painters can **only paint contiguous** boards.
- **We want to minimize the maximum units any single painter paints**.
- Similar to book allocation:

  - **Min value (low)** = max(boards\[])
  - **Max value (high)** = sum(boards\[])

---

### ⚙️ Greedy Helper Function: `countPainters`

```javascript
function countPainters(boards, maxTime) {
  let painters = 1;
  let total = 0;

  for (let board of boards) {
    if (total + board <= maxTime) {
      total += board;
    } else {
      painters++;
      total = board;
    }
  }

  return painters;
}
```

---

### 💻 JavaScript Code

```javascript
function findMinTime(boards, k) {
  let low = Math.max(...boards);
  let high = boards.reduce((a, b) => a + b, 0);
  let result = high;

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);
    let paintersNeeded = countPainters(boards, mid);

    if (paintersNeeded <= k) {
      result = mid;
      high = mid - 1; // try to minimize time
    } else {
      low = mid + 1;
    }
  }

  return result;
}
```

---

### 🧵 Dry Run

```text
boards = [10, 20, 30, 40], K = 2
low = 40, high = 100

Try mid = 70 → 2 painters → valid → update ans = 70
Try mid = 55 → 3 painters → invalid → move right
Try mid = 60 → 2 painters → valid → update ans = 60
Try mid = 50 → 3 painters → invalid
Try mid = 55 → 3 painters → invalid
Try mid = 56 → 3 → invalid → end
Final answer = 60
```

---

### ⏱ Time & Space Complexity

| Metric           | Value                                 |
| ---------------- | ------------------------------------- |
| Time Complexity  | O(N \* log S) where S = sum of boards |
| Space Complexity | O(1)                                  |

---

### 📌 Summary

| Feature        | Description                        |
| -------------- | ---------------------------------- |
| Input          | `boards[]`, number of painters `k` |
| Output         | Minimum time to paint all boards   |
| Constraints    | Only contiguous painting allowed   |
| Algorithm Used | Binary Search on Answer            |
| Lower Bound    | `max(boards[])`                    |
| Upper Bound    | `sum(boards[])`                    |

---

## 12. **Minimize Maximum Distance Between Gas Stations**

### 🔍 Problem Statement

You are given:

- An array `arr[]` of size `n` which contains **sorted positions** of existing gas stations on the X-axis.
- An integer `k` representing the number of **new gas stations** you can add.

You need to:
✅ Place the `k` new gas stations **only between** existing stations.
✅ **Minimize the maximum distance** `dist` between any two adjacent gas stations.

Return the minimum possible value of `dist` after placing all `k` stations.
🧠 **Answer must be correct up to 6 decimal places.**

---

### 🧪 Examples

#### Example 1:

```txt
Input: arr = [1, 2, 3, 4, 5], k = 4
Output: 0.5
Explanation:
Insert 1 station between each pair: [1, 1.5, 2, 2.5, 3, 3.5, 4, 4.5, 5]
Max distance between any two stations = 0.5
```

#### Example 2:

```txt
Input: arr = [1, 2, 3, 4], k = 1
Output: 1
Explanation:
Even if you place one gas station anywhere, at least one distance will still be 1.
```

#### Example 3:

```txt
Input: arr = [1, 10], k = 2
Output: 2
Explanation:
Insert two stations: [1, 3, 5, 7, 10]
All distances = 2 or less.
```

---

### 🧠 Intuition

- You can only place stations **between existing stations**, not before the first or after the last.
- For a **gap** of `length d`, if you insert `x` gas stations in that segment, the new maximum gap becomes `d / (x + 1)`.

To **minimize the maximum gap**, we must **distribute gas stations such that the largest segment distance is as small as possible**.

---

### 🔎 Binary Search on Answer

We will use **binary search on the value of `dist`**:

- Minimum possible distance `low = 0.0`
- Maximum possible distance `high = max(arr[i+1] - arr[i])`

#### 💡 Check Function

We need a helper function `isPossible(dist)`:

- Count how many gas stations are needed to ensure no gap > `dist`.
- For each gap:

  ```txt
  count += Math.floor((arr[i+1] - arr[i]) / dist)
  ```

- If `count <= k`, then it is **possible** to achieve `dist`.

---

### 💻 JavaScript Code

```javascript
function minimizeMaxDist(arr, k) {
  let low = 0.0,
    high = 0.0;
  let n = arr.length;

  for (let i = 0; i < n - 1; i++) {
    high = Math.max(high, arr[i + 1] - arr[i]);
  }

  function isPossible(dist) {
    let count = 0;
    for (let i = 0; i < n - 1; i++) {
      let gap = arr[i + 1] - arr[i];
      count += Math.floor(gap / dist);
    }
    return count <= k;
  }

  let eps = 1e-6;
  while (high - low > eps) {
    let mid = (low + high) / 2;
    if (isPossible(mid)) {
      high = mid;
    } else {
      low = mid;
    }
  }

  return high.toFixed(6);
}
```

---

### 🧵 Dry Run

```txt
arr = [1, 10], k = 2
low = 0.0, high = 9

Try mid = 4.5 → Need 2 stations → valid
Try smaller → mid = 2.25 → Need 3 stations → invalid
Try larger → mid = 3.4 → Need 2 stations → valid

Binary search continues until precision < 1e-6
```

---

### ⏱ Time & Space Complexity

| Metric           | Value                        |
| ---------------- | ---------------------------- |
| Time Complexity  | O(n \* log10^6) → O(n \* 60) |
| Space Complexity | O(1)                         |

---

### 🧠 Summary

| Component         | Description                              |
| ----------------- | ---------------------------------------- |
| Problem Type      | Binary Search on Answer                  |
| Key Concept       | Distribute k gas stations optimally      |
| Goal              | Minimize the maximum distance            |
| Precision         | Binary search until `high - low < 1e-6`  |
| Decision Function | Count gas stations needed for given dist |

---

## 13. **Median of Two Sorted Arrays**

### 🔍 Problem Statement

You are given two sorted arrays `nums1` and `nums2` of sizes `m` and `n`.

**Task:**
Return the **median** of the two sorted arrays.

📈 The overall run time complexity must be **O(log (m+n))**.

---

### 🔗 Pre-requisite

- **Binary Search on Partition**
- Knowledge of **median in arrays**
- Two-pointer vs Binary Search trade-off

---

### 🧪 Examples

#### Example 1:

```text
Input: nums1 = [1, 3], nums2 = [2]
Merged: [1, 2, 3]
Median = 2
```

#### Example 2:

```text
Input: nums1 = [1, 2], nums2 = [3, 4]
Merged: [1, 2, 3, 4]
Median = (2 + 3) / 2 = 2.5
```

#### Example 3:

```text
Input: nums1 = [], nums2 = [1]
Output: 1
```

#### Example 4:

```text
Input: nums1 = [0, 0], nums2 = [0, 0]
Output: 0
```

---

### 🧠 Intuition

- **Brute-force**: Merge both arrays → O(m+n)
- But we want **O(log(min(m, n)) time**.

🔍 **Idea**:

- We’ll binary search the smaller array.
- Partition both arrays such that:

  - Left half has ≤ right half values
  - Sizes of left and right are equal (or differ by 1)

💡 When valid partition is found:

- If odd total length: max(left part) is the median
- If even total length: median = (max of left + min of right) / 2

---

### ⚙️ Key Helper: Partition Logic

For arrays `A` and `B`, let:

- `i` = cut in `A`
- `j` = cut in `B` such that `i + j = (m + n + 1) / 2`

Now check if:

```
Aleft <= Bright and Bleft <= Aright
```

If not:

- If `Aleft > Bright` → move `i` left
- Else → move `i` right

---

### 💻 JavaScript Code

```javascript
function findMedianSortedArrays(nums1, nums2) {
  if (nums1.length > nums2.length) {
    [nums1, nums2] = [nums2, nums1];
  }

  const m = nums1.length,
    n = nums2.length;
  let low = 0,
    high = m;

  while (low <= high) {
    let i = Math.floor((low + high) / 2);
    let j = Math.floor((m + n + 1) / 2) - i;

    let Aleft = i === 0 ? -Infinity : nums1[i - 1];
    let Aright = i === m ? Infinity : nums1[i];
    let Bleft = j === 0 ? -Infinity : nums2[j - 1];
    let Bright = j === n ? Infinity : nums2[j];

    if (Aleft <= Bright && Bleft <= Aright) {
      if ((m + n) % 2 === 0) {
        return (Math.max(Aleft, Bleft) + Math.min(Aright, Bright)) / 2;
      } else {
        return Math.max(Aleft, Bleft);
      }
    } else if (Aleft > Bright) {
      high = i - 1;
    } else {
      low = i + 1;
    }
  }

  return 0; // Should never reach here
}
```

---

### 🧵 Dry Run

```text
nums1 = [1, 3]
nums2 = [2]

i = 1, j = 1
Aleft = 1, Aright = 3
Bleft = 2, Bright = ∞

Valid partition!
Odd length → median = max(1, 2) = 2
```

---

### ⏱ Time & Space Complexity

| Metric           | Value             |
| ---------------- | ----------------- |
| Time Complexity  | O(log(min(m, n))) |
| Space Complexity | O(1)              |

---

### 📌 Summary

| Feature    | Description                       |
| ---------- | --------------------------------- |
| Input      | Two sorted arrays nums1 and nums2 |
| Output     | Median value                      |
| Constraint | Run time must be O(log (m+n))     |
| Strategy   | Binary Search on Smaller Array    |
| Edge Cases | Empty arrays, even vs odd size    |

---

## 14. **Find the K-th Element in Two Sorted Arrays**

### 🔍 Problem Statement

You are given two sorted arrays of size `m` and `n` respectively.

**Task:**
Find the element that would be at the **k-th position (1-based)** in the final merged sorted array, **without merging them completely**.

---

### 🔗 Pre-requisite

- Binary Search
- Median of Two Sorted Arrays
- Lower Bound on Answer

---

### 🧪 Examples

#### Example 1:

```text
Input: nums1 = [2, 3, 6, 7, 9], nums2 = [1, 4, 8, 10], k = 5
Output: 6

Merged Array = [1, 2, 3, 4, 6, 7, 8, 9, 10]
5th element = 6
```

#### Example 2:

```text
Input: nums1 = [1, 2], nums2 = [3, 4, 5, 6], k = 4
Output: 4
```

#### Example 3:

```text
Input: nums1 = [100, 112, 256, 349, 770], nums2 = [72, 86, 113, 119, 265, 445, 892], k = 7
Output: 256
```

---

### 🧠 Intuition

We need to find the **k-th smallest element** between two sorted arrays.

### ❌ Brute Force

- Merge both arrays → then return `merged[k-1]`
- **Time:** O(k) or O(m + n)
- **Not optimal** when `m + n` is large

---

### ✅ Optimal Approach: Binary Search on Partition

Let’s do **binary search on the smaller array** to find how many elements from `nums1` we can take (say `cut1`), and take `cut2 = k - cut1` from `nums2`.

We ensure:

```
max(nums1[cut1 - 1], nums2[cut2 - 1]) <= min(nums1[cut1], nums2[cut2])
```

This ensures that all elements on the left of the partition are ≤ those on the right.

Once the partition is valid, the **k-th smallest element is**:

```
max(nums1[cut1 - 1], nums2[cut2 - 1])
```

---

### 💻 JavaScript Code

```javascript
function kthElement(nums1, nums2, k) {
  if (nums1.length > nums2.length) {
    [nums1, nums2] = [nums2, nums1]; // ensure nums1 is smaller
  }

  let m = nums1.length,
    n = nums2.length;
  let low = Math.max(0, k - n),
    high = Math.min(k, m);

  while (low <= high) {
    let cut1 = Math.floor((low + high) / 2);
    let cut2 = k - cut1;

    let l1 = cut1 === 0 ? -Infinity : nums1[cut1 - 1];
    let l2 = cut2 === 0 ? -Infinity : nums2[cut2 - 1];
    let r1 = cut1 === m ? Infinity : nums1[cut1];
    let r2 = cut2 === n ? Infinity : nums2[cut2];

    if (l1 <= r2 && l2 <= r1) {
      return Math.max(l1, l2);
    } else if (l1 > r2) {
      high = cut1 - 1;
    } else {
      low = cut1 + 1;
    }
  }

  return -1;
}
```

---

### 🧵 Dry Run

```text
nums1 = [2, 3, 6, 7, 9], nums2 = [1, 4, 8, 10], k = 5

cut1 = 3, cut2 = 2
l1 = 6, l2 = 4, r1 = 7, r2 = 8

=> Valid partition → max(6, 4) = 6
```

---

### ⏱ Time & Space Complexity

| Metric           | Value             |
| ---------------- | ----------------- |
| Time Complexity  | O(log(min(k, m))) |
| Space Complexity | O(1)              |

---

### 📌 Summary

| Feature      | Description                    |
| ------------ | ------------------------------ |
| Input        | Two sorted arrays + position k |
| Output       | The k-th smallest element      |
| Optimization | Binary Search on Smaller Array |
| Edge Cases   | k < size of smaller array      |
| Note         | 1-based indexing assumed for k |

---

# **Binary Search in 2D Arrays**

### ✅ There are **TWO Major Variants**:

### 💡 **Variant 1: Row-wise & Column-wise Sorted**

**Matrix Property:**

- Each row is **sorted in ascending order**.
- Each column is also **sorted in ascending order**.
- But the rows are **independent**, i.e., `matrix[i][j] <= matrix[i][j+1]` and `matrix[i][j] <= matrix[i+1][j]`

---

## 💡 **Variant 2: Fully Sorted 2D Matrix (1D View)**

**Matrix Property:**

- Each row is sorted.
- The **first element of each row is greater than the last element of the previous row.**
- Effectively, the entire 2D matrix is like a **sorted 1D array**.

---

#### Example:

```text
matrix = [
  [1, 3, 5, 7],
  [10, 11, 16, 20],
  [23, 30, 34, 60]
]
```

---

## 📎 Follow-up Variations

- K-th Smallest in Row-Col Sorted Matrix
- Search Range in Matrix
- Matrix Peak Element (2D Binary Search)

---

## 1. **Row with Maximum Number of 1s in Sorted Matrix**

### 🔍 Problem Statement

You are given a binary matrix `mat[][]` of size `n x m` containing only 0s and 1s.

**Important Condition:**
Each **row is sorted in non-decreasing order** → all 0s appear before 1s.

**Task:**
Return the **index** of the row with the **maximum number of 1s**.
If two rows have the same number of 1s, return the one with the **lower index**.
If there is **no 1 at all**, return `-1`.

---

### 🧪 Examples

#### Example 1:

```txt
Input:
n = 3, m = 3
mat = [
  [1, 1, 1],
  [0, 0, 1],
  [0, 0, 0]
]

Output: 0
Explanation: Row 0 has 3 ones (maximum).
```

#### Example 2:

```txt
Input:
n = 2, m = 2
mat = [
  [0, 0],
  [0, 0]
]

Output: -1
Explanation: No 1 found in any row.
```

---

### 🧠 Intuition

- Since each row is **sorted**, all 1s (if any) are on the **right**.
- The **first occurrence of 1** in a row tells us the count of 1s in that row: `count = m - indexOfFirst1`.
- We need to **minimize the index of first 1** to **maximize count**.

---

### ⚙️ Helper: First Occurrence of 1 using Binary Search

```javascript
function firstOneIndex(row) {
  let low = 0,
    high = row.length - 1;
  let index = row.length; // assume 1 not found

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);

    if (row[mid] === 1) {
      index = mid;
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }

  return index; // if not found, returns row.length
}
```

---

### 💻 JavaScript Code: Find Row with Max 1s

```javascript
function rowWithMaxOnes(mat) {
  let n = mat.length,
    m = mat[0].length;
  let maxOnes = 0;
  let resultRow = -1;

  for (let i = 0; i < n; i++) {
    let index = firstOneIndex(mat[i]);
    let onesCount = m - index;

    if (onesCount > maxOnes) {
      maxOnes = onesCount;
      resultRow = i;
    }
  }

  return maxOnes === 0 ? -1 : resultRow;
}
```

---

### 🧵 Dry Run

```txt
Input matrix:
[
  [1, 1, 1],  // index 0, first 1 at 0 → 3 ones
  [0, 0, 1],  // index 1, first 1 at 2 → 1 one
  [0, 0, 0]   // index 2, no 1 found
]

Row 0 → 3 ones (best so far)
Row 1 → 1 one
Row 2 → 0 ones
=> Return 0
```

---

### ⏱ Time & Space Complexity

| Metric           | Value         |
| ---------------- | ------------- |
| Time Complexity  | O(n \* log m) |
| Space Complexity | O(1)          |

---

### 🛠 Optimized Approach (O(N+M))

**Idea:**
Start from **top-right** and move:

- **Left** if we find a 1 (update best row)
- **Down** if we find a 0

```javascript
function rowWithMaxOnesOptimized(mat) {
  let n = mat.length,
    m = mat[0].length;
  let i = 0,
    j = m - 1;
  let maxRow = -1;

  while (i < n && j >= 0) {
    if (mat[i][j] === 1) {
      maxRow = i;
      j--; // move left
    } else {
      i++; // move down
    }
  }

  return maxRow;
}
```

✅ **Time Complexity:** `O(n + m)`
✅ **Space Complexity:** `O(1)`

---

### 📌 Summary

| Feature      | Description                          |
| ------------ | ------------------------------------ |
| Input        | Binary matrix with sorted rows       |
| Output       | Row index with maximum 1s            |
| Approach 1   | Binary Search per row → O(n log m)   |
| Approach 2   | Start from top-right corner → O(n+m) |
| Special Case | If no 1 is found, return -1          |

---

## 2. **Search a 2D Matrix (Binary Search on 2D)**

### 🔍 Problem Statement

You are given a 2D matrix `matrix` with `m` rows and `n` columns that satisfies:

1. **Each row is sorted** in non-decreasing order.
2. **First element of each row > last element of the previous row** (matrix is row-wise sorted like a 1D sorted array).

🎯 **Goal:** Given an integer `target`, return `true` if it's found in the matrix; otherwise, return `false`.

🕒 Must solve in `O(log(m * n))` time complexity.

---

### 🧪 Examples

#### Example 1:

```txt
Input: matrix = [
                 [1,3,5,7],
                 [10,11,16,20],
                 [23,30,34,60]],
       target = 3

Output: true
```

#### Example 2:

```txt
Input: matrix = [
                 [1,3,5,7],
                 [10,11,16,20],
                 [23,30,34,60]],
       target = 13

Output: false
```

---

### 🧠 Intuition

Even though it’s a 2D matrix, because:

- Each row is sorted.
- First element of each row > last element of previous row.

➡️ The entire matrix behaves like a **1D sorted array**.

We can **apply binary search** on this 1D representation, treating the 2D matrix as a flattened sorted list.

---

### 🗺️ Mapping 1D to 2D

For any index `mid` in the 1D version:

```js
row = Math.floor(mid / n);
col = mid % n;
value = matrix[row][col];
```

---

### 💻 JavaScript Code

```javascript
function searchMatrix(matrix, target) {
  let m = matrix.length;
  let n = matrix[0].length;

  let low = 0;
  let high = m * n - 1;

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);
    let row = Math.floor(mid / n);
    let col = mid % n;
    let value = matrix[row][col];

    if (value === target) return true;
    else if (value < target) low = mid + 1;
    else high = mid - 1;
  }

  return false;
}
```

---

### 🧵 Dry Run

```txt
matrix = [[1, 3, 5, 7],
          [10,11,16,20],
          [23,30,34,60]]
target = 16

m = 3, n = 4 → Total elements = 12
Search range: [0, 11]

mid = 5 → row = 1, col = 1 → matrix[1][1] = 11 → too small
mid = 8 → row = 2, col = 0 → matrix[2][0] = 23 → too large
mid = 6 → row = 1, col = 2 → matrix[1][2] = 16 ✅ Found!
```

---

### ⏱ Time & Space Complexity

| Metric           | Value           |
| ---------------- | --------------- |
| Time Complexity  | `O(log(m * n))` |
| Space Complexity | `O(1)`          |

---

### 📌 Summary

| Feature     | Description                          |
| ----------- | ------------------------------------ |
| Input       | `matrix[][]`, `target`               |
| Output      | `true` if found, else `false`        |
| Matrix Type | 2D but sorted like 1D                |
| Core Idea   | Binary Search on 1D → map back to 2D |
| Complexity  | O(log(m \* n)) time, O(1) space      |

---

## 3. **Search in 2D Matrix II**

### 🔍 Problem Statement

You are given an `m x n` matrix with the following properties:

1. Each row is sorted from **left to right**.
2. Each column is sorted from **top to bottom**.

🎯 **Goal:** Return `true` if the target exists in the matrix, otherwise return `false`.

---

### 🧪 Examples

#### Example 1:

```
Input:
matrix = [
          [1,  4,  7, 11, 15],
          [2,  5,  8, 12, 19],
          [3,  6,  9, 16, 22],
          [10,13, 14,17, 24],
          [18,21, 23,26, 30]]
target = 5

Output: true
```

#### Example 2:

```
Input:
matrix = [
          [1,  4,  7, 11, 15],
          [2,  5,  8, 12, 19],
          [3,  6,  9, 16, 22],
          [10,13, 14,17, 24],
          [18,21, 23,26, 30]]
target = 20

Output: false
```

---

### 🧠 Intuition

- Start from **top-right corner** of the matrix:

  - If `matrix[i][j] == target` → ✅ Found
  - If `matrix[i][j] > target` → Move **left** (column--)
  - If `matrix[i][j] < target` → Move **down** (row++)

Why does this work?

- From top-right:

  - Going left → values decrease.
  - Going down → values increase.

- This lets us **eliminate a row or a column** in each step → O(m + n)

---

### 💻 JavaScript Code

```javascript
function searchMatrix(matrix, target) {
  let m = matrix.length;
  let n = matrix[0].length;

  let row = 0;
  let col = n - 1;

  while (row < m && col >= 0) {
    let value = matrix[row][col];

    if (value === target) return true;
    else if (value > target) col--; // move left
    else row++; // move down
  }

  return false;
}
```

---

### 🧵 Dry Run

```txt
Target = 16
Start at matrix[0][4] = 15 → too small → move down
matrix[1][4] = 19 → too big → move left
matrix[1][3] = 12 → too small → move down
matrix[2][3] = 16 → ✅ Found
```

---

### ⏱ Time & Space Complexity

| Metric           | Value    |
| ---------------- | -------- |
| Time Complexity  | O(m + n) |
| Space Complexity | O(1)     |

---

### 📌 Summary

| Feature           | Description                             |
| ----------------- | --------------------------------------- |
| Input             | `matrix[][]`, `target`                  |
| Output            | `true` if found, else `false`           |
| Matrix Properties | Sorted rows & columns                   |
| Approach          | Top-Right Pointer Shrinkage             |
| Time Complexity   | O(m + n)                                |
| Better Than       | Brute-force O(m\*n), O(log(m\*n)) fails |

---

## 4. **2D Peak Element (Binary Search in 2D)**

### 🔍 Problem Statement

A **peak element** in a 2D matrix is one that is **strictly greater** than all its **4-directional neighbors**: left, right, top, and bottom.

You are given a matrix `mat` of size `m x n`. Return any **position `[i, j]`** of a peak.

**Constraints**:

- Every cell has **unique** adjacent values (i.e. no two adjacent cells are equal).
- Matrix is surrounded by virtual cells of `-1`.
- You must solve this in **O(m log n)** or **O(n log m)** time.

---

### 🧪 Examples

#### Example 1:

```
Input: mat = [[1, 4],
              [3, 2]]

Output: [0, 1] or [1, 0]

Explanation: 4 > 1 & 2, and 3 > 1 & 2
```

#### Example 2:

```
Input: mat = [
              [10, 20, 15],
              [21, 30, 14],
              [7,  16, 32]
             ]

Output: [1, 1] or [2, 2]

Explanation: 30 and 32 are both peak elements.
```

---

### 🧠 Intuition

We cannot do brute force (`O(m * n)`), so we use **Binary Search on columns** or **rows**.

We pick a **middle column**, find the **maximum element in that column**, and compare it with its neighbors (left and right). Based on that:

- If the max is a peak, return it.
- If left neighbor is greater → move left half.
- If right neighbor is greater → move right half.

This way, we **reduce the search space by half** each time → like binary search.

---

### 💻 JavaScript Code (O(m log n))

```javascript
function findPeakGrid(mat) {
  const m = mat.length;
  const n = mat[0].length;

  let left = 0;
  let right = n - 1;

  while (left <= right) {
    const midCol = Math.floor((left + right) / 2);

    // Find max in midCol
    let maxRow = 0;
    for (let row = 0; row < m; row++) {
      if (mat[row][midCol] > mat[maxRow][midCol]) {
        maxRow = row;
      }
    }

    const leftVal = midCol > 0 ? mat[maxRow][midCol - 1] : -1;
    const rightVal = midCol < n - 1 ? mat[maxRow][midCol + 1] : -1;

    if (mat[maxRow][midCol] > leftVal && mat[maxRow][midCol] > rightVal) {
      return [maxRow, midCol];
    } else if (leftVal > mat[maxRow][midCol]) {
      right = midCol - 1;
    } else {
      left = midCol + 1;
    }
  }

  return [-1, -1]; // Should not happen based on constraints
}
```

---

### 🧵 Dry Run

```txt
Input: mat = [[10, 20, 15],
              [21, 30, 14],
              [7,  16, 32]]

→ midCol = 1
→ maxRow in col 1 = row 1 (value = 30)

Check neighbors: 21 (left) & 14 (right)
→ 30 > both → return [1,1]
```

---

### ⏱ Time & Space Complexity

| Metric           | Value      |
| ---------------- | ---------- |
| Time Complexity  | O(m log n) |
| Space Complexity | O(1)       |

---

### 📌 Summary

| Feature         | Description                        |
| --------------- | ---------------------------------- |
| Input           | 2D matrix with sorted neighbors    |
| Output          | Index `[i, j]` of any peak element |
| Constraints     | No two adjacent elements are equal |
| Optimization    | Binary Search on Columns (or Rows) |
| Time Complexity | O(m log n) or O(n log m)           |

---

## 5. **Median in a Row-wise Sorted Matrix**

### 🔍 Problem Statement

You are given a `M x N` matrix where **each row is sorted in non-decreasing order**.

You need to find the **median** of all elements in the matrix.
Note: The total number of elements `M * N` is **odd**, so the median is always a single integer.

---

### 🧪 Examples

#### Example 1:

```
Input:
M = 3, N = 3
matrix = [
  [1, 4, 9],
  [2, 5, 6],
  [3, 8, 7]
]

Result: 5

Explanation:
Flattened & sorted array: [1, 2, 3, 4, 5, 6, 7, 8, 9]
Median = 5 (middle element)
```

#### Example 2:

```
Input:
M = 3, N = 3
matrix = [
  [1, 3, 8],
  [2, 3, 4],
  [1, 2, 5]
]

Result: 3

Explanation:
Flattened & sorted array: [1, 1, 2, 2, 3, 3, 4, 5, 8]
Median = 3
```

---

### 🧠 Intuition

You **cannot flatten and sort the matrix** directly → **O(M \* N log(M \* N))** is too slow.

Instead, use **Binary Search on Answer**!

- The **minimum** value will lie between `min(matrix[i][0])`
- The **maximum** value will lie between `max(matrix[i][N-1])`
- Goal: Binary search for the smallest number `X` such that **at least (M\*N)/2 + 1** numbers are ≤ `X`

Use a helper function to **count how many elements are ≤ mid** in each row using **upper bound logic (binary search)**.

---

### ⚙️ Helper Function: Count of Elements ≤ Mid

```javascript
function upperBound(row, target) {
  let low = 0,
    high = row.length;
  while (low < high) {
    let mid = Math.floor((low + high) / 2);
    if (row[mid] <= target) {
      low = mid + 1;
    } else {
      high = mid;
    }
  }
  return low; // number of elements <= target
}
```

---

### 💻 JavaScript Code

```javascript
function findMedian(matrix, m, n) {
  let low = 1;
  let high = 1e9;

  const desired = Math.floor((m * n) / 2);

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);
    let count = 0;

    for (let i = 0; i < m; i++) {
      count += upperBound(matrix[i], mid);
    }

    if (count <= desired) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  return low;
}
```

---

### 🧵 Dry Run

```txt
matrix = [
  [1, 3, 8],
  [2, 3, 4],
  [1, 2, 5]
]

Total elements = 9
Desired count = 4 (we need 5th element)

Binary search on range [1, 1e9]
mid = 5 → count = 7 → enough → move left
mid = 3 → count = 5 → enough → move left
mid = 2 → count = 3 → too few → move right

Eventually → answer = 3
```

---

### ⏱ Time & Space Complexity

| Metric           | Value                           |
| ---------------- | ------------------------------- |
| Time Complexity  | O(log(max - min) \* M \* log N) |
| Space Complexity | O(1)                            |

---

### 📌 Summary

| Feature       | Description                   |
| ------------- | ----------------------------- |
| Input         | Matrix of dimensions `M x N`  |
| Output        | Median value of the matrix    |
| Constraint    | Each row is sorted            |
| Optimization  | Binary Search on Answer       |
| Key Operation | Count how many elements ≤ mid |

---
