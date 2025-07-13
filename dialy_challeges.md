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

# 🗓️ 11-07-25

## 🧮 **Most Booked Meeting Room (with Delay and Rescheduling)**

### 📘 **Problem Statement**

You are given:

- An integer `n`, the number of meeting rooms labeled from `0` to `n-1`.
- A 2D array `meetings[][]`, where `meetings[i] = [start, end]` represents a meeting request.

Each meeting must be assigned to:

- The **unused room with the lowest index**, if available.
- Otherwise, it is **delayed until the earliest available room becomes free**, but it must **keep the same duration**.

**When multiple meetings are waiting**, those with **earlier original `start` times** get priority.

---

🔁 **Goal**: Return the room that handled the **most meetings**. If multiple rooms tie, return the one with the **lowest number**.

---

### 🧪 **Test Cases**

#### **Test Case 1**

```js
Input: (n = 2),
  (meetings = [
    [0, 10],
    [1, 5],
    [2, 7],
    [3, 4],
  ]);
Output: 0;
```

✅ **Explanation**:

- Room 0 → \[0,10), then \[10,11)
- Room 1 → \[1,5), then \[5,10)
  Both have 2 meetings → Return **0**

---

#### **Test Case 2**

```js
Input: (n = 3),
  (meetings = [
    [1, 20],
    [2, 10],
    [3, 5],
    [4, 9],
    [6, 8],
  ]);
Output: 1;
```

✅ **Explanation**:

- Room 0 → \[1,20)
- Room 1 → \[2,10), \[10,12)
- Room 2 → \[3,5), \[5,10)
  Room 1 and 2 had 2 each, but **room 1 is smaller** → Return **1**

---

### 💡 **Key Insight**

This is a **heap simulation problem** with:

- One **min-heap for free rooms** (by room number).
- One **min-heap for busy rooms** (by end time, and room number for tie-break).
- Sort `meetings` by their **original start time**.
- Track meeting **counts per room**.

---

### ✅ **JavaScript Code**

```javascript
class MinHeap {
  constructor(compare) {
    this.data = [];
    this.compare = compare;
  }

  size() {
    return this.data.length;
  }

  top() {
    return this.data[0];
  }

  push(val) {
    this.data.push(val);
    this._heapifyUp();
  }

  pop() {
    if (this.data.length === 1) return this.data.pop();
    const top = this.data[0];
    this.data[0] = this.data.pop();
    this._heapifyDown();
    return top;
  }

  _heapifyUp() {
    let i = this.data.length - 1;
    while (i > 0) {
      const p = Math.floor((i - 1) / 2);
      if (this.compare(this.data[i], this.data[p]) < 0) {
        [this.data[i], this.data[p]] = [this.data[p], this.data[i]];
        i = p;
      } else break;
    }
  }

  _heapifyDown() {
    let i = 0;
    const n = this.data.length;
    while (true) {
      let smallest = i;
      const l = 2 * i + 1,
        r = 2 * i + 2;
      if (l < n && this.compare(this.data[l], this.data[smallest]) < 0)
        smallest = l;
      if (r < n && this.compare(this.data[r], this.data[smallest]) < 0)
        smallest = r;
      if (smallest !== i) {
        [this.data[i], this.data[smallest]] = [
          this.data[smallest],
          this.data[i],
        ];
        i = smallest;
      } else break;
    }
  }
}

/**
 * @param {number} n
 * @param {number[][]} meetings
 * @return {number}
 */
const mostBooked = (n, meetings) => {
  meetings.sort((a, b) => a[0] - b[0]);

  const roomCount = new Array(n).fill(0);

  // MinHeap for free rooms by room number
  const freeRooms = new MinHeap((a, b) => a - b);
  for (let i = 0; i < n; i++) freeRooms.push(i);

  // MinHeap for busy rooms by [endTime, room]
  const busyRooms = new MinHeap((a, b) =>
    a[0] !== b[0] ? a[0] - b[0] : a[1] - b[1]
  );

  for (let [start, end] of meetings) {
    const duration = end - start;

    // Free rooms that have become available by current start time
    while (busyRooms.size() && busyRooms.top()[0] <= start) {
      const [_, room] = busyRooms.pop();
      freeRooms.push(room);
    }

    if (freeRooms.size() > 0) {
      const room = freeRooms.pop();
      roomCount[room]++;
      busyRooms.push([end, room]);
    } else {
      const [nextEndTime, room] = busyRooms.pop();
      roomCount[room]++;
      busyRooms.push([nextEndTime + duration, room]);
    }
  }

  let maxMeetings = 0,
    resultRoom = 0;
  for (let i = 0; i < n; i++) {
    if (roomCount[i] > maxMeetings) {
      maxMeetings = roomCount[i];
      resultRoom = i;
    }
  }

  return resultRoom;
};
```

---

### ⏱ **Time & Space Complexity**

| Metric | Value                                        |
| ------ | -------------------------------------------- |
| Time   | `O(m log n)` where `m` is number of meetings |
| Space  | `O(n + m)`                                   |

- Sorting meetings takes `O(m log m)`
- Each insertion/removal from the heaps is `O(log n)`
- We process each meeting once

---

# 12-07-25

# 🏆 Tournament Round Matchup

## 🧾 **Problem Statement**

You are given:

- `n`: total number of players, numbered from `1` to `n`.
- `firstPlayer` and `secondPlayer`: two **top players** who **only lose to each other**.

### 🧩 Rules:

- Players are arranged in a line.
- In each round:

  - The **ith** player from the **start** plays the **ith** player from the **end**.
  - If odd number of players, the **middle one advances automatically**.

- After each round, **winners are sorted by their original number order**.

### 🎯 Goal:

Return `[earliest, latest]` round in which `firstPlayer` and `secondPlayer` may compete.

---

## 🧪 Test Cases

### ✅ Test Case 1

```js
Input: (n = 11), (firstPlayer = 2), (secondPlayer = 4);
Output: [3, 4];
```

#### ✅ Explanation:

- **Earliest** path: Let weak players win to eliminate others fast.

  - Round 1: 1 2 3 4 5 6 7 8 9 10 11
  - Round 2: 2 3 4 5 6 11
  - Round 3: 2 3 4 ← match!

- **Latest** path: Let `1, 3` win instead of 2’s and 4’s pathmates.

  - Round 1: 1 2 3 4 5 6 7 8 9 10 11
  - Round 2: 1 2 3 4 5 6
  - Round 3: 1 2 4
  - Round 4: 2 4 ← match!

---

### ✅ Test Case 2

```js
Input: (n = 5), (firstPlayer = 1), (secondPlayer = 5);
Output: [1, 1];
```

#### ✅ Explanation:

- Players 1 and 5 meet **immediately** in Round 1: (1 vs 5)

---

## 💡 Key Insight

Simulate each round with:

- A **bitmask** representing which players are still in.
- Choose any outcome for non-key matches.
- Use DFS to try **all valid paths**.
- Track when `firstPlayer` meets `secondPlayer`.

---

Here's your provided **bitmask-based DFS solution**, fully annotated and structured in the same style as previous explanations, under the label `sol`.

---

## ✅ JavaScript Code (🔹`sol` version)

```javascript
/**
 * @param {number} n
 * @param {number} firstPlayer
 * @param {number} secondPlayer
 * @return {number[]}
 */
var earliestAndLatest = function (n, firstPlayer, secondPlayer) {
  let min = Infinity;
  let max = -Infinity;

  // Convert to 0-based indices
  firstPlayer--;
  secondPlayer--;

  /**
   * Recursive DFS with bitmask.
   * @param {number} mask - current players (bitmask)
   * @param {number} i - left index
   * @param {number} j - right index
   * @param {number} round - current round number
   */
  function solve(mask, i, j, round) {
    if (i >= j) {
      // All matchups processed → next round
      solve(mask, 0, n - 1, round + 1);
      return;
    }

    // If i-th player is out → skip
    if ((mask & (1 << i)) === 0) {
      solve(mask, i + 1, j, round);
    }
    // If j-th player is out → skip
    else if ((mask & (1 << j)) === 0) {
      solve(mask, i, j - 1, round);
    }
    // i and j are both still in play
    else if (
      (i === firstPlayer && j === secondPlayer) ||
      (i === secondPlayer && j === firstPlayer)
    ) {
      // Found the round they meet
      min = Math.min(min, round);
      max = Math.max(max, round);
    } else {
      // Try both outcomes:
      // Case 1: j wins → i is removed
      if (i !== firstPlayer && i !== secondPlayer) {
        solve(mask ^ (1 << i), i + 1, j - 1, round);
      }
      // Case 2: i wins → j is removed
      if (j !== firstPlayer && j !== secondPlayer) {
        solve(mask ^ (1 << j), i + 1, j - 1, round);
      }
    }
  }

  // All players initially active (bitmask 111...1)
  solve((1 << n) - 1, 0, n - 1, 1);

  return [min, max];
};
```

---

## 💡 Key Insight

- Represent the current state using a **bitmask** (`1 << n`), where `1` means the player is still in the game.
- In each round:

  - Recursively simulate all valid outcomes for non-critical matchups.
  - Prune the simulation when `firstPlayer` and `secondPlayer` meet.

---

## ⏱ Time & Space Complexity

| Metric | Value                  |
| ------ | ---------------------- |
| Time   | `O(2^n)` worst case    |
| Space  | `O(n)` recursion depth |

- Works efficiently since `n ≤ 28`.

---

## 🧪 Example

```js
Input: (n = 11), (firstPlayer = 2), (secondPlayer = 4);
Output: [3, 4];
```

```js
Input: (n = 5), (firstPlayer = 1), (secondPlayer = 5);
Output: [1, 1];
```

---

## ✅ Summary Table

| Feature      | Description                                |
| ------------ | ------------------------------------------ |
| Approach     | Bitmask + DFS backtracking                 |
| Key Idea     | Track survivors and simulate both outcomes |
| First/Second | Only lose to each other                    |
| Output       | \[Earliest Round, Latest Round]            |

---

# 13-07-25

# 🏆 Largest Number Formation

## 🧾 **Problem Statement**

You are given an array of **non-negative integers**. You need to **arrange them such that they form the largest possible number**.

### 🎯 Goal:

Return the **largest number** that can be formed by arranging the elements as strings.

- If the result is all zeros (e.g., `[0,0]`), return `"0"`.

---

## 🧪 Test Cases

### ✅ Test Case 1

```js
Input: [3, 30, 34, 5, 9];
Output: "9534330";
```

#### ✅ Explanation:

- Optimal order: `9`, `5`, `34`, `3`, `30`
- Concatenated result: `"9534330"`

---

### ✅ Test Case 2

```js
Input: [0, 0];
Output: "0";
```

#### ✅ Explanation:

- Since all elements are zero, just return `"0"`

---

## 💡 Key Insight

- Sort numbers as **strings**, but **not** in traditional numerical or lexicographical order.

- Compare two numbers `a` and `b` by checking:

  ```js
  a + b > b + a;
  ```

- This ensures the arrangement results in the **maximum concatenated value**.

---

## ✅ JavaScript Code

```javascript
/**
 * @param {number[]} arr
 * @return {string}
 */
function formLargestNumber(arr) {
  // Convert all numbers to strings
  arr = arr.map(String);

  // Sort using custom comparator
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      const ab = arr[i] + arr[j];
      const ba = arr[j] + arr[i];
      if (ab < ba) {
        // Swap if ba should come before ab
        [arr[i], arr[j]] = [arr[j], arr[i]];
      }
    }
  }

  // Edge case: all zeros → return "0"
  if (arr[0] === "0") return "0";

  return arr.join("");
}
```

---

## ⏱ Time & Space Complexity

| Metric | Value        |
| ------ | ------------ |
| Time   | `O(n^2 * k)` |
| Space  | `O(n * k)`   |

- `n`: number of elements
- `k`: average length of number as string
- Sorting via nested loop (like bubble sort)

> In production, you'd want to use `arr.sort()` with a custom comparator for better performance (`O(n log n)`).

---

## 🧪 Additional Example

```js
Input: [10, 2];
Output: "210";
```

- Comparison: "210" > "102"

---

## ✅ Summary Table

| Feature   | Description                                          |
| --------- | ---------------------------------------------------- |
| Approach  | Custom comparator via pairwise string comparison     |
| Key Idea  | Compare (a + b) vs (b + a) for best arrangement      |
| Edge Case | Leading zeros → return `"0"` if first digit is `"0"` |
| Output    | Largest concatenated number as a string              |

---
