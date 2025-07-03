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
