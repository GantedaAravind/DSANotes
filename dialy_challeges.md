## 🔁 ** Kth Character After Infinite Operations**

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
