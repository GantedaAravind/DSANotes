# 📚 Sliding Window Technique

## 🧠 What is Sliding Window?

The **Sliding Window** technique is used to **reduce the time complexity** of problems involving **contiguous sequences** (subarrays/substrings). It avoids unnecessary recalculations by maintaining a running computation as the window "slides" across the data structure.

---

## ⚙️ Types of Sliding Window

1. **Fixed-Size Sliding Window**

   - Window size is constant (`k`)
   - Useful for problems like maximum sum of subarray of size `k`

2. **Variable-Size Sliding Window (Dynamic Window)**

   - Window size grows/shrinks based on a condition (e.g., sum ≤ k, unique characters, etc.)

---

## 🔍 **4 Core Patterns**

### 🔹 **Pattern 1: Constant Window Size**

#### 🔸 Problem Type:

- Maximum sum of subarray of size `k`
- Average of subarrays
- Count of fixed-size windows

#### ✅ Idea:

Keep a window of size `k` and:

- Slide it one element at a time
- Add incoming element
- Remove outgoing element

#### 🧪 Example Problem:

**Find the maximum sum of any subarray of size `k`**

#### 💡 Code Template (JavaScript):

```js
function maxSumSubarray(arr, k) {
  let maxSum = 0,
    windowSum = 0;
  for (let end = 0; end < arr.length; end++) {
    windowSum += arr[end];
    if (end >= k - 1) {
      maxSum = Math.max(maxSum, windowSum);
      windowSum -= arr[end - k + 1]; // remove the element going out
    }
  }
  return maxSum;
}
```

#### ⏱ Time Complexity:

**O(N)** — each element is added and removed once

---

### 🔹 **Pattern 2: Longest Subarray/Substring With a Condition**

#### 🔸 Problem Type:

- Longest substring without repeating characters
- Longest subarray with sum ≤ `k`
- Longest substring with at most `k` distinct characters

#### ✅ Idea:

1. Expand the window by moving `R`
2. If the window becomes invalid, **shrink** it from the left using `L`
3. Track the **maximum window length** when the condition is satisfied

---

#### 🧪 Example Problem:

**Find the length of longest subarray with sum ≤ K**

#### 💡 Code Template (JS):

```js
function longestSubarrayWithSumK(arr, k) {
  let start = 0,
    end = 0;
  let sum = 0,
    maxLength = 0;

  while (end < arr.length) {
    sum += arr[end];

    while (sum > k) {
      sum -= arr[start];
      start++;
    }

    maxLength = Math.max(maxLength, end - start + 1);
    end++;
  }

  return maxLength;
}
```

#### 🔍 Optimized Tip:

If the question asks **only the length**, the `while` loop can often be replaced with an `if` for better performance.

#### ⏱ Time Complexity:

- General: **O(2N)** (expand + shrink)
- Optimized: **O(N)**

---

### 🔹 **Pattern 3: Count Number of Subarrays with a Condition**

#### 🔸 Problem Type:

- Count subarrays with sum exactly equal to `K`

#### ✅ Idea:

Use the insight:

```
count(subarrays with sum ≤ K) - count(subarrays with sum ≤ K-1) = count(sum == K)
```

You can reuse the logic from Pattern 2 to count subarrays with sum ≤ K and sum ≤ K-1.

#### 💡 Code Snippet:

```js
function countSubarraysWithSumAtMostK(arr, k) {
  let start = 0,
    sum = 0,
    count = 0;

  for (let end = 0; end < arr.length; end++) {
    sum += arr[end];

    while (sum > k) {
      sum -= arr[start];
      start++;
    }

    count += end - start + 1;
  }

  return count;
}

function countSubarraysWithSumK(arr, k) {
  return (
    countSubarraysWithSumAtMostK(arr, k) -
    countSubarraysWithSumAtMostK(arr, k - 1)
  );
}
```

### 🔍 **What does `end - start + 1` mean?**

At any point in the loop:

- `start` is the beginning of the current valid window.
- `end` is the current index we're processing.

The expression `end - start + 1` gives us the **number of subarrays that end at index `end`** and **start anywhere from `start` to `end`**.

---

### 📦 Example:

Let’s say:

```js
(arr = [1, 2, 3]), (k = 5);
```

You reach `end = 2` (element = 3), and suppose `start = 1`, and the sum in that window is ≤ 5.

So, the **subarrays ending at index 2 and starting from index 1 to 2 are**:

- `[2, 3]`
- `[3]`

So, total = `2` subarrays → `end - start + 1 = 2 - 1 + 1 = 2`

✔ These are all subarrays that are **valid**, because the sum from `start` to `end` is within the required constraint (sum ≤ k).

---

### 🧠 Why do we add this to `count`?

Because for every `end`, we are collecting:

- All subarrays ending at `end` that satisfy the condition.

So this line is **accumulating the total number of valid subarrays** as we iterate through the array.

---

### 🔁 Dry Run:

```js
arr = [1, 2, 1], k = 3

start = 0
end = 0: sum = 1 → count += 1 (subarrays: [1])
end = 1: sum = 1 + 2 = 3 → count += 2 (subarrays: [1,2], [2])
end = 2: sum = 3 + 1 = 4 > 3 → shrink window
    → sum = 4 - arr[0] = 3, start = 1
    → count += 2 (subarrays: [2,1], [1])
```

➡ Final count = `1 + 2 + 2 = 5`

---

#### ⏱ Time Complexity: **O(N)**

---

### 🔹 **Pattern 4: Shortest/Minimum Window or Length With a Condition**

#### 🔸 Problem Type:

- Minimum size subarray with sum ≥ K
- Minimum window substring

#### ✅ Idea:

1. Expand `end` until the condition is satisfied
2. Then shrink `start` to reduce the window size as much as possible while keeping it valid

#### 🧪 Example Problem:

**Find the length of the smallest subarray with sum ≥ K**

#### 💡 Code Template:

```js
function minSubarrayLen(nums, k) {
  let start = 0,
    sum = 0,
    minLength = Infinity;

  for (let end = 0; end < nums.length; end++) {
    sum += nums[end];

    while (sum >= k) {
      minLength = Math.min(minLength, end - start + 1);
      sum -= nums[start];
      start++;
    }
  }

  return minLength === Infinity ? 0 : minLength;
}
```

#### ⏱ Time Complexity:

**O(N)**

---

## 🧠 Key Concepts Recap

| Pattern                              | Window Type   | Goal                       | Time Complexity |
| ------------------------------------ | ------------- | -------------------------- | --------------- |
| Max/Min of subarray of size K        | Fixed-size    | Find max/min/sum in window | O(N)            |
| Longest substring/subarray with cond | Variable-size | Maximize length with cond  | O(N) or O(2N)   |
| Count of valid subarrays             | Variable-size | Count valid ranges         | O(N)            |
| Smallest subarray with condition     | Variable-size | Minimize window size       | O(N)            |

---

## 📌 Template for Variable-Size Sliding Window

```js
let start = 0;
for (let end = 0; end < arr.length; end++) {
  // Expand window with arr[end]

  while (/* invalid window */) {
    // Shrink window from start
    start++;
  }

  // Process valid window: length, count, etc.
}
```

---

## ✅ Two Pointer vs Sliding Window

| Technique      | Main Use                             |
| -------------- | ------------------------------------ |
| Two Pointers   | Sorted arrays, problems like Two Sum |
| Sliding Window | Contiguous window-based problems     |

---

# **Medium Problems**

## 🔢 **1. Longest Substring Without Repeating Characters**

### 📘 Problem Statement

Given a string `s`, find the **length of the longest substring** without repeating characters.

> Return the maximum length of such a substring.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: "abcabcbb";
Output: 3;
// Explanation: "abc" is the longest substring without repeating characters.
```

#### ✅ Test Case 2:

```js
Input: "bbbbb";
Output: 1;
// Explanation: "b" is the longest substring.
```

#### ✅ Test Case 3:

```js
Input: "pwwkew";
Output: 3;
// Explanation: "wke" is the longest.
```

#### ✅ Test Case 4:

```js
Input: "";
Output: 0;
```

---

### 🧠 Intuition

We need to find the **longest substring** where **no characters repeat**.
This means:

- We need a **window** that keeps all characters **unique**.
- If a duplicate is found → **shrink** the window until the duplicate is removed.

This is a classic **sliding window** problem with a **Set** or **Map** for tracking characters.

---

### 🔄 Dry Run: Input `"abcabcbb"`

| Step | i (end) | Char | Window                      | Set     | Start | Length |
| ---- | ------- | ---- | --------------------------- | ------- | ----- | ------ |
| 0    | 0       | a    | "a"                         | {a}     | 0     | 1      |
| 1    | 1       | b    | "ab"                        | {a,b}   | 0     | 2      |
| 2    | 2       | c    | "abc"                       | {a,b,c} | 0     | 3      |
| 3    | 3       | a    | Duplicate → move start to 1 | {b,c,a} | 1     | 3      |
| 4    | 4       | b    | Duplicate → move start to 2 | {c,a,b} | 2     | 3      |

→ Max length found = `3`

---

### 💡 Optimized Approach: Sliding Window with Set

Use two pointers (`start`, `end`), and a Set to track unique characters in the current window.

---

### ✅ JavaScript Code

```js
function lengthOfLongestSubstring(s) {
  const set = new Set();
  let start = 0,
    maxLength = 0;

  for (let end = 0; end < s.length; end++) {
    while (set.has(s[end])) {
      set.delete(s[start]);
      start++;
    }
    set.add(s[end]);
    maxLength = Math.max(maxLength, end - start + 1);
  }

  return maxLength;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity                                       |
| -------- | ------------------------------------------------ |
| ⏳ Time  | O(n)                                             |
| 💾 Space | O(min(n, charset)) (Set of characters in window) |

---

### 📌 Summary

| Approach          | Time  | Space | Notes                                        |
| ----------------- | ----- | ----- | -------------------------------------------- |
| Brute Force       | O(n²) | O(n)  | Check all substrings for uniqueness          |
| ✅ Sliding Window | O(n)  | O(k)  | Optimal; k = size of character set (e.g. 26) |

---

## 🔢 **2. Max Consecutive Ones III**

### 📘 Problem Statement

You are given a binary array `nums[]` and an integer `k`.

> Return the maximum number of consecutive `1`’s in the array if you can flip at most `k` `0`’s.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (nums = [1, 1, 1, 0, 0, 0, 1, 1, 1, 1, 0]), (k = 2);
Output: 6;
// Explanation: Flip 2 zeros at positions 5 and 10 → [1,1,1,0,0,1,1,1,1,1,1]
```

#### ✅ Test Case 2:

```js
Input: (nums = [0, 0, 1, 1, 1, 0, 0]), (k = 0);
Output: 3;
// Explanation: No flips → max streak of 1s = 3
```

#### ✅ Test Case 3:

```js
Input: (nums = [1, 0, 1, 0, 1]), (k = 1);
Output: 3;
// Flip one 0 (either index 1 or 3) → streak = 3
```

---

### 🧠 Intuition

We need the longest subarray that contains at most `k` zeroes (since we can flip `k` zeroes to ones).

Use the **sliding window** approach:

- Expand the window from the right.
- If the count of zeroes in the window exceeds `k`, **shrink** from the left.
- Track the maximum window size that satisfies the condition.

---

### 🔄 Dry Run: Input `[1,1,1,0,0,0,1,1,1,1,0]`, `k = 2`

| Step | start                           | end | zeroCount | Window                     | Length   |     |
| ---- | ------------------------------- | --- | --------- | -------------------------- | -------- | --- |
| 0    | 0                               | 2   | 0         | \[1,1,1]                   | 3        |     |
| 3    | 0                               | 3   | 1         | \[1,1,1,0]                 | 4        |     |
| 4    | 0                               | 4   | 2         | \[1,1,1,0,0]               | 5        |     |
| 5    | 0                               | 5   | 3 ❌      | Shrink → start = 1 → 2 → 3 | \[0,0,0] | 3   |
| 6–10 | Move and track → max window = 6 |     |           |                            |          |     |

---

### 💡 Optimized Approach: Sliding Window (Count 0s)

---

### ✅ JavaScript Code

```js
function longestOnes(nums, k) {
  let start = 0;
  let maxLength = 0;
  let zeroCount = 0;

  for (let end = 0; end < nums.length; end++) {
    if (nums[end] === 0) zeroCount++;

    while (zeroCount > k) {
      if (nums[start] === 0) zeroCount--;
      start++;
    }

    maxLength = Math.max(maxLength, end - start + 1);
  }

  return maxLength;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity |
| -------- | ---------- |
| ⏳ Time  | O(n)       |
| 💾 Space | O(1)       |

---

### 📌 Summary

| Approach          | Time  | Space | Notes                                      |
| ----------------- | ----- | ----- | ------------------------------------------ |
| Brute Force       | O(n²) | O(1)  | Try all subarrays (inefficient)            |
| ✅ Sliding Window | O(n)  | O(1)  | Count 0’s, shrink window when `k` exceeded |

---

## 🔢 **3. Fruit Into Baskets**

(Also known as **Longest Subarray with At Most Two Distinct Elements**)

### 📘 Problem Statement

You are given an array `fruits[]`, where each element represents a type of fruit.

You have **two baskets**, and each basket can hold only **one type of fruit**, but any number of them.

> Return the **length of the longest subarray** that contains **at most two distinct types** of fruits.

This is equivalent to finding the **longest subarray with at most 2 distinct elements**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: [1, 2, 1];
Output: 3;
// Explanation: All 3 fruits can go into the baskets
```

#### ✅ Test Case 2:

```js
Input: [0, 1, 2, 2];
Output: 3;
// Explanation: Pick [1,2,2]
```

#### ✅ Test Case 3:

```js
Input: [1, 2, 3, 2, 2];
Output: 4;
// Explanation: Longest valid subarray is [2,3,2,2]
```

#### ✅ Test Case 4:

```js
Input: [3, 3, 3, 1, 2, 1, 1, 2, 3, 3, 4];
Output: 5;
// Explanation: Pick [1,2,1,1,2]
```

---

### 🧠 Intuition

This is a classic **variable-size sliding window** problem where:

- We want a window with **at most 2 different elements**.
- If we ever have **more than 2 types**, we shrink the window from the left.

We’ll use a **Map** or **Object** to count the frequency of each fruit in the current window.

---

### 🔄 Dry Run: Input `[1,2,3,2,2]`

| Step | end | Fruit | Map (type→count) | Start | Action                           | Max Len |
| ---- | --- | ----- | ---------------- | ----- | -------------------------------- | ------- |
| 0    | 0   | 1     | {1:1}            | 0     | Add 1                            | 1       |
| 1    | 1   | 2     | {1:1, 2:1}       | 0     | Add 2                            | 2       |
| 2    | 2   | 3     | {1:1,2:1,3:1}    | 0→1→2 | Shrink until 2 types → {2:1,3:1} | 2       |
| 3    | 3   | 2     | {2:2,3:1}        | 2     | Add 2                            | 2       |
| 4    | 4   | 2     | {2:3,3:1}        | 2     | Add 2                            | 3       |

→ Final max = 4

---

### 💡 Optimized Approach: Sliding Window + Map

---

### ✅ JavaScript Code

```js
function totalFruit(fruits) {
  let start = 0;
  let maxLen = 0;
  const map = new Map();

  for (let end = 0; end < fruits.length; end++) {
    const fruit = fruits[end];
    map.set(fruit, (map.get(fruit) || 0) + 1);

    while (map.size > 2) {
      const leftFruit = fruits[start];
      map.set(leftFruit, map.get(leftFruit) - 1);
      if (map.get(leftFruit) === 0) map.delete(leftFruit);
      start++;
    }

    maxLen = Math.max(maxLen, end - start + 1);
  }

  return maxLen;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity                   |
| -------- | ---------------------------- |
| ⏳ Time  | O(n)                         |
| 💾 Space | O(1) or O(k) (k = max types) |

---

### 📌 Summary

| Approach          | Time  | Space | Notes                                      |
| ----------------- | ----- | ----- | ------------------------------------------ |
| Brute Force       | O(n²) | O(1)  | Check all subarrays                        |
| ✅ Sliding Window | O(n)  | O(k)  | k = number of fruit types (at most 2 here) |

---

## 🔢 **4. Longest Repeating Character Replacement**

### 📘 Problem Statement

You are given a string `s` and an integer `k`.
You can choose **at most `k` characters** in the string and replace them with **any uppercase letter**.

> Return the **length of the longest substring** containing the same letter after performing **at most `k` replacements**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (s = "ABAB"), (k = 2);
Output: 4;
// Explanation: Replace two 'B's with 'A' to get "AAAA"
```

#### ✅ Test Case 2:

```js
Input: (s = "AABABBA"), (k = 1);
Output: 4;
// Explanation: Replace one 'B' to get "AABAAA" or "AAABBA"
```

#### ✅ Test Case 3:

```js
Input: (s = "ABCDE"), (k = 1);
Output: 2;
// Replace any one letter → longest same-letter substring = 2
```

---

### 🧠 Intuition

We want the **longest window** where, by changing **at most `k` characters**, all characters become the **same**.

Key Insight:

- Count the **frequency of the most frequent character** in the current window.
- If the remaining characters (`window size - maxFreq`) > `k`, shrink the window.

---

### 🔄 Dry Run: Input `"AABABBA"`, `k = 1`

| Step | end | Char | Count Map  | MaxFreq | Window Size | Action                 | Start   | MaxLen |
| ---- | --- | ---- | ---------- | ------- | ----------- | ---------------------- | ------- | ------ |
| 0    | 0   | A    | {A:1}      | 1       | 1           | Valid                  | 0       | 1      |
| 1    | 1   | A    | {A:2}      | 2       | 2           | Valid                  | 0       | 2      |
| 2    | 2   | B    | {A:2, B:1} | 2       | 3           | Valid (3-2 ≤ 1)        | 0       | 3      |
| 3    | 3   | A    | {A:3, B:1} | 3       | 4           | Valid (4-3 ≤ 1)        | 0       | 4      |
| 4    | 4   | B    | {A:3, B:2} | 3       | 5           | Invalid (5-3 > 1) ❌   | start++ | 1 → 1  |
| 5    | 5   | B    | {A:2, B:3} | 3       | 5           | Invalid (5-3 > 1) ❌   | start++ | 2 → 2  |
| 6    | 6   | A    | {A:2, B:3} | 3       | 5           | Valid (5-3 = 2 > k) ❌ | start++ | 3 → 3  |

→ Final `maxLen = 4`

---

### 💡 Optimized Approach: Sliding Window + Frequency Map

---

### ✅ JavaScript Code

```js
function characterReplacement(s, k) {
  let start = 0;
  let maxCount = 0;
  const freq = new Array(26).fill(0);
  let maxLength = 0;

  for (let end = 0; end < s.length; end++) {
    const index = s.charCodeAt(end) - 65;
    freq[index]++;
    maxCount = Math.max(maxCount, freq[index]);

    while (end - start + 1 - maxCount > k) {
      freq[s.charCodeAt(start) - 65]--;
      start++;
    }

    maxLength = Math.max(maxLength, end - start + 1);
  }

  return maxLength;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity                                      |
| -------- | ----------------------------------------------- |
| ⏳ Time  | O(n)                                            |
| 💾 Space | O(1) (26 letters in uppercase English alphabet) |

---

### 📌 Summary

| Approach          | Time  | Space | Notes                                  |
| ----------------- | ----- | ----- | -------------------------------------- |
| Brute Force       | O(n²) | O(1)  | Try all substrings                     |
| ✅ Sliding Window | O(n)  | O(1)  | Optimal; track max character frequency |

---

## 🔢 **5. Binary Subarrays With Sum**

### 📘 Problem Statement

You are given a binary array `nums[]` (i.e., contains only 0s and 1s), and an integer `goal`.

> Return the **number of subarrays** whose **sum is exactly equal to `goal`**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (nums = [1, 0, 1, 0, 1]), (goal = 2);
Output: 4;
// Explanation: The 4 subarrays are:
// [1,0,1], [0,1,0,1], [1,0,1], [1,0,1]
```

#### ✅ Test Case 2:

```js
Input: (nums = [0, 0, 0, 0, 0]), (goal = 0);
Output: 15;
// Explanation: All possible subarrays with only 0s and sum = 0
```

#### ✅ Test Case 3:

```js
Input: (nums = [1, 1, 1, 1, 1]), (goal = 3);
Output: 3;
```

---

### 💡 **Approch 1 :Sliding Window (Only Works When All Elements Are Non-negative)**

The sliding window approach can be used when all array elements are **non-negative** — which is true for binary arrays.

But remember:

> ❗ The sliding window helps only for **“at most K”** problems.
> To solve for **exactly `goal`**, we use the trick:

```
count(sum == goal) = count(sum ≤ goal) - count(sum ≤ goal - 1)
```

---

#### 🧠 Intuition

We’ll define a helper function:

```js
countAtMost(k): returns number of subarrays with sum ≤ k
```

Then,

```js
numSubarraysWithSum(goal) = countAtMost(goal) - countAtMost(goal - 1)
```

---

#### 🔁 Dry Run of countAtMost(2) — Input: \[1,0,1,0,1]

- `start = 0`, `end` moves forward
- Add elements to `sum`
- If `sum > k`, shrink window by moving `start` forward
- Count += `end - start + 1` (subarrays ending at `end`)

---

#### ✅ JavaScript Code (Sliding Window)

```js
function numSubarraysWithSum(nums, goal) {
  return countAtMost(nums, goal) - countAtMost(nums, goal - 1);
}

function countAtMost(nums, k) {
  if (k < 0) return 0;

  let start = 0,
    sum = 0,
    count = 0;

  for (let end = 0; end < nums.length; end++) {
    sum += nums[end];

    while (sum > k) {
      sum -= nums[start++];
    }

    count += end - start + 1;
  }

  return count;
}
```

---

#### ⏱ Time & Space Complexity

| Metric   | Complexity |
| -------- | ---------- |
| ⏳ Time  | O(n)       |
| 💾 Space | O(1)       |

---

### Approch 2 : Prefix Sum

#### 🧠 Intuition

We want the **count of subarrays with sum exactly equal to `goal`**.

Instead of a direct sliding window (which works only when elements are all non-negative and `sum ≤ k`), this problem benefits from the **Prefix Sum + Hash Map** pattern.

> 🔑 Key Idea:
> Let’s count how many times a **prefix sum** has occurred so far.
> For each index `i` with prefix sum `currSum`, check if `currSum - goal` has been seen before.

---

#### 🧮 Prefix Sum Formula:

Let `prefixSum[i] = sum of nums[0..i]`
If `prefixSum[j] - prefixSum[i] == goal`, then `nums[i+1..j]` is a valid subarray.

So, track frequency of each prefix sum using a Map.

---

#### 🔄 Dry Run: Input `[1,0,1,0,1]`, `goal = 2`

| i   | num | prefixSum | prefixMap            | count               |
| --- | --- | --------- | -------------------- | ------------------- |
| 0   | 1   | 1         | {0:1, 1:1}           | 0                   |
| 1   | 0   | 1         | {0:1, 1:2}           | 0                   |
| 2   | 1   | 2         | {0:1, 1:2, 2:1}      | +2 (1 seen 2 times) |
| 3   | 0   | 2         | {0:1, 1:2, 2:2}      | +2                  |
| 4   | 1   | 3         | {0:1, 1:2, 2:2, 3:1} | +2                  |

✅ Final answer: `2 + 2 = 4`

---

#### 💡 Optimized Approach: Prefix Sum + Hash Map

---

#### ✅ JavaScript Code

```js
function numSubarraysWithSum(nums, goal) {
  const prefixMap = new Map();
  prefixMap.set(0, 1); // base case

  let sum = 0,
    count = 0;

  for (const num of nums) {
    sum += num;

    if (prefixMap.has(sum - goal)) {
      count += prefixMap.get(sum - goal);
    }

    prefixMap.set(sum, (prefixMap.get(sum) || 0) + 1);
  }

  return count;
}
```

---

#### ⏱ Time & Space Complexity

| Metric   | Complexity |
| -------- | ---------- |
| ⏳ Time  | O(n)       |
| 💾 Space | O(n)       |

---

### 📌 Summary

| Approach                   | Time    | Space | Notes                                                    |
| -------------------------- | ------- | ----- | -------------------------------------------------------- |
| Brute Force                | O(n²)   | O(1)  | Check all subarrays                                      |
| Prefix Sum + Hash Map      | ✅ O(n) | O(n)  | Best for sum = goal                                      |
| ✅ Sliding Window (2 pass) | O(n)    | O(1)  | Use only when all elements ≥ 0 (works for binary arrays) |

---

## 🔢 **6. Count Number of Nice Subarrays**

### 📘 Problem Statement

You are given an array of integers `nums[]` and an integer `k`.

> A subarray is **nice** if it contains **exactly `k` odd numbers**.

Return the number of **nice subarrays**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (nums = [1, 1, 2, 1, 1]), (k = 3);
Output: 2;
// Explanation: Two subarrays: [1,1,2,1], [1,2,1,1]
```

#### ✅ Test Case 2:

```js
Input: (nums = [2, 4, 6]), (k = 1);
Output: 0;
// Explanation: No subarray contains 1 odd number.
```

#### ✅ Test Case 3:

```js
Input: (nums = [2, 2, 2, 1, 2, 2, 1, 2, 2, 2]), (k = 2);
Output: 16;
```

---

### 🧠 Intuition

This is conceptually the **same problem** as:

> Count number of subarrays with exactly `k` special elements (in this case, odd numbers).

So we convert it into a **prefix sum problem** where we treat each `odd number` as `1` and `even number` as `0`.

> Then we want: **count of subarrays whose sum = `k`**

---

### 🧮 Transform

Convert the array:

```js
nums = [1, 1, 2, 1, 1] → isOdd = [1, 1, 0, 1, 1]
Now we want: count of subarrays with sum = k
```

This is **identical** to **"Binary Subarrays With Sum"**, and we can apply either:

- Prefix Sum + Hash Map ✅
- Sliding Window (for sum ≤ K) ✅

---

### ✅ Approach 1: Prefix Sum + Hash Map

---

### ✅ JavaScript Code

```js
function numberOfSubarrays(nums, k) {
  const map = new Map();
  map.set(0, 1); // base case

  let count = 0,
    oddCount = 0;

  for (const num of nums) {
    oddCount += num % 2;

    if (map.has(oddCount - k)) {
      count += map.get(oddCount - k);
    }

    map.set(oddCount, (map.get(oddCount) || 0) + 1);
  }

  return count;
}
```

---

### ⏱ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(n)       |

---

### ✅ Approach 2: Sliding Window Trick (count of subarrays with exactly `k` = atMost(k) - atMost(k-1))

---

### ✅ JavaScript Code

```js
function numberOfSubarrays(nums, k) {
  return atMost(nums, k) - atMost(nums, k - 1);
}

function atMost(nums, k) {
  let start = 0,
    count = 0,
    oddCount = 0;

  for (let end = 0; end < nums.length; end++) {
    if (nums[end] % 2 !== 0) oddCount++;

    while (oddCount > k) {
      if (nums[start] % 2 !== 0) oddCount--;
      start++;
    }

    count += end - start + 1;
  }

  return count;
}
```

---

### ⏱ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(1)       |

---

### 📌 Summary

| Approach                     | Time  | Space | Notes                                          |
| ---------------------------- | ----- | ----- | ---------------------------------------------- |
| Brute Force                  | O(n²) | O(1)  | Inefficient for large arrays                   |
| ✅ Prefix Sum + Hash Map     | O(n)  | O(n)  | Best for sum = k type problems                 |
| ✅ Sliding Window Difference | O(n)  | O(1)  | Works well here due to non-negative odd counts |

---

## 🔢 **7. Number of Substrings Containing All Three Characters**

### 📘 Problem Statement

You are given a string `s` consisting only of characters `'a'`, `'b'`, and `'c'`.

> Return the **number of substrings** that contain **at least one occurrence of each** of the three characters `'a'`, `'b'`, and `'c'`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: "abc";
Output: 1;
// Explanation: Only one substring "abc" has all three.
```

#### ✅ Test Case 2:

```js
Input: "aaacb";
Output: 3;
// Explanation: Substrings with all 3 chars: ["aaacb", "aacb", "acb"]
```

#### ✅ Test Case 3:

```js
Input: "abcabc";
Output: 10;
```

---

### 🧠 Intuition

We want to count **all substrings** that contain **at least one 'a', one 'b', and one 'c'**.

➡️ We'll use the **sliding window** approach:

- Use a hashmap or array to count characters inside a window `[start...end]`.
- For each `end`, expand window and maintain counts.
- When the window contains **all three characters**, all substrings starting from current `start` to end of string will be valid.

So, **count += (s.length - end)**

---

### 🔄 Dry Run: Input = `"aaacb"`

| Step | start | end | Window            | Valid?                    | Count |
| ---- | ----- | --- | ----------------- | ------------------------- | ----- |
| 0    | 0     | 2   | {'a':3}           | ❌                        | 0     |
| 1    | 0     | 3   | {'a':3, c:1}      | ❌                        | 0     |
| 2    | 0     | 4   | {'a':3, c:1, b:1} | ✅ → Add (5-4)=1, (5-4)=1 | +1    |
| 3    | 1     | 4   | {'a':2, c:1, b:1} | ✅ → +1                   | +2    |
| 4    | 2     | 4   | {'a':1, c:1, b:1} | ✅ → +1                   | +3    |
|      | 3     | 4   | {'a':0, c:1, b:1} | ❌                        | —     |

✅ Final answer: 3

---

### 💡 Optimized Sliding Window Approach

---

### ✅ JavaScript Code

```js
function numberOfSubstrings(s) {
  let count = [0, 0, 0]; // count of a, b, c
  let res = 0,
    start = 0;

  for (let end = 0; end < s.length; end++) {
    count[s.charCodeAt(end) - 97]++;

    // shrink window until all 3 are present
    while (count[0] > 0 && count[1] > 0 && count[2] > 0) {
      res += s.length - end; // all substrings from [start...end], [start...end+1]...
      count[s.charCodeAt(start) - 97]--;
      start++;
    }
  }

  return res;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity |                      |
| -------- | ---------- | -------------------- |
| ⏳ Time  | O(n)       |                      |
| 💾 Space | O(1)       | Only 3 chars tracked |

---

### 📌 Summary

| Approach          | Time  | Space | Notes                                              |
| ----------------- | ----- | ----- | -------------------------------------------------- |
| Brute Force       | O(n³) | O(1)  | Generate all substrings → check each one           |
| ✅ Sliding Window | O(n)  | O(1)  | Optimal; shrink window when condition is satisfied |

---

## 🔢 **8. Maximum Points You Can Obtain from Cards**

### 📘 Problem Statement

You are given an integer array `cardPoints[]` and an integer `k`.

> You can pick exactly **`k` cards** from either the **beginning or the end** of the array.

Return the **maximum score** you can get by picking `k` cards.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (cardPoints = [1, 2, 3, 4, 5, 6, 1]), (k = 3);
Output: 12;
// Pick first 2 and last 1: 1 + 2 + 1 = 4 (bad)
// Best: Pick last 3 → 6 + 1 + 5 = 12
```

#### ✅ Test Case 2:

```js
Input: (cardPoints = [2, 2, 2]), (k = 2);
Output: 4;
```

#### ✅ Test Case 3:

```js
Input: (cardPoints = [9, 7, 7, 9, 7, 7, 9]), (k = 7);
Output: 55;
// Pick all cards
```

---

### 🧠 Intuition

You’re allowed to pick `k` cards, but **only from the two ends**.

If we imagine choosing some `i` cards from the left and `k - i` from the right, we can try all such combinations.

Instead of brute-forcing all such picks, we can **convert the problem**:

> Total cards = `n`, we need to remove `n - k` **consecutive** cards (one subarray) such that the **sum of the remaining** is **maximum**.

So, find the **minimum sum of a subarray of size `n - k`**, then subtract that from the total sum.

---

### 🔄 Dry Run: `[1,2,3,4,5,6,1]`, `k = 3`, `n = 7`

→ Need to remove `n - k = 4` cards in a row

Sliding window of size 4:

- Window 0-3: \[1,2,3,4] → sum = 10
- Window 1-4: \[2,3,4,5] → sum = 14
- Window 2-5: \[3,4,5,6] → sum = 18
- Window 3-6: \[4,5,6,1] → sum = 16

Minimum sum = 10 → Max score = `sum(all) - 10 = 22 - 10 = 12`

---

### 💡 Optimized Sliding Window Approach

---

### ✅ JavaScript Code

```js
function maxScore(cardPoints, k) {
  const n = cardPoints.length;
  const windowSize = n - k;

  let total = cardPoints.reduce((a, b) => a + b, 0);

  if (k === n) return total;

  let minWindowSum = Infinity;
  let windowSum = 0;

  for (let i = 0; i < n; i++) {
    windowSum += cardPoints[i];

    if (i >= windowSize) {
      windowSum -= cardPoints[i - windowSize];
    }

    if (i >= windowSize - 1) {
      minWindowSum = Math.min(minWindowSum, windowSum);
    }
  }

  return total - minWindowSum;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity |
| -------- | ---------- |
| ⏳ Time  | O(n)       |
| 💾 Space | O(1)       |

---

# **Hard Problems**

## 🔢 **1. Longest Substring with At Most K Distinct Characters**

### 📘 Problem Statement

Given a string `s` and an integer `k`, return the **length of the longest substring** that contains **at most `k` distinct characters**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (s = "eceba"), (k = 2);
Output: 3;
// Explanation: "ece" is the longest substring with at most 2 distinct characters.
```

#### ✅ Test Case 2:

```js
Input: (s = "aa"), (k = 1);
Output: 2;
```

#### ✅ Test Case 3:

```js
Input: (s = "abcadcacacaca"), (k = 3);
Output: 11;
// Explanation: "cadcacacaca"
```

---

### 🧠 Intuition

We use a **sliding window** to find the **maximum length** of a substring with **at most `k` unique characters**.

Maintain a frequency map or counter of characters in the current window.

- If the number of unique characters exceeds `k`, **shrink** the window from the left until valid again.
- For every valid window, update the max length.

---

### 🔄 Dry Run: Input = `"eceba"`, k = 2

| Step | start | end | Char | Map             | Action                                 | MaxLen |
| ---- | ----- | --- | ---- | --------------- | -------------------------------------- | ------ |
| 0    | 0     | 0   | 'e'  | {e:1}           | valid → update max = 1                 | 1      |
| 1    | 0     | 1   | 'c'  | {e:1, c:1}      | valid → update max = 2                 | 2      |
| 2    | 0     | 2   | 'e'  | {e:2, c:1}      | valid → update max = 3                 | 3      |
| 3    | 0     | 3   | 'b'  | {e:2, c:1, b:1} | 3 > 2 → shrink from start (remove 'e') | —      |
|      | 1     |     |      | {e:1, c:1, b:1} | shrink → remove 'c' → {e:1, b:1}       | valid  |
| 4    | 2     | 4   | 'a'  | {e:1, b:1, a:1} | again 3 → shrink to remove 'e'         | —      |

✅ Longest valid substring was `"ece"` → length 3.

---

### 💡 Sliding Window + Hash Map Approach

---

### ✅ JavaScript Code

```js
function lengthOfLongestSubstringKDistinct(s, k) {
  if (k === 0) return 0;

  let start = 0,
    maxLen = 0;
  const map = new Map();

  for (let end = 0; end < s.length; end++) {
    const ch = s[end];
    map.set(ch, (map.get(ch) || 0) + 1);

    while (map.size > k) {
      const leftChar = s[start];
      map.set(leftChar, map.get(leftChar) - 1);
      if (map.get(leftChar) === 0) map.delete(leftChar);
      start++;
    }

    maxLen = Math.max(maxLen, end - start + 1);
  }

  return maxLen;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity |                                      |
| -------- | ---------- | ------------------------------------ |
| ⏳ Time  | O(n)       |                                      |
| 💾 Space | O(k)       | Only `k` distinct characters tracked |

---

### 📌 Summary

| Approach          | Time  | Space | Notes                                            |
| ----------------- | ----- | ----- | ------------------------------------------------ |
| Brute Force       | O(n²) | O(k)  | Generate all substrings and count distinct chars |
| ✅ Sliding Window | O(n)  | O(k)  | Most efficient solution for this problem         |

---

## 🔢 **2. Subarrays with Exactly K Different Integers**

### 📘 Problem Statement

You are given an integer array `nums[]` and an integer `k`.

> Return the number of **subarrays with exactly `k` distinct integers**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (nums = [1, 2, 1, 2, 3]), (k = 2);
Output: 7;

// Explanation: Valid subarrays with 2 distinct integers:
// [1,2], [2,1], [1,2], [2,3], [1,2,1], [2,1,2], [1,2,3]
```

#### ✅ Test Case 2:

```js
Input: (nums = [1, 2, 1, 3, 4]), (k = 3);
Output: 6;
```

---

### 🧠 Intuition

To count **subarrays with exactly `k` different integers**, use the technique:

> 🔁 `exactlyK(k) = atMostK(k) - atMostK(k - 1)`

Why?

- `atMostK(k)` counts subarrays with ≤ k unique elements.
- Subtract `atMostK(k - 1)` (those with ≤ k - 1) to get exactly `k`.

---

### 🔄 Dry Run: `[1,2,1,2,3]`, `k = 2`

Compute:

- `atMost(2)` → 12 subarrays
- `atMost(1)` → 5 subarrays
- ✅ `exactly(2) = 12 - 5 = 7`

---

### ✅ Approach: Sliding Window with Hash Map

---

### ✅ JavaScript Code

```js
function subarraysWithKDistinct(nums, k) {
  return atMostK(nums, k) - atMostK(nums, k - 1);
}

function atMostK(nums, k) {
  const freq = new Map();
  let left = 0,
    count = 0;

  for (let right = 0; right < nums.length; right++) {
    if (!freq.has(nums[right])) freq.set(nums[right], 0);
    if (freq.get(nums[right]) === 0) k--;
    freq.set(nums[right], freq.get(nums[right]) + 1);

    while (k < 0) {
      freq.set(nums[left], freq.get(nums[left]) - 1);
      if (freq.get(nums[left]) === 0) k++;
      left++;
    }

    count += right - left + 1;
  }

  return count;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity |                              |
| -------- | ---------- | ---------------------------- |
| ⏳ Time  | O(n)       |                              |
| 💾 Space | O(n)       | For hash map (in worst case) |

---

### 📌 Summary

| Approach                     | Time  | Space | Notes                                         |
| ---------------------------- | ----- | ----- | --------------------------------------------- |
| Brute Force                  | O(n²) | O(n)  | Try all subarrays, count distinct elements    |
| ✅ Sliding Window Difference | O(n)  | O(n)  | Most optimal for exactly-k distinct subarrays |

---

## 🔢 **3. Minimum Window Substring**

### 📘 Problem Statement

You are given two strings `s` and `t`.
Return the **minimum window substring** of `s` such that every character in `t` (including duplicates) is included in the window.

> If no such window exists, return an empty string `""`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (s = "ADOBECODEBANC"), (t = "ABC");
Output: "BANC";
```

#### ✅ Test Case 2:

```js
Input: (s = "a"), (t = "a");
Output: "a";
```

#### ✅ Test Case 3:

```js
Input: (s = "a"), (t = "aa");
Output: "";
// Explanation: Not enough 'a's in s
```

---

### 🧠 Intuition

We use a **sliding window** to expand the window (`right` pointer) and shrink it (`left` pointer) to find the **minimum window** that contains all characters from `t`.

Use two hash maps:

- `need`: stores the required frequency of each character in `t`
- `window`: tracks characters in the current window

> When the window satisfies the condition (contains all `t` chars in required amounts), try to **shrink it** to get the minimum.

---

### 🔄 Dry Run: Input `s = "ADOBECODEBANC"`, `t = "ABC"`

- Start expanding window:
  A → D → O → B → E → C ✅ valid window = `"ADOBEC"`
- Try shrinking → `"DOBEC"` → `"OBEC"` → not valid
- Expand more until `"BANC"` → valid
- It's smaller → ✅ answer = `"BANC"`

---

### 💡 Sliding Window with HashMap and Count

---

### ✅ JavaScript Code

```js
function minWindow(s, t) {
  if (!s || !t || s.length < t.length) return "";

  const need = new Map();
  for (const ch of t) {
    need.set(ch, (need.get(ch) || 0) + 1);
  }

  let left = 0,
    right = 0;
  let required = need.size;
  let formed = 0;
  const window = new Map();

  let ans = [Infinity, 0, 0]; // [len, left, right]

  while (right < s.length) {
    const ch = s[right];
    window.set(ch, (window.get(ch) || 0) + 1);

    if (need.has(ch) && window.get(ch) === need.get(ch)) {
      formed++;
    }

    while (left <= right && formed === required) {
      if (right - left + 1 < ans[0]) {
        ans = [right - left + 1, left, right];
      }

      const leftChar = s[left];
      window.set(leftChar, window.get(leftChar) - 1);
      if (need.has(leftChar) && window.get(leftChar) < need.get(leftChar)) {
        formed--;
      }
      left++;
    }

    right++;
  }

  return ans[0] === Infinity ? "" : s.slice(ans[1], ans[2] + 1);
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity |                                      |
| -------- | ---------- | ------------------------------------ |
| ⏳ Time  | O(n + m)   | n = length of `s`, m = length of `t` |
| 💾 Space | O(n + m)   | For maps                             |

---

### 📌 Summary

| Approach          | Time      | Space  | Notes                                           |
| ----------------- | --------- | ------ | ----------------------------------------------- |
| Brute Force       | O(n³)     | O(1)   | Generate all substrings and check frequency     |
| ✅ Sliding Window | ✅ O(n+m) | O(n+m) | Optimal and elegant solution using two pointers |

---

## 🔢 **4. Minimum Window Subsequence**

### 📘 Problem Statement

You are given two strings `s1` and `s2`.

> Find the **minimum window in `s1`** which will contain `s2` **as a subsequence**.
> If there is no such window in `s1`, return `""`.
> If there are multiple answers, return the one with the **left-most starting index**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (s1 = "abcdebdde"), (s2 = "bde");
Output: "bcde";
// "bcde" is the smallest window in s1 where b, d, e appear in order.
```

#### ✅ Test Case 2:

```js
Input: (s1 = "jmeqksfrsdcmsiwvaovztaqenprpvnbstl"), (s2 = "k");
Output: "k";
// Single character match.
```

#### ✅ Test Case 3:

```js
Input: (s1 = "fgrqsqsnodwmxzkzxwqegkndaa"), (s2 = "fnok");
Output: "fgrqsqsnodwmxzk";
```

---

### 🧠 Intuition

This is **not** a standard sliding window problem because we want `s2` to appear as a **subsequence**, not a **substring**.

We’ll **scan `s1` to match `s2`** (forward), and once matched, we’ll **scan backward** to shrink the window as much as possible.

---

### 🔄 Dry Run:

`s1 = "abcdebdde"`, `s2 = "bde"`

- Start from `i = 0`:

  - Forward scan: match `b → d → e` at `i = 1, 3, 4`
  - Now backtrack: minimize the window by moving left
  - Shrunk window = `"bcde"` → update answer

Repeat until the end of `s1`.

---

### 💡 Forward + Backward Two-Pointer Approach

---

### ✅ JavaScript Code

```js
function minWindowSubsequence(s1, s2) {
  let minLen = Infinity,
    startIndex = -1;

  for (let i = 0; i < s1.length; i++) {
    if (s1[i] !== s2[0]) continue;

    let j = i,
      k = 0;

    // Forward scan to match s2 in s1
    while (j < s1.length && k < s2.length) {
      if (s1[j] === s2[k]) {
        k++;
      }
      j++;
    }

    // If full s2 matched
    if (k === s2.length) {
      // Now backtrack to minimize window
      let end = j - 1;
      k = s2.length - 1;
      while (k >= 0) {
        if (s1[j - 1] === s2[k]) k--;
        j--;
      }

      j++; // window starts at j now

      if (end - j + 1 < minLen) {
        minLen = end - j + 1;
        startIndex = j;
      }
    }
  }

  return minLen === Infinity
    ? ""
    : s1.substring(startIndex, startIndex + minLen);
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity |                                    |
| -------- | ---------- | ---------------------------------- |
| ⏳ Time  | O(n \* m)  | n = length of s1, m = length of s2 |
| 💾 Space | O(1)       | Constant extra space               |

---

### 📌 Summary

| Approach                 | Time         | Space | Notes                                            |
| ------------------------ | ------------ | ----- | ------------------------------------------------ |
| Brute Force              | O(n² \* m)   | O(1)  | Check all substrings for subsequence             |
| ✅ Two-Pointer (Optimal) | ✅ O(n \* m) | O(1)  | Forward scan to match, backward scan to minimize |

---

Here you go! Below is the explanation of the **“Count Subsequences with min + max ≤ target”** problem in the exact format you used:

---

## ✅ 5. **Count Subsequences with Sum of Min and Max ≤ Target**

Given an array of `n` integers `nums` and an integer `target`, return the **number of non-empty subsequences** such that the **sum of the minimum and maximum element** in the subsequence is **less than or equal to `target`**.
Return the result **modulo `10⁹ + 7`**.

---

### 🧪 Test Cases

#### Test Case 1:

```javascript
Input: (nums = [3, 5, 6, 7]), (target = 9);
Output: 4;
```

#### Test Case 2:

```javascript
Input: (nums = [3, 3, 6, 8]), (target = 10);
Output: 6;
```

#### Test Case 3:

```javascript
Input: (nums = [2, 3, 3, 4, 6, 7]), (target = 12);
Output: 61;
```

---

### 💡 Intuition

We need to find **subsequences** where the **sum of the smallest and largest element** is at most `target`.

- A brute-force approach to generate all subsequences takes `O(2^n)` time — not feasible.
- Instead:

  - **Sort** the array to make it easier to pick `min` and `max`.
  - Use a **two-pointer** technique:

    - Fix one pointer `left` at the beginning (minimum).
    - Move `right` to find the farthest index where `nums[left] + nums[right] <= target`.
    - All subsequences from `left` to `right` can be counted as `2^(right - left)`.

---

### 🔄 Dry Run

Input:

```javascript
(nums = [3, 5, 6, 7]), (target = 9);
```

Sorted: `[3, 5, 6, 7]`

1. left = 0, right = 2 → 3 + 6 = 9 ✅
   → Subsequences = 2^(2 - 0) = 4
   → Add 4 to answer, move left

2. left = 1, right = 2 → 5 + 6 = 11 ❌ → move right to 1
   5 + 5 = 10 ❌ → move right to 0 → left > right → stop

✅ Final answer: `4`

---

### 🧑‍💻 Code (JavaScript)

```javascript
function numSubseq(nums, target) {
  const MOD = 1e9 + 7;
  nums.sort((a, b) => a - b);

  const pow2 = Array(nums.length).fill(1);
  for (let i = 1; i < nums.length; i++) {
    pow2[i] = (pow2[i - 1] * 2) % MOD;
  }

  let left = 0,
    right = nums.length - 1;
  let count = 0;

  while (left <= right) {
    if (nums[left] + nums[right] <= target) {
      count = (count + pow2[right - left]) % MOD;
      left++;
    } else {
      right--;
    }
  }

  return count;
}

// Test
console.log(numSubseq([3, 5, 6, 7], 9)); // Output: 4
console.log(numSubseq([3, 3, 6, 8], 10)); // Output: 6
console.log(numSubseq([2, 3, 3, 4, 6, 7], 12)); // Output: 61
```

---

### ⏱️ Time & Space Complexity

#### ⏳ Time Complexity: `O(n log n)`

- Sorting takes `O(n log n)`
- Two-pointer scan takes `O(n)`
- Precomputing powers of 2 also takes `O(n)`

#### 🗂️ Space Complexity: `O(n)`

- For storing powers of 2 in `pow2` array

---

Let me know if you'd like this in Python or C++ as well!
