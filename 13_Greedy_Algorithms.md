# 📘 Greedy Algorithm

## 🧠 What is a Greedy Algorithm?

A **Greedy Algorithm** is an approach for solving optimization problems by **making the locally optimal choice at each step** with the hope of finding a global optimum.

> At each step, you pick the best option **without reconsidering** previous choices.

---

## 🧱 Key Characteristics

| Property                          | Description                                                                                   |
| --------------------------------- | --------------------------------------------------------------------------------------------- |
| **Local Optimization**            | Always picks the best solution at the current moment.                                         |
| **No Backtracking**               | Doesn't go back to change decisions once made.                                                |
| **Fast & Simple**                 | Greedy solutions are often faster and simpler than dynamic programming.                       |
| **Doesn't work for all problems** | Only works when a problem exhibits a **greedy-choice property** and **optimal substructure**. |

---

## ✅ When Can You Use Greedy?

### 🔁 Optimal Substructure

The problem can be broken down into subproblems, and the global solution is built from local solutions.

### 🔂 Greedy Choice Property

A global optimum can be arrived at by choosing local optimums.

---

## 🧮 Greedy vs Dynamic Programming

| Feature                    | Greedy                 | Dynamic Programming      |
| -------------------------- | ---------------------- | ------------------------ |
| Choice                     | Local optimal          | Checks all possibilities |
| Backtracking               | No                     | Yes                      |
| Reusability of Subproblems | Sometimes              | Always                   |
| Use-case                   | Simple & fast problems | Complex problems         |

---

## 🧑‍🏫 Step-by-Step Greedy Algorithm Design

1. **Understand the problem**
2. **Sort or prioritize data (if needed)**
3. **Make the best choice at each step**
4. **Track results / update state**
5. **Repeat until goal is met or all choices used**

---

## ⚠️ Pitfalls of Greedy

- **Not always optimal** — Doesn’t work for 0/1 Knapsack, longest increasing subsequence, matrix chain multiplication.
- Needs **proof of correctness** for each case.
- Overuse can lead to **incorrect assumptions**.

---

# **Easy Problems**

## 🔢 **1. Assign Cookies**

### 📘 Problem Statement

You are given two integer arrays:

- `g[]` representing the **greed factor** of each child.
- `s[]` representing the **sizes of cookies**.

> A child will be content if they are given a cookie with size **≥ greed factor**.
>
> Return the **maximum number of content children** you can satisfy.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (g = [1, 2, 3]), (s = [1, 1]);
Output: 1;
// Only the child with greed 1 can be satisfied with a cookie of size 1.
```

#### ✅ Test Case 2:

```js
Input: (g = [1, 2]), (s = [1, 2, 3]);
Output: 2;
// Both children can be satisfied with cookies of size 1 and 2.
```

#### ✅ Test Case 3:

```js
Input: (g = [5, 10, 2, 9, 15, 9]), (s = [6, 1, 20, 3, 8]);
Output: 3;
```

---

### 🧠 Intuition

We want to assign the **smallest possible cookie** to each child that still satisfies their greed.

This is a **greedy problem**:

- Sort both arrays.
- Always give the **smallest suitable cookie** to the **least greedy unsatisfied child**.

---

### 🔄 Dry Run

```plaintext
g = [1, 2, 3]
s = [1, 1]

Sort:
g = [1, 2, 3]
s = [1, 1]

Try to satisfy children from left:
Child 1 (greed=1) → Cookie 1 → ✅
Child 2 (greed=2) → Cookie 1 → ❌

✅ Total = 1
```

---

### ✅ Greedy Two-Pointer Approach

---

### ✅ JavaScript Code

```js
function findContentChildren(g, s) {
  g.sort((a, b) => a - b); // sort greed factors
  s.sort((a, b) => a - b); // sort cookie sizes

  let child = 0,
    cookie = 0;

  while (child < g.length && cookie < s.length) {
    if (s[cookie] >= g[child]) {
      child++;
    }
    cookie++;
  }

  return child;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity                         |
| -------- | ---------------------------------- |
| ⏳ Time  | O(n log n + m log m) – for sorting |
| 💾 Space | O(1)                               |

---

### 📌 Summary

| Approach                     | Time Complexity         | Space | Notes                                   |
| ---------------------------- | ----------------------- | ----- | --------------------------------------- |
| Brute Force                  | O(n \* m)               | O(1)  | Check every child with every cookie     |
| ✅ Greedy Sort + Two Pointer | ✅ O(n log n + m log m) | O(1)  | Efficient and optimal for interview use |

---

## 🔢 **2. Fractional Knapsack Problem**

### 📘 Problem Statement

You are given:

- A list of `n` items where each item has a **value `v[i]`** and a **weight `w[i]`**.
- A **knapsack with capacity `W`**.

> You can take **fractions of items**.
>
> Your goal is to maximize the total value placed in the knapsack.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (values = [60, 100, 120]), (weights = [10, 20, 30]), (W = 50);
Output: 240.0;
// Take item 1 fully (10), item 2 fully (20), and 2/3 of item 3 (20)
```

#### ✅ Test Case 2:

```js
Input: values = [500], weights = [30], W = 10
Output: 166.666...
// Take 1/3 of the item
```

#### ✅ Test Case 3:

```js
Input: (values = [10, 20, 30]), (weights = [5, 10, 15]), (W = 100);
Output: 60;
// All items fit
```

---

### 🧠 Intuition

This is a classic **Greedy Optimization Problem**.

We want to maximize **value per weight**. So, we:

- Compute value/weight for each item.
- Sort items in descending order of this ratio.
- Pick as much of the highest ratio item as possible.

---

### 🔄 Dry Run

```plaintext
values = [60, 100, 120]
weights = [10, 20, 30]
W = 50

value/weight:
Item1 = 6.0
Item2 = 5.0
Item3 = 4.0

Sort by ratio: [Item1, Item2, Item3]

Take:
- Full of Item1: weight=10 → value=60, W=40
- Full of Item2: weight=20 → value=100, W=20
- 20/30 of Item3: value = (20 * 4) = 80

Total = 60 + 100 + 80 = 240
```

---

### ✅ Greedy Sort + Pick Approach

---

### ✅ JavaScript Code

```js
function fractionalKnapsack(values, weights, capacity) {
  const items = values.map((v, i) => ({
    value: v,
    weight: weights[i],
    ratio: v / weights[i],
  }));

  items.sort((a, b) => b.ratio - a.ratio);

  let totalValue = 0;
  for (let item of items) {
    if (capacity === 0) break;

    if (item.weight <= capacity) {
      totalValue += item.value;
      capacity -= item.weight;
    } else {
      totalValue += item.ratio * capacity;
      capacity = 0;
    }
  }

  return totalValue;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity                      |
| -------- | ------------------------------- |
| ⏳ Time  | O(n log n) – due to sorting     |
| 💾 Space | O(n) – for storing item objects |

---

### 📌 Summary

| Approach                  | Time           | Space | Notes                           |
| ------------------------- | -------------- | ----- | ------------------------------- |
| Brute Force               | ❌ Not optimal | -     | Not feasible for fractions      |
| ✅ Greedy (Sort by ratio) | ✅ O(n log n)  | O(n)  | Optimal for fractional knapsack |

---

## 🔢 **3. Greedy Algorithm to Find Minimum Number of Coins**

### 📘 Problem Statement

You are given an amount `V` and a set of coin denominations `coins[]` (all positive integers).

> Find the **minimum number of coins** needed to make the amount `V`.
>
> You may **assume an infinite supply** of each coin denomination.
>
> If it’s **not possible** to form the amount, return `-1`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (coins = [1, 2, 5]), (V = 11);
Output: 3;
// 5 + 5 + 1 → 3 coins
```

#### ✅ Test Case 2:

```js
Input: (coins = [1, 10, 25]), (V = 30);
Output: 2;
// 25 + 5 → not possible, but 25 + 5 (if 5 exists) would be better
// But with [1, 10, 25]: 25 + 1 + 1 + 1 + 1 + 1 = 6 → Better to use 10 + 10 + 10 = 3
// Actually 25 + 1 + 1 + 1 + 1 + 1 = 6 → Answer is 3 with 10s
```

#### ✅ Test Case 3 (Indian currency):

```js
Input: (coins = [1, 2, 5, 10, 20, 50, 100, 200, 500, 2000]), (V = 93);
Output: 4;
// 50 + 20 + 20 + 2 + 1 = 5 coins
```

---

### 🧠 Intuition

We always want to use the **largest denomination coin** available that doesn't exceed the remaining amount.

> This strategy only works when the coin system is **canonical**, like Indian or US currency.

---

### 🔄 Dry Run

```plaintext
coins = [1, 2, 5, 10, 20, 50, 100, 200, 500, 2000]
V = 93

Sort in descending order:
[2000, 500, 200, 100, 50, 20, 10, 5, 2, 1]

Take:
- 50 → remaining = 43
- 20 → remaining = 23
- 20 → remaining = 3
- 2 → remaining = 1
- 1 → remaining = 0

Coins used = [50, 20, 20, 2, 1] → ✅ 5 coins
```

---

### ✅ Greedy Sort + Select Approach

---

### ✅ JavaScript Code

```js
function minCoins(coins, V) {
  coins.sort((a, b) => b - a); // Sort descending
  let count = 0;
  let i = 0;

  while (V > 0 && i < coins.length) {
    if (coins[i] <= V) {
      let used = Math.floor(V / coins[i]);
      count += used;
      V -= used * coins[i];
    }
    i++;
  }

  return V === 0 ? count : -1; // Return -1 if exact change not possible
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity                  |
| -------- | --------------------------- |
| ⏳ Time  | O(n log n) – for sorting    |
| 💾 Space | O(1) – constant extra space |

---

### 📌 Summary

| Approach     | Time                | Space | Notes                                                                  |
| ------------ | ------------------- | ----- | ---------------------------------------------------------------------- |
| Brute Force  | Exponential         | O(1)  | Try every combination – not feasible                                   |
| ✅ Greedy    | ✅ O(n log n)       | O(1)  | Works well when coin system is canonical (like Indian)                 |
| ❌ Fails for | Non-canonical coins | -     | Eg: coins = \[1, 3, 4], V = 6 → greedy gives 1+1+4, but 3+3 is optimal |

---

### ⚠️ Important Note:

This **Greedy solution does not always give optimal results** for **non-standard coin systems**. For such cases, use **Dynamic Programming** (Coin Change Problem).

---

## 🔢 **4. Lemonade Change**

### 📘 Problem Statement

At a lemonade stand, each lemonade costs **$5**. Customers queue up and pay with a **$5, $10, or $20 bill**.

> Initially, you have **no change**.
>
> Return `true` if you can give the correct change to every customer, else return `false`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: [5, 5, 5, 10, 20];
Output: true;
// Change for 10 → one 5
// Change for 20 → one 10 + one 5
```

#### ✅ Test Case 2:

```js
Input: [5, 5, 10, 10, 20];
Output: false;
// No 5 left to give change for 20
```

#### ✅ Test Case 3:

```js
Input: [5, 5, 10];
Output: true;
```

#### ✅ Test Case 4:

```js
Input: [10, 10];
Output: false;
// Can't give change for the first 10
```

---

### 🧠 Intuition

We simulate giving change greedily:

- **$5 bill:** No change needed → just collect.
- **$10 bill:** Need one $5 as change.
- **$20 bill:** Prefer to give one $10 and one $5 (larger denominations first). If not, give three $5 bills.

The goal is to always **preserve smaller bills** when possible for future customers.

---

### 🔄 Dry Run

```plaintext
Input = [5, 5, 5, 10, 20]
Start: five = 0, ten = 0

5 → five = 1
5 → five = 2
5 → five = 3
10 → use one five → five = 2, ten = 1
20 → use one ten + one five → five = 1, ten = 0

✅ All customers served
```

---

### ✅ JavaScript Code

```js
function lemonadeChange(bills) {
  let five = 0,
    ten = 0;

  for (let bill of bills) {
    if (bill === 5) {
      five++;
    } else if (bill === 10) {
      if (five === 0) return false;
      five--;
      ten++;
    } else {
      // bill === 20
      if (ten > 0 && five > 0) {
        ten--;
        five--;
      } else if (five >= 3) {
        five -= 3;
      } else {
        return false;
      }
    }
  }

  return true;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity                                |
| -------- | ----------------------------------------- |
| ⏳ Time  | O(n) – One pass through bills             |
| 💾 Space | O(1) – Only two counters used (five, ten) |

---

### 📌 Summary

| Bill Given | Change Needed | Strategy                                  |
| ---------- | ------------- | ----------------------------------------- |
| $5         | $0            | Collect $5                                |
| $10        | $5            | Give one $5                               |
| $20        | $15           | Prefer: one $10 + one $5 → else three $5s |

---

# Medium Problems

## 🔢 **1. N Meetings in One Room**

### 📘 Problem Statement

You are given `N` meetings with:

- A `start[]` array representing start times.
- An `end[]` array representing end times.

> You need to schedule the **maximum number of non-overlapping meetings** in one room.
>
> Return the count of meetings that can be scheduled.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (start = [1, 3, 0, 5, 8, 5]), (end = [2, 4, 6, 7, 9, 9]);
Output: 4;
// Meetings at index 0, 1, 3, 4 can be scheduled.
```

#### ✅ Test Case 2:

```js
Input: (start = [1, 2, 3]), (end = [4, 5, 6]);
Output: 3;
// All meetings can be scheduled without overlapping
```

#### ✅ Test Case 3:

```js
Input: (start = [1, 3, 2]), (end = [2, 4, 3]);
Output: 2;
// Select meetings 0 and 2 or 2 and 1
```

---

### 🧠 Intuition

This is a **classic greedy interval scheduling** problem.

> The greedy choice is to always select the **meeting that finishes earliest**, so that we can fit more meetings after it.

---

### 🔄 Dry Run

```plaintext
start = [1, 3, 0, 5, 8, 5]
end   = [2, 4, 6, 7, 9, 9]

Pair and sort by end times:
[(1, 2), (3, 4), (0, 6), (5, 7), (8, 9), (5, 9)]

Now schedule:
- First: (1, 2) → yes
- Next: (3, 4) → yes
- (0, 6) → no (overlaps)
- (5, 7) → yes
- (8, 9) → yes
- (5, 9) → no (overlaps)

✅ Total = 4 meetings
```

---

### ✅ JavaScript Code

```js
function maxMeetings(start, end) {
  const n = start.length;
  const meetings = [];

  for (let i = 0; i < n; i++) {
    meetings.push({ start: start[i], end: end[i] });
  }

  // Sort meetings by end time
  meetings.sort((a, b) => a.end - b.end);

  let count = 1;
  let lastEnd = meetings[0].end;

  for (let i = 1; i < n; i++) {
    if (meetings[i].start > lastEnd) {
      count++;
      lastEnd = meetings[i].end;
    }
  }

  return count;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity                         |
| -------- | ---------------------------------- |
| ⏳ Time  | O(n log n) – sorting by end time   |
| 💾 Space | O(n) – for storing meeting objects |

---

### 📌 Summary

| Approach                | Time          | Space | Notes                                    |
| ----------------------- | ------------- | ----- | ---------------------------------------- |
| Brute Force (Try all)   | Exponential   | O(1)  | Not feasible for large N                 |
| ✅ Greedy (sort by end) | ✅ O(n log n) | O(n)  | Standard and optimal interval scheduling |

---

## 🔢 **2. Jump Game**

### 📘 Problem Statement

You are given an array `nums` of length `n` where each element represents the **maximum jump length** from that position.

> Return `true` if you can **reach the last index**, otherwise return `false`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: nums = [2, 3, 1, 1, 4];
Output: true;
// Jump from 0 → 1 → 4
```

#### ✅ Test Case 2:

```js
Input: nums = [3, 2, 1, 0, 4];
Output: false;
// You get stuck at index 3
```

#### ✅ Test Case 3:

```js
Input: nums = [0];
Output: true;
// Already at the last index
```

#### ✅ Test Case 4:

```js
Input: nums = [1, 0, 1, 0];
Output: false;
// Can't reach index 2
```

---

### 🧠 Intuition

We want to **greedily track the farthest index** we can reach while iterating through the array.

> If at any index `i`, the farthest reachable position is **less than `i`**, we are stuck.

---

### 🔄 Dry Run

```plaintext
nums = [2, 3, 1, 1, 4]
Index:    0  1  2  3  4
Reachable:

Start with farthest = 0

i = 0 → max(farthest, 0 + nums[0]) = max(0, 2) = 2
i = 1 → 1 ≤ 2 → farthest = max(2, 1 + 3) = 4
i = 2 → 2 ≤ 4 → farthest = max(4, 2 + 1) = 4
i = 3 → 3 ≤ 4 → farthest = max(4, 3 + 1) = 4
i = 4 → 4 ≤ 4 → ✅

We reached the last index → return true
```

---

### ✅ JavaScript Code

```js
function canJump(nums) {
  let farthest = 0;

  for (let i = 0; i < nums.length; i++) {
    if (i > farthest) return false;
    farthest = Math.max(farthest, i + nums[i]);
  }

  return true;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity                       |
| -------- | -------------------------------- |
| ⏳ Time  | O(n) – Single pass through array |
| 💾 Space | O(1) – Constant space            |

---

### 📌 Summary

| Approach                | Time        | Space | Notes                                      |
| ----------------------- | ----------- | ----- | ------------------------------------------ |
| Brute Force (Recursion) | Exponential | O(n)  | Tries all paths – inefficient              |
| Dynamic Programming     | O(n²)       | O(n)  | Memoize reachable indices                  |
| ✅ Greedy (Max Reach)   | ✅ O(n)     | O(1)  | Most efficient and preferred in interviews |

---

## 🔢 **3. Jump Game II**

### 📘 Problem Statement

You are given an array `nums` where each element represents the **maximum jump length** from that position.

> Return the **minimum number of jumps** required to reach the **last index**.
>
> You can always reach the last index.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: nums = [2, 3, 1, 1, 4];
Output: 2;
// Jump from index 0 → 1 → 4
```

#### ✅ Test Case 2:

```js
Input: nums = [2, 3, 0, 1, 4];
Output: 2;
```

#### ✅ Test Case 3:

```js
Input: nums = [1, 2, 3];
Output: 2;
// 0 → 1 → 2
```

#### ✅ Test Case 4:

```js
Input: nums = [1];
Output: 0;
// Already at last index
```

---

### 🧠 Intuition

We want to **minimize the number of jumps**. So, we use a **greedy BFS-like level traversal**:

- We track the **current range** we can jump within.
- When we reach the end of the current range, we **increment the jump** and update the new range.

> Think of it as: “How far can I go with this jump?”
> Then: “When I need another jump, what’s the farthest I can go from this level?”

---

### 🔄 Dry Run

```plaintext
nums = [2, 3, 1, 1, 4]

Initialize:
jumps = 0
currEnd = 0
farthest = 0

i = 0 → farthest = max(0, 0 + 2) = 2
i = 1 → farthest = max(2, 1 + 3) = 4
i = 2 → farthest = max(4, 2 + 1) = 4

When i == currEnd (0 → reached end of first jump range):
→ jumps = 1, currEnd = farthest = 2

Continue...

i = 3 → farthest = max(4, 3 + 1) = 4
i = 4 → reached last index

When i == currEnd again (2):
→ jumps = 2, currEnd = farthest = 4

✅ Done with 2 jumps
```

---

### ✅ JavaScript Code

```js
function jump(nums) {
  let jumps = 0;
  let currEnd = 0;
  let farthest = 0;

  for (let i = 0; i < nums.length - 1; i++) {
    farthest = Math.max(farthest, i + nums[i]);

    if (i === currEnd) {
      jumps++;
      currEnd = farthest;
    }
  }

  return jumps;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity                |
| -------- | ------------------------- |
| ⏳ Time  | O(n) – Single pass        |
| 💾 Space | O(1) – Only counters used |

---

### 📌 Summary

| Approach                | Time        | Space | Notes                                               |
| ----------------------- | ----------- | ----- | --------------------------------------------------- |
| Brute Force             | Exponential | O(1)  | Try all paths                                       |
| DP (Tabulation)         | O(n²)       | O(n)  | Check all reachable jumps from every index          |
| ✅ Greedy (Optimal BFS) | ✅ O(n)     | O(1)  | Tracks level of reach using currentEnd and farthest |

---

## 🔢 **4. Minimum Number of Platforms Required for a Railway**

### 📘 Problem Statement

Given arrival and departure times of `n` trains at a station in two arrays:

- `arr[]` → arrival times
- `dep[]` → departure times

> Find the **minimum number of platforms** required so that no train has to wait for a platform.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: arr = [900, 940, 950, 1100, 1500, 1800];
dep = [910, 1200, 1120, 1130, 1900, 2000];
Output: 3;
```

#### ✅ Test Case 2:

```js
Input: arr = [100, 200, 300, 400];
dep = [500, 600, 700, 800];
Output: 4;
// All trains overlap
```

#### ✅ Test Case 3:

```js
Input: arr = [900, 1000, 1100];
dep = [930, 1030, 1130];
Output: 1;
// No overlap
```

---

### 🧠 Intuition

- Treat arrivals and departures as **events**.
- Sort both arrays.
- Use a **two-pointer technique** to simulate a **timeline**:

  - If a train arrives before another departs → need a new platform.
  - Else → a platform is freed.

---

### 🔄 Dry Run

```plaintext
arr = [900, 940, 950, 1100, 1500, 1800]
dep = [910, 1200, 1120, 1130, 1900, 2000]

Sort:
arr = [900, 940, 950, 1100, 1500, 1800]
dep = [910, 1120, 1130, 1200, 1900, 2000]

Start:
- i = 1, j = 0, platforms = 1, maxPlatforms = 1

→ arr[1] = 940 ≤ dep[0] = 910 ❌ → no
→ arr[1] = 940 > dep[0] = 910 ✅ → one departs → platforms = 0
→ arr[1] = 940 arrives → platforms = 1
→ and so on...

Track max platform count.
```

---

### ✅ Two-Pointer Greedy Timeline Approach

---

### ✅ JavaScript Code

```js
function findMinPlatforms(arr, dep) {
  arr.sort((a, b) => a - b);
  dep.sort((a, b) => a - b);

  let i = 1,
    j = 0;
  let platforms = 1,
    maxPlatforms = 1;

  while (i < arr.length && j < dep.length) {
    if (arr[i] <= dep[j]) {
      platforms++;
      i++;
    } else {
      platforms--;
      j++;
    }

    maxPlatforms = Math.max(maxPlatforms, platforms);
  }

  return maxPlatforms;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity                      |
| -------- | ------------------------------- |
| ⏳ Time  | O(n log n) – for sorting        |
| 💾 Space | O(1) – constant auxiliary space |

---

### 📌 Summary

| Approach              | Time          | Space | Notes                                          |
| --------------------- | ------------- | ----- | ---------------------------------------------- |
| Brute Force           | O(n²)         | O(1)  | Check overlap of every pair                    |
| ✅ Greedy (2-pointer) | ✅ O(n log n) | O(1)  | Optimal. Sort arrivals & departures separately |

---

## 🔢 **5. Job Sequencing Problem**

### 📘 Problem Statement

You are given an array of `n` jobs. Each job has:

- An `id`
- A `deadline`
- A `profit`

Each job takes **1 unit of time**, and **only one job** can be scheduled at a time.

> Schedule jobs to **maximize total profit**, ensuring that no job **misses its deadline**.

Return the **maximum number of jobs done** and the **maximum profit**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: jobs = [
  { id: "a", deadline: 2, profit: 100 },
  { id: "b", deadline: 1, profit: 19 },
  { id: "c", deadline: 2, profit: 27 },
  { id: "d", deadline: 1, profit: 25 },
  { id: "e", deadline: 3, profit: 15 },
];
Output: [2, 127];
// Schedule: 'a' at time 2, 'c' at time 1
```

#### ✅ Test Case 2:

```js
Input: jobs = [
  { id: "a", deadline: 1, profit: 10 },
  { id: "b", deadline: 1, profit: 20 },
  { id: "c", deadline: 1, profit: 30 },
];
Output: [1, 30];
// Only one job can be scheduled, choose max profit one
```

---

### 🧠 Intuition

To **maximize profit**, we should:

- Schedule **high-profit jobs first**
- Try to schedule them **before or on their deadline**

Use a **greedy strategy**:

1. Sort jobs by **profit descending**
2. For each job, try to put it in the **latest possible slot ≤ deadline**

---

### 🔄 Dry Run

```plaintext
jobs = [a(2,100), b(1,19), c(2,27), d(1,25), e(3,15)]

After sorting by profit:
[a(2,100), c(2,27), d(1,25), b(1,19), e(3,15)]

Slots = [null, null, null]

Try:
a → deadline 2 → put at slot 2 ✅
c → deadline 2 → slot 2 is taken → try 1 ✅
d → deadline 1 → slot 1 is taken ❌
b → deadline 1 → ❌
e → deadline 3 → slot 3 ✅

Final: [c, a, e] → 3 jobs, profit = 27 + 100 + 15 = 142
```

---

### ✅ Greedy + Latest Free Slot Allocation

---

### ✅ JavaScript Code

```js
function jobScheduling(jobs) {
  // Sort by profit descending
  jobs.sort((a, b) => b.profit - a.profit);

  const maxDeadline = Math.max(...jobs.map((job) => job.deadline));
  const slots = Array(maxDeadline + 1).fill(null); // index 0 unused

  let count = 0,
    totalProfit = 0;

  for (let job of jobs) {
    for (let i = job.deadline; i > 0; i--) {
      if (!slots[i]) {
        slots[i] = job.id;
        count++;
        totalProfit += job.profit;
        break;
      }
    }
  }

  return [count, totalProfit];
}
```

---

### ⏱ Time & Space Complexity

| Metric  | Complexity          |
| ------- | ------------------- |
| ⏳ Time | O(n log n + n \* d) |

> (Sort + loop through deadlines ≤ d) |
> \| 💾 Space | O(d) – slots array, where d = max deadline |

---

### 📌 Summary

| Approach    | Time                   | Space | Notes                                                   |
| ----------- | ---------------------- | ----- | ------------------------------------------------------- |
| Brute Force | O(n²)                  | O(1)  | Try all permutations                                    |
| ✅ Greedy   | ✅ O(n log n + n \* d) | O(d)  | Sort by profit, assign latest available slot ≤ deadline |

---

## 🔢 **6. Candy (Greedy)**

### 📘 Problem Statement

There are `n` children standing in a line. Each child is assigned a **rating** value.

> You must give each child at least **one candy**.
>
> Children with a **higher rating than their immediate neighbor(s)** must get **more candies** than them.

Return the **minimum number of candies** you must give.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: ratings = [1, 0, 2];
Output: 5;
// Candies: [2, 1, 2]
```

#### ✅ Test Case 2:

```js
Input: ratings = [1, 2, 2];
Output: 4;
// Candies: [1, 2, 1]
```

#### ✅ Test Case 3:

```js
Input: ratings = [1, 3, 4, 5, 2];
Output: 11;
// Candies: [1, 2, 3, 4, 1]
```

#### ✅ Test Case 4:

```js
Input: ratings = [1, 2, 3, 1, 0];
Output: 9;
// Candies: [1, 2, 3, 2, 1]
```

---

### 🧠 Intuition

This is a **two-pass greedy algorithm**:

1. **Left to right**: If `ratings[i] > ratings[i-1]`, then `candies[i] = candies[i-1] + 1`
2. **Right to left**: If `ratings[i] > ratings[i+1]`, then `candies[i] = max(candies[i], candies[i+1] + 1)`

We make sure that **both left and right neighbors** are satisfied.

---

### 🔄 Dry Run

```plaintext
ratings = [1, 0, 2]

Left to right:
Initialize candies = [1, 1, 1]

i = 1: 0 < 1 → no change
i = 2: 2 > 0 → candies[2] = candies[1] + 1 = 2
→ candies = [1, 1, 2]

Right to left:
i = 1: 0 < 2 → no change
i = 0: 1 > 0 → candies[0] = max(1, 1 + 1) = 2
→ candies = [2, 1, 2]

Sum = 5 ✅
```

---

### ✅ Two-Pass Greedy Approach

---

### ✅ JavaScript Code

```js
function candy(ratings) {
  const n = ratings.length;
  const candies = Array(n).fill(1);

  // Left to right
  for (let i = 1; i < n; i++) {
    if (ratings[i] > ratings[i - 1]) {
      candies[i] = candies[i - 1] + 1;
    }
  }

  // Right to left
  for (let i = n - 2; i >= 0; i--) {
    if (ratings[i] > ratings[i + 1]) {
      candies[i] = Math.max(candies[i], candies[i + 1] + 1);
    }
  }

  return candies.reduce((a, b) => a + b, 0);
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity              |
| -------- | ----------------------- |
| ⏳ Time  | O(n) – Two passes       |
| 💾 Space | O(n) – To store candies |

---

### 📌 Summary

| Pass         | Purpose                               |
| ------------ | ------------------------------------- |
| Left → Right | Ensure increasing sequences get more  |
| Right → Left | Ensure decreasing sequences are valid |
| Final Sum    | Get total minimum candies             |

---

## 🔢 **7. Shortest Job First (SJF) Scheduling – Non-Preemptive**

### 📘 Problem Statement

You're given a list of `n` processes, each with:

- A **Process ID**
- A **Burst Time** (execution time)
- An **Arrival Time**

> Implement the **Shortest Job First (SJF)** **non-preemptive** scheduling algorithm and calculate:
>
> - Completion Time
> - Turnaround Time = Completion Time - Arrival Time
> - Waiting Time = Turnaround Time - Burst Time

---

### 🧪 Test Case

#### ✅ Test Case:

```plaintext
Processes = [
  { pid: 1, arrival: 0, burst: 7 },
  { pid: 2, arrival: 2, burst: 4 },
  { pid: 3, arrival: 4, burst: 1 },
  { pid: 4, arrival: 5, burst: 4 }
]
```

Expected scheduling order (by burst time among available processes):

- P1 → P3 → P2 → P4

---

### 🧠 Intuition

This is **non-preemptive**, so once a process starts, it runs to completion.

- At every point in time, select the **available process with the shortest burst time**.
- If no process has arrived yet, **increment the time**.

---

### 🔄 Dry Run (Timeline)

```plaintext
Time | Process | Explanation
-----|---------|-------------
  0  | P1      | Only P1 has arrived
  7  | P3      | P3 arrives at 4, shortest burst (1)
  8  | P2      | P2 (burst 4) and P4 (burst 4) both available → choose lowest PID
 12  | P4      | Last process
 16  | Done
```

---

### ✅ JavaScript Code (Non-Preemptive SJF)

```js
function sjfScheduling(processes) {
  const n = processes.length;
  const completed = [];
  const isDone = Array(n).fill(false);
  let time = 0,
    count = 0;

  const result = processes.map((p, index) => ({
    pid: p.pid,
    arrival: p.arrival,
    burst: p.burst,
    completion: 0,
    turnaround: 0,
    waiting: 0,
    index,
  }));

  while (count < n) {
    let idx = -1;
    let minBurst = Infinity;

    for (let i = 0; i < n; i++) {
      if (
        !isDone[i] &&
        processes[i].arrival <= time &&
        processes[i].burst < minBurst
      ) {
        minBurst = processes[i].burst;
        idx = i;
      }
    }

    if (idx === -1) {
      time++;
      continue;
    }

    time += processes[idx].burst;
    result[idx].completion = time;
    result[idx].turnaround = time - processes[idx].arrival;
    result[idx].waiting = result[idx].turnaround - processes[idx].burst;
    isDone[idx] = true;
    count++;
  }

  // Sort by process ID before returning
  result.sort((a, b) => a.pid - b.pid);

  return result;
}
```

---

### 📋 Example Output

```js
const processes = [
  { pid: 1, arrival: 0, burst: 7 },
  { pid: 2, arrival: 2, burst: 4 },
  { pid: 3, arrival: 4, burst: 1 },
  { pid: 4, arrival: 5, burst: 4 },
];

console.table(sjfScheduling(processes));
```

Expected table:

| PID | Arrival | Burst | Completion | Turnaround | Waiting |
| --- | ------- | ----- | ---------- | ---------- | ------- |
| 1   | 0       | 7     | 7          | 7          | 0       |
| 2   | 2       | 4     | 12         | 10         | 6       |
| 3   | 4       | 1     | 8          | 4          | 3       |
| 4   | 5       | 4     | 16         | 11         | 7       |

---

### ⏱ Time & Space Complexity

| Metric   | Complexity                             |
| -------- | -------------------------------------- |
| ⏳ Time  | O(n²) – Each process checks all others |
| 💾 Space | O(n) – For tracking results            |

---

### 📌 Summary

| Term            | Formula                   |
| --------------- | ------------------------- |
| Completion Time | When the process finishes |
| Turnaround Time | Completion - Arrival      |
| Waiting Time    | Turnaround - Burst        |

---

## 🔢 **8. Least Recently Used (LRU) Page Replacement Algorithm**

### 📘 Problem Statement

Given:

- A **page reference string** (array of page requests)
- A fixed number of **page frames** (capacity)

> Implement the **LRU Page Replacement Algorithm**.
> At any point, the **least recently used page** (i.e., the one not used for the longest time) is replaced when the cache is full.

Return:

- The total number of **page faults**

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (pages = [1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5]), (capacity = 3);
Output: 9;
```

#### ✅ Test Case 2:

```js
Input: (pages = [7, 0, 1, 2, 0, 3, 0, 4]), (capacity = 4);
Output: 6;
```

#### ✅ Test Case 3:

```js
Input: (pages = [1, 2, 3, 4, 1, 2, 5, 6]), (capacity = 4);
Output: 6;
```

---

### 🧠 Intuition

We want to simulate a **cache of fixed size**.

- If the page is in the cache → it's a **hit**.
- If not → **page fault**, add to cache.
- If the cache is full → **evict the least recently used** (i.e., the oldest accessed).

To do this efficiently:

- Use a `Map` or `LinkedHashMap` that maintains **insertion order or access order**.
- Or simulate using a **Set + Queue** or **Doubly Linked List + HashMap**.

---

### 🔄 Dry Run

```plaintext
Pages = [1, 2, 3, 4, 1, 2, 5], Capacity = 3

Step-by-step:
- 1 → fault → [1]
- 2 → fault → [1, 2]
- 3 → fault → [1, 2, 3]
- 4 → fault, evict 1 → [2, 3, 4]
- 1 → fault, evict 2 → [3, 4, 1]
- 2 → fault, evict 3 → [4, 1, 2]
- 5 → fault, evict 4 → [1, 2, 5]

✅ Total faults = 7
```

---

### ✅ JavaScript Code (Using `Map` for LRU)

```js
function lruPageFaults(pages, capacity) {
  let pageFaults = 0;
  const cache = new Map();

  for (let page of pages) {
    if (cache.has(page)) {
      // Move page to end to show it was recently used
      cache.delete(page);
    } else {
      pageFaults++;
      if (cache.size === capacity) {
        // Delete least recently used (first item in Map)
        const lru = cache.keys().next().value;
        cache.delete(lru);
      }
    }
    cache.set(page, true); // Add or update
  }

  return pageFaults;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity                                      |
| -------- | ----------------------------------------------- |
| ⏳ Time  | O(n) – each page insert/delete is O(1) in `Map` |
| 💾 Space | O(capacity) – storing cache                     |

---

### 📌 Summary

| Concept    | Description                                |
| ---------- | ------------------------------------------ |
| LRU        | Remove least recently accessed page        |
| Cache      | Track using `Map`, `Queue`, or Linked List |
| Page Fault | When a page is not in the current cache    |

---

## 🔢 **9. Insert Interval**

### 📘 Problem Statement

You are given a list of **non-overlapping**, sorted intervals `[start, end]`, and a new interval to insert.

> Insert the new interval into the list such that the resulting list is **also sorted** and has **no overlapping intervals**.

Return the updated list of merged intervals.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (intervals = [
  [1, 3],
  [6, 9],
]),
  (newInterval = [2, 5]);
Output: [
  [1, 5],
  [6, 9],
];
```

#### ✅ Test Case 2:

```js
Input: (intervals = [
  [1, 2],
  [3, 5],
  [6, 7],
  [8, 10],
  [12, 16],
]),
  (newInterval = [4, 8]);
Output: [
  [1, 2],
  [3, 10],
  [12, 16],
];
```

#### ✅ Test Case 3:

```js
Input: (intervals = []), (newInterval = [5, 7]);
Output: [[5, 7]];
```

#### ✅ Test Case 4:

```js
Input: (intervals = [[1, 5]]), (newInterval = [0, 0]);
Output: [
  [0, 0],
  [1, 5],
];
```

---

### 🧠 Intuition

We iterate through the `intervals`:

- **Before Overlap**: Add all intervals that end before the new interval starts.
- **Overlap**: Merge overlapping intervals with the new one.
- **After Overlap**: Add remaining intervals after merging.

---

### 🔄 Dry Run

```plaintext
intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], new = [4,8]

1. [1,2] → ends before new starts → add
2. [3,5] overlaps → merge to [3,8]
3. [6,7] overlaps → merge to [3,8]
4. [8,10] overlaps → merge to [3,10]
5. [12,16] after → add

Result = [[1,2], [3,10], [12,16]]
```

---

### ✅ JavaScript Code

```js
function insertInterval(intervals, newInterval) {
  const result = [];
  let i = 0;
  const n = intervals.length;

  // 1. Add intervals before overlap
  while (i < n && intervals[i][1] < newInterval[0]) {
    result.push(intervals[i]);
    i++;
  }

  // 2. Merge overlapping intervals
  while (i < n && intervals[i][0] <= newInterval[1]) {
    newInterval[0] = Math.min(newInterval[0], intervals[i][0]);
    newInterval[1] = Math.max(newInterval[1], intervals[i][1]);
    i++;
  }
  result.push(newInterval);

  // 3. Add remaining intervals
  while (i < n) {
    result.push(intervals[i]);
    i++;
  }

  return result;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity             |
| -------- | ---------------------- |
| ⏳ Time  | O(n) – one full pass   |
| 💾 Space | O(n) – to store result |

---

### 📌 Summary

| Step             | Action                        |
| ---------------- | ----------------------------- |
| Before overlap   | Directly add to result        |
| Overlapping area | Merge with new interval       |
| After overlap    | Add remaining intervals as-is |

---

## 🔢 **10. Merge Intervals**

### 📘 Problem Statement

You are given an array of intervals where each interval is represented as `[start, end]`.

> Merge all **overlapping intervals** and return an array of the merged intervals, sorted by the start time.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: intervals = [
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

#### ✅ Test Case 2:

```js
Input: intervals = [
  [1, 4],
  [4, 5],
];
Output: [[1, 5]];
```

#### ✅ Test Case 3:

```js
Input: intervals = [
  [1, 10],
  [2, 3],
  [4, 5],
  [6, 7],
];
Output: [[1, 10]];
```

#### ✅ Test Case 4:

```js
Input: intervals = [
  [5, 7],
  [1, 3],
];
Output: [
  [1, 3],
  [5, 7],
];
```

---

### 🧠 Intuition

- First, sort all intervals based on **start time**.
- Then **merge overlapping intervals** by:

  - Comparing current interval with the **last interval in the result list**
  - If overlapping → **merge** (`end = max(end1, end2)`)
  - Else → add as a new interval

---

### 🔄 Dry Run

```plaintext
Input: [[1,3],[2,6],[8,10],[15,18]]

Sort → [[1,3],[2,6],[8,10],[15,18]]

Start:
- Add [1,3] to result
- [2,6] overlaps with [1,3] → merge → [1,6]
- [8,10] → no overlap → add
- [15,18] → no overlap → add

✅ Output: [[1,6],[8,10],[15,18]]
```

---

### ✅ JavaScript Code

```js
function mergeIntervals(intervals) {
  if (intervals.length <= 1) return intervals;

  // Step 1: Sort by start time
  intervals.sort((a, b) => a[0] - b[0]);

  const merged = [intervals[0]];

  for (let i = 1; i < intervals.length; i++) {
    const last = merged[merged.length - 1];
    const curr = intervals[i];

    if (curr[0] <= last[1]) {
      // Overlapping intervals → merge
      last[1] = Math.max(last[1], curr[1]);
    } else {
      // No overlap → add to result
      merged.push(curr);
    }
  }

  return merged;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity                |
| -------- | ------------------------- |
| ⏳ Time  | O(n log n) – for sorting  |
| 💾 Space | O(n) – for storing result |

---

### 📌 Summary

| Step        | Action                          |
| ----------- | ------------------------------- |
| 1. Sort     | Based on start times            |
| 2. Traverse | Merge overlapping intervals     |
| 3. Result   | Return list of merged intervals |

---

## 🔢 **11. Non-overlapping Intervals**

### 📘 Problem Statement

You are given an array of `intervals`, where each interval is `[start, end]`.

> Find the **minimum number of intervals you need to remove** to make the rest **non-overlapping**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: intervals = [
  [1, 2],
  [2, 3],
  [3, 4],
  [1, 3],
];
Output: 1;
// Remove [1,3]
```

#### ✅ Test Case 2:

```js
Input: intervals = [
  [1, 2],
  [1, 2],
  [1, 2],
];
Output: 2;
// Remove 2 intervals to leave 1 non-overlapping
```

#### ✅ Test Case 3:

```js
Input: intervals = [
  [1, 2],
  [2, 3],
];
Output: 0;
// Already non-overlapping
```

#### ✅ Test Case 4:

```js
Input: intervals = [
  [1, 100],
  [11, 22],
  [1, 11],
  [2, 12],
];
Output: 2;
```

---

### 🧠 Intuition

This is the **inverse of activity selection**:

- Instead of selecting the **maximum number of non-overlapping intervals**, we want to **remove the minimum number of overlapping intervals**.

### ✅ Greedy Insight:

- **Always pick intervals with the earliest end time** to leave more space for upcoming intervals.
- Count how many we can **keep**, then subtract from the total to get how many to **remove**.

---

### 🔄 Dry Run

```plaintext
intervals = [[1,2],[2,3],[3,4],[1,3]]
Sort by end → [[1,2],[1,3],[2,3],[3,4]]

Start with prevEnd = -∞

1. [1,2] → non-overlapping → keep, prevEnd = 2
2. [1,3] → 1 < 2 → overlapping → skip
3. [2,3] → 2 >= 2 → non-overlapping → keep, prevEnd = 3
4. [3,4] → 3 >= 3 → non-overlapping → keep, prevEnd = 4

Kept = 3 → Remove = 4 - 3 = 1 ✅
```

---

### ✅ JavaScript Code (Greedy Approach)

```js
function eraseOverlapIntervals(intervals) {
  if (intervals.length <= 1) return 0;

  // Step 1: Sort by end time
  intervals.sort((a, b) => a[1] - b[1]);

  let count = 1; // first interval is always selected
  let prevEnd = intervals[0][1];

  for (let i = 1; i < intervals.length; i++) {
    if (intervals[i][0] >= prevEnd) {
      count++;
      prevEnd = intervals[i][1];
    }
  }

  return intervals.length - count;
}
```

---

### ⏱ Time & Space Complexity

| Metric   | Complexity            |
| -------- | --------------------- |
| ⏳ Time  | O(n log n) – sorting  |
| 💾 Space | O(1) – constant space |

---

### 📌 Summary

| Step     | Action                           |
| -------- | -------------------------------- |
| Sort     | By interval end time             |
| Traverse | Count non-overlapping intervals  |
| Result   | Total - Count = Minimum removals |

---
