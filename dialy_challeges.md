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

## 🧮 **5. K-th Character After Sequence of Copy and Transform Operations**

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
