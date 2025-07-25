# Basic Math Logic

# 🔢 Count Digits of a Number

### 🧠 Problem Statement:

**Given an integer `n`, count how many digits it has.**

### 🔍 Example:

- Input: `n = 3489`
- Output: `4` (Because 3489 has 4 digits)

---

## ✅ Approach 1: Using Loop and Division

### 💡 Intuition:

- Repeatedly divide the number by `10`.
- Each division removes the last digit.
- Count how many times we can divide before the number becomes `0`.

---

### 🔄 Diagram (Example: n = 3489):

```
Iteration | Number (n) | Operation       | Count
----------|-------------|----------------|------
    1     |   3489      | 3489 / 10 = 348|  1
    2     |   348       | 348 / 10 = 34  |  2
    3     |   34        | 34 / 10 = 3    |  3
    4     |   3         | 3 / 10 = 0     |  4
```

✅ Total Digits = `4`

---

### 🧑‍💻 JavaScript Code:

```javascript
function countDigits(n) {
  let count = 0;
  while (n > 0) {
    n = Math.floor(n / 10); // Remove last digit
    count++;
  }
  return count;
}
console.log(countDigits(3489)); // Output: 4
```

---

### 💎 Edge Case:

If `n = 0`, it should return `1`, since 0 is a single digit.

```javascript
function countDigits(n) {
  if (n === 0) return 1;
  let count = 0;
  while (n > 0) {
    n = Math.floor(n / 10);
    count++;
  }
  return count;
}
```

---

## ✅ Approach 2: Convert to String

### 💡 Intuition:

- Convert the number to a string.
- Count how many characters the string has.

---

### 🧑‍💻 JavaScript Code:

```javascript
function countDigits(n) {
  return n.toString().length;
}
console.log(countDigits(3489)); // Output: 4
```

✅ Simple and clean for small problems.

---

## ✅ Approach 3: Using Math (Logarithmic)

### 💡 Intuition:

- `Math.log10(n)` gives the number of digits minus 1.
- Formula: `Math.floor(Math.log10(n)) + 1`

### ⚠️ Works only when `n > 0`

---

### 🧑‍💻 Code:

```javascript
function countDigits(n) {
  if (n === 0) return 1;
  return Math.floor(Math.log10(n)) + 1;
}
console.log(countDigits(3489)); // Output: 4
```

---

## 📚 Summary Table:

| Approach           | Technique      | Time Complexity | Space |
| ------------------ | -------------- | --------------- | ----- |
| Loop + Division    | Manual count   | O(log₁₀N)       | O(1)  |
| String Conversion  | Convert to str | O(1)            | O(1)  |
| Logarithmic (Math) | Log base 10    | O(1)            | O(1)  |

---

## 📌 Notes for Beginners

- Use `Math.floor()` to remove the decimal after division.
- Use `n.toString().length` only for simple, non-performance-critical problems.
- Always check for `n === 0` as a special case.

---

Perfect! Let’s create **beginner-friendly DSA notes** for the **"Reverse a Number"** problem. This is another foundational problem that helps build strong logic using **loops**, **modulus**, and **division**.

---

# 🔁 Reverse a Number

## 🧠 Problem Statement

**Given an integer `n`, return the number obtained by reversing its digits.**

### 🔍 Example:

- Input: `n = 1234`

- Output: `4321`

- Input: `n = 1000`

- Output: `1` (Leading zeros are ignored)

---

## ✅ Approach: Using Modulus (%) and Division

### 💡 Intuition:

- Use `% 10` to get the **last digit**.
- Use `Math.floor(n / 10)` to **remove the last digit**.
- Build the reversed number by multiplying previous result by 10 and adding the new digit.

---

### 🔄 Visual Diagram (Example: n = 1234)

We extract digits from **right to left** and build the reverse from **left to right**.

```
n = 1234 → reverse = 0

Step 1: digit = 1234 % 10 = 4
        reverse = 0 * 10 + 4 = 4
        n = 1234 / 10 = 123

Step 2: digit = 123 % 10 = 3
        reverse = 4 * 10 + 3 = 43
        n = 123 / 10 = 12

Step 3: digit = 2
        reverse = 43 * 10 + 2 = 432
        n = 1

Step 4: digit = 1
        reverse = 432 * 10 + 1 = 4321
        n = 0
```

---

## 🧑‍💻 JavaScript Code

```javascript
function reverseNumber(n) {
  let rev = 0;

  while (n > 0) {
    let digit = n % 10; // Get last digit
    rev = rev * 10 + digit; // Append digit to reversed number
    n = Math.floor(n / 10); // Remove last digit
  }

  return rev;
}

console.log(reverseNumber(1234)); // Output: 4321
```

---

## 📎 Edge Case: If n = 0

```javascript
console.log(reverseNumber(0)); // Output: 0
```

---

## 🧠 Bonus: Handle Negative Numbers

If you want to support negative numbers:

```javascript
function reverseNumber(n) {
  let isNegative = n < 0;
  n = Math.abs(n);

  let rev = 0;
  while (n > 0) {
    let digit = n % 10;
    rev = rev * 10 + digit;
    n = Math.floor(n / 10);
  }

  return isNegative ? -rev : rev;
}
console.log(reverseNumber(-456)); // Output: -654
```

---

Great! Let's now move on to the next important and beginner-friendly number problem: **Check if a number is a Palindrome**.

---

# 🔁 Palindrome Number

---

## 🧠 Problem Statement

**Given an integer `n`, check whether it is a palindrome or not.**

### ✅ A number is called a **palindrome** if it reads the same forward and backward.

### 🔍 Examples:

- Input: `121` → ✅ Palindrome
- Input: `123` → ❌ Not a Palindrome
- Input: `0` → ✅ Palindrome
- Input: `1221` → ✅ Palindrome
- Input: `-121` → ❌ Not a Palindrome (Negative numbers are not considered palindromes)

---

## ✅ Approach: Reverse the Number and Compare

### 💡 Intuition:

- A number is a palindrome if its **reverse equals the original**.
- So:

  1. Save original number
  2. Reverse the number using modulus + division
  3. Compare the reversed number with the original

---

### 🔄 Diagram (n = 121)

```
Original: 121
Reverse:  121

→ 121 == 121 → ✅ Palindrome
```

---

## 🧑‍💻 JavaScript Code

```javascript
function isPalindrome(n) {
  if (n < 0) return false; // Negative numbers are not palindromes

  let original = n;
  let reversed = 0;

  while (n > 0) {
    let digit = n % 10;
    reversed = reversed * 10 + digit;
    n = Math.floor(n / 10);
  }

  return reversed === original;
}

console.log(isPalindrome(121)); // true
console.log(isPalindrome(123)); // false
console.log(isPalindrome(-121)); // false
```

---

## 📎 Edge Cases

| Input  | Output | Reason                |
| ------ | ------ | --------------------- |
| `121`  | true   | Reverse is 121        |
| `123`  | false  | Reverse is 321        |
| `0`    | true   | Single digit          |
| `-121` | false  | Negative number       |
| `1221` | true   | Even-digit palindrome |

---

## ✅ Extra Challenge: Palindrome as a String

You can also check using string methods (for fun):

```javascript
function isPalindrome(n) {
  if (n < 0) return false;
  let str = n.toString();
  return str === str.split("").reverse().join("");
}
```

---

## 📚 Summary

| Operation     | Use                    |
| ------------- | ---------------------- |
| `% 10`        | Get the last digit     |
| `/ 10`        | Remove the last digit  |
| Compare       | reversed === original  |
| Negative Case | Return false for n < 0 |

---

Awesome! Let's now add notes for one of the most classic and important DSA topics: **GCD (Greatest Common Divisor)** or **HCF (Highest Common Factor)**.

These concepts are often used in **math-based DSA problems**, number theory, and even in simplifying fractions.

---

# 📘 GCD / HCF

## 🧠 What is GCD or HCF?

- The **GCD (Greatest Common Divisor)** or **HCF (Highest Common Factor)** of two numbers is the **largest number that divides both numbers exactly**.

---

### 🔍 Examples:

- GCD(12, 18) = 6
  (Factors of 12: 1, 2, 3, 4, 6, 12;
  Factors of 18: 1, 2, 3, 6, 9, 18;
  Common: 1, 2, 3, 6 → Greatest = **6**)

---

## ✅ Approaches to Find GCD

### 1️⃣ **Naive Approach (Loop from 1 to min(a, b))**

### 2️⃣ **Efficient Approach: Euclidean Algorithm (Most Recommended)**

---

## 🔂 1. Naive Approach (Loop)

### 💡 Intuition:

- Check all numbers from `1` to `min(a, b)`
- Return the largest one that divides both numbers

### 🧑‍💻 JavaScript Code:

```javascript
function gcdNaive(a, b) {
  let gcd = 1;
  for (let i = 1; i <= Math.min(a, b); i++) {
    if (a % i === 0 && b % i === 0) {
      gcd = i;
    }
  }
  return gcd;
}

console.log(gcdNaive(12, 18)); // Output: 6
```

---

# ⚡ 2. Efficient Approach: Euclidean Algorithm

### 💡 Intuition:

- Use this rule:

  ```
  GCD(a, b) = GCD(b, a % b)
  ```

- Repeat until `b = 0`, then `GCD = a`.

---

### 🔄 Diagram (GCD of 48, 18):

```
GCD(48, 18)
→ GCD(18, 48 % 18) = GCD(18, 12)
→ GCD(12, 18 % 12) = GCD(12, 6)
→ GCD(6, 12 % 6)   = GCD(6, 0)
→ Answer = 6
```

---

### 🧑‍💻 JavaScript Code:

```javascript
function gcd(a, b) {
  while (b !== 0) {
    let temp = b;
    b = a % b;
    a = temp;
  }
  return a;
}

console.log(gcd(48, 18)); // Output: 6
```

---

### ✅ Recursive Version:

```javascript
function gcd(a, b) {
  if (b === 0) return a;
  return gcd(b, a % b);
}
```

> **Every 2 steps, the numbers shrink by at least half.**

### 🔍 Let’s Zoom Into 2 Steps

### 🧮 Step 1:

Start with `a > b`.

- Compute `r1 = a % b`
  Now the new pair is `(b, r1)`.

### 🧮 Step 2:

- Compute `r2 = b % r1`
  Now the new pair is `(r1, r2)`.

We want to prove:

> After these 2 steps, the **smaller number becomes ≤ half** of the previous one.

#W# 🧠 Why Does This Matter?

Every 2 steps, we’re shrinking the number by at least half.

So the size of the number drops like this:

```
n → n/2 → n/4 → n/8 → ... until it becomes 0
```

This is a **logarithmic drop**, and it only takes about `log₂(n)` steps to get to zero.

---

#E# 📚 Summary Table

| Approach       | Time Complexity   | Space | Suitable For           |
| -------------- | ----------------- | ----- | ---------------------- |
| Naive Loop     | O(min(a, b))      | O(1)  | Small inputs           |
| Euclidean Algo | O(log(min(a, b))) | O(1)  | Large numbers, DSA use |

---

### ✍️ LCM

- LCM using GCD
  `LCM(a, b) = (a * b) / GCD(a, b)`

---

# **Armstrong Numbers** (a.k.a. Narcissistic Numbers)

## ✨ What is an Armstrong Number?

An **Armstrong number** is a number that **equals the sum of its own digits each raised to the power of the number of digits**. ([exercism.org][1])

**Examples:**

- `9`: 1-digit → $9^1 = 9$
- `153`: 3-digit → $1^3+5^3+3^3=153$
- `1634`: 4-digit → $1^4+6^4+3^4+4^4=1634$ ([read.learnyard.com][2])

---

## 🧠 Intuition

To check if `n` is Armstrong:

1. Count digits: let that be `k`.
2. Extract each digit.
3. Compute sum of each digit^`k`.
4. If sum equals original `n`, it's an Armstrong number.

---

### 📊 Visual Steps (Example: n = 153)

```
153 → digits count k = 3
Extract and raise:
  3^3 = 27
  5^3 = 125
  1^3 = 1
Sum = 27 + 125 + 1 = 153 → Armstrong!
```

---

## 🧑‍💻 JavaScript Code: Standard Method

```javascript
function isArmstrong(number) {
  const digits = number.toString().split("");
  const k = digits.length;
  let sum = 0;

  for (let d of digits) {
    sum += Math.pow(parseInt(d), k);
  }

  return sum === number;
}

// Tests:
console.log(isArmstrong(9)); // true
console.log(isArmstrong(153)); // true
console.log(isArmstrong(154)); // false
console.log(isArmstrong(1634)); // true
```

This uses string conversion and looping. ([read.learnyard.com][2], [w3resource.com][3])

---

## ⏱️ Alternative: Pure Math Approach

```javascript
function isArmstrongMath(number) {
  let temp = number;
  const k = number.toString().length;
  let sum = 0;

  while (temp > 0) {
    let digit = temp % 10;
    sum += Math.pow(digit, k);
    temp = Math.floor(temp / 10);
  }

  return sum === number;
}
```

This avoids strings and works using loops and math. ([geeksforgeeks.org][4])

---

## 📚 Complexity

| Step                   | Time Complexity | Notes                             |
| ---------------------- | --------------- | --------------------------------- |
| Counting digits (k)    | O(log₁₀ n)      | Number of digits                  |
| Summing k digit-powers | O(k)            | Each iteration does digit work    |
| **Total**              | **O(log n)**    | Effective for very large integers |

Memory is **O(1)** beyond the input.

---

## 📎 Edge Cases

- **Single-digit** numbers (`0–9`) always qualify.
- Works for numbers with any digit count (3+, 4+, etc.).
- Input `0` → `0^1 = 0`, so considered Armstrong.
- Leading zeros don't affect (e.g., `010` is `10`, not a palindrome concept here).

---

# 📘 Print All Divisors of a Number

## 🧠 What is a Divisor?

A number **`d`** is a **divisor** of `n` if:

> `n % d === 0`
> (i.e., it divides `n` exactly with no remainder)

### 🔍 Example:

For `n = 12`, the divisors are:
**1, 2, 3, 4, 6, 12**

---

## ✅ Approach 1: Brute Force (From 1 to n)

### 💡 Intuition:

- Loop from `1` to `n`
- If `n % i == 0`, then `i` is a divisor

### 🧑‍💻 JavaScript Code:

```javascript
function printDivisors(n) {
  for (let i = 1; i <= n; i++) {
    if (n % i === 0) {
      console.log(i);
    }
  }
}

printDivisors(12); // Output: 1 2 3 4 6 12
```

### ⏱️ Time Complexity: `O(n)`

Good for small values of `n`.

---

## ✅ Approach 2: Optimized – Loop from 1 to √n

### 💡 Intuition:

- Divisors come in **pairs**:
  If `i` divides `n`, then `n / i` is also a divisor.
- Loop only up to `√n`, and print both `i` and `n / i`.

---

### 🔄 Diagram for n = 36:

```
i     | 36 % i | Output
------|--------|--------
1     | 0      | 1, 36
2     | 0      | 2, 18
3     | 0      | 3, 12
4     | 0      | 4, 9
6     | 0      | 6     (only once, because 6*6 = 36)
```

---

### 🧑‍💻 JavaScript Code:

```javascript
function printDivisorsOptimized(n) {
  for (let i = 1; i * i <= n; i++) {
    if (n % i === 0) {
      console.log(i);
      if (i !== n / i) {
        console.log(n / i); // Paired divisor
      }
    }
  }
}

printDivisorsOptimized(36);
// Output (unordered): 1 36 2 18 3 12 4 9 6
```

---

### ✅ Optional: Sorted Output

To print in **ascending order**, collect and sort:

```javascript
function getSortedDivisors(n) {
  const small = [];
  const large = [];

  for (let i = 1; i * i <= n; i++) {
    if (n % i === 0) {
      small.push(i);
      if (i !== n / i) large.push(n / i);
    }
  }

  return small.concat(large.reverse());
}

console.log(getSortedDivisors(36)); // [1, 2, 3, 4, 6, 9, 12, 18, 36]
```

---

## 📚 Summary

| Approach        | Time Complexity | Space | Notes                       |
| --------------- | --------------- | ----- | --------------------------- |
| Brute Force     | O(n)            | O(1)  | Simple but slow for large n |
| Optimized √n    | O(√n)           | O(1)  | Fast for large values       |
| Sorted Divisors | O(√n + k log k) | O(k)  | Slightly more for sorting   |

---

# 🔍 Check if a Number is Prime

## 🧠 What is a Prime Number?

A number **`n`** is called **prime** if:

- `n > 1`, and
- The only positive divisors of `n` are `1` and `n` itself.

---

### ✅ Examples:

- **Prime**: 2, 3, 5, 7, 11, 13, 17...
- **Not Prime**: 1 (only 1 divisor), 4 (divisible by 2), 9 (divisible by 3)

---

## ✅ Approach 1: Brute Force (Check 1 to n)

### 💡 Intuition:

- Count how many numbers divide `n`
- If more than 2 divisors, it's not prime

### ❌ Not efficient for large numbers

---

## ✅ Approach 2: Efficient – Loop from 2 to √n

### 💡 Why √n?

If a number `n` is **not prime**, it must have a factor less than or equal to `√n`.
For example:

- 36 = 6 × 6 → only need to check up to 6

---

### 🧑‍💻 JavaScript Code (Efficient):

```javascript
function isPrime(n) {
  if (n <= 1) return false; // 0 and 1 are not prime
  if (n === 2) return true; // 2 is prime
  if (n % 2 === 0) return false; // Even numbers > 2 are not prime

  for (let i = 3; i * i <= n; i += 2) {
    if (n % i === 0) return false;
  }
  return true;
}

// Test cases
console.log(isPrime(1)); // false
console.log(isPrime(2)); // true
console.log(isPrime(19)); // true
console.log(isPrime(100)); // false
```

---

## 📎 Edge Cases

| Input | Output | Reason                          |
| ----- | ------ | ------------------------------- |
| 1     | false  | Only one divisor                |
| 2     | true   | First and smallest prime number |
| 0     | false  | Not considered prime            |
| -5    | false  | Only positive integers > 1      |

---

## 📚 Summary

| Step                 | Time Complexity | Notes                       |
| -------------------- | --------------- | --------------------------- |
| Brute Force (1 to n) | O(n)            | Slow for large `n`          |
| Optimized (1 to √n)  | O(√n)           | Best for checking large `n` |

---

# 🔢 **Sieve of Eratosthenes – Find All Primes from 1 to n**

## 🧠 Problem Statement:

**Given an integer `n`, return all prime numbers from `1` to `n`.**

---

## 🔍 Example:

- Input: `n = 10`
- Output: `[2, 3, 5, 7]`
  (Because these are the only prime numbers between 1 and 10)

---

## ✅ Approach: Sieve of Eratosthenes

---

## 💡 Intuition:

- A **prime number** is only divisible by **1 and itself**.
- Instead of checking each number one by one (slow!), we **mark multiples of primes as non-prime**.
- Efficiently eliminates all non-primes in a range using a **boolean array**.

---

## 🧠 Core Idea:

1. Create a boolean array `isPrime[]` of size `n+1` and initialize all values as `true`.
2. Set `isPrime[0]` and `isPrime[1]` to `false` (0 and 1 are not prime).
3. Start from `2` and iterate till `√n`:

   - If `isPrime[i]` is `true`, mark **all multiples of `i`** as `false`.

4. At the end, the indices where `isPrime[i]` is still `true` are primes.

---

## 🔄 Diagram (n = 10):

```
Initial:  [F, F, T, T, T, T, T, T, T, T, T]
Index:     0  1  2  3  4  5  6  7  8  9 10

Step i=2: Mark 4,6,8,10 -> [F, F, T, T, F, T, F, T, F, T, F]
Step i=3: Mark 6,9     -> [F, F, T, T, F, T, F, T, F, F, F]

Primes: Indices with `true` = [2, 3, 5, 7]
```

---

## 🧑‍💻 JavaScript Code:

```javascript
function sieveOfEratosthenes(n) {
  const isPrime = new Array(n + 1).fill(true);
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

console.log(sieveOfEratosthenes(10)); // Output: [2, 3, 5, 7]
```

---

## 📚 Summary Table:

| Concept               | Technique                | Time Complexity  | Space Complexity |
| --------------------- | ------------------------ | ---------------- | ---------------- |
| Sieve of Eratosthenes | Mark multiples of primes | `O(n log log n)` | `O(n)`           |

---

## 📌 Notes for Beginners:

- Marking from `i * i` instead of `2 * i` improves performance.
- Use `i * i <= n` to limit the outer loop, since larger factors would’ve already been marked.
- This is much faster than checking primality one-by-one up to `n`.

---

# 🔢 **Segmented Sieve – Find Primes Between M and N (Large Range)**

### 🧠 Problem Statement:

**Given two integers `M` and `N` such that `1 ≤ M ≤ N ≤ 10^14` and `N - M ≤ 10^6`, find all prime numbers in the range `[M, N]`.**

---

### 💡 Why Normal Sieve Fails?

- Regular sieve requires memory of size `N`, which is not feasible when `N = 10^14`.
- But since the gap `N - M` is small, we can use a **Segmented Sieve** to sieve only this small segment.

---

## ✅ Intuition:

1. First, **generate all primes up to √N** using normal **Sieve of Eratosthenes**.
2. Create a boolean array of size `(N - M + 1)` initialized to `true` (assume all are prime).
3. For each prime `p` ≤ √N:

   - Mark **multiples of `p` in the range \[M, N]** as non-prime.

4. The remaining `true` values in the segment represent **prime numbers in `[M, N]`**.

---

## 🔄 Step-by-step Example (M = 22, N = 29):

1. √29 = 5.3 ⇒ Sieve primes up to 5 → \[2, 3, 5]
2. Create segment: `isPrimeSegment[22..29]` → size = 8, all `true`
3. For each prime `p`, mark multiples:

   - p = 2 → mark 22, 24, 26, 28
   - p = 3 → mark 24, 27
   - p = 5 → mark 25

4. Remaining unmarked: \[23, 29] → ✅ primes in \[22, 29]

---

## 🧑‍💻 JavaScript Code

```javascript
function sieve(limit) {
  const isPrime = new Array(limit + 1).fill(true);
  isPrime[0] = isPrime[1] = false;

  for (let i = 2; i * i <= limit; i++) {
    if (isPrime[i]) {
      for (let j = i * i; j <= limit; j += i) {
        isPrime[j] = false;
      }
    }
  }

  const primes = [];
  for (let i = 2; i <= limit; i++) {
    if (isPrime[i]) primes.push(i);
  }
  return primes;
}

function segmentedSieve(M, N) {
  const limit = Math.floor(Math.sqrt(N));
  const primes = sieve(limit);

  const isPrimeSegment = new Array(N - M + 1).fill(true);

  for (const p of primes) {
    // Find the first multiple of p in [M, N]
    let start = Math.max(p * p, Math.ceil(M / p) * p);

    for (let j = start; j <= N; j += p) {
      isPrimeSegment[j - M] = false;
    }
  }

  if (M === 1) isPrimeSegment[0] = false;

  const result = [];
  for (let i = 0; i < isPrimeSegment.length; i++) {
    if (isPrimeSegment[i]) {
      result.push(M + i);
    }
  }

  return result;
}

// Example usage:
console.log(segmentedSieve(10 ** 14, 10 ** 14 + 50));
```

---

## 📚 Summary Table:

| Concept         | Technique                            | Time Complexity            | Space Complexity |
| --------------- | ------------------------------------ | -------------------------- | ---------------- |
| Segmented Sieve | Sieve up to √N, then mark in \[M, N] | `O(√N + (N−M) log log √N)` | `O(√N + N−M)`    |

---

## 📌 Notes for Beginners:

- `Math.max(p * p, ceil(M / p) * p)` ensures we start marking in `[M, N]`.
- Use regular sieve only up to `√N` which is small even for `N = 10^14` (i.e., up to `10^7`).
- The segment size is small (`≤ 10^6`), so this method is fast and memory-efficient.

---
