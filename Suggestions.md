### ✅ **Sorting Algorithms**

- **Merge Sort**: Use when stable sort is needed; works well on linked lists or large datasets.
- **Quick Sort**: Fast average case; good for in-memory arrays, avoid for worst-case unless randomized.
- **Heap Sort**: Use when constant space is needed and stability is not important.
- **Counting/Radix Sort**: Use for integers with limited range.

---

### ✅ **Sorted Arrays**

- **Binary Search**: Use on sorted arrays to reduce time to `O(log n)`.

- When to Use Binary Search on Answers find the **optimal answer (min/max)** when the **search space is numeric and monotonic** (either increasing or decreasing behavior).

---

### ✅ **Precomputation Techniques**

> Use when you want **constant-time lookups** after preprocessing.

- `Prefix Sum` : subarray sum: `O(1)` queries after `O(n)` prep.

- `Suffix Sum`
  : Sum from index `i` to end in `O(1)`.

- `Prefix Max / Min` : Track max/min up to index `i`.

- `Suffix Max / Min` : Track max/min from index `i` to end.

- `Prefix XOR`: Subarray XOR: `prefix[r] ^ prefix[l-1]`.

- `Difference Array` : Efficient range updates. Finalize with prefix sum.

- `Cumulative Frequency`: Count ≤ x in `O(1)` using prefix freq array.

- `Hash Map Frequency`: Track element counts in `O(1)`.

- `Sparse Table` : Fast static range min/max. `O(1)` query, no updates.

- `Prefix Product (Log)`: Subarray product via logs: `sum(logs)` → exp.

### ✅ **Hashing (HashMap / HashSet)**

- Use when fast insert, delete, and search (`O(1)` avg) is needed.
- Best for frequency maps, lookups, avoiding duplicates.

---

### ✅ **Heap (Priority Queue)**

- Use for top `k` problems (`n log k` instead of `n log n`).
- **Min-Heap**: For **k largest** elements.
- **Max-Heap**: For **k smallest** elements.
- Use in Dijkstra’s, Huffman coding, or scheduling tasks.

---

### ✅ **Two Pointers / Sliding Window**

- Use for subarray/substring problems (e.g., max sum, longest window).
- Efficient in reducing nested loops to `O(n)`.

---

### ✅ **Greedy**

- Use when local optimal choices lead to global optimal (e.g., activity selection, Huffman coding).
- Usually simpler and faster if applicable.

---

### ✅ **Recursion & Backtracking**

- There are multiple ways
- Use for exhaustive search in combinations, permutations, N-Queens, Sudoku.
- Backtracking = recursion with pruning.

---

### ✅ **Divide and Conquer**

- Use to break problem into subproblems: merge sort, quick sort, binary search.
- Efficient for large input sizes.

---

### ✅ **Dynamic Programming (DP)**

- Use when problem has **overlapping subproblems + optimal substructure**.
- Good for: Knapsack, DP on strings, LIS, LCS, etc.
- Use memoization (`top-down`) or tabulation (`bottom-up`).

---

### ✅ **Graphs**

- **DFS/BFS**: Traversal, connected components, shortest paths (unweighted).
- **Dijkstra’s**: Shortest path in weighted graphs with non-negative weights.
- **Bellman-Ford**: Shortest path with negative weights.
- **Floyd-Warshall**: All-pairs shortest paths.
- **Union-Find (DSU)**: Cycle detection, Kruskal’s MST, disjoint sets.

---

### ✅ **Trie**

- Use for prefix-based searching: dictionary, autocomplete, bitwise problems (XOR).
- Efficient for string sets or IP routing.

---

### ✅ **Segment Tree / Binary Indexed Tree (Fenwick Tree)**

- Use for **range queries** and **updates** (sum, min, max) in `O(log n)` time.
- Segment Tree: More flexible, supports complex operations.
- Fenwick Tree: More space-efficient for cumulative frequency.

---

### ✅ **Linked List**

- Use when frequent insert/delete from middle or ends are needed.
- Doubly linked list for LRU Cache.
- Use for dynamic memory when size is not known in advance.

---

### ✅ **Stack**

- Use for expression evaluation, backtracking, or tracking state (e.g., parentheses validation, histogram).
- Supports LIFO operations.

---

### ✅ **Queue / Deque**

- Queue: BFS, task scheduling (FIFO).
- Deque: Sliding window max/min, LRU cache.

---

### 🔹 **If it's an optimization problem:**

- Use **Greedy** if:

  - Making the best choice at each step leads to the best overall solution.
  - No need to check all combinations.

- Use **Dynamic Programming (DP)** if:

  - Choices depend on previous results.
  - Problem has overlapping subproblems and needs memory to avoid recomputation.

👉 **Try Greedy first** — if it fails, use **DP**.

## ✅ **Golden Rule of Thumb**

> **1 second ≈ 10⁷ to 10⁸ operations** is safe in most online judges (like LeetCode).

This lets you **estimate which time complexity is safe**, based on input size.

---

### 🧮 Reference Table (Input Size vs Time Complexity)

| Max Input Size (`n`) | Safe Time Complexity          | Unsafe / TLE Risk  |
| -------------------- | ----------------------------- | ------------------ |
| ≤ 10                 | O(n!), O(2ⁿ), O(n³)           | —                  |
| ≤ 20                 | O(2ⁿ), O(n!)                  | —                  |
| ≤ 100                | ✅ O(n²)                      | ⚠️ O(n³), O(2ⁿ)    |
| ≤ 1,000              | ✅ O(n²)                      | ⚠️ O(n³)           |
| ≤ 10⁴                | ✅ O(n·log n), O(n²) (barely) | ⚠️ O(n²) may TLE   |
| ≤ 10⁵                | ✅ O(n·log n), O(n)           | ❌ O(n²) will TLE  |
| ≤ 10⁶                | ✅ O(n), O(n·log n)           | ❌ O(n²), O(n¹․⁵)  |
| ≤ 10⁷ or more        | ✅ O(n) only (linear)         | ❌ Anything slower |

---

### 🚦 How to Use This?

#### Step 1: Read the constraints.

For example:

```txt
1 <= nums.length <= 10⁵
```

That tells you:

- **n is up to 10⁵**, so
- You **cannot afford O(n²)**.
- You need **O(n)** or **O(n·log n)** at worst.

---

#### Step 2: Match to time complexity

Use the table to guide:

- Use **HashMaps / Sets / Sorting (O(n log n))** if needed.
- Avoid nested loops unless guaranteed small input (like n ≤ 500).

---

### ✅ Example Decisions

#### Example 1:

```txt
n <= 10^5
```

→ **Only O(n log n)** or **O(n)** is safe.

- ✅ Sorting
- ✅ Prefix sum
- ✅ Sliding window
- ❌ Nested loops (O(n²))

---

#### Example 2:

```txt
matrix of size ≤ 100 x 100
```

→ O(n³) might be okay.

---

#### Example 3:

```txt
1 <= n <= 20
```

→ This is **very small** → brute force or backtracking is fine.

- ✅ Bitmask DP
- ✅ O(2ⁿ)

---

### 🧠 Practice Tip

When you solve a problem:

1. **Estimate the number of operations** your code does.
2. Compare with the safe threshold: `10⁷ to 10⁸`.
3. If you're above it → Time to optimize.

---
