# 🧠 Bit Manipulation

## ✅ What is Bit Manipulation?

**Bit Manipulation** refers to the act of algorithmically manipulating bits (0s and 1s) of integers. It's a powerful technique used to **optimize space and time**, especially in competitive programming and system-level coding.

Integers are stored as **binary numbers** in memory. Bit manipulation exploits this to do fast computations.

---

## 🧮 Binary System Review

- Binary: Base-2 system with digits `0` and `1`.
- Each digit is a **bit**.
- Example:
  Decimal `13` = Binary `1101`

---

## 📚 Useful Bitwise Operators in JavaScript (and most languages)

| Operator    | Symbol | Description               | Example                       |     |     |
| ----------- | ------ | ------------------------- | ----------------------------- | --- | --- |
| AND         | `&`    | 1 if both bits are 1      | `5 & 3 = 1`                   |     |     |
| OR          | `\|`   | 1 if any bit is 1         | `5  \| 3 = 7`                 |
| XOR         | `^`    | 1 if bits are different   | `5 ^ 3 = 6`                   |     |     |
| NOT         | `~`    | Inverts all bits          | `~5 = -6` (in 2's complement) |     |     |
| LEFT SHIFT  | `<<`   | Shifts bits left, adds 0s | `5 << 1 = 10`                 |     |     |
| RIGHT SHIFT | `>>`   | Shifts bits right         | `5 >> 1 = 2`                  |     |     |

---

## 🔎 Bitwise Truth Table

| A   | B   | A & B | A \| B | A ^ B |
| --- | --- | ----- | ------ | ----- |
| 0   | 0   | 0     | 0      | 0     |
| 0   | 1   | 0     | 1      | 1     |
| 1   | 0   | 0     | 1      | 1     |
| 1   | 1   | 1     | 1      | 0     |

---

## 🧠 What is 2's Complement?

**2’s complement** is a binary system used to represent **signed integers** (both positive and negative) in computers.

- The **most significant bit (MSB)** indicates the **sign**:

  - `0` → positive
  - `1` → negative

---

### 🧮 How to Get Value in 2’s Complement (for Binary Number)

#### ✅ If MSB is 0:

- It’s **positive**
- Just convert normally

#### ✅ If MSB is 1:

- It’s **negative**
- Use the following method:

#### 🔄 Steps:

1. **Check MSB** (leftmost bit)
2. If MSB = 1, it’s **negative**:

   - Invert all bits (`~`)
   - Add 1
   - Convert to decimal
   - Final result = **`- (that decimal)`**

---

### 🔢 Example 1: 8-bit `11111100`

#### Step-by-step:

- MSB = `1` → it’s **negative**
- Binary = `11111100`

1. Invert all bits: `00000011`
2. Add 1 → `00000100` = `4`
3. Final result = `-4`

✅ `11111100 (binary)` → `-4 (decimal)`

---

### 🔢 Example 2: 8-bit `10000001`

- MSB = 1 → negative
- Invert: `01111110`
- Add 1: `01111111` = 127
- Final result = `-127`

✅ `10000001` → `-127`

---

### 🔢 Example 3: 8-bit `00010110`

- MSB = 0 → positive
- Convert normally = `22`

✅ `00010110` → `22`

---

#### ✅ TL;DR: To Convert 2’s Complement to Integer

- If MSB is `0`: convert normally
- If MSB is `1`:
  → `invert` → `add 1` → `convert` → `negate`

## **`~` Bitwise NOT or complement**

### 🔍 What is the `~` (Bitwise NOT) Operator?

The `~` operator takes a **single operand** and **inverts all its bits**:

| Bit | \~Bit |
| --- | ----- |
| 0   | 1     |
| 1   | 0     |

In JavaScript, all numbers are 64-bit **floating point** internally, but **bitwise operations** convert them to **signed 32-bit integers** (2’s complement).

---

### 🧠 How It Works: 2’s Complement View

Let’s say you have:

```js
x = 5;
```

#### Step-by-step:

1. `5` in **32-bit binary**:

   ```
   00000000 00000000 00000000 00000101
   ```

2. `~5` → flip every bit:

   ```
   11111111 11111111 11111111 11111010
   ```

3. Result is **-6** → Why?

In 2’s complement:

```
~x = -x - 1
```

So:

```js
~5 = -5 - 1 = -6
```

---

### 📘 Key Rule:

```js
(~x === -x - 1 - x) === ~x + 1;
```

✅ Always true for **integers**

---

### 🔢 Examples

| Expression | Binary View                 | Result |
| ---------- | --------------------------- | ------ |
| `~0`       | `000...0000` → `111...1111` | `-1`   |
| `~1`       | `000...0001` → `111...1110` | `-2`   |
| `~2`       | `000...0010` → `111...1101` | `-3`   |
| `~(-1)`    | `111...1111` → `000...0000` | `0`    |
| `~(-2)`    | `111...1110` → `000...0001` | `1`    |

---

### ✅ Code Examples in JavaScript

```js
console.log(~0); // -1
console.log(~1); // -2
console.log(~2); // -3
console.log(~5); // -6
console.log(~-1); // 0
console.log(~-10); // 9
```

---

### ⚙️ Real-World Uses

#### ✅ 1. **Toggle all bits (like image masks, pixel inversion)**

```js
let x = 42;
let inverted = ~x; // flip all bits
```

#### ✅ 2. **Bit tricks (like checking for 0)**

```js
if (~arr.indexOf(val)) {
  // means index is not -1
}
```

Because `~(-1)` becomes `0`, which is falsy.

#### ✅ 3. **Convert bit-flips back**

```js
x = 7;
console.log(~~x); // returns 7 again
```

---

### ⚠️ Notes on JavaScript

- Bitwise operations **coerce** numbers to 32-bit **signed integers**
- Large numbers like `2^31` will wrap due to overflow

---

# **Learn Bit Manipulation**

## **1. Check if the i-th Bit is Set or Not**

### 📘 Problem Statement

You're given an integer `n` and a position `i` (0-based index from right).
Check whether the **i-th bit** of `n` is set (**1**) or not (**0**).

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: n = 13, i = 2
Explanation: 13 = 1101 (binary), 2nd bit from right is 1 → set
Output: true
```

#### ✅ Test Case 2:

```js
Input: n = 13, i = 1
Explanation: 13 = 1101, 1st bit is 0 → not set
Output: false
```

#### ✅ Test Case 3:

```js
Input: (n = 0), (i = 3);
Output: false;
```

#### ✅ Test Case 4:

```js
Input: (n = 1), (i = 0);
Output: true;
```

---

### 💡 Intuition

- To check if the i-th bit is set, shift `1` to the left by `i` positions and perform bitwise AND:

```js
(n & (1 << i)) !== 0;
```

- If the result is non-zero → bit is set

---

### 🔄 Dry Run

Let `n = 13 (1101)` and `i = 2`

- `1 << 2 = 0100`
- `1101 & 0100 = 0100` → Non-zero → Set ✅

---

### 🧑‍💻 JavaScript Code

```js
function isBitSet(n, i) {
  return (n & (1 << i)) !== 0;
}

// Test
console.log(isBitSet(13, 2)); // true
console.log(isBitSet(13, 1)); // false
```

---

### ⏱️ Time & Space Complexity

- **Time:** `O(1)` — Constant time operation
- **Space:** `O(1)`

---

### 📌 Summary

| Operation      | Bitwise Expression    | Result       |
| -------------- | --------------------- | ------------ |
| Check i-th bit | `(n & (1 << i)) != 0` | true / false |

---

## **2. Check if a Number is Odd or Not**

### 📘 Problem Statement

Given an integer `n`, determine whether it is **odd** or **even** using **bit manipulation**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: 7;
Output: true; // 7 is odd
```

#### ✅ Test Case 2:

```js
Input: 10;
Output: false; // 10 is even
```

#### ✅ Test Case 3:

```js
Input: 0;
Output: false;
```

#### ✅ Test Case 4:

```js
Input: -3;
Output: true;
```

---

### 💡 Intuition

In **binary**, the **least significant bit (LSB)** of a number tells you if it's odd or even:

- If the **last bit is 1**, it's **odd**
- If the **last bit is 0**, it's **even**

We can check the last bit using bitwise AND with `1`:

```js
(n & 1) === 1 → odd
(n & 1) === 0 → even
```

---

### 🔄 Dry Run

Let `n = 7 (0111)`:

- `7 & 1 = 0111 & 0001 = 0001` → 1 → Odd ✅

Let `n = 10 (1010)`:

- `10 & 1 = 1010 & 0001 = 0000` → 0 → Even ✅

---

### 🧑‍💻 JavaScript Code

```js
function isOdd(n) {
  return (n & 1) === 1;
}

// Test
console.log(isOdd(7)); // true
console.log(isOdd(10)); // false
console.log(isOdd(0)); // false
console.log(isOdd(-3)); // true
```

---

### ⏱️ Time & Space Complexity

- **Time:** `O(1)` — constant time
- **Space:** `O(1)`

---

## **3. Check if a Number is Power of 2 or Not**

### 📘 Problem Statement

Given an integer `n`, determine whether it is a **power of 2** using **bit manipulation**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: 1;
Output: true; // 2^0 = 1
```

#### ✅ Test Case 2:

```js
Input: 8;
Output: true; // 2^3 = 8
```

#### ✅ Test Case 3:

```js
Input: 6;
Output: false;
```

#### ✅ Test Case 4:

```js
Input: 0;
Output: false;
```

---

### 💡 Intuition

A number is a power of 2 **if and only if**:

- It has **exactly one set bit** in its binary representation.
- This means `n & (n - 1) === 0`

👉 Why?
When `n` is a power of 2, its binary form looks like: `1000...0`
Subtracting 1 flips the **rightmost set bit** and all bits to its right, so:

```text
Example:
n = 8 → 1000
n - 1 = 7 → 0111
n & (n - 1) = 1000 & 0111 = 0000
```

---

### 🔄 Dry Run

Let `n = 16`:

- Binary: `10000`
- `n - 1 = 15` → `01111`
- `n & (n - 1) = 00000` → ✅ Power of 2

Let `n = 10`:

- Binary: `1010`
- `n - 1 = 1001`
- `n & (n - 1) = 1000` → ≠ 0 → ❌ Not power of 2

---

### 🧑‍💻 JavaScript Code

```js
function isPowerOfTwo(n) {
  return n > 0 && (n & (n - 1)) === 0;
}

// Test
console.log(isPowerOfTwo(1)); // true
console.log(isPowerOfTwo(8)); // true
console.log(isPowerOfTwo(6)); // false
console.log(isPowerOfTwo(0)); // false
```

---

### ⏱️ Time & Space Complexity

- **Time:** `O(1)`
- **Space:** `O(1)`

---

## **4. Count the Number of Set Bits**

### 📘 Problem Statement

Given a non-negative integer `n`, **count the number of set bits** (i.e., the number of `1`s in the binary representation of `n`).

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: 5
Explanation: 5 → 101 → 2 set bits
Output: 2
```

#### ✅ Test Case 2:

```js
Input: 15
Explanation: 15 → 1111 → 4 set bits
Output: 4
```

#### ✅ Test Case 3:

```js
Input: 0;
Output: 0;
```

#### ✅ Test Case 4:

```js
Input: 1;
Output: 1;
```

---

### 💡 Intuition

There are two common approaches:

---

### ⚙️ Approach 1: **Brian Kernighan's Algorithm** ✅ _Optimal_

- Each time, we remove the **rightmost set bit** by doing `n = n & (n - 1)`
- Count how many times we can do that before `n` becomes 0

### 🔄 Dry Run (n = 13 → 1101)

1. `1101 & 1100 = 1100`
2. `1100 & 1011 = 1000`
3. `1000 & 0111 = 0000`

→ 3 set bits ✅

---

### 🧑‍💻 JavaScript Code (Kernighan’s Algorithm)

```js
function countSetBits(n) {
  let count = 0;
  while (n > 0) {
    n = n & (n - 1); // Remove rightmost set bit
    count++;
  }
  return count;
}
```

---

### ⚙️ Approach 2: **Simple Bit-by-Bit Method** _(Less Efficient)_

```js
function countSetBits(n) {
  let count = 0;
  while (n > 0) {
    count += n & 1;
    n >>= 1;
  }
  return count;
}
```

---

### ⏱️ Time & Space Complexity

| Approach        | Time Complexity       | Space Complexity |
| --------------- | --------------------- | ---------------- |
| Brian Kernighan | `O(k)` (k = set bits) | `O(1)`           |
| Bit-by-Bit      | `O(log n)`            | `O(1)`           |

---

## 🔢 **5. Set/Unset the Rightmost Unset Bit**

### 📘 Problem Statement

You're given an integer `n`.
Your task is to **set** or **unset** the **rightmost unset bit (0)** in its binary representation.

---

### 🔧 Two Operations:

### ✅ A. **Set the Rightmost Unset Bit**

> Turn the first `0` (from the right) into a `1`

---

### 🧪 Test Cases (Set Rightmost Unset Bit)

#### Test Case 1:

```js
Input: 10 → 1010
Output: 1011 → 11
```

#### Test Case 2:

```js
Input: 7 → 0111
Output: 1111 → 15
```

#### Test Case 3:

```js
Input: 15 → 1111
Output: 1111 → 15 (no unset bits)
```

---

### 💡 Intuition (Set)

- To set the **rightmost 0**, do:

```js
n | (n + 1);
```

#### Why it works:

- Adding 1 flips the rightmost `0` to `1` and all `1`s to the right to `0`.
- `OR` will set that `0` to `1` while preserving all other bits.

---

### 🧑‍💻 JavaScript Code

```js
function setRightmostUnsetBit(n) {
  return n | (n + 1);
}
```

---

### ⏱️ Time & Space Complexity

| Operation               | Time   | Space  |
| ----------------------- | ------ | ------ |
| Set rightmost unset bit | `O(1)` | `O(1)` |

---

## 🔢 **6. Swap Two Numbers (Without Temp Variable)**

### 📘 Problem Statement

Given two integers `a` and `b`, **swap their values** using **bitwise operations only**, without using a third variable.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (a = 5), (b = 7);
Output: (a = 7), (b = 5);
```

#### ✅ Test Case 2:

```js
Input: (a = 0), (b = 10);
Output: (a = 10), (b = 0);
```

#### ✅ Test Case 3:

```js
Input: (a = -3), (b = 9);
Output: (a = 9), (b = -3);
```

---

### 💡 Intuition

We can use **XOR `^`** to swap values without a temp variable:

```js
a = a ^ b;
b = a ^ b; // (a ^ b) ^ b = a
a = a ^ b; // (a ^ b) ^ a = b
```

This works because XOR has the following properties:

- `a ^ a = 0`
- `a ^ 0 = a`
- `a ^ b ^ b = a`

---

### 🔄 Dry Run

Let `a = 5 (0101)`, `b = 7 (0111)`

```text
Step 1: a = a ^ b → 0101 ^ 0111 = 0010 (a = 2)
Step 2: b = a ^ b → 0010 ^ 0111 = 0101 (b = 5)
Step 3: a = a ^ b → 0010 ^ 0101 = 0111 (a = 7)
```

✅ Swapped: a = 7, b = 5

---

### 🧑‍💻 JavaScript Code

```js
function swap(a, b) {
  console.log(`Before Swap: a = ${a}, b = ${b}`);
  a = a ^ b;
  b = a ^ b;
  a = a ^ b;
  console.log(`After Swap: a = ${a}, b = ${b}`);
}

// Test
swap(5, 7);
swap(0, 10);
swap(-3, 9);
```

---

### ⏱️ Time & Space Complexity

- **Time:** `O(1)`
- **Space:** `O(1)`

---

### 📌 Summary

| Operation      | Code                      |
| -------------- | ------------------------- |
| Swap using XOR | `a ^= b; b ^= a; a ^= b;` |

---

## 🔢 **7. Divide Two Integers Without Using `*`, `/`, or `%` Operators**

### 📘 Problem Statement

Given two integers `dividend` and `divisor`, **divide them** and return the **quotient**, **without using**:

- `*` (multiplication)
- `/` (division)
- `%` (modulus)

You **must truncate** toward zero (i.e., 7 / -3 = -2).

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (dividend = 10), (divisor = 3);
Output: 3;
```

#### ✅ Test Case 2:

```js
Input: (dividend = 7), (divisor = -3);
Output: -2;
```

#### ✅ Test Case 3:

```js
Input: (dividend = 0), (divisor = 1);
Output: 0;
```

#### ✅ Test Case 4:

```js
Input: (dividend = -2147483648), (divisor = -1);
Output: 2147483647; // Clamp to MAX_INT (32-bit)
```

---

### 💡 Intuition

Use **bit shifting and subtraction**:

- We subtract the largest multiple of divisor (`divisor × 2^k`) from dividend.
- Bit shifting lets us quickly check `divisor << k` ≤ dividend.
- Repeat until dividend < divisor.

---

### 🔄 Dry Run

Let `dividend = 10`, `divisor = 3`:

- 3 << 1 = 6 → subtract 6 → quotient += 2
- remaining 4 → 3 << 0 = 3 → subtract 3 → quotient += 1
- result: `3`

---

### 🧑‍💻 JavaScript Code

```js
function divide(dividend, divisor) {
  const MAX_INT = 2 ** 31 - 1;
  const MIN_INT = -(2 ** 31);

  // Handle overflow edge case
  if (dividend === MIN_INT && divisor === -1) return MAX_INT;

  // Determine sign
  const sign = dividend > 0 === divisor > 0 ? 1 : -1;

  // Work with absolute values
  let a = Math.abs(dividend);
  let b = Math.abs(divisor);
  let quotient = 0;

  while (a >= b) {
    let temp = b,
      multiple = 1;
    while (temp << 1 <= a) {
      temp <<= 1;
      multiple <<= 1;
    }
    a -= temp;
    quotient += multiple;
  }

  return sign * quotient;
}
```

---

### ⏱️ Time & Space Complexity

- **Time:** `O(log² N)`

  - Outer loop: log(dividend)
  - Inner loop: log(dividend)

- **Space:** `O(1)`

---

### ⚠️ Edge Cases

- Division by zero → Not handled (you can throw an error if needed)
- Integer overflow (e.g., `-2³¹ / -1`) → Clamp to `2³¹ - 1`

---

# Interview Problems

## 🔢 **1. Count Number of Bits to Be Flipped to Convert A to B**

### 📘 Problem Statement

Given two integers `A` and `B`, return the **number of bits that need to be flipped** in `A` to convert it into `B`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (A = 10), (B = 20);
Binary: (A = 1010), (B = 10100);
Output: 4;
```

#### ✅ Test Case 2:

```js
Input: A = 7, B = 10
Binary: A = 0111, B = 1010 → 3 bits differ
Output: 3
```

#### ✅ Test Case 3:

```js
Input: (A = 0), (B = 0);
Output: 0;
```

---

### 💡 Intuition

To find differing bits between A and B:

1. Take XOR of A and B → bits set in the result are where A and B differ.
2. Count number of set bits in the result.

```js
A ^ B → bits that are different
```

Then use **Kernighan's Algorithm** to count set bits efficiently.

---

### 🔄 Dry Run (A = 10, B = 20)

- A = `01010`, B = `10100`
- A ^ B = `11110`
- Number of 1s = 4 → ✅ 4 bits to flip

---

### 🧑‍💻 JavaScript Code

```js
function countFlips(A, B) {
  let xor = A ^ B;
  let count = 0;

  while (xor > 0) {
    xor = xor & (xor - 1); // remove rightmost set bit
    count++;
  }

  return count;
}

// Test
console.log(countFlips(10, 20)); // 4
console.log(countFlips(7, 10)); // 3
console.log(countFlips(0, 0)); // 0
```

---

### ⏱️ Time & Space Complexity

- **Time:** `O(k)` where `k` = number of differing bits (at most `log n`)
- **Space:** `O(1)`

---

### 📌 Summary

| Step       | Expression        | Meaning                   |
| ---------- | ----------------- | ------------------------- |
| XOR        | `A ^ B`           | Bits that differ          |
| Count bits | `xor & (xor - 1)` | Removes rightmost set bit |

---

## 🔢 **2. Find the Number that Appears Odd Number of Times**

### 📘 Problem Statement

Given an array of integers where **all numbers occur even number of times** **except one number**, which occurs **odd number of times** — find that number.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: [1, 2, 3, 2, 3, 1, 3];
Output: 3;
```

#### ✅ Test Case 2:

```js
Input: [4, 5, 4, 5, 4];
Output: 4;
```

#### ✅ Test Case 3:

```js
Input: [99];
Output: 99;
```

---

### 💡 Intuition

When you XOR a number with itself, it becomes 0:
`a ^ a = 0`
When you XOR with 0:
`a ^ 0 = a`

So if all elements appear even number of times **except one**, their XOR cancels out, and you're left with the odd-occurring number.

---

### 🔄 Dry Run (Input = \[1, 2, 3, 2, 3, 1, 3])

```text
Step-by-step XOR:
1 ^ 2 = 3
3 ^ 3 = 0
0 ^ 2 = 2
2 ^ 3 = 1
1 ^ 1 = 0
0 ^ 3 = 3 → ✅
```

---

### 🧑‍💻 JavaScript Code

```js
function findOddOccurrence(arr) {
  let result = 0;

  for (let num of arr) {
    result ^= num;
  }

  return result;
}

// Test
console.log(findOddOccurrence([1, 2, 3, 2, 3, 1, 3])); // 3
console.log(findOddOccurrence([4, 5, 4, 5, 4])); // 4
console.log(findOddOccurrence([99])); // 99
```

---

### ⏱️ Time & Space Complexity

- **Time:** `O(n)` — Single pass
- **Space:** `O(1)` — Constant space

---

## 🔢 **3. Generate the Power Set (All Subsequences)**

### 📘 Problem Statement

Given an array or string of **distinct elements**, return the **power set** — all possible **subsets** (including empty and full set).

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: [1, 2];
Output: [[], [1], [2], [1, 2]];
```

#### ✅ Test Case 2:

```js
Input: [1, 2, 3];
Output: [[], [1], [2], [3], [1, 2], [1, 3], [2, 3], [1, 2, 3]];
```

#### ✅ Test Case 3:

```js
Input: [];
Output: [[]];
```

---

### 💡 Intuition (Bitmasking)

If the input has `n` elements, then:

- The power set will have `2^n` subsets.
- Each subset can be represented by an **n-bit number**:

  - Each bit represents inclusion (1) or exclusion (0) of the i-th element.

---

### 🔄 Dry Run (nums = \[1, 2, 3])

We loop over numbers from `0` to `2^3 - 1 = 7`:

```text
0 → 000 → []
1 → 001 → [3]
2 → 010 → [2]
3 → 011 → [2, 3]
4 → 100 → [1]
5 → 101 → [1, 3]
6 → 110 → [1, 2]
7 → 111 → [1, 2, 3]
```

---

### 🧑‍💻 JavaScript Code

```js
function powerSet(nums) {
  const result = [];
  const n = nums.length;
  const total = 1 << n; // 2^n subsets

  for (let mask = 0; mask < total; mask++) {
    const subset = [];
    for (let i = 0; i < n; i++) {
      if ((mask & (1 << i)) !== 0) {
        subset.push(nums[i]);
      }
    }
    result.push(subset);
  }

  return result;
}

// Test
console.log(powerSet([1, 2, 3]));
```

---

### ⏱️ Time & Space Complexity

- **Time:** `O(n × 2^n)` — Each of the `2^n` subsets may contain up to `n` elements
- **Space:** `O(n × 2^n)` — For storing the result

---

## 🔢 **4. Find XOR of Numbers from `L` to `R`**

### 📘 Problem Statement

Given two integers `L` and `R`, compute the XOR of all numbers in the range:

```text
L ^ (L+1) ^ (L+2) ^ ... ^ R
```

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: L = 3, R = 9
Output: 10

Explanation:
3 ^ 4 ^ 5 ^ 6 ^ 7 ^ 8 ^ 9 = 10
```

#### ✅ Test Case 2:

```js
Input: (L = 5), (R = 5);
Output: 5;
```

#### ✅ Test Case 3:

```js
Input: (L = 0), (R = 4);
Output: 4;
```

---

### 💡 Intuition

Instead of looping from `L` to `R`, we use this **property of XOR from 0 to n**:

```text
XOR(0 to n) =
  n      if n % 4 == 0
  1      if n % 4 == 1
  n + 1  if n % 4 == 2
  0      if n % 4 == 3
```

To compute `XOR(L to R)`, use:

```text
XOR(L to R) = XOR(0 to R) ^ XOR(0 to L-1)
```

---

### 🔄 Dry Run

Let L = 3, R = 9

- XOR(0 to 9) = 1 (because 9 % 4 = 1)
- XOR(0 to 2) = 3 (because 2 % 4 = 2 → 3)
- Result = 1 ^ 3 = 2 ✅

Oops! Wait — this contradicts the earlier brute-force result of 10.

Let’s double-check the brute-force XOR:

```text
3 ^ 4 = 7
7 ^ 5 = 2
2 ^ 6 = 4
4 ^ 7 = 3
3 ^ 8 = 11
11 ^ 9 = 2 ✅
```

Actual: **2**, not 10.

---

### 🧑‍💻 JavaScript Code

```js
// XOR from 0 to n using pattern
function xorFrom0ToN(n) {
  if (n % 4 === 0) return n;
  if (n % 4 === 1) return 1;
  if (n % 4 === 2) return n + 1;
  return 0;
}

function xorFromLtoR(L, R) {
  return xorFrom0ToN(R) ^ xorFrom0ToN(L - 1);
}

// Test
console.log(xorFromLtoR(3, 9)); // 2
console.log(xorFromLtoR(5, 5)); // 5
console.log(xorFromLtoR(0, 4)); // 4
```

---

### ⏱️ Time & Space Complexity

- **Time:** `O(1)` — Pattern-based constant time
- **Space:** `O(1)`

---

## 🔢 **5. Find the Two Numbers Appearing Odd Number of Times**

### 📘 Problem Statement

Given an array where **exactly two numbers appear odd number of times**, and all others appear even number of times, find **those two numbers**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: [4, 3, 4, 4, 5, 5, 3, 6];
Output: [4, 6]; // Order may vary
```

#### ✅ Test Case 2:

```js
Input: [2, 3, 7, 9, 2, 3, 9, 11];
Output: [7, 11];
```

#### ✅ Test Case 3:

```js
Input: [10, 15, 10, 15, 99, 77];
Output: [99, 77];
```

---

### 💡 Intuition

Let’s break it down using XOR:

### 🧠 Step-by-Step Approach:

1. **XOR all elements**:

   - This gives us: `xor = x ^ y` (where x and y are the odd-appearing numbers)

2. **Find rightmost set bit** in `xor`:

   - It tells us a position where `x` and `y` differ.

3. **Divide elements into 2 groups** based on that bit:

   - Group 1: bit set → will contain either `x` or `y`
   - Group 2: bit not set → contains the other one

4. **XOR each group separately** → will isolate `x` and `y`

---

### 🔄 Dry Run (arr = \[4, 3, 4, 4, 5, 5, 3, 6])

- XOR all:
  `4 ^ 3 ^ 4 ^ 4 ^ 5 ^ 5 ^ 3 ^ 6 = 2`
- Rightmost set bit: `2 & (-2)` = `2` → means bit position 1 is set

Now divide:

- Group 1 (`bit set at pos 1`): 3, 3, 6 → `3 ^ 3 ^ 6 = 6`
- Group 2 (`bit not set at pos 1`): 4, 4, 4, 5, 5 → `4 ^ 4 ^ 4 ^ 5 ^ 5 = 4`

✅ Final: \[6, 4]

---

### 🧑‍💻 JavaScript Code

```js
function findTwoOddNumbers(arr) {
  let xor = 0;

  // Step 1: XOR of all elements = x ^ y
  for (let num of arr) {
    xor ^= num;
  }

  // Step 2: Find rightmost set bit in xor
  let rightmostSetBit = xor & -xor;

  // Step 3: Divide into two groups
  let num1 = 0,
    num2 = 0;
  for (let num of arr) {
    if (num & rightmostSetBit) {
      num1 ^= num;
    } else {
      num2 ^= num;
    }
  }

  return [num1, num2]; // order doesn't matter
}

// Test
console.log(findTwoOddNumbers([4, 3, 4, 4, 5, 5, 3, 6])); // [4, 6]
console.log(findTwoOddNumbers([2, 3, 7, 9, 2, 3, 9, 11])); // [7, 11]
```

---

### ⏱️ Time & Space Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`

---

# **Advanced Math**

## 🔢 **1. Print Prime Factors of a Number**

### 📘 Problem Statement

Given a positive integer `n`, **print all its prime factors** in ascending order.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: 18;
Output: [2, 3, 3];
```

#### ✅ Test Case 2:

```js
Input: 100;
Output: [2, 2, 5, 5];
```

#### ✅ Test Case 3:

```js
Input: 29;
Output: [29];
```

#### ✅ Test Case 4:

```js
Input: 1;
Output: [];
```

---

### 💡 Intuition

To get all prime factors of `n`:

1. First divide out all `2`s (smallest prime)
2. Then check for all odd numbers up to √n:

   - If a number divides `n`, it's a factor — divide it repeatedly

3. If `n > 1` at the end, `n` itself is prime

---

### 🔄 Dry Run

For `n = 18`:

- 18 divisible by 2 → push 2 → now n = 9
- 9 divisible by 3 → push 3 twice → now n = 1
  ✅ Prime factors: \[2, 3, 3]

---

### 🧑‍💻 JavaScript Code

```js
function primeFactors(n) {
  const result = [];

  // Step 1: Remove all 2s
  while (n % 2 === 0) {
    result.push(2);
    n = n / 2;
  }

  // Step 2: Check odd numbers from 3 to sqrt(n)
  for (let i = 3; i * i <= n; i += 2) {
    while (n % i === 0) {
      result.push(i);
      n = n / i;
    }
  }

  // Step 3: If n is still greater than 1, it's prime
  if (n > 1) {
    result.push(n);
  }

  return result;
}

// Test
console.log(primeFactors(18)); // [2, 3, 3]
console.log(primeFactors(100)); // [2, 2, 5, 5]
console.log(primeFactors(29)); // [29]
console.log(primeFactors(1)); // []
```

---

### ⏱️ Time & Space Complexity

- **Time:** `O(√n)`
- **Space:** `O(log n)` (for result array)

---

## 🔢 **2. Print All Divisors of a Number**

### 📘 Problem Statement

Given a positive integer `n`, print **all of its divisors** (numbers that divide `n` exactly), in **ascending order**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: 10;
Output: [1, 2, 5, 10];
```

#### ✅ Test Case 2:

```js
Input: 36;
Output: [1, 2, 3, 4, 6, 9, 12, 18, 36];
```

#### ✅ Test Case 3:

```js
Input: 1;
Output: [1];
```

---

### 💡 Intuition

- A **naive approach** checks all numbers from `1` to `n` → `O(n)` time.
- An **efficient approach** checks from `1` to `√n`, and for every `i` such that `n % i == 0`, both `i` and `n / i` are divisors.

---

### 🔄 Dry Run (n = 36)

- `i = 1`: 36 % 1 == 0 → push 1 and 36
- `i = 2`: 36 % 2 == 0 → push 2 and 18
- `i = 3`: push 3 and 12
- ...
- Final result: \[1, 36, 2, 18, 3, 12, 4, 9, 6, 6] → remove duplicates, sort

---

### 🧑‍💻 JavaScript Code

```js
function allDivisors(n) {
  const result = new Set();

  for (let i = 1; i * i <= n; i++) {
    if (n % i === 0) {
      result.add(i);
      result.add(n / i);
    }
  }

  return [...result].sort((a, b) => a - b);
}

// Test
console.log(allDivisors(10)); // [1, 2, 5, 10]
console.log(allDivisors(36)); // [1, 2, 3, 4, 6, 9, 12, 18, 36]
console.log(allDivisors(1)); // [1]
```

---

### ⏱️ Time & Space Complexity

- **Time:** `O(√n + k log k)`

  - `√n` iterations + sorting `k` divisors

- **Space:** `O(k)` — number of divisors

---

## 🔢 **3. Sieve of Eratosthenes**

### 📘 Problem Statement

Given an integer `n`, print **all prime numbers** from `2` to `n` using the **Sieve of Eratosthenes** algorithm.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: 10;
Output: [2, 3, 5, 7];
```

#### ✅ Test Case 2:

```js
Input: 1;
Output: [];
```

#### ✅ Test Case 3:

```js
Input: 20;
Output: [2, 3, 5, 7, 11, 13, 17, 19];
```

---

### 💡 Intuition

The **Sieve of Eratosthenes** is an efficient algorithm to find all primes ≤ `n` in **O(n log log n)** time.

#### Idea:

1. Create a boolean array `isPrime[]` of size `n+1` and initialize all as `true`
2. Starting from `p = 2`:

   - If `isPrime[p]` is true, mark all multiples of `p` (from `p*p` to `n`) as false

3. Remaining true indices are prime numbers

---

### 🔄 Dry Run (n = 10)

```text
isPrime = [F, F, T, T, T, T, T, T, T, T, T]

p = 2 → mark 4, 6, 8, 10
p = 3 → mark 9
Final: [2, 3, 5, 7]
```

---

### 🧑‍💻 JavaScript Code

```js
function sieveOfEratosthenes(n) {
  const isPrime = Array(n + 1).fill(true);
  isPrime[0] = isPrime[1] = false;

  for (let i = 2; i * i <= n; i++) {
    if (isPrime[i]) {
      for (let j = i * i; j <= n; j += i) {
        isPrime[j] = false;
      }
    }
  }

  const primes = [];
  for (let i = 2; i <= n; i++) {
    if (isPrime[i]) primes.push(i);
  }

  return primes;
}

// Test
console.log(sieveOfEratosthenes(10)); // [2, 3, 5, 7]
console.log(sieveOfEratosthenes(20)); // [2, 3, 5, 7, 11, 13, 17, 19]
console.log(sieveOfEratosthenes(1)); // []
```

---

### ⏱️ Time & Space Complexity

- **Time:** `O(n log log n)`
- **Space:** `O(n)` (for the `isPrime` array)

---

## 🔢 **4. Prime Factorization Using Sieve (O(log n) per query)**

### 📘 Problem Statement

Preprocess using a sieve so that for **any number ≤ n**, you can return its **prime factorization** efficiently in `O(log n)` time.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: n = 30
Output: [2, 3, 5]
Explanation: 30 = 2 × 3 × 5
```

#### ✅ Test Case 2:

```js
Input: n = 60;
Output: [2, 2, 3, 5];
```

#### ✅ Test Case 3:

```js
Input: n = 97;
Output: [97]; // It's a prime number
```

---

### 💡 Intuition

To factorize in `O(log n)`:

1. Use a **Modified Sieve** to precompute the **Smallest Prime Factor (SPF)** of every number up to `maxN`
2. Then, for any number `n`, divide repeatedly by its `spf[n]` to extract prime factors

---

### 🧠 SPF Array

For each number `i`:

- `spf[i] = smallest prime that divides i`

E.g. `spf[60] = 2`, `spf[30] = 2`, `spf[25] = 5`

---

### 🧑‍💻 JavaScript Code

```js
function computeSPF(N) {
  const spf = Array(N + 1).fill(0);
  for (let i = 0; i <= N; i++) spf[i] = i;

  for (let i = 2; i * i <= N; i++) {
    if (spf[i] === i) {
      for (let j = i * i; j <= N; j += i) {
        if (spf[j] === j) {
          spf[j] = i;
        }
      }
    }
  }

  return spf;
}

function getPrimeFactors(n, spf) {
  const result = [];
  while (n > 1) {
    result.push(spf[n]);
    n = Math.floor(n / spf[n]);
  }
  return result;
}

// Demo
const N = 1000000;
const spf = computeSPF(N);

console.log(getPrimeFactors(30, spf)); // [2, 3, 5]
console.log(getPrimeFactors(60, spf)); // [2, 2, 3, 5]
console.log(getPrimeFactors(97, spf)); // [97]
```

---

### 🔄 Dry Run (n = 60)

- spf\[60] = 2 → push 2 → n = 30
- spf\[30] = 2 → push 2 → n = 15
- spf\[15] = 3 → push 3 → n = 5
- spf\[5] = 5 → push 5 → n = 1
  ✅ Final: \[2, 2, 3, 5]

---

### ⏱️ Time & Space Complexity

- **Preprocessing (sieve):** `O(n log log n)`
- **Factorization per query:** `O(log n)` (since a number has at most `log n` prime factors)
- **Space:** `O(n)` for the `spf` array

---
