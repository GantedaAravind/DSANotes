# 📘 Recursion: Complete Notes

## 🔁 What is Recursion?

**Recursion** is a programming technique where a function calls itself to solve smaller instances of a problem.

> “Divide the problem into smaller sub-problems and solve recursively.”

---

## 🧠 Key Concepts

- **Base Case:** The condition where recursion ends.
- **Recursive Case:** The part where the function calls itself with a smaller input.

---

## 🏗️ Structure of a Recursive Function

```javascript
function recurse(params) {
  if (baseCaseCondition) {
    return result; // Base case
  }
  return recurse(smallerParams); // Recursive case
}
```

---

## 🔄 Types of Recursion

1. **Tail Recursion**

   - Recursive call is the last statement
   - Easier to optimize (some compilers convert it into iteration)

2. **Head Recursion**

   - Recursive call happens before any operation

3. **Tree Recursion**

   - A function calls itself more than once (e.g., Fibonacci)

4. **Indirect Recursion**

   - Multiple functions call each other in a recursive manner

5. **Nested Recursion**

   - Recursion inside the parameters of recursion (e.g., Ackermann’s Function)

> 📌 _Insert images from Google for each type for clarity_

---

## 📊 Time & Space Complexity

| Type          | Time Complexity       | Space Complexity        |
| ------------- | --------------------- | ----------------------- |
| Factorial     | O(n)                  | O(n)                    |
| Fibonacci     | O(2^n) (brute) / O(n) | O(n) (with memoization) |
| Binary Search | O(log n)              | O(log n)                |

---

## 🧮 Examples

### ✅ Example 1: Factorial

**Definition**:
`n! = n × (n-1)!` and `0! = 1`

**Code:**

```javascript
function factorial(n) {
  if (n === 0) return 1; // Base case
  return n * factorial(n - 1); // Recursive case
}
console.log(factorial(5)); // 120
```

**Dry Run:**

```text
factorial(3)
=> 3 * factorial(2)
   => 2 * factorial(1)
       => 1 * factorial(0)
           => 1 (Base case)
       => 1 * 1 = 1
   => 2 * 1 = 2
=> 3 * 2 = 6
```

---

### ✅ Example 2: Fibonacci (Brute Force)

```javascript
function fib(n) {
  if (n <= 1) return n;
  return fib(n - 1) + fib(n - 2);
}
console.log(fib(5)); // 5
```

## ![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRm9qycMjJm6diATbBZp5iTi0w06Dcyv0J-Kg&s)

### ✅ Example 3: Sum of Digits

```javascript
function sumOfDigits(n) {
  if (n === 0) return 0;
  return (n % 10) + sumOfDigits(Math.floor(n / 10));
}
console.log(sumOfDigits(123)); // 6
```

---

## 🧪 Recursion vs Iteration

| Aspect      | Recursion                              | Iteration                      |
| ----------- | -------------------------------------- | ------------------------------ |
| Approach    | Function calls itself                  | Looping (for, while)           |
| Stack Usage | Uses call stack                        | Constant space (in most cases) |
| Performance | Slower due to overhead                 | Faster                         |
| Readability | More intuitive for tree/graph problems | Better for simple loops        |

---

## ⚠️ Common Pitfalls

- Forgetting base case → leads to **infinite recursion**
- Stack Overflow error (too deep recursion)
- Re-computation of sub-problems (→ use memoization)

---

## 🛠️ Tips

- Always define a **base case**
- Prefer **memoization** for overlapping subproblems
- Use **helper functions** for carrying parameters

---

# Basic Problems

## 1. **Recursive Implementation of `atoi()`**

Implement the `atoi()` function recursively, which converts a numeric string into its corresponding integer value.

> Only consider valid input (you can assume the input string contains only digits and an optional leading `-` or `+` sign, no spaces or invalid characters).

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: "1234";
Output: 1234;
```

#### Test Case 2:

```js
Input: "-456";
Output: -456;
```

#### Test Case 3:

```js
Input: "0";
Output: 0;
```

#### Test Case 4:

```js
Input: "+789";
Output: 789;
```

---

### 💡 Intuition

- Recursively convert the substring to integer:

  - Base Case: If the string is empty, return `0`.
  - Convert the first character to a digit and combine it with the result of the recursive call on the rest of the string.

- Handle optional sign (`+` or `-`) at the beginning.

---

### 🔄 Dry Run (Test Case: "-456")

1. Detect `-`, so result will be negative.
2. Recurse on `"456"`:

   - `'4'` → 4 \* 10^2 = 400
   - `'5'` → 5 \* 10^1 = 50
   - `'6'` → 6 \* 10^0 = 6
     → Result = 400 + 50 + 6 = **456**, apply `-` → **-456**

---

### 🧑‍💻 JavaScript Code (Recursive `atoi()`)

```javascript
function recursiveAtoi(str) {
  function helper(s, n) {
    if (s.length === 0) return 0;
    let digit = s.charCodeAt(0) - "0".charCodeAt(0);
    return digit * Math.pow(10, n - 1) + helper(s.slice(1), n - 1);
  }

  let isNegative = false;

  if (str[0] === "-") {
    isNegative = true;
    str = str.slice(1);
  } else if (str[0] === "+") {
    str = str.slice(1);
  }

  const num = helper(str, str.length);
  return isNegative ? -num : num;
}

// Test
console.log(recursiveAtoi("1234")); // 1234
console.log(recursiveAtoi("-456")); // -456
console.log(recursiveAtoi("+789")); // 789
console.log(recursiveAtoi("0")); // 0
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(n)`
  (We process each character once, and each call takes constant time.)
- **Space Complexity:** `O(n)`
  (Due to recursion stack.)

---

## 2. **Pow(x, n)**

Implement the function `pow(x, n)` that calculates `x` raised to the power `n` (i.e., `xⁿ`).
You must not use built-in exponentiation functions like `Math.pow`.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: (x = 2.0), (n = 10);
Output: 1024.0;
```

#### Test Case 2:

```js
Input: (x = 2.1), (n = 3);
Output: 9.261;
```

#### Test Case 3:

```js
Input: (x = 2.0), (n = -2);
Output: 0.25;
```

#### Test Case 4:

```js
Input: (x = 1.0), (n = 1000);
Output: 1.0;
```

---

### 💡 Approach 1: Brute Force (Recursive)

#### 🔎 Intuition

Multiply `x` repeatedly for `n` times. If `n` is negative, compute `1 / (x^|n|)`.

---

#### 🔄 Dry Run (Test Case 1)

`pow(2, 3)`
→ `2 * pow(2, 2)`
→ `2 * (2 * pow(2, 1))`
→ `2 * (2 * (2 * pow(2, 0)))`
→ `2 * 2 * 2 * 1` → ✅ `8`

---

#### 🧑‍💻 JavaScript Code (Recursive Brute Force)

```javascript
function pow(x, n) {
  if (n === 0) return 1;
  if (n < 0) return 1 / pow(x, -n);
  return x * pow(x, n - 1);
}
```

---

### ⏱️ Time & Space Complexity

- **Time:** `O(n)`
- **Space:** `O(n)` (recursion stack)

---

### 💡 Approach 2: Optimized (Fast Exponentiation using Divide & Conquer)

#### 🔎 Intuition

Use the identity:

- If `n` is even: `xⁿ = (x²)^(n/2)`
- If `n` is odd: `xⁿ = x * (x²)^((n-1)/2)`

This reduces the number of recursive calls to `log n`.

---

#### 🔄 Dry Run (Test Case: `x = 2`, `n = 10`)

- `pow(2, 10)`
  → `pow(2 * 2, 5)`
  → `2 * pow(4 * 4, 2)`
  → `pow(16 * 16, 1)`
  → `2 * 256` → `512`
  (Actually computed differently but fast using fewer calls)

---

#### 🧑‍💻 JavaScript Code (Optimized)

```javascript
function pow(x, n) {
  if (n === 0) return 1;

  if (n < 0) {
    x = 1 / x;
    n = -n;
  }

  if (n % 2 === 0) {
    const half = pow(x, n / 2);
    return half * half;
  } else {
    return x * pow(x, n - 1);
  }
}
```

✅ **Handles negative powers**
✅ **Optimized to O(log n)**

---

### ⏱️ Time & Space Complexity

- **Time:** `O(log n)`
- **Space:** `O(log n)` (recursion stack)

---

### ✅ Summary

| Approach          | Time     | Space    | Notes                            |
| ----------------- | -------- | -------- | -------------------------------- |
| Brute Force       | O(n)     | O(n)     | Simple, but slow for large `n`   |
| Fast Power (D\&C) | O(log n) | O(log n) | Optimal solution using recursion |

---

## 3. **Count Good Digit Strings**

Given an integer `n`, return the total number of **good digit strings** of length `n`.
A digit string is **good** if:

- At **even indices** (0-based), the digit is **even** → \[0, 2, 4, 6, 8] (5 options)
- At **odd indices**, the digit is **prime** → \[2, 3, 5, 7] (4 options)

Since the answer can be very large, return it **modulo 10⁹ + 7**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: n = 1
Output: 5
Explanation: Valid digits at index 0 (even): 0, 2, 4, 6, 8
```

#### Test Case 2:

```js
Input: n = 4
Output: 400
Explanation:
- Even indices: index 0 and 2 → 5 options each
- Odd indices: index 1 and 3 → 4 options each
- Total = 5^2 * 4^2 = 25 * 16 = 400
```

#### Test Case 3:

```js
Input: n = 2
Output: 20
Explanation: 5 options at even index 0, 4 options at odd index 1 → 5 * 4 = 20
```

#### Test Case 4:

```js
Input: n = 50;
Output: 564908303;
```

---

### 💡 Intuition

- Even positions → 5 choices
- Odd positions → 4 choices
- Let `evenCount = Math.ceil(n / 2)`
- Let `oddCount = Math.floor(n / 2)`
- Total good strings = `5^evenCount * 4^oddCount (mod 10^9 + 7)`

Use **modular exponentiation** to compute large powers efficiently.

---

### 🔄 Dry Run (Test Case 2: n = 4)

- Even indices: 0, 2 → 2 digits → `5^2 = 25`
- Odd indices: 1, 3 → 2 digits → `4^2 = 16`
- Total = `25 * 16 = 400`

---

### 🧑‍💻 JavaScript Code

```javascript
const MOD = 1_000_000_007;

// Fast exponentiation with modulo
function modPow(base, exp, mod) {
  let result = 1;
  base %= mod;

  while (exp > 0) {
    if (exp % 2 === 1) {
      result = (result * base) % mod;
    }
    base = (base * base) % mod;
    exp = Math.floor(exp / 2);
  }

  return result;
}

function countGoodNumbers(n) {
  const evenCount = Math.ceil(n / 2);
  const oddCount = Math.floor(n / 2);

  const evenWays = modPow(5, evenCount, MOD);
  const oddWays = modPow(4, oddCount, MOD);

  return (evenWays * oddWays) % MOD;
}

// Test
console.log(countGoodNumbers(1)); // 5
console.log(countGoodNumbers(4)); // 400
console.log(countGoodNumbers(50)); // 564908303
```

---

### ⏱️ Time & Space Complexity

- **Time:** `O(log n)`

  - Modular exponentiation is logarithmic in `n`.

- **Space:** `O(1)` (iterative implementation)

---

### ✅ Summary

| Aspect             | Value                             |
| ------------------ | --------------------------------- |
| Even indices count | `ceil(n / 2)` → 5 options         |
| Odd indices count  | `floor(n / 2)` → 4 options        |
| Total ways         | `5^even * 4^odd mod 10^9+7`       |
| Optimization       | Modular Exponentiation `O(log n)` |

---

# SubSequences

## 🧵 What is a **Subsequence**?

### 📘 **Definition:**

A **subsequence** is a new sequence that you create **by deleting some (or no) elements** from the original sequence **without changing the order** of the remaining elements.

> So, a subsequence keeps the order **same**, but doesn’t require the elements to be **next to each other**.

---

### ✅ Real-Life Example

Imagine you have the word:

```
"abcde"
```

Now, look at these possible subsequences:

| Subsequence  | How it was formed                              |
| ------------ | ---------------------------------------------- |
| `"ace"`      | Removed `b` and `d`, order remains `a → c → e` |
| `"abc"`      | No letters removed                             |
| `"ae"`       | Removed `b`, `c`, and `d`                      |
| `""` (empty) | Removed everything                             |

But these **are not** subsequences:

- `"eca"` ❌ (wrong order: `e` comes after `c` and `a`)
- `"acb"` ❌ (wrong order: `c` comes after `b` in the original)

---

### 🔗 Subsequence vs Substring

Let’s clear the confusion:

| Concept             | Subsequence                               | Substring                                |
| ------------------- | ----------------------------------------- | ---------------------------------------- |
| What is it?         | Remove any characters while keeping order | Take a **continuous** part of the string |
| Example             | `"ace"` from `"abcde"`                    | `"bcd"` from `"abcde"`                   |
| Must be continuous? | ❌ No                                     | ✅ Yes                                   |
| Order matters?      | ✅ Yes                                    | ✅ Yes                                   |

---

### 💡 Visual Example

Imagine this is your string:

```
a   b   c   d   e
|       |       |
↓       ↓       ↓
a       c       e   ← Valid Subsequence
```

You're just **picking** characters **without changing their order**.

---

### 📐 Total Number of Subsequences

For a string of length `n`, the total number of subsequences is:

```
2^n (including the empty string "")
```

Why? Because for every character, you have 2 choices:

1. Include it in the subsequence
2. Don’t include it

Example:
For `"abc"` → 2³ = 8 subsequences:

- `""`
- `"a"`
- `"b"`
- `"c"`
- `"ab"`
- `"ac"`
- `"bc"`
- `"abc"`

---

### ❓Common Questions Beginners Ask:

| Question                           | Answer |
| ---------------------------------- | ------ |
| Can a subsequence skip characters? | Yes ✅ |
| Can it change the order?           | No ❌  |
| Is every substring a subsequence?  | Yes ✅ |
| Is every subsequence a substring?  | No ❌  |

---

## 1. **Generate All Binary Strings of Length `n`**

Given an integer `n`, generate and print all binary strings of length `n`.
Each character in the string can only be `'0'` or `'1'`.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: n = 2;
Output: ["00", "01", "10", "11"];
```

#### Test Case 2:

```js
Input: n = 1;
Output: ["0", "1"];
```

#### Test Case 3:

```js
Input: n = 3;
Output: ["000", "001", "010", "011", "100", "101", "110", "111"];
```

#### Test Case 4:

```js
Input: n = 0;
Output: [""];
```

---

### 💡 Intuition

This is a **backtracking / recursion** problem:

- We start with an empty string.
- At each step, we **add '0' or '1'** to the string.
- We stop when the string length becomes `n`.

Think of it as generating all combinations of `n` bits.

---

### 🔄 Dry Run (Test Case 1: n = 2)

We build the string step-by-step:

1. Start: `""`
2. Add `'0'` → `"0"`

   - Add `'0'` → `"00"` ✅
   - Add `'1'` → `"01"` ✅

3. Add `'1'` → `"1"`

   - Add `'0'` → `"10"` ✅
   - Add `'1'` → `"11"` ✅

Result: `["00", "01", "10", "11"]`

---

### 🧑‍💻 JavaScript Code

```javascript
function generateBinaryStrings(n) {
  const result = [];

  function backtrack(current) {
    if (current.length === n) {
      result.push(current);
      return;
    }

    backtrack(current + "0");
    backtrack(current + "1");
  }

  backtrack("");
  return result;
}

// Test
console.log(generateBinaryStrings(2)); // ["00", "01", "10", "11"]
console.log(generateBinaryStrings(3)); // ["000", ..., "111"]
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(2^n)`

  - There are `2^n` possible binary strings.

- **Space Complexity:** `O(n)` (recursion stack), plus `O(2^n * n)` for storing results.

---

### ✅ Summary

| Concept         | Details                         |
| --------------- | ------------------------------- |
| Problem Type    | Backtracking / Recursion        |
| Total strings   | `2^n`                           |
| Example (n = 3) | 000, 001, ..., 111              |
| Efficient for   | Small to moderate values of `n` |

---

## 2. **Generate Parentheses**

Given `n` pairs of parentheses, generate **all combinations** of well-formed (valid) parentheses.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: n = 1;
Output: ["()"];
```

#### Test Case 2:

```js
Input: n = 2;
Output: ["(())", "()()"];
```

#### Test Case 3:

```js
Input: n = 3;
Output: ["((()))", "(()())", "(())()", "()(())", "()()()"];
```

#### Test Case 4:

```js
Input: n = 0;
Output: [""];
```

---

### 💡 Intuition

We use **backtracking** to generate all valid strings:

- At any time, we can add:

  - `'('` **if** the count of `'('` is less than `n`
  - `')'` **if** the count of `')'` is less than `'('` (to keep it valid)

- Stop when the string has `2 * n` characters

This way, we **only generate valid combinations** — no need to filter invalid ones later.

---

### 🔄 Dry Run (Test Case: n = 2)

Start: `""`, left = 2, right = 2

1. Add `'('`: `"("`, left = 1, right = 2
2. Add `'('`: `"(("`, left = 0, right = 2

   - Add `')'`: `"(()"`, left = 0, right = 1

     - Add `')'`: `"(())"` ✅

3. Backtrack: `"("`, left = 1, right = 2

   - Add `')'`: `"()"`, left = 1, right = 1

     - Add `'('`: `"()("`, left = 0, right = 1

       - Add `')'`: `"()()"` ✅

---

### 🧑‍💻 JavaScript Code

```javascript
function generateParentheses(n) {
  const result = [];

  function backtrack(current, open, close) {
    if (current.length === 2 * n) {
      result.push(current);
      return;
    }

    if (open < n) {
      backtrack(current + "(", open + 1, close);
    }

    if (close < open) {
      backtrack(current + ")", open, close + 1);
    }
  }

  backtrack("", 0, 0);
  return result;
}

// Test
console.log(generateParentheses(3));
// Output: ["((()))", "(()())", "(())()", "()(())", "()()()"]
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(2^n)` (actually closer to Catalan number: `C(n) = (1 / (n + 1)) * C(2n, n)`)
- **Space Complexity:** `O(2n)` recursion depth + output list

---

### ✅ Summary

| Concept             | Details                           |
| ------------------- | --------------------------------- |
| Problem Type        | Backtracking                      |
| Decision Choices    | Add `'('` or `')'` based on rules |
| Base Case           | When `current.length === 2 * n`   |
| Unique Output Count | Catalan Number `C(n)`             |

---

## 3. **Print All Subsequences / Power Set**

Given a string or an array, print **all possible subsequences** (also known as the **power set**).

- A **subsequence** can include **any subset of elements** in the same relative order.
- The **power set** is the set of **all subsets**, including the empty set and the original input itself.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: "abc";
Output: ["", "a", "b", "c", "ab", "ac", "bc", "abc"];
```

#### Test Case 2:

```js
Input: [1, 2];
Output: [[], [1], [2], [1, 2]];
```

#### Test Case 3:

```js
Input: "a";
Output: ["", "a"];
```

#### Test Case 4:

```js
Input: "";
Output: [""];
```

---

### 💡 Intuition

This is a **backtracking / recursion** problem.

At each step, we have **2 choices**:

- **Include** the current element in the subsequence.
- **Exclude** the current element.

We explore both possibilities recursively.

---

### 🔄 Dry Run (Test Case: "ab")

```
Start: ""
→ Include 'a' → "a"
  → Include 'b' → "ab" ✅
  → Exclude 'b' → "a" ✅
→ Exclude 'a' → ""
  → Include 'b' → "b" ✅
  → Exclude 'b' → "" ✅

Result: ["ab", "a", "b", ""]
```

---

### 🧑‍💻 JavaScript Code (For Strings)

```javascript
function getAllSubsequences(str) {
  const result = [];

  function backtrack(index, current) {
    if (index === str.length) {
      result.push(current);
      return;
    }

    // Include current character
    backtrack(index + 1, current + str[index]);

    // Exclude current character
    backtrack(index + 1, current);
  }

  backtrack(0, "");
  return result;
}

// Test
console.log(getAllSubsequences("abc"));
// Output: ["abc", "ab", "ac", "a", "bc", "b", "c", ""]
```

---

### 🧑‍💻 JavaScript Code (For Arrays)

```javascript
function getAllSubsets(arr) {
  const result = [];

  function backtrack(index, current) {
    if (index === arr.length) {
      result.push([...current]);
      return;
    }

    // Include arr[index]
    current.push(arr[index]);
    backtrack(index + 1, current);
    current.pop(); // Backtrack

    // Exclude arr[index]
    backtrack(index + 1, current);
  }

  backtrack(0, []);
  return result;
}

// Test
console.log(getAllSubsets([1, 2]));
// Output: [ [1, 2], [1], [2], [] ]
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(2^n)`
  Every element has 2 choices: include or exclude.
- **Space Complexity:** `O(n)` recursion depth + output storage.

---

### ✅ Summary

| Feature             | Description              |
| ------------------- | ------------------------ |
| Type                | Recursion / Backtracking |
| Choices per element | Include or exclude       |
| Total combinations  | `2^n` subsequences       |
| Includes empty set? | ✅ Yes                   |
| Also called         | Power Set                |

---

## 4. **Count All Subsequences with Sum K**

You are given an array of integers and a target sum `K`.
Your task is to **count the number of subsequences** whose sum is exactly `K`.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: arr = [1, 2, 1], K = 2
Output: 2
Explanation: [1, 1] and [2]
```

#### Test Case 2:

```js
Input: arr = [1, 2, 3], K = 3
Output: 2
Explanation: [1, 2] and [3]
```

#### Test Case 3:

```js
Input: arr = [1, 1, 1, 1], K = 2
Output: 6
Explanation: All pairs of [1, 1]
```

#### Test Case 4:

```js
Input: arr = [5, 6, 7], K = 20
Output: 0
Explanation: No subsequence has sum 20
```

---

### 💡 Intuition

This is a **recursion + backtracking + counting** problem.

At each index, you have **2 choices**:

- **Include** the current number in the sum
- **Exclude** it

We recursively try both options and count the number of times the sum becomes exactly `K`.

---

### 🔄 Dry Run (Test Case: \[1, 2, 1], K = 2)

All subsequences:

- \[1, 2, 1] → sum = 4 ❌
- \[1, 2] → sum = 3 ❌
- \[1, 1] → ✅
- \[2, 1] → sum = 3 ❌
- \[1] → ✅
- \[2] → ✅
- \[] → sum = 0 ❌

Valid: \[1, 1], \[2] → Count = 2 ✅

---

### 🧑‍💻 JavaScript Code (Recursive)

```javascript
function countSubsequencesWithSumK(arr, k) {
  function count(index, currentSum) {
    // Base case: reached end
    if (index === arr.length) {
      return currentSum === k ? 1 : 0;
    }

    // Include current element
    const include = count(index + 1, currentSum + arr[index]);

    // Exclude current element
    const exclude = count(index + 1, currentSum);

    return include + exclude;
  }

  return count(0, 0);
}

// Test
console.log(countSubsequencesWithSumK([1, 2, 1], 2)); // Output: 2
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(2^n)`
  Every element has 2 choices: include or exclude
- **Space Complexity:** `O(n)` for recursion stack

---

## 5. **Check if There Exists a Subsequence with Sum K**

You're given an array of integers and a target sum `K`.
Your task is to **check if there is at least one subsequence** whose sum is exactly `K`.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: arr = [1, 2, 3], K = 5
Output: true
Explanation: Subsequence [2, 3] has sum 5
```

#### Test Case 2:

```js
Input: (arr = [1, 2, 3]), (K = 6);
Output: true;
Explanation: Subsequence[(1, 2, 3)];
```

#### Test Case 3:

```js
Input: (arr = [1, 1, 1, 1]), (K = 3);
Output: true;
```

#### Test Case 4:

```js
Input: arr = [1, 2, 3], K = 10
Output: false
Explanation: No subsequence has sum 10
```

---

### 💡 Intuition

This is a **classic recursion / backtracking** problem, similar to the **Subset Sum** problem.

At every index, you have two choices:

- **Include** the current element in the sum
- **Exclude** the current element

We explore both and return `true` if any path leads to sum = `K`.

---

### 🔄 Dry Run (Test Case: \[1, 2, 3], K = 5)

1. Include 1 → sum = 1

   - Include 2 → sum = 3

     - Include 3 → sum = 6 ❌
     - Exclude 3 → sum = 3 ❌

   - Exclude 2 → sum = 1

     - Include 3 → sum = 4 ❌
     - Exclude 3 → sum = 1 ❌

2. Exclude 1 → sum = 0

   - Include 2 → sum = 2

     - Include 3 → ✅ sum = 5 ✅

---

### 🧑‍💻 JavaScript Code

```javascript
function isSubsetSum(arr, k) {
  function backtrack(index, currentSum) {
    // Base case: sum reached
    if (currentSum === k) return true;

    // Base case: end of array
    if (index === arr.length) return false;

    // Include current element
    const include = backtrack(index + 1, currentSum + arr[index]);

    // Exclude current element
    const exclude = backtrack(index + 1, currentSum);

    return include || exclude;
  }

  return backtrack(0, 0);
}

// Test
console.log(isSubsetSum([1, 2, 3], 5)); // true
console.log(isSubsetSum([1, 2, 3], 10)); // false
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(2^n)` (brute-force for all subsequences)
- **Space Complexity:** `O(n)` (recursion stack)

---

## 6. **Combination Sum**

You're given an array of **distinct** integers `candidates` and a target integer `target`.
Your task is to return **all unique combinations** of `candidates` where the **chosen numbers sum up to `target`**.

- You **can use the same number multiple times**.
- Return the combinations in **any order**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: (candidates = [2, 3, 6, 7]), (target = 7);
Output: [[2, 2, 3], [7]];
```

#### Test Case 2:

```js
Input: (candidates = [2, 3, 5]), (target = 8);
Output: [
  [2, 2, 2, 2],
  [2, 3, 3],
  [3, 5],
];
```

#### Test Case 3:

```js
Input: (candidates = [2]), (target = 1);
Output: [];
```

#### Test Case 4:

```js
Input: (candidates = [1]), (target = 1);
Output: [[1]];
```

---

### 💡 Intuition

This is a **backtracking** problem.
We try every number at each step and **recurse** with:

- Reduced `target`
- Updated path (current combination)
- Same index (because we can reuse the same element)

We stop when:

- `target == 0` → ✅ valid combination
- `target < 0` → ❌ invalid path

---

### 🔄 Dry Run (Test Case 1: \[2, 3, 6, 7], target = 7)

Start: \[], sum = 0

- Pick 2 → \[2], sum = 2

  - Pick 2 again → \[2, 2], sum = 4

    - Pick 2 again → \[2, 2, 2], sum = 6

      - Pick 2 → sum = 8 ❌
      - Pick 3 → sum = 9 ❌

    - Pick 3 → \[2, 2, 3] → ✅ sum = 7 ✅

- Pick 7 → \[7] → ✅ ✅

---

### 🧑‍💻 JavaScript Code

```javascript
function combinationSum(candidates, target) {
  const result = [];

  function backtrack(start, path, remaining) {
    if (remaining === 0) {
      result.push([...path]);
      return;
    }

    if (remaining < 0) return;

    for (let i = start; i < candidates.length; i++) {
      path.push(candidates[i]);
      backtrack(i, path, remaining - candidates[i]); // reuse allowed
      path.pop(); // backtrack
    }
  }

  backtrack(0, [], target);
  return result;
}

// Test
console.log(combinationSum([2, 3, 6, 7], 7));
// Output: [[2, 2, 3], [7]]
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(2^t)` where `t = target` (explores all combinations)
- **Space Complexity:** `O(target)` for recursion stack

---

## 7. **Combination Sum II**

You're given a list of **integers that may contain duplicates** and a `target`.
Return **all unique combinations** where the candidate numbers **sum to `target`**.

- Each number may **only be used once** in each combination.
- The **output must not contain duplicate combinations**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: (candidates = [10, 1, 2, 7, 6, 1, 5]), (target = 8);
Output: [
  [1, 1, 6],
  [1, 2, 5],
  [1, 7],
  [2, 6],
];
```

#### Test Case 2:

```js
Input: (candidates = [2, 5, 2, 1, 2]), (target = 5);
Output: [[1, 2, 2], [5]];
```

#### Test Case 3:

```js
Input: (candidates = [1, 1, 1, 1, 1]), (target = 3);
Output: [[1, 1, 1]];
```

#### Test Case 4:

```js
Input: (candidates = [3, 1, 3, 5, 1, 1]), (target = 8);
Output: [
  [1, 1, 1, 5],
  [1, 1, 3, 3],
  [3, 5],
];
```

---

### 💡 Intuition

The **key difference** from Combination Sum I is:

| Feature              | Combination Sum I | Combination Sum II                 |
| -------------------- | ----------------- | ---------------------------------- |
| Duplicates in input? | ❌ No             | ✅ Yes                             |
| Reuse of element?    | ✅ Yes            | ❌ No (only once)                  |
| Need to sort input?  | Optional          | ✅ Yes (to skip duplicates easily) |

So we must:

- Sort the input array
- Skip duplicate values at the same recursion level to avoid duplicate combinations
- Only move forward in the array (`i + 1`), not `i` (since we can't reuse elements)

---

### 🔄 Dry Run (Test Case: \[2, 5, 2, 1, 2], target = 5)

After sorting → `[1, 2, 2, 2, 5]`

Valid paths:

- `[1, 2, 2]`
- `[5]`

We skip:

- Picking same `2` again from the same recursion level

---

### 🧑‍💻 JavaScript Code

```javascript
function combinationSum2(candidates, target) {
  const result = [];
  candidates.sort((a, b) => a - b); // Sort to handle duplicates

  function backtrack(start, path, remaining) {
    if (remaining === 0) {
      result.push([...path]);
      return;
    }

    for (let i = start; i < candidates.length; i++) {
      // Skip duplicates at the same recursive level
      if (i > start && candidates[i] === candidates[i - 1]) continue;

      if (candidates[i] > remaining) break;

      path.push(candidates[i]);
      backtrack(i + 1, path, remaining - candidates[i]); // i+1 → no reuse
      path.pop(); // backtrack
    }
  }

  backtrack(0, [], target);
  return result;
}

// Test
console.log(combinationSum2([10, 1, 2, 7, 6, 1, 5], 8));
// Output: [[1,1,6],[1,2,5],[1,7],[2,6]]
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(2^n)` worst-case (but pruning improves it)
- **Space Complexity:** `O(n)` recursion depth + result list

---

### ✅ Summary

| Feature                      | Value                             |
| ---------------------------- | --------------------------------- |
| Input may contain duplicates | ✅ Yes                            |
| Element reuse allowed?       | ❌ No (only once per combination) |
| Sorting needed?              | ✅ Yes (to skip duplicates)       |
| Output uniqueness?           | ✅ Required                       |

---

### 💬 Pro Tip:

- Always sort the array first when working with **duplicates**.
- In recursion: to **avoid duplicate results**, **skip same elements** when `i > start` and `arr[i] === arr[i - 1]`.

---

Would you like to go through:

- **Combination Sum III** (choose exactly `k` numbers that sum to `n`), or
- **Compare all 3 versions** in a single table?

Let me know!

## 8. **Subset Sum I**

You're given an array of integers. Your task is to **find all possible subset sums** (i.e., the sum of each possible subset of the array elements).

> Return the **subset sums in increasing order**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: arr = [1, 2]
Output: [0, 1, 2, 3]
Explanation:
Subsets → [], [1], [2], [1,2] → Sums → 0, 1, 2, 3
```

#### Test Case 2:

```js
Input: arr = [5];
Output: [0, 5];
```

#### Test Case 3:

```js
Input: arr = [1, 2, 3];
Output: [0, 1, 2, 3, 3, 4, 5, 6];
```

#### Test Case 4:

```js
Input: arr = [];
Output: [0];
```

---

### 💡 Intuition

This is a **classic backtracking** problem where:

- Each element has two choices: **Include** it in the sum or **exclude** it.
- This forms `2^n` total subset combinations.

We collect each **sum of the current path** during recursion.

---

### 🔄 Dry Run (Test Case: \[1, 2])

Subset choices:

- \[] → 0
- \[1] → 1
- \[2] → 2
- \[1, 2] → 3

Result (sorted): `[0, 1, 2, 3]`

---

### 🧑‍💻 JavaScript Code

```javascript
function subsetSums(arr) {
  const result = [];

  function backtrack(index, currentSum) {
    if (index === arr.length) {
      result.push(currentSum);
      return;
    }

    // Include current element
    backtrack(index + 1, currentSum + arr[index]);

    // Exclude current element
    backtrack(index + 1, currentSum);
  }

  backtrack(0, 0);
  return result.sort((a, b) => a - b);
}

// Test
console.log(subsetSums([1, 2])); // Output: [0, 1, 2, 3]
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(2^n log(2^n))`

  - `2^n` subset sums + sorting

- **Space Complexity:** `O(2^n)` for storing all subset sums

---

## 9. **Subset Sum II**

_(a.k.a. Generate all unique subsets when input has duplicates)_

You’re given an array of integers that **may contain duplicates**.
Your task is to return **all possible unique subsets** (the power set).

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: arr = [1, 2, 2];
Output: [[], [1], [1, 2], [1, 2, 2], [2], [2, 2]];
```

#### Test Case 2:

```js
Input: arr = [1, 2, 2, 2];
Output: [[], [1], [1, 2], [1, 2, 2], [1, 2, 2, 2], [2], [2, 2], [2, 2, 2]];
```

#### Test Case 3:

```js
Input: arr = [4, 4, 4, 1, 4];
Output: [
  [],
  [1],
  [1, 4],
  [1, 4, 4],
  [1, 4, 4, 4],
  [1, 4, 4, 4, 4],
  [4],
  [4, 4],
  [4, 4, 4],
  [4, 4, 4, 4],
];
```

---

### 💡 Intuition

Same **include/exclude** strategy as Subset Sum I, but:

✅ We **must skip duplicates** to avoid generating duplicate subsets.

✅ To do this, we:

- **Sort the array**
- **Skip the element if it's the same as the previous one at the same recursion level**

---

### 🔄 Dry Run (Input: \[1, 2, 2])

Sorted: `[1, 2, 2]`

- Start: `[]`

  - Add 1 → `[1]`

    - Add 2 → `[1, 2]`

      - Add 2 → `[1, 2, 2]`

    - Skip 2 at index 2 because we already used it at index 1

  - Add 2 → `[2]`

    - Add 2 → `[2, 2]`

- Skip duplicate 2s at index 2 when not part of new path

---

### 🧑‍💻 JavaScript Code

```javascript
function subsetsWithDup(nums) {
  const result = [];
  nums.sort((a, b) => a - b); // Sort to bring duplicates together

  function backtrack(index, path) {
    result.push([...path]);

    for (let i = index; i < nums.length; i++) {
      // Skip duplicates
      if (i > index && nums[i] === nums[i - 1]) continue;

      path.push(nums[i]);
      backtrack(i + 1, path);
      path.pop(); // backtrack
    }
  }

  backtrack(0, []);
  return result;
}

// Test
console.log(subsetsWithDup([1, 2, 2]));
// Output: [[], [1], [1, 2], [1, 2, 2], [2], [2, 2]]
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(2^n)` — generates all unique subsets
- **Space Complexity:** `O(n)` recursion + `O(2^n)` result list

---

### 🧠 Tip for Interviews:

Always sort the input if you need to **remove duplicate subsets or combinations**.
Use the logic:

```js
if (i > index && nums[i] === nums[i - 1]) continue;
```

→ It ensures you don’t choose the same element **again at the same tree level**.

---

## 10. **Combination Sum III**

You are given two integers `k` and `n`.

Your task is to return **all possible combinations** of `k` **distinct numbers** (from 1 to 9) that **add up to `n`**.

- Each number is **used only once**.
- You must only use numbers from **1 to 9**.
- The combinations must be **unique**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: (k = 3), (n = 7);
Output: [[1, 2, 4]];
```

#### Test Case 2:

```js
Input: (k = 3), (n = 9);
Output: [
  [1, 2, 6],
  [1, 3, 5],
  [2, 3, 4],
];
```

#### Test Case 3:

```js
Input: k = 4, n = 1
Output: []
Explanation: No combination of 4 distinct numbers from 1–9 adds to 1.
```

#### Test Case 4:

```js
Input: (k = 3), (n = 2);
Output: [];
```

---

### 💡 Intuition

This is a **classic backtracking problem** with two key constraints:

- You can only use **numbers from 1 to 9**
- You must choose **exactly `k` numbers** whose sum is `n`

So, at each step:

- Choose a number `i` from `start` to 9
- Include it if:

  - It doesn't exceed remaining sum
  - You haven't picked `k` numbers yet

---

### 🔄 Dry Run (k = 3, n = 9)

Start: \[], sum = 0

Try:

- \[1] → \[1,2] → \[1,2,6] ✅ sum = 9
- \[1,3,5] ✅
- \[2,3,4] ✅
  → All with exactly 3 elements

---

### 🧑‍💻 JavaScript Code

```javascript
function combinationSum3(k, n) {
  const result = [];

  function backtrack(start, path, remaining) {
    // Base case: path has k numbers
    if (path.length === k) {
      if (remaining === 0) {
        result.push([...path]);
      }
      return;
    }

    for (let i = start; i <= 9; i++) {
      if (i > remaining) break; // Prune if number exceeds target

      path.push(i);
      backtrack(i + 1, path, remaining - i); // Use each number only once
      path.pop(); // backtrack
    }
  }

  backtrack(1, [], n);
  return result;
}

// Test
console.log(combinationSum3(3, 9));
// Output: [[1,2,6],[1,3,5],[2,3,4]]
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(2^9)` → Because we choose from 1–9 with backtracking
- **Space Complexity:** `O(k)` (depth of recursion tree) + result list

---

### ✅ Summary

| Feature               | Value                                         |
| --------------------- | --------------------------------------------- |
| Input size            | Fixed (1–9)                                   |
| Use number once?      | ✅ Yes                                        |
| Total numbers to pick | Exactly `k`                                   |
| Target sum            | Must be exactly `n`                           |
| Output uniqueness     | ✅ Required (each combination must be unique) |

---

## 11. **Letter Combinations of a Phone Number**

You're given a string `digits` consisting of digits from **2 to 9**, mapping to letters like on a phone keypad.

Return **all possible letter combinations** that the number could represent.

> If `digits` is empty, return an empty array.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: digits = "23";
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"];
```

#### Test Case 2:

```js
Input: digits = "";
Output: [];
```

#### Test Case 3:

```js
Input: digits = "2";
Output: ["a", "b", "c"];
```

---

### 🔢 Keypad Mapping

```
2 → abc
3 → def
4 → ghi
5 → jkl
6 → mno
7 → pqrs
8 → tuv
9 → wxyz
```

---

### 💡 Intuition

At each digit:

- You have multiple choices (letters).
- Choose one letter and move to the next digit.
- Use **backtracking** to explore all combinations.

---

### 🔄 Dry Run (digits = "23")

- digit `2` → \['a','b','c']
- digit `3` → \['d','e','f']

Combinations:

- a + d → "ad"
- a + e → "ae"
- ...
- c + f → "cf"

Result:
`["ad","ae","af","bd","be","bf","cd","ce","cf"]`

---

### 🧑‍💻 JavaScript Code

```javascript
function letterCombinations(digits) {
  if (digits.length === 0) return [];

  const result = [];
  const map = {
    2: "abc",
    3: "def",
    4: "ghi",
    5: "jkl",
    6: "mno",
    7: "pqrs",
    8: "tuv",
    9: "wxyz",
  };

  function backtrack(index, path) {
    if (index === digits.length) {
      result.push(path);
      return;
    }

    const letters = map[digits[index]];
    for (let letter of letters) {
      backtrack(index + 1, path + letter);
    }
  }

  backtrack(0, "");
  return result;
}

// Test
console.log(letterCombinations("23"));
// Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(4^n)`
  Each digit can map up to 4 letters (e.g., 7 or 9).
- **Space Complexity:** `O(n)` for recursion stack + result list

---

# Hard ( Trying out all combos)

## 1. **Palindrome Partitioning**

You're given a string `s`, and your task is to **partition the string** such that every substring in the partition is a **palindrome**.

Return **all possible palindrome partitions** of `s`.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: "aab";
Output: [
  ["a", "a", "b"],
  ["aa", "b"],
];
```

#### Test Case 2:

```js
Input: "a";
Output: [["a"]];
```

#### Test Case 3:

```js
Input: "racecar";
Output: [
  ["r", "a", "c", "e", "c", "a", "r"],
  ["r", "a", "cec", "a", "r"],
  ["r", "aceca", "r"],
  ["racecar"],
];
```

---

### 💡 Intuition

You explore **all possible partitions** of the string using **backtracking**, and at each step, **only continue** if the current substring is a **palindrome**.

- Start from index 0 and explore all palindromic prefixes
- If a prefix is a palindrome, **recurse** on the remaining string
- Once the entire string is consumed, add the current partition to the result

---

### 🔄 Dry Run (s = "aab")

Start: index = 0, path = \[]

- "a" is a palindrome → recurse on "ab"

  - "a" is a palindrome → recurse on "b"

    - "b" is a palindrome → ✅ \["a", "a", "b"]

- Backtrack
- "aa" is a palindrome → recurse on "b" → ✅ \["aa", "b"]

---

### 🧑‍💻 JavaScript Code

```javascript
function partition(s) {
  const result = [];

  function isPalindrome(str, left, right) {
    while (left < right) {
      if (str[left] !== str[right]) return false;
      left++;
      right--;
    }
    return true;
  }

  function backtrack(start, path) {
    if (start === s.length) {
      result.push([...path]);
      return;
    }

    for (let end = start; end < s.length; end++) {
      if (isPalindrome(s, start, end)) {
        path.push(s.substring(start, end + 1));
        backtrack(end + 1, path);
        path.pop();
      }
    }
  }

  backtrack(0, []);
  return result;
}

// Test
console.log(partition("aab"));
// Output: [["a","a","b"],["aa","b"]]
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(2^n)` (explores all possible partitions)
- **Space Complexity:** `O(n)` recursion depth + result list

---

## 2. **Word Search**

You are given a 2D board of characters and a word.
Return `true` if the word **exists in the grid**, otherwise return `false`.

- The word can be constructed from **letters of sequentially adjacent cells**, where "adjacent" cells are horizontally or vertically neighboring.
- **You may not reuse the same cell** more than once in a single path.

---

### 🧪 Test Cases

#### Test Case 1:

```js
board = [
  ["A", "B", "C", "E"],
  ["S", "F", "C", "S"],
  ["A", "D", "E", "E"],
];
word = "ABCCED";
Output: true;
```

#### Test Case 2:

```js
word = "SEE";
Output: true;
```

#### Test Case 3:

```js
word = "ABCB";
Output: false;
```

---

### 💡 Intuition

Use **DFS backtracking**:

- Try to match the first character of the word at every cell.
- If it matches, explore its 4 neighbors (up, down, left, right) recursively.
- **Mark the cell as visited** temporarily (like `'#'`) to avoid reuse.
- Backtrack after the recursive call by **restoring** the cell's original value.

---

### 🔄 Dry Run

Let's say word = `"ABCCED"`

Starting from board\[0]\[0] = 'A'
→ match → go to right → 'B'
→ match → go to right → 'C'
→ match → go down → 'C'
→ match → go left → 'E'
→ match → go up → 'D'
→ match ✅

---

### 🧑‍💻 JavaScript Code

```javascript
function exist(board, word) {
  const rows = board.length;
  const cols = board[0].length;

  function dfs(r, c, i) {
    if (i === word.length) return true;

    // Out of bounds or mismatch
    if (r < 0 || c < 0 || r >= rows || c >= cols || board[r][c] !== word[i])
      return false;

    const temp = board[r][c];
    board[r][c] = "#"; // Mark as visited

    // Explore 4 directions
    const found =
      dfs(r + 1, c, i + 1) ||
      dfs(r - 1, c, i + 1) ||
      dfs(r, c + 1, i + 1) ||
      dfs(r, c - 1, i + 1);

    board[r][c] = temp; // Restore
    return found;
  }

  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      if (dfs(r, c, 0)) return true;
    }
  }

  return false;
}

// Test
console.log(
  exist(
    [
      ["A", "B", "C", "E"],
      ["S", "F", "C", "S"],
      ["A", "D", "E", "E"],
    ],
    "ABCCED"
  )
); // Output: true
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(N * 3^L)`
  Where `N = total cells`, and `L = length of word`

  - 3 choices after the first (excluding the direction we came from)

- **Space Complexity:** `O(L)` (recursion stack)

---

## 3. **N-Queens Problem**

You're given an integer `n`.
Place `n` queens on an `n x n` chessboard such that **no two queens attack each other**.

Return **all distinct solutions** to the problem.

- Each solution contains a board configuration (as an array of strings).
- A queen can attack horizontally, vertically, and diagonally.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: n = 4;
Output: [
  [".Q..", "...Q", "Q...", "..Q."],

  ["..Q.", "Q...", "...Q", ".Q.."],
];
```

#### Test Case 2:

```js
Input: n = 1;
Output: [["Q"]];
```

#### Test Case 3:

```js
Input: n = 2;
Output: []; // No valid way to place 2 queens
```

---

### 💡 Intuition

Use **backtracking row-by-row**:

- Try placing a queen in each column of a row.
- Before placing, check if it's safe (not under attack).
- If it's safe, place it and recurse to the next row.
- If a full board is formed, add the board to the result.
- Backtrack and try other positions.

✅ To optimize safety checks, use 3 helper sets:

- `cols` → columns under attack
- `diag1` → major diagonal (`row - col`)
- `diag2` → minor diagonal (`row + col`)

---

### 🔄 Dry Run (n = 4)

Start with row 0 → try columns 0 to 3

- If queen placed in col = 1, recurse on row 1

  - Try valid column, and so on
    → When row == n, push board config
    → Backtrack and try other combinations

---

### 🧑‍💻 JavaScript Code

```javascript
function solveNQueens(n) {
  const result = [];
  const board = Array(n)
    .fill()
    .map(() => Array(n).fill("."));
  const cols = new Set();
  const diag1 = new Set(); // row - col
  const diag2 = new Set(); // row + col

  function backtrack(row) {
    if (row === n) {
      const snapshot = board.map((row) => row.join(""));
      result.push(snapshot);
      return;
    }

    for (let col = 0; col < n; col++) {
      if (cols.has(col) || diag1.has(row - col) || diag2.has(row + col))
        continue;

      board[row][col] = "Q";
      cols.add(col);
      diag1.add(row - col);
      diag2.add(row + col);

      backtrack(row + 1);

      board[row][col] = ".";
      cols.delete(col);
      diag1.delete(row - col);
      diag2.delete(row + col);
    }
  }

  backtrack(0);
  return result;
}

// Test
console.log(solveNQueens(4));
// Output: [[".Q..","...Q","Q...","..Q."], ["..Q.","Q...","...Q",".Q.."]]
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(N!)`
  Since we try each column per row with pruning
- **Space Complexity:**

  - `O(N^2)` for storing board configurations
  - `O(N)` for recursion + sets

---

## 4. **Rat in a Maze**

You're given an `N x N` grid (or maze) filled with `1`s (open cell) and `0`s (blocked cell).
A **rat** starts at `(0, 0)` and must reach `(N - 1, N - 1)` by moving only through **open cells**.

The rat can move in **4 directions**:

- Down (`D`)
- Left (`L`)
- Right (`R`)
- Up (`U`)

Return **all possible paths** from source to destination as strings of directions.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: maze = [
  [1, 0, 0, 0],
  [1, 1, 0, 1],
  [0, 1, 0, 0],
  [1, 1, 1, 1],
];

Output: ["DDRDRR", "DRDDRR"];
```

#### Test Case 2:

```js
Input: maze = [
  [1, 0],
  [0, 1],
];

Output: []; // No path available
```

---

### 💡 Intuition

We use **backtracking** to explore all possible paths from `(0, 0)` to `(N-1, N-1)`:

At each cell:

- If it's safe and within bounds, mark it as visited
- Move in all 4 directions (D, L, R, U)
- On reaching `(N-1, N-1)`, add the current path
- Backtrack (unmark cell) to explore other paths

---

### 🔄 Dry Run (on 4x4 maze above)

Start at (0,0) → D → D → R → D → R → R → Reached
→ path = `"DDRDRR"`
Backtrack and try alternative paths.

---

### 🧑‍💻 JavaScript Code

```javascript
function findPaths(maze, n) {
  const result = [];
  const visited = Array.from({ length: n }, () => Array(n).fill(false));

  const directions = [
    [1, 0, "D"], // Down
    [0, -1, "L"], // Left
    [0, 1, "R"], // Right
    [-1, 0, "U"], // Up
  ];

  function isSafe(x, y) {
    return (
      x >= 0 && x < n && y >= 0 && y < n && maze[x][y] === 1 && !visited[x][y]
    );
  }

  function backtrack(x, y, path) {
    if (x === n - 1 && y === n - 1) {
      result.push(path);
      return;
    }

    for (let [dx, dy, move] of directions) {
      const newX = x + dx;
      const newY = y + dy;

      if (isSafe(newX, newY)) {
        visited[x][y] = true;
        backtrack(newX, newY, path + move);
        visited[x][y] = false; // backtrack
      }
    }
  }

  if (maze[0][0] === 1) {
    backtrack(0, 0, "");
  }

  return result;
}

// Test
const maze = [
  [1, 0, 0, 0],
  [1, 1, 0, 1],
  [0, 1, 0, 0],
  [1, 1, 1, 1],
];

console.log(findPaths(maze, 4));
// Output: ["DDRDRR", "DRDDRR"]
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(4^(N^2))` worst case (4 choices per cell)
- **Space Complexity:**

  - `O(N^2)` for visited matrix
  - `O(path length)` recursion stack

---

## 5. **Word Break**

You're given a string `s` and a dictionary `wordDict` of strings.
Return `true` if `s` **can be segmented** into a **space-separated** sequence of one or more **dictionary words**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: s = "leetcode";
wordDict = ["leet", "code"];

Output: true;
```

#### Test Case 2:

```js
Input: s = "applepenapple";
wordDict = ["apple", "pen"];

Output: true;
```

#### Test Case 3:

```js
Input: s = "catsandog";
wordDict = ["cats", "dog", "sand", "and", "cat"];

Output: false;
```

---

### 💡 Intuition

This is a **DP on substring** or **recursive partitioning** problem.

At each index `i`:

- Try all substrings from `i` to `j`
- If `s.slice(i, j)` is in dictionary AND the rest of the string can also be broken → ✅

To **optimize**, we use **memoization** to avoid recomputing from the same index.

---

### 🔄 Dry Run

Let’s say:
`s = "leetcode", wordDict = ["leet", "code"]`

- Try "l", not in dict ❌
- Try "le", "lee", "leet" ✅

  - Now try from index 4 → "code" ✅ → done

---

### 🧑‍💻 JavaScript Code (with Memoization)

```javascript
function wordBreak(s, wordDict) {
  const wordSet = new Set(wordDict);
  const memo = new Map();

  function canBreak(start) {
    if (start === s.length) return true;
    if (memo.has(start)) return memo.get(start);

    for (let end = start + 1; end <= s.length; end++) {
      const word = s.slice(start, end);
      if (wordSet.has(word) && canBreak(end)) {
        memo.set(start, true);
        return true;
      }
    }

    memo.set(start, false);
    return false;
  }

  return canBreak(0);
}

// Test
console.log(wordBreak("leetcode", ["leet", "code"])); // true
console.log(wordBreak("catsandog", ["cats", "dog", "sand", "and", "cat"])); // false
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(n^2)`

  - We check all substrings and use memoization

- **Space Complexity:** `O(n)` recursion + `O(n)` memo

---

## 6. **M-Coloring Problem**

You're given:

- An undirected graph with `n` nodes represented by an **adjacency matrix** `graph[][]`
- A number `m` (maximum number of colors)

Your task is to return **true** if the graph can be **colored using at most `m` colors**, such that **no two adjacent vertices share the same color**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: graph = [
  [0, 1, 1, 1],
  [1, 0, 1, 0],
  [1, 1, 0, 1],
  [1, 0, 1, 0],
];
m = 3;
Output: true;
```

#### Test Case 2:

```js
Input: graph = [
  [0, 1, 1, 1],
  [1, 0, 1, 0],
  [1, 1, 0, 1],
  [1, 0, 1, 0],
];
m = 2;
Output: false;
```

---

### 💡 Intuition

This is a **graph coloring** backtracking problem.

For each node `i`, try assigning colors from `1` to `m`:

- Before assigning a color, check if it’s **safe** (i.e., no adjacent node has the same color)
- If it’s safe, proceed to color the next node
- If all nodes are colored without conflict → return `true`

---

### 🔄 Dry Run (n = 4, m = 3)

Try assigning:

- Node 0 → color 1
- Node 1 → color 2
- Node 2 → color 3
- Node 3 → color 2
  → All adjacent nodes have different colors → ✅

---

### 🧑‍💻 JavaScript Code

```javascript
function graphColoring(graph, m) {
  const n = graph.length;
  const colors = Array(n).fill(0);

  function isSafe(node, color) {
    for (let i = 0; i < n; i++) {
      if (graph[node][i] === 1 && colors[i] === color) {
        return false;
      }
    }
    return true;
  }

  function solve(node) {
    if (node === n) return true;

    for (let c = 1; c <= m; c++) {
      if (isSafe(node, c)) {
        colors[node] = c;
        if (solve(node + 1)) return true;
        colors[node] = 0; // backtrack
      }
    }

    return false;
  }

  return solve(0);
}

// Test
const graph = [
  [0, 1, 1, 1],
  [1, 0, 1, 0],
  [1, 1, 0, 1],
  [1, 0, 1, 0],
];
console.log(graphColoring(graph, 3)); // true
console.log(graphColoring(graph, 2)); // false
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(m^n)`
  For each node, we try `m` colors
- **Space Complexity:** `O(n)` for color assignment

---

## 7. **Sudoku Solver**

You're given a `9 x 9` partially filled Sudoku board.
Fill the board so that:

- Each **row**, **column**, and **3x3 sub-box** contains digits **1–9** exactly once.
- Empty cells are denoted by `"."`.

---

### 🧪 Test Case

#### Input:

```js
board = [
  ["5", "3", ".", ".", "7", ".", ".", ".", "."],
  ["6", ".", ".", "1", "9", "5", ".", ".", "."],
  [".", "9", "8", ".", ".", ".", ".", "6", "."],
  ["8", ".", ".", ".", "6", ".", ".", ".", "3"],
  ["4", ".", ".", "8", ".", "3", ".", ".", "1"],
  ["7", ".", ".", ".", "2", ".", ".", ".", "6"],
  [".", "6", ".", ".", ".", ".", "2", "8", "."],
  [".", ".", ".", "4", "1", "9", ".", ".", "5"],
  [".", ".", ".", ".", "8", ".", ".", "7", "9"],
];
```

#### Output:

(Completed board with all rules satisfied)

---

### 💡 Intuition

Use **backtracking**:

- For each cell:

  - If it's empty:

    - Try placing digits from `'1'` to `'9'`
    - If placing a digit is **safe** (no duplicates in row, col, box), recurse
    - If solved → return true
    - If not → backtrack (reset to '.')

- Once all cells are filled, return the board

---

### 🔄 Dry Run (small 3x3 portion)

- Empty cell at (0,2)
- Try "1" → not in row/col/box → ✅
- Recurse for next empty cell
- If stuck → backtrack and try next number

---

### 🧑‍💻 JavaScript Code

```javascript
function solveSudoku(board) {
  function isValid(r, c, ch) {
    for (let i = 0; i < 9; i++) {
      // Check row, col, and 3x3 box
      if (
        board[r][i] === ch ||
        board[i][c] === ch ||
        board[3 * Math.floor(r / 3) + Math.floor(i / 3)][
          3 * Math.floor(c / 3) + (i % 3)
        ] === ch
      ) {
        return false;
      }
    }
    return true;
  }

  function solve() {
    for (let r = 0; r < 9; r++) {
      for (let c = 0; c < 9; c++) {
        if (board[r][c] === ".") {
          for (let ch = 1; ch <= 9; ch++) {
            const digit = ch.toString();
            if (isValid(r, c, digit)) {
              board[r][c] = digit;

              if (solve()) return true;

              board[r][c] = "."; // backtrack
            }
          }
          return false; // no digit fits here
        }
      }
    }
    return true; // fully filled
  }

  solve();
}

// Usage
let board = [
  ["5", "3", ".", ".", "7", ".", ".", ".", "."],
  ["6", ".", ".", "1", "9", "5", ".", ".", "."],
  [".", "9", "8", ".", ".", ".", ".", "6", "."],
  ["8", ".", ".", ".", "6", ".", ".", ".", "3"],
  ["4", ".", ".", "8", ".", "3", ".", ".", "1"],
  ["7", ".", ".", ".", "2", ".", ".", ".", "6"],
  [".", "6", ".", ".", ".", ".", "2", "8", "."],
  [".", ".", ".", "4", "1", "9", ".", ".", "5"],
  [".", ".", ".", ".", "8", ".", ".", "7", "9"],
];

solveSudoku(board);
console.log(board); // Modified in-place
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** \~ `O(9^(n))` → n = number of empty cells
- **Space Complexity:** `O(1)` (board modified in-place)

---

### ✅ Summary

| Feature      | Value                           |
| ------------ | ------------------------------- |
| Problem Type | Backtracking + Constraint Check |
| Grid Size    | Fixed 9x9                       |
| Empty Cell   | `'.'`                           |
| Valid Move   | Unique in row, col, 3x3 box     |
| Return Type  | In-place filled grid            |

---

### 🧠 Tips for Interview

- Sudoku solving = combination of **search** and **pruning**
- You can optimize using:

  - Precomputed sets for rows/cols/boxes
  - Constraint propagation

---

## 8. **Expression Add Operators**

You're given a string `num` containing only digits and an integer `target`.
Add the binary operators `'+'`, `'-'`, or `'*'` between the digits in `num` so that the expression evaluates to the **target value**.

Return **all valid expressions** that evaluate to `target`.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: (num = "123"), (target = 6);
Output: ["1+2+3", "1*2*3"];
```

#### Test Case 2:

```js
Input: (num = "232"), (target = 8);
Output: ["2*3+2", "2+3*2"];
```

#### Test Case 3:

```js
Input: (num = "105"), (target = 5);
Output: ["1*0+5", "10-5"];
```

#### Test Case 4:

```js
Input: (num = "00"), (target = 0);
Output: ["0+0", "0-0", "0*0"];
```

#### Test Case 5:

```js
Input: (num = "3456237490"), (target = 9191);
Output: [];
```

---

### 💡 Intuition

We’ll use **backtracking** and **build expressions** step by step.

At each digit:

- Either **append it** to the current number (for multi-digit numbers)
- Or **place an operator** before it

Key challenge:

- Handle multiplication correctly:
  Since multiplication has precedence, keep track of **previous operand** to adjust current value.

Also, avoid numbers with **leading zeros**, e.g., `"05"` is invalid.

---

### 🔄 Dry Run (num = "123", target = 6)

- Start: "1" → Try "+" → "1+2" → Try "+" → "1+2+3" = 6 ✅
- Try "*" → "1*2\*3" = 6 ✅

---

### 🧑‍💻 JavaScript Code

```javascript
function addOperators(num, target) {
  const result = [];

  function backtrack(index, path, evaluated, prevNum) {
    if (index === num.length) {
      if (evaluated === target) {
        result.push(path);
      }
      return;
    }

    for (let i = index; i < num.length; i++) {
      if (i !== index && num[index] === "0") break; // Skip leading zero
      const currStr = num.slice(index, i + 1);
      const currNum = parseInt(currStr);

      if (index === 0) {
        backtrack(i + 1, currStr, currNum, currNum); // First number, no operator
      } else {
        backtrack(i + 1, path + "+" + currStr, evaluated + currNum, currNum);
        backtrack(i + 1, path + "-" + currStr, evaluated - currNum, -currNum);
        backtrack(
          i + 1,
          path + "*" + currStr,
          evaluated - prevNum + prevNum * currNum,
          prevNum * currNum
        );
      }
    }
  }

  backtrack(0, "", 0, 0);
  return result;
}

// Test
console.log(addOperators("123", 6)); // ["1+2+3", "1*2*3"]
console.log(addOperators("105", 5)); // ["1*0+5", "10-5"]
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:**

  - Exponential: `O(4^n)` in worst case (since 3 operators tried per digit)

- **Space Complexity:**

  - `O(n)` recursion stack + result list

---

### 🚀 Bonus Variants

- Add parentheses to influence precedence
- Only allow `+` and `-`
- Minimum number of operators to reach target

---

## 9. **Generate All Permutations**

You're given an array (or string) of distinct elements.
Return **all possible permutations** (i.e., all possible orderings).

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: [1, 2, 3];
Output: [
  [1, 2, 3],
  [1, 3, 2],
  [2, 1, 3],
  [2, 3, 1],
  [3, 2, 1],
  [3, 1, 2],
];
```

#### Test Case 2:

```js
Input: [1];
Output: [[1]];
```

---

### **Approch 1**

#### 💡 Intuition

Use **backtracking** and **swap-based recursion**:

- Start at index 0, try swapping every element from `i → n - 1` into position `i`
- Recurse for the next index
- After recursion, **undo the swap** (backtrack)

---

#### 🔄 Dry Run (nums = \[1, 2])

- `i = 0`:

  - swap(0,0) → \[1,2] → recurse
  - swap(1,1) → \[1,2] ✅
  - backtrack

- `i = 0`:

  - swap(0,1) → \[2,1] → recurse
  - swap(1,1) → \[2,1] ✅
  - backtrack

---

#### 🧑‍💻 JavaScript Code

```javascript
function permute(nums) {
  const result = [];

  function backtrack(index) {
    if (index === nums.length) {
      result.push([...nums]);
      return;
    }

    for (let i = index; i < nums.length; i++) {
      [nums[i], nums[index]] = [nums[index], nums[i]]; // Swap
      backtrack(index + 1);
      [nums[i], nums[index]] = [nums[index], nums[i]]; // Backtrack
    }
  }

  backtrack(0);
  return result;
}

// Test
console.log(permute([1, 2, 3]));
```

---

#### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(n × n!)`

  - `n!` permutations, and each takes `O(n)` time to copy

- **Space Complexity:** `O(n)` for recursion + result list

---

Great! Let’s now solve the **Permutations problem using Bitmasking (mask approach)** — a **powerful optimization technique** often used in problems involving combinations or permutations of a fixed set.

This will be **Problem 10** in your sequence.

---

### **Approch 2**

---

#### 💡 Intuition

- Initialize `mask = 0` (no elements used)
- At each recursion level:

  - Loop over all elements
  - If the i-th bit of the mask is `0`, it means the element is unused
  - Add the element to path, set the i-th bit to `1`, and recurse

- When path length equals `nums.length`, push a copy to the result

---

#### 🔄 Bitmask Dry Run (nums = \[1,2])

- mask = 00

  - pick 1 → mask = 01 → pick 2 → mask = 11 → ✅
  - backtrack
  - pick 2 → mask = 10 → pick 1 → mask = 11 → ✅

---

#### 🧑‍💻 JavaScript Code (Masking)

```javascript
function permuteWithMask(nums) {
  const result = [];
  const n = nums.length;

  function backtrack(path, mask) {
    if (path.length === n) {
      result.push([...path]);
      return;
    }

    for (let i = 0; i < n; i++) {
      // Check if the i-th bit is 0 (not used)
      if ((mask & (1 << i)) === 0) {
        path.push(nums[i]);
        backtrack(path, mask | (1 << i)); // Set i-th bit to 1
        path.pop();
      }
    }
  }

  backtrack([], 0);
  return result;
}

// Test
console.log(permuteWithMask([1, 2, 3]));
```

---

#### 🧠 Bitmask Basics

| Bit Operation   | Meaning                  |                  |
| --------------- | ------------------------ | ---------------- |
| `1 << i`        | Shift 1 to the i-th bit  |                  |
| `mask & (1<<i)` | Check if i-th bit is set |                  |
| \`mask          | (1<\<i)\`                | Set the i-th bit |

---

#### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(n × n!)`
- **Space Complexity:** `O(n)` for call stack

---

#### 🔁 Variants

- **Permutations with Duplicates** (needs sorting + visited set)
- **String permutations**
- **Next permutation in lexicographic order**
- **Kth permutation**
