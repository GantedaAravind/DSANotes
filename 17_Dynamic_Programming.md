# 🧠 **Dynamic Programming (DP)**

## 📌 **What is Dynamic Programming?**

Dynamic Programming is an algorithmic technique used for **solving problems with overlapping subproblems and optimal substructure** by **storing intermediate results** to avoid redundant work.

> 💡 It is mainly used to **optimize recursive solutions** and is ideal for problems involving **combinatorics**, **optimization**, and **decision-making**.

---

## 🧱 **Key Properties of DP**

1. ### **Overlapping Subproblems**

   - The problems where smaller subproblems can solved several times.
   - Example: In Fibonacci, `fib(5)` calls `fib(4)` and `fib(3)`, and so does `fib(4)` again.

2. ### **Optimal Substructure**

   - The solution to the main problem can be built from the **optimal solutions** of its subproblems.
   - Example: Shortest path from A to C via B can be found if we know the shortest paths from A to B and B to C.

## 🛠️ **Approaches to Solve DP Problems**

### 1. **Top-Down Approach (Memoization)**

- Use recursion and store results in a table (usually a map or array).
- Avoid recomputation of the same inputs.

```js
// Fibonacci using Top-Down
function fib(n, memo = {}) {
  if (n <= 1) return n;
  if (memo[n]) return memo[n];
  return (memo[n] = fib(n - 1, memo) + fib(n - 2, memo));
}
```

### 2. **Bottom-Up Approach (Tabulation)**

- Solve smaller subproblems first and build the solution iteratively.

```js
// Fibonacci using Bottom-Up
function fib(n) {
  let dp = [0, 1];
  for (let i = 2; i <= n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
  }
  return dp[n];
}
```

## 🛑 **When NOT to Use DP**

- When subproblems are **not overlapping**.
- When the problem can be solved greedily or via divide & conquer **without recomputation**.

---

## 🔢 **Fibonacci Number**

### 📘 Problem Statement

Given a number `n`, return the **n-th Fibonacci number**, where:

- F(0) = 0
- F(1) = 1
- F(n) = F(n-1) + F(n-2), for n ≥ 2

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: n = 0
Output: 0
```

#### ✅ Test Case 2:

```txt
Input: n = 1
Output: 1
```

#### ✅ Test Case 3:

```txt
Input: n = 5
Output: 5
Explanation: Fib series = 0, 1, 1, 2, 3, **5**
```

#### ✅ Test Case 4:

```txt
Input: n = 10
Output: 55
Explanation: Fib series = 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, **55**
```

---

---

### 🚀 Approach 1: Naive Recursion

#### 🧠 Intuition

This approach **directly follows** the recurrence relation. It tries all possibilities.
But it ends up **recomputing the same things over and over**.

#### 📘 Code

```js
function fib(n) {
  if (n <= 1) return n;
  return fib(n - 1) + fib(n - 2);
}
```

---

#### 🔍 Dry Run: `fib(4)`

```
fib(4)
├── fib(3)
│   ├── fib(2)
│   │   ├── fib(1) → 1
│   │   └── fib(0) → 0
│   └── fib(1) → 1
├── fib(2)
│   ├── fib(1) → 1
│   └── fib(0) → 0
```

You can see `fib(2)` and `fib(1)` are repeated multiple times.

---

#### ❌ Problems

- **Very slow** for large `n`
- **Exponential time** due to repeated calls

---

#### ⏱ Complexity

- **Time**: O(2^n)
- **Space**: O(n) (recursion stack)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Intuition

We still use recursion, but **cache the results** of subproblems.

Before computing `fib(n)`, we check if it’s already been solved. If yes, return it.

---

#### 📘 Code

```js
function fib(n, memo = {}) {
  if (n <= 1) return n;
  if (memo[n] !== undefined) return memo[n]; // check cache
  memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
  return memo[n];
}
```

---

#### 🔍 Dry Run: `fib(5)`

```
fib(5)
→ fib(4) + fib(3)
→ [fib(3) + fib(2)] + [fib(2) + fib(1)]
→ [fib(2) + fib(1)] + [fib(1) + fib(0)]
→ all base cases hit
→ results stored:
  memo[2] = 1
  memo[3] = 2
  memo[4] = 3
  memo[5] = 5
```

So, each value is calculated **only once**.

---

#### ⏱ Complexity

- **Time**: O(n) ✅
- **Space**: O(n) (memo + recursion stack)

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

We **eliminate recursion**.
We start from base cases (0 and 1), then use a **loop** to build the answer from the bottom.

---

#### 📘 Code

```js
function fib(n) {
  if (n <= 1) return n;
  const dp = new Array(n + 1).fill(0);
  dp[1] = 1;
  for (let i = 2; i <= n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
  }
  return dp[n];
}
```

---

#### 🔍 Dry Run for `n = 5`

```
dp[0] = 0
dp[1] = 1

i = 2 → dp[2] = 1
i = 3 → dp[3] = 2
i = 4 → dp[4] = 3
i = 5 → dp[5] = 5
```

Answer is `dp[5] = 5`

---

#### ⏱ Complexity

- **Time**: O(n) ✅
- **Space**: O(n) (dp array)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

We realize that we only ever use the **last two values** (`F(n-1)` and `F(n-2)`), so we don’t need the whole array.

Just **keep two variables** and update them in every loop.

---

#### 📘 Code

```js
function fib(n) {
  if (n <= 1) return n;
  let prev1 = 0,
    prev2 = 1;
  for (let i = 2; i <= n; i++) {
    const curr = prev1 + prev2;
    prev1 = prev2;
    prev2 = curr;
  }
  return prev2;
}
```

---

#### 🔍 Dry Run for `n = 5`

```
prev1 = 0, prev2 = 1
i = 2 → curr = 1 → prev1 = 1, prev2 = 1
i = 3 → curr = 2 → prev1 = 1, prev2 = 2
i = 4 → curr = 3 → prev1 = 2, prev2 = 3
i = 5 → curr = 5 → prev1 = 3, prev2 = 5
```

Answer is `5`

---

#### ⏱ Complexity

- **Time**: O(n) ✅
- **Space**: O(1) ✅ (Best approach)

---

### 📌 Summary Table

| Approach            | Time   | Space   | Notes                       |
| ------------------- | ------ | ------- | --------------------------- |
| Naive Recursion     | O(2^n) | O(n)    | Too slow for large `n`      |
| Memoization (Top)   | O(n)   | O(n)    | Stores intermediate results |
| Tabulation (Bottom) | O(n)   | O(n)    | Iterative + Easy to debug   |
| Space Optimization  | O(n)   | O(1) ✅ | Best in both time & space   |

---

Sure! Here's a complete **note-style explanation** on the **time complexity of the recursive Fibonacci algorithm using recursion tree analysis**:

---

## 📘 Fibonacci Recursive Time Complexity — Notes

## ✅ 1. Problem Definition

The classic recursive Fibonacci function:

```js
function fib(n) {
  if (n <= 1) return n;
  return fib(n - 1) + fib(n - 2);
}
```

---

## 🔁 2. Recursive Formula

```
fib(n) = fib(n - 1) + fib(n - 2)
Base cases: fib(0) = 0, fib(1) = 1
```

---

## 🌳 3. Recursion Tree Structure

Each `fib(n)` calls:

- `fib(n - 1)`
- `fib(n - 2)`

Each of these again makes **2 recursive calls**, and so on.

So, the recursive calls form a **binary tree** structure:

- Every non-base node has **2 children**
- The tree grows until `n = 0` or `n = 1`

Example for `fib(4)`:

```
              fib(4)
             /     \
        fib(3)     fib(2)
       /     \     /     \
   fib(2)  fib(1) fib(1) fib(0)
   /    \
fib(1) fib(0)
```

Total function calls = **number of nodes = 9**

---

## ⏱️ 4. Why Time Complexity = Number of Nodes?

- Each recursive call (node) does **constant work** (base check + add).
- So **total time** is proportional to the **number of calls**.
- ➤ **Each call = one node in recursion tree**
- ➤ **Total time = O(number of nodes)**

---

## 📈 5. Total Nodes in Tree ≈ O(2ⁿ)

- Recursion tree is approximately a **full binary tree** of height `n`
- A full binary tree with height `n` has ≈ `2ⁿ` nodes
- Therefore:

```
T(n) ≈ 2ⁿ  → Time complexity = O(2ⁿ)
```

---

## 📦 6. Time & Space Complexity

| Complexity Type  | Value | Reason                                |
| ---------------- | ----- | ------------------------------------- |
| Time Complexity  | O(2ⁿ) | Exponential number of recursive calls |
| Space Complexity | O(n)  | Max depth of recursion stack          |

---

## 🧠 7. Why This Is Inefficient

- Many **repeated subproblems** (e.g., `fib(2)`, `fib(1)` appear many times)
- Wasted computation → makes recursion slow

---

## 🚀 8. Optimized Alternatives

| Method                 | Time Complexity | Space Complexity |
| ---------------------- | --------------- | ---------------- |
| Memoization (Top-down) | O(n)            | O(n)             |
| Tabulation (Bottom-up) | O(n)            | O(1)             |
| Matrix Exponentiation  | O(log n)        | O(1)             |

---

## **Determine the time complexity of any recursion**

### 🔁 1. **Write the Recurrence Relation**

If a function calls itself recursively, figure out:

- How many times it calls itself
- How the input size reduces
- Any additional work done outside the recursion

👉 **Example:**

```js
function fact(n) {
  if (n == 0) return 1;
  return n * fact(n - 1);
}
```

This does **one recursive call**, reducing `n` by 1 →
**Recurrence:** T(n) = T(n - 1) + O(1)
➡️ **Time Complexity:** O(n)

---

### 🔁 2. **Use Recursion Tree Method**

Break down the recursive calls level by level like a tree, and sum all work.

👉 **Example:**

```js
function fib(n) {
  if (n <= 1) return n;
  return fib(n - 1) + fib(n - 2);
}
```

Here, each call makes **2 calls**, so it's a binary tree of height `n`.

➡️ Total nodes ≈ 2ⁿ
➡️ **Time Complexity:** O(2ⁿ) (exponential)

---

### 🧮 3. **Master Theorem** (for Divide & Conquer)

Use when recursion is of the form:
**T(n) = aT(n/b) + O(n^d)**

- `a` = number of recursive calls
- `n/b` = size of each subproblem
- `O(n^d)` = work done outside recursion

👉 **Example (Merge Sort):**

```js
T(n) = 2T(n/2) + O(n)
```

➡️ `a = 2`, `b = 2`, `d = 1`
➡️ **Time Complexity:** O(n log n)

---

### 📌 4. **Memoization/DP? Then it’s Subproblem Count × Work per Subproblem**

👉 **Example:**

```js
function fib(n, dp) {
  if (n <= 1) return n;
  if (dp[n] != -1) return dp[n];
  return (dp[n] = fib(n - 1, dp) + fib(n - 2, dp));
}
```

There are **O(n)** subproblems and each solved in O(1) due to memoization
➡️ **Time Complexity:** O(n)

---

# 1D Dp

## 🔢 **1. Climbing Stairs**

### 📘 Problem Statement

You are climbing a staircase. It takes `n` steps to reach the top. Each time, you can either **climb 1 or 2 steps**.

Return the number of **distinct ways** you can climb to the top.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: n = 1
Output: 1
Explanation: Only 1 way → [1]
```

#### ✅ Test Case 2:

```txt
Input: n = 2
Output: 2
Explanation: Two ways → [1+1], [2]
```

#### ✅ Test Case 3:

```txt
Input: n = 3
Output: 3
Explanation: [1+1+1], [1+2], [2+1]
```

#### ✅ Test Case 4:

```txt
Input: n = 5
Output: 8
Explanation: 8 different ways to climb 5 steps using 1 and 2 steps
```

---

### 🚀 Approach 1: Naive Recursion

#### 🧠 Intuition

This problem follows the **same recurrence as Fibonacci**:

- To reach step `n`, you either:
  - Came from step `n-1` (1 step up), or
  - Came from step `n-2` (2 steps up)
- So: `ways(n) = ways(n-1) + ways(n-2)`

#### 📘 Code

```js
function climbStairs(n) {
  if (n <= 1) return 1;
  return climbStairs(n - 1) + climbStairs(n - 2);
}
```

---

#### 🔍 Dry Run: `climbStairs(4)`

```
climbStairs(4)
├── climbStairs(3)
│   ├── climbStairs(2)
│   │   ├── climbStairs(1) → 1
│   │   └── climbStairs(0) → 1
│   └── climbStairs(1) → 1
├── climbStairs(2) → already calculated
```

---

#### ❌ Problems

- Recomputes subproblems many times
- **Very slow for large `n`**

#### ⏱ Complexity

- **Time**: O(2^n)
- **Space**: O(n) (recursive stack)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Intuition

Store the result of each subproblem to avoid recalculating it.

#### 📘 Code

```js
function climbStairs(n, memo = {}) {
  if (n <= 1) return 1;
  if (memo[n] !== undefined) return memo[n];
  memo[n] = climbStairs(n - 1, memo) + climbStairs(n - 2, memo);
  return memo[n];
}
```

---

#### 🔍 Dry Run: `climbStairs(4)`

```
→ climbStairs(3) + climbStairs(2)
→ climbStairs(2) + climbStairs(1)
→ climbStairs(1) + climbStairs(0)
→ memo filled: {2: 2, 3: 3, 4: 5}
```

---

#### ⏱ Complexity

- **Time**: O(n)
- **Space**: O(n) (memo + call stack)

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Start from base cases and **build up** using a loop.

#### 📘 Code

```js
function climbStairs(n) {
  if (n <= 1) return 1;
  const dp = new Array(n + 1).fill(0);
  dp[0] = dp[1] = 1;
  for (let i = 2; i <= n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
  }
  return dp[n];
}
```

---

#### 🔍 Dry Run: `n = 4`

```
dp[0] = 1
dp[1] = 1
dp[2] = 2
dp[3] = 3
dp[4] = 5
```

---

#### ⏱ Complexity

- **Time**: O(n)
- **Space**: O(n)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

Only the last two results are needed → use two variables.

#### 📘 Code

```js
function climbStairs(n) {
  if (n <= 1) return 1;
  let prev1 = 1,
    prev2 = 1;
  for (let i = 2; i <= n; i++) {
    const curr = prev1 + prev2;
    prev1 = prev2;
    prev2 = curr;
  }
  return prev2;
}
```

---

#### 🔍 Dry Run: `n = 4`

```
prev1 = 1, prev2 = 1
i = 2 → curr = 2 → prev1 = 1, prev2 = 2
i = 3 → curr = 3 → prev1 = 2, prev2 = 3
i = 4 → curr = 5 → prev1 = 3, prev2 = 5
```

---

#### ⏱ Complexity

- **Time**: O(n)
- **Space**: O(1) ✅

---

### 📌 Summary Table

| Approach           | Time   | Space   | Notes                |
| ------------------ | ------ | ------- | -------------------- |
| Naive Recursion    | O(2^n) | O(n)    | Exponential and slow |
| Memoization        | O(n)   | O(n)    | Fast, top-down       |
| Tabulation         | O(n)   | O(n)    | Iterative and clean  |
| Space Optimization | O(n)   | O(1) ✅ | Most efficient       |

---

## 🔢 **2. Frog Jump (1 Step or 2 Step)**

### 📘 Problem Statement

A frog is at the 0th stair. There are `n` stairs, and the frog wants to reach the `n`th stair.

The frog can jump **either 1 or 2 steps** at a time. The cost of each stair is given in an array `height[]`, where `height[i]` represents the height of the `i-th` stair.

The **energy cost** for a jump from stair `i` to `j` is:

```
abs(height[i] - height[j])
```

Find the **minimum total energy** required to reach the last stair (i.e., index `n - 1`).

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: height = [10, 20]
Output: 10
Explanation: Jump from 0 → 1, cost = |10 - 20| = 10
```

#### ✅ Test Case 2:

```txt
Input: height = [10, 20, 10]
Output: 0
Explanation: Jump from 0 → 2, cost = |10 - 10| = 0
```

#### ✅ Test Case 3:

```txt
Input: height = [30, 10, 60, 10, 60, 50]
Output: 40
Explanation: Path = 0 → 1 → 3 → 5
Cost = 20 + 0 + 40 = 60 OR
Path = 0 → 2 → 3 → 5
Cost = 30 + 50 + 40 = 120 → So best is 0 → 1 → 3 → 5 = 40
```

---

### 🚀 Approach 1: Naive Recursion

#### 🧠 Intuition

From stair `i`, the frog can jump to:

- `i - 1` (cost: `|height[i] - height[i - 1]|`)
- `i - 2` (cost: `|height[i] - height[i - 2]|`)

We try both paths recursively and return the **minimum**.

---

#### 📘 Code

```js
function frogJump(n, height) {
  if (n === 0) return 0;
  let left = frogJump(n - 1, height) + Math.abs(height[n] - height[n - 1]);
  let right = Infinity;
  if (n > 1) {
    right = frogJump(n - 2, height) + Math.abs(height[n] - height[n - 2]);
  }
  return Math.min(left, right);
}
```

---

#### 🔍 Dry Run: `height = [10, 30, 40]`

```
frogJump(2)
├── frogJump(1) + |40 - 30| = ?
│   └── frogJump(0) + |30 - 10| = 20
│   → 20 + 10 = 30
├── frogJump(0) + |40 - 10| = 30
→ min(30, 30) = 30
```

---

#### ❌ Problems

- Overlapping subproblems
- Recomputes same states

---

#### ⏱ Complexity

- **Time**: O(2^n)
- **Space**: O(n) (recursion depth)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Intuition

Store answers to subproblems in a `dp[]` array to avoid recomputation.

---

#### 📘 Code

```js
function frogJump(n, height, dp = []) {
  if (n === 0) return 0;
  if (dp[n] !== undefined) return dp[n];

  let left = frogJump(n - 1, height, dp) + Math.abs(height[n] - height[n - 1]);
  let right = Infinity;
  if (n > 1) {
    right = frogJump(n - 2, height, dp) + Math.abs(height[n] - height[n - 2]);
  }

  return (dp[n] = Math.min(left, right));
}
```

---

#### 🔍 Dry Run: `height = [10, 30, 40, 20]`

```
dp = [0, undefined, undefined, undefined]
→ frogJump(3)
   → frogJump(2)
      → frogJump(1)
         → frogJump(0)
→ results memoized: dp[1]=20, dp[2]=30, dp[3]=30
```

---

#### ⏱ Complexity

- **Time**: O(n)
- **Space**: O(n) (dp + recursion stack)

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Build the solution from base cases `0` and `1` step by step.

---

#### 📘 Code

```js
function frogJump(n, height) {
  const dp = new Array(n).fill(0);
  dp[0] = 0;

  for (let i = 1; i < n; i++) {
    let left = dp[i - 1] + Math.abs(height[i] - height[i - 1]);
    let right =
      i > 1 ? dp[i - 2] + Math.abs(height[i] - height[i - 2]) : Infinity;
    dp[i] = Math.min(left, right);
  }

  return dp[n - 1];
}
```

---

#### 🔍 Dry Run: `height = [10, 20, 10]`

```
dp[0] = 0
i = 1 → dp[1] = |20 - 10| = 10
i = 2 → dp[2] = min(|10 - 20| + 10, |10 - 10| + 0) = min(20, 0) = 0
```

---

#### ⏱ Complexity

- **Time**: O(n)
- **Space**: O(n)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

Only last 2 values are required → use two variables.

---

#### 📘 Code

```js
function frogJump(n, height) {
  let prev1 = 0,
    prev2 = 0;
  for (let i = 1; i < n; i++) {
    let oneStep = prev1 + Math.abs(height[i] - height[i - 1]);
    let twoStep =
      i > 1 ? prev2 + Math.abs(height[i] - height[i - 2]) : Infinity;
    let curr = Math.min(oneStep, twoStep);
    prev2 = prev1;
    prev1 = curr;
  }
  return prev1;
}
```

---

#### 🔍 Dry Run: `height = [10, 30, 40, 20]`

```
i = 1 → curr = |30 - 10| = 20
i = 2 → min(20 + |40 - 30|, 0 + |40 - 10|) = min(30, 30) = 30
i = 3 → min(30 + |20 - 40|, 20 + |20 - 30|) = min(50, 30) = 30
```

---

#### ⏱ Complexity

- **Time**: O(n)
- **Space**: O(1) ✅

---

### 📌 Summary Table

| Approach           | Time   | Space   | Notes                         |
| ------------------ | ------ | ------- | ----------------------------- |
| Naive Recursion    | O(2^n) | O(n)    | Exponential, impractical      |
| Memoization        | O(n)   | O(n)    | Avoids recomputation          |
| Tabulation         | O(n)   | O(n)    | Iterative, easy to debug      |
| Space Optimization | O(n)   | O(1) ✅ | Best space-efficient approach |

---

## 🔢 **3. Frog Jump with K Distance**

### 📘 Problem Statement

A frog is at the 0th stair and wants to reach the `(n-1)`th stair. The frog can jump from stair `i` to any stair in the range `i+1` to `i+k`.

The cost to jump from stair `i` to stair `j` is:

```
abs(height[i] - height[j])
```

Return the **minimum total cost** to reach the last stair.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: height = [10, 30, 40, 50, 20], k = 3
Output: 30
Explanation: 0 → 1 → 4 → Cost = 20 + 10 = 30 ✅
```

#### ✅ Test Case 2:

```txt
Input: height = [10, 20, 10], k = 2
Output: 0
Explanation: 0 → 2 → Cost = 0 ✅
```

#### ✅ Test Case 3:

```txt
Input: height = [40, 10, 20, 70, 80, 10], k = 4
Output: 30
```

---

### ✅ Approach 1: Naive Recursion (No Memoization)

#### 🧠 Intuition

Try all possible jump paths recursively. From stair `n`, the frog can come from `n-1`, `n-2`, ..., `n-k`. Recursively compute the cost for all valid jumps.

#### 📘 Code

```js
function frogJump(n, height, k) {
  if (n === 0) return 0;

  let minCost = Infinity;

  for (let j = 1; j <= k; j++) {
    if (n - j >= 0) {
      let jumpCost =
        frogJump(n - j, height, k) + Math.abs(height[n] - height[n - j]);
      minCost = Math.min(minCost, jumpCost);
    }
  }

  return minCost;
}
```

#### ⏱ Complexity

- **Time**: ❌ O(kⁿ) — exponential time due to recomputation
- **Space**: O(n) — due to recursion stack

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Intuition

Same as the recursive approach, but **store already computed results** in a `dp` array to avoid recomputation.

#### 📘 Code

```js
function frogJump(n, height, k, dp = []) {
  if (n === 0) return 0;
  if (dp[n] !== undefined) return dp[n];

  let minCost = Infinity;

  for (let j = 1; j <= k; j++) {
    if (n - j >= 0) {
      let jumpCost =
        frogJump(n - j, height, k, dp) + Math.abs(height[n] - height[n - j]);
      minCost = Math.min(minCost, jumpCost);
    }
  }

  return (dp[n] = minCost);
}
```

#### 🧪 Call It Like:

```js
frogJump(height.length - 1, height, k);
```

#### ⏱ Complexity

- **Time**: ✅ O(n × k)
- **Space**: O(n) (dp + recursion stack)

---

### ✅ Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Instead of starting from the top and going down recursively, we build the solution **from the base up** using iteration.

#### 📘 Code

```js
function frogJump(n, height, k) {
  const dp = new Array(n).fill(Infinity);
  dp[0] = 0;

  for (let i = 1; i < n; i++) {
    for (let j = 1; j <= k; j++) {
      if (i - j >= 0) {
        let jumpCost = dp[i - j] + Math.abs(height[i] - height[i - j]);
        dp[i] = Math.min(dp[i], jumpCost);
      }
    }
  }

  return dp[n - 1];
}
```

#### ⏱ Complexity

- **Time**: ✅ O(n × k)
- **Space**: O(n)

---

### ✅ Approach 4: Space Optimization

#### 🧠 Intuition

You might think to reduce space by only keeping track of the last `k` computed values instead of the entire `dp` array.

> ⚠️ This works **only if `k` is small and fixed**.

If `k` can be large or variable, **you need the full `dp[]`**, because any of the previous `k` values might be needed.

---

### 🧮 Summary Table

| Approach               | Time Complexity | Space Complexity | Notes                                |
| ---------------------- | --------------- | ---------------- | ------------------------------------ |
| Naive Recursion        | ❌ O(kⁿ)        | O(n)             | Exponential — slow for large `n`     |
| Memoization (Top-Down) | ✅ O(n × k)     | O(n)             | Best for recursion lovers            |
| Tabulation (Bottom-Up) | ✅ O(n × k)     | O(n)             | Best for clarity and performance     |
| Space Optimization     | ⚠️ O(n × k)     | ⚠️ O(n) or less  | Only useful if `k` is small or fixed |

---

## 🔢 **4. Maximum Sum of Non-Adjacent Elements**

### 📘 Problem Statement

You are given an array of integers `arr[]` of length `n`.

Find the **maximum sum** of elements such that **no two chosen elements are adjacent** in the array.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: arr = [2, 1, 4, 9]
Output: 11
Explanation: Pick 2 + 9 = 11
```

#### ✅ Test Case 2:

```txt
Input: arr = [3, 2, 7, 10]
Output: 13
Explanation: Pick 3 + 10 = 13
```

#### ✅ Test Case 3:

```txt
Input: arr = [5, 5, 10, 100, 10, 5]
Output: 110
Explanation: Pick 5 + 100 + 5 = 110
```

#### ✅ Test Case 4:

```txt
Input: arr = [1]
Output: 1
```

#### ✅ Test Case 5:

```txt
Input: arr = [0, 0, 0, 0]
Output: 0
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

At index `i`, we have **two choices**:

- **Pick** the current element → move to `i - 2`
- **Not pick** it → move to `i - 1`

Take the max of both options.

---

#### 📘 Code

```js
function solve(i, arr) {
  if (i === 0) return arr[0];
  if (i < 0) return 0;

  let pick = arr[i] + solve(i - 2, arr);
  let notPick = solve(i - 1, arr);

  return Math.max(pick, notPick);
}

function maxSum(arr) {
  return solve(arr.length - 1, arr);
}
```

---

#### 🔍 Dry Run: `arr = [3, 2, 5]`

```
solve(2)
├── pick = 5 + solve(0) = 5 + 3 = 8
├── notPick = solve(1)
     ├── pick = 2 + solve(-1) = 2 + 0 = 2
     └── notPick = solve(0) = 3
     → max(2, 3) = 3
→ max(8, 3) = 8 ✅
```

---

#### ❌ Problems

- Recomputes subproblems
- Exponential time

#### ⏱ Complexity

- **Time**: O(2^n)
- **Space**: O(n) (recursion stack)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Intuition

Same recursive logic, but store results of subproblems in `dp[]`.

---

#### 📘 Code

```js
function solve(i, arr, dp) {
  if (i === 0) return arr[0];
  if (i < 0) return 0;
  if (dp[i] !== -1) return dp[i];

  let pick = arr[i] + solve(i - 2, arr, dp);
  let notPick = solve(i - 1, arr, dp);

  return (dp[i] = Math.max(pick, notPick));
}

function maxSum(arr) {
  const dp = new Array(arr.length).fill(-1);
  return solve(arr.length - 1, arr, dp);
}
```

---

#### 🔍 Dry Run: `arr = [3, 2, 5]`

```
dp = [-1, -1, -1]
solve(2)
→ calls solve(0) and solve(1), fills dp[0], dp[1], then dp[2]
```

---

#### ⏱ Complexity

- **Time**: O(n)
- **Space**: O(n) (dp + recursion stack)

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Iteratively build the `dp[]` array from base cases.

---

#### 📘 Code

```js
function maxSum(arr) {
  const n = arr.length;
  if (n === 0) return 0;
  if (n === 1) return arr[0];

  const dp = new Array(n);
  dp[0] = arr[0];
  dp[1] = Math.max(arr[0], arr[1]);

  for (let i = 2; i < n; i++) {
    let pick = arr[i] + dp[i - 2];
    let notPick = dp[i - 1];
    dp[i] = Math.max(pick, notPick);
  }

  return dp[n - 1];
}
```

---

#### 🔍 Dry Run: `arr = [3, 2, 7, 10]`

```
dp[0] = 3
dp[1] = max(3, 2) = 3
i = 2 → dp[2] = max(3 + 7, 3) = 10
i = 3 → dp[3] = max(3 + 10, 10) = 13
```

---

#### ⏱ Complexity

- **Time**: O(n)
- **Space**: O(n)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

We only need the last two states → use two variables instead of full dp array.

---

#### 📘 Code

```js
function maxSum(arr) {
  const n = arr.length;
  if (n === 0) return 0;
  if (n === 1) return arr[0];

  let prev1 = arr[0];
  let prev2 = Math.max(arr[0], arr[1]);

  for (let i = 2; i < n; i++) {
    const pick = arr[i] + prev1;
    const notPick = prev2;
    const curr = Math.max(pick, notPick);
    prev1 = prev2;
    prev2 = curr;
  }

  return prev2;
}
```

---

#### 🔍 Dry Run: `arr = [3, 2, 7, 10]`

```
prev1 = 3
prev2 = max(3, 2) = 3

i = 2 → curr = max(7 + 3, 3) = 10 → prev1 = 3, prev2 = 10
i = 3 → curr = max(10 + 3, 10) = 13 → prev1 = 10, prev2 = 13
```

---

#### ⏱ Complexity

- **Time**: O(n)
- **Space**: O(1) ✅

---

### 📌 Summary Table

| Approach           | Time   | Space   | Notes                      |
| ------------------ | ------ | ------- | -------------------------- |
| Recursion          | O(2^n) | O(n)    | Brute force                |
| Memoization        | O(n)   | O(n)    | Top-down DP                |
| Tabulation         | O(n)   | O(n)    | Bottom-up DP               |
| Space Optimization | O(n)   | O(1) ✅ | Most optimal and preferred |

---

## 🔢 **5. House Robber (Maximum Non-Adjacent Sum Variant)**

### 📘 Problem Statement

You are given an array `nums[]` where each element represents the **amount of money** at each house. A robber can’t rob **two adjacent houses**.

Return the **maximum amount** of money the robber can rob **without alerting the police** (i.e., robbing two adjacent houses is not allowed).

This is a direct variant of the "Maximum Sum of Non-Adjacent Elements" problem.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: nums = [1, 2, 3, 1]
Output: 4
Explanation: Rob houses 1 and 3 → 1 + 3 = 4
```

#### ✅ Test Case 2:

```txt
Input: nums = [2, 7, 9, 3, 1]
Output: 12
Explanation: Rob houses 1, 3, 5 → 2 + 9 + 1 = 12
```

#### ✅ Test Case 3:

```txt
Input: nums = [0]
Output: 0
```

#### ✅ Test Case 4:

```txt
Input: nums = [4, 1, 2, 9, 1]
Output: 13
Explanation: Rob 1st and 4th = 4 + 9 = 13
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

At each house `i`, you either:

- **Rob it** and go to `i-2`
- **Skip it** and go to `i-1`

Take the max of both.

---

#### 📘 Code

```js
function robRec(i, nums) {
  if (i === 0) return nums[0];
  if (i < 0) return 0;

  let pick = nums[i] + robRec(i - 2, nums);
  let notPick = robRec(i - 1, nums);

  return Math.max(pick, notPick);
}

function rob(nums) {
  return robRec(nums.length - 1, nums);
}
```

---

#### 🔍 Dry Run: `nums = [1, 2, 3]`

```
robRec(2)
├── pick = 3 + robRec(0) = 3 + 1 = 4
├── notPick = robRec(1)
     ├── pick = 2 + robRec(-1) = 2
     └── notPick = robRec(0) = 1
     → max = 2
→ max(4, 2) = 4 ✅
```

---

#### ❌ Problems

- Exponential time due to repeated subproblems

---

#### ⏱ Complexity

- **Time**: O(2^n)
- **Space**: O(n)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Intuition

Use a `dp[]` array to cache already computed values.

---

#### 📘 Code

```js
function robRec(i, nums, dp) {
  if (i === 0) return nums[0];
  if (i < 0) return 0;
  if (dp[i] !== -1) return dp[i];

  let pick = nums[i] + robRec(i - 2, nums, dp);
  let notPick = robRec(i - 1, nums, dp);

  return (dp[i] = Math.max(pick, notPick));
}

function rob(nums) {
  const n = nums.length;
  const dp = new Array(n).fill(-1);
  return robRec(n - 1, nums, dp);
}
```

---

#### 🔍 Dry Run: `nums = [1, 2, 3, 1]`

```
→ robRec(3)
→ Computes robRec(1) and robRec(2), stores in dp[1], dp[2], dp[3]
→ Avoids recomputation
```

---

#### ⏱ Complexity

- **Time**: O(n)
- **Space**: O(n) (dp + recursion stack)

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Build up solution from base cases using a loop.

---

#### 📘 Code

```js
function rob(nums) {
  const n = nums.length;
  if (n === 0) return 0;
  if (n === 1) return nums[0];

  const dp = new Array(n);
  dp[0] = nums[0];
  dp[1] = Math.max(nums[0], nums[1]);

  for (let i = 2; i < n; i++) {
    const pick = nums[i] + dp[i - 2];
    const notPick = dp[i - 1];
    dp[i] = Math.max(pick, notPick);
  }

  return dp[n - 1];
}
```

---

#### 🔍 Dry Run: `nums = [2, 7, 9, 3, 1]`

```
dp[0] = 2
dp[1] = max(2, 7) = 7
dp[2] = max(9 + 2, 7) = 11
dp[3] = max(3 + 7, 11) = 11
dp[4] = max(1 + 11, 11) = 12
→ Answer = dp[4] = 12
```

---

#### ⏱ Complexity

- **Time**: O(n)
- **Space**: O(n)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

We only need two variables (`prev1`, `prev2`) instead of full `dp[]`.

---

#### 📘 Code

```js
function rob(nums) {
  const n = nums.length;
  if (n === 0) return 0;
  if (n === 1) return nums[0];

  let prev1 = nums[0];
  let prev2 = Math.max(nums[0], nums[1]);

  for (let i = 2; i < n; i++) {
    const curr = Math.max(prev2, nums[i] + prev1);
    prev1 = prev2;
    prev2 = curr;
  }

  return prev2;
}
```

---

#### 🔍 Dry Run: `nums = [2, 7, 9, 3, 1]`

```
prev1 = 2
prev2 = max(2, 7) = 7

i = 2 → curr = max(7, 9 + 2) = 11
i = 3 → curr = max(11, 3 + 7) = 11
i = 4 → curr = max(11, 1 + 11) = 12
→ Answer = 12
```

---

#### ⏱ Complexity

- **Time**: O(n)
- **Space**: O(1) ✅

---

### 📌 Summary Table

| Approach           | Time   | Space   | Notes                 |
| ------------------ | ------ | ------- | --------------------- |
| Recursion          | O(2^n) | O(n)    | Brute force, slow     |
| Memoization        | O(n)   | O(n)    | Caches subproblems    |
| Tabulation         | O(n)   | O(n)    | Iterative and clean   |
| Space Optimization | O(n)   | O(1) ✅ | Most optimal approach |

---

# 2D DP

## 🔢 **1. Ninja's Training**

### 📘 Problem Statement

A Ninja is training for `N` days. Each day, he can perform one of **three activities**: Running, Fighting Practice, or Learning New Skills.

Each activity has a certain **point value** for each day, given in a 2D array `points[n][3]`, where:

- `points[i][0]` = points for Running on day `i`
- `points[i][1]` = points for Fighting on day `i`
- `points[i][2]` = points for Learning on day `i`

The constraint: The **Ninja can’t do the same activity on two consecutive days**.

Find the **maximum total points** the Ninja can earn over `N` days.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input:
n = 3
points = [
  [10, 40, 70],  // Day 0
  [20, 50, 80],  // Day 1
  [30, 60, 90]   // Day 2
]
Output: 210
Explanation:
Day 0 → Task 2 (70)
Day 1 → Task 1 (50)
Day 2 → Task 0 (30)
Total = 70 + 50 + 90 = 210 ✅
```

#### ✅ Test Case 2:

```txt
n = 1
points = [[100, 10, 1]]
Output: 100
```

#### ✅ Test Case 3:

```txt
n = 2
points = [[5, 6, 7], [1, 2, 10]]
Output: 17
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

On day `i`, try all tasks (`0, 1, 2`) **except** the task done on day `i - 1`. Try all valid combinations recursively.

---

#### 📘 Code

```js
function ninjaTraining(day, last, points) {
  if (day === 0) {
    let maxPoint = 0;
    for (let task = 0; task < 3; task++) {
      if (task !== last) {
        maxPoint = Math.max(maxPoint, points[0][task]);
      }
    }
    return maxPoint;
  }

  let maxPoint = 0;
  for (let task = 0; task < 3; task++) {
    if (task !== last) {
      const point = points[day][task] + ninjaTraining(day - 1, task, points);
      maxPoint = Math.max(maxPoint, point);
    }
  }

  return maxPoint;
}
```

🧪 Call:

```js
ninjaTraining(n - 1, 3, points);
```

(last = 3 → no previous task constraint)

---

#### ❌ Problems

- Recomputes subproblems
- Exponential time

#### ⏱ Complexity

- **Time**: O(3^n)
- **Space**: O(n)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Intuition

Use `dp[day][lastTask]` to memoize subproblems.

---

#### 📘 Code

```js
function ninjaTraining(n, points) {
  const dp = Array.from({ length: n }, () => Array(4).fill(-1));

  function solve(day, last) {
    if (day === 0) {
      let maxPoint = 0;
      for (let task = 0; task < 3; task++) {
        if (task !== last) {
          maxPoint = Math.max(maxPoint, points[0][task]);
        }
      }
      return maxPoint;
    }

    if (dp[day][last] !== -1) return dp[day][last];

    let maxPoint = 0;
    for (let task = 0; task < 3; task++) {
      if (task !== last) {
        const point = points[day][task] + solve(day - 1, task);
        maxPoint = Math.max(maxPoint, point);
      }
    }

    return (dp[day][last] = maxPoint);
  }

  return solve(n - 1, 3);
}
```

---

#### 🔍 Dry Run:

```
dp[day][last] stores best score for (day, last_task)
→ Avoids recomputation
```

---

#### ⏱ Complexity

- **Time**: O(n × 4 × 3) = O(n)
- **Space**: O(n × 4) + O(n) recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Create a 2D `dp[n][4]` where:

- `dp[day][last]` = max points from day `0..day` with previous task = `last`

---

#### 📘 Code

```js
function ninjaTraining(n, points) {
  const dp = Array.from({ length: n }, () => Array(4).fill(0));

  // Base case (Day 0)
  for (let last = 0; last < 4; last++) {
    let maxPoint = 0;
    for (let task = 0; task < 3; task++) {
      if (task !== last) {
        maxPoint = Math.max(maxPoint, points[0][task]);
      }
    }
    dp[0][last] = maxPoint;
  }

  for (let day = 1; day < n; day++) {
    for (let last = 0; last < 4; last++) {
      dp[day][last] = 0;
      for (let task = 0; task < 3; task++) {
        if (task !== last) {
          let activity = points[day][task] + dp[day - 1][task];
          dp[day][last] = Math.max(dp[day][last], activity);
        }
      }
    }
  }

  return dp[n - 1][3]; // last task can be anything
}
```

---

#### 🔍 Dry Run: For `n = 3`, base case fills:

```
dp[0][0] = max(points[0][1], points[0][2])
dp[0][1] = max(points[0][0], points[0][2])
dp[0][2] = max(points[0][0], points[0][1])
dp[0][3] = max(points[0][0], points[0][1], points[0][2])
```

---

#### ⏱ Complexity

- **Time**: O(n × 4 × 3) = O(n)
- **Space**: O(n × 4)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

Only previous day’s row needed → use 1D `prev[4]` array.

---

#### 📘 Code

```js
function ninjaTraining(n, points) {
  let prev = Array(4).fill(0);

  // Base case (Day 0)
  for (let last = 0; last < 4; last++) {
    let maxPoint = 0;
    for (let task = 0; task < 3; task++) {
      if (task !== last) {
        maxPoint = Math.max(maxPoint, points[0][task]);
      }
    }
    prev[last] = maxPoint;
  }

  for (let day = 1; day < n; day++) {
    const temp = Array(4).fill(0);
    for (let last = 0; last < 4; last++) {
      temp[last] = 0;
      for (let task = 0; task < 3; task++) {
        if (task !== last) {
          const activity = points[day][task] + prev[task];
          temp[last] = Math.max(temp[last], activity);
        }
      }
    }
    prev = temp;
  }

  return prev[3]; // No last task restriction
}
```

---

#### 🔍 Dry Run:

```
prev = stores day-1 results
temp = calculates current day
→ Only 1 array updated each day ✅
```

---

#### ⏱ Complexity

- **Time**: O(n × 4 × 3) = O(n)
- **Space**: O(4) = O(1) ✅

---

### 📌 Summary Table

| Approach           | Time   | Space    | Notes                  |
| ------------------ | ------ | -------- | ---------------------- |
| Recursion          | O(3^n) | O(n)     | Brute-force            |
| Memoization        | O(n)   | O(n × 4) | Top-down DP            |
| Tabulation         | O(n)   | O(n × 4) | Bottom-up DP           |
| Space Optimization | O(n)   | O(1) ✅  | Best optimized version |

---

## 🔢 **2. Grid Unique Paths (DP on Grids)**

### 📘 Problem Statement

You are given a grid of size `m x n`. Starting from the **top-left corner (0,0)**, you need to reach the **bottom-right corner (m-1, n-1)**.

At any point, you can only **move right** or **move down**.

Return the **total number of unique paths** to reach the destination.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: m = 2, n = 2
Output: 2
Explanation: Two paths → Right → Down, or Down → Right
```

#### ✅ Test Case 2:

```txt
Input: m = 3, n = 3
Output: 6
Paths:
→→↓↓, →↓→↓, →↓↓→, ↓→→↓, ↓→↓→, ↓↓→→
```

#### ✅ Test Case 3:

```txt
Input: m = 1, n = 5
Output: 1
Only 1 horizontal path
```

#### ✅ Test Case 4:

```txt
Input: m = 5, n = 1
Output: 1
Only 1 vertical path
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

From cell `(i,j)`, we can either:

- Move **down** → `(i-1, j)`
- Move **right** → `(i, j-1)`

Base Case:

- If `i === 0 && j === 0`, we reached the start → return 1
- If `i < 0 || j < 0`, we’re out of bounds → return 0

---

#### 📘 Code

```js
function countPaths(i, j) {
  if (i === 0 && j === 0) return 1;
  if (i < 0 || j < 0) return 0;

  return countPaths(i - 1, j) + countPaths(i, j - 1);
}

function uniquePaths(m, n) {
  return countPaths(m - 1, n - 1);
}
```

---

#### ❌ Problems

- **Overlapping subproblems** (many repeated calls)
- **Exponential time**

#### ⏱ Complexity

- **Time**: O(2^(m + n))
- **Space**: O(m + n) (recursion stack)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Intuition

Store results of `(i, j)` in `dp[i][j]` to avoid recomputation.

---

#### 📘 Code

```js
function countPaths(i, j, dp) {
  if (i === 0 && j === 0) return 1;
  if (i < 0 || j < 0) return 0;
  if (dp[i][j] !== -1) return dp[i][j];

  return (dp[i][j] = countPaths(i - 1, j, dp) + countPaths(i, j - 1, dp));
}

function uniquePaths(m, n) {
  const dp = Array.from({ length: m }, () => Array(n).fill(-1));
  return countPaths(m - 1, n - 1, dp);
}
```

---

#### 🔍 Dry Run: `m = 2, n = 2`

```
countPaths(1,1) → countPaths(0,1) + countPaths(1,0)
→ Reuses countPaths(0,0) = 1
→ Total = 2 ✅
```

---

#### ⏱ Complexity

- **Time**: O(m × n)
- **Space**: O(m × n) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Create a `dp[m][n]` array where `dp[i][j]` = number of ways to reach cell `(i,j)`.

---

#### 📘 Code

```js
function uniquePaths(m, n) {
  const dp = Array.from({ length: m }, () => Array(n).fill(0));
  dp[0][0] = 1;

  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (i > 0) dp[i][j] += dp[i - 1][j];
      if (j > 0) dp[i][j] += dp[i][j - 1];
    }
  }

  return dp[m - 1][n - 1];
}
```

---

#### 🔍 Dry Run: `m = 3, n = 3`

```
Initialize dp[0][0] = 1

Fill first row and column = 1
Rest:
dp[1][1] = dp[0][1] + dp[1][0] = 1 + 1 = 2
dp[1][2] = dp[0][2] + dp[1][1] = 1 + 2 = 3
dp[2][2] = dp[1][2] + dp[2][1] = 3 + 3 = 6 ✅
```

---

#### ⏱ Complexity

- **Time**: O(m × n)
- **Space**: O(m × n)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

At any point, we only need the **previous row** to calculate the current row → use 2 arrays.

---

#### 📘 Code

```js
function uniquePaths(m, n) {
  let prev = new Array(n).fill(1);

  for (let i = 1; i < m; i++) {
    const curr = new Array(n).fill(0);
    curr[0] = 1;
    for (let j = 1; j < n; j++) {
      curr[j] = curr[j - 1] + prev[j];
    }
    prev = curr;
  }

  return prev[n - 1];
}
```

---

#### 🔍 Dry Run: `m = 3, n = 3`

```
prev = [1, 1, 1]
row 2 → curr = [1, 2, 3]
row 3 → curr = [1, 3, 6] → final = 6 ✅
```

---

#### ⏱ Complexity

- **Time**: O(m × n)
- **Space**: O(n) ✅

---

### 🔢 Bonus Approach: Combinatorics

#### 🧠 Intuition

Total moves = `m - 1` downs and `n - 1` rights
Total permutations = `C(m + n - 2, m - 1)`

---

#### 📘 Code

```js
function factorial(x) {
  let res = 1;
  for (let i = 2; i <= x; i++) res *= i;
  return res;
}

function uniquePaths(m, n) {
  return factorial(m + n - 2) / (factorial(m - 1) * factorial(n - 1));
}
```

Or more efficiently with multiplicative formula (to avoid overflows).

---

#### ⏱ Complexity

- **Time**: O(min(m, n))
- **Space**: O(1)

---

### 📌 Summary Table

| Approach           | Time        | Space    | Notes                       |
| ------------------ | ----------- | -------- | --------------------------- |
| Recursion          | O(2^(m+n))  | O(m + n) | Too slow                    |
| Memoization        | O(m × n)    | O(m × n) | Top-down + caching          |
| Tabulation         | O(m × n)    | O(m × n) | Easy to debug               |
| Space Optimization | O(m × n)    | O(n) ✅  | Best for large input        |
| Combinatorics      | O(min(m,n)) | O(1) ✅  | Fastest (no DP), math-based |

---

## 🔢 **3. Grid Unique Paths II (with Obstacles)**

### 📘 Problem Statement

You are given a grid of size `m x n` filled with **0s** and **1s**:

- `0` represents an **empty cell**
- `1` represents an **obstacle**

You are initially at the **top-left cell (0, 0)** and want to reach the **bottom-right cell (m-1, n-1)**.
You can **only move right or down**.

Return the **number of unique paths** that **avoid the obstacles**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input:
grid = [
  [0, 0, 0],
  [0, 1, 0],
  [0, 0, 0]
]
Output: 2
Explanation:
There are two valid paths: →→↓↓ and ↓↓→→
```

#### ✅ Test Case 2:

```txt
Input:
grid = [
  [0, 1],
  [0, 0]
]
Output: 1
```

#### ✅ Test Case 3:

```txt
Input:
grid = [
  [1, 0]
]
Output: 0
Explanation: Starting cell is an obstacle
```

#### ✅ Test Case 4:

```txt
Input:
grid = [
  [0]
]
Output: 1
```

---

### 🚀 Approach 1: Recursion (with obstacles)

#### 🧠 Intuition

From `(i,j)`, we can move:

- Up → `(i-1, j)`
- Left → `(i, j-1)`

Avoid cells with obstacles (`grid[i][j] === 1`)

---

#### 📘 Code

```js
function countPaths(i, j, grid) {
  if (i >= 0 && j >= 0 && grid[i][j] === 1) return 0;
  if (i === 0 && j === 0) return 1;
  if (i < 0 || j < 0) return 0;

  return countPaths(i - 1, j, grid) + countPaths(i, j - 1, grid);
}

function uniquePathsWithObstacles(grid) {
  const m = grid.length,
    n = grid[0].length;
  return countPaths(m - 1, n - 1, grid);
}
```

---

#### ❌ Problems

- Inefficient due to recomputation
- Not suitable for large inputs

#### ⏱ Complexity

- **Time**: O(2^(m+n))
- **Space**: O(m+n)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Intuition

Use `dp[i][j]` to store paths to cell `(i, j)`

---

#### 📘 Code

```js
function countPaths(i, j, grid, dp) {
  if (i >= 0 && j >= 0 && grid[i][j] === 1) return 0;
  if (i === 0 && j === 0) return 1;
  if (i < 0 || j < 0) return 0;
  if (dp[i][j] !== -1) return dp[i][j];

  return (dp[i][j] =
    countPaths(i - 1, j, grid, dp) + countPaths(i, j - 1, grid, dp));
}

function uniquePathsWithObstacles(grid) {
  const m = grid.length,
    n = grid[0].length;
  const dp = Array.from({ length: m }, () => Array(n).fill(-1));
  return countPaths(m - 1, n - 1, grid, dp);
}
```

---

#### 🔍 Dry Run: Grid with obstacle at (1,1)

```
→ When we hit grid[i][j] === 1, return 0
→ Recursively explore valid cells, memoizing results
```

---

#### ⏱ Complexity

- **Time**: O(m × n)
- **Space**: O(m × n) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Use a 2D `dp[][]` array.
If current cell is **not an obstacle**, build from top and left.

---

#### 📘 Code

```js
function uniquePathsWithObstacles(grid) {
  const m = grid.length;
  const n = grid[0].length;
  const dp = Array.from({ length: m }, () => Array(n).fill(0));

  // If starting cell is blocked
  if (grid[0][0] === 1) return 0;

  dp[0][0] = 1;

  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (grid[i][j] === 1) {
        dp[i][j] = 0;
      } else {
        if (i > 0) dp[i][j] += dp[i - 1][j];
        if (j > 0) dp[i][j] += dp[i][j - 1];
      }
    }
  }

  return dp[m - 1][n - 1];
}
```

---

#### 🔍 Dry Run: Grid with obstacle

```
dp[0][0] = 1

→ Build row by row
→ If cell is blocked, skip it
→ Each cell: sum of top and left (if not blocked)
```

---

#### ⏱ Complexity

- **Time**: O(m × n)
- **Space**: O(m × n)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

We only need the previous row → optimize to use 1D array.

---

#### 📘 Code

```js
function uniquePathsWithObstacles(grid) {
  const m = grid.length;
  const n = grid[0].length;
  let prev = new Array(n).fill(0);

  for (let i = 0; i < m; i++) {
    let curr = new Array(n).fill(0);
    for (let j = 0; j < n; j++) {
      if (grid[i][j] === 1) {
        curr[j] = 0;
      } else if (i === 0 && j === 0) {
        curr[j] = 1;
      } else {
        const up = i > 0 ? prev[j] : 0;
        const left = j > 0 ? curr[j - 1] : 0;
        curr[j] = up + left;
      }
    }
    prev = curr;
  }

  return prev[n - 1];
}
```

---

#### 🔍 Dry Run:

```
curr[j] = from top (prev[j]) + from left (curr[j-1])
→ Works as long as you update row by row
→ Obstacle cells = 0
```

---

#### ⏱ Complexity

- **Time**: O(m × n)
- **Space**: O(n) ✅

---

### 📌 Summary Table

| Approach           | Time     | Space    | Notes                     |
| ------------------ | -------- | -------- | ------------------------- |
| Recursion          | O(2^n)   | O(m + n) | Brute force, not feasible |
| Memoization        | O(m × n) | O(m × n) | Caches valid paths        |
| Tabulation         | O(m × n) | O(m × n) | Clean and iterative       |
| Space Optimization | O(m × n) | O(n) ✅  | Best for large inputs     |

---

## 🔢 **4. Minimum Path Sum in a Grid**

### 📘 Problem Statement

You are given a `m x n` grid filled with **non-negative integers**.
Start at the **top-left cell (0, 0)** and reach the **bottom-right cell (m-1, n-1)**.

At each step, you may only move **right** or **down**.

Return the **minimum path sum** from top-left to bottom-right.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input:
grid = [
  [1, 3, 1],
  [1, 5, 1],
  [4, 2, 1]
]
Output: 7
Explanation: 1 → 3 → 1 → 1 → 1 = 7
```

#### ✅ Test Case 2:

```txt
Input:
grid = [
  [1, 2, 3],
  [4, 5, 6]
]
Output: 12
Explanation: 1 → 2 → 3 → 6 = 12
```

#### ✅ Test Case 3:

```txt
Input:
grid = [
  [5]
]
Output: 5
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

From `(i,j)`, we can come from:

- Up → `(i-1, j)`
- Left → `(i, j-1)`

Recursively calculate min path to `(i, j)`.

---

#### 📘 Code

```js
function minPath(i, j, grid) {
  if (i === 0 && j === 0) return grid[0][0];
  if (i < 0 || j < 0) return Infinity;

  const up = minPath(i - 1, j, grid);
  const left = minPath(i, j - 1, grid);
  return grid[i][j] + Math.min(up, left);
}

function minPathSum(grid) {
  const m = grid.length,
    n = grid[0].length;
  return minPath(m - 1, n - 1, grid);
}
```

---

#### ❌ Problems

- Too many repeated calls
- Not efficient for large inputs

#### ⏱ Complexity

- **Time**: O(2^(m+n))
- **Space**: O(m + n) (recursion)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Intuition

Store results of subproblems in `dp[i][j]`.

---

#### 📘 Code

```js
function minPath(i, j, grid, dp) {
  if (i === 0 && j === 0) return grid[0][0];
  if (i < 0 || j < 0) return Infinity;
  if (dp[i][j] !== -1) return dp[i][j];

  const up = minPath(i - 1, j, grid, dp);
  const left = minPath(i, j - 1, grid, dp);
  return (dp[i][j] = grid[i][j] + Math.min(up, left));
}

function minPathSum(grid) {
  const m = grid.length,
    n = grid[0].length;
  const dp = Array.from({ length: m }, () => Array(n).fill(-1));
  return minPath(m - 1, n - 1, grid, dp);
}
```

---

#### 🔍 Dry Run: For (2,2)

```
minPath(2,2) → min( minPath(1,2), minPath(2,1) )
Each value is cached after first call.
```

---

#### ⏱ Complexity

- **Time**: O(m × n)
- **Space**: O(m × n) + O(m + n) stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Build `dp[i][j]` = min path to reach `(i,j)` using `dp[i-1][j]` and `dp[i][j-1]`.

---

#### 📘 Code

```js
function minPathSum(grid) {
  const m = grid.length,
    n = grid[0].length;
  const dp = Array.from({ length: m }, () => Array(n).fill(0));

  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (i === 0 && j === 0) dp[i][j] = grid[i][j];
      else {
        const up = i > 0 ? dp[i - 1][j] : Infinity;
        const left = j > 0 ? dp[i][j - 1] : Infinity;
        dp[i][j] = grid[i][j] + Math.min(up, left);
      }
    }
  }

  return dp[m - 1][n - 1];
}
```

---

#### 🔍 Dry Run for Example Grid:

```
Fill first row and column by accumulating sums
Then:
dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])
```

---

#### ⏱ Complexity

- **Time**: O(m × n)
- **Space**: O(m × n)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

Use only **one row** to keep track of previous values (just like in Unique Paths II).

---

#### 📘 Code

```js
function minPathSum(grid) {
  const m = grid.length,
    n = grid[0].length;
  let prev = new Array(n).fill(0);

  for (let i = 0; i < m; i++) {
    const curr = new Array(n).fill(0);
    for (let j = 0; j < n; j++) {
      if (i === 0 && j === 0) curr[j] = grid[i][j];
      else {
        const up = i > 0 ? prev[j] : Infinity;
        const left = j > 0 ? curr[j - 1] : Infinity;
        curr[j] = grid[i][j] + Math.min(up, left);
      }
    }
    prev = curr;
  }

  return prev[n - 1];
}
```

---

#### 🔍 Dry Run:

```
prev = [accumulated row]
curr[j] = grid[i][j] + min(left, up)
→ Just 2 arrays needed
```

---

#### ⏱ Complexity

- **Time**: O(m × n)
- **Space**: O(n) ✅

---

### 📌 Summary Table

| Approach           | Time       | Space    | Notes                         |
| ------------------ | ---------- | -------- | ----------------------------- |
| Recursion          | O(2^(m+n)) | O(m + n) | Not feasible for large grids  |
| Memoization        | O(m × n)   | O(m × n) | Top-down DP with caching      |
| Tabulation         | O(m × n)   | O(m × n) | Iterative & easy to debug     |
| Space Optimization | O(m × n)   | O(n) ✅  | Best space-efficient approach |

---

## 🔢 **5. Minimum Path Sum in a Triangular Grid**

### 📘 Problem Statement

You are given a **triangle array** like this:

```txt
[
     [2],
    [3, 4],
   [6, 5, 7],
  [4, 1, 8, 3]
]
```

Start at the **top (0,0)** and move **to adjacent numbers** on the row below.
At each step, you may move to **`i+1, j` or `i+1, j+1`**.
Return the **minimum path sum** from top to bottom.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input:
[
 [2],
 [3,4],
 [6,5,7],
 [4,1,8,3]
]
Output: 11
Explanation: 2 + 3 + 5 + 1 = 11
```

#### ✅ Test Case 2:

```txt
Input:
[
 [1],
 [2,3],
 [3,6,7],
 [8,9,6,10]
]
Output: 14
Explanation: 1 + 2 + 3 + 8 = 14
```

#### ✅ Test Case 3:

```txt
Input:
[
 [5]
]
Output: 5
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

Start from `(0,0)` and move either:

- Down → `(i+1, j)`
- Diagonal → `(i+1, j+1)`

---

#### 📘 Code

```js
function minimumPath(i, j, triangle) {
  const n = triangle.length;
  if (i === n - 1) return triangle[i][j];

  const down = minimumPath(i + 1, j, triangle);
  const diag = minimumPath(i + 1, j + 1, triangle);

  return triangle[i][j] + Math.min(down, diag);
}

function minimumTotal(triangle) {
  return minimumPath(0, 0, triangle);
}
```

---

#### ❌ Problems

- **Exponential time** for large input
- Too many repeated calls

#### ⏱ Complexity

- **Time**: O(2^n)
- **Space**: O(n) (recursion depth)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Intuition

Store intermediate results in a `dp[i][j]` table.

---

#### 📘 Code

```js
function minimumPath(i, j, triangle, dp) {
  const n = triangle.length;
  if (i === n - 1) return triangle[i][j];
  if (dp[i][j] !== -1) return dp[i][j];

  const down = minimumPath(i + 1, j, triangle, dp);
  const diag = minimumPath(i + 1, j + 1, triangle, dp);

  return (dp[i][j] = triangle[i][j] + Math.min(down, diag));
}

function minimumTotal(triangle) {
  const n = triangle.length;
  const dp = Array.from({ length: n }, (_, i) => Array(i + 1).fill(-1));
  return minimumPath(0, 0, triangle, dp);
}
```

---

#### 🔍 Dry Run:

```
At each cell: store min path from that point downwards.
Final result is stored in dp[0][0].
```

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(n²) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Start from the bottom of the triangle and build up.

`dp[i][j] = triangle[i][j] + min(dp[i+1][j], dp[i+1][j+1])`

---

#### 📘 Code

```js
function minimumTotal(triangle) {
  const n = triangle.length;
  const dp = Array.from({ length: n }, () => Array(n).fill(0));

  // Base case: last row
  for (let j = 0; j < n; j++) {
    dp[n - 1][j] = triangle[n - 1][j];
  }

  // Build up from second-last row
  for (let i = n - 2; i >= 0; i--) {
    for (let j = 0; j <= i; j++) {
      dp[i][j] = triangle[i][j] + Math.min(dp[i + 1][j], dp[i + 1][j + 1]);
    }
  }

  return dp[0][0];
}
```

---

#### 🔍 Dry Run:

```txt
Start with last row:
[4, 1, 8, 3]

Go up one row:
[6, 5, 7] → [7, 6, 10]
[3, 4] → [9, 10]
[2] → [11]
```

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(n²)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

Only keep the current and next row.
We can reduce `dp[i][j]` to just a 1D array.

---

#### 📘 Code

```js
function minimumTotal(triangle) {
  const n = triangle.length;
  let front = [...triangle[n - 1]];

  for (let i = n - 2; i >= 0; i--) {
    const curr = [];
    for (let j = 0; j <= i; j++) {
      curr[j] = triangle[i][j] + Math.min(front[j], front[j + 1]);
    }
    front = curr;
  }

  return front[0];
}
```

---

#### 🔍 Dry Run:

```txt
front = [4, 1, 8, 3]
curr = [7, 6, 10]
→ Next: [9, 10]
→ Final: [11]
```

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(n) ✅

---

### 📌 Summary Table

| Approach            | Time   | Space   | Notes                            |
| ------------------- | ------ | ------- | -------------------------------- |
| Recursion           | O(2^n) | O(n)    | Not feasible for large triangles |
| Memoization (Top)   | O(n²)  | O(n²)   | Recursive + cache                |
| Tabulation (Bottom) | O(n²)  | O(n²)   | Bottom-up, intuitive             |
| Space Optimization  | O(n²)  | O(n) ✅ | Best for time & space efficiency |

---

## 🔢 **6. Minimum / Maximum Falling Path Sum (DP-12)**

### 📘 Problem Statement

You are given an `n x n` grid (matrix) of integers.

A **falling path** starts at any cell in the **first row**, and moves down to the cell **directly below or diagonally left/right**.

Return the **minimum** (or **maximum**) falling path sum — i.e., the **sum of the path** with the smallest (or largest) total from top to bottom.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input:
[
  [2, 1, 3],
  [6, 5, 4],
  [7, 8, 9]
]
Output: 13
Explanation: 1 → 4 → 8 = 13
```

#### ✅ Test Case 2:

```txt
Input:
[
  [-19, 57],
  [-40, -5]
]
Output: -59
Explanation: -19 → -40 = -59
```

#### ✅ Test Case 3:

```txt
Input:
[
  [10]
]
Output: 10
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

At each cell `(i, j)` in the matrix, you can move to:

- `(i+1, j-1)` → left-diagonal
- `(i+1, j)` → down
- `(i+1, j+1)` → right-diagonal

Base case:

- If `i == n-1` → return matrix\[i]\[j]

---

#### 📘 Code

```js
function helper(i, j, matrix) {
  const n = matrix.length;
  if (j < 0 || j >= n) return Infinity; // out of bounds
  if (i === n - 1) return matrix[i][j];

  const down = helper(i + 1, j, matrix);
  const left = helper(i + 1, j - 1, matrix);
  const right = helper(i + 1, j + 1, matrix);

  return matrix[i][j] + Math.min(down, left, right);
}

function minFallingPathSum(matrix) {
  const n = matrix.length;
  let res = Infinity;

  for (let j = 0; j < n; j++) {
    res = Math.min(res, helper(0, j, matrix));
  }

  return res;
}
```

---

#### ❌ Problems

- Redundant subproblem calls
- Exponential time

---

#### ⏱ Complexity

- **Time**: O(3^n)
- **Space**: O(n) recursion stack

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Intuition

Use a 2D `dp[i][j]` array to store minimum path sum from `(i, j)` to bottom.

---

#### 📘 Code

```js
function helper(i, j, matrix, dp) {
  const n = matrix.length;
  if (j < 0 || j >= n) return Infinity;
  if (i === n - 1) return matrix[i][j];
  if (dp[i][j] !== -1) return dp[i][j];

  const down = helper(i + 1, j, matrix, dp);
  const left = helper(i + 1, j - 1, matrix, dp);
  const right = helper(i + 1, j + 1, matrix, dp);

  return (dp[i][j] = matrix[i][j] + Math.min(down, left, right));
}

function minFallingPathSum(matrix) {
  const n = matrix.length;
  const dp = Array.from({ length: n }, () => Array(n).fill(-1));
  let minSum = Infinity;

  for (let j = 0; j < n; j++) {
    minSum = Math.min(minSum, helper(0, j, matrix, dp));
  }

  return minSum;
}
```

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(n²) + recursion

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

We start filling `dp[][]` from the **bottom row up**.

Each cell takes `min(down, left-diag, right-diag)` from the row below.

---

#### 📘 Code

```js
function minFallingPathSum(matrix) {
  const n = matrix.length;
  const dp = Array.from({ length: n }, () => Array(n).fill(0));

  // Base case: last row is same
  for (let j = 0; j < n; j++) {
    dp[n - 1][j] = matrix[n - 1][j];
  }

  for (let i = n - 2; i >= 0; i--) {
    for (let j = 0; j < n; j++) {
      const down = dp[i + 1][j];
      const left = j > 0 ? dp[i + 1][j - 1] : Infinity;
      const right = j < n - 1 ? dp[i + 1][j + 1] : Infinity;

      dp[i][j] = matrix[i][j] + Math.min(down, left, right);
    }
  }

  return Math.min(...dp[0]);
}
```

---

#### 🔍 Dry Run:

```
Start from bottom row → build values going up
Top row stores min path sums starting from each cell
```

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(n²)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

Since we only need the next row to build the current, we can use two 1D arrays.

---

#### 📘 Code

```js
function minFallingPathSum(matrix) {
  const n = matrix.length;
  let next = [...matrix[n - 1]];

  for (let i = n - 2; i >= 0; i--) {
    const curr = Array(n).fill(0);
    for (let j = 0; j < n; j++) {
      const down = next[j];
      const left = j > 0 ? next[j - 1] : Infinity;
      const right = j < n - 1 ? next[j + 1] : Infinity;

      curr[j] = matrix[i][j] + Math.min(down, left, right);
    }
    next = curr;
  }

  return Math.min(...next);
}
```

---

#### 🔍 Dry Run:

```
next = last row
curr[j] = matrix[i][j] + min(next[j], next[j-1], next[j+1])
→ Final result = min(curr)
```

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(n) ✅

---

### 📌 Summary Table

| Approach           | Time   | Space   | Notes                          |
| ------------------ | ------ | ------- | ------------------------------ |
| Recursion          | O(3^n) | O(n)    | Very slow                      |
| Memoization        | O(n²)  | O(n²)   | Top-down, avoids recomputation |
| Tabulation         | O(n²)  | O(n²)   | Bottom-up, easy to implement   |
| Space Optimization | O(n²)  | O(n) ✅ | Best for large inputs          |

---

## 🔢 **7. Ninja and His Friends** (3D DP)

### 📘 Problem Statement

You are given a `n x m` **grid of chocolates**, where `grid[i][j]` is the number of chocolates in cell `(i, j)`.

There are **two ninjas**:

- **Ninja 1** starts at `(0, 0)`
- **Ninja 2** starts at `(0, m - 1)`

In each step, both ninjas move **down** to the next row (i + 1), and each can move:

- **left (j - 1)**, **down (j)**, or **right (j + 1)**

Both collect chocolates from the cells they land on.
If both land on the **same cell**, chocolate is counted **only once**.

Return the **maximum chocolates** they can collect by the time they reach the **last row**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input:
grid = [
  [3, 1, 1],
  [2, 5, 1],
  [1, 5, 5],
  [2, 1, 1]
]

Output: 24
Explanation: Ninja1 → (0,0)→(1,1)→(2,1)→(3,1)
Ninja2 → (0,2)→(1,1)→(2,2)→(3,2)
```

#### ✅ Test Case 2:

```txt
Input:
grid = [
  [1, 0, 0, 0, 0, 0],
  [0, 0, 0, 0, 0, 0],
  [0, 0, 2, 4, 1, 0]
]
Output: 5
```

#### ✅ Test Case 3:

```txt
Input:
grid = [
  [1]
]
Output: 1
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

At each `(i, j1, j2)` position:

- `i` → current row
- `j1` → Ninja1 column
- `j2` → Ninja2 column

Try **all 9 combinations** of next moves:

- `(-1, -1), (-1, 0), (-1, +1), (0, -1), ... (+1, +1)`
  (i.e., both ninjas can move in 3 ways)

Avoid boundaries and **avoid double counting when j1 == j2**.

---

#### 📘 Code

```js
function maxChoco(i, j1, j2, grid) {
  const r = grid.length,
    c = grid[0].length;
  if (j1 < 0 || j1 >= c || j2 < 0 || j2 >= c) return -Infinity;
  if (i === r - 1) {
    if (j1 === j2) return grid[i][j1];
    return grid[i][j1] + grid[i][j2];
  }

  let maxi = -Infinity;
  for (let dj1 = -1; dj1 <= 1; dj1++) {
    for (let dj2 = -1; dj2 <= 1; dj2++) {
      const value =
        (j1 === j2 ? grid[i][j1] : grid[i][j1] + grid[i][j2]) +
        maxChoco(i + 1, j1 + dj1, j2 + dj2, grid);
      maxi = Math.max(maxi, value);
    }
  }

  return maxi;
}

function maximumChocolates(r, c, grid) {
  return maxChoco(0, 0, c - 1, grid);
}
```

---

#### ❌ Problems

- Tries all 9 possibilities at each level
- Exponential time

---

#### ⏱ Complexity

- **Time**: O(3^r × 3^r)
- **Space**: O(r) (recursive calls)

---

### ✅ Approach 2: Memoization (Top-Down 3D DP)

#### 🧠 Intuition

Use `dp[i][j1][j2]` to store max chocolates from `(i, j1, j2)` onward.

---

#### 📘 Code

```js
function maxChoco(i, j1, j2, grid, dp) {
  const r = grid.length,
    c = grid[0].length;
  if (j1 < 0 || j1 >= c || j2 < 0 || j2 >= c) return -Infinity;
  if (i === r - 1) {
    if (j1 === j2) return grid[i][j1];
    return grid[i][j1] + grid[i][j2];
  }

  if (dp[i][j1][j2] !== -1) return dp[i][j1][j2];

  let maxi = -Infinity;
  for (let dj1 = -1; dj1 <= 1; dj1++) {
    for (let dj2 = -1; dj2 <= 1; dj2++) {
      const val =
        (j1 === j2 ? grid[i][j1] : grid[i][j1] + grid[i][j2]) +
        maxChoco(i + 1, j1 + dj1, j2 + dj2, grid, dp);
      maxi = Math.max(maxi, val);
    }
  }

  return (dp[i][j1][j2] = maxi);
}

function maximumChocolates(r, c, grid) {
  const dp = Array.from({ length: r }, () =>
    Array.from({ length: c }, () => Array(c).fill(-1))
  );
  return maxChoco(0, 0, c - 1, grid, dp);
}
```

---

#### ⏱ Complexity

- **Time**: O(r × c × c × 9) = O(r × c²)
- **Space**: O(r × c²) (for memo) + O(r) (recursion)

---

### 🧮 Approach 3: Tabulation (Bottom-Up 3D DP)

#### 🧠 Intuition

We build the `dp[i][j1][j2]` table bottom-up.

Base case: last row `dp[r-1][j1][j2]`

Transition:

```txt
dp[i][j1][j2] = grid[i][j1] + grid[i][j2] (or once if j1 == j2)
+ max(dp[i+1][new_j1][new_j2])
```

---

#### 📘 Code

```js
function maximumChocolates(r, c, grid) {
  const dp = Array.from({ length: r }, () =>
    Array.from({ length: c }, () => Array(c).fill(0))
  );

  for (let j1 = 0; j1 < c; j1++) {
    for (let j2 = 0; j2 < c; j2++) {
      if (j1 === j2) dp[r - 1][j1][j2] = grid[r - 1][j1];
      else dp[r - 1][j1][j2] = grid[r - 1][j1] + grid[r - 1][j2];
    }
  }

  for (let i = r - 2; i >= 0; i--) {
    for (let j1 = 0; j1 < c; j1++) {
      for (let j2 = 0; j2 < c; j2++) {
        let maxi = -Infinity;
        for (let dj1 = -1; dj1 <= 1; dj1++) {
          for (let dj2 = -1; dj2 <= 1; dj2++) {
            const nj1 = j1 + dj1,
              nj2 = j2 + dj2;
            if (nj1 >= 0 && nj1 < c && nj2 >= 0 && nj2 < c) {
              let val = j1 === j2 ? grid[i][j1] : grid[i][j1] + grid[i][j2];
              val += dp[i + 1][nj1][nj2];
              maxi = Math.max(maxi, val);
            }
          }
        }
        dp[i][j1][j2] = maxi;
      }
    }
  }

  return dp[0][0][c - 1];
}
```

---

#### ⏱ Complexity

- **Time**: O(r × c² × 9) = O(r × c²)
- **Space**: O(r × c²)

---

### 🧊 Approach 4: Space Optimization (Optional)

It’s **possible but tricky** (since it’s 3D).
We only need the next row → we can use `2 × c × c` arrays.

---

### 📌 Summary Table

| Approach            | Time        | Space     | Notes                               |
| ------------------- | ----------- | --------- | ----------------------------------- |
| Recursion           | Exponential | O(r)      | TLE                                 |
| Memoization (Top)   | O(r × c²)   | O(r × c²) | Caches overlapping states           |
| Tabulation (Bottom) | O(r × c²)   | O(r × c²) | Best balance of readability & speed |
| Space Optimization  | O(r × c²)   | O(c²) ✅  | Advanced, less intuitive            |

---

# DP On SubSequences

## 🔢 **1. Subset Sum Equal to Target**

### 📘 Problem Statement

Given an array of `n` non-negative integers and a target sum `target`, determine whether there **exists a subset** whose elements **sum up to exactly `target`**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: arr = [2, 3, 7, 8, 10], target = 11
Output: true
Explanation: 3 + 8 = 11
```

#### ✅ Test Case 2:

```txt
Input: arr = [1, 2, 3, 9], target = 5
Output: true
Explanation: 2 + 3 = 5
```

#### ✅ Test Case 3:

```txt
Input: arr = [1, 2, 7, 1, 5], target = 10
Output: true
Explanation: 2 + 1 + 7 = 10
```

#### ✅ Test Case 4:

```txt
Input: arr = [1, 3, 5], target = 9
Output: false
Explanation: No subset adds up to 9
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

We try to either:

- **Pick** the current element (if ≤ target)
- **Skip** the current element

Check if either leads to a valid subset sum.

---

#### 📘 Code

```js
function isSubsetSum(i, target, arr) {
  if (target === 0) return true;
  if (i === 0) return arr[0] === target;

  const notPick = isSubsetSum(i - 1, target, arr);
  const pick =
    arr[i] <= target ? isSubsetSum(i - 1, target - arr[i], arr) : false;

  return pick || notPick;
}

function subsetSumToTarget(n, target, arr) {
  return isSubsetSum(n - 1, target, arr);
}
```

---

#### ❌ Problems

- **Exponential time**
- Repeats many subproblems

---

#### ⏱ Complexity

- **Time**: O(2^n)
- **Space**: O(n) (recursive stack)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Intuition

Use `dp[i][target]` to cache subproblems.

---

#### 📘 Code

```js
function isSubsetSum(i, target, arr, dp) {
  if (target === 0) return true;
  if (i === 0) return arr[0] === target;
  if (dp[i][target] !== -1) return dp[i][target];

  const notPick = isSubsetSum(i - 1, target, arr, dp);
  const pick =
    arr[i] <= target ? isSubsetSum(i - 1, target - arr[i], arr, dp) : false;

  return (dp[i][target] = pick || notPick);
}

function subsetSumToTarget(n, target, arr) {
  const dp = Array.from({ length: n }, () => Array(target + 1).fill(-1));
  return isSubsetSum(n - 1, target, arr, dp);
}
```

---

#### ⏱ Complexity

- **Time**: O(n × target)
- **Space**: O(n × target) + recursion

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Create a `dp[n][target+1]` table.

`dp[i][t]` = whether it's possible to make sum `t` using elements `0 to i`.

---

#### 📘 Code

```js
function subsetSumToTarget(n, target, arr) {
  const dp = Array.from({ length: n }, () => Array(target + 1).fill(false));

  // Base cases
  for (let i = 0; i < n; i++) dp[i][0] = true;
  if (arr[0] <= target) dp[0][arr[0]] = true;

  for (let i = 1; i < n; i++) {
    for (let t = 1; t <= target; t++) {
      const notPick = dp[i - 1][t];
      const pick = arr[i] <= t ? dp[i - 1][t - arr[i]] : false;
      dp[i][t] = pick || notPick;
    }
  }

  return dp[n - 1][target];
}
```

---

#### ⏱ Complexity

- **Time**: O(n × target)
- **Space**: O(n × target)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

Only need the **previous row**, so we can use 2 arrays.

---

#### 📘 Code

```js
function subsetSumToTarget(n, target, arr) {
  let prev = Array(target + 1).fill(false);
  prev[0] = true;
  if (arr[0] <= target) prev[arr[0]] = true;

  for (let i = 1; i < n; i++) {
    const curr = Array(target + 1).fill(false);
    curr[0] = true;
    for (let t = 1; t <= target; t++) {
      const notPick = prev[t];
      const pick = arr[i] <= t ? prev[t - arr[i]] : false;
      curr[t] = pick || notPick;
    }
    prev = curr;
  }

  return prev[target];
}
```

---

#### 🔍 Dry Run (arr = \[2, 3, 7, 8, 10], target = 11):

```
i=0 → arr[0] = 2 → dp[0][2] = true
i=1 → arr[1] = 3 → update 5, etc.
dp[n-1][11] = true
```

---

#### ⏱ Complexity

- **Time**: O(n × target)
- **Space**: O(target) ✅

---

### 📌 Summary Table

| Approach            | Time          | Space         | Notes                         |
| ------------------- | ------------- | ------------- | ----------------------------- |
| Recursion           | O(2^n)        | O(n)          | Brute force                   |
| Memoization (Top)   | O(n × target) | O(n × target) | Caches subproblems            |
| Tabulation (Bottom) | O(n × target) | O(n × target) | Iterative, easy to understand |
| Space Optimized     | O(n × target) | O(target) ✅  | Best approach                 |

---

## 🔢 **2. Partition Equal Subset Sum**

### 📘 Problem Statement

Given an array of `n` **non-negative integers**, determine whether it can be **partitioned into two subsets** such that the **sum of elements in both subsets is equal**.

---

### 🧠 Insight

This is a direct variation of the **Subset Sum Equal to Target** problem.

If `totalSum` of all elements is **odd**, it’s **impossible** to divide into two equal subsets.

If `totalSum` is **even**, just check:
Can we find a subset whose sum is `totalSum / 2`?

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: arr = [1, 5, 11, 5]
Output: true
Explanation: Subsets {1, 5, 5} and {11}
```

#### ✅ Test Case 2:

```txt
Input: arr = [1, 2, 3, 5]
Output: false
Explanation: No equal partition possible
```

#### ✅ Test Case 3:

```txt
Input: arr = [2, 2, 3, 5]
Output: false
```

#### ✅ Test Case 4:

```txt
Input: arr = [3, 1, 1, 2, 2, 1]
Output: true
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

Check if subset with sum = `totalSum / 2` exists (like subset sum).

---

#### 📘 Code

```js
function canPartition(arr) {
  const total = arr.reduce((a, b) => a + b, 0);
  if (total % 2 !== 0) return false;
  const target = total / 2;

  function helper(i, target) {
    if (target === 0) return true;
    if (i === 0) return arr[0] === target;

    const notPick = helper(i - 1, target);
    const pick = arr[i] <= target ? helper(i - 1, target - arr[i]) : false;

    return pick || notPick;
  }

  return helper(arr.length - 1, target);
}
```

---

#### ❌ Problems

- Exponential time
- Recomputes overlapping subproblems

---

#### ⏱ Complexity

- **Time**: O(2^n)
- **Space**: O(n)

---

### ✅ Approach 2: Memoization (Top-Down)

#### 🧠 Intuition

Use `dp[i][target]` to store results of subproblems.

---

#### 📘 Code

```js
function canPartition(arr) {
  const n = arr.length;
  const total = arr.reduce((a, b) => a + b, 0);
  if (total % 2 !== 0) return false;
  const target = total / 2;

  const dp = Array.from({ length: n }, () => Array(target + 1).fill(-1));

  function helper(i, t) {
    if (t === 0) return true;
    if (i === 0) return arr[0] === t;
    if (dp[i][t] !== -1) return dp[i][t];

    const notPick = helper(i - 1, t);
    const pick = arr[i] <= t ? helper(i - 1, t - arr[i]) : false;

    return (dp[i][t] = pick || notPick);
  }

  return helper(n - 1, target);
}
```

---

#### ⏱ Complexity

- **Time**: O(n × target)
- **Space**: O(n × target) + recursion

---

### 🧮 Approach 3: Tabulation (Bottom-Up)

#### 🧠 Intuition

Classic 2D DP. Build up `dp[n][target+1]` iteratively.

---

#### 📘 Code

```js
function canPartition(arr) {
  const n = arr.length;
  const total = arr.reduce((a, b) => a + b, 0);
  if (total % 2 !== 0) return false;
  const target = total / 2;

  const dp = Array.from({ length: n }, () => Array(target + 1).fill(false));
  for (let i = 0; i < n; i++) dp[i][0] = true;
  if (arr[0] <= target) dp[0][arr[0]] = true;

  for (let i = 1; i < n; i++) {
    for (let t = 1; t <= target; t++) {
      const notPick = dp[i - 1][t];
      const pick = arr[i] <= t ? dp[i - 1][t - arr[i]] : false;
      dp[i][t] = pick || notPick;
    }
  }

  return dp[n - 1][target];
}
```

---

#### ⏱ Complexity

- **Time**: O(n × target)
- **Space**: O(n × target)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

Only need the previous row → reduce to 1D.

---

#### 📘 Code

```js
function canPartition(arr) {
  const n = arr.length;
  const total = arr.reduce((a, b) => a + b, 0);
  if (total % 2 !== 0) return false;
  const target = total / 2;

  let prev = Array(target + 1).fill(false);
  prev[0] = true;
  if (arr[0] <= target) prev[arr[0]] = true;

  for (let i = 1; i < n; i++) {
    const curr = Array(target + 1).fill(false);
    curr[0] = true;
    for (let t = 1; t <= target; t++) {
      const notPick = prev[t];
      const pick = arr[i] <= t ? prev[t - arr[i]] : false;
      curr[t] = pick || notPick;
    }
    prev = curr;
  }

  return prev[target];
}
```

---

#### 🔍 Dry Run (arr = \[1, 5, 11, 5]):

```
total = 22 → target = 11
Check if subset with sum 11 exists → Yes → return true
```

---

#### ⏱ Complexity

- **Time**: O(n × target)
- **Space**: O(target) ✅

---

### 📌 Summary Table

| Approach            | Time          | Space         | Notes                               |
| ------------------- | ------------- | ------------- | ----------------------------------- |
| Recursion           | O(2^n)        | O(n)          | Brute force                         |
| Memoization (Top)   | O(n × target) | O(n × target) | Avoids recomputation                |
| Tabulation (Bottom) | O(n × target) | O(n × target) | Clean iterative approach            |
| Space Optimized     | O(n × target) | O(target) ✅  | Best space-efficient implementation |

---

## 🔢 **3. Partition Set Into 2 Subsets With Minimum Absolute Sum Difference**

### 📘 Problem Statement

You are given an array `arr[]` of `n` positive integers.
**Partition the array into two subsets** such that the **absolute difference** between their sums is **minimum**.

Return the **minimum absolute difference**.

---

### 🧠 Insight

- Total sum = `S`
- Goal: split into two subsets with sums `s1` and `s2`, where `s1 + s2 = S`
- Minimize `|s1 - s2| = |S - 2*s1|`
- So, we try to find the **maximum s1 ≤ S/2** such that a subset of `arr` sums to `s1`

This reduces to a classic **subset sum** problem.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: arr = [1, 2, 3, 9]
Output: 3
Explanation: Subsets {1, 2, 3} and {9} → |6 - 9| = 3
```

#### ✅ Test Case 2:

```txt
Input: arr = [1, 2, 7]
Output: 4
Explanation: {1, 2} and {7} → |3 - 7| = 4
```

#### ✅ Test Case 3:

```txt
Input: arr = [10, 20, 15, 5, 25]
Output: 5
Explanation: Partitioned into {10, 20, 5} and {15, 25}
```

#### ✅ Test Case 4:

```txt
Input: arr = [1, 6, 11, 5]
Output: 1
Explanation: {1, 6, 5} and {11}
```

---

### 🚀 Approach 1: Recursion (Subset Sum Exploration)

#### 🧠 Intuition

Try all possible subset sums `s1 ≤ totalSum/2` and track `|S - 2*s1|`.

But recursion will be **exponential** — not optimal for large arrays.

---

#### ⏱ Complexity

- **Time**: O(2^n)
- **Space**: O(n)

---

### ✅ Approach 2: DP with Tabulation (Subset Sum)

#### 🧠 Intuition

1. Calculate `totalSum` of array.
2. Use a DP array `dp[n][sum+1]` to record whether a subset sum `t` is possible using first `i` elements.
3. In the end, check all `s1 ∈ [0..totalSum/2]` and choose the one with **minimum |totalSum - 2\*s1|**

---

#### 📘 Code

```js
function minSubsetSumDiff(arr) {
  const n = arr.length;
  const total = arr.reduce((a, b) => a + b, 0);
  const dp = Array.from({ length: n }, () => Array(total + 1).fill(false));

  // Base cases
  for (let i = 0; i < n; i++) dp[i][0] = true;
  if (arr[0] <= total) dp[0][arr[0]] = true;

  // Fill DP table
  for (let i = 1; i < n; i++) {
    for (let t = 1; t <= total; t++) {
      const notPick = dp[i - 1][t];
      const pick = arr[i] <= t ? dp[i - 1][t - arr[i]] : false;
      dp[i][t] = pick || notPick;
    }
  }

  // Find the minimum difference
  let minDiff = Infinity;
  for (let s1 = 0; s1 <= Math.floor(total / 2); s1++) {
    if (dp[n - 1][s1]) {
      const s2 = total - s1;
      minDiff = Math.min(minDiff, Math.abs(s2 - s1));
    }
  }

  return minDiff;
}
```

---

#### 🔍 Dry Run (arr = \[1, 6, 11, 5]):

```
total = 23
Try all s1 from 0 to 11:
  s1 = 11 → s2 = 12 → diff = 1 ✅
```

---

#### ⏱ Complexity

- **Time**: O(n × totalSum)
- **Space**: O(n × totalSum)

---

### 🧊 Approach 3: Space Optimized DP

#### 🧠 Intuition

We only need the **previous row**, so we can use 1D array.

---

#### 📘 Code

```js
function minSubsetSumDiff(arr) {
  const n = arr.length;
  const total = arr.reduce((a, b) => a + b, 0);

  let prev = Array(total + 1).fill(false);
  prev[0] = true;
  if (arr[0] <= total) prev[arr[0]] = true;

  for (let i = 1; i < n; i++) {
    const curr = Array(total + 1).fill(false);
    curr[0] = true;
    for (let t = 1; t <= total; t++) {
      const notPick = prev[t];
      const pick = arr[i] <= t ? prev[t - arr[i]] : false;
      curr[t] = pick || notPick;
    }
    prev = curr;
  }

  let minDiff = Infinity;
  for (let s1 = 0; s1 <= Math.floor(total / 2); s1++) {
    if (prev[s1]) {
      const s2 = total - s1;
      minDiff = Math.min(minDiff, Math.abs(s2 - s1));
    }
  }

  return minDiff;
}
```

---

#### ⏱ Complexity

- **Time**: O(n × totalSum)
- **Space**: O(totalSum) ✅

---

### 📌 Summary Table

| Approach           | Time            | Space           | Notes                                  |
| ------------------ | --------------- | --------------- | -------------------------------------- |
| Recursion          | O(2^n)          | O(n)            | Brute force                            |
| Tabulation DP      | O(n × totalSum) | O(n × totalSum) | Standard subset sum + difference logic |
| Space Optimized DP | O(n × totalSum) | O(totalSum) ✅  | Most efficient approach                |

---

## 🔢 **4. Count Subsets with Sum K**

### 📘 Problem Statement

Given an array `arr[]` of size `n` and an integer `k`, return the **number of subsets** whose **sum equals exactly `k`**.

---

### 🧠 Insight

We don't just care **whether a subset exists**, but **how many** subsets add up to the given sum.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: arr = [1, 2, 3], k = 3
Output: 2
Explanation: Subsets are [1,2] and [3]
```

#### ✅ Test Case 2:

```txt
Input: arr = [1, 1, 1, 1], k = 2
Output: 6
Explanation: Subsets of size 2 adding to 2
```

#### ✅ Test Case 3:

```txt
Input: arr = [2, 3, 5, 6, 8, 10], k = 10
Output: 3
Explanation: [2,8], [10], [5, 3, 2]
```

#### ✅ Test Case 4:

```txt
Input: arr = [0, 0, 0, 0], k = 0
Output: 16
Explanation: 2^4 subsets all sum to 0
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

At each step, try:

- **Pick** the current element if ≤ k
- **Not pick** it
  Return total number of ways from both choices.

---

#### 📘 Code

```js
function countSubsets(i, target, arr) {
  if (i === 0) {
    if (target === 0 && arr[0] === 0) return 2;
    if (target === 0 || target === arr[0]) return 1;
    return 0;
  }

  const notPick = countSubsets(i - 1, target, arr);
  const pick = arr[i] <= target ? countSubsets(i - 1, target - arr[i], arr) : 0;

  return pick + notPick;
}

function countSubsetsWithSumK(arr, k) {
  return countSubsets(arr.length - 1, k, arr);
}
```

---

#### ❌ Problems

- **Overlapping subproblems**
- **Exponential time** for large inputs

---

#### ⏱ Complexity

- **Time**: O(2^n)
- **Space**: O(n) (recursion depth)

---

### ✅ Approach 2: Memoization (Top-Down)

#### 🧠 Intuition

Use `dp[i][target]` to store results to avoid recomputation.

---

#### 📘 Code

```js
function countSubsets(i, target, arr, dp) {
  if (i === 0) {
    if (target === 0 && arr[0] === 0) return 2;
    if (target === 0 || target === arr[0]) return 1;
    return 0;
  }

  if (dp[i][target] !== -1) return dp[i][target];

  const notPick = countSubsets(i - 1, target, arr, dp);
  const pick =
    arr[i] <= target ? countSubsets(i - 1, target - arr[i], arr, dp) : 0;

  return (dp[i][target] = pick + notPick);
}

function countSubsetsWithSumK(arr, k) {
  const n = arr.length;
  const dp = Array.from({ length: n }, () => Array(k + 1).fill(-1));
  return countSubsets(n - 1, k, arr, dp);
}
```

---

#### ⏱ Complexity

- **Time**: O(n × k)
- **Space**: O(n × k + n)

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Build the DP table from base case `dp[0][...]` to `dp[n][k]`.

---

#### 📘 Code

```js
function countSubsetsWithSumK(arr, k) {
  const n = arr.length;
  const dp = Array.from({ length: n }, () => Array(k + 1).fill(0));

  // Handle base cases
  dp[0][0] = arr[0] === 0 ? 2 : 1;
  if (arr[0] !== 0 && arr[0] <= k) dp[0][arr[0]] = 1;

  for (let i = 1; i < n; i++) {
    for (let target = 0; target <= k; target++) {
      const notPick = dp[i - 1][target];
      const pick = arr[i] <= target ? dp[i - 1][target - arr[i]] : 0;
      dp[i][target] = pick + notPick;
    }
  }

  return dp[n - 1][k];
}
```

---

#### 🔍 Dry Run for `arr = [1, 2, 3], k = 3`:

```
Subsets: [1,2], [3]
Count = 2
```

---

#### ⏱ Complexity

- **Time**: O(n × k)
- **Space**: O(n × k)

---

### 🧊 Approach 4: Space Optimized

#### 🧠 Intuition

We only need the **previous row**, so we can reduce to 1D space.

---

#### 📘 Code

```js
function countSubsetsWithSumK(arr, k) {
  const n = arr.length;
  let prev = Array(k + 1).fill(0);

  prev[0] = arr[0] === 0 ? 2 : 1;
  if (arr[0] !== 0 && arr[0] <= k) prev[arr[0]] = 1;

  for (let i = 1; i < n; i++) {
    const curr = Array(k + 1).fill(0);
    curr[0] = 1;
    for (let target = 0; target <= k; target++) {
      const notPick = prev[target];
      const pick = arr[i] <= target ? prev[target - arr[i]] : 0;
      curr[target] = pick + notPick;
    }
    prev = curr;
  }

  return prev[k];
}
```

---

#### ⏱ Complexity

- **Time**: O(n × k)
- **Space**: O(k) ✅

---

### 📌 Summary Table

| Approach        | Time     | Space    | Notes                |
| --------------- | -------- | -------- | -------------------- |
| Recursion       | O(2^n)   | O(n)     | Brute force          |
| Memoization     | O(n × k) | O(n × k) | Avoids recomputation |
| Tabulation      | O(n × k) | O(n × k) | Clean and iterative  |
| Space Optimized | O(n × k) | O(k) ✅  | Most efficient       |

---

## 🔢 **5. Count Partitions with Given Difference**

### 📘 Problem Statement

You are given an array `arr[]` of size `n` and a number `d`.

Return the **number of ways** to **partition the array into two subsets** such that the **absolute difference** between their sums is exactly `d`.

---

### 🧠 Insight

Let’s say:

- Subset 1 sum = `S1`
- Subset 2 sum = `S2`
- Total sum = `S1 + S2 = total`

We are given: `|S1 - S2| = d`
So:

```
S1 - S2 = d
S1 + S2 = total
----------------
=> 2*S1 = total + d
=> S1 = (total + d) / 2
```

Hence, this reduces to:
✅ **Count the number of subsets with sum = (total + d) / 2**

But we must ensure:

- `(total + d)` is even and
- `(total + d) / 2 ≥ 0`

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: arr = [1, 1, 2, 3], d = 1
Output: 3
Explanation: 3 subsets → {1, 2}, {1, 2}, {1, 1, 3}
```

#### ✅ Test Case 2:

```txt
Input: arr = [1, 2, 3, 4, 5], d = 3
Output: 3
```

#### ✅ Test Case 3:

```txt
Input: arr = [1, 2, 7], d = 4
Output: 2
```

#### ✅ Test Case 4:

```txt
Input: arr = [1, 2, 3], d = 10
Output: 0
Explanation: Not possible
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

Reduce the problem to **counting subsets with target sum = (total + d) / 2**

Try both:

- Pick current element if ≤ target
- Don’t pick current element

---

#### 📘 Code

```js
function countWays(i, target, arr) {
  if (i === 0) {
    if (target === 0 && arr[0] === 0) return 2;
    if (target === 0 || target === arr[0]) return 1;
    return 0;
  }

  const notPick = countWays(i - 1, target, arr);
  const pick = arr[i] <= target ? countWays(i - 1, target - arr[i], arr) : 0;

  return pick + notPick;
}

function countPartitionsWithDiff(arr, d) {
  const total = arr.reduce((a, b) => a + b, 0);
  if ((total + d) % 2 !== 0) return 0;

  const target = (total + d) / 2;
  return countWays(arr.length - 1, target, arr);
}
```

---

#### ⏱ Complexity

- **Time**: O(2^n)
- **Space**: O(n)

---

### ✅ Approach 2: Memoization (Top-Down)

#### 🧠 Intuition

Use a DP table `dp[i][target]` to avoid recomputing subproblems.

---

#### 📘 Code

```js
function countWays(i, target, arr, dp) {
  if (i === 0) {
    if (target === 0 && arr[0] === 0) return 2;
    if (target === 0 || target === arr[0]) return 1;
    return 0;
  }

  if (dp[i][target] !== -1) return dp[i][target];

  const notPick = countWays(i - 1, target, arr, dp);
  const pick =
    arr[i] <= target ? countWays(i - 1, target - arr[i], arr, dp) : 0;

  return (dp[i][target] = pick + notPick);
}

function countPartitionsWithDiff(arr, d) {
  const total = arr.reduce((a, b) => a + b, 0);
  if ((total + d) % 2 !== 0) return 0;

  const target = (total + d) / 2;
  const n = arr.length;
  const dp = Array.from({ length: n }, () => Array(target + 1).fill(-1));
  return countWays(n - 1, target, arr, dp);
}
```

---

#### ⏱ Complexity

- **Time**: O(n × target)
- **Space**: O(n × target) + O(n) recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up)

#### 🧠 Intuition

Standard bottom-up 2D DP.
Track the number of ways to make each sum using elements from 0 to i.

---

#### 📘 Code

```js
function countPartitionsWithDiff(arr, d) {
  const total = arr.reduce((a, b) => a + b, 0);
  if ((total + d) % 2 !== 0) return 0;

  const target = (total + d) / 2;
  const n = arr.length;

  const dp = Array.from({ length: n }, () => Array(target + 1).fill(0));

  // Base case
  dp[0][0] = arr[0] === 0 ? 2 : 1;
  if (arr[0] !== 0 && arr[0] <= target) dp[0][arr[0]] = 1;

  for (let i = 1; i < n; i++) {
    for (let t = 0; t <= target; t++) {
      const notPick = dp[i - 1][t];
      const pick = arr[i] <= t ? dp[i - 1][t - arr[i]] : 0;
      dp[i][t] = pick + notPick;
    }
  }

  return dp[n - 1][target];
}
```

---

#### ⏱ Complexity

- **Time**: O(n × target)
- **Space**: O(n × target)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

Use 1D array to store only previous row values and update in-place.

---

#### 📘 Code

```js
function countPartitionsWithDiff(arr, d) {
  const total = arr.reduce((a, b) => a + b, 0);
  if ((total + d) % 2 !== 0) return 0;

  const target = (total + d) / 2;
  const n = arr.length;

  let prev = Array(target + 1).fill(0);

  prev[0] = arr[0] === 0 ? 2 : 1;
  if (arr[0] !== 0 && arr[0] <= target) prev[arr[0]] = 1;

  for (let i = 1; i < n; i++) {
    const curr = Array(target + 1).fill(0);
    curr[0] = 1;

    for (let t = 0; t <= target; t++) {
      const notPick = prev[t];
      const pick = arr[i] <= t ? prev[t - arr[i]] : 0;
      curr[t] = pick + notPick;
    }

    prev = curr;
  }

  return prev[target];
}
```

---

#### 🔍 Dry Run for `arr = [1, 1, 2, 3], d = 1`

```
total = 7 → target = (7+1)/2 = 4
Count number of subsets with sum = 4
Answer = 3
```

---

#### ⏱ Complexity

- **Time**: O(n × target)
- **Space**: O(target) ✅

---

### 📌 Summary Table

| Approach           | Time          | Space         | Notes                         |
| ------------------ | ------------- | ------------- | ----------------------------- |
| Recursion          | O(2^n)        | O(n)          | Brute force                   |
| Memoization        | O(n × target) | O(n × target) | Top-down DP                   |
| Tabulation         | O(n × target) | O(n × target) | Bottom-up iterative DP        |
| Space Optimization | O(n × target) | O(target) ✅  | Best space-optimized solution |

---

## 🔢 **6. Minimum Coins (Unbounded Knapsack Variant)**

### 📘 Problem Statement

Given an array of distinct coin denominations `coins[]` and a target amount `amount`, return the **minimum number of coins** needed to make up that amount. If it is not possible to form the amount, return `-1`.

Each coin can be used **unlimited times** (unbounded knapsack style).

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: coins = [1, 2, 5], amount = 11
Output: 3
Explanation: 5 + 5 + 1 = 11
```

#### ✅ Test Case 2:

```txt
Input: coins = [2], amount = 3
Output: -1
Explanation: Impossible to form 3 using only 2s
```

#### ✅ Test Case 3:

```txt
Input: coins = [1], amount = 0
Output: 0
Explanation: No coins needed
```

#### ✅ Test Case 4:

```txt
Input: coins = [1, 3, 4], amount = 6
Output: 2
Explanation: 3 + 3 or 2 + 4
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

Try every coin at every step:

- If a coin ≤ remaining amount, try taking it and reduce the amount.
- Find the **minimum number of coins** among all valid options.

---

#### 📘 Code

```js
function minCoins(i, target, coins) {
  if (i === 0) {
    if (target % coins[0] === 0) return target / coins[0];
    return Infinity;
  }

  const notPick = minCoins(i - 1, target, coins);
  const pick =
    coins[i] <= target ? 1 + minCoins(i, target - coins[i], coins) : Infinity;

  return Math.min(pick, notPick);
}

function coinChange(coins, amount) {
  const res = minCoins(coins.length - 1, amount, coins);
  return res === Infinity ? -1 : res;
}
```

---

#### ❌ Problems

- **Overlapping subproblems**
- **Exponential Time**

---

#### ⏱ Complexity

- **Time**: O(2^amount)
- **Space**: O(amount)

---

### ✅ Approach 2: Memoization (Top-Down)

#### 🧠 Intuition

Store results of subproblems in a `dp[i][target]` table to avoid recomputation.

---

#### 📘 Code

```js
function minCoins(i, target, coins, dp) {
  if (i === 0) {
    if (target % coins[0] === 0) return target / coins[0];
    return Infinity;
  }

  if (dp[i][target] !== -1) return dp[i][target];

  const notPick = minCoins(i - 1, target, coins, dp);
  const pick =
    coins[i] <= target
      ? 1 + minCoins(i, target - coins[i], coins, dp)
      : Infinity;

  return (dp[i][target] = Math.min(pick, notPick));
}

function coinChange(coins, amount) {
  const n = coins.length;
  const dp = Array.from({ length: n }, () => Array(amount + 1).fill(-1));
  const res = minCoins(n - 1, amount, coins, dp);
  return res === Infinity ? -1 : res;
}
```

---

#### ⏱ Complexity

- **Time**: O(n × amount)
- **Space**: O(n × amount) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Use a `dp[n][amount + 1]` table.
`dp[i][t]` represents minimum coins to get total `t` using first `i` coins.

---

#### 📘 Code

```js
function coinChange(coins, amount) {
  const n = coins.length;
  const dp = Array.from({ length: n }, () => Array(amount + 1).fill(Infinity));

  for (let t = 0; t <= amount; t++) {
    if (t % coins[0] === 0) dp[0][t] = t / coins[0];
  }

  for (let i = 1; i < n; i++) {
    for (let t = 0; t <= amount; t++) {
      const notPick = dp[i - 1][t];
      const pick = coins[i] <= t ? 1 + dp[i][t - coins[i]] : Infinity;
      dp[i][t] = Math.min(pick, notPick);
    }
  }

  const ans = dp[n - 1][amount];
  return ans === Infinity ? -1 : ans;
}
```

---

#### ⏱ Complexity

- **Time**: O(n × amount)
- **Space**: O(n × amount)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

Use two 1D arrays (or one with overwrite) since we only need current and previous rows.

---

#### 📘 Code

```js
function coinChange(coins, amount) {
  const n = coins.length;
  let prev = Array(amount + 1).fill(Infinity);

  for (let t = 0; t <= amount; t++) {
    if (t % coins[0] === 0) prev[t] = t / coins[0];
  }

  for (let i = 1; i < n; i++) {
    const curr = Array(amount + 1).fill(Infinity);
    for (let t = 0; t <= amount; t++) {
      const notPick = prev[t];
      const pick = coins[i] <= t ? 1 + curr[t - coins[i]] : Infinity;
      curr[t] = Math.min(pick, notPick);
    }
    prev = curr;
  }

  return prev[amount] === Infinity ? -1 : prev[amount];
}
```

---

#### 🔍 Dry Run for `coins = [1, 2, 5], amount = 11`:

```
dp[0][...] → [0, 1, 2, ..., 11] using only 1
dp[1][...] → updated using coin 2
dp[2][...] → updated using coin 5 → dp[11] = 3 ✅
```

---

#### ⏱ Complexity

- **Time**: O(n × amount)
- **Space**: O(amount) ✅

---

### 📌 Summary Table

| Approach           | Time          | Space         | Notes                                  |
| ------------------ | ------------- | ------------- | -------------------------------------- |
| Recursion          | Exponential   | O(amount)     | Brute force                            |
| Memoization        | O(n × amount) | O(n × amount) | Avoids recomputation                   |
| Tabulation         | O(n × amount) | O(n × amount) | Iterative DP                           |
| Space Optimization | O(n × amount) | O(amount) ✅  | Most optimal for large `amount` values |

---

## 🔢 **7. Target Sum**

### 📘 Problem Statement

You are given an array of integers `arr[]` and an integer `target`.

Assign `+` or `–` sign before each element so that the final **expression evaluates to `target`**.

Return the **total number of ways** to do so.

---

### 🔁 Relation to Subset Sum

This problem is a transformation of **subset sum**.

Let:

- `S1 = sum of elements with '+' sign`
- `S2 = sum of elements with '-' sign`

We have:

```
S1 - S2 = target
S1 + S2 = totalSum
=> 2 * S1 = target + totalSum
=> S1 = (target + totalSum) / 2
```

Thus, reduce to **count number of subsets with sum = (target + totalSum) / 2**

---

### ⚠️ Important Conditions

- `target + totalSum` must be even
- Subset sum must be non-negative

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: arr = [1, 1, 2, 3], target = 1
Output: 3
Explanation: 3 ways to assign signs and get sum 1
```

#### ✅ Test Case 2:

```txt
Input: arr = [1], target = 1
Output: 1
Explanation: Only one way: +1
```

#### ✅ Test Case 3:

```txt
Input: arr = [1, 2, 3, 4, 5], target = 3
Output: 3
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

Use the subset sum idea:
Convert to count the number of subsets with sum = `(target + totalSum)/2`

---

#### 📘 Code

```js
function countWays(i, sum, arr) {
  if (i === 0) {
    if (sum === 0 && arr[0] === 0) return 2;
    if (sum === 0 || sum === arr[0]) return 1;
    return 0;
  }

  const notPick = countWays(i - 1, sum, arr);
  const pick = arr[i] <= sum ? countWays(i - 1, sum - arr[i], arr) : 0;

  return pick + notPick;
}

function targetSum(arr, target) {
  const total = arr.reduce((a, b) => a + b, 0);
  if ((total + target) % 2 !== 0) return 0;

  const sum = (total + target) / 2;
  return countWays(arr.length - 1, sum, arr);
}
```

---

#### ❌ Problems

- Exponential time
- Repeated calculations

---

#### ⏱ Complexity

- **Time**: O(2^n)
- **Space**: O(n)

---

### ✅ Approach 2: Memoization (Top-Down)

#### 🧠 Intuition

Use `dp[i][sum]` to store subproblem answers.

---

#### 📘 Code

```js
function countWays(i, sum, arr, dp) {
  if (i === 0) {
    if (sum === 0 && arr[0] === 0) return 2;
    if (sum === 0 || sum === arr[0]) return 1;
    return 0;
  }

  if (dp[i][sum] !== -1) return dp[i][sum];

  const notPick = countWays(i - 1, sum, arr, dp);
  const pick = arr[i] <= sum ? countWays(i - 1, sum - arr[i], arr, dp) : 0;

  return (dp[i][sum] = pick + notPick);
}

function targetSum(arr, target) {
  const total = arr.reduce((a, b) => a + b, 0);
  if ((total + target) % 2 !== 0 || total < Math.abs(target)) return 0;

  const sum = (total + target) / 2;
  const n = arr.length;
  const dp = Array.from({ length: n }, () => Array(sum + 1).fill(-1));
  return countWays(n - 1, sum, arr, dp);
}
```

---

#### ⏱ Complexity

- **Time**: O(n × sum)
- **Space**: O(n × sum + n)

---

### 🧮 Approach 3: Tabulation (Bottom-Up)

#### 🧠 Intuition

Build the solution from base cases using 2D table.

---

#### 📘 Code

```js
function targetSum(arr, target) {
  const total = arr.reduce((a, b) => a + b, 0);
  if ((total + target) % 2 !== 0 || total < Math.abs(target)) return 0;

  const sum = (total + target) / 2;
  const n = arr.length;
  const dp = Array.from({ length: n }, () => Array(sum + 1).fill(0));

  dp[0][0] = arr[0] === 0 ? 2 : 1;
  if (arr[0] !== 0 && arr[0] <= sum) dp[0][arr[0]] = 1;

  for (let i = 1; i < n; i++) {
    for (let s = 0; s <= sum; s++) {
      const notPick = dp[i - 1][s];
      const pick = arr[i] <= s ? dp[i - 1][s - arr[i]] : 0;
      dp[i][s] = pick + notPick;
    }
  }

  return dp[n - 1][sum];
}
```

---

#### ⏱ Complexity

- **Time**: O(n × sum)
- **Space**: O(n × sum)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

Only current and previous row needed — use 1D array.

---

#### 📘 Code

```js
function targetSum(arr, target) {
  const total = arr.reduce((a, b) => a + b, 0);
  if ((total + target) % 2 !== 0 || total < Math.abs(target)) return 0;

  const sum = (total + target) / 2;
  let prev = Array(sum + 1).fill(0);

  prev[0] = arr[0] === 0 ? 2 : 1;
  if (arr[0] !== 0 && arr[0] <= sum) prev[arr[0]] = 1;

  for (let i = 1; i < arr.length; i++) {
    const curr = Array(sum + 1).fill(0);
    curr[0] = 1;

    for (let s = 0; s <= sum; s++) {
      const notPick = prev[s];
      const pick = arr[i] <= s ? prev[s - arr[i]] : 0;
      curr[s] = pick + notPick;
    }

    prev = curr;
  }

  return prev[sum];
}
```

---

#### 🔍 Dry Run for `arr = [1, 1, 2, 3], target = 1`

```
total = 7 → sum = (7 + 1)/2 = 4
Count subsets with sum = 4 → Answer: 3
```

---

#### ⏱ Complexity

- **Time**: O(n × sum)
- **Space**: O(sum) ✅

---

### 📌 Summary Table

| Approach           | Time        | Space      | Notes                                 |
| ------------------ | ----------- | ---------- | ------------------------------------- |
| Recursion          | Exponential | O(n)       | Brute force                           |
| Memoization        | O(n × sum)  | O(n × sum) | Top-down DP                           |
| Tabulation         | O(n × sum)  | O(n × sum) | Bottom-up DP                          |
| Space Optimization | O(n × sum)  | O(sum) ✅  | Most efficient in both time and space |

---

## 🔢 **8. Coin Change 2**

### 📘 Problem Statement

You are given an array `coins[]` representing different denominations and an integer `amount`.
Return the **number of combinations** to make up that amount using **any number of coins**.

- You may **use the same coin** unlimited times (unbounded knapsack).
- The order of coins **does not matter** (i.e., 1+2 = 2+1 → only count once).

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: coins = [1, 2, 5], amount = 5
Output: 4
Explanation:
- 5
- 2 + 2 + 1
- 2 + 1 + 1 + 1
- 1 + 1 + 1 + 1 + 1
```

#### ✅ Test Case 2:

```txt
Input: coins = [2], amount = 3
Output: 0
Explanation: No combination possible
```

#### ✅ Test Case 3:

```txt
Input: coins = [10], amount = 10
Output: 1
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

Try to:

- **Pick** the coin (stay on same index because unlimited supply)
- **Not pick** the coin (go to next index)

---

#### 📘 Code

```js
function countWays(i, target, coins) {
  if (i === 0) {
    return target % coins[0] === 0 ? 1 : 0;
  }

  const notPick = countWays(i - 1, target, coins);
  const pick = coins[i] <= target ? countWays(i, target - coins[i], coins) : 0;

  return pick + notPick;
}

function coinChange2(coins, amount) {
  return countWays(coins.length - 1, amount, coins);
}
```

---

#### ❌ Problems

- **Exponential time**
- Repeats subproblems

---

#### ⏱ Complexity

- **Time**: O(2^amount)
- **Space**: O(amount)

---

### ✅ Approach 2: Memoization (Top-Down)

#### 🧠 Intuition

Use `dp[i][target]` to cache results and avoid recomputation.

---

#### 📘 Code

```js
function countWays(i, target, coins, dp) {
  if (i === 0) {
    return target % coins[0] === 0 ? 1 : 0;
  }

  if (dp[i][target] !== -1) return dp[i][target];

  const notPick = countWays(i - 1, target, coins, dp);
  const pick =
    coins[i] <= target ? countWays(i, target - coins[i], coins, dp) : 0;

  return (dp[i][target] = pick + notPick);
}

function coinChange2(coins, amount) {
  const n = coins.length;
  const dp = Array.from({ length: n }, () => Array(amount + 1).fill(-1));
  return countWays(n - 1, amount, coins, dp);
}
```

---

#### ⏱ Complexity

- **Time**: O(n × amount)
- **Space**: O(n × amount) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up)

#### 🧠 Intuition

Build a 2D DP table where `dp[i][t]` means:
**number of ways to make sum `t` using coins\[0..i]**

---

#### 📘 Code

```js
function coinChange2(coins, amount) {
  const n = coins.length;
  const dp = Array.from({ length: n }, () => Array(amount + 1).fill(0));

  // Base case
  for (let t = 0; t <= amount; t++) {
    if (t % coins[0] === 0) dp[0][t] = 1;
  }

  for (let i = 1; i < n; i++) {
    for (let t = 0; t <= amount; t++) {
      const notPick = dp[i - 1][t];
      const pick = coins[i] <= t ? dp[i][t - coins[i]] : 0;
      dp[i][t] = pick + notPick;
    }
  }

  return dp[n - 1][amount];
}
```

---

#### ⏱ Complexity

- **Time**: O(n × amount)
- **Space**: O(n × amount)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

Since we only need `prev` and `curr`, we can use 1D array.

---

#### 📘 Code

```js
function coinChange2(coins, amount) {
  const n = coins.length;
  let dp = Array(amount + 1).fill(0);

  // Base case: using first coin
  for (let t = 0; t <= amount; t++) {
    if (t % coins[0] === 0) dp[t] = 1;
  }

  for (let i = 1; i < n; i++) {
    const curr = Array(amount + 1).fill(0);
    for (let t = 0; t <= amount; t++) {
      const notPick = dp[t];
      const pick = coins[i] <= t ? curr[t - coins[i]] : 0;
      curr[t] = pick + notPick;
    }
    dp = curr;
  }

  return dp[amount];
}
```

---

#### 🔍 Dry Run for `coins = [1, 2, 5], amount = 5`

```
dp[5] = 4
Ways: [5], [2+2+1], [2+1+1+1], [1+1+1+1+1]
```

---

#### ⏱ Complexity

- **Time**: O(n × amount)
- **Space**: O(amount) ✅

---

### 📌 Summary Table

| Approach           | Time          | Space         | Notes                |
| ------------------ | ------------- | ------------- | -------------------- |
| Recursion          | Exponential   | O(amount)     | Brute force          |
| Memoization        | O(n × amount) | O(n × amount) | Top-down DP          |
| Tabulation         | O(n × amount) | O(n × amount) | Iterative            |
| Space Optimization | O(n × amount) | O(amount) ✅  | Best for large input |

---

## 🔢 **9. Unbounded Knapsack**

### 📘 Problem Statement

You're given:

- `n` items, each with a weight `wt[i]` and value `val[i]`
- A knapsack with maximum weight capacity `W`

Find the **maximum total value** you can obtain **by choosing items repeatedly** (i.e., each item can be picked **unlimited times**).

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: wt = [2, 4, 6], val = [5, 11, 13], W = 10
Output: 27
Explanation: Choose 2×[4 weight, 11 val] + 1×[2 weight, 5 val]
```

#### ✅ Test Case 2:

```txt
Input: wt = [1, 3, 4, 5], val = [10, 40, 50, 70], W = 8
Output: 110
Explanation: 2×[3, 40] + 1×[1, 10] = 40+40+10+10+10+10 = 110
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

At each item, we try:

- **Pick** the item (stay at same index since it's unbounded)
- **Skip** the item (go to previous index)

---

#### 📘 Code

```js
function unboundedKnapsack(i, W, wt, val) {
  if (i === 0) return Math.floor(W / wt[0]) * val[0];

  const notPick = unboundedKnapsack(i - 1, W, wt, val);
  const pick =
    wt[i] <= W ? val[i] + unboundedKnapsack(i, W - wt[i], wt, val) : -Infinity;

  return Math.max(pick, notPick);
}

function solveUnboundedKnapsack(wt, val, W) {
  return unboundedKnapsack(wt.length - 1, W, wt, val);
}
```

---

#### ❌ Problems

- Exponential time
- Overlapping subproblems

---

#### ⏱ Complexity

- **Time**: O(2^n)
- **Space**: O(W)

---

### ✅ Approach 2: Memoization (Top-Down)

#### 🧠 Intuition

Cache subproblem results using `dp[i][W]`.

---

#### 📘 Code

```js
function unboundedKnapsack(i, W, wt, val, dp) {
  if (i === 0) return Math.floor(W / wt[0]) * val[0];

  if (dp[i][W] !== -1) return dp[i][W];

  const notPick = unboundedKnapsack(i - 1, W, wt, val, dp);
  const pick =
    wt[i] <= W
      ? val[i] + unboundedKnapsack(i, W - wt[i], wt, val, dp)
      : -Infinity;

  return (dp[i][W] = Math.max(pick, notPick));
}

function solveUnboundedKnapsack(wt, val, W) {
  const n = wt.length;
  const dp = Array.from({ length: n }, () => Array(W + 1).fill(-1));
  return unboundedKnapsack(n - 1, W, wt, val, dp);
}
```

---

#### ⏱ Complexity

- **Time**: O(n × W)
- **Space**: O(n × W) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up)

#### 🧠 Intuition

Create `dp[n][W+1]` table.
`dp[i][w]` = max value for weight `w` using items `0...i`.

---

#### 📘 Code

```js
function solveUnboundedKnapsack(wt, val, W) {
  const n = wt.length;
  const dp = Array.from({ length: n }, () => Array(W + 1).fill(0));

  for (let w = 0; w <= W; w++) {
    dp[0][w] = Math.floor(w / wt[0]) * val[0];
  }

  for (let i = 1; i < n; i++) {
    for (let w = 0; w <= W; w++) {
      const notPick = dp[i - 1][w];
      const pick = wt[i] <= w ? val[i] + dp[i][w - wt[i]] : -Infinity;
      dp[i][w] = Math.max(pick, notPick);
    }
  }

  return dp[n - 1][W];
}
```

---

#### ⏱ Complexity

- **Time**: O(n × W)
- **Space**: O(n × W)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

We only need the **current row** → use 1D array (`dp[w]`).

---

#### 📘 Code

```js
function solveUnboundedKnapsack(wt, val, W) {
  const n = wt.length;
  const dp = Array(W + 1).fill(0);

  for (let w = 0; w <= W; w++) {
    dp[w] = Math.floor(w / wt[0]) * val[0];
  }

  for (let i = 1; i < n; i++) {
    for (let w = 0; w <= W; w++) {
      const pick = wt[i] <= w ? val[i] + dp[w - wt[i]] : -Infinity;
      dp[w] = Math.max(dp[w], pick);
    }
  }

  return dp[W];
}
```

---

#### 🔍 Dry Run (wt = \[2, 4, 6], val = \[5, 11, 13], W = 10)

```
dp[10] = max value with any number of items → 27
```

---

#### ⏱ Complexity

- **Time**: O(n × W)
- **Space**: O(W) ✅

---

### 📌 Summary Table

| Approach           | Time        | Space    | Notes                          |
| ------------------ | ----------- | -------- | ------------------------------ |
| Recursion          | Exponential | O(W)     | Brute force                    |
| Memoization        | O(n × W)    | O(n × W) | Top-down + caching             |
| Tabulation         | O(n × W)    | O(n × W) | Bottom-up iteration            |
| Space Optimization | O(n × W)    | O(W) ✅  | Best approach for large inputs |

---

## 🔢 **10. Rod Cutting Problem**

### 📘 Problem Statement

Given a rod of length `N` and an array `price[]` of size `N` where `price[i]` denotes the **price of a rod of length `i+1`**,
determine the **maximum total price** obtainable by cutting the rod into pieces **any number of times**.

✅ You can **cut the rod in any number of pieces**,
✅ And can reuse lengths (unbounded).

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: N = 4, price = [2, 5, 7, 8]
Output: 10
Explanation: 2 cuts of length 2 (price 5) → 5 + 5 = 10
```

#### ✅ Test Case 2:

```txt
Input: N = 5, price = [2, 5, 7, 8, 10]
Output: 12
Explanation: 2 cuts of length 2 + 1 cut of length 1 → 5 + 5 + 2 = 12
```

#### ✅ Test Case 3:

```txt
Input: N = 8, price = [1, 5, 8, 9, 10, 17, 17, 20]
Output: 22
Explanation: best is 2+6 cut → 5 + 17 = 22
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

Try all piece lengths (1 to N), and for each, either:

- **Pick it** → reduce rod length by that piece, keep index
- **Don't pick** → go to smaller index (i.e., smaller cut size)

---

#### 📘 Code

```js
function cutRodRec(i, length, price) {
  if (i === 0) return length * price[0];

  const notPick = cutRodRec(i - 1, length, price);
  const rodLength = i + 1;

  const pick =
    rodLength <= length
      ? price[i] + cutRodRec(i, length - rodLength, price)
      : -Infinity;

  return Math.max(pick, notPick);
}

function rodCutting(price, N) {
  return cutRodRec(price.length - 1, N, price);
}
```

---

#### ❌ Problems

- Recomputes subproblems
- **Exponential** in time

---

#### ⏱ Complexity

- **Time**: O(2^N)
- **Space**: O(N)

---

### ✅ Approach 2: Memoization (Top-Down)

#### 🧠 Intuition

Store results of subproblems: `dp[i][length] = max price`

---

#### 📘 Code

```js
function cutRodRec(i, length, price, dp) {
  if (i === 0) return length * price[0];
  if (dp[i][length] !== -1) return dp[i][length];

  const notPick = cutRodRec(i - 1, length, price, dp);
  const rodLength = i + 1;

  const pick =
    rodLength <= length
      ? price[i] + cutRodRec(i, length - rodLength, price, dp)
      : -Infinity;

  return (dp[i][length] = Math.max(pick, notPick));
}

function rodCutting(price, N) {
  const dp = Array.from({ length: N }, () => Array(N + 1).fill(-1));
  return cutRodRec(N - 1, N, price, dp);
}
```

---

#### ⏱ Complexity

- **Time**: O(N × N)
- **Space**: O(N × N) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up)

#### 🧠 Intuition

Build DP table where `dp[i][len]` = max price for rod of length `len` using cuts 0...i.

---

#### 📘 Code

```js
function rodCutting(price, N) {
  const dp = Array.from({ length: N }, () => Array(N + 1).fill(0));

  for (let len = 0; len <= N; len++) {
    dp[0][len] = len * price[0]; // only use piece of length 1
  }

  for (let i = 1; i < N; i++) {
    for (let len = 0; len <= N; len++) {
      const notPick = dp[i - 1][len];
      const rodLength = i + 1;
      const pick =
        rodLength <= len ? price[i] + dp[i][len - rodLength] : -Infinity;
      dp[i][len] = Math.max(pick, notPick);
    }
  }

  return dp[N - 1][N];
}
```

---

#### ⏱ Complexity

- **Time**: O(N²)
- **Space**: O(N²)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

We only need current and previous row → use 1D array

---

#### 📘 Code

```js
function rodCutting(price, N) {
  let dp = Array(N + 1).fill(0);

  for (let len = 0; len <= N; len++) {
    dp[len] = len * price[0];
  }

  for (let i = 1; i < N; i++) {
    for (let len = 0; len <= N; len++) {
      const rodLength = i + 1;
      const pick =
        rodLength <= len ? price[i] + dp[len - rodLength] : -Infinity;
      dp[len] = Math.max(dp[len], pick);
    }
  }

  return dp[N];
}
```

---

#### 🔍 Dry Run for `price = [2, 5, 7, 8], N = 4`:

```
dp[0...4] evolves as:
dp[4] = max value obtainable for length 4 = 10
```

---

#### ⏱ Complexity

- **Time**: O(N²)
- **Space**: O(N) ✅

---

### 📌 Summary Table

| Approach           | Time   | Space   | Notes                           |
| ------------------ | ------ | ------- | ------------------------------- |
| Recursion          | O(2^N) | O(N)    | Brute force                     |
| Memoization        | O(N²)  | O(N²)   | Top-down with caching           |
| Tabulation         | O(N²)  | O(N²)   | Bottom-up iterative             |
| Space Optimization | O(N²)  | O(N) ✅ | Most efficient for large inputs |

---

# Dp On Strings

## 🔢 **1. Longest Common Subsequence (LCS)**

### 📘 Problem Statement

Given two strings `text1` and `text2`, return the **length of their longest common subsequence**.

A **subsequence** of a string is a sequence that appears in the **same relative order**, but not necessarily contiguous.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: text1 = "abcde", text2 = "ace"
Output: 3
Explanation: LCS is "ace"
```

#### ✅ Test Case 2:

```txt
Input: text1 = "abc", text2 = "abc"
Output: 3
Explanation: LCS is "abc"
```

#### ✅ Test Case 3:

```txt
Input: text1 = "abc", text2 = "def"
Output: 0
Explanation: No common subsequence
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

Try comparing the last characters:

- If they match, we take 1 + LCS of remaining parts.
- If not, we skip one character from either string.

---

#### 📘 Code

```js
function lcs(i, j, text1, text2) {
  if (i < 0 || j < 0) return 0;

  if (text1[i] === text2[j]) {
    return 1 + lcs(i - 1, j - 1, text1, text2);
  } else {
    return Math.max(lcs(i - 1, j, text1, text2), lcs(i, j - 1, text1, text2));
  }
}

function longestCommonSubsequence(text1, text2) {
  return lcs(text1.length - 1, text2.length - 1, text1, text2);
}
```

---

#### ❌ Problems

- Exponential time (2^n)
- Overlaps subproblems heavily

---

#### ⏱ Complexity

- **Time**: O(2^min(n, m))
- **Space**: O(n + m) recursion stack

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Intuition

Store `dp[i][j] = LCS(text1[0..i], text2[0..j])`.

---

#### 📘 Code

```js
function lcs(i, j, text1, text2, dp) {
  if (i < 0 || j < 0) return 0;
  if (dp[i][j] !== -1) return dp[i][j];

  if (text1[i] === text2[j]) {
    return (dp[i][j] = 1 + lcs(i - 1, j - 1, text1, text2, dp));
  } else {
    return (dp[i][j] = Math.max(
      lcs(i - 1, j, text1, text2, dp),
      lcs(i, j - 1, text1, text2, dp)
    ));
  }
}

function longestCommonSubsequence(text1, text2) {
  const n = text1.length;
  const m = text2.length;
  const dp = Array.from({ length: n }, () => Array(m).fill(-1));
  return lcs(n - 1, m - 1, text1, text2, dp);
}
```

---

#### ⏱ Complexity

- **Time**: O(n × m)
- **Space**: O(n × m) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Build a table `dp[n+1][m+1]` where `dp[i][j]` is the LCS of first `i` chars of `text1` and first `j` of `text2`.

---

#### 📘 Code

```js
function longestCommonSubsequence(text1, text2) {
  const n = text1.length;
  const m = text2.length;
  const dp = Array.from({ length: n + 1 }, () => Array(m + 1).fill(0));

  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= m; j++) {
      if (text1[i - 1] === text2[j - 1]) {
        dp[i][j] = 1 + dp[i - 1][j - 1];
      } else {
        dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
      }
    }
  }

  return dp[n][m];
}
```

---

#### ⏱ Complexity

- **Time**: O(n × m)
- **Space**: O(n × m)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

We only need the **previous row** → use 2 arrays

---

#### 📘 Code

```js
function longestCommonSubsequence(text1, text2) {
  const n = text1.length;
  const m = text2.length;
  let prev = Array(m + 1).fill(0);
  let curr = Array(m + 1).fill(0);

  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= m; j++) {
      if (text1[i - 1] === text2[j - 1]) {
        curr[j] = 1 + prev[j - 1];
      } else {
        curr[j] = Math.max(prev[j], curr[j - 1]);
      }
    }
    [prev, curr] = [curr, prev]; // swap
  }

  return prev[m];
}
```

---

#### 🔍 Dry Run

For `text1 = "abcde"` and `text2 = "ace"`:

```
dp[5][3] → 3 (matches: a, c, e)
```

---

#### ⏱ Complexity

- **Time**: O(n × m)
- **Space**: O(m) ✅

---

### 📌 Summary Table

| Approach           | Time     | Space    | Notes                          |
| ------------------ | -------- | -------- | ------------------------------ |
| Recursion          | O(2^n)   | O(n + m) | Brute force                    |
| Memoization        | O(n × m) | O(n × m) | Top-down + caching             |
| Tabulation         | O(n × m) | O(n × m) | Iterative, easy to understand  |
| Space Optimization | O(n × m) | O(m) ✅  | Best approach for large inputs |

---

## 🔢 **2. Print Longest Common Subsequence**

### 📘 Problem Statement

Given two strings `text1` and `text2`, return the **Longest Common Subsequence (LCS)** string itself.

If multiple LCS exist, returning **any one** of them is acceptable.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: text1 = "abcde", text2 = "ace"
Output: "ace"
```

#### ✅ Test Case 2:

```txt
Input: text1 = "AGGTAB", text2 = "GXTXAYB"
Output: "GTAB"
```

#### ✅ Test Case 3:

```txt
Input: text1 = "abc", text2 = "def"
Output: ""
```

---

### 🚀 Approach: Tabulation + Backtracking

#### 🧠 Intuition

1. First build the LCS length table using bottom-up DP.
2. Then, **backtrack** from the bottom-right of the table:

   - If `text1[i-1] === text2[j-1]`, it's part of LCS → move diagonally.
   - Else move to the cell with the **larger value** (left or top).

---

#### 📘 Code

```js
function printLCS(text1, text2) {
  const n = text1.length;
  const m = text2.length;

  // Step 1: Create DP table
  const dp = Array.from({ length: n + 1 }, () => Array(m + 1).fill(0));

  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= m; j++) {
      if (text1[i - 1] === text2[j - 1]) {
        dp[i][j] = 1 + dp[i - 1][j - 1];
      } else {
        dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
      }
    }
  }

  // Step 2: Backtrack to build the LCS string
  let i = n,
    j = m;
  const lcs = [];

  while (i > 0 && j > 0) {
    if (text1[i - 1] === text2[j - 1]) {
      lcs.push(text1[i - 1]); // or text2[j - 1]
      i--;
      j--;
    } else if (dp[i - 1][j] > dp[i][j - 1]) {
      i--;
    } else {
      j--;
    }
  }

  return lcs.reverse().join("");
}
```

---

#### 🔍 Dry Run

For `text1 = "abcde"`, `text2 = "ace"`:

```
dp[5][3] = 3
Trace back: e → c → a ⇒ LCS = "ace"
```

---

#### ⏱ Complexity

- **Time**: O(n × m)
- **Space**: O(n × m)

---

#### ✅ Optional: Space Optimization (only for LCS **length**)

- You cannot optimize space and still backtrack **without full table**, so this version keeps the full table.

---

### 📌 Summary

| Step                 | Description                     |
| -------------------- | ------------------------------- |
| Build DP Table       | O(n × m) using LCS recurrence   |
| Backtrack LCS String | From dp\[n]\[m] to dp\[0]\[0]   |
| Final Output         | The LCS string in correct order |

---

## 🔢 **3. Longest Common Substring**

### 📘 Problem Statement

Given two strings `text1` and `text2`, return the **length of the longest common substring**.
A **substring** is a sequence of characters that appears **contiguously** in both strings.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: text1 = "abcde", text2 = "abfce"
Output: 2
Explanation: "ab" is the longest common substring
```

#### ✅ Test Case 2:

```txt
Input: text1 = "abcdef", text2 = "zcdemf"
Output: 3
Explanation: "cde"
```

#### ✅ Test Case 3:

```txt
Input: text1 = "abc", text2 = "xyz"
Output: 0
Explanation: No common substring
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

Try every pair `(i, j)` of positions.

- If characters match → 1 + recurse to `(i-1, j-1)`
- Else → start fresh from 0.

Keep track of maximum match length globally.

---

#### 📘 Code

```js
function longestCommonSubstringRec(i, j, count, text1, text2) {
  if (i < 0 || j < 0) return count;

  if (text1[i] === text2[j]) {
    count = longestCommonSubstringRec(i - 1, j - 1, count + 1, text1, text2);
  }

  const skip1 = longestCommonSubstringRec(i - 1, j, 0, text1, text2);
  const skip2 = longestCommonSubstringRec(i, j - 1, 0, text1, text2);

  return Math.max(count, skip1, skip2);
}

function longestCommonSubstring(text1, text2) {
  const n = text1.length,
    m = text2.length;
  return longestCommonSubstringRec(n - 1, m - 1, 0, text1, text2);
}
```

---

#### ❌ Problems

- Time complexity is **exponential**
- Redundant overlapping calls

---

#### ⏱ Complexity

- **Time**: O(2^(n+m))
- **Space**: O(n + m) (recursion depth)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Intuition

Cache the results of `(i, j)` when `count = 0`.
We can’t memoize on `count`, so we'll return and update a `maxLen` externally.

---

#### 📘 Code

```js
function longestCommonSubstring(text1, text2) {
  const n = text1.length,
    m = text2.length;
  const dp = Array.from({ length: n }, () => Array(m).fill(-1));
  let maxLen = 0;

  function solve(i, j) {
    if (i < 0 || j < 0) return 0;

    if (dp[i][j] !== -1) return dp[i][j];

    if (text1[i] === text2[j]) {
      dp[i][j] = 1 + solve(i - 1, j - 1);
      maxLen = Math.max(maxLen, dp[i][j]);
    } else {
      dp[i][j] = 0;
    }

    // Still make calls to check all possibilities
    solve(i - 1, j);
    solve(i, j - 1);

    return dp[i][j];
  }

  solve(n - 1, m - 1);
  return maxLen;
}
```

---

#### ⏱ Complexity

- **Time**: O(n × m)
- **Space**: O(n × m) + recursion

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Create a `dp[n+1][m+1]` table
`dp[i][j]` stores length of common substring ending at `text1[i-1]` and `text2[j-1]`.

---

#### 📘 Code

```js
function longestCommonSubstring(text1, text2) {
  const n = text1.length,
    m = text2.length;
  const dp = Array.from({ length: n + 1 }, () => Array(m + 1).fill(0));
  let maxLen = 0;

  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= m; j++) {
      if (text1[i - 1] === text2[j - 1]) {
        dp[i][j] = 1 + dp[i - 1][j - 1];
        maxLen = Math.max(maxLen, dp[i][j]);
      } else {
        dp[i][j] = 0;
      }
    }
  }

  return maxLen;
}
```

---

#### 🔍 Dry Run

For `text1 = "abcde"`, `text2 = "abfce"`:

```
dp[2][2] = 2 ("ab")
dp[3][4] = 1 ("c")
dp[4][5] = 2 ("de")
→ max = 2
```

---

#### ⏱ Complexity

- **Time**: O(n × m)
- **Space**: O(n × m)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

Use two 1D arrays: `prev` and `curr`, as only `i-1` row is needed.

---

#### 📘 Code

```js
function longestCommonSubstring(text1, text2) {
  const n = text1.length,
    m = text2.length;
  let prev = Array(m + 1).fill(0),
    curr = Array(m + 1).fill(0);
  let maxLen = 0;

  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= m; j++) {
      if (text1[i - 1] === text2[j - 1]) {
        curr[j] = 1 + prev[j - 1];
        maxLen = Math.max(maxLen, curr[j]);
      } else {
        curr[j] = 0;
      }
    }
    [prev, curr] = [curr, prev]; // swap
  }

  return maxLen;
}
```

---

#### ⏱ Complexity

- **Time**: O(n × m)
- **Space**: O(m) ✅

---

### 📌 Summary Table

| Approach           | Time     | Space    | Notes                  |
| ------------------ | -------- | -------- | ---------------------- |
| Recursion          | O(2^n)   | O(n + m) | Brute force, slow      |
| Memoization        | O(n × m) | O(n × m) | Top-down + caching     |
| Tabulation         | O(n × m) | O(n × m) | Iterative, efficient   |
| Space Optimization | O(n × m) | O(m) ✅  | Best in time and space |

---

## 🔢 **4. Longest Palindromic Subsequence**

### 📘 Problem Statement

Given a string `s`, return the **length of the longest subsequence** of `s` that is also a **palindrome**.

A **subsequence** doesn't need to be contiguous, but characters must appear in order.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: s = "bbbab"
Output: 4
Explanation: One LPS is "bbbb"
```

#### ✅ Test Case 2:

```txt
Input: s = "cbbd"
Output: 2
Explanation: One LPS is "bb"
```

#### ✅ Test Case 3:

```txt
Input: s = "abc"
Output: 1
Explanation: Each character itself is a palindrome
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

Check:

- If `s[i] === s[j]` → include both ends: `2 + f(i+1, j-1)`
- Else → take max of skipping either end.

---

#### 📘 Code

```js
function lps(i, j, s) {
  if (i > j) return 0;
  if (i === j) return 1;

  if (s[i] === s[j]) {
    return 2 + lps(i + 1, j - 1, s);
  } else {
    return Math.max(lps(i + 1, j, s), lps(i, j - 1, s));
  }
}

function longestPalindromicSubsequence(s) {
  return lps(0, s.length - 1, s);
}
```

---

#### ❌ Problems

- Many subproblems are recomputed
- Exponential growth

---

#### ⏱ Complexity

- **Time**: O(2^n)
- **Space**: O(n) (recursion stack)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Intuition

Memoize results using `dp[i][j]` to store LPS length in `s[i...j]`.

---

#### 📘 Code

```js
function longestPalindromicSubsequence(s) {
  const n = s.length;
  const dp = Array.from({ length: n }, () => Array(n).fill(-1));

  function lps(i, j) {
    if (i > j) return 0;
    if (i === j) return 1;
    if (dp[i][j] !== -1) return dp[i][j];

    if (s[i] === s[j]) {
      dp[i][j] = 2 + lps(i + 1, j - 1);
    } else {
      dp[i][j] = Math.max(lps(i + 1, j), lps(i, j - 1));
    }
    return dp[i][j];
  }

  return lps(0, n - 1);
}
```

---

#### ⏱ Complexity

- **Time**: O(n × n)
- **Space**: O(n × n) + recursion

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Start filling for substrings of increasing length.

`dp[i][j] = LPS in s[i...j]`

---

#### 📘 Code

```js
function longestPalindromicSubsequence(s) {
  const n = s.length;
  const dp = Array.from({ length: n }, () => Array(n).fill(0));

  // Every single character is a palindrome of length 1
  for (let i = 0; i < n; i++) {
    dp[i][i] = 1;
  }

  // Fill the table
  for (let len = 2; len <= n; len++) {
    for (let i = 0; i <= n - len; i++) {
      let j = i + len - 1;
      if (s[i] === s[j]) {
        dp[i][j] = 2 + dp[i + 1][j - 1];
      } else {
        dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
      }
    }
  }

  return dp[0][n - 1];
}
```

---

#### 🔍 Dry Run

For `s = "bbbab"`:

```
dp[0][4] = 4 ("bbbb")
dp[0][3] = 3 ("bbb")
...
```

---

#### ⏱ Complexity

- **Time**: O(n × n)
- **Space**: O(n × n)

---

### 🧊 Approach 4: Space Optimization

#### 🧠 Intuition

Can optimize space by keeping only two diagonals: `curr` and `prev`.

⚠️ Slightly tricky because we rely on `dp[i+1][j-1]`, so full optimization isn't straightforward.
But we can optimize partially using 1D arrays (like LCS) if needed.

However, **in practice** we usually keep the 2D table to **reconstruct the sequence** if needed.

---

#### ✅ Alternate Trick

You can solve LPS using **LCS** between `s` and `reverse(s)`!

```js
function longestPalindromicSubsequence(s) {
  const t = s.split("").reverse().join("");
  const n = s.length;
  const dp = Array.from({ length: n + 1 }, () => Array(n + 1).fill(0));

  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= n; j++) {
      if (s[i - 1] === t[j - 1]) {
        dp[i][j] = 1 + dp[i - 1][j - 1];
      } else {
        dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
      }
    }
  }

  return dp[n][n];
}
```

---

### 📌 Summary Table

| Approach               | Time     | Space    | Notes                          |
| ---------------------- | -------- | -------- | ------------------------------ |
| Recursion              | O(2^n)   | O(n)     | Exponential, slow              |
| Memoization (Top-Down) | O(n × n) | O(n × n) | Stores overlapping subproblems |
| Tabulation (Bottom-Up) | O(n × n) | O(n × n) | Iterative, easy to track       |
| LCS Trick (s vs rev)   | O(n × n) | O(n × n) | Clean, elegant alternative     |

---

## 🔢 **5. Minimum Insertions to Make String a Palindrome (DP-29)**

### 📘 Problem Statement

Given a string `s`, return the **minimum number of insertions** needed to make `s` a palindrome.

👉 You can insert characters **anywhere** in the string.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: "abcaa"
Output: 1
Explanation: Insert 'b' at the end → "abcaab"
```

#### ✅ Test Case 2:

```txt
Input: "aebcbda"
Output: 2
Explanation: Insert 'd' and 'a' → "adbecbda"
```

#### ✅ Test Case 3:

```txt
Input: "race"
Output: 3
Explanation: Insert "e", "c", and "a" → "ecarace"
```

---

##@ 🚀 Key Insight

The **minimum insertions = Total length - Length of Longest Palindromic Subsequence (LPS)**

Because:

- A palindrome = string where `s[i] == s[n-1-i]`
- So if you find the longest subsequence that’s already a palindrome, the rest **must be fixed** using insertions

---

### ✅ Approach 1: LPS via Recursion

#### 🧠 Intuition

Find the LPS length recursively, then subtract from string length.

---

#### 📘 Code

```js
function lps(i, j, s) {
  if (i > j) return 0;
  if (i === j) return 1;

  if (s[i] === s[j]) {
    return 2 + lps(i + 1, j - 1, s);
  } else {
    return Math.max(lps(i + 1, j, s), lps(i, j - 1, s));
  }
}

function minInsertions(s) {
  const n = s.length;
  const len = lps(0, n - 1, s);
  return n - len;
}
```

---

#### ⏱ Complexity

- **Time**: O(2^n)
- **Space**: O(n)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Intuition

Memoize the recursive calls using `dp[i][j]`.

---

#### 📘 Code

```js
function minInsertions(s) {
  const n = s.length;
  const dp = Array.from({ length: n }, () => Array(n).fill(-1));

  function lps(i, j) {
    if (i > j) return 0;
    if (i === j) return 1;
    if (dp[i][j] !== -1) return dp[i][j];

    if (s[i] === s[j]) {
      dp[i][j] = 2 + lps(i + 1, j - 1);
    } else {
      dp[i][j] = Math.max(lps(i + 1, j), lps(i, j - 1));
    }
    return dp[i][j];
  }

  return n - lps(0, n - 1);
}
```

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(n²)

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Use a 2D `dp[i][j]` to store LPS of `s[i...j]`.
Then `minInsertions = n - dp[0][n-1]`

---

#### 📘 Code

```js
function minInsertions(s) {
  const n = s.length;
  const dp = Array.from({ length: n }, () => Array(n).fill(0));

  for (let i = 0; i < n; i++) {
    dp[i][i] = 1;
  }

  for (let len = 2; len <= n; len++) {
    for (let i = 0; i <= n - len; i++) {
      let j = i + len - 1;
      if (s[i] === s[j]) {
        dp[i][j] = 2 + dp[i + 1][j - 1];
      } else {
        dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
      }
    }
  }

  return n - dp[0][n - 1];
}
```

---

#### 🔍 Dry Run

For `s = "aebcbda"`:

```
LPS = "abcba" → length 5
Insertions = 7 - 5 = 2
```

---

### 🧊 Approach 4: Space Optimization (Using LCS Trick)

#### 🧠 Intuition

LPS(s) = LCS(s, reverse(s))
So use **1D DP for LCS** of `s` and `rev(s)`

---

#### 📘 Code

```js
function minInsertions(s) {
  const n = s.length;
  const rev = s.split("").reverse().join("");
  let prev = Array(n + 1).fill(0),
    curr = Array(n + 1).fill(0);

  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= n; j++) {
      if (s[i - 1] === rev[j - 1]) {
        curr[j] = 1 + prev[j - 1];
      } else {
        curr[j] = Math.max(prev[j], curr[j - 1]);
      }
    }
    [prev, curr] = [curr, prev];
  }

  return n - prev[n];
}
```

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(n) ✅

---

### 📌 Summary Table

| Approach             | Time   | Space   | Notes                        |
| -------------------- | ------ | ------- | ---------------------------- |
| Recursion            | O(2^n) | O(n)    | Brute force                  |
| Memoization          | O(n²)  | O(n²)   | Top-down DP                  |
| Tabulation           | O(n²)  | O(n²)   | Bottom-up, stable            |
| LCS Trick + 1D space | O(n²)  | O(n) ✅ | Best space-efficient version |

---

## 🔢 **6. Minimum Insertions/Deletions to Convert String A to B**

### 📘 Problem Statement

Given two strings `str1` and `str2`, find the **minimum number of insertions and deletions** required to convert `str1` into `str2`.

✅ **Allowed operations**:

- You can **insert** any character into `str1`
- You can **delete** any character from `str1`
  🔴 **You CANNOT replace** characters.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: str1 = "heap", str2 = "pea"
Output: 3
Explanation:
LCS = "ea" → Delete 'h', 'p', Insert 'p' → 2 deletions + 1 insertion
```

#### ✅ Test Case 2:

```txt
Input: str1 = "abcdef", str2 = "ace"
Output: 3
Explanation:
LCS = "ace" → Delete 'b', 'd', 'f'
```

---

### 🔑 Key Insight: Use **LCS**

Let:

- `n = str1.length`
- `m = str2.length`
- `lcsLen = length of Longest Common Subsequence(str1, str2)`

Then:

- **Minimum Deletions** = `n - lcsLen`
- **Minimum Insertions** = `m - lcsLen`

---

### ✅ Approach 1: Recursion (LCS Based)

#### 🧠 Intuition

First write the recursive LCS function → subtract from lengths to get required ops.

---

#### 📘 Code

```js
function lcs(i, j, s1, s2) {
  if (i < 0 || j < 0) return 0;
  if (s1[i] === s2[j]) return 1 + lcs(i - 1, j - 1, s1, s2);
  return Math.max(lcs(i - 1, j, s1, s2), lcs(i, j - 1, s1, s2));
}

function minInsDel(str1, str2) {
  const lcsLen = lcs(str1.length - 1, str2.length - 1, str1, str2);
  return {
    insertions: str2.length - lcsLen,
    deletions: str1.length - lcsLen,
  };
}
```

---

#### ⏱ Complexity

- **Time**: O(2^(n+m))
- **Space**: O(n + m)

---

### ✅ Approach 2: Memoization (Top-Down)

#### 📘 Code

```js
function minInsDel(str1, str2) {
  const n = str1.length,
    m = str2.length;
  const dp = Array.from({ length: n }, () => Array(m).fill(-1));

  function lcs(i, j) {
    if (i < 0 || j < 0) return 0;
    if (dp[i][j] !== -1) return dp[i][j];

    if (str1[i] === str2[j]) {
      return (dp[i][j] = 1 + lcs(i - 1, j - 1));
    }
    return (dp[i][j] = Math.max(lcs(i - 1, j), lcs(i, j - 1)));
  }

  const lcsLen = lcs(n - 1, m - 1);

  return {
    insertions: m - lcsLen,
    deletions: n - lcsLen,
  };
}
```

---

#### ⏱ Complexity

- **Time**: O(n × m)
- **Space**: O(n × m) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up)

#### 📘 Code

```js
function minInsDel(str1, str2) {
  const n = str1.length,
    m = str2.length;
  const dp = Array.from({ length: n + 1 }, () => Array(m + 1).fill(0));

  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= m; j++) {
      if (str1[i - 1] === str2[j - 1]) {
        dp[i][j] = 1 + dp[i - 1][j - 1];
      } else {
        dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
      }
    }
  }

  const lcsLen = dp[n][m];
  return {
    insertions: m - lcsLen,
    deletions: n - lcsLen,
  };
}
```

---

### 🧊 Approach 4: Space Optimization

#### 📘 Code

```js
function minInsDel(str1, str2) {
  const n = str1.length,
    m = str2.length;
  let prev = Array(m + 1).fill(0),
    curr = Array(m + 1).fill(0);

  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= m; j++) {
      if (str1[i - 1] === str2[j - 1]) {
        curr[j] = 1 + prev[j - 1];
      } else {
        curr[j] = Math.max(prev[j], curr[j - 1]);
      }
    }
    [prev, curr] = [curr, prev];
  }

  const lcsLen = prev[m];
  return {
    insertions: m - lcsLen,
    deletions: n - lcsLen,
  };
}
```

---

### 🔍 Dry Run (str1 = "heap", str2 = "pea")

- LCS = "ea" → length 2
- Insertions = 3 - 2 = 1
- Deletions = 4 - 2 = 2

✅ Total operations = **3**

---

### 📌 Summary Table

| Approach        | Time     | Space    | Notes                                   |
| --------------- | -------- | -------- | --------------------------------------- |
| Recursion       | O(2^n)   | O(n)     | Exponential, not suitable for big input |
| Memoization     | O(n × m) | O(n × m) | Top-down with caching                   |
| Tabulation      | O(n × m) | O(n × m) | Easy to debug, bottom-up                |
| Space Optimized | O(n × m) | O(m) ✅  | Efficient and clean                     |

---

## 🔢 **7. Shortest Common Supersequence**

### 📘 Problem Statement

Given two strings `str1` and `str2`, return the **length** of the **shortest string** that has both `str1` and `str2` as **subsequences**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: str1 = "brute", str2 = "groot"
Output: 7
Explanation: SCS = "brugrootte" or "brguroote" → length = 7
```

#### ✅ Test Case 2:

```txt
Input: str1 = "abc", str2 = "ac"
Output: 3
Explanation: SCS = "abc"
```

#### ✅ Test Case 3:

```txt
Input: str1 = "geek", str2 = "eke"
Output: 5
Explanation: SCS = "geeke" or "gekke"
```

---

### 💡 Key Insight

We want the **shortest string** that **contains both `str1` and `str2` as subsequences**.

The idea is to **merge** both strings but **avoid repeating** common characters.

Let:

- `len1 = str1.length`
- `len2 = str2.length`
- `LCS = Longest Common Subsequence of str1 and str2`

Then:

```
Length of SCS = len1 + len2 - LCS
```

---

### ✅ Approach 1: Recursion for LCS

#### 🧠 Intuition

Recursively compute LCS, then apply the formula.

---

#### 📘 Code

```js
function lcs(i, j, s1, s2) {
  if (i < 0 || j < 0) return 0;
  if (s1[i] === s2[j]) return 1 + lcs(i - 1, j - 1, s1, s2);
  return Math.max(lcs(i - 1, j, s1, s2), lcs(i, j - 1, s1, s2));
}

function shortestCommonSupersequence(str1, str2) {
  const len1 = str1.length;
  const len2 = str2.length;
  const lcsLen = lcs(len1 - 1, len2 - 1, str1, str2);
  return len1 + len2 - lcsLen;
}
```

---

#### ⏱ Complexity

- **Time**: O(2^n)
- **Space**: O(n)

---

### ✅ Approach 2: Memoization (Top-Down DP)

---

#### 📘 Code

```js
function shortestCommonSupersequence(str1, str2) {
  const n = str1.length,
    m = str2.length;
  const dp = Array.from({ length: n }, () => Array(m).fill(-1));

  function lcs(i, j) {
    if (i < 0 || j < 0) return 0;
    if (dp[i][j] !== -1) return dp[i][j];
    if (str1[i] === str2[j]) return (dp[i][j] = 1 + lcs(i - 1, j - 1));
    return (dp[i][j] = Math.max(lcs(i - 1, j), lcs(i, j - 1)));
  }

  const lcsLen = lcs(n - 1, m - 1);
  return n + m - lcsLen;
}
```

---

#### ⏱ Complexity

- **Time**: O(n × m)
- **Space**: O(n × m) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up)

---

#### 📘 Code

```js
function shortestCommonSupersequence(str1, str2) {
  const n = str1.length,
    m = str2.length;
  const dp = Array.from({ length: n + 1 }, () => Array(m + 1).fill(0));

  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= m; j++) {
      if (str1[i - 1] === str2[j - 1]) {
        dp[i][j] = 1 + dp[i - 1][j - 1];
      } else {
        dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
      }
    }
  }

  const lcsLen = dp[n][m];
  return n + m - lcsLen;
}
```

---

### 🧊 Approach 4: Space Optimization (if only length needed)

---

#### 📘 Code

```js
function shortestCommonSupersequence(str1, str2) {
  const n = str1.length,
    m = str2.length;
  let prev = Array(m + 1).fill(0),
    curr = Array(m + 1).fill(0);

  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= m; j++) {
      if (str1[i - 1] === str2[j - 1]) {
        curr[j] = 1 + prev[j - 1];
      } else {
        curr[j] = Math.max(prev[j], curr[j - 1]);
      }
    }
    [prev, curr] = [curr, prev];
  }

  const lcsLen = prev[m];
  return n + m - lcsLen;
}
```

---

### 🔍 Dry Run

For `str1 = "brute"` and `str2 = "groot"`:

- LCS = "rt"
- len1 = 5, len2 = 5
- SCS length = 5 + 5 - 2 = 8

---

### 📌 Summary Table

| Approach               | Time     | Space    | Notes                        |
| ---------------------- | -------- | -------- | ---------------------------- |
| Recursion              | O(2^n)   | O(n)     | Exponential, brute force     |
| Memoization (Top-Down) | O(n × m) | O(n × m) | Efficient with caching       |
| Tabulation (Bottom-Up) | O(n × m) | O(n × m) | Preferred approach           |
| Space Optimized        | O(n × m) | O(m) ✅  | Best for length-only version |

---

## 🔢 **8. Distinct Subsequences (DP-32)**

### 📘 Problem Statement

Given two strings `s` and `t`, return the **number of distinct subsequences** of `s` which equal `t`.

> A subsequence of a string is formed by deleting **0 or more characters** without changing the order of the remaining characters.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: s = "rabbbit", t = "rabbit"
Output: 3
Explanation:
There are 3 ways to delete a 'b' to make "rabbbit" → "rabbit"
```

#### ✅ Test Case 2:

```txt
Input: s = "babgbag", t = "bag"
Output: 5
Explanation:
Ways: b**a**g, b**a**g, b**g**a**g, b**a**b**g, etc.
```

#### ✅ Test Case 3:

```txt
Input: s = "abcde", t = "ace"
Output: 1
```

---

### ✅ Approach 1: Recursion

#### 🧠 Intuition

We try to match characters one by one:

- If `s[i] === t[j]`, we can **either take it or skip it**.
- If they don’t match, we **must skip** `s[i]`.

---

#### 📘 Code

```js
function countWays(i, j, s, t) {
  if (j < 0) return 1; // matched all of t
  if (i < 0) return 0; // s exhausted, t not matched

  if (s[i] === t[j]) {
    return countWays(i - 1, j - 1, s, t) + countWays(i - 1, j, s, t);
  } else {
    return countWays(i - 1, j, s, t);
  }
}

function numDistinct(s, t) {
  return countWays(s.length - 1, t.length - 1, s, t);
}
```

---

#### ❌ Problems

- Exponential time due to overlapping subproblems

---

#### ⏱ Complexity

- **Time**: O(2^n)
- **Space**: O(n + m)

---

### ✅ Approach 2: Memoization (Top-Down)

#### 📘 Code

```js
function numDistinct(s, t) {
  const n = s.length,
    m = t.length;
  const dp = Array.from({ length: n }, () => Array(m).fill(-1));

  function countWays(i, j) {
    if (j < 0) return 1;
    if (i < 0) return 0;
    if (dp[i][j] !== -1) return dp[i][j];

    if (s[i] === t[j]) {
      return (dp[i][j] = countWays(i - 1, j - 1) + countWays(i - 1, j));
    } else {
      return (dp[i][j] = countWays(i - 1, j));
    }
  }

  return countWays(n - 1, m - 1);
}
```

---

#### ⏱ Complexity

- **Time**: O(n × m)
- **Space**: O(n × m) + recursion

---

### 🧮 Approach 3: Tabulation (Bottom-Up)

---

#### 📘 Code

```js
function numDistinct(s, t) {
  const n = s.length,
    m = t.length;
  const dp = Array.from({ length: n + 1 }, () => Array(m + 1).fill(0));

  for (let i = 0; i <= n; i++) dp[i][0] = 1; // empty t can always be matched

  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= m; j++) {
      if (s[i - 1] === t[j - 1]) {
        dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j];
      } else {
        dp[i][j] = dp[i - 1][j];
      }
    }
  }

  return dp[n][m];
}
```

---

### 🧊 Approach 4: Space Optimization

---

#### 📘 Code

```js
function numDistinct(s, t) {
  const n = s.length,
    m = t.length;
  let prev = Array(m + 1).fill(0);
  prev[0] = 1;

  for (let i = 1; i <= n; i++) {
    let curr = Array(m + 1).fill(0);
    curr[0] = 1;
    for (let j = 1; j <= m; j++) {
      if (s[i - 1] === t[j - 1]) {
        curr[j] = prev[j - 1] + prev[j];
      } else {
        curr[j] = prev[j];
      }
    }
    prev = curr;
  }

  return prev[m];
}
```

---

#### 🔍 Dry Run (s = "rabbbit", t = "rabbit")

- LCS = rabbit
- Ways to form "rabbit" from "rabbbit" = 3

---

### 📌 Summary Table

| Approach           | Time     | Space    | Notes                            |
| ------------------ | -------- | -------- | -------------------------------- |
| Recursion          | O(2^n)   | O(n)     | Brute-force, too slow            |
| Memoization        | O(n × m) | O(n × m) | Top-down with caching            |
| Tabulation         | O(n × m) | O(n × m) | Bottom-up and intuitive          |
| Space Optimization | O(n × m) | O(m) ✅  | Best choice for space efficiency |

---

## 🔢 **9. Edit Distance (DP-33)**

### 📘 Problem Statement

Given two strings `str1` and `str2`, return the **minimum number of operations** required to convert `str1` into `str2`.

✅ **Allowed operations**:

- **Insert**
- **Delete**
- **Replace**

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: str1 = "horse", str2 = "ros"
Output: 3
Explanation: horse → rorse → rose → ros
```

#### ✅ Test Case 2:

```txt
Input: str1 = "intention", str2 = "execution"
Output: 5
Explanation: Replace 'i'→'e', 'n'→'x', etc.
```

#### ✅ Test Case 3:

```txt
Input: str1 = "ab", str2 = "abc"
Output: 1
Explanation: Insert 'c'
```

---

### ✅ Approach 1: Recursion

#### 🧠 Intuition

Try all 3 operations at every mismatch:

- If characters match: move diagonally
- Else: min of

  - Insert → `i, j-1`
  - Delete → `i-1, j`
  - Replace → `i-1, j-1`

---

#### 📘 Code

```js
function editDist(i, j, s1, s2) {
  if (i < 0) return j + 1; // need to insert all of s2[0..j]
  if (j < 0) return i + 1; // need to delete all of s1[0..i]

  if (s1[i] === s2[j]) return editDist(i - 1, j - 1, s1, s2);

  return (
    1 +
    Math.min(
      editDist(i, j - 1, s1, s2), // Insert
      editDist(i - 1, j, s1, s2), // Delete
      editDist(i - 1, j - 1, s1, s2) // Replace
    )
  );
}

function minDistance(str1, str2) {
  return editDist(str1.length - 1, str2.length - 1, str1, str2);
}
```

---

#### ⏱ Complexity

- **Time**: O(3^n)
- **Space**: O(n + m)

---

### ✅ Approach 2: Memoization (Top-Down DP)

---

#### 📘 Code

```js
function minDistance(str1, str2) {
  const n = str1.length,
    m = str2.length;
  const dp = Array.from({ length: n }, () => Array(m).fill(-1));

  function editDist(i, j) {
    if (i < 0) return j + 1;
    if (j < 0) return i + 1;
    if (dp[i][j] !== -1) return dp[i][j];

    if (str1[i] === str2[j]) {
      return (dp[i][j] = editDist(i - 1, j - 1));
    }

    return (dp[i][j] =
      1 +
      Math.min(
        editDist(i, j - 1), // Insert
        editDist(i - 1, j), // Delete
        editDist(i - 1, j - 1) // Replace
      ));
  }

  return editDist(n - 1, m - 1);
}
```

---

#### ⏱ Complexity

- **Time**: O(n × m)
- **Space**: O(n × m) + recursion

---

### 🧮 Approach 3: Tabulation (Bottom-Up)

---

#### 📘 Code

```js
function minDistance(str1, str2) {
  const n = str1.length,
    m = str2.length;
  const dp = Array.from({ length: n + 1 }, () => Array(m + 1).fill(0));

  for (let i = 0; i <= n; i++) dp[i][0] = i;
  for (let j = 0; j <= m; j++) dp[0][j] = j;

  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= m; j++) {
      if (str1[i - 1] === str2[j - 1]) {
        dp[i][j] = dp[i - 1][j - 1];
      } else {
        dp[i][j] =
          1 +
          Math.min(
            dp[i][j - 1], // Insert
            dp[i - 1][j], // Delete
            dp[i - 1][j - 1] // Replace
          );
      }
    }
  }

  return dp[n][m];
}
```

---

### 🧊 Approach 4: Space Optimization

---

#### 📘 Code

```js
function minDistance(str1, str2) {
  const n = str1.length,
    m = str2.length;
  let prev = Array(m + 1).fill(0),
    curr = Array(m + 1).fill(0);

  for (let j = 0; j <= m; j++) prev[j] = j;

  for (let i = 1; i <= n; i++) {
    curr[0] = i;
    for (let j = 1; j <= m; j++) {
      if (str1[i - 1] === str2[j - 1]) {
        curr[j] = prev[j - 1];
      } else {
        curr[j] =
          1 +
          Math.min(
            curr[j - 1], // Insert
            prev[j], // Delete
            prev[j - 1] // Replace
          );
      }
    }
    [prev, curr] = [curr, prev];
  }

  return prev[m];
}
```

---

#### 🔍 Dry Run (str1 = "horse", str2 = "ros")

```txt
LCS not enough, so we check ops:
"horse" → "ros"
1. Replace 'h' → 'r'
2. Remove 'e'
3. Remove 'o'

Answer: 3
```

---

### 📌 Summary Table

| Approach           | Time     | Space    | Notes                         |
| ------------------ | -------- | -------- | ----------------------------- |
| Recursion          | O(3^n)   | O(n + m) | Too slow for large input      |
| Memoization        | O(n × m) | O(n × m) | Top-down with caching         |
| Tabulation         | O(n × m) | O(n × m) | Bottom-up, intuitive and fast |
| Space Optimization | O(n × m) | O(m) ✅  | Most optimal                  |

---

## 🔢 **10. Wildcard Matching (DP-34)**

### 📘 Problem Statement

You're given two strings:

- `s` → the input string
- `p` → the pattern string, which may include:

  - `'?'` matches any **single character**
  - `'*'` matches **any sequence of characters**, including empty

Return `true` if the **entire string `s` matches the pattern `p`**, otherwise `false`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: s = "adceb", p = "*a*b"
Output: true
```

#### ✅ Test Case 2:

```txt
Input: s = "aa", p = "a"
Output: false
```

#### ✅ Test Case 3:

```txt
Input: s = "cb", p = "?a"
Output: false
```

#### ✅ Test Case 4:

```txt
Input: s = "abcabczzzde", p = "*abc???de*"
Output: true
```

---

### ✅ Approach 1: Recursion

#### 🧠 Intuition

- If `s[i] === p[j]` or `p[j] === '?'`: move both pointers back.
- If `p[j] === '*'`: try both:

  - Match 0 characters → move `j - 1`
  - Match 1 character from `s` → move `i - 1`

---

#### 📘 Code

```js
function isMatchRec(i, j, s, p) {
  if (i < 0 && j < 0) return true;
  if (j < 0) return false;
  if (i < 0) {
    for (let k = 0; k <= j; k++) {
      if (p[k] !== "*") return false;
    }
    return true;
  }

  if (s[i] === p[j] || p[j] === "?") {
    return isMatchRec(i - 1, j - 1, s, p);
  }

  if (p[j] === "*") {
    return isMatchRec(i, j - 1, s, p) || isMatchRec(i - 1, j, s, p);
  }

  return false;
}

function isMatch(s, p) {
  return isMatchRec(s.length - 1, p.length - 1, s, p);
}
```

---

#### ⏱ Complexity

- **Time**: O(2^(n + m)) – exponential
- **Space**: O(n + m)

---

### ✅ Approach 2: Memoization (Top-Down)

---

#### 📘 Code

```js
function isMatch(s, p) {
  const n = s.length,
    m = p.length;
  const dp = Array.from({ length: n }, () => Array(m).fill(-1));

  function match(i, j) {
    if (i < 0 && j < 0) return true;
    if (j < 0) return false;
    if (i < 0) {
      for (let k = 0; k <= j; k++) {
        if (p[k] !== "*") return false;
      }
      return true;
    }

    if (dp[i][j] !== -1) return dp[i][j];

    if (s[i] === p[j] || p[j] === "?") {
      return (dp[i][j] = match(i - 1, j - 1));
    }

    if (p[j] === "*") {
      return (dp[i][j] = match(i, j - 1) || match(i - 1, j));
    }

    return (dp[i][j] = false);
  }

  return match(n - 1, m - 1);
}
```

---

#### ⏱ Complexity

- **Time**: O(n × m)
- **Space**: O(n × m) + recursion

---

### 🧮 Approach 3: Tabulation (Bottom-Up)

---

#### 📘 Code

```js
function isMatch(s, p) {
  const n = s.length,
    m = p.length;
  const dp = Array.from({ length: n + 1 }, () => Array(m + 1).fill(false));

  dp[0][0] = true;

  // Pattern matches empty string
  for (let j = 1; j <= m; j++) {
    if (p[j - 1] === "*") dp[0][j] = dp[0][j - 1];
  }

  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= m; j++) {
      if (s[i - 1] === p[j - 1] || p[j - 1] === "?") {
        dp[i][j] = dp[i - 1][j - 1];
      } else if (p[j - 1] === "*") {
        dp[i][j] = dp[i][j - 1] || dp[i - 1][j];
      }
    }
  }

  return dp[n][m];
}
```

---

### 🧊 Approach 4: Space Optimization

---

#### 📘 Code

```js
function isMatch(s, p) {
  const n = s.length,
    m = p.length;
  let prev = Array(m + 1).fill(false);
  prev[0] = true;

  for (let j = 1; j <= m; j++) {
    if (p[j - 1] === "*") prev[j] = prev[j - 1];
  }

  for (let i = 1; i <= n; i++) {
    let curr = Array(m + 1).fill(false);
    for (let j = 1; j <= m; j++) {
      if (s[i - 1] === p[j - 1] || p[j - 1] === "?") {
        curr[j] = prev[j - 1];
      } else if (p[j - 1] === "*") {
        curr[j] = prev[j] || curr[j - 1];
      }
    }
    prev = curr;
  }

  return prev[m];
}
```

---

#### 🔍 Dry Run (s = `"adceb"`, p = `"*a*b"`)

```txt
dp table is built as follows:

    ""  *   a   *   b
""  T   T   F   F   F
a   F   T   T   T   F
d   F   T   F   T   F
c   F   T   F   T   F
e   F   T   F   T   F
b   F   T   F   T   T
```

Answer: **true**

---

### 📌 Summary Table

| Approach           | Time     | Space    | Notes                         |
| ------------------ | -------- | -------- | ----------------------------- |
| Recursion          | O(2^n)   | O(n + m) | Brute force, exponential      |
| Memoization        | O(n × m) | O(n × m) | Top-down with caching         |
| Tabulation         | O(n × m) | O(n × m) | Bottom-up efficient           |
| Space Optimization | O(n × m) | O(m) ✅  | Most space-efficient solution |

---

# DP On Stocks

## 🔢 **1. Best Time to Buy and Sell Stock (DP-35)**

### 📘 Problem Statement

You are given an array `prices[]`, where `prices[i]` is the **price of a given stock on day `i`**.

You can **only buy once and sell once**, and must sell **after** buying.

Return the **maximum profit** you can achieve. If you can't make any profit, return `0`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: prices = [7, 1, 5, 3, 6, 4]
Output: 5
Explanation: Buy at 1, Sell at 6
```

#### ✅ Test Case 2:

```txt
Input: prices = [7, 6, 4, 3, 1]
Output: 0
Explanation: Prices only decline — no profit
```

#### ✅ Test Case 3:

```txt
Input: prices = [2, 4, 1]
Output: 2
```

#### ✅ Test Case 4:

```txt
Input: prices = [3, 2, 6, 5, 0, 3]
Output: 4
Explanation: Buy at 2, sell at 6
```

---

### ✅ Approach 1: Brute-force (Nested Loops)

#### 🧠 Intuition

Try buying on each day `i` and selling on each future day `j > i`, and track the max profit.

---

#### 📘 Code

```js
function maxProfit(prices) {
  let maxProfit = 0;
  for (let i = 0; i < prices.length; i++) {
    for (let j = i + 1; j < prices.length; j++) {
      maxProfit = Math.max(maxProfit, prices[j] - prices[i]);
    }
  }
  return maxProfit;
}
```

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(1)

❌ Not efficient for large input.

---

### ✅ Approach 2: Greedy (One Pass)

#### 🧠 Intuition

Track the **minimum price seen so far**, and at each step compute profit = `current price - min price`.
Update `maxProfit` accordingly.

---

#### 📘 Code

```js
function maxProfit(prices) {
  let minPrice = Infinity;
  let maxProfit = 0;

  for (let price of prices) {
    if (price < minPrice) {
      minPrice = price;
    } else {
      maxProfit = Math.max(maxProfit, price - minPrice);
    }
  }

  return maxProfit;
}
```

---

#### 🔍 Dry Run: prices = \[7, 1, 5, 3, 6, 4]

```
min = ∞ → 7 → 1
i = 2 → price = 5 → profit = 4 → maxProfit = 4
i = 3 → price = 3 → profit = 2 → maxProfit = 4
i = 4 → price = 6 → profit = 5 → maxProfit = 5
i = 5 → price = 4 → profit = 3 → maxProfit = 5
```

✅ Answer: 5

---

#### ⏱ Complexity

- **Time**: O(n) ✅
- **Space**: O(1) ✅

---

### 🧠 Alternate View: As DP

- Let `minSoFar` be the lowest price up to day `i`
- Let `dp[i] = max(dp[i-1], prices[i] - minSoFar)`

This reduces to Greedy because we only need `minSoFar` and `maxProfit`.

---

### 📌 Summary Table

| Approach        | Time    | Space   | Notes                        |
| --------------- | ------- | ------- | ---------------------------- |
| Brute Force     | O(n²)   | O(1)    | Too slow                     |
| Greedy (1-pass) | O(n) ✅ | O(1) ✅ | Best choice for this problem |

---

## 🔢 **2. Best Time to Buy and Sell Stock – II (DP-36)**

### 📘 Problem Statement

You are given an array `prices[]`, where `prices[i]` is the **stock price on day `i`**.

You are allowed to **make as many transactions as you like** — buy & sell multiple times — but **you must sell before buying again**.

Return the **maximum profit** you can achieve.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: prices = [7, 1, 5, 3, 6, 4]
Output: 7
Explanation: Buy at 1 → sell at 5, buy at 3 → sell at 6
```

#### ✅ Test Case 2:

```txt
Input: prices = [1, 2, 3, 4, 5]
Output: 4
Explanation: Buy at 1 → sell at 5
```

#### ✅ Test Case 3:

```txt
Input: prices = [7, 6, 4, 3, 1]
Output: 0
Explanation: No profitable transaction possible
```

---

### ✅ Approach 1: Greedy (Simple)

#### 🧠 Intuition

Buy at every local minima and sell at every local maxima.

Since you can do unlimited transactions:

- For every `i`, if `price[i] > price[i - 1]`, take the profit `price[i] - price[i - 1]`.

---

#### 📘 Code

```js
function maxProfit(prices) {
  let profit = 0;
  for (let i = 1; i < prices.length; i++) {
    if (prices[i] > prices[i - 1]) {
      profit += prices[i] - prices[i - 1];
    }
  }
  return profit;
}
```

---

#### 🔍 Dry Run (prices = \[1, 5, 3, 6, 4])

```
i = 1 → 5 > 1 → profit += 4 → total = 4
i = 2 → 3 < 5 → skip
i = 3 → 6 > 3 → profit += 3 → total = 7
i = 4 → 4 < 6 → skip
```

✅ Final profit = **7**

---

#### ⏱ Complexity

- **Time**: O(n) ✅
- **Space**: O(1)

---

### ✅ Approach 2: Recursion

#### 📘 Code

```js
function solve(i, canBuy, prices) {
  if (i === prices.length) return 0;

  if (canBuy) {
    const buy = -prices[i] + solve(i + 1, 0, prices);
    const skip = solve(i + 1, 1, prices);
    return Math.max(buy, skip);
  } else {
    const sell = prices[i] + solve(i + 1, 1, prices);
    const skip = solve(i + 1, 0, prices);
    return Math.max(sell, skip);
  }
}

function maxProfit(prices) {
  return solve(0, 1, prices);
}
```

---

#### ⏱ Complexity

- **Time**: O(2^n) ❌ (Too slow)
- **Space**: O(n)

---

### ✅ Approach 3: Memoization (Top-Down DP)

---

#### 📘 Code

```js
function maxProfit(prices) {
  const n = prices.length;
  const dp = Array.from({ length: n }, () => Array(2).fill(-1));

  function solve(i, canBuy) {
    if (i === n) return 0;
    if (dp[i][canBuy] !== -1) return dp[i][canBuy];

    if (canBuy) {
      const buy = -prices[i] + solve(i + 1, 0);
      const skip = solve(i + 1, 1);
      return (dp[i][canBuy] = Math.max(buy, skip));
    } else {
      const sell = prices[i] + solve(i + 1, 1);
      const skip = solve(i + 1, 0);
      return (dp[i][canBuy] = Math.max(sell, skip));
    }
  }

  return solve(0, 1);
}
```

---

#### ⏱ Complexity

- **Time**: O(n × 2) = O(n)
- **Space**: O(n × 2) + recursion

---

### 🧮 Approach 4: Tabulation (Bottom-Up DP)

---

#### 📘 Code

```js
function maxProfit(prices) {
  const n = prices.length;
  const dp = Array.from({ length: n + 1 }, () => Array(2).fill(0));

  for (let i = n - 1; i >= 0; i--) {
    for (let buy = 0; buy <= 1; buy++) {
      if (buy === 1) {
        dp[i][buy] = Math.max(-prices[i] + dp[i + 1][0], dp[i + 1][1]);
      } else {
        dp[i][buy] = Math.max(prices[i] + dp[i + 1][1], dp[i + 1][0]);
      }
    }
  }

  return dp[0][1];
}
```

---

### 🧊 Approach 5: Space Optimization

---

#### 📘 Code

```js
function maxProfit(prices) {
  const n = prices.length;
  let ahead = [0, 0]; // ahead[0] = can't buy, ahead[1] = can buy
  let curr = [0, 0];

  for (let i = n - 1; i >= 0; i--) {
    curr[1] = Math.max(-prices[i] + ahead[0], ahead[1]); // can buy
    curr[0] = Math.max(prices[i] + ahead[1], ahead[0]); // can't buy
    ahead = [...curr];
  }

  return curr[1];
}
```

---

### 📌 Summary Table

| Approach            | Time      | Space   | Notes                                |
| ------------------- | --------- | ------- | ------------------------------------ |
| Greedy              | O(n) ✅   | O(1) ✅ | Fastest, works when unlimited trades |
| Recursion           | O(2^n) ❌ | O(n)    | Too slow                             |
| Memoization (Top)   | O(n)      | O(n×2)  | DP with cache                        |
| Tabulation (Bottom) | O(n)      | O(n×2)  | Iterative version                    |
| Space Optimization  | O(n)      | O(1) ✅ | Best choice for DP-based solution    |

---

## 🔢 **3. Best Time to Buy and Sell Stock – III (At Most 2 Transactions)**

### 📘 Problem Statement

You are given an array `prices[]` where `prices[i]` is the price of a stock on day `i`.

You are allowed to complete **at most two transactions** (i.e., buy + sell = 1 transaction).
You may not engage in multiple transactions at the same time (i.e., you must sell before buying again).

**Return the maximum profit** you can achieve.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: prices = [3,3,5,0,0,3,1,4]
Output: 6
Explanation: Buy at 0, sell at 3, buy at 1, sell at 4
```

#### ✅ Test Case 2:

```txt
Input: prices = [1,2,3,4,5]
Output: 4
Explanation: Buy at 1, sell at 5
```

#### ✅ Test Case 3:

```txt
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: Prices only decline
```

---

### ✅ Approach 1: Recursion

#### 🧠 Intuition

At every day, we have a few choices:

- **Buy**, if we can
- **Sell**, if holding a stock
- **Skip**, go to next day

Use a `limit` variable to **track the number of transactions left**.

---

#### 📘 Code

```js
function solve(i, canBuy, limit, prices) {
  if (i === prices.length || limit === 0) return 0;

  if (canBuy) {
    const buy = -prices[i] + solve(i + 1, 0, limit, prices);
    const skip = solve(i + 1, 1, limit, prices);
    return Math.max(buy, skip);
  } else {
    const sell = prices[i] + solve(i + 1, 1, limit - 1, prices);
    const skip = solve(i + 1, 0, limit, prices);
    return Math.max(sell, skip);
  }
}

function maxProfit(prices) {
  return solve(0, 1, 2, prices);
}
```

---

#### ⏱ Complexity

- **Time**: O(2^n × 2 × k) ❌
- **Space**: O(n × 2 × k)

---

### ✅ Approach 2: Memoization (Top-Down DP)

---

#### 📘 Code

```js
function maxProfit(prices) {
  const n = prices.length;
  const dp = Array.from({ length: n }, () =>
    Array.from({ length: 2 }, () => Array(3).fill(-1))
  );

  function solve(i, canBuy, limit) {
    if (i === n || limit === 0) return 0;
    if (dp[i][canBuy][limit] !== -1) return dp[i][canBuy][limit];

    if (canBuy) {
      const buy = -prices[i] + solve(i + 1, 0, limit);
      const skip = solve(i + 1, 1, limit);
      return (dp[i][canBuy][limit] = Math.max(buy, skip));
    } else {
      const sell = prices[i] + solve(i + 1, 1, limit - 1);
      const skip = solve(i + 1, 0, limit);
      return (dp[i][canBuy][limit] = Math.max(sell, skip));
    }
  }

  return solve(0, 1, 2);
}
```

---

#### ⏱ Complexity

- **Time**: O(n × 2 × 3) = O(n)
- **Space**: O(n × 2 × 3) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up)

---

#### 📘 Code

```js
function maxProfit(prices) {
  const n = prices.length;
  const dp = Array.from({ length: n + 1 }, () =>
    Array.from({ length: 2 }, () => Array(3).fill(0))
  );

  for (let i = n - 1; i >= 0; i--) {
    for (let canBuy = 0; canBuy <= 1; canBuy++) {
      for (let limit = 1; limit <= 2; limit++) {
        if (canBuy) {
          const buy = -prices[i] + dp[i + 1][0][limit];
          const skip = dp[i + 1][1][limit];
          dp[i][canBuy][limit] = Math.max(buy, skip);
        } else {
          const sell = prices[i] + dp[i + 1][1][limit - 1];
          const skip = dp[i + 1][0][limit];
          dp[i][canBuy][limit] = Math.max(sell, skip);
        }
      }
    }
  }

  return dp[0][1][2];
}
```

---

### 🧊 Approach 4: Space Optimization

---

#### 📘 Code

```js
function maxProfit(prices) {
  const n = prices.length;
  let after = Array.from({ length: 2 }, () => Array(3).fill(0));
  let curr = Array.from({ length: 2 }, () => Array(3).fill(0));

  for (let i = n - 1; i >= 0; i--) {
    for (let canBuy = 0; canBuy <= 1; canBuy++) {
      for (let limit = 1; limit <= 2; limit++) {
        if (canBuy) {
          const buy = -prices[i] + after[0][limit];
          const skip = after[1][limit];
          curr[canBuy][limit] = Math.max(buy, skip);
        } else {
          const sell = prices[i] + after[1][limit - 1];
          const skip = after[0][limit];
          curr[canBuy][limit] = Math.max(sell, skip);
        }
      }
    }
    after = curr.map((row) => [...row]); // deep copy
  }

  return after[1][2];
}
```

---

#### 🔍 Dry Run (prices = \[3,3,5,0,0,3,1,4])

```
Profit using at most 2 transactions = 6
→ Buy at 0, sell at 3
→ Buy at 1, sell at 4
```

---

### 📌 Summary Table

| Approach            | Time     | Space            | Notes                         |
| ------------------- | -------- | ---------------- | ----------------------------- |
| Recursion           | O(2^n)   | O(n)             | Too slow                      |
| Memoization (Top)   | O(n×2×3) | O(n×2×3)         | Efficient with DP cache       |
| Tabulation (Bottom) | O(n×2×3) | O(n×2×3)         | Iterative DP                  |
| Space Optimization  | O(n×2×3) | O(2×3) = O(1) ✅ | Best approach (optimal space) |

---

## 🔢 **4. Best Time to Buy and Sell Stock – IV (At Most `k` Transactions)**

### 📘 Problem Statement

You are given:

- An integer `k` (maximum number of transactions allowed)
- An array `prices[]` where `prices[i]` is the stock price on day `i`.

You need to **maximize your profit** by performing **at most `k` transactions** (each transaction = buy + sell).

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: k = 2, prices = [2, 4, 1]
Output: 2
Explanation: Buy at 2, sell at 4
```

#### ✅ Test Case 2:

```txt
Input: k = 2, prices = [3,2,6,5,0,3]
Output: 7
Explanation: Buy at 2, sell at 6, buy at 0, sell at 3
```

#### ✅ Test Case 3:

```txt
Input: k = 1, prices = [1, 2]
Output: 1
```

#### ✅ Test Case 4:

```txt
Input: k = 3, prices = [7,6,4,3,1]
Output: 0
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

- You can make at most `k` transactions.
- At every index:

  - If you **can buy**, try buying or skipping
  - If you **can't buy**, try selling or skipping

- Track `limit` (remaining transactions)

---

#### 📘 Code

```js
function solve(i, canBuy, k, prices) {
  if (i === prices.length || k === 0) return 0;

  if (canBuy) {
    const buy = -prices[i] + solve(i + 1, 0, k, prices);
    const skip = solve(i + 1, 1, k, prices);
    return Math.max(buy, skip);
  } else {
    const sell = prices[i] + solve(i + 1, 1, k - 1, prices);
    const skip = solve(i + 1, 0, k, prices);
    return Math.max(sell, skip);
  }
}

function maxProfit(k, prices) {
  return solve(0, 1, k, prices);
}
```

---

#### ⏱ Complexity

- **Time**: O(2^n × k) ❌
- **Space**: O(n × k)

---

### ✅ Approach 2: Memoization (Top-Down DP)

---

#### 📘 Code

```js
function maxProfit(k, prices) {
  const n = prices.length;
  const dp = Array.from({ length: n }, () =>
    Array.from({ length: 2 }, () => Array(k + 1).fill(-1))
  );

  function solve(i, canBuy, limit) {
    if (i === n || limit === 0) return 0;
    if (dp[i][canBuy][limit] !== -1) return dp[i][canBuy][limit];

    if (canBuy) {
      const buy = -prices[i] + solve(i + 1, 0, limit);
      const skip = solve(i + 1, 1, limit);
      return (dp[i][canBuy][limit] = Math.max(buy, skip));
    } else {
      const sell = prices[i] + solve(i + 1, 1, limit - 1);
      const skip = solve(i + 1, 0, limit);
      return (dp[i][canBuy][limit] = Math.max(sell, skip));
    }
  }

  return solve(0, 1, k);
}
```

---

#### ⏱ Complexity

- **Time**: O(n × 2 × k) = O(nk)
- **Space**: O(nk × 2 + recursion)

---

### 🧮 Approach 3: Tabulation (Bottom-Up)

---

#### 📘 Code

```js
function maxProfit(k, prices) {
  const n = prices.length;
  const dp = Array.from({ length: n + 1 }, () =>
    Array.from({ length: 2 }, () => Array(k + 1).fill(0))
  );

  for (let i = n - 1; i >= 0; i--) {
    for (let canBuy = 0; canBuy <= 1; canBuy++) {
      for (let limit = 1; limit <= k; limit++) {
        if (canBuy) {
          const buy = -prices[i] + dp[i + 1][0][limit];
          const skip = dp[i + 1][1][limit];
          dp[i][canBuy][limit] = Math.max(buy, skip);
        } else {
          const sell = prices[i] + dp[i + 1][1][limit - 1];
          const skip = dp[i + 1][0][limit];
          dp[i][canBuy][limit] = Math.max(sell, skip);
        }
      }
    }
  }

  return dp[0][1][k];
}
```

---

### 🧊 Approach 4: Space Optimization

We can optimize using two 2D arrays (`prev` and `curr`) of size `[2][k+1]`.

---

#### 📘 Code

```js
function maxProfit(k, prices) {
  const n = prices.length;
  let after = Array.from({ length: 2 }, () => Array(k + 1).fill(0));
  let curr = Array.from({ length: 2 }, () => Array(k + 1).fill(0));

  for (let i = n - 1; i >= 0; i--) {
    for (let canBuy = 0; canBuy <= 1; canBuy++) {
      for (let limit = 1; limit <= k; limit++) {
        if (canBuy) {
          const buy = -prices[i] + after[0][limit];
          const skip = after[1][limit];
          curr[canBuy][limit] = Math.max(buy, skip);
        } else {
          const sell = prices[i] + after[1][limit - 1];
          const skip = after[0][limit];
          curr[canBuy][limit] = Math.max(sell, skip);
        }
      }
    }
    after = curr.map((row) => [...row]);
  }

  return after[1][k];
}
```

---

### 📌 Summary Table

| Approach            | Time        | Space        | Notes                       |
| ------------------- | ----------- | ------------ | --------------------------- |
| Recursion           | O(2^n) ❌   | O(n × k)     | Brute force – not efficient |
| Memoization (Top)   | O(n × k) ✅ | O(n × k × 2) | DP with cache               |
| Tabulation (Bottom) | O(n × k) ✅ | O(n × k × 2) | Iterative DP                |
| Space Optimization  | O(n × k) ✅ | O(k × 2) ✅  | Best approach               |

---

## 🔢 **5. Best Time to Buy and Sell Stock with Cooldown (DP-39)**

### 📘 Problem Statement

You are given an array `prices[]` of length `n`, where `prices[i]` represents the price of a stock on day `i`.

You can complete as many transactions as you like, but:

> After selling a stock, you **cannot buy** on the **next day** (1 day **cooldown** is required).

Return the **maximum profit** you can achieve.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: prices = [1,2,3,0,2]
Output: 3
Explanation: Buy at 1, sell at 3, cooldown, buy at 0, sell at 2
```

#### ✅ Test Case 2:

```txt
Input: prices = [1]
Output: 0
Explanation: No transactions possible
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

At each day `i`, we can:

- **Buy** (if allowed) → go to `i+1` in sell mode
- **Sell** → go to `i+2` (cooldown day)
- **Skip** → go to `i+1` and keep the same state

---

#### 📘 Code

```js
function solve(i, canBuy, prices) {
  if (i >= prices.length) return 0;

  if (canBuy) {
    const buy = -prices[i] + solve(i + 1, 0, prices);
    const skip = solve(i + 1, 1, prices);
    return Math.max(buy, skip);
  } else {
    const sell = prices[i] + solve(i + 2, 1, prices); // cooldown
    const skip = solve(i + 1, 0, prices);
    return Math.max(sell, skip);
  }
}

function maxProfit(prices) {
  return solve(0, 1, prices);
}
```

---

#### ⏱ Complexity

- **Time**: O(2^n) ❌
- **Space**: O(n)

---

### ✅ Approach 2: Memoization (Top-Down DP)

---

#### 📘 Code

```js
function maxProfit(prices) {
  const n = prices.length;
  const dp = Array.from({ length: n }, () => Array(2).fill(-1));

  function solve(i, canBuy) {
    if (i >= n) return 0;
    if (dp[i][canBuy] !== -1) return dp[i][canBuy];

    if (canBuy) {
      const buy = -prices[i] + solve(i + 1, 0);
      const skip = solve(i + 1, 1);
      return (dp[i][canBuy] = Math.max(buy, skip));
    } else {
      const sell = prices[i] + solve(i + 2, 1); // cooldown
      const skip = solve(i + 1, 0);
      return (dp[i][canBuy] = Math.max(sell, skip));
    }
  }

  return solve(0, 1);
}
```

---

#### ⏱ Complexity

- **Time**: O(n × 2) = O(n)
- **Space**: O(n × 2) + recursion

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

---

#### 📘 Code

```js
function maxProfit(prices) {
  const n = prices.length;
  const dp = Array.from({ length: n + 2 }, () => Array(2).fill(0));

  for (let i = n - 1; i >= 0; i--) {
    dp[i][1] = Math.max(-prices[i] + dp[i + 1][0], dp[i + 1][1]); // buy
    dp[i][0] = Math.max(prices[i] + dp[i + 2][1], dp[i + 1][0]); // sell
  }

  return dp[0][1];
}
```

---

#### ⏱ Complexity

- **Time**: O(n)
- **Space**: O(n)

---

### 🧊 Approach 4: Space Optimization

---

#### 📘 Code

```js
function maxProfit(prices) {
  const n = prices.length;
  let ahead1 = [0, 0]; // i+1
  let ahead2 = [0, 0]; // i+2
  let curr = [0, 0];

  for (let i = n - 1; i >= 0; i--) {
    curr[1] = Math.max(-prices[i] + ahead1[0], ahead1[1]);
    curr[0] = Math.max(prices[i] + ahead2[1], ahead1[0]);

    ahead2 = [...ahead1];
    ahead1 = [...curr];
  }

  return curr[1];
}
```

---

#### 🔍 Dry Run (prices = \[1,2,3,0,2])

```
Day 0: Buy at 1 → sell at 3 → cooldown → buy at 0 → sell at 2 = 3
```

---

### 📌 Summary Table

| Approach            | Time      | Space    | Notes                         |
| ------------------- | --------- | -------- | ----------------------------- |
| Recursion           | O(2^n) ❌ | O(n)     | Brute force, too slow         |
| Memoization (Top)   | O(n) ✅   | O(n × 2) | Efficient with caching        |
| Tabulation (Bottom) | O(n) ✅   | O(n × 2) | Iterative version             |
| Space Optimization  | O(n) ✅   | O(1) ✅  | Best space-efficient approach |

---

## 🔢 **6. Best Time to Buy and Sell Stock with Transaction Fee**

### 📘 Problem Statement

You are given an integer array `prices[]`, where `prices[i]` is the price of a given stock on day `i`.

You are also given an integer `fee` — the **transaction fee** for each **buy + sell** operation.

Your task is to maximize your **total profit**. You may complete as many transactions as you like, but you must **sell before buying again**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: prices = [1, 3, 2, 8, 4, 9], fee = 2
Output: 8
Explanation:
- Buy at 1, sell at 8 → profit = 8 - 1 - 2 = 5
- Buy at 4, sell at 9 → profit = 9 - 4 - 2 = 3
Total = 8
```

#### ✅ Test Case 2:

```txt
Input: prices = [1, 3, 7, 5, 10, 3], fee = 3
Output: 6
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

At each day `i`:

- If we **can buy**, we either:

  - **Buy**, pay price, go to next day in "sell" mode
  - **Skip**, stay in buy mode

- If we **can sell**, we either:

  - **Sell**, gain price - fee, go to next day in "buy" mode
  - **Skip**, stay in sell mode

---

#### 📘 Code

```js
function solve(i, canBuy, prices, fee) {
  if (i === prices.length) return 0;

  if (canBuy) {
    const buy = -prices[i] + solve(i + 1, 0, prices, fee);
    const skip = solve(i + 1, 1, prices, fee);
    return Math.max(buy, skip);
  } else {
    const sell = prices[i] - fee + solve(i + 1, 1, prices, fee);
    const skip = solve(i + 1, 0, prices, fee);
    return Math.max(sell, skip);
  }
}

function maxProfit(prices, fee) {
  return solve(0, 1, prices, fee);
}
```

---

#### ⏱ Complexity

- **Time**: O(2^n) ❌
- **Space**: O(n)

---

### ✅ Approach 2: Memoization (Top-Down DP)

---

#### 📘 Code

```js
function maxProfit(prices, fee) {
  const n = prices.length;
  const dp = Array.from({ length: n }, () => Array(2).fill(-1));

  function solve(i, canBuy) {
    if (i === n) return 0;
    if (dp[i][canBuy] !== -1) return dp[i][canBuy];

    if (canBuy) {
      const buy = -prices[i] + solve(i + 1, 0);
      const skip = solve(i + 1, 1);
      return (dp[i][canBuy] = Math.max(buy, skip));
    } else {
      const sell = prices[i] - fee + solve(i + 1, 1);
      const skip = solve(i + 1, 0);
      return (dp[i][canBuy] = Math.max(sell, skip));
    }
  }

  return solve(0, 1);
}
```

---

#### ⏱ Complexity

- **Time**: O(n × 2) = O(n)
- **Space**: O(n × 2) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

---

#### 📘 Code

```js
function maxProfit(prices, fee) {
  const n = prices.length;
  const dp = Array.from({ length: n + 1 }, () => Array(2).fill(0));

  for (let i = n - 1; i >= 0; i--) {
    dp[i][1] = Math.max(-prices[i] + dp[i + 1][0], dp[i + 1][1]);
    dp[i][0] = Math.max(prices[i] - fee + dp[i + 1][1], dp[i + 1][0]);
  }

  return dp[0][1];
}
```

---

### 🧊 Approach 4: Space Optimization

---

#### 📘 Code

```js
function maxProfit(prices, fee) {
  let aheadBuy = 0,
    aheadNotBuy = 0;

  for (let i = prices.length - 1; i >= 0; i--) {
    const currBuy = Math.max(-prices[i] + aheadNotBuy, aheadBuy);
    const currNotBuy = Math.max(prices[i] - fee + aheadBuy, aheadNotBuy);
    aheadBuy = currBuy;
    aheadNotBuy = currNotBuy;
  }

  return aheadBuy;
}
```

---

#### 🔍 Dry Run Example (prices = \[1,3,2,8,4,9], fee = 2)

```
→ Buy at 1, sell at 8 → profit = 5
→ Buy at 4, sell at 9 → profit = 3
→ Total = 8
```

---

### 📌 Summary Table

| Approach            | Time      | Space    | Notes                          |
| ------------------- | --------- | -------- | ------------------------------ |
| Recursion           | O(2^n) ❌ | O(n)     | Too slow for large inputs      |
| Memoization (Top)   | O(n) ✅   | O(n × 2) | Caches overlapping subproblems |
| Tabulation (Bottom) | O(n) ✅   | O(n × 2) | Iterative, easy to follow      |
| Space Optimization  | O(n) ✅   | O(1) ✅  | Best in both time and space    |

---

# DP On LIS

## 🔢 **1. Longest Increasing Subsequence (DP-41)**

### 📘 Problem Statement

Given an array of integers `nums`, return the **length of the longest increasing subsequence (LIS)**.

> A subsequence is a sequence derived by deleting some or no elements without changing the order of the remaining elements.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The LIS is [2,3,7,101]
```

#### ✅ Test Case 2:

```txt
Input: nums = [0,1,0,3,2,3]
Output: 4
```

#### ✅ Test Case 3:

```txt
Input: nums = [7,7,7,7,7,7,7]
Output: 1
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

At each index, we have **two choices**:

- **Pick** the current number if it's greater than the previous one.
- **Skip** the current number.

We explore all possible subsequences and track the max.

---

#### 📘 Code

```js
function solve(index, prevIndex, nums) {
  if (index === nums.length) return 0;

  let notPick = solve(index + 1, prevIndex, nums);
  let pick = 0;
  if (prevIndex === -1 || nums[index] > nums[prevIndex]) {
    pick = 1 + solve(index + 1, index, nums);
  }

  return Math.max(pick, notPick);
}

function lengthOfLIS(nums) {
  return solve(0, -1, nums);
}
```

---

#### ⏱ Complexity

- **Time**: O(2^n) ❌
- **Space**: O(n)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Optimization Idea

Use a 2D DP table: `dp[index][prevIndex + 1]`
(Shifted by +1 to handle `-1` index)

---

#### 📘 Code

```js
function lengthOfLIS(nums) {
  const n = nums.length;
  const dp = Array.from({ length: n }, () => Array(n + 1).fill(-1));

  function solve(index, prevIndex) {
    if (index === n) return 0;
    if (dp[index][prevIndex + 1] !== -1) return dp[index][prevIndex + 1];

    let notPick = solve(index + 1, prevIndex);
    let pick = 0;
    if (prevIndex === -1 || nums[index] > nums[prevIndex]) {
      pick = 1 + solve(index + 1, index);
    }

    return (dp[index][prevIndex + 1] = Math.max(pick, notPick));
  }

  return solve(0, -1);
}
```

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(n²) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

---

#### 📘 Code

```js
function lengthOfLIS(nums) {
  const n = nums.length;
  const dp = Array.from({ length: n + 1 }, () => Array(n + 1).fill(0));

  for (let i = n - 1; i >= 0; i--) {
    for (let prev = i - 1; prev >= -1; prev--) {
      const notPick = dp[i + 1][prev + 1];
      let pick = 0;
      if (prev === -1 || nums[i] > nums[prev]) {
        pick = 1 + dp[i + 1][i + 1];
      }
      dp[i][prev + 1] = Math.max(pick, notPick);
    }
  }

  return dp[0][0];
}
```

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(n²)

---

### 🧊 Approach 4: Space Optimization (1D DP)

We realize we only need 1D `dp[i] = length of LIS ending at index i`.

---

#### 📘 Code

```js
function lengthOfLIS(nums) {
  const n = nums.length;
  const dp = Array(n).fill(1);

  for (let i = 1; i < n; i++) {
    for (let j = 0; j < i; j++) {
      if (nums[i] > nums[j]) {
        dp[i] = Math.max(dp[i], dp[j] + 1);
      }
    }
  }

  return Math.max(...dp);
}
```

---

#### 🔍 Dry Run Example: nums = \[10,9,2,5,3,7,101,18]

```txt
dp = [1,1,1,2,2,3,4,4]
Max = 4 → [2,3,7,101]
```

---

### 🧠 BONUS: Approach 5 - Binary Search (Patience Sorting)

Time: **O(n log n)**
Use a list `tail[]` to keep the smallest tail of increasing subsequences.

---

#### 📘 Code

```js
function lengthOfLIS(nums) {
  const tail = [];

  for (let num of nums) {
    let left = 0,
      right = tail.length;
    while (left < right) {
      const mid = Math.floor((left + right) / 2);
      if (tail[mid] < num) left = mid + 1;
      else right = mid;
    }

    if (left < tail.length) tail[left] = num;
    else tail.push(num);
  }

  return tail.length;
}
```

---

### 📌 Summary Table

| Approach               | Time          | Space   | Notes                            |
| ---------------------- | ------------- | ------- | -------------------------------- |
| Recursion              | O(2^n) ❌     | O(n)    | Brute-force                      |
| Memoization (Top)      | O(n²) ✅      | O(n²)   | Efficient and intuitive          |
| Tabulation (Bottom)    | O(n²) ✅      | O(n²)   | Iterative bottom-up DP           |
| Space Optimization     | O(n²) ✅      | O(n) ✅ | Most common 1D-DP solution       |
| Binary Search (Greedy) | O(n log n) ✅ | O(n) ✅ | Most optimal for just LIS length |

---

## 🔢 **2. Print Longest Increasing Subsequence**

### 📘 Problem Statement

Given an array of integers `nums`, print the **actual elements** of the **longest increasing subsequence (LIS)**.

> A subsequence is formed by deleting some or no elements without changing the order.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: nums = [10, 9, 2, 5, 3, 7, 101, 18]
Output: [2, 3, 7, 101]
```

#### ✅ Test Case 2:

```txt
Input: nums = [0, 1, 0, 3, 2, 3]
Output: [0, 1, 2, 3] or [0, 1, 3]
```

---

### ✅ Approach: 1D DP + Parent Tracking

#### 🧠 Intuition

We use a `dp[i]` array to store the **length of LIS ending at `i`**, and a `parent[i]` array to help us **reconstruct the sequence**.

---

#### 📘 Code

```js
function printLIS(nums) {
  const n = nums.length;
  const dp = Array(n).fill(1);
  const parent = Array(n).fill(-1);

  let maxLen = 1;
  let lastIndex = 0;

  for (let i = 0; i < n; i++) {
    for (let j = 0; j < i; j++) {
      if (nums[i] > nums[j] && dp[j] + 1 > dp[i]) {
        dp[i] = dp[j] + 1;
        parent[i] = j;
      }
    }

    if (dp[i] > maxLen) {
      maxLen = dp[i];
      lastIndex = i;
    }
  }

  // Reconstruct LIS from parent[]
  const lis = [];
  while (lastIndex !== -1) {
    lis.push(nums[lastIndex]);
    lastIndex = parent[lastIndex];
  }

  return lis.reverse();
}
```

---

#### 🔍 Dry Run for `nums = [10, 9, 2, 5, 3, 7, 101, 18]`

- `dp = [1, 1, 1, 2, 2, 3, 4, 4]`
- `parent = [-1, -1, -1, 2, 2, 4, 5, 5]`
- `lastIndex = 6` (value 101)
- Backtrack from 101 → 7 → 3 → 2 → reverse = `[2, 3, 7, 101]`

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(n) (for `dp`, `parent`, and result)

---

#### 🧠 Optional: Binary Search + Reconstruction (Hard)

If you want **O(n log n)** LIS with printing, you need to track indices using binary search and maintain **predecessors**, which is more complex.

---

### 📌 Summary Table

| Step              | Method                 | Time          | Space | Notes                            |
| ----------------- | ---------------------- | ------------- | ----- | -------------------------------- |
| Find LIS length   | 1D DP                  | O(n²) ✅      | O(n)  | Simple and readable              |
| Reconstruct LIS   | Parent Tracking        | O(n) ✅       | O(n)  | Backtrack using `parent[]` array |
| Optimized Version | Patience Sorting + Map | O(n log n) ✅ | O(n)  | Complex but faster               |

---

## 🔢 **3. Longest Increasing Subsequence (DP-43)**

### 📘 Problem Statement

Given an integer array `nums`, return the **length of the Longest Increasing Subsequence (LIS)**.

> A subsequence is a sequence that appears in the same relative order, but not necessarily contiguous.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: LIS = [2,3,7,101]
```

#### ✅ Test Case 2:

```txt
Input: nums = [0,1,0,3,2,3]
Output: 4
```

#### ✅ Test Case 3:

```txt
Input: nums = [7,7,7,7,7]
Output: 1
```

---

### 🚀 Approach 1: Recursion

#### 🧠 Intuition

Try all subsequences, for every index:

- Either **take** it (if `nums[i] > prev`) or **skip**.

---

#### 📘 Code

```js
function solve(i, prevIndex, nums) {
  if (i === nums.length) return 0;

  let notTake = solve(i + 1, prevIndex, nums);
  let take = 0;

  if (prevIndex === -1 || nums[i] > nums[prevIndex]) {
    take = 1 + solve(i + 1, i, nums);
  }

  return Math.max(take, notTake);
}

function lengthOfLIS(nums) {
  return solve(0, -1, nums);
}
```

---

#### ⏱ Complexity

- **Time**: O(2ⁿ) ❌
- **Space**: O(n)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Optimization

Memoize results using `dp[i][prevIndex+1]`.

---

#### 📘 Code

```js
function lengthOfLIS(nums) {
  const n = nums.length;
  const dp = Array.from({ length: n }, () => Array(n + 1).fill(-1));

  function solve(i, prevIndex) {
    if (i === n) return 0;
    if (dp[i][prevIndex + 1] !== -1) return dp[i][prevIndex + 1];

    let notTake = solve(i + 1, prevIndex);
    let take = 0;

    if (prevIndex === -1 || nums[i] > nums[prevIndex]) {
      take = 1 + solve(i + 1, i);
    }

    return (dp[i][prevIndex + 1] = Math.max(take, notTake));
  }

  return solve(0, -1);
}
```

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(n²) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

---

#### 📘 Code

```js
function lengthOfLIS(nums) {
  const n = nums.length;
  const dp = Array(n).fill(1);
  let maxLen = 1;

  for (let i = 1; i < n; i++) {
    for (let j = 0; j < i; j++) {
      if (nums[i] > nums[j]) {
        dp[i] = Math.max(dp[i], dp[j] + 1);
      }
    }
    maxLen = Math.max(maxLen, dp[i]);
  }

  return maxLen;
}
```

---

#### 🔍 Dry Run (nums = \[10,9,2,5,3,7,101,18])

```txt
dp = [1,1,1,2,2,3,4,4]
LIS length = 4
```

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(n)

---

### 💎 Approach 4: Patience Sorting (Binary Search – O(n log n))

#### 🧠 Idea

Maintain a `tail[]` array:

- For every `num`:

  - Find the first index where `tail[idx] ≥ num` using binary search
  - Replace it or push at end

---

#### 📘 Code

```js
function lengthOfLIS(nums) {
  const tail = [];

  for (const num of nums) {
    let left = 0,
      right = tail.length;
    while (left < right) {
      const mid = Math.floor((left + right) / 2);
      if (tail[mid] < num) left = mid + 1;
      else right = mid;
    }

    if (left < tail.length) {
      tail[left] = num;
    } else {
      tail.push(num);
    }
  }

  return tail.length;
}
```

---

#### 🔍 Dry Run: \[10,9,2,5,3,7,101,18]

```txt
tail evolves:
[10]
[9]
[2]
[2,5]
[2,3]
[2,3,7]
[2,3,7,101]
[2,3,7,18]

LIS length = 4
```

---

#### ⏱ Complexity

- **Time**: O(n log n) ✅
- **Space**: O(n)

---

### 📌 Summary Table

| Approach               | Time          | Space   | Notes                                 |
| ---------------------- | ------------- | ------- | ------------------------------------- |
| Recursion              | O(2^n) ❌     | O(n)    | Brute force                           |
| Memoization (Top-Down) | O(n²) ✅      | O(n²)   | DP + Memo                             |
| Tabulation (Bottom-Up) | O(n²) ✅      | O(n) ✅ | Classic DP                            |
| Patience Sorting       | O(n log n) ✅ | O(n) ✅ | Most efficient for length calculation |

---

## 🔢 **4. Largest Divisible Subset**

### 📘 Problem Statement

Given a set of **distinct positive integers**, return the **largest subset** such that **every pair `(Si, Sj)` in the subset** satisfies:

```
Si % Sj == 0 || Sj % Si == 0
```

If there are multiple such subsets, return **any** of them.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: nums = [1, 2, 3]
Output: [1, 2]
```

#### ✅ Test Case 2:

```txt
Input: nums = [1, 2, 4, 8]
Output: [1, 2, 4, 8]
```

#### ✅ Test Case 3:

```txt
Input: nums = [4, 8, 10, 240]
Output: [4, 8, 240]
```

---

### 🚀 Preprocessing Step

Sort the array so we always try to build divisible sequences from **smallest to largest**.

---

### ❌ Approach 1: Recursion

#### 🧠 Intuition

Try including each number if divisible by the previous selected.
Try both pick and not-pick for each index.

---

#### 📘 Code

```js
function solve(i, prevIndex, nums) {
  if (i === nums.length) return [];

  const notPick = solve(i + 1, prevIndex, nums);

  let pick = [];
  if (prevIndex === -1 || nums[i] % nums[prevIndex] === 0) {
    pick = [nums[i], ...solve(i + 1, i, nums)];
  }

  return pick.length > notPick.length ? pick : notPick;
}

function largestDivisibleSubset(nums) {
  nums.sort((a, b) => a - b);
  return solve(0, -1, nums);
}
```

---

#### ⏱ Complexity

- **Time**: O(2^n) ❌
- **Space**: O(n)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Optimization

Store results in a 2D memo table `dp[i][prev+1]` to avoid recomputation.

---

#### 📘 Code

```js
function largestDivisibleSubset(nums) {
  nums.sort((a, b) => a - b);
  const n = nums.length;
  const dp = Array.from({ length: n }, () => Array(n + 1).fill(null));

  function solve(i, prevIndex) {
    if (i === n) return [];

    if (dp[i][prevIndex + 1] !== null) return dp[i][prevIndex + 1];

    const notPick = solve(i + 1, prevIndex);

    let pick = [];
    if (prevIndex === -1 || nums[i] % nums[prevIndex] === 0) {
      pick = [nums[i], ...solve(i + 1, i)];
    }

    dp[i][prevIndex + 1] = pick.length > notPick.length ? pick : notPick;
    return dp[i][prevIndex + 1];
  }

  return solve(0, -1);
}
```

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(n²) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

We use the LIS strategy but instead of strictly increasing, we check divisibility:
`nums[i] % nums[j] == 0`.

Track:

- `dp[i] = max length ending at index i`
- `parent[i] = previous index in the path`

---

#### 📘 Code

```js
function largestDivisibleSubset(nums) {
  nums.sort((a, b) => a - b);
  const n = nums.length;
  const dp = Array(n).fill(1);
  const parent = Array(n).fill(-1);

  let maxLen = 1,
    lastIndex = 0;

  for (let i = 1; i < n; i++) {
    for (let j = 0; j < i; j++) {
      if (nums[i] % nums[j] === 0 && dp[j] + 1 > dp[i]) {
        dp[i] = dp[j] + 1;
        parent[i] = j;
      }
    }

    if (dp[i] > maxLen) {
      maxLen = dp[i];
      lastIndex = i;
    }
  }

  // Reconstruct the subset
  const subset = [];
  while (lastIndex !== -1) {
    subset.push(nums[lastIndex]);
    lastIndex = parent[lastIndex];
  }

  return subset.reverse();
}
```

---

#### 🔍 Dry Run (nums = \[1, 2, 4, 8])

```txt
dp =    [1, 2, 3, 4]
parent =[-1, 0, 1, 2]
lastIndex = 3 → subset = [1,2,4,8]
```

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(n)

---

### 🧊 Space Optimization?

Since we **need the path** (actual subset), **parent tracking** is essential, so space optimization isn’t practical here.

But if you only want **LENGTH of the subset**, you can just use a 1D `dp[]`.

---

### 📌 Summary Table

| Approach        | Time      | Space   | Notes                                   |
| --------------- | --------- | ------- | --------------------------------------- |
| Recursion       | O(2^n) ❌ | O(n)    | Brute force                             |
| Memoization     | O(n²) ✅  | O(n²)   | Avoids recomputation                    |
| Tabulation      | O(n²) ✅  | O(n) ✅ | Optimal for subset + easy to trace      |
| Space Optimized | ❌        | ❌      | Not suitable (need path reconstruction) |

---

## 🔢 **5. Longest String Chain**

### 📘 Problem Statement

You are given an array of strings `words`. A **word chain** is a sequence of words where each word is formed by **adding one letter** to the previous word (anywhere in the string).

Return the **length of the longest possible word chain**.

> If `wordA` is a predecessor of `wordB`, then you can get `wordB` by adding **one character** to `wordA`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: words = ["a", "b", "ba", "bca", "bda", "bdca"]
Output: 4
Explanation: "a" → "ba" → "bda" → "bdca"
```

#### ✅ Test Case 2:

```txt
Input: words = ["xbc", "pcxbcf", "xb", "cxbc", "pcxbc"]
Output: 5
Explanation: "xb" → "xbc" → "cxbc" → "pcxbc" → "pcxbcf"
```

#### ✅ Test Case 3:

```txt
Input: words = ["abcd", "dbqca"]
Output: 1
```

---

### 🧠 Key Insight

Sort the array by word **length**. For each word, try to remove **one character at every position** and check if the remaining string exists in the set or map.

---

### 🚀 Approach 1: Recursion (TLE ❌)

#### 🧠 Intuition

For every word, try all possible predecessors by removing one character and recursively compute the longest chain.

---

#### 📘 Code

```js
function isPredecessor(shorter, longer) {
  if (longer.length - shorter.length !== 1) return false;
  let i = 0,
    j = 0;
  while (i < shorter.length && j < longer.length) {
    if (shorter[i] === longer[j]) i++;
    j++;
  }
  return i === shorter.length;
}

function dfs(curr, words) {
  let maxLen = 1;
  for (const next of words) {
    if (isPredecessor(curr, next)) {
      maxLen = Math.max(maxLen, 1 + dfs(next, words));
    }
  }
  return maxLen;
}

function longestStrChain(words) {
  let maxLength = 1;
  for (const word of words) {
    maxLength = Math.max(maxLength, dfs(word, words));
  }
  return maxLength;
}
```

---

#### ⏱ Complexity

- **Time**: Exponential ❌
- **Space**: O(n)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Optimization

Memoize the result of each `word` to avoid recomputation.

---

#### 📘 Code

```js
function longestStrChain(words) {
  const wordSet = new Set(words);
  const memo = new Map();

  function dfs(word) {
    if (memo.has(word)) return memo.get(word);

    let maxLen = 1;
    for (let i = 0; i < word.length; i++) {
      const prev = word.slice(0, i) + word.slice(i + 1);
      if (wordSet.has(prev)) {
        maxLen = Math.max(maxLen, 1 + dfs(prev));
      }
    }

    memo.set(word, maxLen);
    return maxLen;
  }

  let maxOverall = 0;
  for (const word of words) {
    maxOverall = Math.max(maxOverall, dfs(word));
  }
  return maxOverall;
}
```

---

#### ⏱ Complexity

- **Time**: O(n \* L²)
  (n = #words, L = max length of a word)
- **Space**: O(n) (for memo and recursion stack)

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

- Sort words by length
- For each word, try removing one char at every index to find possible predecessors in `dp`
- `dp[word] = max(dp[prevWord] + 1)` for all valid `prevWord`

---

#### 📘 Code

```js
function longestStrChain(words) {
  words.sort((a, b) => a.length - b.length);
  const dp = new Map();
  let maxLen = 1;

  for (const word of words) {
    let best = 0;
    for (let i = 0; i < word.length; i++) {
      const prev = word.slice(0, i) + word.slice(i + 1);
      best = Math.max(best, dp.get(prev) || 0);
    }
    dp.set(word, best + 1);
    maxLen = Math.max(maxLen, best + 1);
  }

  return maxLen;
}
```

---

#### 🔍 Dry Run (words = \["a", "ba", "bda", "bdca"])

```txt
Sort: ["a", "ba", "bda", "bdca"]
dp["a"] = 1
dp["ba"] = dp["a"] + 1 = 2
dp["bda"] = dp["ba"] + 1 = 3
dp["bdca"] = dp["bda"] + 1 = 4
```

---

#### ⏱ Complexity

- **Time**: O(n \* L²) ✅
- **Space**: O(n) ✅

---

### 🧊 Space Optimization?

Since we store intermediate chain lengths per word, and all words are different, `dp[word]` is necessary. Space is already optimal (`O(n)`), **no further optimization possible**.

---

### 📌 Summary Table

| Approach               | Time         | Space           | Notes                      |
| ---------------------- | ------------ | --------------- | -------------------------- |
| Recursion              | Exponential  | O(n)            | Too slow                   |
| Memoization (Top-Down) | O(n × L²) ✅ | O(n) ✅         | Caches subproblems         |
| Tabulation (Bottom-Up) | O(n × L²) ✅ | O(n) ✅         | Best for real-world inputs |
| Space Optimized        | N/A          | Already Optimal | `Map` storage is essential |

---

## 🔢 **6. Longest Bitonic Subsequence**

### 📘 Problem Statement

Given an array of `n` integers, find the **length of the Longest Bitonic Subsequence (LBS)**.
A **bitonic subsequence** is a sequence which:

- First **strictly increases**
- Then **strictly decreases**

> A valid subsequence must have at least one increasing and one decreasing phase (unless it's strictly increasing or decreasing only).

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: nums = [1, 11, 2, 10, 4, 5, 2, 1]
Output: 6
Explanation: The LBS is [1, 2, 10, 4, 2, 1]
```

#### ✅ Test Case 2:

```txt
Input: nums = [12, 11, 40, 5, 3, 1]
Output: 5
Explanation: [11, 40, 5, 3, 1]
```

#### ✅ Test Case 3:

```txt
Input: nums = [1, 2, 3, 4, 5]
Output: 5
Explanation: Entire array is increasing (decreasing part can be empty)
```

---

### 🚀 Approach 1: Recursion (TLE ❌)

#### 🧠 Intuition

You calculate:

- LIS ending at each index
- LDS starting at each index

LBS\[i] = LIS\[i] + LDS\[i] - 1 (since `nums[i]` is counted twice)

---

#### 📘 Code (Recursion for LIS and LDS)

```js
function LIS(i, nums) {
  let maxLen = 1;
  for (let prev = 0; prev < i; prev++) {
    if (nums[i] > nums[prev]) {
      maxLen = Math.max(maxLen, 1 + LIS(prev, nums));
    }
  }
  return maxLen;
}

function LDS(i, nums) {
  let maxLen = 1;
  for (let next = i + 1; next < nums.length; next++) {
    if (nums[i] > nums[next]) {
      maxLen = Math.max(maxLen, 1 + LDS(next, nums));
    }
  }
  return maxLen;
}

function longestBitonicSubsequence(nums) {
  let maxLen = 0;
  const n = nums.length;
  for (let i = 0; i < n; i++) {
    const inc = LIS(i, nums);
    const dec = LDS(i, nums);
    maxLen = Math.max(maxLen, inc + dec - 1);
  }
  return maxLen;
}
```

---

#### ⏱ Complexity

- **Time**: O(2ⁿ) ❌
- **Space**: O(n)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Optimization

Store results of LIS/LDS using two 1D DP arrays:

- `dp1[i] = LIS ending at i`
- `dp2[i] = LDS starting from i`

---

#### 📘 Code

```js
function longestBitonicSubsequence(nums) {
  const n = nums.length;
  const dp1 = Array(n).fill(-1);
  const dp2 = Array(n).fill(-1);

  function LIS(i) {
    if (dp1[i] !== -1) return dp1[i];
    let maxLen = 1;
    for (let prev = 0; prev < i; prev++) {
      if (nums[i] > nums[prev]) {
        maxLen = Math.max(maxLen, 1 + LIS(prev));
      }
    }
    return (dp1[i] = maxLen);
  }

  function LDS(i) {
    if (dp2[i] !== -1) return dp2[i];
    let maxLen = 1;
    for (let next = i + 1; next < n; next++) {
      if (nums[i] > nums[next]) {
        maxLen = Math.max(maxLen, 1 + LDS(next));
      }
    }
    return (dp2[i] = maxLen);
  }

  let maxBitonic = 0;
  for (let i = 0; i < n; i++) {
    const inc = LIS(i);
    const dec = LDS(i);
    maxBitonic = Math.max(maxBitonic, inc + dec - 1);
  }

  return maxBitonic;
}
```

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(n) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

Build LIS and LDS using classic DP, then combine:

- LIS\[i]: max increasing subsequence ending at i
- LDS\[i]: max decreasing subsequence starting at i

Then, compute: `LBS[i] = LIS[i] + LDS[i] - 1`

---

#### 📘 Code

```js
function longestBitonicSubsequence(nums) {
  const n = nums.length;
  const LIS = Array(n).fill(1);
  const LDS = Array(n).fill(1);

  // Compute LIS
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < i; j++) {
      if (nums[i] > nums[j]) {
        LIS[i] = Math.max(LIS[i], LIS[j] + 1);
      }
    }
  }

  // Compute LDS
  for (let i = n - 1; i >= 0; i--) {
    for (let j = n - 1; j > i; j--) {
      if (nums[i] > nums[j]) {
        LDS[i] = Math.max(LDS[i], LDS[j] + 1);
      }
    }
  }

  // Combine LIS and LDS
  let maxBitonic = 0;
  for (let i = 0; i < n; i++) {
    maxBitonic = Math.max(maxBitonic, LIS[i] + LDS[i] - 1);
  }

  return maxBitonic;
}
```

---

#### 🔍 Dry Run

Input: `[1, 11, 2, 10, 4, 5, 2, 1]`
LIS: `[1, 2, 2, 3, 3, 4, 3, 1]`
LDS: `[1, 5, 1, 4, 3, 3, 2, 1]`
→ max = `LIS[i] + LDS[i] - 1` = **6**

---

#### ⏱ Complexity

- **Time**: O(n²) ✅
- **Space**: O(n) ✅

---

### 🧊 Space Optimization

Not feasible ❌

Why?

- We must retain LIS and LDS arrays for each index to compute final values.
- Hence, O(n) space is **already optimal**.

---

### 📌 Summary Table

| Approach           | Time     | Space   | Notes                                    |
| ------------------ | -------- | ------- | ---------------------------------------- |
| Recursion          | O(2ⁿ) ❌ | O(n)    | Brute force                              |
| Memoization        | O(n²) ✅ | O(n) ✅ | Caches LIS and LDS for each index        |
| Tabulation         | O(n²) ✅ | O(n) ✅ | Best approach                            |
| Space Optimization | ❌       | ❌      | Not applicable (requires full LIS & LDS) |

---

## 🔢 **7. Number of Longest Increasing Subsequences (DP-47)**

### 📘 Problem Statement

Given an array `nums`, return the **number of longest increasing subsequences** (LIS) in it.

A subsequence is strictly increasing if for every pair `i < j`, we have `nums[i] < nums[j]`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: nums = [1, 3, 5, 4, 7]
Output: 2
Explanation: LIS = [1,3,4,7] and [1,3,5,7]
```

#### ✅ Test Case 2:

```txt
Input: nums = [2, 2, 2, 2]
Output: 4
Explanation: Each single 2 is a LIS of length 1
```

#### ✅ Test Case 3:

```txt
Input: nums = [1, 2, 4, 3, 5, 4, 7, 2]
Output: 3
```

---

### 🚀 Approach 1: Recursion (TLE ❌)

#### 🧠 Intuition

We try all possible increasing subsequences and count the number of longest ones.

---

#### 📘 Code

```js
function countLIS(nums) {
  let maxLen = 0,
    count = 0;

  function dfs(i, prev, length) {
    if (i === nums.length) {
      if (length > maxLen) {
        maxLen = length;
        count = 1;
      } else if (length === maxLen) {
        count++;
      }
      return;
    }

    // Option 1: Include nums[i]
    if (prev === -1 || nums[i] > nums[prev]) {
      dfs(i + 1, i, length + 1);
    }

    // Option 2: Skip nums[i]
    dfs(i + 1, prev, length);
  }

  dfs(0, -1, 0);
  return count;
}
```

---

#### ❌ Issues

- Explores all 2ⁿ subsequences
- Time complexity is exponential

---

#### ⏱ Complexity

- **Time**: O(2ⁿ)
- **Space**: O(n)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Observation

Memoizing combinations of index and previous element is tricky because we also need to track the **count** of each length. So memoization becomes **too complex** to be efficient.

Hence, we skip memoization and move to the standard and accepted…

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

#### 🧠 Intuition

We use **2 arrays**:

- `dp[i]`: Length of LIS ending at index `i`
- `count[i]`: Number of such LIS ending at index `i`

---

#### 📘 Code

```js
function countLIS(nums) {
  const n = nums.length;
  const dp = Array(n).fill(1);
  const count = Array(n).fill(1);

  let maxLen = 1;

  for (let i = 0; i < n; i++) {
    for (let j = 0; j < i; j++) {
      if (nums[i] > nums[j]) {
        if (dp[j] + 1 > dp[i]) {
          dp[i] = dp[j] + 1;
          count[i] = count[j];
        } else if (dp[j] + 1 === dp[i]) {
          count[i] += count[j];
        }
      }
    }
    maxLen = Math.max(maxLen, dp[i]);
  }

  let totalCount = 0;
  for (let i = 0; i < n; i++) {
    if (dp[i] === maxLen) {
      totalCount += count[i];
    }
  }

  return totalCount;
}
```

---

#### 🔍 Dry Run

For `nums = [1, 3, 5, 4, 7]`:

```txt
dp:     [1, 2, 3, 3, 4]
count:  [1, 1, 1, 1, 2]
maxLen = 4
Result = count of elements with dp[i] == 4 → count[4] = 2
```

---

#### ⏱ Complexity

- **Time**: O(n²)
- **Space**: O(n)

---

### 🧊 Space Optimization

🧨 Not possible here.

#### ❓ Why?

We need:

- `dp[i]` to store LIS lengths
- `count[i]` to store number of ways to reach that length

Both are essential and can't be compressed further into constant space.

---

### 📌 Summary Table

| Approach           | Time      | Space     | Notes                                     |
| ------------------ | --------- | --------- | ----------------------------------------- |
| Recursion          | O(2ⁿ) ❌  | O(n)      | Too slow                                  |
| Memoization        | ✖ Skipped | ✖ Complex | Unwieldy due to count tracking complexity |
| Tabulation         | O(n²) ✅  | O(n) ✅   | Efficient and standard                    |
| Space Optimization | ❌        | ❌        | Not possible (2 arrays needed)            |

---

# Partition DP

## 🔢 **1. Matrix Chain Multiplication (DP-42)**

### 📘 Problem Statement

Given a sequence of matrices, find the **minimum number of scalar multiplications** needed to multiply the chain of matrices.

You are given an array `dims` of length `n+1` where the `i`th matrix has dimensions `dims[i-1] x dims[i]`. The goal is to parenthesize the product to minimize the cost.

> The cost of multiplying a matrix `A` of dimension `p x q` with `B` of dimension `q x r` is `p * q * r`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: dims = [1, 2, 3, 4]
Output: 18
Explanation:
Matrices: A1(1x2), A2(2x3), A3(3x4)
Minimum cost = 18 by ((A1 x A2) x A3)
```

#### ✅ Test Case 2:

```txt
Input: dims = [40, 20, 30, 10, 30]
Output: 26000
Explanation:
Minimum cost achieved by optimal parenthesization.
```

#### ✅ Test Case 3:

```txt
Input: dims = [10, 20, 30]
Output: 6000
```

---

### 🚀 Approach 1: Recursion (Brute Force)

#### 🧠 Intuition

At each step, try all possible places to split the chain into two parts, recursively calculate the cost of multiplying each part, and add the cost of multiplying the two resulting matrices.

---

#### 📘 Code

```js
function matrixChainRecursion(dims, i, j) {
  if (i === j) return 0;

  let minCost = Infinity;

  for (let k = i; k < j; k++) {
    const costLeft = matrixChainRecursion(dims, i, k);
    const costRight = matrixChainRecursion(dims, k + 1, j);
    const costMerge = dims[i - 1] * dims[k] * dims[j];
    const totalCost = costLeft + costRight + costMerge;

    minCost = Math.min(minCost, totalCost);
  }

  return minCost;
}

function matrixChainMultiplication(dims) {
  const n = dims.length;
  return matrixChainRecursion(dims, 1, n - 1);
}
```

---

#### ⏱ Complexity

- **Time**: O(2^n) ❌ (Exponential due to repeated subproblems)
- **Space**: O(n) (Recursion stack)

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Optimization Idea

Store results of subproblems in a 2D DP array to avoid recomputation.

---

#### 📘 Code

```js
function matrixChainMemo(dims) {
  const n = dims.length;
  const dp = Array.from({ length: n }, () => Array(n).fill(-1));

  function solve(i, j) {
    if (i === j) return 0;
    if (dp[i][j] !== -1) return dp[i][j];

    let minCost = Infinity;

    for (let k = i; k < j; k++) {
      const costLeft = solve(i, k);
      const costRight = solve(k + 1, j);
      const costMerge = dims[i - 1] * dims[k] * dims[j];
      const totalCost = costLeft + costRight + costMerge;

      minCost = Math.min(minCost, totalCost);
    }

    dp[i][j] = minCost;
    return minCost;
  }

  return solve(1, n - 1);
}
```

---

#### ⏱ Complexity

- **Time**: O(n³) ✅
- **Space**: O(n²) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

---

#### 📘 Code

```js
function matrixChainTabulation(dims) {
  const n = dims.length;
  const dp = Array.from({ length: n }, () => Array(n).fill(0));

  for (let length = 2; length < n; length++) {
    for (let i = 1; i <= n - length; i++) {
      const j = i + length - 1;
      dp[i][j] = Infinity;

      for (let k = i; k < j; k++) {
        const cost = dp[i][k] + dp[k + 1][j] + dims[i - 1] * dims[k] * dims[j];
        dp[i][j] = Math.min(dp[i][j], cost);
      }
    }
  }

  return dp[1][n - 1];
}
```

---

#### ⏱ Complexity

- **Time**: O(n³) ✅
- **Space**: O(n²)

---

### 🧊 Approach 4: Space Optimization

Matrix Chain Multiplication inherently needs 2D DP because each subproblem depends on intervals `[i..j]`. Hence, **space optimization beyond 2D is not generally applicable**.

---

### 🔍 Dry Run Example: dims = \[1, 2, 3, 4]

```txt
We want to compute minimum multiplication cost for matrices:
A1: 1x2, A2: 2x3, A3: 3x4

Possible splits:
- Split at k=1:
  cost = matrixChain(1,1) + matrixChain(2,3) + 1*2*4
       = 0 + cost(2,3) + 8
       = 0 + (cost for multiplying A2 and A3) + 8
- Split at k=2:
  cost = matrixChain(1,2) + matrixChain(3,3) + 1*3*4
       = cost(1,2) + 0 + 12

Calculate and choose minimum.
Final answer = 18
```

---

### 📌 Summary Table

| Approach            | Time         | Space | Notes                           |
| ------------------- | ------------ | ----- | ------------------------------- |
| Recursion           | O(2^n) ❌    | O(n)  | Brute force                     |
| Memoization (Top)   | O(n³) ✅     | O(n²) | Avoids recomputation            |
| Tabulation (Bottom) | O(n³) ✅     | O(n²) | Iterative DP                    |
| Space Optimization  | Not feasible | N/A   | 2D DP required due to intervals |

---

## 🔢 **2. Minimum Cost to Cut the Stick (DP-43)**

### 📘 Problem Statement

You are given a stick of length `n` and an array `cuts` where each element represents a position to cut the stick.

When you cut the stick at position `x`, the cost is equal to the length of the stick segment being cut.

Return the **minimum total cost** to perform all cuts in any order.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: n = 7, cuts = [1, 3, 4, 5]
Output: 16
Explanation:
One optimal order of cuts is [3, 5, 1, 4].
Total cost = 7 + 4 + 3 + 2 = 16
```

#### ✅ Test Case 2:

```txt
Input: n = 9, cuts = [5, 6, 1, 4, 2]
Output: 22
```

---

### 🚀 Approach 1: Recursion (Brute Force)

#### 🧠 Intuition

At each step, pick a cut to perform next between current segment boundaries `start` and `end`. The cost of cutting at position `cut` is `(end - start)`. Recursively solve for left and right segments and add cost.

Try all possible cuts in the current segment and take the minimum cost.

---

#### 📘 Code

```js
function minCostRecursion(n, cuts, start = 0, end = n) {
  if (cuts.length === 0) return 0;

  let minCost = Infinity;

  for (let i = 0; i < cuts.length; i++) {
    const cut = cuts[i];

    // Only consider cuts within current segment
    if (cut > start && cut < end) {
      // Remaining cuts excluding current cut
      const leftCuts = cuts.filter((c) => c < cut);
      const rightCuts = cuts.filter((c) => c > cut);

      const costLeft = minCostRecursion(n, leftCuts, start, cut);
      const costRight = minCostRecursion(n, rightCuts, cut, end);

      const cost = end - start + costLeft + costRight;
      minCost = Math.min(minCost, cost);
    }
  }

  return minCost === Infinity ? 0 : minCost;
}
```

---

#### ⏱ Complexity

- **Time**: Exponential, O(k!) in worst case (k = number of cuts) ❌
- **Space**: O(k) recursion stack

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Optimization Idea

Sort the cuts and add boundaries `0` and `n` to form an extended array. Use DP to store minimum cost between cuts `i` and `j`. The problem reduces to finding the minimum cost to cut the segment between `cuts[i]` and `cuts[j]`.

---

#### 📘 Code

```js
function minCost(n, cuts) {
  cuts.push(0, n);
  cuts.sort((a, b) => a - b);

  const m = cuts.length;
  const dp = Array.from({ length: m }, () => Array(m).fill(-1));

  function solve(i, j) {
    if (j - i <= 1) return 0; // No cuts possible between i and j

    if (dp[i][j] !== -1) return dp[i][j];

    let minCost = Infinity;
    for (let k = i + 1; k < j; k++) {
      const costLeft = solve(i, k);
      const costRight = solve(k, j);
      const cost = cuts[j] - cuts[i] + costLeft + costRight;
      minCost = Math.min(minCost, cost);
    }

    return (dp[i][j] = minCost);
  }

  return solve(0, m - 1);
}
```

---

#### ⏱ Complexity

- **Time**: O(k³) ✅
- **Space**: O(k²) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

---

#### 📘 Code

```js
function minCost(n, cuts) {
  cuts.push(0, n);
  cuts.sort((a, b) => a - b);

  const m = cuts.length;
  const dp = Array.from({ length: m }, () => Array(m).fill(0));

  for (let length = 2; length < m; length++) {
    for (let i = 0; i + length < m; i++) {
      const j = i + length;
      dp[i][j] = Infinity;

      for (let k = i + 1; k < j; k++) {
        const cost = cuts[j] - cuts[i] + dp[i][k] + dp[k][j];
        dp[i][j] = Math.min(dp[i][j], cost);
      }
    }
  }

  return dp[0][m - 1];
}
```

---

#### ⏱ Complexity

- **Time**: O(k³) ✅
- **Space**: O(k²)

---

### 🔍 Dry Run Example: n = 7, cuts = \[1, 3, 4, 5]

```txt
Sorted cuts = [0,1,3,4,5,7]

Calculate minimum cost for segments:
- Between 0 and 7 considering all cuts
- Break problem into subproblems like (0,3), (3,7), etc.

Final minimum cost = 16
```

---

### 📌 Summary Table

| Approach            | Time     | Space | Notes                  |
| ------------------- | -------- | ----- | ---------------------- |
| Recursion           | O(k!) ❌ | O(k)  | Brute force            |
| Memoization (Top)   | O(k³) ✅ | O(k²) | Efficient top-down DP  |
| Tabulation (Bottom) | O(k³) ✅ | O(k²) | Iterative bottom-up DP |

---

## 🔢 **3. Burst Balloons (DP-44)**

### 📘 Problem Statement

You are given `n` balloons, indexed from `0` to `n-1`. Each balloon has a number on it represented by an array `nums`.

You want to burst all the balloons. When you burst balloon `i`, you get coins equal to:

```
nums[left] * nums[i] * nums[right]
```

where `left` and `right` are the indices of the balloons adjacent to `i` **before** bursting it.

If `left` or `right` does not exist (balloon is at boundary), treat the value as `1`.

Return the **maximum coins** you can collect by bursting the balloons wisely.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: nums = [3,1,5,8]
Output: 167
Explanation:
Burst balloons in order 1,5,3,8 (or another optimal sequence) to get max coins.
```

#### ✅ Test Case 2:

```txt
Input: nums = [1,5]
Output: 10
```

---

### 🚀 Approach 1: Recursion (Brute Force)

#### 🧠 Intuition

We think about the last balloon to burst in a subarray `[left, right]`. If we fix balloon `i` as the last balloon to burst in this range, the coins gained are:

```
nums[left-1] * nums[i] * nums[right+1] + coins from bursting left..i-1 + coins from bursting i+1..right
```

Recursively calculate the max coins by trying every balloon as the last burst in the current range.

---

#### 📘 Code

```js
function maxCoinsRecursion(nums, left, right) {
  if (left > right) return 0;

  let maxCoins = 0;

  for (let i = left; i <= right; i++) {
    const coins = (nums[left - 1] || 1) * nums[i] * (nums[right + 1] || 1);
    const coinsLeft = maxCoinsRecursion(nums, left, i - 1);
    const coinsRight = maxCoinsRecursion(nums, i + 1, right);

    maxCoins = Math.max(maxCoins, coins + coinsLeft + coinsRight);
  }

  return maxCoins;
}

function maxCoins(nums) {
  const n = nums.length;
  // Pad nums with 1 at both ends
  const padded = [1, ...nums, 1];
  return maxCoinsRecursion(padded, 1, n);
}
```

---

#### ⏱ Complexity

- **Time**: Exponential, O(n!) ❌
- **Space**: O(n) recursion stack

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Optimization Idea

Store results of subproblems `(left, right)` in a 2D DP array to avoid recomputation.

---

#### 📘 Code

```js
function maxCoins(nums) {
  const n = nums.length;
  const padded = [1, ...nums, 1];
  const dp = Array.from({ length: n + 2 }, () => Array(n + 2).fill(-1));

  function solve(left, right) {
    if (left > right) return 0;
    if (dp[left][right] !== -1) return dp[left][right];

    let maxCoins = 0;

    for (let i = left; i <= right; i++) {
      const coins = padded[left - 1] * padded[i] * padded[right + 1];
      const coinsLeft = solve(left, i - 1);
      const coinsRight = solve(i + 1, right);

      maxCoins = Math.max(maxCoins, coins + coinsLeft + coinsRight);
    }

    return (dp[left][right] = maxCoins);
  }

  return solve(1, n);
}
```

---

#### ⏱ Complexity

- **Time**: O(n³) ✅
- **Space**: O(n²) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

---

#### 📘 Code

```js
function maxCoins(nums) {
  const n = nums.length;
  const padded = [1, ...nums, 1];
  const dp = Array.from({ length: n + 2 }, () => Array(n + 2).fill(0));

  for (let length = 1; length <= n; length++) {
    for (let left = 1; left <= n - length + 1; left++) {
      const right = left + length - 1;
      for (let i = left; i <= right; i++) {
        const coins = padded[left - 1] * padded[i] * padded[right + 1];
        const totalCoins = coins + dp[left][i - 1] + dp[i + 1][right];
        dp[left][right] = Math.max(dp[left][right], totalCoins);
      }
    }
  }

  return dp[1][n];
}
```

---

#### ⏱ Complexity

- **Time**: O(n³) ✅
- **Space**: O(n²)

---

### 🔍 Dry Run Example: nums = \[3,1,5,8]

```txt
padded = [1,3,1,5,8,1]

Calculate dp for subarrays of length 1 to n:
- length = 1: max coins bursting single balloon
- length = 2: combine results of smaller subproblems
...
Final result dp[1][4] = 167
```

---

### 📌 Summary Table

| Approach            | Time     | Space | Notes                  |
| ------------------- | -------- | ----- | ---------------------- |
| Recursion           | O(n!) ❌ | O(n)  | Brute force            |
| Memoization (Top)   | O(n³) ✅ | O(n²) | Efficient top-down DP  |
| Tabulation (Bottom) | O(n³) ✅ | O(n²) | Iterative bottom-up DP |

---

## 🔢 **4. Evaluate Boolean Expression to True (DP-45)**

### 📘 Problem Statement

Given a boolean expression string `S` consisting of:

- `'T'` (True)
- `'F'` (False)
- Operators: `'&'` (AND), `'|'` (OR), and `'^'` (XOR)

Count the number of ways to parenthesize the expression such that it evaluates to **True**.

Return the count **modulo** `10^9 + 7`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: S = "T|F&T^F"
Output: 5
```

#### ✅ Test Case 2:

```txt
Input: S = "T^T^F"
Output: 0
Explanation: No parenthesization results in True.
```

---

### 🚀 Approach 1: Recursion (Brute Force)

#### 🧠 Intuition

At each operator, split the expression into left and right parts.

- Calculate ways left can be True/False.
- Calculate ways right can be True/False.
- Combine results according to the operator's truth table.
- Accumulate count of ways to get True for full expression.

---

#### 📘 Code

```js
const MOD = 1e9 + 7;

function countWaysRec(expr, i, j, isTrue) {
  if (i > j) return 0;

  if (i === j) {
    if (isTrue) return expr[i] === "T" ? 1 : 0;
    else return expr[i] === "F" ? 1 : 0;
  }

  let ways = 0;

  for (let k = i + 1; k <= j - 1; k += 2) {
    const leftTrue = countWaysRec(expr, i, k - 1, true);
    const leftFalse = countWaysRec(expr, i, k - 1, false);
    const rightTrue = countWaysRec(expr, k + 1, j, true);
    const rightFalse = countWaysRec(expr, k + 1, j, false);

    const op = expr[k];

    if (op === "&") {
      if (isTrue) ways += leftTrue * rightTrue;
      else
        ways +=
          leftTrue * rightFalse +
          leftFalse * rightTrue +
          leftFalse * rightFalse;
    } else if (op === "|") {
      if (isTrue)
        ways +=
          leftTrue * rightTrue + leftTrue * rightFalse + leftFalse * rightTrue;
      else ways += leftFalse * rightFalse;
    } else if (op === "^") {
      if (isTrue) ways += leftTrue * rightFalse + leftFalse * rightTrue;
      else ways += leftTrue * rightTrue + leftFalse * rightFalse;
    }
  }

  return ways % MOD;
}

function countWays(expression) {
  return countWaysRec(expression, 0, expression.length - 1, true);
}
```

---

#### ⏱ Complexity

- **Time**: Exponential, O(2^n) ❌
- **Space**: O(n) recursion stack

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Optimization Idea

Use 3D DP cache: `dp[i][j][isTrue]` to store number of ways expression `i..j` evaluates to `isTrue`.

---

#### 📘 Code

```js
const MOD = 1e9 + 7;

function countWays(expression) {
  const n = expression.length;
  const dp = Array.from({ length: n }, () =>
    Array.from({ length: n }, () => Array(2).fill(-1))
  );

  function solve(i, j, isTrue) {
    if (i > j) return 0;

    if (i === j) {
      if (isTrue) return expression[i] === "T" ? 1 : 0;
      else return expression[i] === "F" ? 1 : 0;
    }

    if (dp[i][j][isTrue ? 1 : 0] !== -1) return dp[i][j][isTrue ? 1 : 0];

    let ways = 0;

    for (let k = i + 1; k <= j - 1; k += 2) {
      const leftTrue = solve(i, k - 1, true);
      const leftFalse = solve(i, k - 1, false);
      const rightTrue = solve(k + 1, j, true);
      const rightFalse = solve(k + 1, j, false);

      const op = expression[k];

      if (op === "&") {
        if (isTrue) ways += leftTrue * rightTrue;
        else
          ways +=
            leftTrue * rightFalse +
            leftFalse * rightTrue +
            leftFalse * rightFalse;
      } else if (op === "|") {
        if (isTrue)
          ways +=
            leftTrue * rightTrue +
            leftTrue * rightFalse +
            leftFalse * rightTrue;
        else ways += leftFalse * rightFalse;
      } else if (op === "^") {
        if (isTrue) ways += leftTrue * rightFalse + leftFalse * rightTrue;
        else ways += leftTrue * rightTrue + leftFalse * rightFalse;
      }
      ways %= MOD;
    }

    dp[i][j][isTrue ? 1 : 0] = ways;
    return ways;
  }

  return solve(0, n - 1, true);
}
```

---

#### ⏱ Complexity

- **Time**: O(n³) ✅
- **Space**: O(n²) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

---

#### 📘 Code

```js
function countWays(expression) {
  const MOD = 1e9 + 7;
  const n = expression.length;

  const dpTrue = Array.from({ length: n }, () => Array(n).fill(0));
  const dpFalse = Array.from({ length: n }, () => Array(n).fill(0));

  for (let i = 0; i < n; i += 2) {
    dpTrue[i][i] = expression[i] === "T" ? 1 : 0;
    dpFalse[i][i] = expression[i] === "F" ? 1 : 0;
  }

  for (let length = 3; length <= n; length += 2) {
    for (let i = 0; i <= n - length; i += 2) {
      const j = i + length - 1;
      dpTrue[i][j] = 0;
      dpFalse[i][j] = 0;

      for (let k = i + 1; k < j; k += 2) {
        const op = expression[k];

        const leftTrue = dpTrue[i][k - 1];
        const leftFalse = dpFalse[i][k - 1];
        const rightTrue = dpTrue[k + 1][j];
        const rightFalse = dpFalse[k + 1][j];

        if (op === "&") {
          dpTrue[i][j] += leftTrue * rightTrue;
          dpFalse[i][j] +=
            leftTrue * rightFalse +
            leftFalse * rightTrue +
            leftFalse * rightFalse;
        } else if (op === "|") {
          dpTrue[i][j] +=
            leftTrue * rightTrue +
            leftTrue * rightFalse +
            leftFalse * rightTrue;
          dpFalse[i][j] += leftFalse * rightFalse;
        } else if (op === "^") {
          dpTrue[i][j] += leftTrue * rightFalse + leftFalse * rightTrue;
          dpFalse[i][j] += leftTrue * rightTrue + leftFalse * rightFalse;
        }

        dpTrue[i][j] %= MOD;
        dpFalse[i][j] %= MOD;
      }
    }
  }

  return dpTrue[0][n - 1];
}
```

---

#### ⏱ Complexity

- **Time**: O(n³) ✅
- **Space**: O(n²)

---

### 🔍 Dry Run Example: S = "T|F\&T^F"

```txt
Length = 7 (chars)
Operators at odd indices: 1,3,5
Calculate dpTrue and dpFalse for substrings of increasing length.
Final dpTrue[0][6] = 5 ways
```

---

### 📌 Summary Table

| Approach            | Time      | Space | Notes                  |
| ------------------- | --------- | ----- | ---------------------- |
| Recursion           | O(2^n) ❌ | O(n)  | Brute force            |
| Memoization (Top)   | O(n³) ✅  | O(n²) | Efficient with caching |
| Tabulation (Bottom) | O(n³) ✅  | O(n²) | Iterative DP           |

---

## 🔢 **5. Palindrome Partitioning - II (DP-46)**

### 📘 Problem Statement

Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**.

Return the **minimum number of cuts** needed to partition the string into palindromic substrings.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: s = "aab"
Output: 1
Explanation: The palindrome partitioning ["aa","b"] could be produced using 1 cut.
```

#### ✅ Test Case 2:

```txt
Input: s = "a"
Output: 0
Explanation: "a" is already a palindrome, no cuts needed.
```

#### ✅ Test Case 3:

```txt
Input: s = "ab"
Output: 1
```

---

### 🚀 Approach 1: Recursion (Brute Force)

#### 🧠 Intuition

Try all possible partitions, and if the substring `s[i..j]` is palindrome, recursively find minimum cuts in `s[j+1..end]`.

---

#### 📘 Code

```js
function isPalindrome(s, start, end) {
  while (start < end) {
    if (s[start] !== s[end]) return false;
    start++;
    end--;
  }
  return true;
}

function minCutRec(s, start) {
  if (start === s.length) return 0;

  let minCuts = Infinity;

  for (let end = start; end < s.length; end++) {
    if (isPalindrome(s, start, end)) {
      const cuts = 1 + minCutRec(s, end + 1);
      minCuts = Math.min(minCuts, cuts);
    }
  }

  return minCuts;
}

function minCut(s) {
  return minCutRec(s, 0) - 1; // subtract 1 because last cut is not needed
}
```

---

#### ⏱ Complexity

- **Time**: Exponential, O(2^n) ❌
- **Space**: O(n) recursion stack

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Optimization Idea

Use a 1D DP array to memoize minimum cuts for substring starting at each index.

---

#### 📘 Code

```js
function minCut(s) {
  const n = s.length;
  const dp = new Array(n).fill(-1);

  function isPalindrome(str, start, end) {
    while (start < end) {
      if (str[start] !== str[end]) return false;
      start++;
      end--;
    }
    return true;
  }

  function solve(start) {
    if (start === n) return 0;
    if (dp[start] !== -1) return dp[start];

    let minCuts = Infinity;

    for (let end = start; end < n; end++) {
      if (isPalindrome(s, start, end)) {
        const cuts = 1 + solve(end + 1);
        minCuts = Math.min(minCuts, cuts);
      }
    }

    return (dp[start] = minCuts);
  }

  return solve(0) - 1;
}
```

---

#### ⏱ Complexity

- **Time**: O(n² \* n) = O(n³) (due to palindrome check inside loop)
- **Space**: O(n) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP) with Palindrome Preprocessing

---

#### 🧠 Optimization Idea

Precompute a 2D `isPal[i][j]` table to know if substring `s[i..j]` is palindrome in O(1).

Then compute minimum cuts using DP.

---

#### 📘 Code

```js
function minCut(s) {
  const n = s.length;
  const isPal = Array.from({ length: n }, () => Array(n).fill(false));

  // Precompute palindrome substrings
  for (let i = 0; i < n; i++) isPal[i][i] = true;

  for (let length = 2; length <= n; length++) {
    for (let i = 0; i <= n - length; i++) {
      let j = i + length - 1;
      if (s[i] === s[j]) {
        if (length === 2) isPal[i][j] = true;
        else isPal[i][j] = isPal[i + 1][j - 1];
      }
    }
  }

  const dp = new Array(n + 1).fill(0);
  dp[n] = 0; // no cuts needed beyond end

  for (let i = n - 1; i >= 0; i--) {
    let minCuts = Infinity;
    for (let j = i; j < n; j++) {
      if (isPal[i][j]) {
        const cuts = 1 + dp[j + 1];
        minCuts = Math.min(minCuts, cuts);
      }
    }
    dp[i] = minCuts;
  }

  return dp[0] - 1;
}
```

---

#### ⏱ Complexity

- **Time**: O(n²) ✅
- **Space**: O(n²) + O(n)

---

#### 🔍 Dry Run Example: s = "aab"

```txt
isPal matrix:
a   a   b
T   T   F
    T   F
        T

dp array from end:
dp[3] = 0
dp[2] = 1 (cut after 'b')
dp[1] = 1 (cut after 'a')
dp[0] = 1 (cut after "aa")

Result = dp[0] - 1 = 0 cuts
But since "aa" is palindrome, we only need 1 cut in total.
```

---

### ✅ **Optimized DP: Precompute Palindromes + Bottom-Up DP**

#### 🔍 Observation:

A string is a palindrome if:

- The first and last characters are equal: `s[i] === s[j]`
- The middle part `s[i+1..j-1]` is also a palindrome

So we can build `isPal[i][j]` using this recurrence:

```
isPal[i][j] = (s[i] === s[j]) && isPal[i+1][j-1]
```

---

#### 🧠 Base Cases:

- Every **single character** is a palindrome: `isPal[i][i] = true`
- Every **two-character substring** is a palindrome **if** `s[i] === s[i+1]`

---

#### 🔁 Build in Bottom-Up Order:

Start from shorter substrings and use their results to build longer substrings.

- First fill substrings of length 1
- Then length 2
- Then build up to length n

So when computing `isPal[i][j]`, the value of `isPal[i+1][j-1]` is already known.

---

#### 📦 Result:

After building `isPal`, any time we want to check whether `s[i..j]` is a palindrome, we just lookup:

```js
if (isPal[i][j]) {
  // proceed
}
```

This lookup takes **O(1)** time ✅

---

#### ✅ Code

```js
function minCut(s) {
  const n = s.length;
  const isPal = Array.from({ length: n }, () => Array(n).fill(false));

  // Precompute isPal[i][j]
  for (let i = n - 1; i >= 0; i--) {
    for (let j = i; j < n; j++) {
      if (s[i] === s[j]) {
        if (j - i <= 1) {
          isPal[i][j] = true; // length 1 or 2
        } else {
          isPal[i][j] = isPal[i + 1][j - 1];
        }
      }
    }
  }

  const dp = new Array(n + 1).fill(0);
  dp[n] = 0; // no cut needed beyond string

  for (let i = n - 1; i >= 0; i--) {
    let minCuts = Infinity;

    for (let j = i; j < n; j++) {
      if (isPal[i][j]) {
        const cuts = 1 + dp[j + 1];
        minCuts = Math.min(minCuts, cuts);
      }
    }

    dp[i] = minCuts;
  }

  return dp[0] - 1; // subtract final unnecessary cut
}
```

---

#### 🧪 Test Cases

```js
console.log(minCut("aab")); // 1
console.log(minCut("a")); // 0
console.log(minCut("ab")); // 1
console.log(minCut("racecar")); // 0
console.log(minCut("banana")); // 1 => ["b", "anana"]
```

---

#### ⏱ Time & Space Complexity

| Component          | Complexity |
| ------------------ | ---------- |
| Precomputing isPal | O(n²)      |
| Filling DP array   | O(n²)      |
| **Total Time**     | ✅ O(n²)   |
| **Space**          | O(n²)      |

---

#### 📌 Summary Table

| Approach                               | Time     | Space | Notes                            |
| -------------------------------------- | -------- | ----- | -------------------------------- |
| Recursion                              | O(2ⁿ) ❌ | O(n)  | Brute force                      |
| Memoization (Top-Down)                 | O(n³) ❌ | O(n)  | DP + on-the-fly palindrome check |
| ✅ Tabulation + Precomputed Palindrome | O(n²) ✅ | O(n²) | Fastest with boolean table       |

---

## 🔢 **6. Partition Array for Maximum Sum (DP-47)**

### 📘 Problem Statement

Given an integer array `arr` and an integer `k`, partition the array into contiguous subarrays of length **at most** `k`.

After partitioning, each subarray's values are replaced by the maximum value in that subarray.

Return the **maximum sum** of the array after partitioning.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input: arr = [1,15,7,9,2,5,10], k = 3
Output: 84
Explanation:
Partition into [15,15,15], [9,9,9], [10]
Sum = 15 + 15 + 15 + 9 + 9 + 9 + 10 = 84
```

#### ✅ Test Case 2:

```txt
Input: arr = [1,4,1,5,7,3,6,1,9,9,3], k = 4
Output: 83
```

---

### 🚀 Approach 1: Recursion (Brute Force)

#### 🧠 Intuition

Try all possible partitions starting at each index with lengths up to `k`.

For each partition, find the maximum value in that subarray and recursively solve the rest.

---

#### 📘 Code

```js
function maxSumAfterPartitioning(arr, k, start = 0) {
  if (start === arr.length) return 0;

  let maxSum = 0;
  let maxInPartition = 0;

  for (let length = 1; length <= k && start + length <= arr.length; length++) {
    maxInPartition = Math.max(maxInPartition, arr[start + length - 1]);
    const currentSum =
      maxInPartition * length + maxSumAfterPartitioning(arr, k, start + length);
    maxSum = Math.max(maxSum, currentSum);
  }

  return maxSum;
}
```

---

#### ⏱ Complexity

- **Time**: Exponential, O(k^n) ❌
- **Space**: O(n) recursion stack

---

### ✅ Approach 2: Memoization (Top-Down DP)

#### 🧠 Optimization Idea

Store computed maximum sum from index `start` to the end in a DP array to avoid recomputation.

---

#### 📘 Code

```js
function maxSumAfterPartitioning(arr, k) {
  const n = arr.length;
  const dp = new Array(n).fill(-1);

  function solve(start) {
    if (start === n) return 0;
    if (dp[start] !== -1) return dp[start];

    let maxSum = 0;
    let maxInPartition = 0;

    for (let length = 1; length <= k && start + length <= n; length++) {
      maxInPartition = Math.max(maxInPartition, arr[start + length - 1]);
      const currentSum = maxInPartition * length + solve(start + length);
      maxSum = Math.max(maxSum, currentSum);
    }

    return (dp[start] = maxSum);
  }

  return solve(0);
}
```

---

#### ⏱ Complexity

- **Time**: O(n \* k) ✅
- **Space**: O(n) + recursion stack

---

### 🧮 Approach 3: Tabulation (Bottom-Up DP)

---

#### 📘 Code

```js
function maxSumAfterPartitioning(arr, k) {
  const n = arr.length;
  const dp = new Array(n + 1).fill(0);
  dp[n] = 0; // Base case: no elements left

  for (let i = n - 1; i >= 0; i--) {
    let maxSum = 0;
    let maxInPartition = 0;

    for (let length = 1; length <= k && i + length <= n; length++) {
      maxInPartition = Math.max(maxInPartition, arr[i + length - 1]);
      const currentSum = maxInPartition * length + dp[i + length];
      maxSum = Math.max(maxSum, currentSum);
    }

    dp[i] = maxSum;
  }

  return dp[0];
}
```

---

#### ⏱ Complexity

- **Time**: O(n \* k) ✅
- **Space**: O(n)

---

### 🔍 Dry Run Example: arr = \[1,15,7,9,2,5,10], k = 3

```txt
Start from the right:
dp[7] = 0
dp[6] = max(10*1 + dp[7]) = 10
dp[5] = max(5*1 + dp[6], 5*2 + dp[7]) = max(5+10, 10+0) = 15
dp[4] = max(2*1 + dp[5], 9*2 + dp[6], 15*3 + dp[7]) ...
...
dp[0] = 84 (final answer)
```

---

### 📌 Summary Table

| Approach            | Time       | Space | Notes                    |
| ------------------- | ---------- | ----- | ------------------------ |
| Recursion           | O(k^n) ❌  | O(n)  | Brute force              |
| Memoization (Top)   | O(n\*k) ✅ | O(n)  | Cached recursion results |
| Tabulation (Bottom) | O(n\*k) ✅ | O(n)  | Iterative DP             |

---

# DP On Squares

## 🔢 **1. Maximum Rectangle Area with all 1's (DP-48)**

### 📘 Problem Statement

Given a binary matrix `matrix` of size `m x n`, find the area of the **largest rectangle containing only 1's**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input:
matrix = [
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
Output: 6
Explanation: The largest rectangle is of area 6.
```

#### ✅ Test Case 2:

```txt
Input:
matrix = [["0"]]
Output: 0
```

---

### 🚀 Approach 1: Using Largest Rectangle in Histogram (DP + Stack)

#### 🧠 Intuition

- Treat each row of the matrix as the base of a histogram.
- For each row, compute the height of continuous '1's column-wise.
- Then find the largest rectangle area in that histogram.
- The maximum of these areas across all rows is the answer.

---

### Step 1: Largest Rectangle in Histogram (Helper)

Given an array of heights, find the largest rectangle area in the histogram.

---

#### 📘 Largest Rectangle in Histogram Code

```js
function largestRectangleArea(heights) {
  const stack = [];
  let maxArea = 0;
  heights.push(0); // Sentinel to pop all remaining bars

  for (let i = 0; i < heights.length; i++) {
    while (stack.length && heights[i] < heights[stack[stack.length - 1]]) {
      const height = heights[stack.pop()];
      const width = stack.length === 0 ? i : i - stack[stack.length - 1] - 1;
      maxArea = Math.max(maxArea, height * width);
    }
    stack.push(i);
  }

  heights.pop(); // Remove sentinel
  return maxArea;
}
```

---

### Step 2: Use this helper on each row’s histogram heights

---

#### 📘 Full Code

```js
function maximalRectangle(matrix) {
  if (matrix.length === 0) return 0;

  const rows = matrix.length;
  const cols = matrix[0].length;
  const heights = new Array(cols).fill(0);
  let maxArea = 0;

  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      if (matrix[r][c] === "1") {
        heights[c] += 1;
      } else {
        heights[c] = 0;
      }
    }
    maxArea = Math.max(maxArea, largestRectangleArea(heights));
  }

  return maxArea;
}
```

---

#### ⏱ Complexity

- **Time**: O(m \* n) ✅ (each element processed once, and histogram solved in O(n) per row)
- **Space**: O(n) for heights and stack

---

### 🔍 Dry Run Example

```txt
For row 0: heights = [1,0,1,0,0] -> largest rectangle area = 1
For row 1: heights = [2,0,2,1,1] -> largest rectangle area = 3
For row 2: heights = [3,1,3,2,2] -> largest rectangle area = 6 (max so far)
For row 3: heights = [4,0,0,3,0] -> largest rectangle area = 4
Max area = 6
```

---

### 📌 Summary Table

| Approach                 | Time       | Space | Notes                       |
| ------------------------ | ---------- | ----- | --------------------------- |
| Histogram + Stack Method | O(m\*n) ✅ | O(n)  | Optimal and common approach |

---

## 🔢 **2. Count Square Submatrices with All Ones (DP-56)**

### 📘 Problem Statement

Given a binary matrix `matrix` of size `m x n`, return the **number of square submatrices that contain only 1's**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```txt
Input:
matrix = [
  [0,1,1,1],
  [1,1,1,1],
  [0,1,1,1]
]
Output: 15
Explanation: There are 10 squares of size 1x1, 4 squares of size 2x2 and 1 square of size 3x3.
```

#### ✅ Test Case 2:

```txt
Input:
matrix = [
  [1,0,1],
  [1,1,0],
  [1,1,0]
]
Output: 7
```

---

### 🚀 Approach: Dynamic Programming (Bottom-Up)

#### 🧠 Intuition

- Use a DP matrix `dp` of the same size as `matrix`.
- `dp[i][j]` represents the size of the largest square submatrix ending at cell `(i, j)`.
- If `matrix[i][j] == 1`, then:

$$
dp[i][j] = 1 + \min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])
$$

- If `matrix[i][j] == 0`, then `dp[i][j] = 0`.
- The total count of squares is the sum of all `dp[i][j]`.

---

#### 📘 Code

```js
function countSquares(matrix) {
  const m = matrix.length;
  const n = matrix[0].length;
  let count = 0;

  const dp = Array.from({ length: m }, () => Array(n).fill(0));

  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (matrix[i][j] === 1) {
        if (i === 0 || j === 0) {
          dp[i][j] = 1;
        } else {
          dp[i][j] = 1 + Math.min(dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1]);
        }
        count += dp[i][j];
      }
    }
  }

  return count;
}
```

---

#### ⏱ Complexity

- **Time**: O(m \* n) ✅
- **Space**: O(m \* n)

---

### 🔍 Dry Run Example

```txt
Input matrix:
0 1 1 1
1 1 1 1
0 1 1 1
DP matrix:
0 1 1 1
1 1 2 2
0 1 2 3

Sum of DP = 15 (total squares)
```

---

### 📌 Summary Table

| Approach            | Time       | Space   | Notes                         |
| ------------------- | ---------- | ------- | ----------------------------- |
| Dynamic Programming | O(m\*n) ✅ | O(m\*n) | Efficient and straightforward |

---
