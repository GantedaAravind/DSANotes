## 📚 **7. Number of Distinct Substrings in a String (Using Trie)**

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
