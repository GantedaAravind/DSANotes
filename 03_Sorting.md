# 📘 **What is Sorting?**

### 🔠 **Sorting** is the process of **arranging data in a specific order**, typically in **ascending** or **descending** order.

---

## ✅ **Why is Sorting Important?**

- Makes data easier to **search**, **analyze**, and **visualize**
- Essential for algorithms like **Binary Search**
- Used in real-world tasks like **ranking**, **scheduling**, **leaderboards**, etc.

---

## 🔍 **Examples:**

### ➤ Ascending Order:

```js
Input: [5, 2, 9, 1, 3];
Output: [1, 2, 3, 5, 9];
```

### ➤ Descending Order:

```js
Input: [7, 4, 6, 2];
Output: [7, 6, 4, 2];
```

### ➤ Sorting Strings (Alphabetical Order):

```js
Input: ["banana", "apple", "cherry"];
Output: ["apple", "banana", "cherry"];
```

---

# 🔁 Bubble Sort

## 📘 **What is Bubble Sort?**

**Bubble Sort** is a simple comparison-based sorting algorithm.
It **repeatedly steps through the list**, compares adjacent elements, and **swaps them if they are in the wrong order**.

This way, **large elements "bubble up" to the end** with each iteration.

---

## 💡 **How It Works – Intuition**

Imagine air bubbles rising to the surface in water:
In the same way, the largest number in the list keeps moving to the end after each pass.

## 🔍 **Example Input:**

```js
Input array: [5, 1, 4, 2]
```

---

## 📊 Dry Run (Ascending Order)

We perform multiple **passes** over the array:

### 🔁 Pass 1:

```
Compare 5 and 1 → swap → [1, 5, 4, 2]
Compare 5 and 4 → swap → [1, 4, 5, 2]
Compare 5 and 2 → swap → [1, 4, 2, 5] ✅ largest bubbled to the end
```

### 🔁 Pass 2:

```
Compare 1 and 4 → no swap
Compare 4 and 2 → swap → [1, 2, 4, 5]
```

### 🔁 Pass 3:

```
Compare 1 and 2 → no swap ✅ already sorted
```

### ✅ Final Sorted Array: `[1, 2, 4, 5]`

---

## 🧑‍💻 JavaScript Code:

```javascript
function bubbleSort(arr) {
  let n = arr.length;

  for (let i = 0; i < n - 1; i++) {
    let swapped = false;

    for (let j = 0; j < n - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        // Swap using destructuring
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
        swapped = true;
      }
    }

    // If no two elements were swapped in inner loop, array is sorted
    if (!swapped) break;
  }

  return arr;
}
```

---

## 🧠 Key Concepts:

| Feature  | Description                                |
| -------- | ------------------------------------------ |
| Type     | Comparison-based sorting algorithm         |
| Stable   | ✅ Yes (maintains order of equal elements) |
| In-place | ✅ Yes (no extra space needed)             |
| Adaptive | ✅ Yes (optimized version can stop early)  |

---

## ⏱️ Time & Space Complexity

| Case    | Time Complexity | Description                           |
| ------- | --------------- | ------------------------------------- |
| Best    | O(n)            | If already sorted (with swapped flag) |
| Average | O(n²)           | Standard unsorted input               |
| Worst   | O(n²)           | Completely reverse sorted             |
| Space   | O(1)            | In-place sorting                      |

---

## ✅ When to Use Bubble Sort

- For small datasets

## ❌ When NOT to Use

- Large datasets (inefficient)
- Time-critical applications

---

# 🔽 Selection Sort

## 📘 **What is Selection Sort?**

**Selection Sort** is a simple **comparison-based sorting algorithm** that:

- Repeatedly **selects the smallest element** from the **unsorted** part of the array
- Places it in the correct **sorted** position

---

## 💡 **Intuition**

Think of sorting a deck of cards:

- Find the smallest card and place it at the beginning
- Then, find the next smallest from the rest, and so on

---

## 🔍 **Example Input:**

```js
[5, 3, 8, 1];
```

---

## 📊 **Dry Run**

We move through the array and find the **minimum element** in the unsorted part:

### 🔁 Pass 1 (i = 0):

Unsorted part: \[5, 3, 8, 1]
Minimum = 1 → Swap with 5
`→ [1, 3, 8, 5]`

---

### 🔁 Pass 2 (i = 1):

Unsorted part: \[3, 8, 5]
Minimum = 3 → Already in place
`→ [1, 3, 8, 5]`

---

### 🔁 Pass 3 (i = 2):

Unsorted part: \[8, 5]
Minimum = 5 → Swap with 8
`→ [1, 3, 5, 8]`

---

### 🔁 Pass 4 (i = 3):

Only one element left → Already sorted ✅

---

### ✅ Final Output:

```js
[1, 3, 5, 8];
```

---

## 🧑‍💻 JavaScript Code:

```javascript
function selectionSort(arr) {
  const n = arr.length;

  for (let i = 0; i < n - 1; i++) {
    let minIndex = i;

    // Find index of the minimum element
    for (let j = i + 1; j < n; j++) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }

    // Swap the found minimum element with the first unsorted element
    if (minIndex !== i) {
      [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
    }
  }

  return arr;
}
```

---

## 🧠 Key Concepts

| Feature  | Description                             |
| -------- | --------------------------------------- |
| Type     | Comparison-based sorting                |
| Stable   | ❌ No (equal elements may lose order)   |
| In-place | ✅ Yes                                  |
| Adaptive | ❌ No (runs full passes even if sorted) |

---

## ⏱️ Time & Space Complexity

| Case    | Time Complexity | Description                     |
| ------- | --------------- | ------------------------------- |
| Best    | O(n²)           | Always scans full unsorted part |
| Average | O(n²)           | Typical input                   |
| Worst   | O(n²)           | Reverse sorted                  |
| Space   | O(1)            | No extra space used             |

---

## ✅ When to Use Selection Sort

- Small datasets
- When memory is very limited
- When you want predictable behavior

---

## ❌ When NOT to Use

- Large datasets (very inefficient)
- When maintaining relative order of equal items matters

---

# 📥 Insertion Sort

## 📘 **What is Insertion Sort?**

**Insertion Sort** is a simple sorting algorithm that:

- Builds the sorted array **one element at a time**
- Takes each element and **inserts** it into the correct position **among previously sorted elements**

---

## 💡 **Intuition**

Just like **sorting playing cards in your hand**:

- Start with one card
- Take the next card and **insert it at the right spot**
- Repeat for all cards

---

## 🔍 **Example Input:**

```js
[5, 3, 4, 1];
```

---

## 📊 **Dry Run**

### 🔁 Step-by-step (Ascending Order):

Initial array: `[5, 3, 4, 1]`

### Step 1 (i = 1, key = 3):

- Compare 3 with 5 → shift 5 → `[5, 5, 4, 1]`
- Insert 3 → `[3, 5, 4, 1]`

### Step 2 (i = 2, key = 4):

- Compare 4 with 5 → shift 5 → `[3, 5, 5, 1]`
- Compare 4 with 3 → no shift
- Insert 4 → `[3, 4, 5, 1]`

### Step 3 (i = 3, key = 1):

- Compare 1 with 5 → shift 5
- Compare 1 with 4 → shift 4
- Compare 1 with 3 → shift 3
- Insert 1 → `[1, 3, 4, 5]`

✅ Sorted output: `[1, 3, 4, 5]`

---

## 🧑‍💻 JavaScript Code:

```javascript
function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    let key = arr[i];
    let j = i - 1;

    // Shift elements of arr[0...i-1] greater than key
    while (j >= 0 && arr[j] > key) {
      arr[j + 1] = arr[j];
      j--;
    }

    // Insert key at the right position
    arr[j + 1] = key;
  }

  return arr;
}
```

---

## 🧠 Key Concepts

| Feature  | Description                                |
| -------- | ------------------------------------------ |
| Type     | Comparison-based sorting                   |
| Stable   | ✅ Yes (maintains order of equal elements) |
| In-place | ✅ Yes                                     |
| Adaptive | ✅ Yes (faster if array is nearly sorted)  |

---

## ⏱️ Time & Space Complexity

| Case    | Time Complexity | Description          |
| ------- | --------------- | -------------------- |
| Best    | O(n)            | Already sorted array |
| Average | O(n²)           | General case         |
| Worst   | O(n²)           | Reverse sorted       |
| Space   | O(1)            | In-place             |

---

## ✅ When to Use Insertion Sort

- For **small datasets**
- When the input is **nearly sorted**
- When **stability** is required

---

## ❌ When NOT to Use

- On large unsorted arrays (O(n²) is too slow)
- When performance is critical

---

# ⚙️ Merge Sort

## 📘 **What is Merge Sort?**

**Merge Sort** is a **Divide and Conquer** algorithm that:

- **Divides** the array into halves,
- **Recursively sorts** each half,
- And finally **merges** the sorted halves.

---

## 💡 **Intuition**

Like organizing a big messy stack of papers:

- Split into smaller stacks
- Sort each stack
- Merge them back in sorted order

---

## 📊 **Example Input**:

```js
[6, 3, 8, 2];
```

---

## 🔄 **Dry Run (Step-by-Step)**

### ➤ Step 1: Divide

```
[6, 3, 8, 2]
→ Split into [6, 3] and [8, 2]
→ Then [6], [3] and [8], [2]
```

### ➤ Step 2: Sort (Base case)

```
[6] and [3] → Merge → [3, 6]
[8] and [2] → Merge → [2, 8]
```

### ➤ Step 3: Merge final two

```
[3, 6] and [2, 8] → Merge → [2, 3, 6, 8]
```

✅ Final Output: `[2, 3, 6, 8]`

---

## 🧑‍💻 JavaScript Code

```javascript
function mergeSort(arr) {
  if (arr.length <= 1) return arr;

  const mid = Math.floor(arr.length / 2);

  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));

  return merge(left, right);
}

function merge(left, right) {
  const result = [];
  let i = 0,
    j = 0;

  // Merge sorted subarrays
  while (i < left.length && j < right.length) {
    if (left[i] <= right[j]) {
      result.push(left[i]);
      i++;
    } else {
      result.push(right[j]);
      j++;
    }
  }

  // Add any remaining elements
  return result.concat(left.slice(i)).concat(right.slice(j));
}
```

---

## 🧠 Key Concepts

| Feature   | Description                             |
| --------- | --------------------------------------- |
| Type      | Divide and Conquer                      |
| Stable    | ✅ Yes (maintains order of equal items) |
| In-place  | ❌ No (needs extra space)               |
| Recursive | ✅ Yes                                  |

---

## 🧠 **Why `O(n log n)`?**

### Step 1: Understand the Recursion Tree

Let’s assume:

- You are sorting an array of size `n`.

### 🔁 **Each Level of Recursion (log n levels)**

- You divide the array into two halves.
- This splitting continues until each subarray has only one element.
- The number of levels in the recursion tree is:
  ➤ `log₂(n)` — because you're halving the array at every level.

👉 So, the depth of the recursion tree is `log n`.

---

### 🧩 **Work Done at Each Level (O(n))**

At each level of the recursion tree:

- All the elements are part of merging.
- Merging takes linear time for each level (since every element is included in merging once per level).

So the total work per level = `O(n)`.

---

### 🧮 **Total Work = Work per Level × Number of Levels**

```
O(n log n) = O(n) * O(log n)
```

✔️ `n` operations per level
✔️ `log n` levels total

---

## 📌 Final Time Complexity: **O(n log n)**

This is for:

- Best case
- Average case
- Worst case
  Because merge sort **always** divides and merges in the same way regardless of the array's order.

---

## 🧪 Quick Example (Dry Run for Intuition)

Array: `[8, 4, 5, 2]`
Steps:

```
Split:         [8, 4, 5, 2]
              /           \
           [8, 4]         [5, 2]
          /    \         /    \
        [8]    [4]     [5]    [2]

Merge:       [4, 8]     [2, 5]
               \         /
              [2, 4, 5, 8]
```

At each level:

- Total number of elements merged: `n = 4`
- Number of levels: `log₂(4) = 2`

→ So, total work = `2 levels × 4 merges = O(4 log 4) = O(n log n)`

---

## ⏱️ Time & Space Complexity

| Case    | Time Complexity | Description                |
| ------- | --------------- | -------------------------- |
| Best    | O(n log n)      | Always divides in half     |
| Average | O(n log n)      | Regardless of input        |
| Worst   | O(n log n)      | Very consistent            |
| Space   | O(n)            | Needs extra space to merge |

---

## ✅ When to Use Merge Sort

- For **large datasets**
- When you need **consistent performance**
- When **stability** matters

---

## ❌ When NOT to Use

- When memory usage is a concern (uses extra space)
- For small or nearly sorted arrays (Insertion sort is faster)

---

# ⚡ Quick Sort

## 📘 What is Quick Sort?

**Quick Sort** is a **Divide and Conquer** algorithm that:

- Picks a **pivot** element,
- **Partitions** the array into elements **less than** and **greater than** the pivot,
- Recursively sorts the two parts.

---

## 💡 Intuition:

Imagine rearranging books:

- Choose one as a reference (pivot)
- Move smaller ones to its left, bigger ones to its right
- Do the same for each half

---

Certainly! Here's how **Quick Sort** works when the **leftmost element** is chosen as the **pivot**, with a **clear explanation**, **dry run**, and **JavaScript code** for your DSA notes.

---

## 🔍 Example Input:

```js
[6, 3, 8, 2];
```

---

## 🔄 Dry Run (Choose Leftmost Pivot)

**Step 1**: Pivot = 6

- Compare others with 6
- Left = \[3, 2] (less than pivot)
- Right = \[8] (greater than pivot)
  → `quickSort([3, 2]) + [6] + quickSort([8])`

**Step 2**: Sort \[3, 2] → Pivot = 3

- Left = \[2], Right = \[]
  → `[2, 3]`

**Step 3**: \[8] is already sorted

---

### ✅ Final Sorted Output:

```js
[2, 3] + [6] + [8] = [2, 3, 6, 8]
```

---

## 🧑‍💻 JavaScript Code (Pivot = Leftmost Element)

```javascript
function quickSortLeftPivot(arr) {
  if (arr.length <= 1) return arr;

  const pivot = arr[0]; // Choose the first element as pivot
  const left = [];
  const right = [];

  for (let i = 1; i < arr.length; i++) {
    if (arr[i] < pivot) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }

  return [...quickSortLeftPivot(left), pivot, ...quickSortLeftPivot(right)];
}

// Example
console.log(quickSortLeftPivot([6, 3, 8, 2])); // [2, 3, 6, 8]
```

---

## 🧠 Key Concepts

| Feature   | Description                                |
| --------- | ------------------------------------------ |
| Type      | Divide and Conquer                         |
| Stable    | ❌ No (order of equal elements may change) |
| In-place  | ✅ Yes (in optimized versions)             |
| Recursive | ✅ Yes                                     |

---

## ⏱️ **Time Complexities**

| Case        | Time Complexity |
| ----------- | --------------- |
| **Best**    | `O(n log n)`    |
| **Average** | `O(n log n)`    |
| **Worst**   | `O(n²)`         |

---

## 📈 Why These Complexities?

Let’s analyze each case in detail:

---

### ✅ **Best Case: `O(n log n)`**

#### 🔸 When does it happen?

- The pivot **divides the array into two equal halves** every time (balanced partition).

#### 🔸 Why `n log n`?

- At each level, you do **`O(n)` work** for partitioning.
- You get **`log n` levels** if the array is halved every time.

```
Total work = O(n) per level × log n levels = O(n log n)
```

---

### 📊 **Average Case: `O(n log n)`**

#### 🔸 When does it happen?

- The pivot doesn’t always split perfectly but **not too unbalanced** either.
- On average, partitions are like 30-70%, 40-60%, etc.

#### 🔸 Why `n log n` still?

- Though not perfectly balanced, the recursion tree still has roughly `log n` depth on average.
- Each level still involves `O(n)` work for partitioning.

```
Total expected work = O(n log n)
```

➡️ **Randomized pivot** helps achieve this average performance consistently.

---

### ❌ **Worst Case: `O(n²)`**

#### 🔸 When does it happen?

- The pivot always ends up being the **smallest or largest element**.
- This leads to **highly unbalanced partitions**, like one side with `n-1` elements and the other with `0`.

#### 🔸 Why `n²`?

- Recursion depth becomes `n` (every call peels off just one element).
- At each level, partitioning still takes `O(n)` time.

```
Total work = n levels × O(n) per level = O(n²)
```

#### ⚠️ Example:

```text
Input: [1, 2, 3, 4, 5] (sorted array)
Pivot: always choose first or last
→ Terribly unbalanced splits → O(n²)
```

---

## 🧠 Dry Run for Each Case

### Best/Average Case: `[8, 4, 6, 2, 7, 5, 3]`

- Pivot = 5
- Partition → \[4, 2, 3], \[6, 7, 8]
- Balanced → O(n log n)

### Worst Case: `[1, 2, 3, 4, 5, 6, 7]`

- Pivot = first element
- Partition → \[], \[2, 3, 4, 5, 6, 7]
- Skewed → O(n²)

---

## 📦 Space Complexity

| Case          | Space Complexity                            |
| ------------- | ------------------------------------------- |
| In-place sort | `O(log n)` average (due to recursion stack) |
| Worst case    | `O(n)` if skewed recursion                  |

---

## 🛡️ How to Avoid Worst Case?

- Use **randomized pivot**: choose a random element as pivot.
- Or use **median-of-three** pivot selection: choose the median of first, middle, and last.

## ⏱️ Time & Space Complexity

| Case    | Time Complexity | Description                 |
| ------- | --------------- | --------------------------- |
| Best    | O(n log n)      | Perfect partitioning        |
| Average | O(n log n)      | Random input                |
| Worst   | O(n²)           | Already sorted (bad pivot)  |
| Space   | O(log n)        | Due to recursion (in-place) |

---

## ✅ When to Use Quick Sort

- When you need **fast average-case sorting**
- For **large arrays**
- When **memory** is limited (optimized version is in-place)

---

## ❌ When NOT to Use

- For **small arrays** (Insertion Sort is better)
- When **worst-case performance** must be avoided (use Merge Sort)

---

## ✍️ Bonus Tip: Use Random Pivot

To avoid worst-case performance, use a random pivot instead of the first element.

---

# 🔢 Counting Sort

## 📘 **What is Counting Sort?**

**Counting Sort** is a **non-comparison** based sorting algorithm.

> It **counts the frequency** of each number and **builds the sorted array** based on these counts.

---

## ✅ **Best Use Case**:

- Works **only for integers**
- Best when numbers are in a **small, known range**

---

## 🔍 **Example**:

```js
Input:  [4, 2, 2, 8, 3]
Step 1: Count → [0, 0, 2, 1, 1, 0, 0, 0, 1]
Step 2: Sorted → [2, 2, 3, 4, 8]
```

---

## 🧑‍💻 **JavaScript Code**:

```javascript
function countingSort(arr) {
  const max = Math.max(...arr);
  const count = Array(max + 1).fill(0);

  // Count frequencies
  for (let num of arr) {
    count[num]++;
  }

  // Rebuild sorted array
  const result = [];
  for (let i = 0; i < count.length; i++) {
    while (count[i]-- > 0) {
      result.push(i);
    }
  }

  return result;
}
```

---

## ⏱️ **Time & Space Complexity**:

| Case  | Time     | Space |
| ----- | -------- | ----- |
| Best  | O(n + k) | O(k)  |
| Worst | O(n + k) | O(k)  |

- `n` = number of elements
- `k` = range of input (max number)

---

## ✅ Pros:

- Very **fast** when input range is small
- **Stable sort**
- **Non-comparative**

## ❌ Cons:

- Not suitable for **large ranges**
- Only works with **non-negative integers**

---

# 🧮 **Radix Sort**

## 📘 **What is Radix Sort?**

**Radix Sort** is a **non-comparative** sorting algorithm that sorts numbers **digit by digit**, starting from the **least significant digit (LSD)** to the **most significant digit (MSD)**.

It uses a **stable sort** (like Counting Sort) on each digit position.

---

## 🔍 **Example:**

Input:

```js
[170, 45, 75, 90, 802, 24, 2, 66];
```

Sorting steps:

1. **Sort by units** → \[170, 90, 802, 2, 24, 45, 75, 66]
2. **Sort by tens** → \[802, 2, 24, 45, 66, 170, 75, 90]
3. **Sort by hundreds** → \[2, 24, 45, 66, 75, 90, 170, 802] ✅

---

## 🧑‍💻 **JavaScript Code:**

```javascript
function getMax(arr) {
  return Math.max(...arr);
}

function countingSortByDigit(arr, place) {
  const output = new Array(arr.length).fill(0);
  const count = new Array(10).fill(0);

  // Count digit occurrences
  for (let i = 0; i < arr.length; i++) {
    const digit = Math.floor(arr[i] / place) % 10;
    count[digit]++;
  }

  // Compute cumulative count
  for (let i = 1; i < 10; i++) {
    count[i] += count[i - 1];
  }

  // Build output (right to left for stability)
  for (let i = arr.length - 1; i >= 0; i--) {
    const digit = Math.floor(arr[i] / place) % 10;
    output[--count[digit]] = arr[i];
  }

  // Copy to original array
  for (let i = 0; i < arr.length; i++) {
    arr[i] = output[i];
  }
}

function radixSort(arr) {
  const max = getMax(arr);

  for (let place = 1; Math.floor(max / place) > 0; place *= 10) {
    countingSortByDigit(arr, place);
  }

  return arr;
}
```

---

## ⏱️ **Time & Space Complexity:**

| Parameter | Complexity |
| --------- | ---------- |
| Time      | O(n × k)   |
| Space     | O(n + k)   |

- `n` = number of elements
- `k` = number of digits in the maximum number

---

## ✅ **When to Use:**

- When sorting **large numbers**
- When elements are **integers with limited digit length**

---

## ❌ **Limitations:**

- Doesn't work directly with **negative numbers or floats**
- Needs extra space
- Not suitable when digit count `k` is large

---

# 🐚 **Shell Sort**

## 📘 **What is Shell Sort?**

**Shell Sort** is an improved version of **Insertion Sort** that:

- Allows comparisons and swaps **between far elements**
- Gradually reduces the gap between compared elements

> It is named after **Donald Shell**, who introduced it in 1959.

---

## 💡 **Intuition**

Insertion Sort performs poorly on large unsorted arrays.
Shell Sort fixes this by:

- **First sorting distant elements** (using a gap)
- **Then reducing the gap** until it becomes 1 (like insertion sort)

This allows elements to move **faster across the array** and reduces the total number of shifts.

---

## 🔍 **How It Works**

1. Start with a large **gap** (typically `n / 2`)
2. Perform **insertion sort** on elements at that gap
3. Reduce the gap (e.g., `gap = gap / 2`)
4. Repeat until gap = 1

---

### 🧑‍💻 JavaScript Code

```javascript
function shellSort(arr) {
  const n = arr.length;

  // Start with a big gap, then reduce it
  for (let gap = Math.floor(n / 2); gap > 0; gap = Math.floor(gap / 2)) {
    // Do insertion sort for this gap size
    for (let i = gap; i < n; i++) {
      const temp = arr[i];
      let j = i;

      // Shift earlier gap-sorted elements up until correct location found
      while (j >= gap && arr[j - gap] > temp) {
        arr[j] = arr[j - gap];
        j -= gap;
      }

      arr[j] = temp;
    }
  }

  return arr;
}
```

---

# 🐚 Dry Run

### 🔢 Input Array:

```text
[12, 34, 54, 2, 3]
```

---

## ✅ Step 1: Initialize Gap = floor(n / 2) = 5 / 2 = 2

We'll compare and sort elements that are **2 positions apart** (gap = 2):

### First Pass (Gap = 2)

Compare and insert:

- Compare **54** and **12** → no change
- Compare **2** and **34** → 2 < 34 → Shift 34, Insert 2
  ➜ `[12, 2, 54, 34, 3]`
- Compare **3** and **54** → 3 < 54 → Shift 54, Insert 3
  ➜ `[12, 2, 3, 34, 54]`

✅ After gap = 2 →

```text
[12, 2, 3, 34, 54]
```

---

## ✅ Step 2: Reduce Gap → gap = floor(2 / 2) = 1

Now we do **regular insertion sort**:

### Second Pass (Gap = 1)

Compare adjacent elements:

- Compare **2** and **12** → 2 < 12 → Shift 12, insert 2
  ➜ `[2, 12, 3, 34, 54]`
- Compare **3** and **12** → 3 < 12 → Shift 12, insert 3
  ➜ `[2, 3, 12, 34, 54]`
- Compare **34** and **12** → no change
- Compare **54** and **34** → no change

✅ Final sorted array:

```text
[2, 3, 12, 34, 54]
```

---

## 🧠 Visual Summary

| Gap | Comparison Step           | Array State         |
| --- | ------------------------- | ------------------- |
| 2   | Compare 2 ↔ 34 → Insert 2 | \[12, 2, 54, 34, 3] |
| 2   | Compare 3 ↔ 54 → Insert 3 | \[12, 2, 3, 34, 54] |
| 1   | Compare 2 ↔ 12 → Insert 2 | \[2, 12, 3, 34, 54] |
| 1   | Compare 3 ↔ 12 → Insert 3 | \[2, 3, 12, 34, 54] |

---

### ✅ Final Output:

```js
[2, 3, 12, 34, 54];
```

## ⏱️ **Time & Space Complexity**

| Case    | Time Complexity                       |
| ------- | ------------------------------------- |
| Best    | O(n log n) _(with good gap sequence)_ |
| Average | O(n^1.25) to O(n^1.5)                 |
| Worst   | O(n²)                                 |
| Space   | O(1) (in-place)                       |

---

## ✅ Pros:

- **Faster than Insertion Sort** for large arrays
- **In-place** (no extra memory)
- Simple to implement

## ❌ Cons:

- **Not stable**
- Performance depends on **gap sequence** chosen

---

## 📌 Best Use Case:

- When you need better performance than insertion sort
- When you want **in-place sorting** without recursion or extra memory

---

# ⛏️ Heap Sort

## 📘 What is Heap Sort?

**Heap Sort** is a **comparison-based** sorting algorithm that uses a special binary tree structure called a **heap**.

It works in two main steps:

1. **Build a Max Heap**
2. **Extract the maximum element** (root), place it at the end, and **heapify** the rest.

---

## 💡 What is a Heap?

- A **heap** is a **complete binary tree**.
- A **Max Heap** means: every parent is **greater than or equal to** its children.
- The **largest element** is always at the **root** (index `0` in an array).

---

## 🔄 Dry Run Example

### 🔢 Input:

```js
[4, 10, 3, 5, 1];
```

### Step 1: Build Max Heap

Max heap representation:

```text
         10
        /  \
       5    3
      / \
     4   1
```

Array: `[10, 5, 3, 4, 1]`

---

### Step 2: Extract max one by one

#### 1️⃣ Swap root with last:

```
[1, 5, 3, 4, 10] → heapify → [5, 4, 3, 1, 10]
```

#### 2️⃣ Swap root with 4th element:

```
[1, 4, 3, 5, 10] → heapify → [4, 1, 3, 5, 10]
```

#### 3️⃣ Swap root with 3rd:

```
[3, 1, 4, 5, 10] → heapify → [3, 1, 4, 5, 10]
```

#### 4️⃣ Swap root with 2nd:

```
[1, 3, 4, 5, 10] → sorted!
```

✅ Final Output:

```js
[1, 3, 4, 5, 10];
```

---

## 🧑‍💻 JavaScript Code:

```javascript
function heapify(arr, n, i) {
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
    heapify(arr, n, largest);
  }
}

function heapSort(arr) {
  let n = arr.length;

  // Step 1: Build Max Heap
  for (let i = Math.floor(n / 2) - 1; i >= 0; i--) {
    heapify(arr, n, i);
  }

  // Step 2: Extract elements from heap one by one
  for (let i = n - 1; i > 0; i--) {
    [arr[0], arr[i]] = [arr[i], arr[0]]; // Swap max to end
    heapify(arr, i, 0); // Re-heapify reduced heap
  }

  return arr;
}

// Example
console.log(heapSort([4, 10, 3, 5, 1]));
// Output: [1, 3, 4, 5, 10]
```

Absolutely! Let’s break down the `heapify` function clearly, step-by-step. This is **the heart of Heap Sort**, so understanding it is key. 🧠

---

## 🔍 `heapify()` Function in Heap Sort

`heapify(arr, n, i)` ensures that the **subtree rooted at index `i`** obeys the **Max-Heap property**:

> 👉 Parent node is **greater than or equal to** its children.

If not, `heapify` will **swap** and **recursively fix** the heap.

---

## 📐 Parameters:

```javascript
function heapify(arr, n, i)
```

| Parameter | Meaning                                   |
| --------- | ----------------------------------------- |
| `arr`     | The array representing the heap           |
| `n`       | Size of the heap/subarray to heapify      |
| `i`       | Index of the current root node to heapify |

---

## 👣 Step-by-Step Breakdown:

```javascript
let largest = i; // Assume current node is the largest
let left = 2 * i + 1; // Index of left child
let right = 2 * i + 2; // Index of right child
```

### ✔️ Step 1: Compare with Left Child

```javascript
if (left < n && arr[left] > arr[largest]) {
  largest = left;
}
```

- If the **left child exists** and is **greater than current largest**, update `largest`.

### ✔️ Step 2: Compare with Right Child

```javascript
if (right < n && arr[right] > arr[largest]) {
  largest = right;
}
```

- If the **right child exists** and is **greater**, update `largest` again.

### ✔️ Step 3: If `largest` is not the current root (`i`), swap:

```javascript
if (largest !== i) {
  [arr[i], arr[largest]] = [arr[largest], arr[i]]; // Swap

  heapify(arr, n, largest); // Recursively heapify the affected subtree
}
```

---

## 📊 Example Walkthrough

### Given Array:

```js
arr = [4, 10, 3, 5, 1];
(n = 5), (i = 0);
```

```
          4
        /   \
      10     3
     /  \
    5    1
```

### Step-by-step for `heapify(arr, 5, 0)`:

- `i = 0`, `left = 1 (10)`, `right = 2 (3)`
- Compare:

  - `arr[1] (10) > arr[0] (4)` → largest = 1

- Swap `arr[0]` and `arr[1]` → `[10, 4, 3, 5, 1]`
- Now call `heapify(arr, 5, 1)` to fix subtree at index 1

**Subtree at index 1:**

```
         4
        / \
       5   1
```

- `i = 1`, `left = 3 (5)`, `right = 4 (1)`
- `arr[3] (5) > arr[1] (4)` → swap
- Resulting array: `[10, 5, 3, 4, 1]` ✅

---

## ✅ Summary of `heapify()`:

- Maintains **max-heap property**
- Compares node with its **children**
- **Swaps** with the larger child if needed
- **Recursively** fixes the affected subtree

---

## 💡 Tip:

To build a max heap, we call:

```js
for (let i = Math.floor(n / 2) - 1; i >= 0; i--) {
  heapify(arr, n, i);
}
```

We start from the **last non-leaf node** and heapify upwards.

---

## ⏱️ Time & Space Complexity

| Operation  | Complexity      |
| ---------- | --------------- |
| Build Heap | O(n)            |
| Heapify    | O(log n)        |
| Total Time | O(n log n)      |
| Space      | O(1) (in-place) |

---

## ✅ Pros:

- **Efficient** and **in-place**
- **No extra memory** needed
- Good for priority queues (max-heap/min-heap)

## ❌ Cons:

- **Not stable**
- A bit complex to implement than simple sorts

---

## 🧠 Use Case

- When you need **O(n log n)** performance with **no extra space**
- In **priority queues**, **schedulers**, **graph algorithms**

---
