## 🔁 **Kth Character After Infinite Operations**

### 📘 **Problem Statement**

Alice and Bob are playing a game. Initially, Alice has a string:

```
word = "a"
```

In each round, Bob asks Alice to:

- Create a **new string** by changing every character in the current `word` to its **next alphabet character**.

  - `'z'` wraps around to `'a'`

- **Append** the new string to the end of `word`.

This process repeats infinitely.

You are given an integer `k`, and your task is to **return the kth character (1-indexed)** in the resulting string.

---

### 🧪 **Test Cases**

**Test Case 1:**

```javascript
Input: k = 5;
Output: "b";

// word builds like this:
// "a"
// "a" + next("a") → "a" + "b" → "ab"
// "ab" + next("ab") → "ab" + "bc" → "abbc"
// "abbc" + next("abbc") → "abbc" + "bccd" → "abbcbccd"
// 5th char = 'b'
```

**Test Case 2:**

```javascript
Input: k = 10;
Output: "c";
// Resulting string after enough operations: "abbcbccdcdde"
// 10th character = 'c'
```

---

### 💡 **Intuition**

Each round:

- The new string is the transformation of the previous string using `nextChar()`.
- This keeps **doubling** the length approximately (but slightly more due to characters shifting).

We **don’t need to build the full string** of size `k`:

- Instead, simulate the process until the string becomes at least `k` characters long.
- Then return the `k-1` indexed character.

---

You're referring to a **bit-counting based solution** that cleverly avoids building the full string.

Let’s break this down and provide a **clean implementation** using that approach, in your preferred pattern.

---

### 💡 **Intuition (Optimized Insight)**

Every character in the final string can be mapped **without generating the string**.

#### 🔍 Key Observation:

The **number of 1s in the binary representation of (k - 1)** determines the number of times a character was transformed.

For example:

- At position `k = 5`, `k - 1 = 4` → binary = `100` → 1 one → `'a'` + 1 = `'b'`
- At `k = 10`, `k - 1 = 9` → binary = `1001` → 2 ones → `'a'` + 2 = `'c'`

Why?
Because every time a bit is 1 in the binary form, it indicates a **transformation step** contributing to this character’s derivation from `'a'`.

---

### ✅ **JavaScript Implementation (Bit Count Approach)**

```javascript
/**
 * @param {number} k
 * @return {character}
 */
var kthCharacter = function (k) {
  let count = 0;
  let v = k - 1;

  while (v > 0) {
    if ((v & 1) === 1) {
      count++;
    }
    v >>= 1;
  }

  // Wrap around using modulo 26 in case count exceeds 'z'
  return String.fromCharCode((97 + count) % 123); // 'a' is 97
};
```

---

### 🧪 **Examples**

**Input:** `k = 5`

- `k - 1 = 4` → binary `100` → 1 one
- Result: `'a'` + 1 = `'b'` ✅

**Input:** `k = 10`

- `k - 1 = 9` → binary `1001` → 2 ones
- Result: `'a'` + 2 = `'c'` ✅

---

### ⏱ **Time and Space Complexity**

| Operation | Complexity |
| --------- | ---------- |
| Time      | O(log k)   |
| Space     | O(1)       |

No string building, just bit manipulation!

---

### 📌 **Summary Table**

| Step                 | Purpose                              |
| -------------------- | ------------------------------------ |
| `k - 1`              | Convert to 0-indexed                 |
| Bit Count of (k - 1) | Number of transformations from `'a'` |
| ASCII + count        | Convert to resulting character       |

---

## 🧮 **K-th Character After Sequence of Copy and Transform Operations**

### 📘 **Problem Statement**

You start with:

```javascript
word = "a";
```

You're given:

- An integer `k` (1-based index).
- An array of operations (`0` or `1`):

  - `0`: Append word to itself.
  - `1`: Append `next(word)` to word (each char shifted to next in alphabet, `'z' → 'a'`).

After all operations, return the **k-th character** in the resulting string.

---

### 🧪 **Test Cases**

**Test Case 1:**

```javascript
Input: (k = 5), (operations = [0, 0, 0]);
Output: "a";
// After each op: "a" → "aa" → "aaaa" → "aaaaaaaa"
```

**Test Case 2:**

```javascript
Input: (k = 10), (operations = [0, 1, 0, 1]);
Output: "b";
// word evolves:
// "a" → "aa" → "aabb" → "aabbaabb" → "aabbaabbbbccbbcc"
// 10th char = 'b'
```

---

### 💡 **Key Insight**

We can't **build the entire string** (up to `10^14` in size). So:

- Instead of building the string, **track length** and **reverse-simulate** what happens at index `k` during each operation.
- Work **backward** from the final string:

  - If operation was a **copy**, then the string doubled. Figure out if `k` lies in the **original** or **copied** half.
  - If operation was a **transform**, only the second half was transformed. Again, trace `k` accordingly.

---

### 💡 **Optimized Bit-Trick Insight**

We don’t simulate the full word (which would be **massively large**), but instead use **bit logic** on `k - 1`:

- Treat the growth process like a **binary tree**:

  - Each operation doubles the length.
  - The final string is a **traceable path** from root (`"a"`) based on the **binary form of (k - 1)**.

- For every bit that is `1` in the binary form of `k - 1`, we **accumulate transformation operations** if the corresponding operation was a `1`.

This directly tells us how many **transformations** were applied to character `'a'`.

---

### ✅ **JavaScript Code (Your Approach)**

```javascript
/**
 * @param {number} k
 * @param {number[]} operations
 * @return {character}
 */
var kthCharacter = function (k, operations) {
  k--; // Convert to 0-based index
  let count = 0;

  // Binary representation of k
  k.toString(2)
    .split("")
    .reverse()
    .forEach(function (val, idx) {
      if (val === "1") {
        count += operations[idx]; // Only add if this segment came from a "1"
      }
    });

  // Wrap around alphabet using modulo
  return String.fromCharCode(97 + (count % 26));
};
```

---

### ⏱ **Time & Space Complexity**

| Metric | Value    |
| ------ | -------- |
| Time   | O(log k) |
| Space  | O(log k) |

---

### 📌 **Summary Table**

| Concept            | Explanation                                               |
| ------------------ | --------------------------------------------------------- |
| `k - 1`            | Convert to 0-based index (matches binary form)            |
| Binary Traversal   | Use bits to determine which halves `k` came from          |
| Operation Matching | For every `1` bit, accumulate transformation from op list |
| Character Mapping  | `'a'` + total shifts (modulo 26)                          |

---

### 🔎 Why This Works

- Each operation doubles the word.
- The index `k` traces a path through these doubling steps.
- `k - 1` in binary tells us which half of the string the character comes from at each stage.
- We only care about **how many transforms (operation = 1)** were encountered.

---

Here are **clean DSA-style notes** in the exact format you asked for, matching the style of the `"K-th Character After Sequence of Copy and Transform Operations"` explanation.

---

# 08-07-25

## 🧠 **Attend The Maximum Number Of Events**

You’re given a list of events:

```js
events[i] = [startDay, endDay];
```

You can attend **one event per day**, and for each event you can choose **any day between `startDay` and `endDay`** (inclusive) to attend.

🎯 Your goal is to **attend the maximum number of events**.

---

### 🧪 Example

```txt
Input: events = [[1,2], [2,3], [3,4]]
Output: 3
Explanation:
Attend one event on day 1, one on day 2, and one on day 3.
```

---

### ✅ **Approach: Greedy + Min Heap**

### 🔍 Key Insight

We want to always attend the event that ends **earliest**, to keep future days available for events with tighter schedules.

### ⚙️ Steps

1. Sort the events by start day.
2. Use a **min-heap (priority queue)** to always pick the event that ends earliest.
3. Iterate over each day from the first to the last possible event day:

   - Add all events starting **today** to the heap.
   - Remove events from the heap that have **already expired**.
   - If any events are available today, attend the one that ends earliest (i.e., pop from heap).
   - Move to next day.

---

### ✅ **Full Code: Max Events with MinHeap**

```js
// MinHeap class for efficiently getting the event with the earliest end day
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
    const min = this.heap[0];
    const end = this.heap.pop();
    if (this.heap.length > 0) {
      this.heap[0] = end;
      this._heapifyDown();
    }
    return min;
  }

  peek() {
    return this.heap[0] ?? null;
  }

  size() {
    return this.heap.length;
  }

  _heapifyUp() {
    let idx = this.heap.length - 1;
    while (idx > 0) {
      let parent = Math.floor((idx - 1) / 2);
      if (this.heap[parent] <= this.heap[idx]) break;
      [this.heap[parent], this.heap[idx]] = [this.heap[idx], this.heap[parent]];
      idx = parent;
    }
  }

  _heapifyDown() {
    let idx = 0;
    const len = this.heap.length;

    while (true) {
      let left = 2 * idx + 1;
      let right = 2 * idx + 2;
      let smallest = idx;

      if (left < len && this.heap[left] < this.heap[smallest]) smallest = left;
      if (right < len && this.heap[right] < this.heap[smallest])
        smallest = right;

      if (smallest === idx) break;

      [this.heap[smallest], this.heap[idx]] = [
        this.heap[idx],
        this.heap[smallest],
      ];
      idx = smallest;
    }
  }
}
```

---

### 🚀 **Main Function: `maxEvents()`**

```js
function maxEvents(events) {
  // Step 1: Sort events by start day
  events.sort((a, b) => a[0] - b[0]);

  const heap = new MinHeap();
  let day = 1;
  let eventIndex = 0;
  let attended = 0;
  const maxDay = Math.max(...events.map((e) => e[1]));

  // Step 2: Simulate each day
  while (day <= maxDay) {
    // Step 3: Push all events that start today into the heap
    while (eventIndex < events.length && events[eventIndex][0] === day) {
      heap.insert(events[eventIndex][1]); // Insert endDay
      eventIndex++;
    }

    // Step 4: Remove all expired events
    while (heap.size() > 0 && heap.peek() < day) {
      heap.extractMin();
    }

    // Step 5: Attend the event with earliest end day
    if (heap.size() > 0) {
      heap.extractMin(); // Attend this event
      attended++;
    }

    day++;
  }

  return attended;
}
```

---

### 🧪 Example Usage

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
    [1, 2],
    [1, 6],
    [2, 3],
  ])
); // Output: 4
console.log(
  maxEvents([
    [1, 4],
    [4, 4],
    [2, 2],
    [3, 4],
  ])
); // Output: 4
```

---

### ⏱ Time Complexity

- Sorting: **O(n log n)**
- Each event is pushed and popped once → **O(n log n)** using proper heap

> Total: **O(n log n)**
> Space: **O(n)** for the heap

---

### 📌 Summary

| Technique | Description                                      |
| --------- | ------------------------------------------------ |
| Greedy    | Always attend the soonest-ending event available |
| Min-Heap  | Pick event with smallest `endDay` at each step   |
| Sort      | Sort by `startDay` first                         |

---

# 09-07-25

## 🧮 **Maximize Free Time by Rescheduling Meetings**

### 📘 **Problem Statement**

You are given:

- An integer `eventTime` representing the full duration of an event (`0` to `eventTime`).
- Two arrays:

  - `startTime[]`: Start times of `n` **non-overlapping meetings**.
  - `endTime[]`: End times of those meetings.

You can **reschedule at most `k` meetings**, while preserving:

- Same **duration** of each meeting.
- **Relative order** of meetings.
- No **overlap**.
- Meetings must stay **within event time**.

🔁 **Goal**: Reschedule up to `k` meetings to **maximize the longest continuous free time** during the event.

---

### 🧪 **Test Cases**

**Test Case 1:**

```js
Input: (eventTime = 5), (k = 1), (startTime = [1, 3]), (endTime = [2, 5]);
Output: 2;
```

➡️ Reschedule `[1, 2]` to `[2, 3]` → free time from `0 to 2` = **2**

---

**Test Case 2:**

```js
Input: (eventTime = 10),
  (k = 1),
  (startTime = [0, 2, 9]),
  (endTime = [1, 4, 10]);
Output: 6;
```

➡️ Reschedule `[2, 4]` to `[1, 3]` → free time from `3 to 9` = **6**

---

**Test Case 3:**

```js
Input: (eventTime = 5),
  (k = 2),
  (startTime = [0, 1, 2, 3, 4]),
  (endTime = [1, 2, 3, 4, 5]);
Output: 0;
```

➡️ No room to move → **no free gap**

---

### 💡 **Key Insight**

Rather than trying all permutations:

- Meetings must **stay in order** and **not overlap**.
- Only **k meetings** can be moved.
- Try to find **longest continuous gap** between meetings by trying different subsets.

So:

- You calculate the **gaps between meetings** and the trailing free time after the last one.
- Since each rescheduled meeting can potentially **merge two adjacent gaps**, rescheduling `k` meetings gives `k + 1` such segments.
- Using a **sliding window** of size `k + 1`, you find the **maximum sum** of consecutive free time segments.

---

### ✅ **JavaScript Code (Sliding Window Approach)**

```javascript
/**
 * @param {number} eventTime
 * @param {number} k
 * @param {number[]} startTime
 * @param {number[]} endTime
 * @return {number}
 */
var maxFreeTime = function (eventTime, k, startTime, endTime) {
  let freespace = getFreeSpaces(startTime, endTime, eventTime);
  let maxFreeTime = getMaxSumOfWindowLength(freespace, k + 1);
  return maxFreeTime;
};

/**
 * Finds all free intervals between meetings and after last meeting.
 * @param {number[]} startTime
 * @param {number[]} endTime
 * @param {number} eventTime
 * @returns {number[]} Array of free durations
 */
function getFreeSpaces(startTime, endTime, eventTime) {
  let prevEnd = 0;
  let freeSpaces = [];

  for (let i = 0; i < startTime.length; i++) {
    freeSpaces.push(startTime[i] - prevEnd);
    prevEnd = endTime[i];
  }

  // Add space after the last meeting
  freeSpaces.push(eventTime - prevEnd);
  return freeSpaces;
}

/**
 * Sliding window to find max sum of any k+1 contiguous free segments.
 * @param {number[]} nums - Free time segments
 * @param {number} k - Window size (k+1 gaps for k reschedules)
 * @returns {number}
 */
function getMaxSumOfWindowLength(nums, k) {
  let sum = 0;
  let maxSum = 0;

  for (let right = 0; right < nums.length; right++) {
    sum += nums[right];
    if (right - k >= 0) {
      sum -= nums[right - k];
    }
    maxSum = Math.max(maxSum, sum);
  }

  return maxSum;
}
```

---

### 💡 **Key Idea**

---

### ⏱ **Time & Space Complexity**

| Metric | Value |
| ------ | ----- |
| Time   | O(n)  |
| Space  | O(n)  |

---

### 📌 **Summary Table**

| Concept              | Explanation                                            |
| -------------------- | ------------------------------------------------------ |
| `getFreeSpaces()`    | Finds gaps between meetings + final free segment       |
| Sliding Window (k+1) | Simulates merging `k` meetings to unlock `k+1` gaps    |
| Maximize Free Time   | Search for max contiguous sum of `k + 1` free segments |

---

# 10-07-25

# 🗓️ 10-07-25

## 🧮 **Maximize Free Time by Rescheduling One Meeting (Order Change Allowed)**

### 📘 **Problem Statement**

You are given:

- An integer `eventTime` representing the full duration of an event (`0` to `eventTime`).
- Two arrays:

  - `startTime[]`: Start times of `n` non-overlapping meetings.
  - `endTime[]`: End times of those meetings.

Each meeting occurs in the range `[startTime[i], endTime[i]]`.

You can **reschedule at most one meeting**, and you may change:

- Its **start time**, but must maintain the **same duration**.
- Its **position** in the overall meeting list (relative order **can change**).

🔁 **Goal**: Reschedule one meeting to **maximize the longest continuous period of free time**, while ensuring:

- Meetings remain **non-overlapping**.
- All meetings are within `[0, eventTime]`.

---

### 🧪 **Test Cases**

**Test Case 1**

```js
Input: (eventTime = 10), (startTime = [0, 2, 9]), (endTime = [1, 4, 10]);
Output: 6;
```

➡️ Reschedule `[2,4]` to `[1,3]`, meetings become: \[0–1], \[1–3], \[9–10]
➡️ Free time = `[3,9]` → **6**

---

**Test Case 2**

```js
Input: (eventTime = 5), (startTime = [1, 3]), (endTime = [2, 5]);
Output: 2;
```

➡️ Move `[1,2]` to `[2,3]` → Free from `0–2` ⇒ **2**

---

**Test Case 3**

```js
Input: (eventTime = 5),
  (startTime = [0, 1, 2, 3, 4]),
  (endTime = [1, 2, 3, 4, 5]);
Output: 0;
```

➡️ No room to move anything → **0**

---

### 💡 **Key Insight**

Since **only one meeting can be rescheduled** and **reordering is allowed**, we:

1. Compute all the **gaps** between meetings (and after last).
2. Try to **insert the duration of the rescheduled meeting** into any of those gaps.
3. The **maximum continuous free time** is either:

   - **Gap before rescheduling**, or
   - **Gap + inserted meeting duration + adjacent gap**, if we can merge.

4. Use `leftMax` and `rightMax` arrays to efficiently calculate best placements.

---

### ✅ **JavaScript Code**

```javascript
/**
 * @param {number} eventTime
 * @param {number[]} startTime
 * @param {number[]} endTime
 * @return {number}
 */
const maxFreeTime = (eventTime, startTime, endTime) => {
  const len = startTime.length;
  const gaps = new Array(len + 1);
  let lastEnd = 0;

  // Step 1: Calculate gaps between meetings
  startTime.forEach((s, i) => {
    gaps[i] = s - lastEnd;
    lastEnd = endTime[i];
  });

  // Final gap after the last meeting
  gaps[len] = eventTime - lastEnd;

  // Step 2: Build right max array for future gaps
  const rightMax = new Array(len + 1).fill(0);
  rightMax.reduceRight((_, __, i) => {
    if (i < len) rightMax[i] = Math.max(rightMax[i + 1], gaps[i + 1]);
  }, 0);

  // Step 3: Try inserting each meeting in a new position
  let leftMax = 0;
  let maxGap = 0;

  startTime
    .map((_, i) => i + 1)
    .forEach((i) => {
      const dur = endTime[i - 1] - startTime[i - 1];
      const gapL = gaps[i - 1];
      const gapR = gaps[i];

      // If this meeting can fit into left or right side, try merging
      if (leftMax >= dur || rightMax[i] >= dur)
        maxGap = Math.max(maxGap, gapL + dur + gapR);

      // Try merging adjacent gaps directly
      maxGap = Math.max(maxGap, gapL + gapR);

      // Update left max for future iterations
      leftMax = Math.max(leftMax, gapL);
    });

  return maxGap;
};
```

---

### ⏱ **Time & Space Complexity**

| Metric | Value  |
| ------ | ------ |
| Time   | `O(n)` |
| Space  | `O(n)` |

- Efficient linear scan using prefix and suffix max arrays.

---

### 📌 **Summary Table**

| Concept        | Explanation                                               |
| -------------- | --------------------------------------------------------- |
| `gaps[]`       | Stores all free segments between and after meetings       |
| `rightMax[]`   | Suffix max of future gaps for fast lookup                 |
| `leftMax`      | Tracks largest gap on the left side for current iteration |
| Merge Strategy | Try merging adjacent gaps with one rescheduled meeting    |
| Final Output   | Max possible merged gap size (continuous free time)       |

---
