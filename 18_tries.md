## 📘 **What is a Trie?**

A **Trie** (pronounced _"try"_) is a **tree-like data structure** that is used to **store and manage a dynamic set of strings**, especially when they share common prefixes.

It is commonly known as a:

- **Prefix Tree**, because it stores words based on their prefixes.
- **Digital Tree**, because it's often used to store sequences like digits or characters.

---

## ✨ **Why Use a Trie?**

Trie is designed to make **searching for strings very fast**, especially when you want to:

- **Insert words**
- **Search for full words**
- **Check if a prefix exists**

Unlike a HashMap or Set, a Trie takes advantage of **shared prefixes** to save space and optimize performance in some cases.

---

## 🧠 **How Does It Work?**

- Imagine a tree where:

  - Each node represents a **character**.
  - Paths from the root to a node represent **prefixes** of words.
  - A **word ends** when a node is marked as the **end of word**.

### Example:

Let’s say we store these words:
`["bat", "ball", "bake"]`

The Trie would branch like this:

```
        (root)
          |
          b
          |
          a
       /     \
      t      k
     |        \
    [end]     e
              |
             [end]
```

- "bat" and "ball" share `"ba"`.
- "bake" also shares `"ba"` but then goes a different direction.

---

## 🧩 **Key Features of a Trie**

- **Prefix Sharing**: Words with common prefixes share memory space.
- **Fast Prefix Search**: Ideal for autocomplete or dictionary-like applications.
- **Dynamic Size**: You can insert or delete words at any time.
- **Character-by-Character Navigation**: Makes certain string problems easier to solve.

---

## 🔍 **What Makes It Different from Other Data Structures?**

- Tries are optimized for **string operations**.
- Unlike arrays or hash maps, Tries **don’t store whole words directly**. Instead, they store **characters as paths**.
- They use **less space when words share prefixes** but can use more space if not carefully optimized.

---

## 🌳 **1. Trie (Prefix Tree)**

### 📘 **Problem Statement**

A **Trie** (pronounced as "try") or **prefix tree** is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

- `Trie()` Initializes the trie object.
- `insert(word)`: Inserts a word into the Trie.
- `search(word)`: Returns `true` if the word is in the Trie.
- `startsWith(prefix)`: Returns `true` if there is any word in the Trie that starts with the given prefix.

---

### 🧪 **Test Cases**

**Test Case 1:**

```javascript
insert("apple");
search("apple"); // true
search("app"); // false
startsWith("app"); // true
insert("app");
search("app"); // true
```

**Test Case 2:**

```javascript
insert("cat");
insert("cap");
insert("can");
search("can"); // true
startsWith("ca"); // true
startsWith("cab"); // false
```

---

### 💡 **Intuition**

A Trie is a **tree-like structure** where:

- Each node represents a **character**.
- Paths down the tree represent **prefixes**.
- Nodes are marked if they represent the **end of a complete word**.

### 🌲 **Trie Structure (Visual)**

Words: `"cat"`, `"can"`, `"cap"`

```
        root
         |
         c
         |
         a
       / | \
      t  n  p
```

---

### ✅ **JavaScript Implementation**

```javascript
class TrieNode {
  constructor() {
    this.children = {}; // Maps character → TrieNode
    this.isEndOfWord = false; // True if a word ends at this node
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }

  insert(word) {
    let node = this.root;
    for (let ch of word) {
      if (!node.children[ch]) {
        node.children[ch] = new TrieNode();
      }
      node = node.children[ch];
    }
    node.isEndOfWord = true;
  }

  search(word) {
    let node = this.root;
    for (let ch of word) {
      if (!node.children[ch]) return false;
      node = node.children[ch];
    }
    return node.isEndOfWord;
  }

  startsWith(prefix) {
    let node = this.root;
    for (let ch of prefix) {
      if (!node.children[ch]) return false;
      node = node.children[ch];
    }
    return true;
  }
}
```

---

### ⏱ **Time and Space Complexity**

| Operation      | Time Complexity | Space Complexity |
| -------------- | --------------- | ---------------- |
| `insert(word)` | O(L)            | O(L) per word    |
| `search(word)` | O(L)            | O(1) extra       |
| `startsWith()` | O(L)            | O(1) extra       |

- `L` = Length of the word or prefix
- Space depends on number of words and shared prefixes

---

### 📌 **Summary Table**

| Step         | Purpose                    |
| ------------ | -------------------------- |
| Create Node  | Store character and status |
| Insert Word  | Add each char to tree      |
| Search Word  | Follow path, check ending  |
| Prefix Check | Follow path, no end check  |

---

## 🌳 **2. Extended Trie with Word Count and Erase**

### 📘 **Problem Statement**

Design a Trie with the following features:

- `insert("word")`: Insert the word into the Trie.
- `countWordsEqualTo("word")`: Return how many times the exact word exists in the Trie.
- `countWordsStartingWith("prefix")`: Return how many words start with the given prefix.
- `erase("word")`: Delete one occurrence of the word from the Trie (if present).

---

### 🧪 **Test Cases**

#### ✅ Test Case 1:

```javascript
Input: [
  "Trie",
  "insert",
  "countWordsEqualTo",
  "insert",
  "countWordsStartingWith",
  "erase",
  "countWordsStartingWith",
][([], ["apple"], ["apple"], ["app"], ["app"], ["apple"], ["app"])];

Output: [null, null, 1, null, 2, null, 1];
```

#### ✅ Test Case 2:

```javascript
Input: [
  "Trie",
  "insert",
  "countWordsEqualTo",
  "insert",
  "erase",
  "countWordsStartingWith",
][([], ["mango"], ["apple"], ["app"], ["app"], ["mango"])];

Output: [null, null, 0, null, null, 1];
```

---

### 💡 **Intuition**

We enhance the Trie by tracking:

- `countEnd`: Number of times a word ends at this node.
- `countPrefix`: Number of words that pass through this node (prefix count).

When inserting a word:

- Increment `countPrefix` at each node.
- Increment `countEnd` at the last node.

When erasing:

- Decrement both `countPrefix` and `countEnd` appropriately (only if word exists).

---

### 🌲 **Trie Structure (Conceptual)**

Each node contains:

- `children`: Map of characters to child nodes.
- `countEnd`: Number of times a word ends at this node.
- `countPrefix`: Number of words sharing this prefix (including the word itself).

---

### ✅ **JavaScript Implementation**

```javascript
class TrieNode {
  constructor() {
    this.children = {};
    this.countEnd = 0; // Number of times a word ends here
    this.countPrefix = 0; // Number of words with this prefix
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }

  insert(word) {
    let node = this.root;
    for (let ch of word) {
      if (!node.children[ch]) {
        node.children[ch] = new TrieNode();
      }
      node = node.children[ch];
      node.countPrefix += 1;
    }
    node.countEnd += 1;
  }

  countWordsEqualTo(word) {
    let node = this.root;
    for (let ch of word) {
      if (!node.children[ch]) return 0;
      node = node.children[ch];
    }
    return node.countEnd;
  }

  countWordsStartingWith(prefix) {
    let node = this.root;
    for (let ch of prefix) {
      if (!node.children[ch]) return 0;
      node = node.children[ch];
    }
    return node.countPrefix;
  }

  erase(word) {
    if (this.countWordsEqualTo(word) === 0) return; // Word doesn't exist

    let node = this.root;
    for (let ch of word) {
      node = node.children[ch];
      node.countPrefix -= 1;
    }
    node.countEnd -= 1;
  }
}
```

---

### ⏱ **Time and Space Complexity**

| Operation                  | Time Complexity | Space Complexity |
| -------------------------- | --------------- | ---------------- |
| `insert(word)`             | O(L)            | O(L)             |
| `countWordsEqualTo()`      | O(L)            | O(1)             |
| `countWordsStartingWith()` | O(L)            | O(1)             |
| `erase(word)`              | O(L)            | O(1)             |

- `L` = Length of the word or prefix

---

### 💬 Summary

| Feature            | Extended Trie                            |
| ------------------ | ---------------------------------------- |
| Supports Count Ops | Yes                                      |
| Supports Erase     | Yes                                      |
| Time per Op        | O(L)                                     |
| Use Case           | Prefix matching, word tracking, deletion |

---

## 🔠 **3. Longest String with All Prefixes Present in a List**

### 📘 **Problem Statement**

You are given an array of strings. Your task is to find the **longest string** such that **all of its prefixes** are also present in the array.

- If there are **multiple answers**, return the **lexicographically smallest** one.
- If no such string exists, return an **empty string**.

---

### 🧪 **Test Cases**

**Test Case 1:**

```javascript
Input: ["a", "ap", "app", "appl", "apple", "apply"];
Output: "apple";
```

**Test Case 2:**

```javascript
Input: ["a", "ar", "art", "arti", "artic", "articl", "article"];
Output: "article";
```

**Test Case 3:**

```javascript
Input: ["a", "b", "ba", "bac", "baca"];
Output: "baca";
```

**Test Case 4:**

```javascript
Input: ["ab", "abc"];
Output: "";
```

**Test Case 5:**

```javascript
Input: ["x", "xy", "xyz", "xyza", "x"];
Output: "xyz";
```

---

### 💡 **Intuition**

To find the longest valid string:

- We need to **check all prefixes of each string**.
- Only consider strings where **every prefix** (like "a", "ap", "app", ...) is also present.
- We can use a **Trie** or a **Set** to efficiently check prefix existence.
- Maintain the **longest** string seen, and if two are of same length, choose the **lexicographically smaller** one.

---

### ✅ **JavaScript Implementation using Trie**

```javascript
class TrieNode {
  constructor() {
    this.children = {};
    this.isEnd = false;
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }

  insert(word) {
    let node = this.root;
    for (let ch of word) {
      if (!node.children[ch]) {
        node.children[ch] = new TrieNode();
      }
      node = node.children[ch];
    }
    node.isEnd = true;
  }

  // Check if all prefixes of this word are marked as end
  allPrefixesExist(word) {
    let node = this.root;
    for (let ch of word) {
      if (!node.children[ch]) return false;
      node = node.children[ch];
      if (!node.isEnd) return false;
    }
    return true;
  }
}

function longestStringWithAllPrefixes(words) {
  const trie = new Trie();

  for (let word of words) {
    trie.insert(word);
  }

  let answer = "";

  for (let word of words) {
    if (trie.allPrefixesExist(word)) {
      if (
        word.length > answer.length ||
        (word.length === answer.length && word < answer)
      ) {
        answer = word;
      }
    }
  }

  return answer;
}
```

---

### ⏱ **Time and Space Complexity**

| Measure | Complexity |
| ------- | ---------- |
| Time    | `O(N * L)` |
| Space   | `O(N * L)` |

Where:

- `N` = Number of words
- `L` = Average length of each word

---

### 📌 **Summary**

| Step               | Description                                    |
| ------------------ | ---------------------------------------------- |
| Use Set            | Fast lookup of prefixes                        |
| Check all prefixes | For each word, validate prefix existence       |
| Track best answer  | Update based on length and lexicographic order |

---

## 📚 **4. Number of Distinct Substrings in a String (Using Trie)**

### 📘 **Problem Statement**

Given a string `s`, count the **number of distinct substrings** in it (including the empty string `""`).

- Substrings are contiguous characters of `s`.
- Return the count of **unique** substrings.

---

### 🧪 **Test Cases**

**Test Case 1:**

```javascript
Input: "ab"
Output: 3
Explanation:
Substrings: "", "a", "b", "ab"
3 unique non-empty substrings: "a", "b", "ab"
+ 1 empty string → Total = 4
```

**Test Case 2:**

```javascript
Input: "aaa"
Output: 4
Explanation:
Substrings: "", "a", "aa", "aaa"
Only "a", "aa", "aaa" are distinct.
+ 1 empty string → Total = 4
```

---

### 💡 **Intuition**

- Every **suffix** of a string generates all its substrings when inserted into a **Trie**.
- Each **new node** in the Trie represents a **new unique substring**.
- Count the total number of nodes inserted into the Trie (excluding the root), and **add 1 for the empty string**.

---

### 🌲 **Trie Visualization**

For `"ab"`:

- Insert `"ab"`, generates: `a → b`
- Insert `"b"`, generates: `b`

Total distinct substrings = number of nodes (3) + 1 (for `""`) = 4

---

### ✅ **JavaScript Implementation**

```javascript
class TrieNode {
  constructor() {
    this.children = {};
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
    this.count = 0; // count of distinct substrings (nodes created)
  }

  insert(s) {
    let node = this.root;
    for (let ch of s) {
      if (!node.children[ch]) {
        node.children[ch] = new TrieNode();
        this.count++; // New node → new substring
      }
      node = node.children[ch];
    }
  }
}

function countDistinctSubstrings(s) {
  const trie = new Trie();

  for (let i = 0; i < s.length; i++) {
    trie.insert(s.substring(i)); // Insert all suffixes
  }

  return trie.count + 1; // +1 for empty string
}
```

---

### ⏱ **Time & Space Complexity**

| Metric | Complexity                 |
| ------ | -------------------------- |
| Time   | O(n²)                      |
| Space  | O(n²) (for all substrings) |

Where `n = s.length`

---

### 📌 **Summary Table**

| Step                | Explanation                          |
| ------------------- | ------------------------------------ |
| Insert all suffixes | Covers all substrings in the Trie    |
| Count new nodes     | Each new node = new unique substring |
| Add empty string    | Count + 1 to include `""`            |

---

### 🔎 **Space Complexity**

You are given a **single string `s` of length `n`**, and you want to **store all distinct substrings** of `s`.

---

### 1️⃣ **Using HashSet**

#### 🎯 Strategy:

- Generate **all substrings** and insert each into a **HashSet** to avoid duplicates.

#### 🔢 Number of substrings:

There are approximately `O(n²)` substrings:

- Each substring `s[i..j]` where `0 ≤ i ≤ j < n`
- Total = `n(n + 1)/2`

#### 🧠 Space Complexity:

Each substring is stored **as a separate string** of up to `O(n)` length (on average ≈ `n/2`)

So total space:

```
O(n²) substrings × O(n) space each (in worst case) = O(n³)
```

> 📌 **HashSet worst-case space = O(n³)**
> (if strings are stored as separate copies and no prefix reuse)

---

### 2️⃣ **Using Trie**

#### 🎯 Strategy:

- Insert every suffix of the string into the Trie.
- Each path in the Trie implicitly encodes all substrings that start at that suffix.

#### 🔢 Number of nodes:

- Total characters inserted = all suffix substrings:

  - `"abc"` → insert `"abc"`, `"bc"`, `"c"` = `n + (n - 1) + ... + 1 = O(n²)`

- But **shared prefixes** are reused — so total number of Trie nodes ≤ `n(n + 1)/2`

#### 🧠 Space Complexity:

Each **unique character in each unique path** is stored as a node (shared where possible), so:

```
Worst-case = O(n²) nodes (1 per unique substring char)
Each node has: character + pointer map (constant)
```

> 📌 **Trie space = O(n²)**

---

## ⚡ **5. Maximum XOR With an Element From an Array (Using Trie)**

### 📘 **Problem Statement**

You are given:

- An array of positive integers `arr`
- A number `num`

Your task is to return the **maximum value of `num ^ arr[i]`** for any element `arr[i]` in the array.

---

### 🧪 **Test Cases**

**Test Case 1:**

```javascript
Input: arr = [3, 10, 5, 25, 2, 8], num = 5
Output: 28
Explanation: 5 ^ 25 = 28 is the maximum.
```

**Test Case 2:**

```javascript
Input: arr = [0, 1, 2, 3, 4], num = 1
Output: 5
Explanation: 1 ^ 4 = 5
```

**Test Case 3:**

```javascript
Input: arr = [7, 8, 2, 5], num = 6
Output: 15
Explanation: 6 ^ 9 = 15 (after padding to 32-bit and maximizing bit by bit)
```

---

### 💡 **Intuition**

To get the **maximum XOR**, we want to **maximize the difference in bits**:

- At each bit (starting from MSB), we prefer choosing the **opposite bit** of the current bit in `num`.

A **Trie (Prefix Tree)** is built using the **binary representation** of each number in the array (usually padded to 32 bits).

While querying, we traverse the Trie to choose the **complement bit if available**, maximizing the XOR.

---

### ✅ **JavaScript Implementation**

```javascript
class TrieNode {
  constructor() {
    this.links = {}; // {0: TrieNode, 1: TrieNode}
  }

  has(bit) {
    return bit in this.links;
  }

  get(bit) {
    return this.links[bit];
  }

  put(bit, node) {
    this.links[bit] = node;
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }

  insert(num) {
    let node = this.root;
    for (let i = 31; i >= 0; i--) {
      let bit = (num >> i) & 1;
      if (!node.has(bit)) {
        node.put(bit, new TrieNode());
      }
      node = node.get(bit);
    }
  }

  maxXor(num) {
    let node = this.root;
    let maxNum = 0;

    for (let i = 31; i >= 0; i--) {
      let bit = (num >> i) & 1;
      let opp = 1 - bit; // complement

      if (node.has(opp)) {
        maxNum |= 1 << i; // set bit i to 1
        node = node.get(opp);
      } else {
        node = node.get(bit);
      }
    }

    return maxNum;
  }
}

function findMaximumXOR(arr, num) {
  const trie = new Trie();
  for (let val of arr) {
    trie.insert(val);
  }

  return trie.maxXor(num);
}
```

---

### 🔍 Example Dry Run

Input: `arr = [3, 10, 5, 25, 2, 8], num = 5`

- Binary of 5: `00000000000000000000000000000101`
- Insert all `arr[i]` in Trie
- Traverse Trie to pick opposite bits:

  - `5 ^ 25 = 28` → highest possible

---

### ⏱ **Time and Space Complexity**

| Measure | Complexity |
| ------- | ---------- |
| Insert  | O(32 × n)  |
| Query   | O(32)      |
| Space   | O(32 × n)  |

Since we're dealing with 32-bit integers, operations are constant per bit (32 bits max).

---

### 📌 **Summary Table**

| Step              | Description                               |
| ----------------- | ----------------------------------------- |
| Insert Numbers    | Add binary of each array number into Trie |
| XOR Query         | For each bit, pick opposite if possible   |
| Use 32-bit Format | Ensures uniform traversal depth in Trie   |

---

## ⚡ **6. Maximum XOR of Two Numbers in an Array (Trie Approach)**

### 📘 **Problem Statement**

Given an array of integers `nums`, return the **maximum XOR value** of any two elements:

```text
Return max(nums[i] ^ nums[j]) for all 0 ≤ i < j < n
```

---

### 🧪 **Test Cases**

**Test Case 1:**

```javascript
Input: nums = [3,10,5,25,2,8]
Output: 28
Explanation: 5 ^ 25 = 28
```

**Test Case 2:**

```javascript
Input: nums = [14, 70, 53, 83, 49, 91, 36, 80, 92, 51, 66, 70];
Output: 127;
```

---

### 💡 **Intuition**

To find the **maximum XOR**, we want to maximize differing bits in higher positions.

We:

1. **Insert numbers into a Trie**, where each path from root to leaf represents the **32-bit binary** of a number.
2. For each number:

   - Traverse the Trie to find the **best complementary number** (greedy match with opposite bits) to maximize XOR.

---

### ✅ **JavaScript Implementation (Trie Based)**

```javascript
class TrieNode {
  constructor() {
    this.children = {};
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }

  insert(num) {
    let node = this.root;
    for (let i = 31; i >= 0; i--) {
      let bit = (num >> i) & 1;
      if (!node.children[bit]) {
        node.children[bit] = new TrieNode();
      }
      node = node.children[bit];
    }
  }

  getMaxXor(num) {
    let node = this.root;
    let maxXor = 0;

    for (let i = 31; i >= 0; i--) {
      let bit = (num >> i) & 1;
      let toggled = 1 - bit;
      if (node.children[toggled]) {
        maxXor |= 1 << i;
        node = node.children[toggled];
      } else {
        node = node.children[bit];
      }
    }

    return maxXor;
  }
}

function findMaximumXOR(nums) {
  const trie = new Trie();
  let maxXor = 0;

  // Insert first number
  trie.insert(nums[0]);

  for (let i = 1; i < nums.length; i++) {
    // Get max XOR for nums[i] with any number already in Trie
    maxXor = Math.max(maxXor, trie.getMaxXor(nums[i]));

    // Insert current number into Trie
    trie.insert(nums[i]);
  }

  return maxXor;
}
```

---

### ⏱ **Time and Space Complexity**

| Measure | Complexity       |
| ------- | ---------------- |
| Time    | O(n × 32) = O(n) |
| Space   | O(n × 32) = O(n) |

- `n` is number of elements in `nums`
- 32 = fixed number of bits for 32-bit integers

---

### 📌 **Summary Table**

| Step           | Explanation                                |
| -------------- | ------------------------------------------ |
| Insert in Trie | Store each number's binary in a Trie       |
| XOR Query      | Traverse Trie greedily using opposite bits |
| Max XOR        | Track highest XOR seen while processing    |

---
