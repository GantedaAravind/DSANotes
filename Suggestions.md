### ✅ **Sorting Algorithms**

- **Merge Sort**: Use when stable sort is needed; works well on linked lists or large datasets.
- **Quick Sort**: Fast average case; good for in-memory arrays, avoid for worst-case unless randomized.
- **Heap Sort**: Use when constant space is needed and stability is not important.
- **Counting/Radix Sort**: Use for integers with limited range.

---

### ✅ **Searching Algorithms**

- **Binary Search**: Use on sorted arrays to reduce time to `O(log n)`.

---

### ✅ **Prefix Sum**

- Use Prefix Sum when you need to quickly calculate the sum of elements in a subarray multiple times.

---

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
