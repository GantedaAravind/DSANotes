# 📦 Arrays

## 📘 **Definition**:

An **Array** is a **collection of elements** stored in **contiguous memory locations** and accessed using **index numbers**.

It’s like a row of boxes 📦📦📦📦 where each box holds a value, and every box has a number (index) to find it.

---

## 🧠 Think of it like this:

> Imagine a row of lockers, each labeled with a number (index) and holding a value.

```
Index:   0   1   2   3   4
Value: [10, 20, 30, 40, 50]
```

- `arr[0]` = 10
- `arr[2]` = 30

---

## 🧑‍💻 JavaScript Example:

```javascript
let numbers = [10, 20, 30, 40, 50];

console.log(numbers[0]); // 10
console.log(numbers[2]); // 30
```

---

## 📚 Key Features of Arrays:

| Feature               | Description                           |
| --------------------- | ------------------------------------- |
| **Fixed size**        | (in low-level languages like C/C++)   |
| **Index-based**       | Access elements using index (0-based) |
| **Contiguous memory** | Stored together in memory             |
| **Same data type**    | (in some languages)                   |

---

## 🔧 Operations You Can Do:

| Operation         | Example in JS                     | Time Complexity |
| ----------------- | --------------------------------- | --------------- |
| Access element    | `arr[2]` → 30                     | O(1)            |
| Insert at end     | `arr.push(60)`                    | O(1)            |
| Insert at start   | `arr.unshift(5)`                  | O(n)            |
| Delete from end   | `arr.pop()`                       | O(1)            |
| Delete from start | `arr.shift()`                     | O(n)            |
| Traverse (loop)   | `for(let i=0; i<arr.length; i++)` | O(n)            |

---

## 🎯 Real Life Use Cases:

- Storing list of student marks
- Storing temperatures of the week
- Holding positions of game players
- Arrays are used to build other data structures like stacks, queues, heaps, etc.

---

## 🆚 Bonus: Array vs Object in JS

| Feature | Array                   | Object                      |
| ------- | ----------------------- | --------------------------- |
| Indexed | By numbers (0, 1, 2...) | By keys (name, age...)      |
| Order   | Ordered                 | Not guaranteed              |
| Syntax  | `arr[0]`                | `obj.name` or `obj["name"]` |

---

# Easy Problems

## ✅ 1. **Find the Largest Element in an Array**

Given an array of `n` integers, find the **largest element** in the array.

---

### 🧪 Test Cases

#### Test Case 1:

```javascript
Input: [5, 1, 8, 3, 10, 2];
Output: 10;
```

#### Test Case 2:

```javascript
Input: [-5, -9, -3, -1];
Output: -1;
```

#### Test Case 3:

```javascript
Input: [100];
Output: 100;
```

---

### 💡 Intuition

We want to find the **maximum number** in the array.

- Start by assuming the **first element** is the largest.
- Then **scan each element** in the array.
- If you find any element **greater** than your current largest, **update** the largest.

Simple, right? This is a **linear scan** from left to right.

---

### 🔄 Dry Run

Let's dry run this input:

```javascript
arr = [5, 1, 8, 3, 10, 2];
```

1. Start: `max = 5`
2. Compare `1` → `max = 5`
3. Compare `8` → `8 > 5` → update `max = 8`
4. Compare `3` → `max = 8`
5. Compare `10` → `10 > 8` → update `max = 10`
6. Compare `2` → `max = 10`
   ✅ Final Answer: `10`

---

### 🧑‍💻 Code (JavaScript)

```javascript
function findLargestElement(arr) {
  if (arr.length === 0) return null; // Edge case

  let max = arr[0]; // Assume first element is max

  for (let i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
      max = arr[i]; // Update if we find a larger element
    }
  }

  return max;
}

// Test
console.log(findLargestElement([5, 1, 8, 3, 10, 2])); // Output: 10
console.log(findLargestElement([-5, -9, -3, -1])); // Output: -1
console.log(findLargestElement([100])); // Output: 100
```

---

### ⏱️ Time & Space Complexity

#### ⏳ Time Complexity: `O(n)`

- We go through all `n` elements **once**.
- No nested loops — just a single linear pass.

#### 🗂️ Space Complexity: `O(1)`

- No extra data structures used.
- Only one variable (`max`) to store result.

---

## ✅ 2. **Second Largest Element in an Array (without sorting)**

Given an array of integers, find the **second largest element** in the array **without sorting it**.

- If the array has fewer than 2 unique elements, return `null` or handle as needed.

---

### 🧪 2. Test Cases

#### Test Case 1:

```javascript
Input: [12, 35, 1, 10, 34, 1];
Output: 34;
```

#### Test Case 2:

```javascript
Input: [10, 5, 10];
Output: 5;
```

#### Test Case 3:

```javascript
Input: [10];
Output: null;
```

#### Test Case 4:

```javascript
Input: [10, 10, 10];
Output: null;
```

---

### 💡 Intuition

To find the **second largest** without sorting:

- Traverse the array once to find the **largest**.
- Traverse it again to find the **largest element smaller than the maximum**.

But to optimize:

- We can do both in **one pass** by maintaining two variables:

  - `first` → largest so far
  - `second` → second largest so far

Update them during traversal based on conditions.

---

### 🔄 Dry Run

Let’s dry run for:

```javascript
arr = [12, 35, 1, 10, 34, 1];
```

Initialize: `first = -∞`, `second = -∞`

- `12` → first = 12, second = -∞
- `35` → 35 > 12 → first = 35, second = 12
- `1` → no change
- `10` → 10 > second → second = 12 → no change
- `34` → 34 < 35 && 34 > second → second = 34
- `1` → no change

✅ Final result: `second = 34`

---

### 🧑‍💻 Code (JavaScript)

```javascript
function findSecondLargest(arr) {
  if (arr.length < 2) return null;

  let first = -Infinity;
  let second = -Infinity;

  for (let num of arr) {
    if (num > first) {
      second = first;
      first = num;
    } else if (num > second && num !== first) {
      second = num;
    }
  }

  // If second is still -Infinity, there's no second largest
  return second === -Infinity ? null : second;
}

// Tests
console.log(findSecondLargest([12, 35, 1, 10, 34, 1])); // 34
console.log(findSecondLargest([10, 5, 10])); // 5
console.log(findSecondLargest([10])); // null
console.log(findSecondLargest([10, 10, 10])); // null
```

---

### ⏱️ Time & Space Complexity

#### ⏳ Time Complexity: `O(n)`

- We traverse the array only **once**, comparing each element.
- Efficient even for large arrays.

#### 🗂️ Space Complexity: `O(1)`

- We use only two variables: `first` and `second`.

---

## ✅ 3. **Check if the Array is Sorted**

Given an array of integers, determine whether the array is **sorted in non-decreasing order** (i.e., each element is **greater than or equal to the previous one**).

Return `true` if the array is sorted, otherwise return `false`.

---

### 🧪 Test Cases

#### Test Case 1:

```javascript
Input: [1, 2, 3, 4, 5];
Output: true;
```

#### Test Case 2:

```javascript
Input: [1, 2, 2, 3, 5];
Output: true;
```

#### Test Case 3:

```javascript
Input: [5, 4, 3, 2, 1];
Output: false;
```

#### Test Case 4:

```javascript
Input: [10];
Output: true;
```

#### Test Case 5:

```javascript
Input: [];
Output: true; // empty array is considered sorted
```

---

### 💡 Intuition

To check if an array is sorted in non-decreasing order:

- Start from the second element (`index = 1`)
- Compare it with the previous element
- If **any element is smaller than its previous**, the array is **not sorted**

This needs only a **single pass**, no extra space, and no sorting.

---

### 🔄 Dry Run

Let’s dry run this input:

```javascript
arr = [1, 2, 2, 3, 5];
```

Start from index `1`:

- `2 >= 1` → OK
- `2 >= 2` → OK
- `3 >= 2` → OK
- `5 >= 3` → OK

✅ All comparisons passed → array is sorted → return `true`

---

### 🧑‍💻 JavaScript Code

```javascript
function isSorted(arr) {
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] < arr[i - 1]) {
      return false; // found an unsorted pair
    }
  }
  return true;
}

// Test cases
console.log(isSorted([1, 2, 3, 4, 5])); // true
console.log(isSorted([1, 2, 2, 3, 5])); // true
console.log(isSorted([5, 4, 3, 2, 1])); // false
console.log(isSorted([10])); // true
console.log(isSorted([])); // true
```

---

### ⏱️ Time and Space Complexity

### ⏳ Time Complexity: `O(n)`

- Single loop through the array with `n` elements.

### 🗂️ Space Complexity: `O(1)`

- No extra space used.

---

### ✅ Final Notes:

- You can modify the comparison to check for **strictly increasing** by using `arr[i] <= arr[i - 1]`
- To check **non-increasing**, flip the condition: `arr[i] > arr[i - 1]`

---

## ✅ 4. **Remove Duplicates from a Sorted Array**

You are given a **sorted array** (in non-decreasing order). Your task is to **remove the duplicate elements in-place**, so that each unique element appears **only once**.

You must return the **new length** of the array (with unique elements), and the array should be modified **in-place** (i.e., no extra space should be used for another array).

> You do **not** need to return the modified array itself, just the **length of the unique part**.

---

### 🧪 Test Cases

#### Test Case 1:

```javascript
Input: [1, 1, 2]
Output: 2
Modified array: [1, 2, _] (ignore elements beyond new length)
```

#### Test Case 2:

```javascript
Input: [0,0,1,1,1,2,2,3,3,4]
Output: 5
Modified array: [0, 1, 2, 3, 4, _, _, _, _, _]
```

#### Test Case 3:

```javascript
Input: [1,2,3]
Output: 3 (no duplicates)
```

#### Test Case 4:

```javascript
Input: [1,1,1,1]
Output: 1 (all elements same)
```

---

### 💡 Intuition

Since the array is already **sorted**, all duplicates will be **next to each other**. So we can use the **two-pointer approach**:

- Use one pointer (`i`) to **track the position of the last unique element**
- Use another pointer (`j`) to **scan the array**
- When you find a new unique element at `j`, move it to `i+1`, and increment `i`

This method lets us **overwrite** the duplicates with unique values **in-place**.

---

### 🔄 Dry Run

For input:

```js
arr = [0, 0, 1, 1, 2];
```

Start:

- `i = 0` (last unique position)
- Start `j` from 1

| j   | arr\[j] | arr\[i] | Action                          | arr after step   |
| --- | ------- | ------- | ------------------------------- | ---------------- |
| 1   | 0       | 0       | Duplicate → do nothing          | \[0, 0, 1, 1, 2] |
| 2   | 1       | 0       | New element → `i++`, `arr[i]=1` | \[0, 1, 1, 1, 2] |
| 3   | 1       | 1       | Duplicate → do nothing          | \[0, 1, 1, 1, 2] |
| 4   | 2       | 1       | New element → `i++`, `arr[i]=2` | \[0, 1, 2, 1, 2] |

✅ Final result:

- `i = 2`
- New length = `i + 1 = 3`
- Unique part: `[0, 1, 2]`

---

### 🧑‍💻 JavaScript Code

```javascript
function removeDuplicates(nums) {
  if (nums.length === 0) return 0;

  let i = 0; // index of last unique element

  for (let j = 1; j < nums.length; j++) {
    if (nums[j] !== nums[i]) {
      i++;
      nums[i] = nums[j]; // move unique element forward
    }
  }

  return i + 1; // length of unique portion
}

// Test Cases
const arr = [0, 0, 1, 1, 2];
const newLength = removeDuplicates(arr);
console.log(newLength); // 3
console.log(arr.slice(0, newLength)); // [0, 1, 2]
```

---

### ⏱️ Time & Space Complexity

#### ⏳ Time Complexity: `O(n)`

- We traverse the array only **once**.

#### 🗂️ Space Complexity: `O(1)`

- We **do not use extra space**, only index variables.

---

### 🧠 Key Points Recap

- Use the **two-pointer technique** for in-place updates.
- Sorted nature helps to easily spot duplicates.
- Final array doesn't need to be fully cleaned beyond `newLength`.

---

## ✅ 5. **Left Rotate an Array by One Place**

Given an array of size `n`, **rotate** the array **to the left by one position**.

> Each element should shift one position to the left, and the **first element should move to the end**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: [1, 2, 3, 4, 5];
Output: [2, 3, 4, 5, 1];
```

#### Test Case 2:

```js
Input: [10, 20, 30];
Output: [20, 30, 10];
```

#### Test Case 3:

```js
Input: [5];
Output: [5]; // Single element remains unchanged
```

#### Test Case 4:

```js
Input: [];
Output: []; // Empty array remains unchanged
```

---

### 💡 Intuition

In a **left rotation by one place**, every element shifts one index to the **left**:

- The element at index `1` moves to `0`
- The element at index `2` moves to `1`
- ...
- The **first element (index 0)** moves to the **end** of the array

To do this:

1. **Store the first element** in a temporary variable
2. **Shift all elements one position to the left**
3. Place the stored first element at the **end**

This ensures **in-place** modification with **O(1)** extra space.

---

### 🔄 Dry Run

Input:

```js
arr = [1, 2, 3, 4, 5];
```

1. Save `temp = arr[0] = 1`
2. Shift elements:

   - arr\[0] = arr\[1] → 2
   - arr\[1] = arr\[2] → 3
   - arr\[2] = arr\[3] → 4
   - arr\[3] = arr\[4] → 5

3. Place temp at end: `arr[4] = temp = 1`

✅ Final array: `[2, 3, 4, 5, 1]`

---

### 🧑‍💻 JavaScript Code

```javascript
function leftRotateByOne(arr) {
  if (arr.length <= 1) return arr; // No rotation needed

  const temp = arr[0]; // Step 1: Store first element

  for (let i = 0; i < arr.length - 1; i++) {
    arr[i] = arr[i + 1]; // Step 2: Shift left
  }

  arr[arr.length - 1] = temp; // Step 3: Put first at last
  return arr;
}

// Test
console.log(leftRotateByOne([1, 2, 3, 4, 5])); // [2, 3, 4, 5, 1]
console.log(leftRotateByOne([10, 20, 30])); // [20, 30, 10]
console.log(leftRotateByOne([5])); // [5]
console.log(leftRotateByOne([])); // []
```

---

### ⏱️ Time & Space Complexity

#### ⏳ Time Complexity: `O(n)`

- One pass to shift elements (`n-1` operations).

#### 🗂️ Space Complexity: `O(1)`

- Only one temp variable used (no extra array).

---

### 📌 Final Notes

- This is a fundamental operation often used in **circular queues**, **rotation-based problems**, and **array manipulations**.
- If you want to rotate the array **`k` times**, you'd repeat this process `k` times, or use an optimized version with reversal technique.

---

## ✅ 6. **Left Rotate an Array by D Places**

You are given an array of size `n` and an integer `d`. Your task is to **left-rotate** the array by `d` places.

> In a **left rotation**, each element of the array shifts to its **left by one position**, and the elements that fall off the start go to the **end** of the array.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: (arr = [1, 2, 3, 4, 5]), (d = 2);
Output: [3, 4, 5, 1, 2];
```

#### Test Case 2:

```js
Input: (arr = [10, 20, 30, 40, 50]), (d = 4);
Output: [50, 10, 20, 30, 40];
```

#### Test Case 3:

```js
Input: (arr = [1, 2, 3]), (d = 3);
Output: [1, 2, 3]; // Full rotation = original array
```

#### Test Case 4:

```js
Input: (arr = []), (d = 1);
Output: []; // Edge case
```

---

### 💡 Intuition

To rotate left by `d` places:

- Elements from index `0` to `d-1` should move to the **end**
- Elements from index `d` to `n-1` should shift to the **start**

So we can do this:

1. **Split the array** into two parts:

   - First part: `arr[0...d-1]`
   - Second part: `arr[d...n-1]`

2. **Concatenate** them: `second part + first part`

> To rotate in-place (without using extra array), we can use the **Reversal Algorithm**.

---

### 🔄 Dry Run

Input:

```js
(arr = [1, 2, 3, 4, 5]), (d = 2);
```

Split:

- First part: \[1, 2]
- Second part: \[3, 4, 5]

New array = \[3, 4, 5] + \[1, 2]
✅ Output: `[3, 4, 5, 1, 2]`

---

### 🧑‍💻 JavaScript Code

#### ✅ Approach 1: Using Array Slicing (Simple but uses extra space)

```javascript
function leftRotate(arr, d) {
  const n = arr.length;
  if (n === 0) return [];

  d = d % n; // In case d > n
  const rotated = arr.slice(d).concat(arr.slice(0, d));
  return rotated;
}

// Test
console.log(leftRotate([1, 2, 3, 4, 5], 2)); // [3, 4, 5, 1, 2]
```

---

#### ✅ Approach 2: In-place Reversal Algorithm (Optimal, O(1) space)

Steps:

1. Reverse first `d` elements
2. Reverse the remaining `n - d` elements
3. Reverse the whole array

### 🧪 Dry Run: Left Rotate by `d = 2`

```js
Input: (arr = [1, 2, 3, 4, 5]), (d = 2);
```

#### ✅ Step 1: Reverse first `d` elements → `arr[0...1]`

Reverse `[1, 2]` → becomes `[2, 1]`
**Array now:**

```
[2, 1, 3, 4, 5]
```

---

#### ✅ Step 2: Reverse remaining `n-d` elements → `arr[2...4]`

Reverse `[3, 4, 5]` → becomes `[5, 4, 3]`
**Array now:**

```
[2, 1, 5, 4, 3]
```

---

#### ✅ Step 3: Reverse the whole array → `arr[0...4]`

Reverse `[2, 1, 5, 4, 3]` → becomes `[3, 4, 5, 1, 2]`
**Final rotated array:**

```
[3, 4, 5, 1, 2]
```

```javascript
function reverse(arr, start, end) {
  while (start < end) {
    [arr[start], arr[end]] = [arr[end], arr[start]];
    start++;
    end--;
  }
}

function leftRotateInPlace(arr, d) {
  const n = arr.length;
  if (n === 0) return arr;

  d = d % n;

  reverse(arr, 0, d - 1);
  reverse(arr, d, n - 1);
  reverse(arr, 0, n - 1);

  return arr;
}

// Test
let arr = [1, 2, 3, 4, 5];
leftRotateInPlace(arr, 2);
console.log(arr); // [3, 4, 5, 1, 2]
```

---

### ⏱️ Time & Space Complexity

#### 🔁 Time Complexity:

- **O(n)** in both approaches
  (Traverses or reverses all `n` elements once)

#### 🧠 Space Complexity:

- **Approach 1 (Slice)**: `O(n)` due to new array
- **Approach 2 (In-place reversal)**: `O(1)` space, best for interviews!

---

### ✅ Recap:

| Approach        | Time | Space | Notes                        |
| --------------- | ---- | ----- | ---------------------------- |
| Slicing         | O(n) | O(n)  | Simple but uses extra memory |
| Reversal method | O(n) | O(1)  | In-place, most optimal       |

---

## ✅ 7. **Move All Zeros to the End of the Array**

Given an array of integers, **move all the zeros to the end** of the array **without changing the order of non-zero elements**.
The operation should be **in-place** (i.e., no new array should be created).

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: [0, 1, 0, 3, 12];
Output: [1, 3, 12, 0, 0];
```

#### Test Case 2:

```js
Input: [1, 2, 3, 4];
Output: [1, 2, 3, 4]; // No zeros to move
```

#### Test Case 3:

```js
Input: [0, 0, 0, 0];
Output: [0, 0, 0, 0]; // All zeros
```

#### Test Case 4:

```js
Input: [0, 0, 1];
Output: [1, 0, 0];
```

---

### 💡 Intuition

We want to move all zeros to the end, but **preserve the relative order** of non-zero elements.

Approach:

- Use a **two-pointer technique**:

  - One pointer (`i`) to **scan the array**
  - Another pointer (`j`) to **mark the position to place the next non-zero**

Steps:

1. Traverse the array
2. When a non-zero is found at `i`, move it to index `j`, then increment `j`
3. After all non-zero elements are placed, fill the rest of the array from `j` onward with `0`s

This approach maintains order and works in-place.

---

### 🔄 Dry Run

Input:

```js
arr = [0, 1, 0, 3, 12];
```

Initial: `j = 0`

- `i=0`: arr\[0] = 0 → skip
- `i=1`: arr\[1] = 1 → move to arr\[0], now `arr = [1, 1, 0, 3, 12]`, `j++ → 1`
- `i=2`: arr\[2] = 0 → skip
- `i=3`: arr\[3] = 3 → move to arr\[1], now `arr = [1, 3, 0, 3, 12]`, `j++ → 2`
- `i=4`: arr\[4] = 12 → move to arr\[2], now `arr = [1, 3, 12, 3, 12]`, `j++ → 3`

Now fill zeros from `j=3` onward:

- arr\[3] = 0
- arr\[4] = 0

✅ Final array: `[1, 3, 12, 0, 0]`

---

### 🧑‍💻 JavaScript Code

```javascript
function moveZerosToEnd(arr) {
  let j = 0; // Pointer for placing non-zero elements

  // First pass: Move non-zeros to front
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] !== 0) {
      arr[j] = arr[i];
      j++;
    }
  }

  // Second pass: Fill the rest with zeros
  while (j < arr.length) {
    arr[j] = 0;
    j++;
  }

  return arr;
}

// Test
console.log(moveZerosToEnd([0, 1, 0, 3, 12])); // [1, 3, 12, 0, 0]
console.log(moveZerosToEnd([0, 0, 1])); // [1, 0, 0]
console.log(moveZerosToEnd([1, 2, 3, 4])); // [1, 2, 3, 4]
console.log(moveZerosToEnd([0, 0, 0, 0])); // [0, 0, 0, 0]
```

---

### ⏱️ Time & Space Complexity

#### ⏳ Time Complexity: `O(n)`

- We go through the array **twice** (once to move, once to fill zeros)

#### 🗂️ Space Complexity: `O(1)`

- No extra space used, only pointer variables

---

### ✅ Summary

| Feature         | Value       |
| --------------- | ----------- |
| Approach        | Two-pointer |
| Time            | O(n)        |
| Space           | O(1)        |
| In-place        | ✅ Yes      |
| Order Preserved | ✅ Yes      |

---

## ✅ 8. **Linear Search**

You are given an array `arr[]` and a value `target`. Your task is to **find the index of the target** in the array using **Linear Search**.

> If the element is **present**, return its **first occurrence index**.
> If it is **not found**, return `-1`.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: (arr = [10, 20, 30, 40]), (target = 30);
Output: 2;
```

#### Test Case 2:

```js
Input: (arr = [5, 6, 7, 8]), (target = 9);
Output: -1;
```

#### Test Case 3:

```js
Input: (arr = []), (target = 1);
Output: -1; // Empty array
```

#### Test Case 4:

```js
Input: (arr = [2, 4, 2, 6]), (target = 2);
Output: 0; // Return first occurrence
```

---

### 💡 Intuition

Linear Search is the **simplest search algorithm**.

- Start at the **first index**
- Check each element **one by one**
- If element equals target → **return the index**
- If loop ends and no match → **return -1**

It works for:

- Sorted or unsorted arrays
- All data types
- Small or unknown-sized data sets

---

### 🔄 Dry Run

For input:

```js
(arr = [10, 20, 30, 40]), (target = 30);
```

Start scanning:

- `i = 0`: arr\[0] = 10 → not match
- `i = 1`: arr\[1] = 20 → not match
- `i = 2`: arr\[2] = 30 → ✅ match → return `2`

✅ Answer = `2`

---

### 🧑‍💻 JavaScript Code

```javascript
function linearSearch(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) {
      return i; // Target found
    }
  }
  return -1; // Target not found
}

// Tests
console.log(linearSearch([10, 20, 30, 40], 30)); // 2
console.log(linearSearch([5, 6, 7, 8], 9)); // -1
console.log(linearSearch([], 1)); // -1
console.log(linearSearch([2, 4, 2, 6], 2)); // 0
```

---

### ⏱️ Time & Space Complexity

#### 🔁 Time Complexity:

| Case         | Time | Explanation                       |
| ------------ | ---- | --------------------------------- |
| Best Case    | O(1) | Target found at first index       |
| Worst Case   | O(n) | Target not found or at last index |
| Average Case | O(n) | On average, target in middle      |

#### 🧠 Space Complexity: `O(1)`

- No extra space used — in-place search with a loop

---

### ✅ Summary

| Feature          | Value                                    |
| ---------------- | ---------------------------------------- |
| Input Type       | Unsorted / Sorted                        |
| Works with       | Any data type                            |
| Preserves order  | ✅ Yes                                   |
| Time Complexity  | O(n)                                     |
| Space Complexity | O(1)                                     |
| Use Case         | Small / unsorted arrays or unknown sizes |

---

## 9. **Missing Number from Range \[0, n]**

You're given an array `nums` containing `n` **distinct** numbers in the range `[0, n]`.

> Your task is to return the **only number** in that range that is **missing** from the array.

#### 🔑 Constraints:

- Array contains **distinct** values
- All numbers from `0` to `n` **except one** are present

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: nums = [3, 0, 1];
Output: 2;
```

#### Test Case 2:

```js
Input: nums = [0, 1];
Output: 2;
```

#### Test Case 3:

```js
Input: nums = [9, 6, 4, 2, 3, 5, 7, 0, 1];
Output: 8;
```

#### Test Case 4:

```js
Input: nums = [1];
Output: 0;
```

---

### Approch 1

### 💡 Intuition

The array should contain all values from `0` to `n`, **but one number is missing**.

We can solve it in multiple ways. Here's the **most elegant and efficient** one:

#### ✨ Using the Mathematical Formula:

> Sum of first `n` natural numbers is:
> `total = n * (n + 1) / 2`

- Compute this **expected sum**
- Compute the **actual sum** of the array
- The **missing number** = `expected sum - actual sum`

✅ This approach works in **O(n)** time and **O(1)** space.

---

### 🔄 Dry Run

Input:

```js
nums = [3, 0, 1]
n = 3 → length = 3 → so range should be 0 to 3
```

- Expected sum: `3 * (3 + 1) / 2 = 6`
- Actual sum: `3 + 0 + 1 = 4`

Missing = `6 - 4 = 2`

✅ Output: `2`

---

### 🧑‍💻 JavaScript Code

```javascript
function missingNumber(nums) {
  const n = nums.length;
  const expectedSum = (n * (n + 1)) / 2;

  let actualSum = 0;
  for (let num of nums) {
    actualSum += num;
  }

  return expectedSum - actualSum;
}

// Test cases
console.log(missingNumber([3, 0, 1])); // 2
console.log(missingNumber([0, 1])); // 2
console.log(missingNumber([9, 6, 4, 2, 3, 5, 7, 0, 1])); // 8
console.log(missingNumber([1])); // 0
```

---

### ⏱️ Time & Space Complexity

#### ⏳ Time Complexity: `O(n)`

- One pass to compute the sum of the array

#### 🧠 Space Complexity: `O(1)`

- Constant space used — no extra data structures

---

### ✅ Summary

| Method                      | Time       | Space | Efficient?     |
| --------------------------- | ---------- | ----- | -------------- |
| Sum Formula (used here)     | O(n)       | O(1)  | ✅ Yes         |
| Hash Set                    | O(n)       | O(n)  | 🚫 Extra space |
| Sorting + Check Index Match | O(n log n) | O(1)  | 🚫 Slower      |

---

### Approch 2

### 💡 Intuition (Using XOR)

#### ✨ XOR Properties:

- `a ^ a = 0` (XOR of a number with itself is 0)
- `a ^ 0 = a` (XOR with 0 gives the number itself)
- XOR is **commutative** and **associative**, so order doesn’t matter.

#### Trick:

If we XOR all numbers from `0 to n` and then XOR all elements of the array,
**the duplicate numbers cancel out**, and you’re left with the **missing number**.

###### Formula:

```js
missing = (0 ^ 1 ^ 2 ^ ... ^ n) ^ (nums[0] ^ nums[1] ^ ... ^ nums[n-1])
```

---

### 🔄 Dry Run

#### Input:

```js
nums = [3, 0, 1] → n = 3 (array length = 3)
```

Step 1: XOR of full range `0 ^ 1 ^ 2 ^ 3 = 0 ^ 1 = 1; 1 ^ 2 = 3; 3 ^ 3 = 0`
So `xor1 = 0`

Step 2: XOR of array `3 ^ 0 ^ 1 = 3 ^ 0 = 3; 3 ^ 1 = 2`
So `xor2 = 2`

Final: `missing = xor1 ^ xor2 = 0 ^ 2 = 2`

✅ Output = `2`

---

### 🧑‍💻 JavaScript Code

```javascript
function missingNumber(nums) {
  const n = nums.length;
  let xorFull = 0;
  let xorArr = 0;

  for (let i = 0; i <= n; i++) {
    xorFull ^= i; // XOR of all numbers from 0 to n
  }

  for (let num of nums) {
    xorArr ^= num; // XOR of elements in array
  }

  return xorFull ^ xorArr;
}

// Test Cases
console.log(missingNumber([3, 0, 1])); // 2
console.log(missingNumber([0, 1])); // 2
console.log(missingNumber([9, 6, 4, 2, 3, 5, 7, 0, 1])); // 8
```

---

### ⏱️ Time & Space Complexity

#### 🔁 Time Complexity: `O(n)`

- One loop to XOR `0 to n`, one loop for array → total linear

#### 🧠 Space Complexity: `O(1)`

- Constant variables only, no extra memory

---

### ✅ Summary

| Approach          | Time       | Space | Notes                     |
| ----------------- | ---------- | ----- | ------------------------- |
| Sum Formula       | O(n)       | O(1)  | Simple and accurate       |
| XOR Method ✅     | O(n)       | O(1)  | Elegant, no overflow risk |
| Hashing or Set    | O(n)       | O(n)  | Extra space, not optimal  |
| Sorting + Compare | O(n log n) | O(1)  | Slower                    |

---

### ⚠️ Important Note

This technique of **marking elements by making values at specific indices negative** works only when:

- All values in the array are **positive**
- All values lie in the **index range** of the array (i.e., `0 to n-1`)

But in this problem:

- The range is `[0, n]` and **length of array is `n`**, so index `n` is **out of bounds**

🛑 So we **cannot use this exact trick directly** here, because:

- The **missing number might be `n`**, which is **not a valid index** in a `0-indexed array` of length `n`

---

### ✅ Where This Trick Works

This **index-marking (sign flipping)** technique is better suited for problems like:

> **“Find all numbers from 1 to n that are missing in an array”**
> Where array length is `n`, and values are in `[1, n]`.

---

#### Example of such a problem:

```js
Input: [4, 3, 2, 7, 8, 2, 3, 1];
Output: [5, 6]; // 5 and 6 are missing from 1 to 8
```

There we:

1. Loop through the array
2. For each `val = abs(nums[i])`, do `nums[val - 1] *= -1`
3. Then scan for values still positive — their indices are the missing numbers

---

### ❌ Why It Doesn’t Work Here

In **our case**:

- Array has values in `[0, n]`
- Array **length = n**
- So **index `n`** (if missing) can’t be marked

#### ➤ For example:

```js
nums = [0, 1, 2] → n = 3 → missing = 3
```

But we can't access `arr[3]` to mark it as negative!

---

### ✅ Best Solution Here: XOR or SUM Method

Stick to these **safe and optimal** approaches for this specific problem:

- ✅ XOR method
- ✅ Sum method
- ✅ Subtraction logic
  All are `O(n)` time and `O(1)` space.

---

### 🔚 Summary

| Technique        | Works Here? | Why / Why Not                                          |
| ---------------- | ----------- | ------------------------------------------------------ |
| XOR / Sum method | ✅ Yes      | Fast, simple, handles missing `n` properly             |
| Sign flipping    | ❌ No       | Because `n` could be missing, and `n` is out of bounds |
| Hashing (Set)    | ✅ Yes      | But uses extra space                                   |

---

## 10. **Maximum Number of Consecutive 1’s in a Binary Array**

You are given a **binary array** `nums` (only 0s and 1s).

> Return the **maximum number of consecutive 1's** in the array.

---

### 🧪 2. Test Cases

#### Test Case 1:

```js
Input: [1, 1, 0, 1, 1, 1];
Output: 3;
```

#### Test Case 2:

```js
Input: [1, 0, 1, 1, 0, 1];
Output: 2;
```

#### Test Case 3:

```js
Input: [0, 0, 0];
Output: 0;
```

#### Test Case 4:

```js
Input: [1, 1, 1, 1];
Output: 4;
```

---

### 💡 Intuition

We want to count how many `1`s appear **in a row**, and track the **maximum streak**.

---

### 🔄 Dry Run

For input:

```js
nums = [1, 1, 0, 1, 1, 1];
```

- Initialize `maxCount = 0`, `current = 0`
- Traverse:

  - 1 → current = 1
  - 1 → current = 2
  - 0 → reset current = 0, max = 2
  - 1 → current = 1
  - 1 → current = 2
  - 1 → current = 3 → update max = 3

✅ Final Answer: `3`

---

### 🧑‍💻 JavaScript Code (Optimal)

#### ✅ **Approach 1: One Pass, Count Consecutive 1's**

```javascript
function findMaxConsecutiveOnes(nums) {
  let maxCount = 0;
  let currentCount = 0;

  for (let i = 0; i < nums.length; i++) {
    if (nums[i] === 1) {
      currentCount++;
      maxCount = Math.max(maxCount, currentCount);
    } else {
      currentCount = 0;
    }
  }

  return maxCount;
}

// Test
console.log(findMaxConsecutiveOnes([1, 1, 0, 1, 1, 1])); // 3
console.log(findMaxConsecutiveOnes([0, 0, 0])); // 0
console.log(findMaxConsecutiveOnes([1, 1, 1, 1])); // 4
```

---

### ⏱️ Time & Space Complexity

| Metric           | Value  |
| ---------------- | ------ |
| Time Complexity  | O(n)   |
| Space Complexity | O(1)   |
| In-place?        | ✅ Yes |

---

### 🔁 Alternative Approaches

#### 🔸 **Approach 2: Sliding Window (Not Needed Here)**

- Not needed for this case unless there's a constraint like **flip at most 1 zero** (then it becomes an advanced problem).
- So for pure 1’s counting, this adds no benefit.

---

#### 🔸 **Approach 3: Using String (JS Trick)**

Convert array to string and use `.split("0")`:

```javascript
function findMaxConsecutiveOnes(nums) {
  return Math.max(
    ...nums
      .join("")
      .split("0")
      .map((str) => str.length)
  );
}

// Test
console.log(findMaxConsecutiveOnes([1, 1, 0, 1, 1, 1])); // 3
```

###### Pros:

- One-liner
- Looks smart

###### Cons:

- Less readable
- Slightly slower due to string manipulation

---

### ✅ Summary

| Approach       | Time | Space | Readable    | Recommended        |
| -------------- | ---- | ----- | ----------- | ------------------ |
| Count & Reset  | O(n) | O(1)  | ✅ Yes      | ✅ Best            |
| String Trick   | O(n) | O(n)  | 🚫 Tricky   | ⚠️ Optional        |
| Sliding Window | O(n) | O(1)  | 🚫 Overkill | ❌ Not needed here |

---

# Medium Problems

## 1. **Find the Union of Two Sorted Arrays**

You're given two **sorted arrays** `arr1` of size `n` and `arr2` of size `m`.

> Your task is to **find their union**, which includes **all distinct elements** from both arrays in **sorted order**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: (arr1 = [1, 2, 4, 5]), (arr2 = [2, 3, 5, 6]);
Output: [1, 2, 3, 4, 5, 6];
```

#### Test Case 2:

```js
Input: (arr1 = [1, 1, 2]), (arr2 = [2, 2, 3]);
Output: [1, 2, 3];
```

#### Test Case 3:

```js
Input: (arr1 = []), (arr2 = [1, 2, 3]);
Output: [1, 2, 3];
```

#### Test Case 4:

```js
Input: (arr1 = [1, 2, 3]), (arr2 = []);
Output: [1, 2, 3];
```

---

### 💡 Intuition

Since both arrays are already **sorted**, we can leverage that to efficiently merge them, **skipping duplicates** as we go.

Think of this like the **merge step** in Merge Sort:

- Traverse both arrays using two pointers (`i` and `j`)
- Compare elements
- Add the **smaller one** to result if it’s **not a duplicate**
- Skip duplicates to keep result unique

---

### 🔄 Dry Run

Let’s dry-run this:

```js
arr1 = [1, 2, 4, 5];
arr2 = [2, 3, 5, 6];
```

Result = \[]

- i=0, j=0 → 1 < 2 → push 1 → Result: \[1]
- i=1, j=0 → 2 == 2 → push 2 → Result: \[1, 2]
- i=2, j=1 → 4 > 3 → push 3 → Result: \[1, 2, 3]
- i=2, j=2 → 4 < 5 → push 4 → Result: \[1, 2, 3, 4]
- i=3, j=2 → 5 == 5 → push 5 → Result: \[1, 2, 3, 4, 5]
- i=4, j=3 → i out of bounds → push remaining 6 → Result: \[1, 2, 3, 4, 5, 6]

✅ Final Answer: `[1, 2, 3, 4, 5, 6]`

---

### 🧑‍💻 JavaScript Code

#### ✅ **Approach 1: Two Pointer Method (Optimal)**

```javascript
function unionSortedArrays(arr1, arr2) {
  const n = arr1.length;
  const m = arr2.length;
  let i = 0,
    j = 0;
  const result = [];

  while (i < n && j < m) {
    // Skip duplicates in result
    let last = result.length > 0 ? result[result.length - 1] : null;

    if (arr1[i] < arr2[j]) {
      if (arr1[i] !== last) result.push(arr1[i]);
      i++;
    } else if (arr1[i] > arr2[j]) {
      if (arr2[j] !== last) result.push(arr2[j]);
      j++;
    } else {
      if (arr1[i] !== last) result.push(arr1[i]);
      i++;
      j++;
    }
  }

  // Add remaining elements from arr1
  while (i < n) {
    if (arr1[i] !== result[result.length - 1]) result.push(arr1[i]);
    i++;
  }

  // Add remaining elements from arr2
  while (j < m) {
    if (arr2[j] !== result[result.length - 1]) result.push(arr2[j]);
    j++;
  }

  return result;
}

// Test
console.log(unionSortedArrays([1, 2, 4, 5], [2, 3, 5, 6])); // [1, 2, 3, 4, 5, 6]
```

---

#### ✅ **Approach 2: Use Set (Simple but not optimal)**

```javascript
function unionSortedArrays(arr1, arr2) {
  const set = new Set([...arr1, ...arr2]);
  return Array.from(set).sort((a, b) => a - b);
}
```

###### ⚠️ Cons:

- Sorting costs O((n+m) log(n+m))
- Not efficient when arrays are already sorted

---

### ⏱️ 6. Time & Space Complexity

#### **Approach 1: Two Pointers**

| Metric           | Value               |
| ---------------- | ------------------- |
| Time Complexity  | O(n + m)            |
| Space Complexity | O(n + m) for result |

#### **Approach 2: Set + Sort**

| Metric           | Value                 |
| ---------------- | --------------------- |
| Time Complexity  | O((n + m) log(n + m)) |
| Space Complexity | O(n + m)              |

---

### ✅ Summary of Approaches

| Approach        | Time       | Space  | Preserves Order | Skips Duplicates | Sorted Output | Efficient |
| --------------- | ---------- | ------ | --------------- | ---------------- | ------------- | --------- |
| Two Pointers ✅ | O(n + m)   | O(n+m) | ✅              | ✅               | ✅            | ✅ Yes    |
| Set + Sort      | O(n log n) | O(n+m) | 🚫              | ✅               | ✅            | ❌ Less   |

---

## 2. **Find the Unique Element**

You're given an array where:

- **Every element appears twice**, **except one** element that appears **only once**.

> Your task is to find and return that **single number**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: [2, 2, 1];
Output: 1;
```

#### Test Case 2:

```js
Input: [4, 1, 2, 1, 2];
Output: 4;
```

#### Test Case 3:

```js
Input: [7];
Output: 7;
```

---

### 💡 Intuition

There are multiple approaches. Let’s go through each.

---

### ✅ Approaches

---

#### ✅ **Approach 1: Bit Manipulation (Using XOR)** — **Best Solution**

##### 💡 XOR Properties:

- `a ^ a = 0` → same number cancels out
- `a ^ 0 = a` → XOR with 0 gives same number
- XOR is **commutative & associative** → order doesn’t matter

##### 👉 Intuition:

- XOR all elements
- Pairs cancel out (`2 ^ 2 = 0`)
- You're left with the number that appears once

---

#### 🔄 Dry Run

```js
Input: [4, 1, 2, 1, 2]
XOR step by step:
4 ^ 1 = 5
5 ^ 2 = 7
7 ^ 1 = 6
6 ^ 2 = 4

✅ Final Answer = 4
```

---

#### 🧑‍💻 JavaScript Code (Approach 1):

```javascript
function singleNumber(nums) {
  let result = 0;

  for (let num of nums) {
    result ^= num; // XOR
  }

  return result;
}

// Test cases
console.log(singleNumber([2, 2, 1])); // 1
console.log(singleNumber([4, 1, 2, 1, 2])); // 4
console.log(singleNumber([7])); // 7
```

---

#### ⏱ Time & Space Complexity (Approach 1)

| Metric           | Value  |
| ---------------- | ------ |
| Time Complexity  | O(n)   |
| Space Complexity | O(1)   |
| In-place         | ✅ Yes |
| Extra Space Used | ❌ No  |

---

#### 🔁 **Approach 2: HashMap (Frequency Count)**

##### 👉 Logic:

- Store frequency of each number
- Return the number with count `1`

##### ❌ Not optimal — uses extra space.

```javascript
function singleNumber(nums) {
  const map = new Map();

  for (let num of nums) {
    map.set(num, (map.get(num) || 0) + 1);
  }

  for (let [key, value] of map.entries()) {
    if (value === 1) return key;
  }
}
```

---

### ✅ Summary of Approaches

| Approach         | Time | Space | Efficient | Notes                      |
| ---------------- | ---- | ----- | --------- | -------------------------- |
| XOR (Bitwise) ✅ | O(n) | O(1)  | ✅ Best   | Clever, fast, in-place     |
| HashMap          | O(n) | O(n)  | ❌        | Easy, but uses extra space |

---

## 3. **Longest Subarray with Given Sum K (Positive Integers Only)**

You're given an array of **positive integers** `arr[]` and an integer `K`.

> Return the **length** of the **longest contiguous subarray** that sums to `K`.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: (arr = [1, 2, 3, 1, 1, 1, 1]), (K = 3);
Output: 2; // [1, 2] or [3] or [1, 1, 1] (first two)
```

#### Test Case 2:

```js
Input: (arr = [1, 1, 1, 2, 3, 4]), (K = 6);
Output: 3; // [1, 2, 3]
```

#### Test Case 3:

```js
Input: (arr = [1, 2, 1, 1, 1]), (K = 3);
Output: 3; // [1, 1, 1]
```

#### Test Case 4:

```js
Input: (arr = [5, 1, 1, 1, 2]), (K = 6);
Output: 4; // [1, 1, 1, 2]
```

---

### 🔧 Brute Force Approach

#### 🔹 Idea:

- Try **all possible subarrays** using **two loops** (start and end)
- For each subarray, calculate the sum
- If sum == `K`, update max length

---

### 🔄 Dry Run

#### Input:

```js
(arr = [1, 2, 1, 1, 1]), (K = 3);
```

We'll try all subarrays:

| Start | End | Subarray         | Sum | Valid?              |
| ----- | --- | ---------------- | --- | ------------------- |
| 0     | 0   | \[1]             | 1   | ❌                  |
| 0     | 1   | \[1, 2]          | 3   | ✅ len = 2          |
| 0     | 2   | \[1, 2, 1]       | 4   | ❌                  |
| 0     | 3   | \[1, 2, 1, 1]    | 5   | ❌                  |
| 0     | 4   | \[1, 2, 1, 1, 1] | 6   | ❌                  |
| 1     | 1   | \[2]             | 2   | ❌                  |
| 1     | 2   | \[2, 1]          | 3   | ✅ len = 2          |
| 1     | 3   | \[2, 1, 1]       | 4   | ❌                  |
| 1     | 4   | \[2, 1, 1, 1]    | 5   | ❌                  |
| 2     | 2   | \[1]             | 1   | ❌                  |
| 2     | 3   | \[1, 1]          | 2   | ❌                  |
| 2     | 4   | \[1, 1, 1]       | 3   | ✅ ✅ len = 3 (max) |
| 3     | 3   | \[1]             | 1   | ❌                  |
| 3     | 4   | \[1, 1]          | 2   | ❌                  |
| 4     | 4   | \[1]             | 1   | ❌                  |

✅ Final Answer: **3**

---

### 🧑‍💻 JavaScript Code (Brute Force)

```javascript
function longestSubarrayWithSumKBrute(arr, K) {
  let maxLen = 0;

  for (let start = 0; start < arr.length; start++) {
    let sum = 0;

    for (let end = start; end < arr.length; end++) {
      sum += arr[end];

      if (sum === K) {
        maxLen = Math.max(maxLen, end - start + 1);
      }
    }
  }

  return maxLen;
}

// Test
console.log(longestSubarrayWithSumKBrute([1, 2, 1, 1, 1], 3)); // 3
```

---

### ⏱️ Time & Space Complexity

| Metric           | Value  |
| ---------------- | ------ |
| Time Complexity  | O(n²)  |
| Space Complexity | O(1)   |
| In-place         | ✅ Yes |

---

### 🧠 Comparison with Optimal Approach

| Approach       | Time  | Space | Suitable For       |
| -------------- | ----- | ----- | ------------------ |
| Brute Force    | O(n²) | O(1)  | Understanding base |
| Sliding Window | O(n)  | O(1)  | ✅ Large Inputs    |

---

### ✅ Summary

- Brute-force checks **all subarrays**
- Good for learning, but not scalable
- Use **sliding window** when array has only **positive numbers**

### 💡 Approch 2:

Because the array only contains **positive integers**, we can safely use the **sliding window** technique.

> Why? Because:

- Increasing window size increases the sum
- Shrinking the window decreases the sum
- So we can **move left/right pointers** to control the sum efficiently

---

### 🔄 Dry Run

```js
(arr = [1, 2, 1, 1, 1]), (K = 3);
```

- Initialize: `left = 0`, `right = 0`, `sum = 0`, `maxLen = 0`

Step-by-step:

- Add `1` → sum = 1
- Add `2` → sum = 3 → ✅ Found! → maxLen = 2
- Add `1` → sum = 4 → Too much → shrink from left
- Remove `1` → sum = 3 → ✅ Found! → length = 2 → maxLen stays 2
- Add `1` → sum = 4 → Remove `2` → sum = 2
- Add `1` → sum = 3 → ✅ Found → length = 3 → maxLen = 3

✅ Final Answer = `3`

---

### 🧑‍💻 JavaScript Code (Sliding Window)

```javascript
function longestSubarrayWithSumK(arr, K) {
  let left = 0;
  let sum = 0;
  let maxLen = 0;

  for (let right = 0; right < arr.length; right++) {
    sum += arr[right];

    // Shrink window if sum > K
    while (sum > K) {
      sum -= arr[left];
      left++;
    }

    // Check for equal sum
    if (sum === K) {
      maxLen = Math.max(maxLen, right - left + 1);
    }
  }

  return maxLen;
}

// Tests
console.log(longestSubarrayWithSumK([1, 2, 3, 1, 1, 1, 1], 3)); // 2
console.log(longestSubarrayWithSumK([1, 1, 1, 2, 3, 4], 6)); // 3
console.log(longestSubarrayWithSumK([1, 2, 1, 1, 1], 3)); // 3
console.log(longestSubarrayWithSumK([5, 1, 1, 1, 2], 6)); // 4
```

---

### ⏱️ Time & Space Complexity

| Metric           | Value  |
| ---------------- | ------ |
| Time Complexity  | `O(n)` |
| Space Complexity | `O(1)` |
| In-place         | ✅ Yes |

---

### ⚠️ Note: Only Works When All Elements Are Positive

For **negative numbers** or **zero**, this sliding window **won’t work correctly** — you’ll need a **prefix sum + hashmap** approach instead.

---

### ✅ Summary

| Approach          | Suitable When              | Time | Space | Efficient |
| ----------------- | -------------------------- | ---- | ----- | --------- |
| Sliding Window ✅ | All positive elements      | O(n) | O(1)  | ✅ Best   |
| Prefix Sum + Map  | Array has negative numbers | O(n) | O(n)  | ✅ Needed |

---

## 4. **Longest Subarray with Sum K (Positives + Negatives)**

Given an array `arr[]` of `n` integers (can be positive, negative, or zero), and a target `K`,

> Return the **length of the longest contiguous subarray** whose sum is exactly `K`.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: (arr = [1, -1, 5, -2, 3]), (K = 3);
Output: 4; // subarray [1, -1, 5, -2]
```

#### Test Case 2:

```js
Input: (arr = [-2, -1, 2, 1]), (K = 1);
Output: 2; // subarray [2, 1]
```

#### Test Case 3:

```js
Input: (arr = [3, 4, -7, 1, 3, 3, 1, -4]), (K = 7);
Output: 5; // subarray [1, 3, 3, 1, -4]
```

---

### 💡 Intuition

#### ❌ Why Sliding Window Fails:

Sliding window only works when all elements are **positive**, because you can safely expand/shrink the window to move toward `K`.
When **negatives** are included, shrinking can **increase** the sum — so windowing becomes unreliable.

---

#### ✅ Use **Prefix Sum + HashMap**

- Use a variable `sum` to keep track of prefix sum so far
- Use a `Map` to store the **first occurrence** of each prefix sum
- At every index:

  - Check if `sum - K` exists in map

    - If it does, you've found a subarray of sum `K`
    - Calculate the length: `i - map[sum - K]`

  - Store `sum` in map if not already stored (store first occurrence only)

---

### 🔄 Dry Run

#### Input:

```js
(arr = [1, -1, 5, -2, 3]), (K = 3);
```

Let’s walk through step-by-step:

| Index | Value | Sum | `sum - K` | Exists in map? | Length    | Max |
| ----- | ----- | --- | --------- | -------------- | --------- | --- |
| 0     | 1     | 1   | -2        | ❌             |           | 0   |
| 1     | -1    | 0   | -3        | ❌             |           | 0   |
| 2     | 5     | 5   | 2         | ❌             |           | 0   |
| 3     | -2    | 3   | 0         | ✅ At index 1  | 3 - 1 = 2 | 2   |
| 4     | 3     | 6   | 3         | ✅ At index 3  | 4 - 3 = 1 | 2   |

Also, `sum === K` at index 3 → \[0..3] = length 4 → ✅ maxLen = 4

✅ Final Answer = **4**

---

### 🧑‍💻 JavaScript Code (Prefix Sum + HashMap)

```javascript
function longestSubarrayWithSumK(arr, K) {
  let map = new Map();
  let sum = 0;
  let maxLen = 0;

  for (let i = 0; i < arr.length; i++) {
    sum += arr[i];

    // Case 1: If sum itself is K
    if (sum === K) {
      maxLen = i + 1;
    }

    // Case 2: If (sum - K) seen before
    if (map.has(sum - K)) {
      maxLen = Math.max(maxLen, i - map.get(sum - K));
    }

    // Store the first occurrence of this sum
    if (!map.has(sum)) {
      map.set(sum, i);
    }
  }

  return maxLen;
}

// Test Cases
console.log(longestSubarrayWithSumK([1, -1, 5, -2, 3], 3)); // 4
console.log(longestSubarrayWithSumK([-2, -1, 2, 1], 1)); // 2
console.log(longestSubarrayWithSumK([3, 4, -7, 1, 3, 3, 1, -4], 7)); // 5
```

---

### ⏱️ Time & Space Complexity

| Metric           | Value                 |
| ---------------- | --------------------- |
| Time Complexity  | O(n)                  |
| Space Complexity | O(n)                  |
| Extra Space Used | HashMap (prefix sums) |

---

### ✅ Summary

| Approach                | Works With Negatives? | Time | Space | Efficient        |
| ----------------------- | --------------------- | ---- | ----- | ---------------- |
| Sliding Window          | ❌ No                 | O(n) | O(1)  | ✅ For Positives |
| Prefix Sum + HashMap ✅ | ✅ Yes                | O(n) | O(n)  | ✅ Best for All  |

---

## 5. **Two Sum**

Given an array of integers `nums` and an integer `target`,

> Return **indices** of the two numbers such that they **add up to target**.

You may assume that **each input has exactly one solution**, and **you may not use the same element twice**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: (nums = [2, 7, 11, 15]), (target = 9);
Output: [0, 1]; // because nums[0] + nums[1] = 2 + 7 = 9
```

#### Test Case 2:

```js
Input: (nums = [3, 2, 4]), (target = 6);
Output: [1, 2];
```

#### Test Case 3:

```js
Input: (nums = [3, 3]), (target = 6);
Output: [0, 1];
```

---

### 💡 Intuition

We need to **find two numbers whose sum equals the target**.

There are multiple ways to solve this:

---

### 🔁 Approaches

#### ✅ **Approach 1: Brute Force (Nested Loops)**

###### 🔹 Logic:

- Try every pair `(i, j)` such that `i < j`
- Check if `nums[i] + nums[j] === target`

---

#### 🔄 Dry Run

```js
nums = [2, 7, 11, 15], target = 9

i=0, j=1 → 2 + 7 = 9 ✅ return [0, 1]
```

---

#### 🧑‍💻 Code (Brute Force)

```javascript
function twoSumBrute(nums, target) {
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] + nums[j] === target) {
        return [i, j];
      }
    }
  }
}
```

#### ⏱️ Time & Space

| Metric           | Value |
| ---------------- | ----- |
| Time Complexity  | O(n²) |
| Space Complexity | O(1)  |

---

#### ✅✅ **Approach 2: Hash Map (Optimal)**

###### 🔹 Logic:

- Use a map to store numbers we've seen and their indices
- For each `num`, check if `target - num` is already in the map

###### 👉 "Find the complement while iterating."

---

#### 🔄 Dry Run

```js
nums = [2, 7, 11, 15], target = 9

i=0 → 2 → need 7 → not in map → store {2:0}
i=1 → 7 → need 2 → in map ✅ → return [0,1]
```

---

#### 🧑‍💻 Code (Optimal)

```javascript
function twoSum(nums, target) {
  const map = new Map(); // value → index

  for (let i = 0; i < nums.length; i++) {
    let complement = target - nums[i];

    if (map.has(complement)) {
      return [map.get(complement), i];
    }

    map.set(nums[i], i);
  }
}
```

---

#### ⏱️ Time & Space

| Metric           | Value |
| ---------------- | ----- |
| Time Complexity  | O(n)  |
| Space Complexity | O(n)  |

---

### ✅ Summary of Approaches

| Approach        | Time  | Space | Efficient | Notes                |
| --------------- | ----- | ----- | --------- | -------------------- |
| Brute Force     | O(n²) | O(1)  | ❌        | Easy to understand   |
| Hash Map (Best) | O(n)  | O(n)  | ✅        | Fast and widely used |

---

### ✅ Bonus

Would you like:

- The **2Sum variant** where you return **all pairs**?
- Or **return values instead of indices**?
- Or the version where **array is sorted**?

Let me know, and I’ll guide you through!

## 6. **Sort an array of 0s, 1s, and 2s**

Given an array consisting only of **0s, 1s, and 2s**,

> Sort the array **in-place** without using any inbuilt sort function.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: [0, 1, 2, 0, 1, 2];
Output: [0, 0, 1, 1, 2, 2];
```

#### Test Case 2:

```js
Input: [2, 0, 1];
Output: [0, 1, 2];
```

#### Test Case 3:

```js
Input: [0, 0, 0];
Output: [0, 0, 0];
```

---

### 💡 Intuition

There are three common approaches:

---

### 🔁 Approaches

#### ✅ **Approach 1: Counting (Brute Force Style)**

##### 🔹 Logic:

- Count number of 0s, 1s, and 2s
- Overwrite the array with those counts

---

#### 🧑‍💻 Code (Counting)

```javascript
function sortColors(arr) {
  let count0 = 0,
    count1 = 0,
    count2 = 0;

  for (let num of arr) {
    if (num === 0) count0++;
    else if (num === 1) count1++;
    else count2++;
  }

  for (let i = 0; i < arr.length; i++) {
    if (count0 > 0) {
      arr[i] = 0;
      count0--;
    } else if (count1 > 0) {
      arr[i] = 1;
      count1--;
    } else {
      arr[i] = 2;
      count2--;
    }
  }

  return arr;
}
```

#### ⏱️ Time & Space

| Metric           | Value |
| ---------------- | ----- |
| Time Complexity  | O(n)  |
| Space Complexity | O(1)  |

---

#### ✅✅ **Approach 2: Dutch National Flag Algorithm (Optimal)**

##### 🔹 Idea:

Use three pointers:

- `low` – boundary of 0s
- `mid` – current element
- `high` – boundary of 2s

#### 🔄 Dry Run Example:

##### 🧪 Input:

```js
arr = [2, 0, 2, 1, 1, 0];
```

##### 📌 Initialize Pointers:

- `low = 0` → boundary for 0s
- `mid = 0` → current element
- `high = 5` → boundary for 2s

---

##### 🔁 Steps:

| Step | arr                 | low | mid | high | arr\[mid] | Action                                   |
| ---- | ------------------- | --- | --- | ---- | --------- | ---------------------------------------- |
| 1    | \[2, 0, 2, 1, 1, 0] | 0   | 0   | 5    | 2         | Swap arr\[mid] ↔ arr\[high], high--      |
|      | \[0, 0, 2, 1, 1, 2] | 0   | 0   | 4    |           |                                          |
| 2    | \[0, 0, 2, 1, 1, 2] | 0   | 0   | 4    | 0         | Swap arr\[mid] ↔ arr\[low], low++, mid++ |
|      | \[0, 0, 2, 1, 1, 2] | 1   | 1   | 4    |           | No change, already 0                     |
| 3    | \[0, 0, 2, 1, 1, 2] | 1   | 1   | 4    | 0         | Swap arr\[mid] ↔ arr\[low], low++, mid++ |
|      | \[0, 0, 2, 1, 1, 2] | 2   | 2   | 4    |           | No change                                |
| 4    | \[0, 0, 2, 1, 1, 2] | 2   | 2   | 4    | 2         | Swap arr\[mid] ↔ arr\[high], high--      |
|      | \[0, 0, 1, 1, 2, 2] | 2   | 2   | 3    |           |                                          |
| 5    | \[0, 0, 1, 1, 2, 2] | 2   | 2   | 3    | 1         | mid++                                    |
| 6    | \[0, 0, 1, 1, 2, 2] | 2   | 3   | 3    | 1         | mid++                                    |
| 7    | \[0, 0, 1, 1, 2, 2] | 2   | 4   | 3    |           | mid > high, loop ends                    |

---

##### ✅ Final Output:

```js
[0, 0, 1, 1, 2, 2];
```

---

### 🧠 Key Points

- **mid** traverses the array.
- When you find:

  - `0`: Move to front (swap with `low`)
  - `2`: Move to back (swap with `high`)
  - `1`: Do nothing, just `mid++`

- You only traverse the array **once**, making it very efficient.

---

#### ⏱ Time and Space

| Metric           | Value  |
| ---------------- | ------ |
| Time Complexity  | O(n)   |
| Space Complexity | O(1)   |
| In-place         | ✅ Yes |

---

#### 🧑‍💻 Code (Dutch Flag)

```javascript
function sortColors(arr) {
  let low = 0,
    mid = 0,
    high = arr.length - 1;

  while (mid <= high) {
    if (arr[mid] === 0) {
      [arr[low], arr[mid]] = [arr[mid], arr[low]];
      low++;
      mid++;
    } else if (arr[mid] === 1) {
      mid++;
    } else {
      [arr[mid], arr[high]] = [arr[high], arr[mid]];
      high--;
    }
  }

  return arr;
}
```

---

### ✅ Summary of Approaches

| Approach               | Time | Space | In-place | Stable | Notes                     |
| ---------------------- | ---- | ----- | -------- | ------ | ------------------------- |
| Counting (2-pass)      | O(n) | O(1)  | ✅       | ❌     | Simple to implement       |
| Dutch National Flag ✅ | O(n) | O(1)  | ✅       | ❌     | Optimal, 1-pass, in-place |

---

## 7. **Majority Element**

> Given an array `nums[]`, find the **majority element** — the element that appears **more than ⌊n/2⌋ times**.

You may assume that **the majority element always exists** in the input array.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: [3, 2, 3];
Output: 3;
```

#### Test Case 2:

```js
Input: [2, 2, 1, 1, 1, 2, 2];
Output: 2;
```

#### Test Case 3:

```js
Input: [1];
Output: 1;
```

---

### 💡 Intuition

We need to find the number that **occurs more than half** the times.
That means its count is **greater than n/2**.

---

### ✅ Approaches

---

#### 🔁 **Approach 1: HashMap (Frequency Count)**

###### 🔹 Logic:

- Count frequency of each element
- Return the one with frequency > n/2

---

###### 🧑‍💻 Code:

```javascript
function majorityElement(nums) {
  const map = new Map();
  const n = nums.length;

  for (let num of nums) {
    map.set(num, (map.get(num) || 0) + 1);
    if (map.get(num) > Math.floor(n / 2)) {
      return num;
    }
  }
}
```

###### ⏱ Complexity:

| Time | Space |
| ---- | ----- |
| O(n) | O(n)  |

---

#### ✅✅ **Approach 2: Moore’s Voting Algorithm (Optimal)**

###### 🔹 Intuition:

If an element occurs more than n/2 times, it can’t be “canceled” out completely by others.

---

#### 📌 Step-by-step Logic:

- Initialize `count = 0`, `candidate = null`
- For each number:

  - If `count == 0`, set `candidate = num`
  - If `num == candidate`, `count++`
  - Else, `count--`

- After one pass, `candidate` is the majority element.

---

#### 🔄 Dry Run:

```js
Input: [2, 2, 1, 1, 1, 2, 2]

i = 0 → candidate = 2, count = 1
i = 1 → 2 == 2 → count = 2
i = 2 → 1 != 2 → count = 1
i = 3 → 1 != 2 → count = 0
i = 4 → count = 0 → candidate = 1, count = 1
i = 5 → 2 != 1 → count = 0
i = 6 → count = 0 → candidate = 2, count = 1

✅ Final candidate = 2
```

---

#### 🧑‍💻 Code:

```javascript
function majorityElement(nums) {
  let count = 0;
  let candidate = null;

  for (let num of nums) {
    if (count === 0) {
      candidate = num;
    }
    count += num === candidate ? 1 : -1;
  }

  return candidate;
}
```

---

#### ⏱ Time & Space

| Metric            | Value |
| ----------------- | ----- |
| Time Complexity   | O(n)  |
| Space Complexity  | O(1)  |
| In-place          | ✅    |
| Extra Memory Used | ❌    |

---

### ✅ Summary of Approaches

| Approach                 | Time | Space | Notes                    |
| ------------------------ | ---- | ----- | ------------------------ |
| HashMap (counting)       | O(n) | O(n)  | Simple, uses extra space |
| Moore’s Voting Algorithm | O(n) | O(1)  | ✅ Most optimal          |

---

## 8. **Kadane’s Algorithm** – Maximum Subarray Sum

### 🧪 Test Cases

#### Test Case 1:

```js
Input: [-2, 1, -3, 4, -1, 2, 1, -5, 4]
Output: 6
Explanation: [4, -1, 2, 1] has the largest sum = 6
```

#### Test Case 2:

```js
Input: [1];
Output: 1;
```

#### Test Case 3:

```js
Input: [5, 4, -1, 7, 8];
Output: 23;
```

---

### 💡 Intuition

If you’re summing elements and the sum ever goes **negative**, continuing from there is useless — it's better to **restart** from the next element.

---

### 🔁 Dry Run (Kadane’s Algorithm)

#### Input:

```js
arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4];
```

We maintain:

- `maxSum` → maximum seen so far
- `currentSum` → sum of current subarray

| Index | Element | currentSum          | maxSum |
| ----- | ------- | ------------------- | ------ |
| 0     | -2      | max(-2, -2) = -2    | -2     |
| 1     | 1       | max(1, -2 + 1) = 1  | 1      |
| 2     | -3      | max(-3, 1 - 3) = -2 | 1      |
| 3     | 4       | max(4, -2 + 4) = 4  | 4      |
| 4     | -1      | max(-1, 4 - 1) = 3  | 4      |
| 5     | 2       | max(2, 3 + 2) = 5   | 5      |
| 6     | 1       | max(1, 5 + 1) = 6   | 6 ✅   |
| 7     | -5      | max(-5, 6 - 5) = 1  | 6      |
| 8     | 4       | max(4, 1 + 4) = 5   | 6      |

✅ Final Answer: `6`

---

### 🧑‍💻 JavaScript Code

```javascript
function maxSubArray(nums) {
  let maxSum = nums[0];
  let currentSum = nums[0];

  for (let i = 1; i < nums.length; i++) {
    currentSum = Math.max(nums[i], currentSum + nums[i]);
    maxSum = Math.max(maxSum, currentSum);
  }

  return maxSum;
}
```

---

### ⏱ Time & Space Complexity

| Metric           | Value |
| ---------------- | ----- |
| Time Complexity  | O(n)  |
| Space Complexity | O(1)  |
| In-place         | ✅    |

---

### ✅ Summary

| Approach              | Time  | Space | Notes                    |
| --------------------- | ----- | ----- | ------------------------ |
| Kadane’s Algorithm ✅ | O(n)  | O(1)  | Best possible solution   |
| Brute Force           | O(n²) | O(1)  | Try all subarrays (slow) |

---

## 9. print the contiguous subarray with Largest Sum

Given an integer array `nums`,

> Find and **print the contiguous subarray** which has the **largest sum** using **Kadane’s Algorithm** (extended version).

---

### 🧪 Test Case

#### Input:

```js
nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4];
```

#### Output:

```js
Maximum sum: 6
Subarray: [4, -1, 2, 1]
```

---

### 💡 Intuition

Just like regular Kadane’s:

- Maintain `maxSum` and `currentSum`
- Additionally, **track the starting and ending index** of the max subarray

Every time you reset the subarray (when `nums[i] > currentSum + nums[i]`), update a `tempStart` index.

When you find a new `maxSum`, update `start` and `end` accordingly.

---

### 🔁 Dry Run

```js
arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]

Start with:
maxSum = currentSum = -2
start = end = tempStart = 0

i = 1 → 1 > -2 + 1 → currentSum = 1, tempStart = 1
      → currentSum > maxSum → maxSum = 1, start = 1, end = 1

i = 2 → -3 > 1 + (-3)? No → currentSum = -2

i = 3 → 4 > -2 + 4 → currentSum = 4, tempStart = 3
      → maxSum = 4, start = 3, end = 3

i = 4 → -1 → currentSum = 3 → still less than maxSum

i = 5 → 2 → currentSum = 5 → maxSum = 5, end = 5

i = 6 → 1 → currentSum = 6 → maxSum = 6, end = 6 ✅

i = 7 → -5 → currentSum = 1

i = 8 → 4 → currentSum = 5 → maxSum still 6

✅ Subarray: arr[3..6] = [4, -1, 2, 1]
```

---

### 🧑‍💻 JavaScript Code (Print Subarray + Sum)

```javascript
function printMaxSubArray(nums) {
  let maxSum = nums[0];
  let currentSum = nums[0];
  let start = 0;
  let end = 0;
  let tempStart = 0;

  for (let i = 1; i < nums.length; i++) {
    if (nums[i] > currentSum + nums[i]) {
      currentSum = nums[i];
      tempStart = i;
    } else {
      currentSum += nums[i];
    }

    if (currentSum > maxSum) {
      maxSum = currentSum;
      start = tempStart;
      end = i;
    }
  }

  console.log("Maximum sum:", maxSum);
  console.log("Subarray:", nums.slice(start, end + 1));
}

// Example
printMaxSubArray([-2, 1, -3, 4, -1, 2, 1, -5, 4]);
```

---

#### ✅ Output:

```
Maximum sum: 6
Subarray: [4, -1, 2, 1]
```

---

### ⏱ Time & Space Complexity

| Metric           | Value |
| ---------------- | ----- |
| Time Complexity  | O(n)  |
| Space Complexity | O(1)  |
| In-place         | ✅    |

---

### 🧠 Summary

- This is a **beautiful extension** of Kadane’s Algorithm
- By keeping **start/end pointers**, you can recover the subarray
- Still works in **linear time** with no extra space

---

## 10. **Rearrange the Array in Alternating Positive and Negative Items**

> Given an array of **positive and negative integers**, rearrange the elements so that:

- **Positive and negative numbers alternate**.
- The **relative order** should be **preserved** as much as possible.
- The number of positive and negative numbers **need not be equal**.

If one type of number is **exhausted**, simply append the remaining ones at the end.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: [1, 2, 3, -4, -1, 4];
Output: [1, -4, 2, -1, 3, 4];
```

#### Test Case 2:

```js
Input: [-5, -2, 5, 2, 4, 7, 1, 8, 0, -8];
Output: [5, -5, 2, -2, 4, -8, 7, 1, 8, 0];
```

#### Test Case 3:

```js
Input: [-1, -2, -3, 4, 5];
Output: [4, -1, 5, -2, -3];
```

---

### 💡 Intuition

#### 🔹 Step 1:

Separate all **positive** and **negative** numbers into **two queues (or arrays)**.

#### 🔹 Step 2:

Start picking alternately from positive and negative arrays.

---

### 🔄 Dry Run

```js
Input: [1, 2, 3, -4, -1, 4]

Positives: [1, 2, 3, 4]
Negatives: [-4, -1]

Result:
- Pick 1 → positive
- Pick -4 → negative
- Pick 2 → positive
- Pick -1 → negative
- Pick 3 → positive
- Pick 4 → positive (negatives exhausted)

Output: [1, -4, 2, -1, 3, 4]
```

---

### 🧑‍💻 JavaScript Code (Preserve Order)

```javascript
function rearrangeAlternatePosNeg(arr) {
  const pos = [];
  const neg = [];

  for (let num of arr) {
    if (num >= 0) pos.push(num);
    else neg.push(num);
  }

  const result = [];
  let i = 0,
    j = 0;

  // Start with positive if it comes first
  let turn = pos.length >= neg.length ? "pos" : "neg";

  while (i < pos.length && j < neg.length) {
    if (turn === "pos") {
      result.push(pos[i++]);
      turn = "neg";
    } else {
      result.push(neg[j++]);
      turn = "pos";
    }
  }

  // Append remaining elements
  while (i < pos.length) result.push(pos[i++]);
  while (j < neg.length) result.push(neg[j++]);

  return result;
}

// Test
console.log(rearrangeAlternatePosNeg([1, 2, 3, -4, -1, 4]));
console.log(rearrangeAlternatePosNeg([-5, -2, 5, 2, 4, 7, 1, 8, 0, -8]));
console.log(rearrangeAlternatePosNeg([-1, -2, -3, 4, 5]));
```

---

### ⏱ Time & Space Complexity

| Metric           | Value |
| ---------------- | ----- |
| Time Complexity  | O(n)  |
| Space Complexity | O(n)  |
| Stable Order     | ✅    |
| In-place         | ❌    |

---

### ✅ Summary

| Feature          | Value           |
| ---------------- | --------------- |
| Order Preserved  | ✅ Yes          |
| Alternating Sign | ✅ Yes          |
| Equal Count Req  | ❌ Not required |

---

## 11. **Next Permutation**

Given an array of integers `nums`,

> Rearrange the numbers into the **next lexicographically greater permutation**.

If such arrangement is **not possible** (i.e., it's the last permutation), rearrange it as the **lowest possible order** (i.e., sorted in ascending order).

The replacement must be **in-place**, with only constant extra memory.

---

### Test Cases

#### est Case 1:

```js
Input: [1, 2, 3];
Output: [1, 3, 2];
```

#### est Case 2:

```js
Input: [3, 2, 1];
Output: [1, 2, 3]; // last permutation → reset
```

#### est Case 3:

```js
Input: [1, 1, 5];
Output: [1, 5, 1];
```

---

### Intuition

We want to generate the **next lexicographic arrangement**.
If you were listing all permutations in increasing order, this one would come right **after the current one**.

We follow **3 main steps**:

---

### Algorithm Steps

1. **Find the breakpoint (pivot)**:
   Traverse from right → find first index `i` such that `nums[i] < nums[i + 1]`.
   This is the point where we can still make a greater permutation.

2. **Find the number just greater than nums\[i]** (on the right) and **swap them**

3. **Reverse the part after index `i`** (i.e., from `i+1` to end) to get the smallest possible next permutation

---

### Dry Run — Descriptive Step-by-Step

Let’s dry run this example:

#### xample:

```js
Input: [1, 3, 5, 4, 2];
```

---

#### Step 1: Find the first decreasing element from the end

Scan from right:

- `2 < 4`? No
- `4 < 5`? No
- `5 < 3`? No
- `3 < 5`? ✅ Yes → **pivot = index 1**, value `3`

This is the index we want to change to get a greater permutation.

---

#### Step 2: Find the element just larger than `3` (on the right side)

From the right, look for the **smallest element > 3**:

- Check: 2 → No
- Check: 4 → ✅ Yes
- 4 is greater than 3 → we’ll **swap** them.

After swapping:

```js
[1, 4, 5, 3, 2];
```

---

#### Step 3: Reverse the part after the pivot (from index 2 to end)

That is, reverse `[5, 3, 2]` → becomes `[2, 3, 5]`

Final result:

```js
[1, 4, 2, 3, 5];
```

✅ This is the next permutation!

---

### 🧑 JavaScript Code

```javascript
function nextPermutation(nums) {
  let n = nums.length;
  let i = n - 2;

  // Step 1: Find first decreasing element from right
  while (i >= 0 && nums[i] >= nums[i + 1]) {
    i--;
  }

  if (i >= 0) {
    // Step 2: Find just larger element to swap
    let j = n - 1;
    while (nums[j] <= nums[i]) {
      j--;
    }
    [nums[i], nums[j]] = [nums[j], nums[i]];
  }

  // Step 3: Reverse the right part
  let left = i + 1,
    right = n - 1;
  while (left < right) {
    [nums[left], nums[right]] = [nums[right], nums[left]];
    left++;
    right--;
  }

  return nums; // just for display
}
```

---

### Time & Space Complexity

| Metric             | Value |
| ------------------ | ----- |
| Time Complexity    | O(n)  |
| Space Complexity   | O(1)  |
| In-place operation | ✅    |

---

### Summary

| Step   | Description                            |
| ------ | -------------------------------------- |
| Step 1 | Find first decreasing point from end   |
| Step 2 | Swap it with next larger number        |
| Step 3 | Reverse the tail to get minimal change |

---

## 12. **Longest Consecutive Sequence in an Array**

Given an **unsorted array** of integers `nums`,

> Find the length of the **longest sequence of consecutive integers**.

**You must solve it in O(n) time.**

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: [100, 4, 200, 1, 3, 2]
Output: 4
Explanation: The longest consecutive sequence is [1, 2, 3, 4]
```

#### Test Case 2:

```js
Input: [0, 3, 7, 2, 5, 8, 4, 6, 0, 1]
Output: 9
Explanation: Sequence is [0, 1, 2, 3, 4, 5, 6, 7, 8]
```

---

### 💡 Intuition

This is about finding the **longest group of connected numbers** regardless of their positions.

Brute force involves sorting, but that takes `O(n log n)`.
We need a way to check if **`num + 1` exists quickly**, and for that, we use a **HashSet**.

---

### ✅ Approach: Using HashSet (O(n))

#### 🔹 Core Idea:

- Put all elements into a **set**.
- For every number, check if it is the **start of a sequence** by checking if `(num - 1)` is **not in the set**.
- From that starting point, keep incrementing while `num + 1` is in the set.
- Track the **max sequence length**.

---

#### 🔄 Dry Run

```js
Input: [100, 4, 200, 1, 3, 2]

Set: {1, 2, 3, 4, 100, 200}

Iterate through each number:

- 100 → 99 not in set → start = 100 → sequence: [100] → length = 1
- 4 → 3 in set → skip (not start of sequence)
- 200 → 199 not in set → start = 200 → sequence: [200] → length = 1
- 1 → 0 not in set → start = 1 → check 2, 3, 4 → length = 4 ✅
- 3 → 2 in set → skip
- 2 → 1 in set → skip

✅ Maximum length = 4
```

---

### 🧑‍💻 JavaScript Code

```javascript
function longestConsecutive(nums) {
  const numSet = new Set(nums);
  let maxLength = 0;

  for (let num of numSet) {
    if (!numSet.has(num - 1)) {
      let currentNum = num;
      let count = 1;

      while (numSet.has(currentNum + 1)) {
        currentNum++;
        count++;
      }

      maxLength = Math.max(maxLength, count);
    }
  }

  return maxLength;
}
```

---

### ⏱ Time & Space Complexity

| Metric           | Value |
| ---------------- | ----- |
| Time Complexity  | O(n)  |
| Space Complexity | O(n)  |
| In-place         | ❌    |

---

### ✅ Summary

| Step                          | Description                               |
| ----------------------------- | ----------------------------------------- |
| Use Set                       | For O(1) lookups                          |
| Start from num - 1 not in set | Ensures you only count each sequence once |
| Increment count               | For each consecutive element              |

---

### ❌ Brute Force (For Reference Only)

```javascript
function longestConsecutiveBrute(nums) {
  if (nums.length === 0) return 0;
  nums.sort((a, b) => a - b);

  let maxLen = 1,
    currLen = 1;

  for (let i = 1; i < nums.length; i++) {
    if (nums[i] === nums[i - 1]) continue;
    if (nums[i] === nums[i - 1] + 1) {
      currLen++;
    } else {
      currLen = 1;
    }
    maxLen = Math.max(maxLen, currLen);
  }

  return maxLen;
}
```

| Time  | O(n log n) due to sort |
| ----- | ---------------------- |
| Space | O(1) if sort in-place  |

---

Would you like a version that **returns the actual sequence** too?
I can help you modify the code to do that next!

## 13. Set Matrix Zeros

Given a 2D matrix,

> If any cell is **0**, set its entire **row and column to 0**.

You must do it **in-place** (i.e., **without using extra space** for another matrix).

---

### 🧪 Test Case

#### Input:

```js
[
  [1, 1, 1],
  [1, 0, 1],
  [1, 1, 1],
];
```

#### Output:

```js
[
  [1, 0, 1],
  [0, 0, 0],
  [1, 0, 1],
];
```

---

### 💡 Intuition

When you find a `0`, you have to mark its entire row and column as 0.
But if you modify the matrix **immediately**, you will mess up the rest of the matrix.

So we need to **record the rows and columns** that need to be zeroed **before** making any changes.

---

### 🔁 Approach 1: Brute Force

#### 🔹 Steps:

1. When you find a `0`, mark its row and column somewhere.
2. Use a copy or extra arrays for tracking.

#### 🔸 Time: O(m × n)

#### 🔸 Space: O(m + n) – 2 arrays for rows and columns

---

### 🧠 Optimal Approach (O(1) Extra Space)

Use **first row and first column as markers**!

#### 🔹 Strategy:

- Use `matrix[0][j]` to indicate if column `j` should be zero.
- Use `matrix[i][0]` to indicate if row `i` should be zero.
- Use separate boolean to track if `firstCol` should be zero (because `matrix[0][0]` is shared).

---

### 🔄 Dry Run

#### Input:

```js
[
  [1, 1, 1],
  [1, 0, 1],
  [1, 1, 1],
];
```

1. Scan matrix:

   - At (1,1) → it's 0 → mark `matrix[1][0] = 0` and `matrix[0][1] = 0`
   - Markers now:

     ```js
     matrix = [
       [1, 0, 1],
       [0, 0, 1],
       [1, 1, 1],
     ];
     ```

2. Loop from (1,1) again:

   - If `matrix[i][0] == 0` or `matrix[0][j] == 0`, set `matrix[i][j] = 0`

3. Final Output:

   ```js
   [
     [1, 0, 1],
     [0, 0, 0],
     [1, 0, 1],
   ];
   ```

---

### 🧑‍💻 JavaScript Code (Optimal)

```javascript
function setZeroes(matrix) {
  let m = matrix.length;
  let n = matrix[0].length;
  let firstColZero = false;

  // Step 1: use first row and first column as markers
  for (let i = 0; i < m; i++) {
    if (matrix[i][0] === 0) firstColZero = true;

    for (let j = 1; j < n; j++) {
      if (matrix[i][j] === 0) {
        matrix[i][0] = 0; // mark row
        matrix[0][j] = 0; // mark column
      }
    }
  }

  // Step 2: set zero based on markers
  for (let i = 1; i < m; i++) {
    for (let j = 1; j < n; j++) {
      if (matrix[i][0] === 0 || matrix[0][j] === 0) {
        matrix[i][j] = 0;
      }
    }
  }

  // Step 3: zero first row if needed
  if (matrix[0][0] === 0) {
    for (let j = 0; j < n; j++) {
      matrix[0][j] = 0;
    }
  }

  // Step 4: zero first column if needed
  if (firstColZero) {
    for (let i = 0; i < m; i++) {
      matrix[i][0] = 0;
    }
  }

  return matrix; // for display
}
```

---

### ⏱ Time and Space Complexity

| Metric           | Value    |
| ---------------- | -------- |
| Time Complexity  | O(m × n) |
| Space Complexity | O(1) ✅  |
| In-place         | ✅       |

---

### ✅ Summary

| Approach        | Time   | Space   | In-place | Notes                  |
| --------------- | ------ | ------- | -------- | ---------------------- |
| Brute Force     | O(m×n) | O(m+n)  | ❌       | Simple but not optimal |
| Optimal (Marks) | O(m×n) | O(1) ✅ | ✅       | Smart use of matrix    |

---

## 14.**Rotate Matrix by 90 Degrees (Clockwise)**

> Given an `n x n` square matrix, rotate the matrix **by 90 degrees clockwise**, **in-place**.

---

### 🧪 Test Case

#### Input:

```js
[
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
];
```

#### Output:

```js
[
  [7, 4, 1],
  [8, 5, 2],
  [9, 6, 3],
];
```

---

### 💡 Intuition

Rotating the matrix by 90° clockwise is equivalent to:

1. **Transposing** the matrix
2. **Reversing each row**

---

### 🔁 Step-by-Step Dry Run

Let's use the input:

```
Original:
[
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]
```

---

#### 🔹 Step 1: Transpose the Matrix

Swap elements at `(i, j)` with `(j, i)` where `i < j`

```text
Before Transpose:
1 2 3
4 5 6
7 8 9

Transpose:
1 4 7
2 5 8
3 6 9
```

---

#### 🔹 Step 2: Reverse Each Row

```text
Before Reversing:
1 4 7 → 7 4 1
2 5 8 → 8 5 2
3 6 9 → 9 6 3
```

✅ Final Matrix:

```js
[
  [7, 4, 1],
  [8, 5, 2],
  [9, 6, 3],
];
```

---

### 🧑‍💻 JavaScript Code

```javascript
function rotateMatrix(matrix) {
  const n = matrix.length;

  // Step 1: Transpose
  for (let i = 0; i < n; i++) {
    for (let j = i + 1; j < n; j++) {
      [matrix[i][j], matrix[j][i]] = [matrix[j][i], matrix[i][j]];
    }
  }

  // Step 2: Reverse each row
  for (let i = 0; i < n; i++) {
    matrix[i].reverse();
  }

  return matrix; // For display
}
```

---

### ⏱ Time & Space Complexity

| Metric           | Value   |
| ---------------- | ------- |
| Time Complexity  | O(n²)   |
| Space Complexity | O(1) ✅ |
| In-place         | ✅ Yes  |

---

### 🧠 Key Concepts

- **Transpose**: Turn rows into columns
- **Reverse Rows**: Flip each row to finish the 90° rotation

---

### ✅ Summary

| Step             | What it does                            |
| ---------------- | --------------------------------------- |
| Transpose        | Swap `matrix[i][j]` with `matrix[j][i]` |
| Reverse each row | Mirror each row for 90° effect          |

---

## 15. Print the Matrix in Spiral Order

> Given a 2D matrix, print all elements in **spiral order**, starting from the **top-left** and moving clockwise.

---

### 🧪 Test Case

#### Input:

```js
[
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
];
```

#### Output:

```js
[1, 2, 3, 6, 9, 8, 7, 4, 5];
```

---

### 💡 Intuition

We can treat the matrix like **layers or loops**:

- First loop: Top row → Right col → Bottom row → Left col
- Then go one level inside and repeat.

We use 4 pointers to represent boundaries:

- `top`, `bottom`, `left`, `right`

We move in 4 directions repeatedly until the pointers meet.

---

### 🔄 Dry Run

#### Matrix:

```
1 2 3
4 5 6
7 8 9
```

#### Initial boundaries:

- `top = 0`
- `bottom = 2`
- `left = 0`
- `right = 2`

##### Step-by-step:

1. Left to right → `1 2 3`
2. Top to bottom → `6 9`
3. Right to left → `8 7`
4. Bottom to top → `4`

Then:

- Update: `top = 1`, `bottom = 1`, `left = 1`, `right = 1`

5. Left to right → `5`

✅ Final spiral order:

```js
[1, 2, 3, 6, 9, 8, 7, 4, 5];
```

---

### 🧑‍💻 JavaScript Code

```javascript
function spiralOrder(matrix) {
  const result = [];
  if (!matrix.length) return result;

  let top = 0,
    bottom = matrix.length - 1,
    left = 0,
    right = matrix[0].length - 1;

  while (top <= bottom && left <= right) {
    // Move left to right
    for (let i = left; i <= right; i++) {
      result.push(matrix[top][i]);
    }
    top++;

    // Move top to bottom
    for (let i = top; i <= bottom; i++) {
      result.push(matrix[i][right]);
    }
    right--;

    // Move right to left (if row remains)
    if (top <= bottom) {
      for (let i = right; i >= left; i--) {
        result.push(matrix[bottom][i]);
      }
      bottom--;
    }

    // Move bottom to top (if col remains)
    if (left <= right) {
      for (let i = bottom; i >= top; i--) {
        result.push(matrix[i][left]);
      }
      left++;
    }
  }

  return result;
}
```

---

### ⏱ Time & Space Complexity

| Metric           | Value                         |
| ---------------- | ----------------------------- |
| Time Complexity  | O(m × n)                      |
| Space Complexity | O(1) (excluding output array) |

---

### ✅ Summary

| Step          | Action                |
| ------------- | --------------------- |
| Left to Right | Traverse top row      |
| Top to Bottom | Traverse right column |
| Right to Left | Traverse bottom row   |
| Bottom to Top | Traverse left column  |
| Repeat        | Reduce the boundary   |

---

## 16. Count Subarrays with Given Sum

### 👉 Problem Statement

> Given an array of integers `nums` and an integer `k`,
> count the **total number of continuous subarrays** whose sum equals to `k`.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: nums = [1, 1, 1], k = 2
Output: 2
Explanation: [1,1] appears twice
```

#### Test Case 2:

```js
Input: nums = [1, 2, 3], k = 3
Output: 2
Explanation: [1, 2] and [3]
```

---

### 💡 Intuition

Brute force is simple — try every subarray and check its sum. But it's slow.

To solve this in **O(n)** time, we use:

> **Prefix Sum + HashMap**

---

### 🔁 Core Idea

Let’s define:

- `prefixSum`: sum of elements from index `0` to `i`
- If `prefixSum - k` has occurred before, it means a subarray with sum `k` exists

We use a `Map` to store:

- Frequency of each `prefixSum`

---

#### 🧠 Dry Run

##### Example: `nums = [1, 2, 3], k = 3`

| Index | num | prefixSum | prefixSum - k | Seen Before? | Count |
| ----- | --- | --------- | ------------- | ------------ | ----- |
| 0     | 1   | 1         | -2            | No           | 0     |
| 1     | 2   | 3         | 0             | ✅ (1 time)  | 1     |
| 2     | 3   | 6         | 3             | ✅ (1 time)  | 2 ✅  |

✅ Final count: `2`

Explanation:

- \[1,2]
- \[3]

---

### 🧑‍💻 JavaScript Code

```javascript
function countSubarraysWithSum(nums, k) {
  const prefixSumCount = new Map();
  prefixSumCount.set(0, 1); // Important base case

  let prefixSum = 0;
  let count = 0;

  for (let num of nums) {
    prefixSum += num;

    if (prefixSumCount.has(prefixSum - k)) {
      count += prefixSumCount.get(prefixSum - k);
    }

    prefixSumCount.set(prefixSum, (prefixSumCount.get(prefixSum) || 0) + 1);
  }

  return count;
}
```

---

### ⏱ Time & Space Complexity

| Metric           | Value |
| ---------------- | ----- |
| Time Complexity  | O(n)  |
| Space Complexity | O(n)  |
| In-place         | ❌    |

---

### ✅ Summary

| Approach            | Time  | Space | Notes                                 |
| ------------------- | ----- | ----- | ------------------------------------- |
| Brute Force         | O(n²) | O(1)  | Try all subarrays                     |
| Prefix Sum + Map ✅ | O(n)  | O(n)  | Most efficient, handles negatives too |

---

# Hard Problems

## 1.🔺 Pascal's Triangle

> Given an integer `numRows`,
> return the first `numRows` of **Pascal's Triangle**.

Each number is the **sum of the two numbers directly above it**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: 5;
Output: [[1], [1, 1], [1, 2, 1], [1, 3, 3, 1], [1, 4, 6, 4, 1]];
```

#### Test Case 2:

```js
Input: 1;
Output: [[1]];
```

---

### 💡 Intuition

Pascal’s Triangle is like a **pyramid of numbers** where:

- The first and last value of every row is always `1`
- Any middle value is formed by:

  ```
  triangle[i][j] = triangle[i - 1][j - 1] + triangle[i - 1][j]
  ```

You build each row using the values from the **previous row**.

---

### 🔄 Dry Run for `numRows = 5`

Let’s build it step-by-step:

```text
Row 0: [1]

Row 1: [1, 1]

Row 2: [1, 1+1, 1] => [1, 2, 1]

Row 3: [1, 2+1, 1+2, 1] => [1, 3, 3, 1]

Row 4: [1, 3+1, 3+3, 1+3, 1] => [1, 4, 6, 4, 1]
```

---

### 🧑‍💻 JavaScript Code

```javascript
function generatePascalTriangle(numRows) {
  const triangle = [];

  for (let i = 0; i < numRows; i++) {
    const row = new Array(i + 1).fill(1);

    for (let j = 1; j < i; j++) {
      row[j] = triangle[i - 1][j - 1] + triangle[i - 1][j];
    }

    triangle.push(row);
  }

  return triangle;
}
```

---

#### 🧪 Example Usage:

```js
console.log(generatePascalTriangle(5));
```

✅ Output:

```js
[[1], [1, 1], [1, 2, 1], [1, 3, 3, 1], [1, 4, 6, 4, 1]];
```

---

### ⏱ Time & Space Complexity

| Metric           | Value       |
| ---------------- | ----------- |
| Time Complexity  | O(numRows²) |
| Space Complexity | O(numRows²) |

---

### ✅ Summary

| Row Index      | Formula for `j-th` value       |
| -------------- | ------------------------------ |
| j = 0 or j = i | 1 (always 1 at borders)        |
| Else           | `row[j] = prev[j-1] + prev[j]` |

---

## 2.Majority Element (Appearing More Than ⌊n/3⌋ Times)

> Given an integer array `nums`, return **all elements** that appear **more than ⌊n/3⌋ times**.

- You must solve it in **O(n)** time and **O(1)** space.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: [3, 2, 3];
Output: [3];
```

#### Test Case 2:

```js
Input: [1, 1, 1, 3, 3, 2, 2, 2];
Output: [1, 2];
```

#### Test Case 3:

```js
Input: [1, 2, 3, 4];
Output: [];
```

---

### 💡 Intuition

In any array of size `n`, **there can be at most 2 elements** that appear more than `n/3` times.

This is a generalized version of the **Boyer-Moore Voting Algorithm** used for the classic majority (> n/2) element.

---

### 🧠 Algorithm Steps (Boyer-Moore for n/3)

1. **First Pass (Voting Phase):**

   - Use two candidate variables and their counts.
   - Try to assign or reduce votes as you iterate through the array.

2. **Second Pass (Verification Phase):**

   - Count how many times the candidates occur.
   - Include only those that appear > ⌊n/3⌋ times.

---

### 🔄 Dry Run

#### Example: `nums = [1, 1, 1, 3, 3, 2, 2, 2]`

**Pass 1 (Voting):**

- Start: `candidate1 = null`, `count1 = 0`, `candidate2 = null`, `count2 = 0`
- 1 → candidate1 assigned to 1 → count1 = 1
- 1 → count1 = 2
- 1 → count1 = 3
- 3 → candidate2 = 3 → count2 = 1
- 3 → count2 = 2
- 2 → neither matches → decrement both counts → count1 = 2, count2 = 1
- 2 → neither matches → decrement both → count1 = 1, count2 = 0
- 2 → candidate2 = 2 → count2 = 1

After Pass 1:

- candidate1 = 1
- candidate2 = 2

**Pass 2 (Verification):**

- Count 1 → appears 3 times
- Count 2 → appears 3 times
- n = 8, ⌊n/3⌋ = 2

✅ Output: \[1, 2]

---

### 🧑‍💻 JavaScript Code

```javascript
function majorityElement(nums) {
  let count1 = 0,
    count2 = 0;
  let candidate1 = null,
    candidate2 = null;

  // Pass 1: Find potential candidates
  for (let num of nums) {
    if (num === candidate1) {
      count1++;
    } else if (num === candidate2) {
      count2++;
    } else if (count1 === 0) {
      candidate1 = num;
      count1 = 1;
    } else if (count2 === 0) {
      candidate2 = num;
      count2 = 1;
    } else {
      count1--;
      count2--;
    }
  }

  // Pass 2: Verify actual counts
  count1 = 0;
  count2 = 0;

  for (let num of nums) {
    if (num === candidate1) count1++;
    else if (num === candidate2) count2++;
  }

  const result = [];
  const n = nums.length;
  if (count1 > Math.floor(n / 3)) result.push(candidate1);
  if (count2 > Math.floor(n / 3)) result.push(candidate2);

  return result;
}
```

---

### ⏱ Time & Space Complexity

| Metric           | Value   |
| ---------------- | ------- |
| Time Complexity  | O(n)    |
| Space Complexity | O(1) ✅ |
| In-place         | ✅      |

---

### ✅ Summary

| Step        | Action                                     |
| ----------- | ------------------------------------------ |
| First Pass  | Select up to 2 potential majority elements |
| Second Pass | Count and verify occurrences               |
| Output      | Elements > ⌊n/3⌋ occurrences               |

---

## 3.🔍 3-Sum Problem

> Given an array `nums` of `n` integers, return **all unique triplets** `[nums[i], nums[j], nums[k]]` such that:

- `i ≠ j ≠ k`, and
- `nums[i] + nums[j] + nums[k] == 0`.

The solution set must **not contain duplicate triplets**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: [-1, 0, 1, 2, -1, -4];
Output: [
  [-1, -1, 2],
  [-1, 0, 1],
];
```

#### Test Case 2:

```js
Input: [0, 1, 1];
Output: [];
```

#### Test Case 3:

```js
Input: [0, 0, 0];
Output: [[0, 0, 0]];
```

---

### 💡 Intuition

This is a classic **"two-pointer"** problem built on **sorting**.
We fix one number (`nums[i]`) and try to find two others that sum up to `-nums[i]`.

Sorting helps in:

- Easily **skipping duplicates**
- Using **two pointers** to find pairs efficiently

---

### 🧠 Approach (Optimal with Sorting + Two Pointers)

1. **Sort** the array
2. Loop through each element `i` from `0` to `n-3`:

   - Skip duplicates of `nums[i]`
   - For each `i`, use **two pointers**: `left = i + 1` and `right = n - 1`
   - Calculate `sum = nums[i] + nums[left] + nums[right]`

     - If `sum == 0`: push triplet to result, move both pointers
     - If `sum < 0`: move `left` forward
     - If `sum > 0`: move `right` backward

---

### 🔁 Dry Run

#### Input: `[-1, 0, 1, 2, -1, -4]`

After sorting: `[-4, -1, -1, 0, 1, 2]`

Loop over each index `i`:

- `i = 0` → `nums[i] = -4` → target = 4 → try to find 2 numbers = 4 → No valid pair
- `i = 1` → `nums[i] = -1`

  - left = 2 (`-1`), right = 5 (`2`)
  - sum = `-1 + -1 + 2 = 0` ✅ triplet found → `[-1, -1, 2]`
  - move both pointers
  - next sum = `-1 + 0 + 1 = 0` ✅ → `[-1, 0, 1]`

- `i = 2` → `nums[i] = -1` again → skip duplicate
- and so on...

✅ Result: `[[-1, -1, 2], [-1, 0, 1]]`

---

### 🧑‍💻 JavaScript Code

```javascript
function threeSum(nums) {
  const result = [];
  nums.sort((a, b) => a - b); // Step 1: Sort the array

  for (let i = 0; i < nums.length - 2; i++) {
    if (i > 0 && nums[i] === nums[i - 1]) continue; // skip duplicates

    let left = i + 1;
    let right = nums.length - 1;

    while (left < right) {
      const sum = nums[i] + nums[left] + nums[right];

      if (sum === 0) {
        result.push([nums[i], nums[left], nums[right]]);

        // Skip duplicates for left and right
        while (left < right && nums[left] === nums[left + 1]) left++;
        while (left < right && nums[right] === nums[right - 1]) right--;

        left++;
        right--;
      } else if (sum < 0) {
        left++;
      } else {
        right--;
      }
    }
  }

  return result;
}
```

---

### ⏱ Time & Space Complexity

| Metric           | Value                    |
| ---------------- | ------------------------ |
| Time Complexity  | O(n²)                    |
| Space Complexity | O(1) + O(k) (for output) |

---

### ✅ Summary

| Step              | Description                             |
| ----------------- | --------------------------------------- |
| Sort              | To enable two-pointer and deduplication |
| Fix first element | Loop through each unique number         |
| Two-pointer       | Find two numbers that sum to `-nums[i]` |
| Skip duplicates   | Avoid repeating triplets                |

---

### ⚠️ Edge Cases

- `[0, 0, 0]` → must only return one triplet: `[0, 0, 0]`
- Duplicates must be **avoided**

---

### 🧠 Alternative Approach: Using Left & Right Hashmaps

#### 💡 Idea:

- Loop through each number in the array and **fix** it as the middle element (`nums[j]`).
- Use two hashmaps:

  - `leftMap`: frequencies of numbers before index `j`
  - `rightMap`: frequencies of numbers after index `j`

- For each `nums[j]`, look for two numbers `nums[i]` (in left) and `nums[k]` (in right) such that:

  ```
  nums[i] + nums[j] + nums[k] == 0
  → nums[i] + nums[k] == -nums[j]
  ```

---

### 🧑‍💻 JavaScript Code (Left & Right Hashmap)

```javascript
function threeSumHashMap(nums) {
  const resultSet = new Set();
  const result = [];

  const n = nums.length;
  const freqMap = new Map();

  // Build frequency map
  for (const num of nums) {
    freqMap.set(num, (freqMap.get(num) || 0) + 1);
  }

  for (let j = 0; j < n; j++) {
    const leftMap = new Map();
    const rightMap = new Map(freqMap);

    // Decrease count of nums[j] in rightMap since it's the middle element now
    rightMap.set(nums[j], rightMap.get(nums[j]) - 1);

    for (let i = 0; i < j; i++) {
      leftMap.set(nums[i], (leftMap.get(nums[i]) || 0) + 1);
    }

    for (let k = j + 1; k < n; k++) {
      rightMap.set(nums[k], rightMap.get(nums[k]) - 1);

      const target = -nums[j] - nums[k];
      if (leftMap.get(target)) {
        const triplet = [target, nums[j], nums[k]].sort((a, b) => a - b);
        resultSet.add(triplet.toString());
      }
    }
  }

  for (const tripletStr of resultSet) {
    result.push(tripletStr.split(",").map(Number));
  }

  return result;
}
```

---

### ⏱ Time & Space Complexity

| Metric           | Value                        |
| ---------------- | ---------------------------- |
| Time Complexity  | \~O(n²)                      |
| Space Complexity | O(n²) (set + left/right map) |

---

### ✅ Summary Comparison

| Approach           | Time  | Space | Deduplication | Notes                          |
| ------------------ | ----- | ----- | ------------- | ------------------------------ |
| Two-pointer        | O(n²) | O(1)  | Easy          | Fast and space-efficient       |
| Left-Right Hashmap | O(n²) | O(n²) | Needs `Set`   | Intuitive but heavier on space |

---

## 🎯 4-Sum Problem

> Given an array `nums` of `n` integers and an integer `target`,
> return **all unique quadruplets** `[nums[a], nums[b], nums[c], nums[d]]` such that:

```
a ≠ b ≠ c ≠ d and
nums[a] + nums[b] + nums[c] + nums[d] === target
```

**No duplicate quadruplets** allowed.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: (nums = [1, 0, -1, 0, -2, 2]), (target = 0);
Output: [
  [-2, -1, 1, 2],
  [-2, 0, 0, 2],
  [-1, 0, 0, 1],
];
```

#### Test Case 2:

```js
Input: (nums = [2, 2, 2, 2, 2]), (target = 8);
Output: [[2, 2, 2, 2]];
```

---

### 💡 Intuition

This is an extension of the **Two-Pointer** technique from 3-Sum.

- Fix two numbers using **two nested loops**
- Find the remaining **two numbers** using the **two-pointer approach**

---

### ✅ Approach (Sorted + Two Pointers)

#### 🔹 Steps:

1. **Sort the array**
2. Use 2 nested loops (`i`, `j`) to fix the first two elements.
3. Use `left` and `right` pointers to find remaining two numbers that make up the sum.
4. Skip **duplicate elements** to avoid repeating quadruplets.

---

### 🔁 Dry Run

#### Input: `nums = [1, 0, -1, 0, -2, 2], target = 0`

Sorted: `[-2, -1, 0, 0, 1, 2]`

Let’s fix:

- i = 0 → -2
  j = 1 → -1
  Now, target = 0 - (-2 -1) = **3**
  We look for 2 numbers from rest that sum to 3

Continue in this way and skip duplicates.

---

### 🧑‍💻 JavaScript Code

```javascript
function fourSum(nums, target) {
  nums.sort((a, b) => a - b);
  const result = [];
  const n = nums.length;

  for (let i = 0; i < n - 3; i++) {
    if (i > 0 && nums[i] === nums[i - 1]) continue; // Skip duplicate i

    for (let j = i + 1; j < n - 2; j++) {
      if (j > i + 1 && nums[j] === nums[j - 1]) continue; // Skip duplicate j

      let left = j + 1;
      let right = n - 1;

      while (left < right) {
        const sum = nums[i] + nums[j] + nums[left] + nums[right];

        if (sum === target) {
          result.push([nums[i], nums[j], nums[left], nums[right]]);

          // Skip duplicate left and right
          while (left < right && nums[left] === nums[left + 1]) left++;
          while (left < right && nums[right] === nums[right - 1]) right--;

          left++;
          right--;
        } else if (sum < target) {
          left++;
        } else {
          right--;
        }
      }
    }
  }

  return result;
}
```

---

### ⏱ Time & Space Complexity

| Metric           | Value                      |
| ---------------- | -------------------------- |
| Time Complexity  | O(n³)                      |
| Space Complexity | O(1) + O(k)                |
| In-place         | ✅ (ignoring result array) |

---

### ⚠️ Notes on Duplicates

Avoiding duplicates is key. Use these checks:

- Skip `nums[i]` if it's the same as previous
- Skip `nums[j]` if it's the same as previous inside `j` loop
- Skip `nums[left]` and `nums[right]` inside while loop

---

### ✅ Summary

| Step            | Description                      |
| --------------- | -------------------------------- |
| Sort            | Enables two-pointer search       |
| Fix i, j        | Two loops to fix first 2 numbers |
| Two Pointers    | Search for other 2 numbers       |
| Skip Duplicates | Prevent repeated results         |

---

## 5. LargTest Subarray with 0 Sum

> Given an array of integers `nums`, find the **length of the longest subarray** whose sum is **0**.

---

### Test Cases

#### Test Case 1:

```js
Input: [15, -2, 2, -8, 1, 7, 10, 23]
Output: 5
Explanation: Subarray [-2, 2, -8, 1, 7] has sum 0
```

#### Test Case 2:

```js
Input: [1, 2, 3]
Output: 0
Explanation: No subarray with sum 0
```

#### Test Case 3:

```js
Input: [1, -1, 3, -3, 4]
Output: 4
Explanation: Subarray [1, -1, 3, -3] has sum 0
```

---

### Intuition

If we calculate the **prefix sum** as we iterate through the array:

- If the **prefix sum becomes 0**, then subarray from start to current index has 0 sum.
- If the **same prefix sum is seen again**, the subarray between those indices has sum 0.

We store the **first occurrence** of each prefix sum in a `Map`.

---

### Dry Run

#### Input: `[15, -2, 2, -8, 1, 7, 10, 23]`

| Index | Value | Prefix Sum | First Seen Index | Length | Max Length |
| ----- | ----- | ---------- | ---------------- | ------ | ---------- |
| 0     | 15    | 15         | store 0          |        | 0          |
| 1     | -2    | 13         | store 1          |        | 0          |
| 2     | 2     | 15         | 15 seen at 0     | 2      | 2          |
| 3     | -8    | 7          | store 3          |        | 2          |
| 4     | 1     | 8          | store 4          |        | 2          |
| 5     | 7     | 15         | 15 seen at 0     | 5 ✅   | **5**      |
| 6     | 10    | 25         | store 6          |        | 5          |
| 7     | 23    | 48         | store 7          |        | 5          |

✅ Final Answer: **5**

---

### 🧑 JavaScript Code (Optimal - O(n))

```javascript
function maxLenZeroSumSubarray(nums) {
  const map = new Map(); // prefixSum → index
  let maxLen = 0;
  let prefixSum = 0;

  for (let i = 0; i < nums.length; i++) {
    prefixSum += nums[i];

    if (prefixSum === 0) {
      maxLen = i + 1; // subarray from start to i
    }

    if (map.has(prefixSum)) {
      const prevIndex = map.get(prefixSum);
      maxLen = Math.max(maxLen, i - prevIndex);
    } else {
      map.set(prefixSum, i);
    }
  }

  return maxLen;
}
```

---

### Time & Space Complexity

| Metric           | Value |
| ---------------- | ----- |
| Time Complexity  | O(n)  |
| Space Complexity | O(n)  |
| In-place         | ❌    |

---

### Summary

| Step              | Description                                 |
| ----------------- | ------------------------------------------- |
| Prefix Sum        | Running sum of elements                     |
| Map Storage       | Stores first occurrence of each prefix sum  |
| If Sum Repeats    | Subarray between same sums is of zero total |
| Max Length Update | Track max length of such subarrays          |

---

## 6. Count Subarrays with Given XOR = K

> Given an array `nums` and an integer `K`,
> count the **number of subarrays** whose **XOR is equal to K**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: nums = [4, 2, 2, 6, 4], K = 6
Output: 4
Explanation: Subarrays → [4,2], [6], [2,2,6], [4,2,2,6]
```

#### Test Case 2:

```js
Input: nums = [5, 6, 7, 8, 9], K = 5
Output: 2
Explanation: Subarrays → [5], [6, 7, 8, 9]
```

---

### 💡 Intuition

This is a prefix XOR problem.
Let:

- `prefixXor` be XOR of all elements from `0` to `i`
- If `prefixXor ^ K = somePrevXor`, then subarray from after that index to `i` has XOR = K.

So we need to find how many times `prefixXor ^ K` has occurred before.

We use a `Map` (or object) to store frequency of previous prefix XORs.

---

### 🔁 Dry Run

#### Input: nums = `[4, 2, 2, 6, 4]`, K = 6

| Index | Num | PrefixXor | prefixXor ^ K | Map Count      | Answer |
| ----- | --- | --------- | ------------- | -------------- | ------ |
| 0     | 4   | 4         | 2             | 0              | 0      |
| 1     | 2   | 6         | 0             | 1 (initial) ✅ | 1      |
| 2     | 2   | 4         | 2             | 1              | 2      |
| 3     | 6   | 2         | 4             | 1              | 3      |
| 4     | 4   | 6         | 0             | 1              | 4 ✅   |

✅ Final Answer: **4**

---

### 🧑‍💻 JavaScript Code

```javascript
function countSubarraysWithXOR(nums, K) {
  const freqMap = new Map();
  let count = 0;
  let xor = 0;

  freqMap.set(0, 1); // To handle subarrays starting from index 0

  for (let i = 0; i < nums.length; i++) {
    xor ^= nums[i];

    const required = xor ^ K;

    if (freqMap.has(required)) {
      count += freqMap.get(required);
    }

    freqMap.set(xor, (freqMap.get(xor) || 0) + 1);
  }

  return count;
}
```

---

### ⏱ Time & Space Complexity

| Metric           | Value |
| ---------------- | ----- |
| Time Complexity  | O(n)  |
| Space Complexity | O(n)  |

---

### ✅ Summary

| Concept             | Description                                       |
| ------------------- | ------------------------------------------------- |
| Prefix XOR          | Cumulative XOR while iterating                    |
| Map (XOR frequency) | Stores how often a XOR value has appeared         |
| Key Check           | If `prefixXor ^ K` has been seen → valid subarray |

---

## 7. Merge Overlapping Intervals

> Given an array of intervals where `intervals[i] = [start, end]`,
> merge all overlapping intervals and return an array of **non-overlapping** intervals that **cover all intervals** in the input.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: [
  [1, 3],
  [2, 6],
  [8, 10],
  [15, 18],
];
Output: [
  [1, 6],
  [8, 10],
  [15, 18],
];
```

#### Test Case 2:

```js
Input: [
  [1, 4],
  [4, 5],
];
Output: [[1, 5]];
```

#### Test Case 3:

```js
Input: [
  [1, 10],
  [2, 3],
  [4, 5],
];
Output: [[1, 10]];
```

---

### 💡 Intuition

To merge overlapping intervals:

1. **Sort** the intervals by their starting point.
2. Start with the first interval and compare it with the next:

   - If they **overlap**, merge them by updating the end.
   - If they **don’t**, push the previous interval and move to the next.

This greedy approach ensures that overlapping segments are merged sequentially.

---

### 🔁 Dry Run

#### Input: `[[1, 3], [2, 6], [8, 10], [15, 18]]`

##### Step 1: Sort by starting time

```
[[1, 3], [2, 6], [8, 10], [15, 18]]
```

##### Step 2: Initialize `merged = [[1, 3]]`

- Check \[2, 6] → overlaps with \[1, 3] → merge to \[1, 6]
- Check \[8, 10] → no overlap → push \[1, 6], add \[8, 10]
- Check \[15, 18] → no overlap → push \[8, 10], add \[15, 18]

✅ Final: `[[1, 6], [8, 10], [15, 18]]`

---

### 🧑‍💻 JavaScript Code

```javascript
function mergeIntervals(intervals) {
  if (intervals.length <= 1) return intervals;

  // Step 1: Sort intervals by start time
  intervals.sort((a, b) => a[0] - b[0]);

  const merged = [intervals[0]];

  for (let i = 1; i < intervals.length; i++) {
    const lastMerged = merged[merged.length - 1];
    const current = intervals[i];

    if (current[0] <= lastMerged[1]) {
      // Overlap → merge
      lastMerged[1] = Math.max(lastMerged[1], current[1]);
    } else {
      // No overlap → push current
      merged.push(current);
    }
  }

  return merged;
}
```

---

### ⏱ Time & Space Complexity

| Metric            | Value                       |
| ----------------- | --------------------------- |
| Time Complexity   | O(n log n) (due to sorting) |
| Space Complexity  | O(n)                        |
| In-place possible | ❌ (output is new array)    |

---

### ✅ Summary

| Step        | Description                         |
| ----------- | ----------------------------------- |
| Sort        | By starting time                    |
| Merge logic | If current start ≤ last end → merge |
| Output      | Merged non-overlapping intervals    |

---

## 8. Merge Two Sorted Arrays Without Extra Space

> You are given two sorted arrays `arr1[]` of size `n` and `arr2[]` of size `m`.
> Merge them **in-place** without using extra space such that the final result is sorted and all elements from both arrays are in `arr1` and `arr2`.

---

### 🧪 Test Case

#### Input:

```js
arr1 = [1, 3, 5, 7];
arr2 = [0, 2, 6, 8, 9];
```

#### Output:

```js
arr1 = [0, 1, 2, 3];
arr2 = [5, 6, 7, 8, 9];
```

---

### ❌ Brute Force (Extra Space)

- Combine both arrays into one array
- Sort it
- Copy the first `n` elements to `arr1`, next `m` to `arr2`

🟥 **Not allowed** as it uses extra space (O(n + m)).

---

###

Approach: Compare `last of arr1` with `first of arr2`

#### 🔹 Steps:

1. Traverse from the **end of arr1** and **start of arr2**.
2. If `arr1[i] > arr2[0]`:

   - Swap them.
   - Sort `arr2` again to restore order.

3. Repeat for all elements in `arr1` (from right to left).

> 📌 This works because both arrays are already sorted, and we only need to fix the position of swapped elements.

---

### 🧪 Example

#### Input:

```js
arr1 = [1, 3, 5, 7];
arr2 = [0, 2, 6, 8, 9];
```

#### Process:

1. Compare 7 with 0 → swap → arr1 = \[1, 3, 5, 0], arr2 = \[7, 2, 6, 8, 9]
2. Sort arr2 → \[2, 6, 7, 8, 9]
3. Continue with 5 vs 2 → swap → arr1 = \[1, 3, 2, 0], arr2 = \[5, 6, 7, 8, 9]
4. Sort arr2 → \[5, 6, 7, 8, 9]
5. Repeat until arr1 is fixed

#### Final:

```
arr1 = [0, 1, 2, 3]
arr2 = [5, 6, 7, 8, 9]
```

---

### ✅ JavaScript Code

```javascript
function mergeAndSort(arr1, arr2, n, m) {
  for (let i = n - 1; i >= 0; i--) {
    if (arr1[i] > arr2[0]) {
      // Swap
      [arr1[i], arr2[0]] = [arr2[0], arr1[i]];

      // Re-sort arr2[0..m-1] using insertion for O(m)
      let first = arr2[0];
      let k = 1;
      while (k < m && arr2[k] < first) {
        arr2[k - 1] = arr2[k];
        k++;
      }
      arr2[k - 1] = first;
    }
  }
}
```

---

#### 🔍 Why Insertion Sort for arr2?

Only the **first element** of `arr2` may be out of place after each swap,
so we can sort it with **insertion shift** in **O(m)** instead of full sorting (O(m log m)).

---

### ⏱ Time & Space Complexity

| Metric           | Value     |
| ---------------- | --------- |
| Time Complexity  | O(n \* m) |
| Space Complexity | O(1) ✅   |

---

### ✅ Summary

| Step      | Action                                  |
| --------- | --------------------------------------- |
| Compare   | `arr1[i]` with `arr2[0]`                |
| Swap      | If out of order, swap and re-sort arr2  |
| Efficient | Good for small `m`, simple to implement |

---

## 9. Find the Repeating and Missing Number in an Array

> You are given a read-only array of size `n` containing numbers from `1` to `n`.
> Each number occurs **exactly once**, **except** one number that is **missing**, and one number that is **repeating**.

📌 **Return** both:
`[repeating_number, missing_number]`

---

### 🧪 Test Case

#### Input:

```js
nums = [4, 3, 6, 2, 1, 1];
```

#### Output:

```js
[1, 5]
Explanation:
- 1 is repeated
- 5 is missing
```

---

### 💡 Intuition (Approach 1: Mathematical Formula)

Let:

- `n = nums.length`
- `S = sum of first n natural numbers = n(n+1)/2`
- `S2 = sum of squares of first n natural numbers = n(n+1)(2n+1)/6`

Let:

- `sum_actual = sum of given array`
- `sum_sq_actual = sum of squares of given array`

Let:

- `x = missing number`
- `y = repeating number`

We have two equations:

```
x - y = S - sum_actual        → (1)
x² - y² = S2 - sum_sq_actual  → (2)
```

From (2), use identity:

```
(x + y)(x - y) = S2 - sum_sq_actual
```

Solve for `x` and `y`.

---

### 🧑‍💻 JavaScript Code (Math Approach)

```javascript
function findMissingAndRepeating(nums) {
  const n = nums.length;

  let sum = (n * (n + 1)) / 2;
  let sumSq = (n * (n + 1) * (2 * n + 1)) / 6;

  let actualSum = 0;
  let actualSqSum = 0;

  for (let num of nums) {
    actualSum += num;
    actualSqSum += num * num;
  }

  const diff = sum - actualSum; // x - y
  const sumDiff = sumSq - actualSqSum; // x² - y²

  const add = sumDiff / diff; // x + y

  const x = (diff + add) / 2; // missing
  const y = x - diff; // repeating

  return [y, x];
}
```

---

### 🔁 Dry Run

#### Input: `[4, 3, 6, 2, 1, 1]`

- n = 6
- Sum(1 to 6) = 21
- Sum^2(1 to 6) = 91
- Given sum = 17, sum of squares = 87

Now:

- diff = 21 - 17 = 4 = x - y
- sumDiff = 91 - 87 = 4 = x² - y²
- (x + y)(x - y) = 4 → x + y = 1

Solve:

- x = (4 + 1) / 2 = 2.5
  (Invalid due to decimals → this indicates a better approach is needed for integer-safe solution or you may have overflows)

👉 Use hashing or XOR in such cases too!

---

### ✅ Approach 2: XOR (Optimal + No Overflow)

#### Logic:

Let:

- `XOR_total = XOR(1 to n) ⊕ XOR(arr)`
- The result is: `XOR_total = missing ⊕ repeating`

### ✅ Approach: XOR + Bucket (Rightmost Set Bit)

---

### 💡 Intuition

- Let the array have numbers from 1 to n.

- One number is **missing**, and one is **repeating**.

- Let's say:

  ```
  missing = x
  repeating = y
  ```

- We compute:

  ```js
  xor_all = xor(1 to n) ⊕ xor(array) = x ⊕ y
  ```

- Now we know `x ⊕ y`, but not individually.
  We **isolate the rightmost set bit** in `xor_all` to divide the numbers into two **buckets**:

  - Bucket 1: all numbers with that bit set
  - Bucket 2: all numbers with that bit unset

- Why this works:

  - x and y are different → they must differ in **at least one bit**
  - So, putting them into different groups lets us isolate them

---

### 🧪 Test Case

#### Input:

```js
nums = [4, 3, 6, 2, 1, 1];
```

- Expected Output: `[1, 5]`

  - 1 is repeating
  - 5 is missing

---

### 🧑‍💻 JavaScript Code

```javascript
function findMissingAndRepeating(nums) {
  const n = nums.length;
  let xor = 0;

  // Step 1: XOR all array elements and numbers from 1 to n
  for (let i = 0; i < n; i++) {
    xor ^= nums[i];
    xor ^= i + 1;
  }

  // Step 2: Get rightmost set bit (differs between x and y)
  const rightmostSetBit = xor & ~(xor - 1);

  // Step 3: Divide into two buckets
  let bucket1 = 0,
    bucket2 = 0;
  for (let i = 0; i < n; i++) {
    if (nums[i] & rightmostSetBit) {
      bucket1 ^= nums[i];
    } else {
      bucket2 ^= nums[i];
    }

    if ((i + 1) & rightmostSetBit) {
      bucket1 ^= i + 1;
    } else {
      bucket2 ^= i + 1;
    }
  }

  // Step 4: Find which is missing and which is repeating
  const repeating = nums.includes(bucket1) ? bucket1 : bucket2;
  const missing = xor ^ repeating;

  return [repeating, missing];
}
```

---

### 🔁 Dry Run

Let’s dry-run on:
`nums = [4, 3, 6, 2, 1, 1]`
n = 6

#### Step 1: XOR of all elements and 1 to n

```
XOR = 4 ⊕ 3 ⊕ 6 ⊕ 2 ⊕ 1 ⊕ 1 ⊕ 1 ⊕ 2 ⊕ 3 ⊕ 4 ⊕ 5 ⊕ 6
→ Repeated numbers cancel out
→ XOR = 5 ⊕ 1 = 4
```

So, `xor = 4` → `binary = 100` → rightmost set bit is 3rd bit

---

#### Step 2: Buckets

Divide numbers into two buckets based on the 3rd bit (bit `100`):

| Number            | Bit (100) | Bucket |
| ----------------- | --------- | ------ |
| 4                 | set       | B1     |
| 3                 | not set   | B2     |
| 6                 | set       | B1     |
| 2                 | not set   | B2     |
| 1                 | not set   | B2     |
| 1                 | not set   | B2     |
| **Range: 1 to 6** |           |        |
| 1                 | not set   | B2     |
| 2                 | not set   | B2     |
| 3                 | not set   | B2     |
| 4                 | set       | B1     |
| 5                 | set       | B1     |
| 6                 | set       | B1     |

Now XOR within each bucket:

- Bucket 1 (set): `4 ⊕ 6 ⊕ 4 ⊕ 5 ⊕ 6` = 5
- Bucket 2 (unset): `3 ⊕ 2 ⊕ 1 ⊕ 1 ⊕ 1 ⊕ 2 ⊕ 3` = 1

So:

- One is missing: 5
- One is repeating: 1

✅ Return: `[1, 5]`

---

### ⏱ Time & Space Complexity

| Metric           | Value   |
| ---------------- | ------- |
| Time Complexity  | O(n)    |
| Space Complexity | O(1) ✅ |

---

### ✅ Summary

| Step        | Description                                     |
| ----------- | ----------------------------------------------- |
| XOR all     | Get xor of missing ⊕ repeating                  |
| Set bit     | Isolate rightmost set bit in xor                |
| Divide      | Group elements into 2 buckets based on that bit |
| XOR buckets | Extract missing and repeating separately        |
| Check       | Use includes() to identify missing/repeating    |

---

## 10. Count Inversions in an Array

> Given an array of integers, count how many **inversions** are present.
> An inversion is a pair `(i, j)` such that:

```
i < j and arr[i] > arr[j]
```

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: [1, 2, 3, 4, 5]
Output: 0
Explanation: Array is already sorted, so no inversions.
```

#### Test Case 2:

```js
Input: [5, 4, 3, 2, 1]
Output: 10
Explanation: Every pair is an inversion.
```

#### Test Case 3:

```js
Input: [2, 4, 1, 3, 5]
Output: 3
Explanation: (2,1), (4,1), (4,3) are inversions.
```

---

### 💡 Brute Force (O(n²))

```javascript
function countInversionsBrute(arr) {
  let count = 0;
  const n = arr.length;

  for (let i = 0; i < n; i++) {
    for (let j = i + 1; j < n; j++) {
      if (arr[i] > arr[j]) {
        count++;
      }
    }
  }

  return count;
}
```

#### ⏱ Time: O(n²), Space: O(1)

---

### ✅ Optimal Approach: Merge Sort Modification

#### Key Idea:

Use the merge step of **merge sort**:

- When you pick from the **right array** before the **left**, it means all remaining elements in the left part are **greater**, hence all those are inversions.

---

#### 🔁 Dry Run

##### Input: `[2, 4, 1, 3, 5]`

- Split into \[2, 4] and \[1, 3, 5]
- Merge \[2, 4] → no inversion
- Merge \[1, 3, 5] → no inversion
- Final merge:

  - 1 < 2 → 2 elements left in left part → +2 inversions
  - 3 < 4 → 1 element left in left part → +1 inversion

✅ Total = **3**

---

### 🧑‍💻 JavaScript Code (Merge Sort)

```javascript
function countInversions(arr) {
  function mergeSortAndCount(arr, left, right) {
    if (left >= right) return 0;

    const mid = Math.floor((left + right) / 2);
    let count = 0;

    count += mergeSortAndCount(arr, left, mid);
    count += mergeSortAndCount(arr, mid + 1, right);
    count += mergeAndCount(arr, left, mid, right);

    return count;
  }

  function mergeAndCount(arr, left, mid, right) {
    const leftArr = arr.slice(left, mid + 1);
    const rightArr = arr.slice(mid + 1, right + 1);

    let i = 0,
      j = 0,
      k = left,
      invCount = 0;

    while (i < leftArr.length && j < rightArr.length) {
      if (leftArr[i] <= rightArr[j]) {
        arr[k++] = leftArr[i++];
      } else {
        arr[k++] = rightArr[j++];
        invCount += leftArr.length - i; // all remaining in left are > right[j]
      }
    }

    while (i < leftArr.length) arr[k++] = leftArr[i++];
    while (j < rightArr.length) arr[k++] = rightArr[j++];

    return invCount;
  }

  return mergeSortAndCount(arr, 0, arr.length - 1);
}
```

---

### ⏱ Time & Space Complexity

| Metric           | Value                  |
| ---------------- | ---------------------- |
| Time Complexity  | O(n log n) ✅          |
| Space Complexity | O(n) (for temp arrays) |

---

### ✅ Summary

| Step            | Description                                  |
| --------------- | -------------------------------------------- |
| Brute Force     | Compare each pair → O(n²)                    |
| Merge Sort      | Count during merge step → O(n log n)         |
| Inversion Logic | Right element picked before left → inversion |

---

## 11. Reverse Pairs in an Array

> Given an integer array `nums`, return the **number of reverse pairs**.
> A reverse pair is a pair **(i, j)** such that:

```
i < j and nums[i] > 2 * nums[j]
```

📘 It’s similar to the "Count Inversions" problem but with the condition `nums[i] > 2 * nums[j]`.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: nums = [1, 3, 2, 3, 1]
Output: 2
Explanation: Reverse pairs are (1, 4) and (3, 4)
```

#### Test Case 2:

```js
Input: nums = [2, 4, 3, 5, 1]
Output: 3
Explanation: Reverse pairs are (1, 4), (2, 4), and (3, 4)
```

---

### 💡 Intuition (Optimized Approach)

To efficiently count reverse pairs, we use a **modified Merge Sort** approach:

- While merging two sorted halves (left and right),
- For each element in the left half, count how many elements in the right half satisfy:

  ```js
  nums[i] > 2 * nums[j];
  ```

- Since both halves are sorted, this check can be done using a **two-pointer** strategy in linear time.

Then proceed with regular merge sort to sort the array as part of the process.

---

### 🔁 Dry Run

#### Input: `[2, 4, 3, 5, 1]`

- Split: \[2, 4] and \[3, 5, 1]
- Sort and count:

  - \[2, 4] → no reverse pairs
  - \[3, 5, 1] → \[1, 3, 5], pairs: (3,1), (5,1)

- Merge step:

  - Compare \[2, 4] with \[1, 3, 5]
  - Count reverse pairs across halves: (4,1)

✅ Total = 3 reverse pairs

---

### 🧑‍💻 JavaScript Code

```javascript
function reversePairs(nums) {
  function mergeSort(start, end) {
    if (start >= end) return 0;

    let mid = Math.floor((start + end) / 2);
    let count = mergeSort(start, mid) + mergeSort(mid + 1, end);

    // Count reverse pairs
    let j = mid + 1;
    for (let i = start; i <= mid; i++) {
      while (j <= end && nums[i] > 2 * nums[j]) {
        j++;
      }
      count += j - (mid + 1);
    }

    // Merge step
    const temp = [];
    let left = start,
      right = mid + 1;

    while (left <= mid && right <= end) {
      if (nums[left] <= nums[right]) {
        temp.push(nums[left++]);
      } else {
        temp.push(nums[right++]);
      }
    }

    while (left <= mid) temp.push(nums[left++]);
    while (right <= end) temp.push(nums[right++]);

    for (let i = start; i <= end; i++) {
      nums[i] = temp[i - start];
    }

    return count;
  }

  return mergeSort(0, nums.length - 1);
}
```

---

### ⏱ Time & Space Complexity

| Metric           | Value                 |
| ---------------- | --------------------- |
| Time Complexity  | O(n log n) ✅         |
| Space Complexity | O(n) (for merge step) |

---

### ✅ Summary

| Topic        | Description                                    |
| ------------ | ---------------------------------------------- |
| Reverse Pair | i < j and nums\[i] > 2 \* nums\[j]             |
| Brute Force  | O(n²) — slow for large arrays                  |
| Optimal      | Merge Sort with two-pointer count = O(n log n) |
| Pattern      | Similar to inversion count but stricter        |

---

## 12. Maximum Product Subarray

> Given an integer array `nums`, find the **contiguous subarray** (containing at least one number) which has the **largest product**, and return **that product**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: [2, 3, -2, 4]
Output: 6
Explanation: Subarray [2, 3] has product 6.
```

#### Test Case 2:

```js
Input: [-2, 0, -1]
Output: 0
Explanation: The result cannot be 2, because [-2, -1] is not contiguous due to 0.
```

#### Test Case 3:

```js
Input: [-2, 3, -4]
Output: 24
Explanation: [-2, 3, -4] → (-2) * 3 * (-4) = 24
```

### 💡 Intuition Behind the Prefix & Suffix Approach

#### Why do we need this?

- Product of a subarray may be affected by **negative numbers**.
- **Zeros** reset the product — they split the array into subsegments.
- Multiplying from **left to right (prefix)** might miss something the **right to left (suffix)** catches.

#### What does the code do?

- Iterate from both **left (prefix)** and **right (suffix)** simultaneously.
- If the current prefix or suffix product becomes `0`, reset it to `1`.
- Track the **maximum product seen so far**.

This way, you cover all subarrays from **start to end** and **end to start** in a single pass.

---

### 🔁 Dry Run

#### Input: `[1, 2, -3, 0, -4, -5]`

We track:

- `pre`: left-to-right product
- `suff`: right-to-left product
- `ans`: max product so far

| i   | arr\[i] | arr\[n-i-1] | pre       | suff      | ans |
| --- | ------- | ----------- | --------- | --------- | --- |
| 0   | 1       | -5          | 1         | -5        | 1   |
| 1   | 2       | -4          | 2         | 20        | 20  |
| 2   | -3      | 0           | -6        | 1 (reset) | 20  |
| 3   | 0       | -3          | 1 (reset) | -3        | 20  |
| 4   | -4      | 2           | -4        | -6        | 20  |
| 5   | -5      | 1           | 20        | -6        | 20  |

✅ Final Output: `20`

---

### 🧑‍💻 Code

```javascript
function maxProductSubArray(arr) {
  let n = arr.length;
  let pre = 1,
    suff = 1;
  let ans = Number.MIN_SAFE_INTEGER;

  for (let i = 0; i < n; i++) {
    // Reset on zero
    if (pre === 0) pre = 1;
    if (suff === 0) suff = 1;

    pre *= arr[i]; // Prefix product
    suff *= arr[n - i - 1]; // Suffix product

    ans = Math.max(ans, pre, suff);
  }

  return ans;
}

let arr = [1, 2, -3, 0, -4, -5];
console.log("The maximum product subarray is: " + maxProductSubArray(arr));
```

---

### ⏱ Time & Space Complexity

| Metric           | Value   |
| ---------------- | ------- |
| Time Complexity  | O(n) ✅ |
| Space Complexity | O(1) ✅ |

---

### ✅ Comparison to Other Approaches

| Approach                      | Handles Zeros | Handles Negatives | Time |
| ----------------------------- | ------------- | ----------------- | ---- |
| Kadane-like (min & max track) | ✅            | ✅                | O(n) |
| Prefix + Suffix               | ✅            | ✅                | O(n) |
| Observation-based (segment)   | ✅            | ✅                | O(n) |

---

### 📌 Summary

- Elegant and compact solution ✅
- Uses both prefix and suffix scans to catch all possible subarrays
- Avoids special handling for segments or negatives

---
