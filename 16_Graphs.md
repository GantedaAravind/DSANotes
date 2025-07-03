# Graphs in DSA: Beginner to Advanced

## 1. Introduction to Graphs

A **graph** is a non-linear data structure consisting of vertices (nodes) and edges that connect these vertices. Graphs are used to represent relationships between objects and are fundamental in computer science for solving problems like finding shortest paths, network analysis, social media connections, and more.

### Real-world Applications

- Social networks (friends, followers)
- Transportation networks (roads, flights)
- Computer networks (routers, connections)
- Web page linking
- Dependency graphs in software
- Game state representations

## 2. Graph Terminology {#terminology}

### Basic Terms

- **Vertex/Node**: A fundamental unit of a graph
- **Edge**: A connection between two vertices
- **Adjacent**: Two vertices connected by an edge
- **Degree**: Number of edges connected to a vertex
- **Path**: A sequence of vertices connected by edges
- **Cycle**: A path that starts and ends at the same vertex
- **Connected Graph**: Every vertex is reachable from every other vertex
- **Disconnected Graph**: Contains isolated components

### Advanced Terms

- **In-degree**: Number of incoming edges (directed graphs)
- **Out-degree**: Number of outgoing edges (directed graphs)
- **Strongly Connected**: Every vertex is reachable from every other vertex in both directions
- **Weakly Connected**: Underlying undirected graph is connected
- **Bipartite Graph**: Vertices can be divided into two disjoint sets

## 3. Types of Graphs {#types}

### 3.1 Based on Direction

**Undirected Graph**: Edges have no direction

```
A --- B
|     |
C --- D
```

**Directed Graph (Digraph)**: Edges have direction

```
A --> B
|     |
v     v
C --> D
```

### 3.2 Based on Weights

**Unweighted Graph**: All edges have equal weight (usually 1)
**Weighted Graph**: Edges have associated weights/costs

### 3.3 Special Types

- **Complete Graph**: Every vertex is connected to every other vertex
- **Tree**: Connected acyclic graph
- **Forest**: Collection of trees
- **Bipartite Graph**: Vertices can be colored with two colors
- **Planar Graph**: Can be drawn without edge crossings
  Here’s a **complete explanation of Graph Representations** in Data Structures and Algorithms (DSA), including use-cases, advantages, disadvantages, and examples for each.

---

# 📘 Graph Representations

Graphs can be represented in various ways depending on the needs of the algorithm and constraints of the problem (dense vs sparse, directed vs undirected, etc.).

---

## ✅ **1. Adjacency Matrix**

### 🔹 Description:

A 2D matrix `adj[V][V]` where:

- `adj[i][j] = 1` if there is an edge from vertex `i` to vertex `j`.
- `adj[i][j] = weight` if it’s a **weighted graph**.
- `adj[i][j] = 0` means no edge (or `∞` in weighted graph with no edge).

### 🔹 Example:

For the graph:

```
Vertices: 0, 1, 2
Edges: 0-1, 1-2
```

Adjacency Matrix (undirected):

```
   0 1 2
0 [0 1 0]
1 [1 0 1]
2 [0 1 0]
```

### 🔹 Time and Space:

- Space: **O(V²)**
- Add edge: **O(1)**
- Remove edge: **O(1)**
- Check if edge exists: **O(1)**
- Iterate all neighbors: **O(V)**

### ✅ Use When:

- Graph is **dense**
- Frequent edge lookups are needed
- You need a **simple implementation**

### ❌ Not Ideal When:

- Graph is **sparse** (wastes space)

---

## ✅ **2. Adjacency List**

### 🔹 Description:

An array (or map) of lists. Each index `i` stores a list of nodes that are adjacent to node `i`.

### 🔹 Example:

For the same graph:

```
0: [1]
1: [0, 2]
2: [1]
```

In JavaScript (or Python-like pseudocode):

```js
const graph = {
  0: [1],
  1: [0, 2],
  2: [1],
};
```

### 🔹 For Weighted Graph:

Each list contains pairs: `(neighbor, weight)`

```js
const graph = {
  0: [[1, 4]],
  1: [
    [0, 4],
    [2, 3],
  ],
  2: [[1, 3]],
};
```

### 🔹 Time and Space:

- Space: **O(V + E)**
- Add edge: **O(1)**
- Remove edge: **O(degree of node)**
- Check if edge exists: **O(degree of node)**
- Iterate all neighbors: **O(degree of node)**

### ✅ Use When:

- Graph is **sparse**
- You want to optimize for space

### ❌ Not Ideal When:

- You need constant-time edge existence check

---

## ✅ **3. Edge List**

### 🔹 Description:

Graph is represented as a list of edges. Each edge is a pair or triplet: `[u, v]` or `[u, v, weight]`.

### 🔹 Example:

```
Edges: [(0, 1), (1, 2)]
Weighted: [(0, 1, 4), (1, 2, 3)]
```

### 🔹 Time and Space:

- Space: **O(E)**
- Add edge: **O(1)**
- Remove edge: **O(E)**
- Check edge existence: **O(E)**
- Not good for traversal

### ✅ Use When:

- You just need a simple list of all edges (e.g., Kruskal’s Algorithm)
- Edge sorting is important

### ❌ Not Ideal When:

- You need fast adjacency lookup or traversal

---

## 🔁 Summary Table

| Representation   | Space    | Edge Check | Best Use                           |
| ---------------- | -------- | ---------- | ---------------------------------- |
| Adjacency Matrix | O(V²)    | O(1)       | Dense graphs, fast edge lookups    |
| Adjacency List   | O(V + E) | O(degree)  | Sparse graphs, efficient memory    |
| Edge List        | O(E)     | O(E)       | Good for algorithms like Kruskal’s |

---

## 🧠 Notes:

- **Undirected graph**: Add both `u → v` and `v → u`
- **Directed graph**: Add only `u → v`
- **Weighted graph**: Use a tuple `(neighbor, weight)` or object `{to: x, weight: w}`

# **Traversals**

## 🔢 **1. Breadth-First Search (BFS)**

### 📘 **Problem Statement**

You are given an unweighted graph. Implement **BFS traversal** starting from a source node and return the order of traversal.

---

### 🧪 **Test Cases**

**Test Case 1:**
Input:

```
V = 5, Edges = [[0,1],[0,2],[1,3],[1,4]], Start = 0
```

Output:

```
[0,1,2,3,4]
```

**Test Case 2:**
Input:

```
V = 3, Edges = [[0,1],[1,2]], Start = 1
```

Output:

```
[1,0,2]
```

**Test Case 3:**
Input:

```
V = 4, Edges = [[0,1],[2,3]], Start = 0
```

Output:

```
[0,1] (Only the connected component)
```

**Test Case 4:**
Input:

```
V = 1, Edges = [], Start = 0
```

Output:

```
[0]
```

---

### 💡 **Intuition**

BFS explores nodes **level by level** starting from the source node. It uses a **queue** to remember which nodes to visit next and a **visited set/array** to avoid cycles or re-processing.

---

### 🔍 **Dry Run (Test Case 1)**

Graph:

```
       0
      / \
     1   2
    / \
   3   4
```

Steps:

1. Start from node 0 → Add to queue → `queue = [0]`, `visited = {0}`
2. Dequeue 0 → Add neighbors 1 & 2 → `queue = [1, 2]`, `visited = {0,1,2}`
3. Dequeue 1 → Add neighbors 3 & 4 → `queue = [2, 3, 4]`, `visited = {0,1,2,3,4}`
4. Dequeue 2 → No new neighbors
5. Dequeue 3 → No new neighbors
6. Dequeue 4 → No new neighbors

**Traversal Order:** `[0, 1, 2, 3, 4]`

---

### ✅ **JavaScript Code**

```javascript
function bfsTraversal(V, edges, start) {
  const adj = Array.from({ length: V }, () => []);
  for (let [u, v] of edges) {
    adj[u].push(v);
    adj[v].push(u); // remove this if graph is undirected
  }

  const visited = new Array(V).fill(false);
  const queue = [];
  const result = [];

  queue.push(start);
  visited[start] = true;

  while (queue.length > 0) {
    const node = queue.shift();
    result.push(node);

    for (let neighbor of adj[node]) {
      if (!visited[neighbor]) {
        visited[neighbor] = true;
        queue.push(neighbor);
      }
    }
  }

  return result;
}
```

---

### ⏱ **Time and Space Complexity**

- **Time Complexity**: `O(V + E)`
- **Space Complexity**: `O(V + E)` (adjacency list) + `O(V)` (queue + visited)

---

### 📌 **Summary Table**

| Step                   | Purpose                  |
| ---------------------- | ------------------------ |
| Build Adjacency List   | For graph traversal      |
| Use Queue              | Level-order processing   |
| Use Visited Array      | Prevent revisiting nodes |
| Push into result array | Track traversal order    |

---

## 🔢 **2. Depth-First Search (DFS)**

### 📘 **Problem Statement**

You are given an undirected graph. Implement **DFS traversal** starting from a given source node and return the order of visited nodes.

---

### 🧪 **Test Cases**

**Test Case 1:**

```
V = 5, Edges = [[0,1],[0,2],[1,3],[1,4]], Start = 0
Output: [0,1,3,4,2]
```

**Test Case 2:**

```
V = 3, Edges = [[0,1],[1,2]], Start = 1
Output: [1,0,2]
```

**Test Case 3:**

```
V = 4, Edges = [[0,1],[2,3]], Start = 0
Output: [0,1]
```

**Test Case 4:**

```
V = 1, Edges = [], Start = 0
Output: [0]
```

---

### 💡 **Intuition**

DFS explores **as far as possible** along each branch before backtracking. It can be implemented using **recursion** (call stack) or an explicit **stack**.

It’s useful for:

- Finding connected components
- Cycle detection
- Topological sort (for DAGs)
- Maze/graph traversal

---

### 🔍 **Dry Run (Test Case 1)**

Graph:

```
       0
      / \
     1   2
    / \
   3   4
```

Start at node 0:

1. Visit 0 → stack = \[0], visited = {0}
2. Go to 1 → visited = {0,1}
3. Go to 3 → visited = {0,1,3}
4. Backtrack to 1 → Go to 4 → visited = {0,1,3,4}
5. Backtrack to 1 → 0 → then to 2 → visited = {0,1,2,3,4}

**Traversal Order:** `[0,1,3,4,2]`

---

### ✅ **JavaScript Code**

```javascript
function dfsTraversal(V, edges, start) {
  const adj = Array.from({ length: V }, () => []);
  for (let [u, v] of edges) {
    adj[u].push(v);
    adj[v].push(u); // remove this if graph is directed
  }

  const visited = new Array(V).fill(false);
  const result = [];

  function dfs(node) {
    visited[node] = true;
    result.push(node);

    for (let neighbor of adj[node]) {
      if (!visited[neighbor]) {
        dfs(neighbor);
      }
    }
  }

  dfs(start);
  return result;
}
```

---

### ⏱ **Time and Space Complexity**

- **Time Complexity**: `O(V + E)`
- **Space Complexity**: `O(V + E)` (adj list) + `O(V)` (visited + recursion stack)

---

### 📌 **Summary Table**

| Step                 | Purpose          |
| -------------------- | ---------------- |
| Build Adjacency List | For graph        |
| Recursive DFS        | Deep exploration |
| Use Visited Array    | Avoid revisiting |
| Track Order          | Record result    |

---

### 🔄 DFS (Iterative Version Using Stack)

```javascript
function dfsIterative(V, edges, start) {
  const adj = Array.from({ length: V }, () => []);
  for (let [u, v] of edges) {
    adj[u].push(v);
    adj[v].push(u);
  }

  const visited = new Array(V).fill(false);
  const result = [];
  const stack = [start];

  while (stack.length) {
    const node = stack.pop();
    if (!visited[node]) {
      visited[node] = true;
      result.push(node);
      for (let neighbor of adj[node]) {
        if (!visited[neighbor]) {
          stack.push(neighbor);
        }
      }
    }
  }

  return result;
}
```

---

### 💬 Summary

| Feature        | DFS                            |
| -------------- | ------------------------------ |
| Strategy       | Deep before wide               |
| Data Structure | Stack / Recursion              |
| Time           | `O(V + E)`                     |
| Space          | `O(V + E)`                     |
| Best For       | Connectivity, cycles, topology |

---

# **Problems On DFS/BFS**

## 🔢 **1. Number of Provinces**

(Also known as “Number of Connected Components in an Undirected Graph”)

### 📘 Problem Statement

There are `n` cities. Some of them are connected, and some are not. A province is a group of directly or indirectly connected cities. Given a **`n x n` adjacency matrix `isConnected`**, return the number of **provinces**.

- `isConnected[i][j] = 1` means city `i` and `j` are directly connected.
- `isConnected[i][j] = 0` means no direct connection.

---

### 🧪 Test Cases

**Test Case 1:**

```
Input: isConnected = [
 [1,1,0],
 [1,1,0],
 [0,0,1]
]
Output: 2
```

**Test Case 2:**

```
Input: isConnected = [
 [1,0,0],
 [0,1,0],
 [0,0,1]
]
Output: 3
```

**Test Case 3:**

```
Input: isConnected = [
 [1,1,1],
 [1,1,1],
 [1,1,1]
]
Output: 1
```

---

### 💡 Intuition

Treat the cities as **nodes of a graph**, and connections as **edges**. The number of **provinces** is simply the number of **connected components** in this undirected graph.

We perform **DFS or BFS** for each unvisited node, and count how many times we initiate a new traversal — that count is the number of provinces.

---

### 🔍 Dry Run (Test Case 1)

Adjacency matrix:

```
0 - 1     (connected)
2         (isolated)
```

- Start DFS from node 0 → visit 1 → component 1
- Node 2 not visited → new DFS → component 2

✅ Total provinces: **2**

---

### ✅ JavaScript Code (DFS Approach)

```javascript
function findCircleNum(isConnected) {
  const n = isConnected.length;
  const visited = new Array(n).fill(false);
  let provinces = 0;

  function dfs(city) {
    visited[city] = true;
    for (let neighbor = 0; neighbor < n; neighbor++) {
      if (isConnected[city][neighbor] === 1 && !visited[neighbor]) {
        dfs(neighbor);
      }
    }
  }

  for (let city = 0; city < n; city++) {
    if (!visited[city]) {
      dfs(city);
      provinces++;
    }
  }

  return provinces;
}
```

---

### ✅ JavaScript Code (BFS Approach)

```javascript
function findCircleNum(isConnected) {
  const n = isConnected.length;
  const visited = new Array(n).fill(false);
  let provinces = 0;

  for (let city = 0; city < n; city++) {
    if (!visited[city]) {
      const queue = [city];
      while (queue.length > 0) {
        const current = queue.shift();
        visited[current] = true;
        for (let neighbor = 0; neighbor < n; neighbor++) {
          if (isConnected[current][neighbor] === 1 && !visited[neighbor]) {
            queue.push(neighbor);
          }
        }
      }
      provinces++;
    }
  }

  return provinces;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity**: O(N²) — due to iterating over the matrix.
- **Space Complexity**: O(N) — for visited array and recursion/queue.

---

### 📌 Summary Table

| Concept      | Value                           |
| ------------ | ------------------------------- |
| Graph Type   | Undirected, implicit via matrix |
| Approach     | DFS / BFS                       |
| Components   | Provinces                       |
| Input Format | Adjacency Matrix                |

---

## 🔢 **2. Rotten Oranges**

### 📘 Problem Statement

You are given a `m x n` grid where each cell can be:

- `0`: Empty cell
- `1`: Fresh orange
- `2`: Rotten orange

Each minute, **any fresh orange** adjacent (up/down/left/right) to a **rotten orange** becomes rotten.

Return the **minimum time** required to rot all oranges. If it’s impossible to rot all fresh oranges, return `-1`.

---

### 🧪 Test Cases

**Test Case 1:**

```
Input:
[[2,1,1],
 [1,1,0],
 [0,1,1]]

Output: 4
```

**Test Case 2:**

```
Input:
[[2,1,1],
 [0,1,1],
 [1,0,1]]

Output: -1
```

**Test Case 3:**

```
Input:
[[0,2]]

Output: 0
```

---

### 💡 Intuition

This is a **multi-source BFS** problem:

- We start the BFS from **all rotten oranges simultaneously** (time = 0).
- At each level of BFS (minute), the rotting spreads to adjacent fresh oranges.
- We use a **queue** to keep track of oranges that rot others.
- Use a **counter** to track minutes.

---

### 🔍 Dry Run (Test Case 1)

Initial Grid:

```
2 1 1
1 1 0
0 1 1
```

Initial rotten oranges in queue:

```
[[0,0]]
```

#### Minute 1:

- Rot \[0,1] and \[1,0] → Add to queue

#### Minute 2:

- Rot \[0,2] and \[1,1]

#### Minute 3:

- Rot \[2,1]

#### Minute 4:

- Rot \[2,2]

✅ All rotten in **4 minutes**

---

### ✅ JavaScript Code (BFS)

```javascript
function orangesRotting(grid) {
  const rows = grid.length;
  const cols = grid[0].length;
  const queue = [];
  let fresh = 0;
  let time = 0;

  // Step 1: Collect all rotten oranges and count fresh ones
  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      if (grid[r][c] === 2) {
        queue.push([r, c]);
      } else if (grid[r][c] === 1) {
        fresh++;
      }
    }
  }

  const directions = [
    [1, 0],
    [-1, 0],
    [0, 1],
    [0, -1],
  ];

  // Step 2: Multi-source BFS
  while (queue.length && fresh > 0) {
    let size = queue.length;
    for (let i = 0; i < size; i++) {
      const [r, c] = queue.shift();

      for (let [dr, dc] of directions) {
        const nr = r + dr;
        const nc = c + dc;

        if (
          nr >= 0 &&
          nr < rows &&
          nc >= 0 &&
          nc < cols &&
          grid[nr][nc] === 1
        ) {
          grid[nr][nc] = 2;
          queue.push([nr, nc]);
          fresh--;
        }
      }
    }
    time++; // Increase time after each level
  }

  return fresh === 0 ? time : -1;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity**: O(m × n)
  Every cell is visited at most once.

- **Space Complexity**: O(m × n)
  For the queue in worst-case (all oranges are rotten/fresh).

---

### 📌 Summary Table

| Step             | Purpose                   |
| ---------------- | ------------------------- |
| Initialize queue | With all rotten oranges   |
| Count fresh      | To detect if impossible   |
| Directions array | For 4-directional BFS     |
| Multi-level BFS  | Rot level by level        |
| Return -1        | If some fresh left at end |

---

### ⚠️ Edge Cases & Pitfalls

| Case                              | What to do |
| --------------------------------- | ---------- |
| No fresh oranges                  | Return 0   |
| No rotten oranges but fresh exist | Return -1  |
| Already rotten                    | Return 0   |
| Disconnected fresh oranges        | Return -1  |

---

## 🔢 **3. Flood Fill Algorithm**

### 📘 Problem Statement

You are given an image represented by a 2D grid of integers `image[m][n]` where each integer represents a pixel color.
You are also given a coordinate `(sr, sc)` representing the **starting pixel**, and an integer `color` representing the **new color**.

Perform a **"flood fill"** starting from `(sr, sc)` — change the color of the starting pixel and all **4-directionally connected pixels** that have the **same original color** to the new color.

Return the modified image.

---

### 🧪 Test Cases

**Test Case 1:**

```js
Input: (image = [
  [1, 1, 1],
  [1, 1, 0],
  [1, 0, 1],
]),
  (sr = 1),
  (sc = 1),
  (color = 2);

Output: [
  [2, 2, 2],
  [2, 2, 0],
  [2, 0, 1],
];
```

**Test Case 2:**

```js
Input: (image = [
  [0, 0, 0],
  [0, 1, 1],
]),
  (sr = 1),
  (sc = 1),
  (color = 1);

Output: [
  [0, 0, 0],
  [0, 1, 1],
];
```

---

### 💡 Intuition

Flood Fill is essentially a **DFS or BFS** problem on a **2D grid**. Starting from the source pixel, we recursively or iteratively traverse all connected pixels having the **same original color**, and replace their color with the new one.

If the `newColor` is the **same as the old color**, no change is needed.

---

### 🔍 Dry Run (Test Case 1)

Start from `(1,1)`, color = 1 → change to 2
Expand in all 4 directions:

- `(0,1)` → 1 → change to 2
- `(2,1)` → 0 → skip
- `(1,0)` → 1 → change to 2
- `(1,2)` → 0 → skip

Continue recursively or via queue.

---

### ✅ JavaScript Code (DFS Approach)

```javascript
function floodFill(image, sr, sc, color) {
  const rows = image.length;
  const cols = image[0].length;
  const oldColor = image[sr][sc];
  if (oldColor === color) return image;

  function dfs(r, c) {
    if (r < 0 || r >= rows || c < 0 || c >= cols || image[r][c] !== oldColor)
      return;

    image[r][c] = color;

    dfs(r + 1, c);
    dfs(r - 1, c);
    dfs(r, c + 1);
    dfs(r, c - 1);
  }

  dfs(sr, sc);
  return image;
}
```

---

### ✅ JavaScript Code (BFS Approach)

```javascript
function floodFill(image, sr, sc, color) {
  const rows = image.length;
  const cols = image[0].length;
  const oldColor = image[sr][sc];
  if (oldColor === color) return image;

  const queue = [[sr, sc]];
  const directions = [
    [1, 0],
    [-1, 0],
    [0, 1],
    [0, -1],
  ];

  while (queue.length > 0) {
    const [r, c] = queue.shift();

    if (r >= 0 && r < rows && c >= 0 && c < cols && image[r][c] === oldColor) {
      image[r][c] = color;

      for (let [dr, dc] of directions) {
        queue.push([r + dr, c + dc]);
      }
    }
  }

  return image;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity**: O(m × n)
  Every cell is visited at most once.

- **Space Complexity**:

  - DFS recursion stack: O(m × n) worst case
  - BFS queue: O(m × n)

---

### 📌 Summary Table

| Concept      | Value                                    |
| ------------ | ---------------------------------------- |
| Problem Type | 2D Grid Traversal                        |
| Technique    | DFS or BFS                               |
| Directions   | 4-connected (no diagonals)               |
| Edge Case    | If `newColor === oldColor`, return early |

---

## 🔢 **4. Cycle Detection in an Undirected Graph (BFS)**

### 📘 Problem Statement

Given an **undirected graph** with `V` vertices and a list of `edges`, determine whether the graph **contains a cycle**.

Return `true` if there is a cycle, otherwise return `false`.

---

### 🧪 Test Cases

**Test Case 1:**

```js
V = 4, Edges = [[0,1],[1,2],[2,3],[3,0]]
Output: true
Explanation: Cycle exists — 0-1-2-3-0
```

**Test Case 2:**

```js
(V = 3),
  (Edges = [
    [0, 1],
    [1, 2],
  ]);
Output: false;
```

**Test Case 3:**

```js
(V = 5),
  (Edges = [
    [0, 1],
    [1, 2],
    [3, 4],
  ]);
Output: false;
```

**Test Case 4:**

```js
(V = 4),
  (Edges = [
    [0, 1],
    [1, 2],
    [2, 0],
  ]);
Output: true;
```

---

### 💡 Intuition

To detect a **cycle in an undirected graph using BFS**, we:

- Track visited nodes.
- Use a **queue**, where each entry holds the node and its **parent** (since edges are undirected).
- If we revisit a node that’s **not the parent**, then a cycle exists.

---

### 🔍 Dry Run (Test Case 1)

Edges: \[\[0,1],\[1,2],\[2,3],\[3,0]]

Traversal:

- Start BFS at node 0, parent = -1
- Visit 1 → parent = 0
- Visit 2 → parent = 1
- Visit 3 → parent = 2
- Try to visit 0 from 3 → already visited & not parent → ✅ **Cycle Detected**

---

### ✅ JavaScript Code (BFS Approach)

```javascript
function hasCycle(V, edges) {
  const adj = Array.from({ length: V }, () => []);

  // Build adjacency list
  for (let [u, v] of edges) {
    adj[u].push(v);
    adj[v].push(u); // undirected graph
  }

  const visited = new Array(V).fill(false);

  for (let i = 0; i < V; i++) {
    if (!visited[i]) {
      if (bfsCycleCheck(i, adj, visited)) {
        return true;
      }
    }
  }

  return false;
}

function bfsCycleCheck(start, adj, visited) {
  const queue = [[start, -1]];
  visited[start] = true;

  while (queue.length > 0) {
    const [node, parent] = queue.shift();

    for (let neighbor of adj[node]) {
      if (!visited[neighbor]) {
        visited[neighbor] = true;
        queue.push([neighbor, node]);
      } else if (neighbor !== parent) {
        return true; // Cycle detected
      }
    }
  }

  return false;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity**: O(V + E)

  - Every vertex and edge is visited once.

- **Space Complexity**: O(V + E)

  - Adjacency list + queue + visited array

---

### 📌 Summary Table

| Element         | Description                  |
| --------------- | ---------------------------- |
| Graph Type      | Undirected                   |
| Traversal       | BFS + Queue                  |
| Key Technique   | Track parent during BFS      |
| Cycle Condition | Already visited & not parent |

---

## 🔢 **5. Cycle Detection in an Undirected Graph (DFS)**

### 📘 Problem Statement

You are given an undirected graph with `V` vertices and a list of `edges`. Your task is to determine **whether the graph contains a cycle**.

Return:

- `true` → if a cycle exists
- `false` → if no cycle exists

---

### 🧪 Test Cases

**Test Case 1:**

```js
(V = 4),
  (Edges = [
    [0, 1],
    [1, 2],
    [2, 3],
    [3, 0],
  ]);
Output: true;
```

**Test Case 2:**

```js
(V = 3),
  (Edges = [
    [0, 1],
    [1, 2],
  ]);
Output: false;
```

**Test Case 3:**

```js
(V = 5),
  (Edges = [
    [0, 1],
    [1, 2],
    [3, 4],
  ]);
Output: false;
```

**Test Case 4:**

```js
(V = 4),
  (Edges = [
    [0, 1],
    [1, 2],
    [2, 0],
  ]);
Output: true;
```

---

### 💡 Intuition

In **DFS for an undirected graph**, we need to track the **parent node**. If during DFS traversal, we visit a neighbor that is already visited **and is not the parent**, then a **cycle exists**.

---

### 🔍 Dry Run (Test Case 4)

Graph: `0-1-2-0`

- Start DFS at 0 → visit 1 → visit 2 → visit 0
- 0 is already visited, and it’s **not** the parent of 2 → ✅ cycle detected.

---

### ✅ JavaScript Code (DFS Approach)

```javascript
function hasCycle(V, edges) {
  const adj = Array.from({ length: V }, () => []);

  // Step 1: Build adjacency list
  for (let [u, v] of edges) {
    adj[u].push(v);
    adj[v].push(u); // Undirected graph
  }

  const visited = new Array(V).fill(false);

  // Step 2: DFS from each unvisited node
  for (let i = 0; i < V; i++) {
    if (!visited[i]) {
      if (dfsCycleCheck(i, -1, adj, visited)) {
        return true;
      }
    }
  }

  return false;
}

function dfsCycleCheck(node, parent, adj, visited) {
  visited[node] = true;

  for (let neighbor of adj[node]) {
    if (!visited[neighbor]) {
      if (dfsCycleCheck(neighbor, node, adj, visited)) return true;
    } else if (neighbor !== parent) {
      return true; // Cycle found
    }
  }

  return false;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity**: `O(V + E)`
  Every node and edge is visited once.

- **Space Complexity**: `O(V + E)`
  For adjacency list and visited array, plus recursion stack.

---

### 📌 Summary Table

| Step          | Description                              |
| ------------- | ---------------------------------------- |
| Build Graph   | Using adjacency list                     |
| Track Visited | To avoid revisits                        |
| Use Parent    | To differentiate back-edge vs cross-edge |
| DFS Traversal | Recursive                                |
| Cycle Found   | If visited neighbor is not parent        |

---

### ✅ Key Differences (DFS vs BFS)

| Feature         | DFS                | BFS                      |
| --------------- | ------------------ | ------------------------ |
| Approach        | Recursion          | Queue                    |
| Parent Tracking | Pass as argument   | Store with node in queue |
| Performance     | Similar (O(V + E)) | Similar (O(V + E))       |

---

## 🔢 **6. 01 Matrix (Leetcode 542)**

### 📘 Problem Statement

You are given an `m x n` binary matrix `mat` of only **0s and 1s**.

Return a matrix `dist` of the same size where each cell contains the **distance to the nearest 0**.

- Distance is calculated as the **shortest path** (4-directional: up, down, left, right).
- All 0s remain 0.
- All 1s are updated to the minimum steps needed to reach any 0.

---

### 🧪 Test Cases

**Test Case 1:**

```
Input:
[[0,0,0],
 [0,1,0],
 [1,1,1]]

Output:
[[0,0,0],
 [0,1,0],
 [1,2,1]]
```

**Test Case 2:**

```
Input:
[[0,1,1],
 [1,1,1],
 [1,1,0]]

Output:
[[0,1,2],
 [1,2,1],
 [2,1,0]]
```

---

### 💡 Intuition

This is a classic **multi-source BFS** problem:

- All **0s act as sources** from which the BFS starts **simultaneously**.
- Instead of finding the distance for every 1 individually (inefficient), **we perform BFS from all 0s together**, and update the minimum distance for every 1 as we reach it.

Think of the 0s as **starting points** that “spread out” and mark the distance to each 1.

---

### 🔍 Dry Run (Test Case 1)

Start BFS from all `0`s:

```
Initial:
0 0 0
0 1 0
1 1 1

After BFS:
0 0 0
0 1 0
1 2 1
```

Every 1 gets its minimum distance from the nearest 0.

---

### ✅ JavaScript Code (BFS)

```javascript
function updateMatrix(mat) {
  const rows = mat.length;
  const cols = mat[0].length;
  const queue = [];
  const directions = [
    [1, 0],
    [-1, 0],
    [0, 1],
    [0, -1],
  ];

  // Step 1: Mark all 1s as Infinity, and add all 0s to the queue
  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      if (mat[r][c] === 0) {
        queue.push([r, c]);
      } else {
        mat[r][c] = Infinity;
      }
    }
  }

  // Step 2: BFS from all 0s
  while (queue.length > 0) {
    const [r, c] = queue.shift();

    for (let [dr, dc] of directions) {
      const nr = r + dr;
      const nc = c + dc;

      if (
        nr >= 0 &&
        nr < rows &&
        nc >= 0 &&
        nc < cols &&
        mat[nr][nc] > mat[r][c] + 1
      ) {
        mat[nr][nc] = mat[r][c] + 1;
        queue.push([nr, nc]);
      }
    }
  }

  return mat;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity**: O(m × n)

  - Each cell is processed once.

- **Space Complexity**: O(m × n)

  - Queue and updated matrix.

---

### 📌 Summary Table

| Component        | Purpose                            |
| ---------------- | ---------------------------------- |
| Multi-source BFS | All 0s push to queue initially     |
| Directions array | 4-connected neighbors              |
| Distance update  | Only update if new dist is shorter |
| Queue            | Used for level-order BFS           |

---

## 🔢 **7. Surrounded Regions (DFS)**

### 📘 Problem Statement

Given an `m x n` board containing `'X'` and `'O'`:

- Capture all regions surrounded by `'X'`.
- A region is **captured** by flipping all `'O'`s into `'X'` **in that region**.
- A region is **surrounded** if it's **completely enclosed by 'X'** from all 4 directions (top, bottom, left, right).
- Any `'O'` **connected to the border** cannot be flipped.

---

### 🧪 Test Cases

**Test Case 1:**

```js
Input: [
  ["X", "X", "X", "X"],
  ["X", "O", "O", "X"],
  ["X", "X", "O", "X"],
  ["X", "O", "X", "X"],
];

Output: [
  ["X", "X", "X", "X"],
  ["X", "X", "X", "X"],
  ["X", "X", "X", "X"],
  ["X", "O", "X", "X"],
];
```

**Test Case 2:**

```js
Input: [["X"]];

Output: [["X"]];
```

**Test Case 3:**

```js
Input: [
  ["O", "O", "O"],
  ["O", "X", "O"],
  ["O", "O", "O"],
];

Output: [
  ["O", "O", "O"],
  ["O", "X", "O"],
  ["O", "O", "O"],
];
```

---

### 💡 Intuition

- Any `'O'` that is **connected to a border `'O'`** is **not surrounded**.
- So we:

  1. **Mark all `'O'`s connected to border `'O'`s** using DFS (change to a temp char like `'T'`).
  2. **Flip all remaining `'O'`s** to `'X'` (they’re surrounded).
  3. **Flip `'T'` back to `'O'`** (restore border-connected regions).

---

### 🔍 Dry Run (Test Case 1)

Initial:

```
XXXX
XOOX
XXOX
XOXX
```

- Border-connected `'O'`: at `(3,1)` → mark via DFS: change to `'T'`

Temp Marking:

```
XXXX
XOOX
XXOX
XTX X
```

Flip all `'O'` → `'X'` (surrounded)
Flip all `'T'` → `'O'` (safe)

Final:

```
XXXX
XXXX
XXXX
XOXX
```

---

### ✅ JavaScript Code (DFS Approach)

```javascript
function solve(board) {
  if (!board || board.length === 0) return;

  const rows = board.length;
  const cols = board[0].length;

  function dfs(r, c) {
    if (r < 0 || r >= rows || c < 0 || c >= cols || board[r][c] !== "O") return;

    board[r][c] = "T"; // Temporarily mark
    dfs(r + 1, c);
    dfs(r - 1, c);
    dfs(r, c + 1);
    dfs(r, c - 1);
  }

  // Step 1: Run DFS for all 'O's on the border
  for (let r = 0; r < rows; r++) {
    if (board[r][0] === "O") dfs(r, 0);
    if (board[r][cols - 1] === "O") dfs(r, cols - 1);
  }

  for (let c = 0; c < cols; c++) {
    if (board[0][c] === "O") dfs(0, c);
    if (board[rows - 1][c] === "O") dfs(rows - 1, c);
  }

  // Step 2: Flip all remaining 'O' → 'X', and 'T' → 'O'
  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      if (board[r][c] === "O") {
        board[r][c] = "X";
      } else if (board[r][c] === "T") {
        board[r][c] = "O";
      }
    }
  }
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity**: O(m × n)

  - Every cell is visited once during DFS.

- **Space Complexity**: O(m × n) worst case

  - Due to recursion stack.

---

### 📌 Summary Table

| Step    | Description                    |
| ------- | ------------------------------ |
| DFS     | On all border 'O's             |
| Mark    | Change connected 'O' → `'T'`   |
| Flip    | All `'O'` → `'X'` (surrounded) |
| Restore | All `'T'` → `'O'` (safe)       |

---

## 🔢 **8. Number of Enclaves (Flood Fill - Multi-Source)**

### 📘 Problem Statement

You are given an `m x n` binary matrix `grid`, where:

- `0` represents **water**
- `1` represents **land**

An **enclave** is a land cell (`1`) that **cannot** walk off the boundary of the grid in any number of moves (only 4 directions: up, down, left, right).

🧠 Return the number of **land cells that are enclaves** (i.e., not connected to the boundary).

---

### 🧪 Test Cases

**Test Case 1:**

```js
Input: grid = [
  [0, 0, 0, 0],
  [1, 0, 1, 0],
  [0, 1, 1, 0],
  [0, 0, 0, 0],
];

Output: 3;
```

**Test Case 2:**

```js
Input: grid = [
  [0, 1, 1, 0],
  [0, 0, 1, 0],
  [0, 0, 1, 0],
  [0, 0, 0, 0],
];

Output: 0;
```

---

### 💡 Intuition

We treat this as a **flood fill problem**.

- Any **land cell connected to the border** is **not an enclave**.
- We perform a **multi-source flood fill (BFS or DFS)** from all boundary land cells to mark them as visited (or convert to water).
- Finally, we **count all remaining land cells (`1`)** which are not connected to any boundary → ✅ those are enclaves.

---

### 🔍 Dry Run (Test Case 1)

Before:

```
0 0 0 0
1 0 1 0
0 1 1 0
0 0 0 0
```

After flood-filling border-connected land (none in this case):
Only internal component `[1,1]` → 3 land cells → ✅ Enclave size = 3

---

### ✅ JavaScript Code (DFS - Flood Fill)

```javascript
function numEnclaves(grid) {
  const rows = grid.length;
  const cols = grid[0].length;

  function dfs(r, c) {
    if (r < 0 || r >= rows || c < 0 || c >= cols || grid[r][c] !== 1) return;
    grid[r][c] = 0; // Mark visited
    dfs(r + 1, c);
    dfs(r - 1, c);
    dfs(r, c + 1);
    dfs(r, c - 1);
  }

  // Step 1: Flood fill all boundary land cells
  for (let r = 0; r < rows; r++) {
    if (grid[r][0] === 1) dfs(r, 0);
    if (grid[r][cols - 1] === 1) dfs(r, cols - 1);
  }

  for (let c = 0; c < cols; c++) {
    if (grid[0][c] === 1) dfs(0, c);
    if (grid[rows - 1][c] === 1) dfs(rows - 1, c);
  }

  // Step 2: Count remaining land cells
  let count = 0;
  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      if (grid[r][c] === 1) count++;
    }
  }

  return count;
}
```

---

### ✅ JavaScript Code (BFS - Flood Fill)

```javascript
function numEnclaves(grid) {
  const rows = grid.length;
  const cols = grid[0].length;
  const directions = [
    [1, 0],
    [-1, 0],
    [0, 1],
    [0, -1],
  ];

  function bfs(r, c) {
    const queue = [[r, c]];
    grid[r][c] = 0;

    while (queue.length > 0) {
      const [x, y] = queue.shift();
      for (let [dx, dy] of directions) {
        const nx = x + dx;
        const ny = y + dy;
        if (
          nx >= 0 &&
          nx < rows &&
          ny >= 0 &&
          ny < cols &&
          grid[nx][ny] === 1
        ) {
          grid[nx][ny] = 0;
          queue.push([nx, ny]);
        }
      }
    }
  }

  // Step 1: Start BFS from all boundary land cells
  for (let r = 0; r < rows; r++) {
    if (grid[r][0] === 1) bfs(r, 0);
    if (grid[r][cols - 1] === 1) bfs(r, cols - 1);
  }

  for (let c = 0; c < cols; c++) {
    if (grid[0][c] === 1) bfs(0, c);
    if (grid[rows - 1][c] === 1) bfs(rows - 1, c);
  }

  // Step 2: Count remaining land cells
  let count = 0;
  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      if (grid[r][c] === 1) count++;
    }
  }

  return count;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity**: O(m × n)
  Every cell is visited at most once.

- **Space Complexity**:

  - O(m × n) for recursion stack (DFS) or queue (BFS)

---

### 📌 Summary Table

| Step                    | Action                                   |
| ----------------------- | ---------------------------------------- |
| Multi-source flood fill | From all boundary land cells (`1`)       |
| Mark land as visited    | Change to `0` (water)                    |
| Final count             | Count all `1`s remaining inside the grid |

---

## 🔢 **9. Word Ladder I**

### 📘 Problem Statement

Given:

- A `beginWord`
- An `endWord`
- A word list `wordList[]`

Transform `beginWord` to `endWord` by changing **only one letter at a time**, and **each transformed word must be in the wordList**.

🧠 Return the **length of the shortest transformation sequence**, or `0` if no transformation is possible.

> ⚠ You can assume all words are of the same length and lowercase.

---

### 🧪 Test Cases

**Test Case 1:**

```js
Input:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

Output: 5

Explanation: hit → hot → dot → dog → cog
```

**Test Case 2:**

```js
Input:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log"]

Output: 0

Explanation: cog is not in the word list.
```

---

### 💡 Intuition

This is a **shortest path problem** in an **unweighted word graph**, where:

- Each word is a node.
- There's an edge between two words if they differ by exactly one character.
- We can model this as a **BFS traversal** starting from `beginWord`.

To optimize checking, we use:

- A **set** to hold valid words for O(1) lookup.
- A **queue** for BFS traversal.
- A **visited set** to avoid revisiting.

---

### 🔍 Dry Run (Test Case 1)

```text
Queue:
["hit", level=1]

1. hit → hot (in wordList)
2. hot → dot, lot
3. dot → dog
4. dog → cog (endWord found!)

Answer = 5 steps
```

---

### ✅ JavaScript Code (BFS Approach)

```javascript
function ladderLength(beginWord, endWord, wordList) {
  const wordSet = new Set(wordList);
  if (!wordSet.has(endWord)) return 0;

  const queue = [[beginWord, 1]];

  while (queue.length > 0) {
    const [word, level] = queue.shift();

    // Try changing every character
    for (let i = 0; i < word.length; i++) {
      for (let ch = 97; ch <= 122; ch++) {
        const newChar = String.fromCharCode(ch);
        const newWord = word.slice(0, i) + newChar + word.slice(i + 1);

        if (newWord === endWord) return level + 1;

        if (wordSet.has(newWord)) {
          queue.push([newWord, level + 1]);
          wordSet.delete(newWord); // Mark visited
        }
      }
    }
  }

  return 0; // No path found
}
```

---

### ⏱ Time and Space Complexity

Let:

- `L` = length of each word

- `N` = number of words in the wordList

- **Time Complexity**: `O(N * L * 26)`
  For each word and position, we try 26 letters.

- **Space Complexity**: `O(N)`
  For the queue and set.

---

### 📌 Summary Table

| Component      | Description                 |
| -------------- | --------------------------- |
| Graph Model    | Word transformation graph   |
| Traversal      | BFS (shortest path)         |
| Edge Condition | One letter difference       |
| Word Lookup    | Use `Set` for O(1) checking |
| Stop Condition | When `endWord` is reached   |

---

### ⚠️ Edge Cases

| Case                    | Result                                                                  |
| ----------------------- | ----------------------------------------------------------------------- |
| `endWord` not in list   | Return 0                                                                |
| `beginWord === endWord` | Return 1 (but generally not considered valid unless explicitly allowed) |
| No valid transformation | Return 0                                                                |

---

## 🔢 **10. Word Ladder II – Find All Shortest Transformation Sequences**

### 📘 Problem Statement

Given:

- `beginWord` and `endWord`
- A list of valid transformations `wordList`

Return **all shortest transformation sequences** from `beginWord` to `endWord` such that:

- Only **one letter** can be changed at a time.
- Each transformed word must exist in the wordList.
- Return **all shortest sequences** (not just one like in Word Ladder I).

🧠 Each sequence should be a list of words, starting from `beginWord` and ending with `endWord`.

---

### 🧪 Test Cases

**Test Case 1:**

```js
Input: (beginWord = "hit"),
  (endWord = "cog"),
  (wordList = ["hot", "dot", "dog", "lot", "log", "cog"]);

Output: [
  ["hit", "hot", "dot", "dog", "cog"],
  ["hit", "hot", "lot", "log", "cog"],
];
```

**Test Case 2:**

```js
Input: (beginWord = "hit"),
  (endWord = "cog"),
  (wordList = ["hot", "dot", "dog", "lot", "log"]);

Output: [];
```

---

### 💡 Intuition

We are asked for **all shortest paths**, which is a signal to:

1. Use **BFS** to explore all paths **level-by-level** to avoid going deep into non-shortest ones.
2. Track **parents** of each word using a `Map` (reverse adjacency list).
3. After BFS completes, use **backtracking** from `endWord` to `beginWord` using the parent map to construct all valid paths.

---

### 🔍 Dry Run (Test Case 1)

Start BFS from `"hit"`:

- `"hit"` → `"hot"`
- `"hot"` → `"dot"`, `"lot"`
- `"dot"` → `"dog"` → `"cog"`
- `"lot"` → `"log"` → `"cog"`

Now backtrack from `"cog"` to `"hit"` using reverse parent map:

- `cog → dog → dot → hot → hit`
- `cog → log → lot → hot → hit`

Reverse the paths.

---

### ✅ JavaScript Code (BFS + Backtracking)

```javascript
function findLadders(beginWord, endWord, wordList) {
  const wordSet = new Set(wordList);
  if (!wordSet.has(endWord)) return [];

  const res = [];
  const layer = new Map();
  layer.set(beginWord, [[beginWord]]);

  while (layer.size > 0) {
    const newLayer = new Map();

    for (let [word, paths] of layer.entries()) {
      if (word === endWord) {
        for (let path of paths) {
          res.push(path);
        }
      }

      // Try changing every character
      for (let i = 0; i < word.length; i++) {
        for (let c = 97; c <= 122; c++) {
          const newChar = String.fromCharCode(c);
          const newWord = word.slice(0, i) + newChar + word.slice(i + 1);

          if (wordSet.has(newWord)) {
            for (let path of paths) {
              if (!newLayer.has(newWord)) {
                newLayer.set(newWord, []);
              }
              newLayer.get(newWord).push([...path, newWord]);
            }
          }
        }
      }
    }

    // Remove visited words to prevent longer paths
    for (let key of newLayer.keys()) {
      wordSet.delete(key);
    }

    layer.clear();
    for (let [k, v] of newLayer.entries()) {
      layer.set(k, v);
    }

    if (res.length > 0) break; // Found shortest path
  }

  return res;
}
```

---

### ⏱ Time and Space Complexity

Let:

- `N` = number of words

- `L` = word length

- **Time Complexity**:
  Worst case: `O(N × L × 26)` per word transformation
  For path reconstruction: exponential in the number of shortest paths

- **Space Complexity**:
  `O(N × P)` where `P` = average number of paths per word

---

### 📌 Summary Table

| Step          | Description                                        |
| ------------- | -------------------------------------------------- |
| BFS           | Find all shortest paths from `beginWord`           |
| Track Parents | Using path lists stored in `Map<string, string[]>` |
| Backtrack     | From `endWord` to `beginWord` recursively          |
| Prune Early   | Remove visited words after each level              |

---

## 🔢 **11. Number of Distinct Islands**

### 📘 Problem Statement

You are given a `m x n` grid where:

- `1` represents land
- `0` represents water

Two islands are considered **distinct** if and only if **their shapes are different**, **regardless of position**.

🧠 Return the **number of distinct islands** (by shape, not location).

---

### 🧪 Test Cases

**Test Case 1:**

```js
Input:
grid = [
  [1,1,0,0,0],
  [1,1,0,0,0],
  [0,0,0,1,1],
  [0,0,0,1,1]
]

Output: 1
Explanation: Both islands have the same shape.
```

**Test Case 2:**

```js
Input:
grid = [
  [1,1,0,1],
  [1,0,0,0],
  [0,0,0,1],
  [1,1,1,1]
]

Output: 3
Explanation: 3 distinct island shapes exist.
```

---

### 💡 Intuition

To identify **distinct shapes**, we:

- Perform **DFS from each unvisited land cell (`1`)** → this is **multi-source DFS**
- Record the **path/shape relative to the starting cell** using directions (e.g., `U`, `D`, `L`, `R`)
- Use a **Set** to store unique shape signatures.

If two islands follow the same path structure (`"RRDDLU..."`), they are the same shape.

---

### 🔍 Dry Run (Example)

```
grid:
1 1 0
1 0 0
0 0 1

Island 1: starts at (0,0)
→ path: 'oD oR b b'

Island 2: starts at (2,2)
→ path: 'o'

Different shapes → 2 distinct islands
```

---

### ✅ JavaScript Code (DFS + Shape Signature)

```javascript
function numDistinctIslands(grid) {
  const rows = grid.length;
  const cols = grid[0].length;
  const shapes = new Set();

  function dfs(r, c, dir, path) {
    if (r < 0 || r >= rows || c < 0 || c >= cols || grid[r][c] === 0) return;

    grid[r][c] = 0; // Mark as visited
    path.push(dir);

    dfs(r + 1, c, "D", path); // Down
    dfs(r - 1, c, "U", path); // Up
    dfs(r, c + 1, "R", path); // Right
    dfs(r, c - 1, "L", path); // Left

    path.push("B"); // Backtrack marker
  }

  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      if (grid[r][c] === 1) {
        const path = [];
        dfs(r, c, "O", path); // Origin
        shapes.add(path.join(""));
      }
    }
  }

  return shapes.size;
}
```

---

### ⏱ Time and Space Complexity

Let:

- `m` = number of rows

- `n` = number of columns

- **Time Complexity**: `O(m × n)`
  Every cell visited once.

- **Space Complexity**: `O(m × n)`
  For recursion stack and storing unique shape strings.

---

### 📌 Summary Table

| Step               | Description                        |
| ------------------ | ---------------------------------- |
| DFS                | From every unvisited land cell     |
| Track Shape        | Using relative path encoding       |
| Backtrack Encoding | Add `'B'` to mark return direction |
| Unique Shapes      | Use Set to store encoded paths     |

---

## 🔢 **12. Bipartite Graph (DFS)**

### 📘 Problem Statement

Given an undirected graph with `V` vertices (numbered `0` to `V-1`) and edges, determine **if the graph is bipartite**.

A graph is **bipartite** if:

- We can color it using **2 colors**, such that
- **No two adjacent nodes have the same color**

Return `true` if the graph is bipartite, otherwise `false`.

---

### 🧪 Test Cases

**Test Case 1:**

```js
Input: V = 4;
Edges = [
  [0, 1],
  [1, 2],
  [2, 3],
  [3, 0],
];
Output: true;
```

**Test Case 2:**

```js
Input: V = 3;
Edges = [
  [0, 1],
  [1, 2],
  [2, 0],
];
Output: false;
```

**Test Case 3:**

```js
Input: V = 5;
Edges = [
  [0, 1],
  [0, 3],
  [1, 2],
  [2, 3],
  [3, 4],
];
Output: false;
```

---

### 💡 Intuition

A **bipartite graph** is one where we can divide the nodes into **two groups**, and:

- Every edge connects a node in one group to a node in the other.

This is equivalent to **2-coloring the graph** with **no adjacent nodes sharing the same color**.

#### ✅ Key Insight:

Use **DFS** to:

- Try assigning colors alternately (e.g., `0` and `1`)
- If we ever find two connected nodes with **same color**, return `false`

---

### 🔍 Dry Run (Test Case 2)

Edges: 0–1–2–0

1. Start DFS from 0 → color 0
2. Visit 1 → color 1
3. Visit 2 → color 0
4. 2 has neighbor 0 → conflict! Both have color 0 → ❌ not bipartite

---

### ✅ JavaScript Code (DFS)

```javascript
function isBipartite(V, edges) {
  const adj = Array.from({ length: V }, () => []);

  // Build adjacency list
  for (let [u, v] of edges) {
    adj[u].push(v);
    adj[v].push(u);
  }

  const color = new Array(V).fill(-1); // -1 means unvisited

  function dfs(node, col) {
    color[node] = col;

    for (let neighbor of adj[node]) {
      if (color[neighbor] === -1) {
        if (!dfs(neighbor, 1 - col)) return false;
      } else if (color[neighbor] === col) {
        return false; // Same color on both sides
      }
    }

    return true;
  }

  for (let i = 0; i < V; i++) {
    if (color[i] === -1) {
      if (!dfs(i, 0)) return false;
    }
  }

  return true;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity**: `O(V + E)`
  Each node and edge is visited once.

- **Space Complexity**: `O(V + E)`
  Adjacency list + recursion stack

---

### 📌 Summary Table

| Step           | Description                                |
| -------------- | ------------------------------------------ |
| Build Graph    | From edges to adjacency list               |
| Color Array    | `-1` for unvisited, `0` or `1` for colors  |
| DFS Coloring   | Alternate colors on neighbors              |
| Conflict Check | If neighbor has same color → not bipartite |

---

## 🔢 **13. Cycle Detection in Directed Graph (DFS)**

### 📘 Problem Statement

You are given a **directed graph** with `V` vertices numbered from `0 to V-1`.
Determine **if the graph contains a cycle**.

Return:

- `true` if a **cycle exists**
- `false` if the graph is **acyclic**

---

### 🧪 Test Cases

**Test Case 1:**

```js
Input: V = 4;
Edges = [
  [0, 1],
  [1, 2],
  [2, 3],
  [3, 1],
];
Output: true;
```

**Test Case 2:**

```js
Input: V = 5;
Edges = [
  [0, 1],
  [1, 2],
  [2, 3],
  [3, 4],
];
Output: false;
```

**Test Case 3:**

```js
Input: V = 3;
Edges = [
  [0, 1],
  [1, 2],
  [2, 0],
];
Output: true;
```

---

### 💡 Intuition

In a **directed graph**, a **cycle** is present when we revisit a node **while it’s still in the current DFS path**.

To track this:

- Use a `visited[]` array → marks all visited nodes
- Use a `pathVisited[]` (recursion stack) → marks nodes in the **current DFS path**
- If you visit a node already in `pathVisited[]`, a **cycle is detected**.

---

### 🔍 Dry Run (Test Case 3)

Edges:

```
0 → 1 → 2 → 0
```

DFS starts at node 0:

- visit 0 → pathVisited = \[0]
- visit 1 → pathVisited = \[0,1]
- visit 2 → pathVisited = \[0,1,2]
- 2 → 0 is back edge → 0 is already in pathVisited → ✅ Cycle found

---

### ✅ JavaScript Code (DFS)

```javascript
function hasCycleDirectedGraph(V, edges) {
  const adj = Array.from({ length: V }, () => []);

  // Build adjacency list
  for (let [u, v] of edges) {
    adj[u].push(v);
  }

  const visited = new Array(V).fill(false);
  const pathVisited = new Array(V).fill(false);

  function dfs(node) {
    visited[node] = true;
    pathVisited[node] = true;

    for (let neighbor of adj[node]) {
      if (!visited[neighbor]) {
        if (dfs(neighbor)) return true;
      } else if (pathVisited[neighbor]) {
        return true; // Cycle detected
      }
    }

    pathVisited[node] = false; // Backtrack
    return false;
  }

  for (let i = 0; i < V; i++) {
    if (!visited[i]) {
      if (dfs(i)) return true;
    }
  }

  return false;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity**: `O(V + E)`
  Every node and edge is visited once

- **Space Complexity**: `O(V)`
  For visited and pathVisited arrays + recursion stack

---

### 📌 Summary Table

| Component       | Description                                 |
| --------------- | ------------------------------------------- |
| `visited[]`     | Track all globally visited nodes            |
| `pathVisited[]` | Track current DFS path (recursion stack)    |
| Cycle condition | If `pathVisited[neighbor]` → back edge → ✅ |

---

# Topological Sort

## 🔢 **1. Topological Sort (DFS Approach)**

### 📘 Problem Statement

Given a **Directed Acyclic Graph (DAG)** with `V` vertices and edges, return any **topological ordering** of its vertices.

- A **topological sort** is a linear ordering of vertices such that for every directed edge `u → v`, vertex `u` comes **before** `v`.

> 🔔 A topological sort **only exists for DAGs** (graphs with **no cycles**).

---

### 🧪 Test Cases

**Test Case 1:**

```js
Input:
V = 6
Edges = [
  [5, 0],
  [5, 2],
  [4, 0],
  [4, 1],
  [2, 3],
  [3, 1]
]

Output: [5, 4, 2, 3, 1, 0] (or any valid topological order)
```

**Test Case 2:**

```js
Input: V = 3;
Edges = [
  [0, 1],
  [1, 2],
];

Output: [0, 1, 2];
```

---

### 💡 Intuition

Topological sorting is like scheduling tasks:
If one task depends on another, it should come **after** it in the order.

Using **DFS**:

- Perform a **post-order traversal**
- Add the current node to a `stack` **after** visiting all its neighbors
- Reverse the stack to get the correct topological order

---

### 🔍 Dry Run (Test Case 1)

Graph:

```
5 → 0
5 → 2 → 3 → 1
4 → 0
4 → 1
```

#### Steps:

- Start from 5 → explore 2 → 3 → 1 → backtrack
- Push nodes to stack in reverse finishing order
- Stack (before reversing): \[1, 3, 2, 0, 4, 5]
- Final order: **\[5, 4, 0, 2, 3, 1]**

---

### ✅ JavaScript Code (DFS)

```javascript
function topoSortDFS(V, edges) {
  const adj = Array.from({ length: V }, () => []);

  // Build adjacency list
  for (let [u, v] of edges) {
    adj[u].push(v);
  }

  const visited = new Array(V).fill(false);
  const stack = [];

  function dfs(node) {
    visited[node] = true;

    for (let neighbor of adj[node]) {
      if (!visited[neighbor]) {
        dfs(neighbor);
      }
    }

    stack.push(node); // Post-order
  }

  for (let i = 0; i < V; i++) {
    if (!visited[i]) {
      dfs(i);
    }
  }

  return stack.reverse();
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity**: `O(V + E)`
  Every node and edge is visited once

- **Space Complexity**: `O(V)`
  For `visited[]` and recursion stack

---

### 📌 Summary Table

| Component     | Description                           |
| ------------- | ------------------------------------- |
| Graph Type    | **Directed Acyclic Graph (DAG)**      |
| Method        | **DFS + post-order stack**            |
| Key Operation | Push node after all neighbors visited |
| Final Output  | Reverse the stack                     |

---

## 🔢 **2. Topological Sort – Kahn’s Algorithm (BFS)**

### 📘 Problem Statement

Given a **Directed Acyclic Graph (DAG)** with `V` vertices and a list of edges, return any **valid topological ordering** using **Kahn's Algorithm**, which is based on **BFS**.

> ✅ Valid only for DAGs (no cycles).
> 🚫 If the graph contains a cycle, topological sorting is **not possible**.

---

### 🧪 Test Cases

**Test Case 1:**

```js
Input:
V = 6,
Edges = [
  [5, 0],
  [5, 2],
  [4, 0],
  [4, 1],
  [2, 3],
  [3, 1]
]

Output: [4, 5, 2, 0, 3, 1] or [5, 4, 2, 3, 1, 0]
```

**Test Case 2:**

```js
Input: (V = 3),
  (Edges = [
    [0, 1],
    [1, 2],
  ]);

Output: [0, 1, 2];
```

---

### 💡 Intuition

Kahn’s Algorithm builds the topological order using **in-degrees** and **BFS**:

#### ✅ Key Ideas:

1. **In-degree** of a node = number of incoming edges.
2. Nodes with `in-degree = 0` can be safely put in the topological order.
3. After placing a node, reduce the in-degree of its neighbors.
4. Repeat until all nodes are placed.

---

### 🔍 Dry Run (Test Case 1)

Initial in-degrees:

```
0: 2 (from 5, 4)
1: 2 (from 4, 3)
2: 1 (from 5)
3: 1 (from 2)
4: 0
5: 0
```

Queue starts with: `[4, 5]`

Steps:

- Pop 4 → topo = \[4] → reduce in-degree of 0, 1
- Pop 5 → topo = \[4, 5] → reduce in-degree of 0, 2
- 0, 2 now have in-degree 0 → push
- Continue till done

---

### ✅ JavaScript Code (Kahn’s Algorithm)

```javascript
function topoSortKahn(V, edges) {
  const adj = Array.from({ length: V }, () => []);
  const indegree = Array(V).fill(0);

  // Build adjacency list and indegree array
  for (let [u, v] of edges) {
    adj[u].push(v);
    indegree[v]++;
  }

  const queue = [];
  const topo = [];

  // Step 1: Push nodes with 0 in-degree
  for (let i = 0; i < V; i++) {
    if (indegree[i] === 0) {
      queue.push(i);
    }
  }

  // Step 2: BFS
  while (queue.length > 0) {
    const node = queue.shift();
    topo.push(node);

    for (let neighbor of adj[node]) {
      indegree[neighbor]--;
      if (indegree[neighbor] === 0) {
        queue.push(neighbor);
      }
    }
  }

  // Step 3: Check for cycle
  return topo.length === V ? topo : []; // If topo length < V → cycle exists
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity**: `O(V + E)`
  Building graph + processing all nodes/edges once

- **Space Complexity**: `O(V + E)`
  For adjacency list and in-degree array

---

### 📌 Summary Table

| Component       | Description                        |
| --------------- | ---------------------------------- |
| Graph Type      | Directed Acyclic Graph (DAG)       |
| Approach        | BFS + In-degree                    |
| Queue           | Maintains 0 in-degree nodes        |
| Cycle Detection | If `topo.length < V`, cycle exists |

---

### 🔁 When to Use Kahn’s Algorithm vs DFS?

| Aspect          | DFS Approach         | Kahn’s Algorithm (BFS)  |
| --------------- | -------------------- | ----------------------- |
| Simpler to code | ✅ Yes               | ❌ Slightly verbose     |
| Detect cycle    | ❌ Needs extra logic | ✅ Built-in             |
| Order stability | ❌ Not unique        | ✅ Also not unique      |
| Use-case        | Reverse postorder    | Topological with layers |

---

## 🔢 **3. Cycle Detection in Directed Graph (BFS – Kahn's Algorithm)**

### 📘 Problem Statement

You are given a **directed graph** with `V` vertices and a list of edges.
Return `true` if the graph contains a **cycle**, otherwise return `false`.

> ⚠ This is a **cycle detection problem**, not a topological sort problem—but we'll use **Kahn’s Algorithm**, which inherently detects cycles.

---

### 🧪 Test Cases

**Test Case 1:**

```js
Input: V = 4;
Edges = [
  [0, 1],
  [1, 2],
  [2, 3],
  [3, 1],
];
Output: true;
```

**Test Case 2:**

```js
Input: V = 4;
Edges = [
  [0, 1],
  [1, 2],
  [2, 3],
];
Output: false;
```

**Test Case 3:**

```js
Input: V = 3;
Edges = [
  [0, 1],
  [1, 2],
  [2, 0],
];
Output: true;
```

---

### 💡 Intuition

Kahn’s Algorithm is for **topological sorting**, and it works **only for DAGs**.
Hence:

- If we **cannot perform a topological sort** (i.e., some nodes are never added to the result because of cycles), then the graph **must contain a cycle**.

---

### 🔍 Dry Run (Test Case 1)

Graph:

```
0 → 1 → 2 → 3
     ↑     ↓
     ← ← ←
```

In-degrees:

```
0 → 0
1 → 1 (from 0, and from 3)
2 → 1
3 → 1
```

Queue starts with only `0`.

Processing:

- `0 → 1 (indegree 1 → 0)` → `1 → 2` → `2 → 3` → `3 → 1 (cycle!)`

Cycle is detected because not all nodes can be processed.

---

### ✅ JavaScript Code (BFS – Kahn’s Algorithm)

```javascript
function hasCycleDirectedGraph(V, edges) {
  const adj = Array.from({ length: V }, () => []);
  const indegree = new Array(V).fill(0);

  // Build adjacency list and compute in-degrees
  for (let [u, v] of edges) {
    adj[u].push(v);
    indegree[v]++;
  }

  const queue = [];

  // Push nodes with in-degree 0
  for (let i = 0; i < V; i++) {
    if (indegree[i] === 0) queue.push(i);
  }

  let count = 0;

  while (queue.length > 0) {
    const node = queue.shift();
    count++;

    for (let neighbor of adj[node]) {
      indegree[neighbor]--;
      if (indegree[neighbor] === 0) {
        queue.push(neighbor);
      }
    }
  }

  return count !== V; // If not all nodes were processed, a cycle exists
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity**: `O(V + E)`
  Every node and edge is visited once

- **Space Complexity**: `O(V + E)`
  Adjacency list + in-degree + queue

---

### 📌 Summary Table

| Component       | Description                             |
| --------------- | --------------------------------------- |
| In-degree array | Count of incoming edges per node        |
| Queue           | Starts with nodes of in-degree 0        |
| Cycle condition | If any node left unprocessed ⇒ Cycle ✅ |

---

## 🔢 **4. Course Schedule I (Leetcode 207)**

### 📘 Problem Statement

You are given:

- An integer `numCourses` – the number of courses labeled `0` to `numCourses - 1`
- A list `prerequisites[i] = [a, b]` meaning to take course `a`, you must first take course `b`

🔁 **Return true** if it is possible to finish all courses (i.e., the graph is **acyclic**), else **return false**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input:
numCourses = 2
prerequisites = [[1, 0]]

Output: true
Explanation: Take course 0 → then course 1.
```

#### Test Case 2:

```js
Input:
numCourses = 2
prerequisites = [[1, 0], [0, 1]]

Output: false
Explanation: Cycle exists (1 → 0 → 1)
```

---

### 💡 Intuition

This is a classic **cycle detection in directed graph** problem:

- Each course is a **node**
- Each prerequisite is a **directed edge**
- If there’s a **cycle**, we can’t complete all courses

---

### ✅ Approach 1: **BFS – Kahn’s Algorithm**

#### 🔍 Idea:

- Create graph and compute `in-degree` of each node
- Start with nodes with `in-degree 0`
- Process and reduce `in-degree` of neighbors
- If all nodes are processed → no cycle → ✅

---

#### ✅ JavaScript Code (Kahn's BFS)

```javascript
function canFinish(numCourses, prerequisites) {
  const adj = Array.from({ length: numCourses }, () => []);
  const indegree = new Array(numCourses).fill(0);

  for (let [a, b] of prerequisites) {
    adj[b].push(a);
    indegree[a]++;
  }

  const queue = [];

  // Start with courses that have no prerequisites
  for (let i = 0; i < numCourses; i++) {
    if (indegree[i] === 0) queue.push(i);
  }

  let completed = 0;

  while (queue.length > 0) {
    const course = queue.shift();
    completed++;

    for (let neighbor of adj[course]) {
      indegree[neighbor]--;
      if (indegree[neighbor] === 0) {
        queue.push(neighbor);
      }
    }
  }

  return completed === numCourses;
}
```

---

### ✅ Approach 2: **DFS + Recursion Stack**

#### 🔍 Idea:

- Use `visited[]` to mark globally visited nodes
- Use `pathVisited[]` to track nodes in **current DFS path**
- If you revisit a node on the same path → cycle ❌

---

#### ✅ JavaScript Code (DFS Cycle Detection)

```javascript
function canFinish(numCourses, prerequisites) {
  const adj = Array.from({ length: numCourses }, () => []);
  for (let [a, b] of prerequisites) {
    adj[b].push(a);
  }

  const visited = new Array(numCourses).fill(false);
  const pathVisited = new Array(numCourses).fill(false);

  function dfs(node) {
    visited[node] = true;
    pathVisited[node] = true;

    for (let neighbor of adj[node]) {
      if (!visited[neighbor]) {
        if (dfs(neighbor)) return true;
      } else if (pathVisited[neighbor]) {
        return true; // Cycle
      }
    }

    pathVisited[node] = false; // backtrack
    return false;
  }

  for (let i = 0; i < numCourses; i++) {
    if (!visited[i]) {
      if (dfs(i)) return false; // Cycle detected
    }
  }

  return true; // No cycles
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity**: `O(V + E)` for both approaches
- **Space Complexity**: `O(V + E)`
  (adjacency list + visited arrays or in-degree array)

---

### 📌 Summary Table

| Concept    | Description                                |
| ---------- | ------------------------------------------ |
| Graph Type | Directed Graph                             |
| Goal       | Detect cycle → topological order possible? |
| Approach 1 | Kahn’s Algorithm (BFS using in-degrees)    |
| Approach 2 | DFS with recursion stack                   |
| Output     | `true` if all courses can be completed     |

---

## 🔢 **5. Course Schedule II (Leetcode 210)**

### 📘 Problem Statement

You are given:

- `numCourses`: Total number of courses labeled `0` to `numCourses - 1`
- `prerequisites[i] = [a, b]`: To take course `a`, you must first take course `b`

🔁 Return a valid **ordering** of courses you should take to finish all courses.
If **no valid order exists** (i.e., a cycle), return `[]`.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input:
numCourses = 4
prerequisites = [[1, 0], [2, 0], [3, 1], [3, 2]]

Output: [0, 1, 2, 3] or [0, 2, 1, 3]
```

#### Test Case 2:

```js
Input: numCourses = 2;
prerequisites = [
  [1, 0],
  [0, 1],
];

Output: [];
```

---

### 💡 Intuition

This is a **topological sorting** problem on a **directed graph**:

- Nodes = courses
- Edges = `b → a` (b is a prerequisite for a)

#### ✅ Goal:

Find a **topological order** of the graph.
If the graph contains a **cycle**, return `[]`.

---

### ✅ Approach 1: **BFS – Kahn’s Algorithm**

---

#### 🔍 Dry Run (Test Case 1)

Graph:

```
0 → 1
0 → 2
1 → 3
2 → 3
```

In-degrees:

```
0 → 0
1 → 1
2 → 1
3 → 2
```

Start with queue: `[0]`
Process 0 → reduce in-degrees → enqueue `[1,2]` → then 3 → ✅

---

#### ✅ JavaScript Code (BFS)

```javascript
function findOrder(numCourses, prerequisites) {
  const adj = Array.from({ length: numCourses }, () => []);
  const indegree = Array(numCourses).fill(0);

  for (let [a, b] of prerequisites) {
    adj[b].push(a);
    indegree[a]++;
  }

  const queue = [];
  const topo = [];

  // Start with courses having no prerequisites
  for (let i = 0; i < numCourses; i++) {
    if (indegree[i] === 0) queue.push(i);
  }

  while (queue.length > 0) {
    const course = queue.shift();
    topo.push(course);

    for (let neighbor of adj[course]) {
      indegree[neighbor]--;
      if (indegree[neighbor] === 0) {
        queue.push(neighbor);
      }
    }
  }

  return topo.length === numCourses ? topo : [];
}
```

---

### ✅ Approach 2: **DFS with Stack**

---

#### 🔍 Key Idea

- Do a DFS
- Push the node to stack **after visiting all its children** (post-order)
- Reverse the stack to get topological order
- Track recursion path to detect **cycles**

---

#### ✅ JavaScript Code (DFS + Stack)

```javascript
function findOrder(numCourses, prerequisites) {
  const adj = Array.from({ length: numCourses }, () => []);
  for (let [a, b] of prerequisites) {
    adj[b].push(a);
  }

  const visited = new Array(numCourses).fill(0); // 0=unvisited, 1=visiting, 2=visited
  const stack = [];
  let isCycle = false;

  function dfs(node) {
    if (visited[node] === 1) {
      isCycle = true;
      return;
    }
    if (visited[node] === 2) return;

    visited[node] = 1;

    for (let neighbor of adj[node]) {
      dfs(neighbor);
    }

    visited[node] = 2;
    stack.push(node);
  }

  for (let i = 0; i < numCourses; i++) {
    if (visited[i] === 0) dfs(i);
  }

  return isCycle ? [] : stack.reverse();
}
```

---

### ⏱ Time and Space Complexity

Let `V = numCourses`, `E = prerequisites.length`

- **Time Complexity**: `O(V + E)`
  (BFS or DFS traverses every edge and node once)

- **Space Complexity**: `O(V + E)`
  For graph, queue/stack, and visited tracking

---

### 📌 Summary Table

| Feature             | Kahn’s Algorithm (BFS)    | DFS + Stack                   |
| ------------------- | ------------------------- | ----------------------------- |
| Cycle Detection     | Implicit (by topo length) | Explicit (via recursion path) |
| Output Order        | In queue order            | Reverse of post-order         |
| Easy to Understand  | ✅ Yes                    | ⚠ Slightly more involved      |
| Stable for Leetcode | ✅ Yes                    | ✅ Yes                        |

---

## 🔢 **6. Find Eventual Safe States**

### 📘 Problem Statement

You are given a **directed graph**, where `graph[i]` is a list of nodes that node `i` points to.

A node is a **safe node** if **every path starting from that node eventually ends at a terminal node** (i.e., no cycles along any path).

🔁 Return a list of **all safe nodes**, sorted in **ascending order**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: graph = [[1, 2], [2, 3], [5], [0], [5], [], []];
Output: [2, 4, 5, 6];
```

#### Test Case 2:

```js
Input: graph = [[1, 2, 3, 4], [1, 2], [3, 4], [0, 4], []];
Output: [4];
```

---

### 💡 Intuition

This is essentially a **cycle detection** problem in disguise.

- If a node is **part of a cycle** or **can reach a cycle**, it is **not safe**
- A **safe node** will eventually reach only **terminal nodes**

#### ✅ Strategy (DFS + Coloring)

- Use `visited[]` or a `color[]` array:

  - `0` → unvisited
  - `1` → visiting (on recursion stack)
  - `2` → safe (fully processed, no cycles)

---

### 🔍 Dry Run (Test Case 1)

```
graph = [[1,2],[2,3],[5],[0],[5],[],[]]

Visual:
0 → 1 → 2 → 5 ✅
       ↘
        3 → 0 ❌ (cycle)
4 → 5 ✅
6 (no outgoing edge) ✅

Safe nodes = [2, 4, 5, 6]
```

---

### ✅ JavaScript Code (DFS Coloring)

```javascript
function eventualSafeNodes(graph) {
  const n = graph.length;
  const color = new Array(n).fill(0); // 0=unvisited, 1=visiting, 2=safe
  const result = [];

  function dfs(node) {
    if (color[node] !== 0) return color[node] === 2;

    color[node] = 1; // Mark as visiting

    for (let neighbor of graph[node]) {
      if (!dfs(neighbor)) return false;
    }

    color[node] = 2; // Mark as safe
    return true;
  }

  for (let i = 0; i < n; i++) {
    if (dfs(i)) {
      result.push(i);
    }
  }

  return result;
}
```

---

### ⏱ Time and Space Complexity

Let `V = graph.length`, `E = total edges`:

- **Time Complexity**: `O(V + E)`
  Each node and edge is processed once

- **Space Complexity**: `O(V)`
  For `color[]` and recursion stack

---

### 📌 Summary Table

| Concept     | Description                                 |
| ----------- | ------------------------------------------- |
| Safe node   | No cycle in any outgoing path               |
| Unsafe node | Involved in a cycle or can reach one        |
| Key trick   | DFS + 3-color marking to detect cycles      |
| Output      | List of all `safe nodes` in ascending order |

---

## 🔢 **7. Alien Dictionary**

### 📘 Problem Statement

You are given a list of words in a **dictionary sorted in alien language** order.

🧩 Your task:

- Derive the **order of characters** in the alien language.
- Return a **string** representing a valid order of the characters.
- If no valid order exists (i.e., there's a cycle), return `""`.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: words = ["wrt", "wrf", "er", "ett", "rftt"];
Output: "wertf";
```

#### Test Case 2:

```js
Input: words = ["z", "x", "z"];
Output: ""; // cycle: z -> x -> z
```

#### Test Case 3:

```js
Input: words = ["abc", "ab"];
Output: ""; // Invalid input: prefix order is wrong
```

---

### 💡 Intuition

Think of each word as establishing a **partial order** between characters.

Compare adjacent words:

- Find the **first differing character**
- That gives a constraint: `char1 < char2` → **directed edge: char1 → char2**

👉 Now this becomes a **topological sorting problem** on characters.

---

### 🔍 Dry Run (Test Case 1)

```txt
Input: ["wrt","wrf","er","ett","rftt"]

From comparisons:
"wrt" vs "wrf" → t < f → t → f
"wrf" vs "er"  → w < e → w → e
"er" vs "ett" → r < t → r → t
"ett" vs "rftt" → e < r → e → r

Final Graph:
w → e → r → t → f
```

Topological order: **w e r t f**

---

### ✅ JavaScript Code (Kahn’s Algorithm – BFS)

```javascript
function alienOrder(words) {
  const adj = {}; // adjacency list
  const indegree = {}; // indegree count

  // Initialize graph nodes
  for (let word of words) {
    for (let char of word) {
      adj[char] = new Set();
      indegree[char] = 0;
    }
  }

  // Build the graph
  for (let i = 0; i < words.length - 1; i++) {
    let w1 = words[i];
    let w2 = words[i + 1];
    if (w1.length > w2.length && w1.startsWith(w2)) return ""; // invalid input

    for (let j = 0; j < Math.min(w1.length, w2.length); j++) {
      if (w1[j] !== w2[j]) {
        if (!adj[w1[j]].has(w2[j])) {
          adj[w1[j]].add(w2[j]);
          indegree[w2[j]]++;
        }
        break;
      }
    }
  }

  // Kahn’s Algorithm (BFS)
  const queue = [];
  const result = [];

  for (let char in indegree) {
    if (indegree[char] === 0) queue.push(char);
  }

  while (queue.length) {
    const node = queue.shift();
    result.push(node);

    for (let neighbor of adj[node]) {
      indegree[neighbor]--;
      if (indegree[neighbor] === 0) queue.push(neighbor);
    }
  }

  return result.length === Object.keys(indegree).length ? result.join("") : "";
}
```

---

### ⏱ Time and Space Complexity

Let `C = total unique characters`, `W = number of words`, `E = number of edges`.

- **Time Complexity**: `O(C + W × L)`

  - Build graph by comparing pairs → O(W × L)
  - Topo sort → O(C + E)

- **Space Complexity**: `O(C + E)`

  - For adjacency list and indegree map

---

### 📌 Summary Table

| Step                 | Description                                  |
| -------------------- | -------------------------------------------- |
| Build Graph          | From first differing chars in adjacent words |
| Check invalid prefix | If w1 > w2 and w1 startsWith w2              |
| Topo Sort with BFS   | Use in-degree and queue                      |
| Return result or ""  | Return "" if cycle is detected               |

---

### 🧠 DFS-Based Alternative (with cycle detection)

Would you like the **DFS (with color marking)** version as well?

---

# **Shortest Path Alogorithms**

## 🔢 **1. Shortest Path in Undirected Graph with Unit Weights**

### 📘 Problem Statement

You are given:

- An **undirected graph** with `V` vertices and `E` edges.
- The edges have **unit weight** (all weights = 1).
- A `source` node.

🔁 Your task is to find the **shortest path (minimum number of edges)** from the source to all other nodes.

> 🚨 You can return an array where `ans[i]` is the shortest distance from `source` to node `i`.
> If a node is **unreachable**, set its distance to `-1`.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: V = 5;
Edges = [
  [0, 1],
  [0, 2],
  [1, 3],
  [2, 4],
];
Source = 0;

Output: [0, 1, 1, 2, 2];
```

#### Test Case 2:

```js
Input: V = 4;
Edges = [
  [0, 1],
  [1, 2],
];
Source = 0;

Output: [0, 1, 2, -1]; // Node 3 is disconnected
```

---

### 💡 Intuition

This is a **graph traversal** problem where all edge weights = 1.

👉 So, instead of Dijkstra’s Algorithm, we use **BFS**:

- BFS explores the graph in **layers**, making it perfect for finding **shortest path** in **unit weight graphs**.

---

### 🔍 Dry Run (Test Case 1)

Graph:

```
     0
    / \
   1   2
   |    \
   3     4

Start from 0:
- Distance[0] = 0
- Visit 1, 2 → distance = 1
- Visit 3 (from 1), 4 (from 2) → distance = 2
```

---

### ✅ JavaScript Code (BFS)

```javascript
function shortestPathUG(V, edges, source) {
  const adj = Array.from({ length: V }, () => []);
  const distance = Array(V).fill(-1);
  const visited = Array(V).fill(false);

  // Build adjacency list
  for (let [u, v] of edges) {
    adj[u].push(v);
    adj[v].push(u); // undirected
  }

  const queue = [];
  queue.push(source);
  visited[source] = true;
  distance[source] = 0;

  while (queue.length > 0) {
    const node = queue.shift();

    for (let neighbor of adj[node]) {
      if (!visited[neighbor]) {
        visited[neighbor] = true;
        distance[neighbor] = distance[node] + 1;
        queue.push(neighbor);
      }
    }
  }

  return distance;
}
```

---

### ⏱ Time and Space Complexity

Let `V = number of vertices`, `E = number of edges`

- **Time Complexity**: `O(V + E)`

  - Each node and edge is visited once

- **Space Complexity**: `O(V + E)`

  - Adjacency list + distance + queue

---

### 📌 Summary Table

| Feature        | Description                        |
| -------------- | ---------------------------------- |
| Graph Type     | Undirected                         |
| Edge Weights   | Unit (All = 1)                     |
| Traversal Used | BFS                                |
| Suitable For   | Shortest path in UG with unit cost |

---

## 🔢 **2. Shortest Path in a DAG (Directed Acyclic Graph)**

### 📘 Problem Statement

You are given:

- A **Directed Acyclic Graph (DAG)** with `V` vertices and `E` edges.
- Each edge has a **weight** (not necessarily 1).
- A `source` node.

🔁 Find the **shortest distances** from the source node to every other node.
If a node is **unreachable**, return `Infinity` or `-1` for that node.

---

### 🧪 Test Case

#### Test Case:

```js
Input: (V = 6),
  (Edges = [
    [0, 1, 2],
    [0, 4, 1],
    [1, 2, 3],
    [4, 2, 2],
    [2, 3, 6],
    [4, 5, 4],
    [5, 3, 1],
  ]);
Source = 0;

Output: [0, 2, 3, 6, 1, 5]; // shortest distance from 0 to each node
```

---

### 💡 Intuition

Since the graph is a **DAG**, we can:

1. Perform **Topological Sort**.
2. **Relax edges** in the **topological order**.

Why this works:

- Topo sort ensures that when we process a node, **all its prerequisites (ancestors) are already processed**.
- Hence, we can safely update distances.

---

### 🔍 Dry Run (Step-by-step)

Topo Order for above DAG: `[0, 4, 1, 5, 2, 3]`

Initialize distance:

```js
dist = [0, ∞, ∞, ∞, ∞, ∞]
```

Process nodes in topo order:

- From 0 → 1 (dist\[1] = 2), 4 (dist\[4] = 1)
- From 4 → 2 (dist\[2] = min(∞, 1+2) = 3), 5 (dist\[5] = 5)
- From 1 → 2 (dist\[2] = min(3, 2+3) = 3)
- From 5 → 3 (dist\[3] = min(∞, 5+1) = 6)
- From 2 → 3 (dist\[3] = min(6, 3+6) = 6)

Final distances: `[0, 2, 3, 6, 1, 5]`

---

### ✅ JavaScript Code

```javascript
function shortestPathDAG(V, edges, source) {
  const adj = Array.from({ length: V }, () => []);

  // Build graph
  for (let [u, v, wt] of edges) {
    adj[u].push([v, wt]);
  }

  // Step 1: Topological Sort (DFS)
  const visited = new Array(V).fill(false);
  const stack = [];

  function dfs(node) {
    visited[node] = true;
    for (let [neighbor] of adj[node]) {
      if (!visited[neighbor]) {
        dfs(neighbor);
      }
    }
    stack.push(node);
  }

  for (let i = 0; i < V; i++) {
    if (!visited[i]) dfs(i);
  }

  // Step 2: Relax edges using topological order
  const dist = new Array(V).fill(Infinity);
  dist[source] = 0;

  while (stack.length > 0) {
    const node = stack.pop();

    if (dist[node] !== Infinity) {
      for (let [neighbor, weight] of adj[node]) {
        if (dist[node] + weight < dist[neighbor]) {
          dist[neighbor] = dist[node] + weight;
        }
      }
    }
  }

  return dist.map((d) => (d === Infinity ? -1 : d));
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity**: `O(V + E)`

  - Topo sort: O(V + E)
  - Relax edges: O(V + E)

- **Space Complexity**: `O(V + E)`

  - Adjacency list + stack + distance array

---

### 📌 Summary Table

| Feature                  | Description                   |
| ------------------------ | ----------------------------- |
| Graph Type               | Directed Acyclic Graph (DAG)  |
| Edge Weights             | Any (positive or zero)        |
| Traversal Used           | Topological Sort + Relaxation |
| Handles Negative Weights | ✅ Yes (no cycles)            |

---

## 🔢 **3. Dijkstra’s Algorithm (Shortest Path in Weighted Graph – Non-negative Weights)**

### 📘 Problem Statement

You are given:

- A **weighted graph** with `V` vertices and `E` edges.
- All edge weights are **non-negative**.
- A **source** node.

🔁 Your task is to find the **shortest distance from the source node** to every other node.

---

### 🧪 Test Case

#### Test Case:

```js
Input: V = 5;
Edges = [
  [0, 1, 2],
  [0, 2, 4],
  [1, 2, 1],
  [1, 3, 7],
  [2, 4, 3],
  [3, 4, 1],
];
Source = 0;

Output: [0, 2, 3, 9, 6];
```

#### Explanation:

- Shortest path from 0 to 2: 0 → 1 → 2 (cost = 3)
- Shortest path from 0 to 4: 0 → 1 → 2 → 4 (cost = 6)

---

### 💡 Intuition

Dijkstra's Algorithm works like BFS but uses a **priority queue (min-heap)** to always process the **closest unvisited node** first.

It **guarantees the shortest path** in graphs with **non-negative weights**.

---

### 🔍 Dry Run

#### Starting from node 0:

```txt
dist = [0, ∞, ∞, ∞, ∞]
Heap = [[0, 0]]

Step 1: Pop [0, 0]
→ Relax 0→1 (dist[1] = 2), 0→2 (dist[2] = 4)

Step 2: Pop [2, 1]
→ Relax 1→2 (dist[2] = min(4, 2+1) = 3), 1→3 (dist[3] = 2+7 = 9)

Step 3: Pop [3, 2]
→ Relax 2→4 (dist[4] = 3+3 = 6)

Step 4: Pop [6, 4] → 4→ done
Step 5: Pop [9, 3] → done
```

Final `dist`: `[0, 2, 3, 9, 6]`

---

### ✅ JavaScript Code (Using Min Heap / Priority Queue)

```javascript
class MinHeap {
  constructor() {
    this.heap = [];
  }

  push([dist, node]) {
    this.heap.push([dist, node]);
    this.heap.sort((a, b) => a[0] - b[0]); // maintain min-heap
  }

  pop() {
    return this.heap.shift();
  }

  isEmpty() {
    return this.heap.length === 0;
  }
}

function dijkstra(V, edges, source) {
  const adj = Array.from({ length: V }, () => []);
  for (let [u, v, wt] of edges) {
    adj[u].push([v, wt]);
    adj[v].push([u, wt]); // remove if directed
  }

  const dist = new Array(V).fill(Infinity);
  dist[source] = 0;

  const minHeap = new MinHeap();
  minHeap.push([0, source]);

  while (!minHeap.isEmpty()) {
    const [currentDist, node] = minHeap.pop();

    for (let [neighbor, weight] of adj[node]) {
      if (currentDist + weight < dist[neighbor]) {
        dist[neighbor] = currentDist + weight;
        minHeap.push([dist[neighbor], neighbor]);
      }
    }
  }

  return dist;
}
```

---

### ⏱ Time and Space Complexity

Let `V = number of vertices`, `E = number of edges`

- **Time Complexity**:

  - Using binary heap: `O((V + E) log V)`
  - Naive array-based heap: `O(V^2)`

- **Space Complexity**: `O(V + E)`

---

### 📌 Summary Table

| Feature        | Description                                  |
| -------------- | -------------------------------------------- |
| Graph Type     | Weighted (non-negative), Directed/Undirected |
| Edge Weights   | ✅ Non-negative only                         |
| Traversal Used | BFS with priority queue                      |
| Output         | Shortest distance from source to all nodes   |
| Priority Queue | Stores \[distance, node] pairs               |

---

### ❗ Dijkstra’s Algorithm vs Others

| Algorithm             | Handles Negative Weights? | Supports Cycles? | Weighted Graph? | Technique           |
| --------------------- | ------------------------- | ---------------- | --------------- | ------------------- |
| **Dijkstra**          | ❌ No                     | ✅ Yes           | ✅ Yes          | Greedy + Min Heap   |
| **Bellman-Ford**      | ✅ Yes                    | ✅ Yes           | ✅ Yes          | Dynamic Programming |
| **BFS** (Unit Weight) | ✅ N/A                    | ✅ Yes           | ✅ Only unit    | BFS Layer-wise      |

---

## 🔢 **4. Shortest Path in a Binary Maze**

### 📘 Problem Statement

You are given a **2D binary matrix `grid`** of size `n x m`:

- `0` represents **walls** (cannot pass)
- `1` represents **open paths** (can move)

Also given:

- A **source cell**: `[srcRow, srcCol]`
- A **destination cell**: `[destRow, destCol]`

🔁 Find the **minimum number of steps** required to reach the destination from the source using **4-directional movement (up, down, left, right)**.
If the destination is **not reachable**, return `-1`.

---

### 🧪 Test Case

#### Test Case 1:

```js
Input: grid = [
  [1, 0, 1, 1],
  [1, 1, 1, 0],
  [0, 1, 0, 1],
];
src = [0, 0];
dest = [2, 3];

Output: 5;
```

#### Explanation:

Path:
`(0,0) → (1,0) → (1,1) → (1,2) → (2,1) → (2,3)` → steps = 5

---

### 💡 Intuition

This is a classic **shortest path in grid** problem with **unit weights**.

✅ So, we can use **BFS** from the source:

- Track visited cells
- Track distance as levels in BFS

---

### 🔍 Dry Run

Grid:

```
1 0 1 1
1 1 1 0
0 1 0 1
```

Start from (0,0)

- Move to (1,0) → dist = 1
- Then to (1,1) → dist = 2
- Then to (1,2) → dist = 3
- Then to (2,1) → dist = 4
- Then to (2,3) → dist = 5 ✅

---

### ✅ JavaScript Code (BFS)

```javascript
function shortestPathBinaryMaze(grid, source, destination) {
  const n = grid.length;
  const m = grid[0].length;

  const [srcX, srcY] = source;
  const [destX, destY] = destination;

  if (grid[srcX][srcY] === 0 || grid[destX][destY] === 0) return -1;

  const visited = Array.from({ length: n }, () => Array(m).fill(false));
  const queue = [];
  const dirs = [
    [0, 1],
    [1, 0],
    [0, -1],
    [-1, 0],
  ];

  queue.push([srcX, srcY, 0]); // [x, y, distance]
  visited[srcX][srcY] = true;

  while (queue.length > 0) {
    const [x, y, dist] = queue.shift();

    if (x === destX && y === destY) return dist;

    for (let [dx, dy] of dirs) {
      const newX = x + dx;
      const newY = y + dy;

      if (
        newX >= 0 &&
        newX < n &&
        newY >= 0 &&
        newY < m &&
        grid[newX][newY] === 1 &&
        !visited[newX][newY]
      ) {
        visited[newX][newY] = true;
        queue.push([newX, newY, dist + 1]);
      }
    }
  }

  return -1; // not reachable
}
```

---

### ⏱ Time and Space Complexity

Let `n = rows`, `m = columns`

- **Time Complexity**: `O(n * m)`

  - Each cell is visited at most once

- **Space Complexity**: `O(n * m)`

  - For queue and visited matrix

---

### 📌 Summary Table

| Feature      | Description                       |
| ------------ | --------------------------------- |
| Grid Type    | 2D matrix with 0/1                |
| Movement     | 4-directional (↑ ↓ ← →)           |
| Edge Weights | Unit weights → use BFS            |
| Output       | Minimum number of steps to target |

---

## 🔢 **5. Path With Minimum Effort**

### 📘 Problem Statement

You are given an `m x n` grid of integers `heights[][]` representing the height at each cell.

🏔 You can move in **4 directions** (up, down, left, right).

🔁 Your task is to find a path from **(0, 0)** to **(m-1, n-1)** such that the **maximum absolute difference** in heights between adjacent cells along the path is **minimized**.

Return the **minimum effort** required to travel.

---

### 🧪 Test Case

#### Test Case:

```js
Input: heights = [
  [1, 2, 2],
  [3, 8, 2],
  [5, 3, 5],
];

Output: 2;
```

#### Explanation:

Path: (0,0) → (0,1) → (0,2) → (1,2) → (2,2)
Max height difference = `|2 - 2| = 0`, `|2 - 2| = 0`, `|2 - 5| = 3`, but the optimal path has max difference **2**.

---

### 💡 Intuition

You are minimizing the **maximum effort** along the path.

#### ⛳ Approaches:

1. **Dijkstra's Algorithm**: Treat effort as cost and update shortest effort per cell.
2. **Binary Search + BFS/DFS**: Binary search on the "effort", check if a valid path exists.

Let’s cover **Approach 1** (Dijkstra’s Algo) first.

---

### ✅ Approach 1: Dijkstra's Algorithm (Effort as Distance)

- Each cell is a node.
- The **effort to go from (x1, y1) to (x2, y2)** is `abs(heights[x1][y1] - heights[x2][y2])`
- We want to **minimize the max effort** encountered from start to destination.

So:

- Instead of adding weights, use `Math.max(current effort, diff)`
- Use a **min heap** to always process the cell with **smallest effort so far**

---

#### ✅ JavaScript Code – Dijkstra Approach

```javascript
function minimumEffortPath(heights) {
  const m = heights.length;
  const n = heights[0].length;

  const effort = Array.from({ length: m }, () => Array(n).fill(Infinity));
  effort[0][0] = 0;

  const directions = [
    [0, 1],
    [1, 0],
    [0, -1],
    [-1, 0],
  ];
  const heap = [[0, 0, 0]]; // [effort, row, col]

  while (heap.length > 0) {
    heap.sort((a, b) => a[0] - b[0]); // mimic priority queue
    const [currentEffort, x, y] = heap.shift();

    if (x === m - 1 && y === n - 1) return currentEffort;

    for (let [dx, dy] of directions) {
      const nx = x + dx,
        ny = y + dy;
      if (nx >= 0 && nx < m && ny >= 0 && ny < n) {
        const diff = Math.abs(heights[x][y] - heights[nx][ny]);
        const newEffort = Math.max(currentEffort, diff);

        if (newEffort < effort[nx][ny]) {
          effort[nx][ny] = newEffort;
          heap.push([newEffort, nx, ny]);
        }
      }
    }
  }

  return 0;
}
```

---

### 🔍 Dry Run on Test Case

```txt
Start at (0,0) → height 1
Move to (0,1) → diff = 1
Move to (0,2) → diff = 0
Move to (1,2) → diff = 0
Move to (2,2) → diff = 0

Max diff = 1 → but (1,1) has height 8 → going via it costs 5 or 6

Path (0,0) → (1,0) → (2,0) → (2,1) → (2,2): diff = 2 ✅
```

---

### ⏱ Time and Space Complexity

Let `V = m * n` and `E = 4V` (each cell has at most 4 edges)

- **Time Complexity**: `O(V log V)` (optimized with a real heap)
- **Space Complexity**: `O(V)` for effort matrix and priority queue

---

### ✅ Approach 2: Binary Search + BFS

- **Binary Search** on effort range `[0, max height diff]`
- For each mid-effort, check: “Can I reach (m-1, n-1) using only edges with diff ≤ mid?”
- Use BFS to check path feasibility

---

#### ✅ JavaScript Code – Binary Search + BFS

```javascript
function minimumEffortPath(heights) {
  const m = heights.length,
    n = heights[0].length;
  const directions = [
    [0, 1],
    [1, 0],
    [0, -1],
    [-1, 0],
  ];

  const isReachable = (maxEffort) => {
    const visited = Array.from({ length: m }, () => Array(n).fill(false));
    const queue = [[0, 0]];
    visited[0][0] = true;

    while (queue.length) {
      const [x, y] = queue.shift();
      if (x === m - 1 && y === n - 1) return true;

      for (let [dx, dy] of directions) {
        const nx = x + dx,
          ny = y + dy;
        if (
          nx >= 0 &&
          nx < m &&
          ny >= 0 &&
          ny < n &&
          !visited[nx][ny] &&
          Math.abs(heights[x][y] - heights[nx][ny]) <= maxEffort
        ) {
          visited[nx][ny] = true;
          queue.push([nx, ny]);
        }
      }
    }

    return false;
  };

  let low = 0,
    high = 1e6,
    answer = 0;
  while (low <= high) {
    const mid = Math.floor((low + high) / 2);
    if (isReachable(mid)) {
      answer = mid;
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }

  return answer;
}
```

---

### 📌 Summary Table

| Feature    | Description                               |
| ---------- | ----------------------------------------- |
| Graph Type | Grid with weights = abs(height diff)      |
| Goal       | Minimize max height difference along path |
| Traversal  | Dijkstra or Binary Search + BFS/DFS       |
| Output     | Minimum required effort                   |

---

## 🔢 **6. Cheapest Flights Within K Stops**

### 📘 Problem Statement

You are given:

- `n` cities (numbered `0` to `n-1`)
- A list of `flights[] = [from, to, price]`
- A `source` city, `destination` city, and `k` (maximum number of **stops**, not edges)

🎯 Return the **minimum cost** to travel from source to destination with at most `k` **stops** (i.e., `k+1` flights).

🔁 If such a route does **not exist**, return `-1`.

---

### 🧪 Test Case

#### Test Case 1:

```js
(n = 4),
  (flights = [
    [0, 1, 100],
    [1, 2, 100],
    [2, 3, 100],
    [0, 3, 500],
  ]);
(src = 0), (dst = 3), (k = 1);

Output: 500;
```

👉 Cheapest with ≤1 stop: 0 → 3 (cost 500)

---

### 💡 Intuition

We need to find the **cheapest path** with **at most k stops**. Traditional Dijkstra won't work directly because it doesn't limit stops.

We need either:

- **Modified Dijkstra** (tracking number of stops)
- **BFS traversal** with stops level-wise

---

### ✅ Approach 1: **BFS (Queue Based)** – Stops as Levels

At each level (stop), try to expand to neighboring flights.

#### Steps:

1. Build an adjacency list.
2. Use a queue: `[currentNode, totalCost, stopsSoFar]`
3. At each level:

   - If current node is the destination → update `minCost`
   - Else, expand neighbors if stops ≤ k

---

#### ✅ JavaScript Code (BFS Approach)

```javascript
function findCheapestPrice(n, flights, src, dst, k) {
  const adj = Array.from({ length: n }, () => []);
  for (let [u, v, w] of flights) {
    adj[u].push([v, w]);
  }

  const queue = [[src, 0, 0]]; // [node, cost, stops]
  const minCost = new Array(n).fill(Infinity);
  minCost[src] = 0;

  while (queue.length) {
    const [node, cost, stops] = queue.shift();

    if (stops > k) continue;

    for (let [nei, price] of adj[node]) {
      if (cost + price < minCost[nei]) {
        minCost[nei] = cost + price;
        queue.push([nei, cost + price, stops + 1]);
      }
    }
  }

  return minCost[dst] === Infinity ? -1 : minCost[dst];
}
```

---

### 🔍 Dry Run

Flights:

```txt
0 → 1 (100)
1 → 2 (100)
2 → 3 (100)
0 → 3 (500)
```

Start from 0:

- 0 → 1 → 2 → 3 (stops = 3) → invalid if k = 1
- 0 → 3 → cost = 500 → valid

---

### ✅ Approach 2: Modified Dijkstra (Min Heap)

Track:

- Current node
- Cost so far
- Stops so far

Use a priority queue (min-heap) to always expand cheapest option **first**, but allow only `k+1` hops.

---

#### ✅ JavaScript Code (Dijkstra Variation)

```javascript
function findCheapestPrice(n, flights, src, dst, k) {
  const adj = Array.from({ length: n }, () => []);
  for (let [u, v, w] of flights) {
    adj[u].push([v, w]);
  }

  const heap = [[0, src, 0]]; // [cost, node, stops]

  while (heap.length) {
    heap.sort((a, b) => a[0] - b[0]); // mimic min-heap
    const [cost, node, stops] = heap.shift();

    if (node === dst) return cost;
    if (stops > k) continue;

    for (let [nei, price] of adj[node]) {
      heap.push([cost + price, nei, stops + 1]);
    }
  }

  return -1;
}
```

---

### ⏱ Time and Space Complexity

Let `V = number of cities`, `E = number of flights`

- **Time Complexity**:

  - BFS: `O(k × E)` → every edge explored up to `k` stops
  - Dijkstra: `O(E log V)` if optimized heap used

- **Space Complexity**: `O(V + E)`

---

### 📌 Summary Table

| Feature    | Description                               |
| ---------- | ----------------------------------------- |
| Graph Type | Directed weighted graph (flights)         |
| Stops      | Max k stops → limit on path length        |
| Strategy   | BFS (level-wise) or Dijkstra (with stops) |
| Output     | Minimum cost with ≤ k stops               |

---

## 🔢 **7. Network Delay Time**

### 📘 Problem Statement

You are given:

- A **directed weighted graph** with `n` nodes labeled `1` to `n`.
- A list of **edges** `times[] = [u, v, wt]` meaning **signal takes `wt` time to go from `u` to `v`**.
- A **starting node** `k`.

🎯 Find the **time it takes for all nodes** to receive the signal from node `k`.

🔁 If **any node is unreachable**, return `-1`.

---

### 🧪 Test Case

```js
Input: times = [
  [2, 1, 1],
  [2, 3, 1],
  [3, 4, 1],
];
(n = 4), (k = 2);

Output: 2;
```

#### Explanation:

- From node 2:
  → to 1: 1
  → to 3: 1
  → to 4: 2 (via 3)
- Max time among all = **2**

---

### 💡 Intuition

We need to compute **shortest time from source `k` to all nodes** in a **directed graph with positive weights**.

✅ So, **Dijkstra’s Algorithm** is the best fit.

---

### 🔍 Dry Run

Graph:

```txt
2 → 1 (1)
2 → 3 (1)
3 → 4 (1)
```

Dijkstra from 2:

- dist\[2] = 0
- Visit 1 → dist\[1] = 1
- Visit 3 → dist\[3] = 1
- Visit 4 → dist\[4] = 2

All nodes reached → max(dist) = 2 ✅

---

### ✅ JavaScript Code – Dijkstra's Algorithm

```javascript
function networkDelayTime(times, n, k) {
  const adj = Array.from({ length: n + 1 }, () => []);
  for (let [u, v, w] of times) {
    adj[u].push([v, w]);
  }

  const dist = Array(n + 1).fill(Infinity);
  dist[k] = 0;

  const heap = [[0, k]]; // [cost, node]

  while (heap.length) {
    heap.sort((a, b) => a[0] - b[0]); // min heap
    const [time, node] = heap.shift();

    for (let [nei, wt] of adj[node]) {
      if (time + wt < dist[nei]) {
        dist[nei] = time + wt;
        heap.push([dist[nei], nei]);
      }
    }
  }

  let maxTime = Math.max(...dist.slice(1)); // ignore 0-index
  return maxTime === Infinity ? -1 : maxTime;
}
```

---

### ✅ Alternative: Bellman-Ford (If negative weights)

```javascript
function networkDelayTime(times, n, k) {
  const dist = Array(n + 1).fill(Infinity);
  dist[k] = 0;

  for (let i = 1; i <= n - 1; i++) {
    for (let [u, v, w] of times) {
      if (dist[u] !== Infinity && dist[u] + w < dist[v]) {
        dist[v] = dist[u] + w;
      }
    }
  }

  const maxTime = Math.max(...dist.slice(1));
  return maxTime === Infinity ? -1 : maxTime;
}
```

---

### ⏱ Time and Space Complexity

Let `V = n`, `E = times.length`

| Approach         | Time Complexity    | Space Complexity |
| ---------------- | ------------------ | ---------------- |
| **Dijkstra**     | `O((E + V) log V)` | `O(V + E)`       |
| **Bellman-Ford** | `O(V * E)`         | `O(V)`           |

---

### 📌 Summary Table

| Feature    | Description                      |
| ---------- | -------------------------------- |
| Graph Type | Directed, weighted               |
| Goal       | Minimum time to reach all nodes  |
| Strategy   | Dijkstra (positive weights)      |
| Output     | Max of shortest distances from k |

---

## 🔢 **8. Number of Ways to Arrive at Destination**

### 📘 Problem Statement

You are given:

- A graph with `n` nodes (0-indexed).
- A list of edges `roads[] = [u, v, time]` (bidirectional and weighted).
- You start at node `0`, and want to reach node `n - 1`.

🎯 Return the **number of distinct shortest paths** from node `0` to node `n - 1`.

> Since the number can be large, return it modulo **10⁹ + 7**.

---

### 🧪 Test Case

```js
Input: n = 7;
roads = [
  [0, 6, 7],
  [0, 1, 2],
  [1, 2, 3],
  [1, 3, 3],
  [6, 3, 3],
  [3, 5, 1],
  [6, 5, 1],
  [2, 5, 1],
  [0, 4, 5],
  [4, 6, 2],
];

Output: 4;
```

---

### 💡 Intuition

We need to:

1. **Find the shortest time to reach node `n - 1`** → use **Dijkstra**.
2. **Count how many different ways** to reach node `n - 1` with that shortest time.

So while running Dijkstra:

- For each node, track:

  - `dist[i]`: shortest distance from `0` to `i`
  - `ways[i]`: number of ways to reach `i` in `dist[i]` time

---

### 🔍 Dry Run (Short Concept)

- For each node we pop from heap:

  - If a shorter path to `neighbor` is found → update `dist` and set `ways[neighbor] = ways[curr]`
  - If **same** distance is found again → `ways[neighbor] += ways[curr]`

---

### ✅ JavaScript Code

```javascript
function countPaths(n, roads) {
  const mod = 1e9 + 7;

  const adj = Array.from({ length: n }, () => []);
  for (let [u, v, wt] of roads) {
    adj[u].push([v, wt]);
    adj[v].push([u, wt]); // bidirectional
  }

  const dist = Array(n).fill(Infinity);
  const ways = Array(n).fill(0);
  const heap = [[0, 0]]; // [distance, node]

  dist[0] = 0;
  ways[0] = 1;

  while (heap.length) {
    heap.sort((a, b) => a[0] - b[0]); // min heap
    const [currDist, node] = heap.shift();

    for (let [nei, wt] of adj[node]) {
      if (currDist + wt < dist[nei]) {
        dist[nei] = currDist + wt;
        ways[nei] = ways[node];
        heap.push([dist[nei], nei]);
      } else if (currDist + wt === dist[nei]) {
        ways[nei] = (ways[nei] + ways[node]) % mod;
      }
    }
  }

  return ways[n - 1];
}
```

---

### ⏱ Time and Space Complexity

Let `V = number of nodes`, `E = number of edges`

- **Time Complexity**: `O((V + E) log V)` (with heap optimization)
- **Space Complexity**: `O(V + E)`

---

### 📌 Summary Table

| Feature    | Description                          |
| ---------- | ------------------------------------ |
| Graph Type | Weighted undirected                  |
| Goal       | Count shortest paths from 0 to n - 1 |
| Strategy   | Dijkstra + path count array          |
| Output     | Number of ways modulo 10⁹+7          |

---

## 🔢 **9. Minimum Steps to Reach End by Multiplication & Mod**

### 📘 Problem Statement

You are given:

- An integer array `arr[]` of size `n`, where each element `arr[i]` is a **positive integer**.
- An integer `start` and an integer `end`.
- You can perform **any number of operations**, and in each operation:

  - Multiply your current number by `arr[i]`
  - Then take the result modulo `100000`

🎯 Return the **minimum number of operations** required to go from `start` to `end` using the above operations. If it’s **not possible**, return `-1`.

---

### 🧪 Test Cases

#### Test Case 1:

```js
arr = [2, 5, 7];
start = 3;
end = 30;

Output: 2;
```

#### Explanation:

- 3 → 3×10 = 30 (in 2 steps: 3×5 = 15 → 15×2 = 30)
- Or 3×2 = 6 → 6×5 = 30

#### Test Case 2:

```js
arr = [2];
start = 3;
end = 100;

Output: -1;
```

---

### 💡 Intuition

This is a classic **shortest path problem** in an **implicit graph**:

- Each node is a number from `0` to `99999` (because of `% 100000`)
- From each node, we can reach multiple new nodes by:

  - `next = (current * arr[i]) % 100000`

We can solve this using **BFS**, where:

- Each number is a node
- Each multiplication-mod operation is an edge
- We need the **shortest path (minimum steps)** from `start` to `end`

---

### 🔍 Dry Run

Given:
`arr = [2, 5, 7], start = 3, end = 30`

BFS:

```
Start = 3
Level 0: 3
Level 1: (3*2)=6, (3*5)=15, (3*7)=21
Level 2: 6*2=12, 6*5=30 ✅ → Done in 2 steps
```

---

### ✅ JavaScript Code (BFS)

```javascript
function minimumMultiplications(arr, start, end) {
  const mod = 100000;
  const visited = new Array(mod).fill(false);
  const queue = [[start, 0]];

  visited[start] = true;

  while (queue.length > 0) {
    const [current, steps] = queue.shift();

    if (current === end) return steps;

    for (let num of arr) {
      const next = (current * num) % mod;
      if (!visited[next]) {
        visited[next] = true;
        queue.push([next, steps + 1]);
      }
    }
  }

  return -1;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity**: `O(100000 * arr.length)`
  (in worst case, we may visit all `0 to 99999` numbers once)
- **Space Complexity**: `O(100000)` for visited array and queue

---

### 📌 Summary Table

| Feature    | Description                                  |
| ---------- | -------------------------------------------- |
| Graph Type | Implicit (nodes = numbers 0 to 99999)        |
| Edge Cost  | Uniform (1 operation per step)               |
| Traversal  | BFS (unweighted shortest path)               |
| Output     | Minimum steps to reach from `start` to `end` |

---

## 🔢 **10. Bellman-Ford Algorithm**

### 📘 Problem Statement

You are given:

- A directed **weighted graph** with `V` vertices and `E` edges.
- An array of edges `edges[] = [u, v, wt]`.
- A `source` vertex.

🎯 Find the **shortest distances** from `source` to all vertices.

💥 If there is a **negative weight cycle** in the graph, report it.

---

### 🧪 Test Case

#### Test Case 1:

```js
(V = 5), (source = 0);
edges = [
  [0, 1, -1],
  [0, 2, 4],
  [1, 2, 3],
  [1, 3, 2],
  [1, 4, 2],
  [3, 2, 5],
  [3, 1, 1],
  [4, 3, -3],
];

Output: [0, -1, 2, -2, 1];
```

---

### 💡 Intuition

Dijkstra's Algorithm doesn’t work for **negative weight edges**.

✅ Bellman-Ford handles **negative weights** and detects **negative cycles**.

#### Main Idea:

- **Relax all edges `V-1` times**
  (The shortest path can have at most `V-1` edges)
- On the **V-th iteration**, if any edge still gets relaxed → **negative cycle exists**

---

### 🔍 Dry Run

Graph:
0 → 1 (-1), 0 → 2 (4)
1 → 2 (3), 1 → 3 (2), 1 → 4 (2)
4 → 3 (-3)

From 0:

- Initially: dist = `[0, ∞, ∞, ∞, ∞]`
- After 1st iteration: `[0, -1, 4, 1, 1]`
- After 2nd: `[0, -1, 2, -2, 1]`
- No updates on 3rd → done

---

### ✅ JavaScript Code

```javascript
function bellmanFord(V, edges, source) {
  const dist = Array(V).fill(Infinity);
  dist[source] = 0;

  for (let i = 0; i < V - 1; i++) {
    for (let [u, v, wt] of edges) {
      if (dist[u] !== Infinity && dist[u] + wt < dist[v]) {
        dist[v] = dist[u] + wt;
      }
    }
  }

  // Check for negative weight cycle
  for (let [u, v, wt] of edges) {
    if (dist[u] !== Infinity && dist[u] + wt < dist[v]) {
      return "Negative weight cycle detected";
    }
  }

  return dist;
}
```

---

### ⏱ Time and Space Complexity

Let `V = vertices`, `E = edges`

- **Time Complexity**: `O(V * E)`
- **Space Complexity**: `O(V)` (for distance array)

---

### 📌 Summary Table

| Feature                  | Description                           |
| ------------------------ | ------------------------------------- |
| Graph Type               | Directed, weighted                    |
| Handles Negative Weights | ✅ Yes                                |
| Detects Negative Cycles  | ✅ Yes                                |
| Approach                 | Edge Relaxation V-1 times             |
| Edge Cost Constraint     | No constraint on sign of edge weights |

---

### 🧩 Applications

| Use Case                                   | Why Bellman-Ford?                |
| ------------------------------------------ | -------------------------------- |
| 🔹 Routing Algorithms (e.g., RIP protocol) | Handles negative weights         |
| 🔹 Currency Arbitrage Detection            | Detects negative weight cycles   |
| 🔹 Longest Path in DAG (with tweaks)       | Reverse weights and Bellman-Ford |

---

### 🧠 Comparison With Other Shortest Path Algorithms

| Algorithm      | Handles Negative Weights | Detects Negative Cycle | Time Complexity  |
| -------------- | ------------------------ | ---------------------- | ---------------- |
| Dijkstra       | ❌ No                    | ❌ No                  | `O(E + V log V)` |
| Bellman-Ford   | ✅ Yes                   | ✅ Yes                 | `O(V * E)`       |
| Floyd-Warshall | ✅ Yes (all-pairs)       | ✅ Yes                 | `O(V^3)`         |

---

## 🔢 **11. Floyd-Warshall Algorithm**

### 📘 Problem Statement

You are given:

- A **directed weighted graph** with `V` vertices (0-based indexing)
- An adjacency matrix or edge list representing the **weights of edges between all pairs of vertices**
  (`adj[i][j]` is the weight of edge from `i` to `j`, or `Infinity` if there is no direct edge)

🎯 Your task is to find the **shortest distances between all pairs of vertices**.

> If there is a **negative weight cycle**, you can detect that as well.

---

### 🧪 Test Case

#### Test Case 1:

```txt
Input: (Adjacency Matrix)
       0   1   2   3
     ----------------
  0 |  0   5  INF 10
  1 | INF 0   3  INF
  2 | INF INF 0   1
  3 | INF INF INF 0

Output:
[
  [0, 5, 8, 9],
  [INF, 0, 3, 4],
  [INF, INF, 0, 1],
  [INF, INF, INF, 0]
]
```

---

### 💡 Intuition

Floyd-Warshall is a **Dynamic Programming** based all-pairs shortest path algorithm.

#### Key Idea:

For every possible pair of vertices `(i, j)`, try every other node `k` as an **intermediate** node and update:

```
if (dist[i][j] > dist[i][k] + dist[k][j])
    dist[i][j] = dist[i][k] + dist[k][j]
```

You perform this for every `(i, j)` and every `k = 0 to V-1`.

---

### 🔍 Dry Run

Let’s say you’re trying to go from `i → j`.

Initially, direct cost is `dist[i][j]`

Try every `k`:

- Is going `i → k → j` **shorter** than direct?
- If yes, update it.

Repeat this for all `k = 0 to V - 1`.

---

### ✅ JavaScript Code

```javascript
function floydWarshall(V, graph) {
  const dist = Array.from({ length: V }, (_, i) =>
    Array.from({ length: V }, (_, j) => (i === j ? 0 : graph[i][j] ?? Infinity))
  );

  for (let k = 0; k < V; k++) {
    for (let i = 0; i < V; i++) {
      for (let j = 0; j < V; j++) {
        if (dist[i][k] + dist[k][j] < dist[i][j]) {
          dist[i][j] = dist[i][k] + dist[k][j];
        }
      }
    }
  }

  // Check for negative weight cycle
  for (let i = 0; i < V; i++) {
    if (dist[i][i] < 0) {
      return "Negative weight cycle detected";
    }
  }

  return dist;
}
```

---

### ⏱ Time and Space Complexity

Let `V = number of vertices`

| Metric           | Value   |
| ---------------- | ------- |
| Time Complexity  | `O(V³)` |
| Space Complexity | `O(V²)` |

---

### 📌 Summary Table

| Feature         | Description                                 |
| --------------- | ------------------------------------------- |
| Graph Type      | Directed, weighted (with/without negatives) |
| Negative Edges  | ✅ Allowed                                  |
| Negative Cycles | ✅ Detectable                               |
| Goal            | All-pairs shortest path                     |
| Approach        | Dynamic Programming (triple nested loop)    |

---

### 🧩 Applications

| Use Case                          | Why Use Floyd-Warshall?          |
| --------------------------------- | -------------------------------- |
| 🔹 All-pairs shortest paths       | Fast for dense graphs            |
| 🔹 Transitive closure in graphs   | Replace weights with boolean     |
| 🔹 Finding negative weight cycles | Check `dist[i][i] < 0`           |
| 🔹 APSP in Johnson’s Algorithm    | Step 1 uses Bellman-Ford + Floyd |

---

### 🧠 Comparison with Other Algorithms

| Algorithm      | Supports Neg Weights | Detect Neg Cycle | Time Complexity | Use Case           |
| -------------- | -------------------- | ---------------- | --------------- | ------------------ |
| Dijkstra       | ❌ No                | ❌ No            | `O((V+E)logV)`  | One source         |
| Bellman-Ford   | ✅ Yes               | ✅ Yes           | `O(VE)`         | One source         |
| Floyd-Warshall | ✅ Yes               | ✅ Yes           | `O(V³)`         | All-pairs shortest |

---

## 🔢 **12. Find the City With the Smallest Number of Neighbors Within Threshold Distance**

### 📘 Problem Statement

You are given:

- `n` cities numbered from `0` to `n-1`
- A list of edges: `edges[i] = [u, v, wt]` where there is a bidirectional road from `u` to `v` with weight `wt`
- An integer `distanceThreshold`

🎯 Return the **city with the smallest number of reachable cities** such that the **distance is less than or equal to the threshold**.

> If multiple cities have the same number of neighbors, return the **city with the greatest number** (i.e., break ties with higher-numbered city).

---

### 🧪 Test Case

```js
n = 4;
edges = [
  [0, 1, 3],
  [1, 2, 1],
  [1, 3, 4],
  [2, 3, 1],
];
distanceThreshold = 4;

Output: 3;
```

#### Explanation:

- City 0 can reach cities 1, 2 (2 cities)
- City 1 can reach 0, 2, 3 (3 cities)
- City 2 can reach 1, 3, 0 (3 cities)
- City 3 can reach 1, 2 (2 cities)

Cities 0 and 3 have only 2 neighbors → pick **city 3** (higher index)

---

### 💡 Intuition

We need to:

1. Compute **shortest distances** between all pairs → **Floyd-Warshall**
2. For each city, count how many other cities are reachable within `threshold`
3. Track the city with the **smallest count**, and on tie pick the **larger city index**

---

### ✅ JavaScript Code

```javascript
function findTheCity(n, edges, distanceThreshold) {
  const INF = Infinity;
  const dist = Array.from({ length: n }, () => Array(n).fill(INF));

  // Distance to self = 0
  for (let i = 0; i < n; i++) dist[i][i] = 0;

  // Fill direct distances
  for (let [u, v, wt] of edges) {
    dist[u][v] = wt;
    dist[v][u] = wt; // undirected
  }

  // Floyd-Warshall
  for (let k = 0; k < n; k++) {
    for (let i = 0; i < n; i++) {
      for (let j = 0; j < n; j++) {
        if (dist[i][k] + dist[k][j] < dist[i][j]) {
          dist[i][j] = dist[i][k] + dist[k][j];
        }
      }
    }
  }

  let minReachable = n;
  let city = -1;

  for (let i = 0; i < n; i++) {
    let count = 0;
    for (let j = 0; j < n; j++) {
      if (i !== j && dist[i][j] <= distanceThreshold) {
        count++;
      }
    }

    // If fewer reachable, or same count but higher city index
    if (count <= minReachable) {
      minReachable = count;
      city = i;
    }
  }

  return city;
}
```

---

### 🔍 Dry Run (Brief)

For `city = 0`:

- Can reach 1 (3), 2 (4)
- Total = 2

For `city = 3`:

- Can reach 2 (1), 1 (4)
- Total = 2

So output = **3** (as required)

---

### ⏱ Time and Space Complexity

Let `V = n`, `E = number of edges`

- **Time Complexity**: `O(V³)` (Floyd-Warshall)
- **Space Complexity**: `O(V²)` for distance matrix

---

### 📌 Summary Table

| Feature                | Description                            |
| ---------------------- | -------------------------------------- |
| Graph Type             | Undirected, weighted                   |
| Goal                   | City with fewest neighbors ≤ threshold |
| Shortest Path Strategy | Floyd-Warshall                         |
| Tie-breaking           | Pick city with higher index            |

---

# Minimum Spanning Tree

## 1. Introduction to MST

### Definition

A **Minimum Spanning Tree (MST)** of a weighted, connected, undirected graph is a spanning tree with the minimum possible total edge weight.

### Key Concepts

- **Spanning Tree**: A subgraph that includes all vertices and is connected with exactly V-1 edges (no cycles)
- **Minimum**: Among all possible spanning trees, the one with minimum total weight
- **Unique**: MST may not be unique, but the minimum weight is always unique

### Prerequisites

- Graph must be **connected** (otherwise we find Minimum Spanning Forest)
- Graph must be **undirected**
- Edges must have **weights** (can be negative)

### Example

```
Original Graph:
    A ----4---- B
    |           |
    5           2
    |           |
    C ----3---- D

All possible spanning trees:
1. A-B(4), B-D(2), C-D(3) = Weight: 9
2. A-B(4), A-C(5), B-D(2) = Weight: 11
3. A-C(5), C-D(3), B-D(2) = Weight: 10

MST: A-B(4), B-D(2), C-D(3) with total weight = 9
```

## 2. MST Properties and Theorems

### 2.1 Cut Property (Fundamental Property)

**Statement**: For any cut in the graph, the minimum weight edge crossing the cut is in some MST.

**Proof Idea**: If not, we can replace an edge in the MST with this minimum edge to get a tree with smaller weight.

### 2.2 Cycle Property

**Statement**: For any cycle in the graph, the maximum weight edge in the cycle is not in any MST.

**Proof Idea**: If it were in an MST, removing it would disconnect the tree, but we can reconnect using any other edge from the cycle with smaller weight.

### 2.3 Uniqueness Conditions

- If all edge weights are distinct, MST is unique
- If edge weights are not distinct, MST may not be unique, but minimum weight is unique

### 2.4 Exchange Property

If T is an MST and e is an edge not in T, then adding e to T creates exactly one cycle. The heaviest edge in this cycle can be removed to get another MST.

## 🔢 **1. Prim’s Algorithm – Minimum Spanning Tree (MST)**

### 📘 Problem Statement

You are given:

- An **undirected, weighted graph** with `V` vertices and `E` edges.
- The graph is **connected** (i.e., all nodes can be reached).

🎯 Your goal is to find the **total weight of the Minimum Spanning Tree (MST)** — a subset of edges that:

- Connects all vertices
- Has no cycles
- Has **minimum possible total weight**

---

### 🧪 Test Case

```txt
Input:
V = 5
Edges = [
  [0, 1, 2],
  [0, 3, 6],
  [1, 2, 3],
  [1, 3, 8],
  [1, 4, 5],
  [2, 4, 7],
  [3, 4, 9]
]

Output: 16
```

#### Explanation:

MST includes edges:

- 0–1 (2), 1–2 (3), 1–4 (5), 0–3 (6)
  Total = 2 + 3 + 5 + 6 = **16**

---

### 💡 Intuition

Prim’s Algorithm builds the MST **greedily**:

- Start from any node (say 0)
- In each step, pick the **minimum weight edge** that connects a new vertex to the current MST
- Repeat until all vertices are included

This is similar to Dijkstra's algorithm but focuses on **edges**, not distances from a source.

---

### ✅ JavaScript Code Using Min-Heap (Priority Queue)

```javascript
function primMST(V, edges) {
  const adj = Array.from({ length: V }, () => []);

  // Build adjacency list
  for (let [u, v, wt] of edges) {
    adj[u].push([v, wt]);
    adj[v].push([u, wt]); // undirected
  }

  const visited = new Array(V).fill(false);
  const minHeap = [[0, 0]]; // [weight, node]
  let totalCost = 0;

  while (minHeap.length > 0) {
    minHeap.sort((a, b) => a[0] - b[0]); // simulate min-heap
    const [wt, u] = minHeap.shift();

    if (visited[u]) continue;

    visited[u] = true;
    totalCost += wt;

    for (let [v, edgeWt] of adj[u]) {
      if (!visited[v]) {
        minHeap.push([edgeWt, v]);
      }
    }
  }

  return totalCost;
}
```

---

### 🔍 Dry Run on Above Test Case

1. Start from 0:

   - Edge to 1 (2), Edge to 3 (6) → Pick (0–1)

2. Add 1:

   - Edge to 2 (3), 3 (8), 4 (5) → Pick (1–2)

3. Add 2:

   - Edge to 4 (7) → Pick (1–4)

4. Add 4:

   - Edge to 3 (9) → Pick (0–3) because it was in heap earlier

✅ Total = 2 + 3 + 5 + 6 = **16**

---

### ⏱ Time and Space Complexity

Let `V = vertices`, `E = edges`

| Metric           | Value                  |
| ---------------- | ---------------------- |
| Time Complexity  | `O(E log V)` with heap |
| Space Complexity | `O(V + E)`             |

---

### 📌 Summary Table

| Feature      | Description                 |
| ------------ | --------------------------- |
| Graph Type   | Undirected, Weighted        |
| Goal         | Minimum Spanning Tree (MST) |
| Method       | Greedy (edge by edge)       |
| Alternate To | Kruskal’s Algorithm         |
| Edge Weights | Can be positive only        |

---

### 🧩 Applications

| Real-World Use Case | Description                         |
| ------------------- | ----------------------------------- |
| 🔌 Network Design   | Build cheapest network of computers |
| 🏞 Road Construction | Minimum cost to connect all cities  |
| 🌐 Clustering       | Hierarchical clustering             |

---

### 🧠 Comparison with Kruskal’s Algorithm

| Feature        | Prim’s                    | Kruskal’s     |
| -------------- | ------------------------- | ------------- |
| Builds MST     | Vertex-by-vertex          | Edge-by-edge  |
| Data Structure | Min-Heap / Priority Queue | Union-Find    |
| Graph Type     | Dense graphs              | Sparse graphs |

---

## 🔢 **2. Disjoint Set (Union by Rank + Path Compression)**

### 📘 Problem Statement

You are given a collection of `n` nodes and a series of `union` and `find` operations.

🎯 Design a **Disjoint Set Union (DSU)** data structure to efficiently:

- **Find** the representative (parent) of a node’s set
- **Union** two nodes into the same set (if not already)

💡 Goal is to perform `find()` and `union()` in **nearly constant time** using:

- **Path Compression**
- **Union by Rank (or Size)**

---

### 🧪 Example Use Case

```txt
Input:
5 nodes → [0, 1, 2, 3, 4]
Operations:
  union(0, 1)
  union(1, 2)
  find(2) → returns 0 (representative)

Output:
Parent array: [0, 0, 0, 3, 4]
```

---

### 💡 Intuition

Disjoint Set is like organizing elements into **non-overlapping groups (sets)**.

Initially, each node is in its **own set**. As we perform `union(x, y)`, we merge their sets.

To optimize:

- 🔁 **Path Compression**: during `find(x)`, make every node on the path point directly to the root.
- 🏷 **Union by Rank**: always attach the shorter tree under the taller one.

This ensures that the tree remains shallow, giving **almost O(1)** performance.

---

### ✅ JavaScript Implementation

```javascript
class DisjointSet {
  constructor(n) {
    this.parent = Array.from({ length: n }, (_, i) => i);
    this.rank = new Array(n).fill(0); // or size if using union by size
  }

  find(u) {
    if (u !== this.parent[u]) {
      this.parent[u] = this.find(this.parent[u]); // path compression
    }
    return this.parent[u];
  }

  union(u, v) {
    const pu = this.find(u);
    const pv = this.find(v);

    if (pu === pv) return;

    // Union by rank
    if (this.rank[pu] < this.rank[pv]) {
      this.parent[pu] = pv;
    } else if (this.rank[pu] > this.rank[pv]) {
      this.parent[pv] = pu;
    } else {
      this.parent[pv] = pu;
      this.rank[pu]++;
    }
  }
}
```

---

### 🔍 Dry Run

#### Initial:

```
Parent: [0, 1, 2, 3, 4]
Rank:   [0, 0, 0, 0, 0]
```

#### union(0, 1):

- 0 and 1 are roots → attach 1 under 0 → rank\[0] = 1

```
Parent: [0, 0, 2, 3, 4]
Rank:   [1, 0, 0, 0, 0]
```

#### union(1, 2):

- Root of 1 = 0, Root of 2 = 2
- Attach 2 under 0 → no rank change

```
Parent: [0, 0, 0, 3, 4]
Rank:   [1, 0, 0, 0, 0]
```

#### find(2):

- Root of 2 is 0 → no changes needed (already compressed)

---

### ⏱ Time and Space Complexity

| Operation | Time Complexity | Explanation              |
| --------- | --------------- | ------------------------ |
| `find()`  | `O(α(n))`       | Very close to constant   |
| `union()` | `O(α(n))`       | Using rank & compression |
| Space     | `O(n)`          | For `parent` and `rank`  |

> `α(n)` is the **inverse Ackermann function**, which grows extremely slowly.

---

### 📌 Summary Table

| Feature        | Description                              |
| -------------- | ---------------------------------------- |
| Purpose        | Partitioning elements into disjoint sets |
| Core Functions | `find()`, `union()`                      |
| Optimizations  | Path Compression, Union by Rank          |
| Applications   | MST (Kruskal), Connected Components      |

---

## 🔢 **3. Disjoint Set – Union by Size + Path Compression**

### 📘 Problem Statement

You are given `n` elements. Perform union and find operations on them.

🎯 Implement a **Disjoint Set Union (DSU)** data structure that supports:

- `find(u)`: Find the representative (ultimate parent) of node `u`
- `union(u, v)`: Join the sets containing `u` and `v`

💡 Use:

- **Union by Size**: Attach the smaller-sized set under the larger one.
- **Path Compression**: Flatten the trees for faster `find`.

---

### 🧪 Example Use Case

```txt
Input:
n = 7
Operations:
  union(1, 2)
  union(2, 3)
  union(4, 5)
  union(6, 5)
  union(3, 5)
  find(1) → returns 1 or 4 depending on the order

Output:
Parent array: [0,1,1,1,4,4,4]
Size array:   [1,4,1,1,3,1,1]
```

---

### 💡 Intuition

Disjoint Set is used to maintain a collection of non-overlapping sets.

We optimize it by:

- 📌 **Path Compression**: While finding the parent, update all nodes in the path to point directly to the root.
- ⚖️ **Union by Size**: Always attach the smaller set below the larger one — keeps the tree shallow.

---

### ✅ JavaScript Implementation

```javascript
class DisjointSet {
  constructor(n) {
    this.parent = Array.from({ length: n }, (_, i) => i);
    this.size = new Array(n).fill(1);
  }

  find(u) {
    if (u !== this.parent[u]) {
      this.parent[u] = this.find(this.parent[u]); // path compression
    }
    return this.parent[u];
  }

  union(u, v) {
    const pu = this.find(u);
    const pv = this.find(v);

    if (pu === pv) return;

    // Union by size
    if (this.size[pu] < this.size[pv]) {
      this.parent[pu] = pv;
      this.size[pv] += this.size[pu];
    } else {
      this.parent[pv] = pu;
      this.size[pu] += this.size[pv];
    }
  }
}
```

---

### 🔍 Dry Run

#### Initially:

```
Parent: [0, 1, 2, 3, 4, 5, 6]
Size:   [1, 1, 1, 1, 1, 1, 1]
```

#### union(1, 2):

- Roots: 1, 2 → attach 2 under 1

```
Parent: [0, 1, 1, 3, 4, 5, 6]
Size:   [1, 2, 1, 1, 1, 1, 1]
```

#### union(2, 3):

- find(2) = 1, find(3) = 3 → attach 3 under 1

```
Parent: [0, 1, 1, 1, 4, 5, 6]
Size:   [1, 3, 1, 1, 1, 1, 1]
```

---

### ⏱ Time and Space Complexity

| Operation | Time Complexity | Explanation                    |
| --------- | --------------- | ------------------------------ |
| `find()`  | `O(α(n))`       | Inverse Ackermann (very small) |
| `union()` | `O(α(n))`       | Almost constant                |
| Space     | `O(n)`          | `parent[]` and `size[]`        |

---

### 📌 Summary Table

| Feature      | Description                         |
| ------------ | ----------------------------------- |
| Optimization | Union by Size + Path Compression    |
| Goal         | Maintain disjoint sets efficiently  |
| Operations   | `find(u)`, `union(u, v)`            |
| Use Case     | Kruskal’s MST, Connected Components |

---

## 🔢 **4. Kruskal’s Algorithm – Minimum Spanning Tree (MST)**

### 📘 Problem Statement

You are given:

- An **undirected, connected, weighted graph** with `V` vertices and `E` edges.
- Each edge is represented as `[u, v, wt]`.

🎯 Your goal is to return the **minimum total weight** of the **Minimum Spanning Tree** (MST) formed from these edges.

---

### 🧪 Test Case

```txt
Input:
V = 4
Edges = [
  [0, 1, 10],
  [0, 2, 6],
  [0, 3, 5],
  [1, 3, 15],
  [2, 3, 4]
]

Output:
19
```

#### Explanation:

MST includes edges:

- 2–3 (4), 0–3 (5), 0–1 (10)
  Total = **4 + 5 + 10 = 19**

---

### 💡 Intuition

Kruskal’s Algorithm builds the MST **greedily** by:

1. Sorting all edges by **increasing weight**
2. Adding edges one by one **only if they don’t form a cycle**
3. Using **Disjoint Set Union (DSU)** to efficiently check cycle formation

---

### 🧠 How It Works

- Initially, each vertex is its **own set**.
- For each edge `(u, v)`:

  - If `find(u) !== find(v)`: Add edge to MST, `union(u, v)`
  - Else, skip (cycle would be formed)

---

### ✅ JavaScript Code Using Union by Size

```javascript
class DisjointSet {
  constructor(n) {
    this.parent = Array.from({ length: n }, (_, i) => i);
    this.size = new Array(n).fill(1);
  }

  find(u) {
    if (u !== this.parent[u]) {
      this.parent[u] = this.find(this.parent[u]); // Path Compression
    }
    return this.parent[u];
  }

  union(u, v) {
    let pu = this.find(u);
    let pv = this.find(v);
    if (pu === pv) return false;

    // Union by Size
    if (this.size[pu] < this.size[pv]) {
      this.parent[pu] = pv;
      this.size[pv] += this.size[pu];
    } else {
      this.parent[pv] = pu;
      this.size[pu] += this.size[pv];
    }
    return true;
  }
}

function kruskalMST(V, edges) {
  edges.sort((a, b) => a[2] - b[2]); // Sort edges by weight
  const dsu = new DisjointSet(V);
  let totalCost = 0;

  for (const [u, v, wt] of edges) {
    if (dsu.union(u, v)) {
      totalCost += wt;
    }
  }

  return totalCost;
}
```

---

### 🔍 Dry Run

#### Initial Edges Sorted:

```
[2, 3, 4]
[0, 3, 5]
[0, 2, 6]
[0, 1, 10]
[1, 3, 15]
```

Steps:

- Add 2–3 → total = 4
- Add 0–3 → total = 9
- Skip 0–2 (would form cycle)
- Add 0–1 → total = 19

✅ MST = {2–3, 0–3, 0–1} with weight **19**

---

### ⏱ Time and Space Complexity

Let `V = vertices`, `E = edges`

| Step           | Complexity   |
| -------------- | ------------ |
| Sort edges     | `O(E log E)` |
| DSU operations | `O(E α(V))`  |
| Total Time     | `O(E log E)` |
| Space          | `O(V)`       |

---

### 📌 Summary Table

| Feature        | Description                        |
| -------------- | ---------------------------------- |
| Graph Type     | Undirected, weighted, connected    |
| Builds         | MST (Minimum Spanning Tree)        |
| Strategy       | Greedy + Union-Find                |
| Edge Selection | Based on minimum weight (globally) |
| Cycle Check    | Via Disjoint Set                   |

---

### 🧩 Applications

| Use Case                          | Explanation                     |
| --------------------------------- | ------------------------------- |
| 🔌 Network Design                 | Connect systems at minimum cost |
| 🏞 Building Roads/Bridges          | Cheapest way to connect cities  |
| 📶 Optimizing Communication Paths | Minimum wiring with no loops    |

---

### 🧠 Comparison With Prim's Algorithm

| Feature          | Kruskal's       | Prim's         |
| ---------------- | --------------- | -------------- |
| Focus on         | Global min edge | Local min edge |
| Uses             | Disjoint Set    | Priority Queue |
| Works well for   | Sparse graphs   | Dense graphs   |
| Cycle Prevention | DSU             | Visited set    |

---

## 🔢 **5. Number of Operations to Make Network Connected**

### 📘 Problem Statement

You are given:

- `n` computers labeled from `0` to `n - 1`
- A list of `connections` where `connections[i] = [u, v]` represents a direct wired connection between computers `u` and `v`

🎯 You **can remove a cable** and place it between any two computers.

✅ Return the **minimum number of operations** to **connect all the computers**
❌ Return `-1` if it's **not possible**

---

### 🧪 Test Cases

#### Test Case 1:

```txt
n = 4
connections = [[0,1], [0,2], [1,2]]
Output: 1
```

Explanation: 1 extra cable can be used to connect the 4th computer.

---

#### Test Case 2:

```txt
n = 6
connections = [[0,1], [0,2], [0,3], [1,4]]
Output: -1
```

Explanation: We need 2 cables to connect 6 nodes, but we have only 4 cables.

---

### 💡 Intuition

- To connect `n` computers, we need at least `n - 1` **cables**.
- If `connections.length < n - 1` → ❌ Not enough cables → Return `-1`
- Use **Disjoint Set** to count **connected components**.
- We need `components - 1` operations to connect them.

---

### 🔍 Dry Run

Given `n = 4`, connections: `[[0,1], [0,2], [1,2]]`
Edges: 3 cables, but only 2 needed. One is extra.
Connected components = 2 → Need 1 operation → ✅

---

### ✅ JavaScript Code (Union by Size)

```javascript
class DisjointSet {
  constructor(n) {
    this.parent = Array.from({ length: n }, (_, i) => i);
    this.size = new Array(n).fill(1);
  }

  find(u) {
    if (u !== this.parent[u]) {
      this.parent[u] = this.find(this.parent[u]);
    }
    return this.parent[u];
  }

  union(u, v) {
    let pu = this.find(u);
    let pv = this.find(v);
    if (pu === pv) return false;

    if (this.size[pu] < this.size[pv]) {
      this.parent[pu] = pv;
      this.size[pv] += this.size[pu];
    } else {
      this.parent[pv] = pu;
      this.size[pu] += this.size[pv];
    }
    return true;
  }
}

function makeConnected(n, connections) {
  if (connections.length < n - 1) return -1; // not enough cables

  const dsu = new DisjointSet(n);
  let components = n;

  for (const [u, v] of connections) {
    if (dsu.union(u, v)) {
      components--; // connected two components
    }
  }

  return components - 1;
}
```

---

### ⏱ Time and Space Complexity

| Metric           | Value         |
| ---------------- | ------------- |
| Time Complexity  | `O(E * α(N))` |
| Space Complexity | `O(N)`        |

> `α(N)` is the inverse Ackermann function (nearly constant)

---

### 📌 Summary Table

| Feature         | Value                     |
| --------------- | ------------------------- |
| Graph Type      | Undirected                |
| Core Logic      | Disjoint Set (Union-Find) |
| Cables Required | At least `n - 1`          |
| Answer          | `components - 1`          |

---

## 🔢 **6. Most Stones Removed with Same Row or Column**

### 📘 Problem Statement

You are given an array of stones where `stones[i] = [x, y]` represents a stone at coordinate `(x, y)`.

🎯 You can remove a stone **if it shares the same row or the same column** as another stone.

Return the **maximum number of stones you can remove**.

---

### 🧪 Test Cases

#### Test Case 1:

```txt
Input: stones = [[0,0],[0,1],[1,0],[1,2],[2,1],[2,2]]
Output: 5
```

#### Test Case 2:

```txt
Input: stones = [[0,0],[0,2],[1,1],[2,0],[2,2]]
Output: 3
```

---

### 💡 Intuition

Think of this as a **graph** where:

- Stones are **nodes**
- An **edge exists** if two stones are in the same row or same column

We want to count **connected components**.

- From each component, we can remove all but one stone
- So, answer = `total stones - number of connected components`

Use **Disjoint Set Union (DSU)** to track connected components:

- Treat each unique row and column as **nodes**
- Union the row and column for every stone → `union(row, col + 10000)` (to avoid collision)

---

### ✅ JavaScript Code (Union by Size)

```javascript
class DisjointSet {
  constructor() {
    this.parent = {};
    this.size = {};
  }

  find(x) {
    if (!(x in this.parent)) {
      this.parent[x] = x;
      this.size[x] = 1;
    }
    if (this.parent[x] !== x) {
      this.parent[x] = this.find(this.parent[x]);
    }
    return this.parent[x];
  }

  union(x, y) {
    const px = this.find(x);
    const py = this.find(y);
    if (px === py) return;

    if (this.size[px] < this.size[py]) {
      this.parent[px] = py;
      this.size[py] += this.size[px];
    } else {
      this.parent[py] = px;
      this.size[px] += this.size[py];
    }
  }
}

function removeStones(stones) {
  const dsu = new DisjointSet();

  for (const [x, y] of stones) {
    dsu.union(x, y + 10000); // map cols to different space to avoid conflict
  }

  const uniqueRoots = new Set();
  for (const [x, y] of stones) {
    uniqueRoots.add(dsu.find(x));
  }

  return stones.length - uniqueRoots.size;
}
```

---

### 🔍 Dry Run

Given stones:
`[[0,0],[0,1],[1,0],[1,2],[2,1],[2,2]]`

Total = 6 stones
Connected components = 1
→ Remove 6 - 1 = **5** stones ✅

---

### ⏱ Time and Space Complexity

| Metric           | Value         |
| ---------------- | ------------- |
| Time Complexity  | `O(N * α(N))` |
| Space Complexity | `O(N)`        |

Where `α(N)` is the inverse Ackermann function, nearly constant.

---

### 📌 Summary Table

| Feature        | Description                        |
| -------------- | ---------------------------------- |
| Graph Type     | Implicit graph (stones → nodes)    |
| Key Insight    | Connected components via row/col   |
| Data Structure | Disjoint Set Union (DSU)           |
| Output         | `Total stones - num of components` |

---

## 🔢 **7. Accounts Merge**

### 📘 Problem Statement

You are given a list of accounts.
Each account contains:

- A **name** and a list of **emails**.

🎯 Merge all accounts that **share at least one common email** (they belong to the same person).
Return the **merged accounts** in the format:

```txt
[name, email1, email2, ...] (sorted lexicographically)
```

---

### 🧪 Test Case

```txt
Input:
[
  ["John", "johnsmith@mail.com", "john00@mail.com"],
  ["John", "johnnybravo@mail.com"],
  ["John", "johnsmith@mail.com", "john_newyork@mail.com"],
  ["Mary", "mary@mail.com"]
]

Output:
[
  ["John", "john00@mail.com", "john_newyork@mail.com", "johnsmith@mail.com"],
  ["John", "johnnybravo@mail.com"],
  ["Mary", "mary@mail.com"]
]
```

---

### 💡 Intuition

This is a **connected components** problem:

- Treat each **email** as a node
- If two emails are in the same account, they’re **connected**
- Use **Disjoint Set Union (DSU)** to group connected emails

Then:

1. Find connected components using DSU
2. Group emails by their representative
3. Attach the name from the original account

---

### ✅ JavaScript Code

```javascript
class DisjointSet {
  constructor() {
    this.parent = {};
  }

  find(x) {
    if (!(x in this.parent)) this.parent[x] = x;
    if (this.parent[x] !== x) {
      this.parent[x] = this.find(this.parent[x]);
    }
    return this.parent[x];
  }

  union(x, y) {
    const px = this.find(x);
    const py = this.find(y);
    if (px !== py) this.parent[py] = px;
  }
}

function accountsMerge(accounts) {
  const dsu = new DisjointSet();
  const emailToName = {};

  // Step 1: Union all emails in the same account
  for (const account of accounts) {
    const name = account[0];
    const firstEmail = account[1];

    for (let i = 1; i < account.length; i++) {
      const email = account[i];
      dsu.union(firstEmail, email);
      emailToName[email] = name;
    }
  }

  // Step 2: Group emails by their ultimate parent
  const components = {};
  for (const email of Object.keys(emailToName)) {
    const root = dsu.find(email);
    if (!(root in components)) components[root] = [];
    components[root].push(email);
  }

  // Step 3: Build result
  const result = [];
  for (const root in components) {
    const name = emailToName[root];
    const emails = components[root].sort();
    result.push([name, ...emails]);
  }

  return result;
}
```

---

### 🔍 Dry Run (Step-by-Step)

For:

```js
["John", "johnsmith@mail.com", "john00@mail.com"][
  ("John", "johnsmith@mail.com", "john_newyork@mail.com")
];
```

- Union: `johnsmith@mail.com` with `john00@mail.com`
- Union: `johnsmith@mail.com` with `john_newyork@mail.com`
  \=> All 3 are in same component

---

### ⏱ Time and Space Complexity

| Metric           | Value                   |
| ---------------- | ----------------------- |
| Time Complexity  | `O(N * α(N)) + E log E` |
| Space Complexity | `O(N)`                  |

Where `N = total emails`, `α(N)` is inverse Ackermann function
Sorting each group gives the `E log E` part.

---

### 📌 Summary Table

| Feature        | Value                           |
| -------------- | ------------------------------- |
| Graph Type     | Implicit, via email connections |
| Union-Find Use | Connect same-person emails      |
| Output Format  | `[name, sorted_emails...]`      |

---

## 🔢 **8. Number of Islands II**

### 📘 Problem Statement

You are given:

- An `m x n` grid initially filled with water (`0`)
- A list of `positions` where land is added one by one

🎯 After each land addition, return the **number of islands** in the grid.

An **island** is formed by connecting adjacent lands (4-directionally) horizontally or vertically.

---

### 🧪 Test Case

```txt
Input:
m = 3, n = 3
positions = [[0,0],[0,1],[1,2],[2,1],[1,1]]

Output:
[1, 1, 2, 3, 1]
```

🧠 Explanation:

- (0,0): new island → 1
- (0,1): connects to (0,0) → still 1
- (1,2): new island → 2
- (2,1): new island → 3
- (1,1): connects to 3 islands → merged → total = 1

---

### 💡 Intuition

This is a **dynamic connectivity** problem:

- Each land cell is a **node**
- Add land one at a time
- Use **Disjoint Set** to connect newly added land to its neighboring lands
- Count how many **connected components (islands)** exist after each step

---

### ✅ JavaScript Code Using DSU

```javascript
class DisjointSet {
  constructor(m, n) {
    this.parent = {};
    this.rank = {};
    this.count = 0;
  }

  add(x) {
    if (!(x in this.parent)) {
      this.parent[x] = x;
      this.rank[x] = 0;
      this.count++;
    }
  }

  find(x) {
    if (this.parent[x] !== x) {
      this.parent[x] = this.find(this.parent[x]); // Path Compression
    }
    return this.parent[x];
  }

  union(x, y) {
    let px = this.find(x);
    let py = this.find(y);
    if (px === py) return;

    if (this.rank[px] < this.rank[py]) {
      this.parent[px] = py;
    } else if (this.rank[px] > this.rank[py]) {
      this.parent[py] = px;
    } else {
      this.parent[py] = px;
      this.rank[px]++;
    }
    this.count--; // union reduces ## of components
  }
}

function numIslands2(m, n, positions) {
  const dsu = new DisjointSet(m, n);
  const res = [];
  const dirs = [
    [0, 1],
    [1, 0],
    [-1, 0],
    [0, -1],
  ];
  const land = new Set();

  for (let [r, c] of positions) {
    const id = r * n + c;
    if (land.has(id)) {
      res.push(dsu.count);
      continue;
    }

    land.add(id);
    dsu.add(id);

    for (let [dr, dc] of dirs) {
      const nr = r + dr;
      const nc = c + dc;
      const nid = nr * n + nc;

      if (nr >= 0 && nr < m && nc >= 0 && nc < n && land.has(nid)) {
        dsu.union(id, nid);
      }
    }

    res.push(dsu.count);
  }

  return res;
}
```

---

### 🔍 Dry Run

```txt
Grid: 3x3

positions = [[0,0], [0,1], [1,2], [2,1], [1,1]]

Step-by-step:
- Add (0,0): new island → count = 1
- Add (0,1): merge with (0,0) → count = 1
- Add (1,2): new island → count = 2
- Add (2,1): new island → count = 3
- Add (1,1): connects to 3 neighbors → merged into one → count = 1
```

✅ Output: `[1, 1, 2, 3, 1]`

---

### ⏱ Time and Space Complexity

| Metric           | Value                         |
| ---------------- | ----------------------------- |
| Time Complexity  | `O(k * α(n*m))` (almost O(k)) |
| Space Complexity | `O(k)`                        |

Where `k = positions.length` and `α` is the inverse Ackermann function.

---

### 📌 Summary Table

| Feature            | Description              |
| ------------------ | ------------------------ |
| Grid Type          | Dynamic 2D Grid          |
| Key Data Structure | Disjoint Set Union (DSU) |
| Operations Counted | After each land addition |
| Edge Connections   | 4-directional            |

---

## 🔢 **9. Making a Large Island**

### 📘 Problem Statement

You are given an `n x n` grid consisting of `0`s (water) and `1`s (land).

🎯 You can change **at most one** `0` to `1`, and your task is to **return the size of the largest possible island** that can be formed.

📌 An island is formed by 1s connected **4-directionally** (up, down, left, right).

---

### 🧪 Test Case

```txt
Input:
grid = [[1, 0],
        [0, 1]]

Output: 3

Explanation:
Flip (0,1) or (1,0) → island of size 3
```

---

### 💡 Intuition

- First, label each island with a unique id and compute its size using **DFS or DSU**.
- For each `0` cell, consider flipping it:

  - Check its **4-directional neighbors**.
  - If they belong to different islands, sum up their sizes.
  - Track the **maximum** island size formed after a flip.

⚡ Use **Disjoint Set Union (DSU)** to efficiently track connected island sizes.

---

### ✅ JavaScript Code Using DSU

```javascript
class DisjointSet {
  constructor(size) {
    this.parent = Array.from({ length: size }, (_, i) => i);
    this.size = new Array(size).fill(1);
  }

  find(u) {
    if (this.parent[u] !== u) {
      this.parent[u] = this.find(this.parent[u]);
    }
    return this.parent[u];
  }

  union(u, v) {
    let pu = this.find(u);
    let pv = this.find(v);
    if (pu === pv) return;
    if (this.size[pu] < this.size[pv]) {
      this.parent[pu] = pv;
      this.size[pv] += this.size[pu];
    } else {
      this.parent[pv] = pu;
      this.size[pu] += this.size[pv];
    }
  }

  getSize(u) {
    return this.size[this.find(u)];
  }
}

function largestIsland(grid) {
  const n = grid.length;
  const dsu = new DisjointSet(n * n);
  const dirs = [
    [0, 1],
    [1, 0],
    [-1, 0],
    [0, -1],
  ];

  // Step 1: Union all adjacent 1's
  for (let r = 0; r < n; r++) {
    for (let c = 0; c < n; c++) {
      if (grid[r][c] === 1) {
        for (const [dr, dc] of dirs) {
          const nr = r + dr,
            nc = c + dc;
          if (nr >= 0 && nc >= 0 && nr < n && nc < n && grid[nr][nc] === 1) {
            dsu.union(r * n + c, nr * n + nc);
          }
        }
      }
    }
  }

  let maxIsland = 0;

  // Step 2: Try flipping each 0 and check max island size
  for (let r = 0; r < n; r++) {
    for (let c = 0; c < n; c++) {
      if (grid[r][c] === 0) {
        const uniqueIslands = new Set();
        for (const [dr, dc] of dirs) {
          const nr = r + dr,
            nc = c + dc;
          if (nr >= 0 && nc >= 0 && nr < n && nc < n && grid[nr][nc] === 1) {
            uniqueIslands.add(dsu.find(nr * n + nc));
          }
        }

        let size = 1;
        for (const islandId of uniqueIslands) {
          size += dsu.size[islandId];
        }

        maxIsland = Math.max(maxIsland, size);
      }
    }
  }

  // Step 3: Edge case – all 1’s already
  for (let i = 0; i < n * n; i++) {
    if (grid[Math.floor(i / n)][i % n] === 1) {
      maxIsland = Math.max(maxIsland, dsu.getSize(i));
    }
  }

  return maxIsland;
}
```

---

### 🔍 Dry Run Example

#### Grid:

```
1 0
0 1
```

- Initially, 2 islands of size 1
- Flip (0,1) → connects (0,0) and (1,1) → size 3
  ✅ Max island = 3

---

### ⏱ Time and Space Complexity

| Metric           | Value    |
| ---------------- | -------- |
| Time Complexity  | `O(N^2)` |
| Space Complexity | `O(N^2)` |

> Efficient for large grids (up to `50x50` or `100x100`)

---

### 📌 Summary Table

| Feature          | Description                      |
| ---------------- | -------------------------------- |
| Grid Type        | Square Grid `n x n`              |
| Strategy         | DSU + Adjacency Check            |
| Edge Connections | 4-directional                    |
| Final Output     | Largest Island Size after 1 flip |

---

## 🔢 **10. Swim in Rising Water**

### 📘 Problem Statement

You're given an `n x n` grid of integers where:

- `grid[i][j]` represents the time when the water rises enough to pass through cell `(i, j)`.

🎯 You start at `(0, 0)` and want to reach `(n - 1, n - 1)`.
You can **only swim to 4-directional adjacent cells** where the water level is **at least** the time of that cell.

⏱ Return the **minimum time** when you can **safely reach** the bottom-right corner.

---

### 🧪 Test Case

```txt
Input:
grid = [[0, 2],
        [1, 3]]

Output: 3
```

**Explanation:**

- You must wait until time `3` to swim from (0,0) → (1,1).

---

### 💡 Intuition

This is like a **weighted shortest path problem** on a grid:

- Cost to move to a cell is the **maximum elevation** seen so far.
- We want to **minimize** the **maximum elevation** encountered from start to end.

So:

- Use a **Min Heap** (priority queue) to always expand the cell with the **lowest elevation** next.
- This is like **Dijkstra’s algorithm** where cost is the max height.

---

### ✅ JavaScript Code (Using Min Heap)

```javascript
class MinHeap {
  constructor() {
    this.data = [];
  }

  push(val) {
    this.data.push(val);
    this._bubbleUp();
  }

  pop() {
    if (this.size() === 1) return this.data.pop();
    const min = this.data[0];
    this.data[0] = this.data.pop();
    this._bubbleDown();
    return min;
  }

  size() {
    return this.data.length;
  }

  _bubbleUp() {
    let i = this.data.length - 1;
    const current = this.data[i];
    while (i > 0) {
      let parent = Math.floor((i - 1) / 2);
      if (this.data[parent][0] <= current[0]) break;
      [this.data[parent], this.data[i]] = [this.data[i], this.data[parent]];
      i = parent;
    }
  }

  _bubbleDown() {
    let i = 0;
    const length = this.data.length;
    while (true) {
      let left = 2 * i + 1;
      let right = 2 * i + 2;
      let smallest = i;

      if (left < length && this.data[left][0] < this.data[smallest][0])
        smallest = left;
      if (right < length && this.data[right][0] < this.data[smallest][0])
        smallest = right;

      if (smallest === i) break;
      [this.data[i], this.data[smallest]] = [this.data[smallest], this.data[i]];
      i = smallest;
    }
  }
}

function swimInWater(grid) {
  const n = grid.length;
  const visited = Array.from({ length: n }, () => Array(n).fill(false));
  const dirs = [
    [0, 1],
    [1, 0],
    [-1, 0],
    [0, -1],
  ];

  const heap = new MinHeap();
  heap.push([grid[0][0], 0, 0]);
  visited[0][0] = true;

  while (heap.size()) {
    const [maxTime, r, c] = heap.pop();

    if (r === n - 1 && c === n - 1) return maxTime;

    for (const [dr, dc] of dirs) {
      const nr = r + dr,
        nc = c + dc;
      if (nr >= 0 && nc >= 0 && nr < n && nc < n && !visited[nr][nc]) {
        visited[nr][nc] = true;
        heap.push([Math.max(maxTime, grid[nr][nc]), nr, nc]);
      }
    }
  }
}
```

---

### 🔍 Dry Run

For `grid = [[0,2],[1,3]]`:

- Start at (0,0) → elevation 0
- Add neighbors (1,0)=1 and (0,1)=2
- Pick (1,0) → max so far: 1
- Add (1,1)=3 → max = 3
- Reached (1,1) ✅

Result = **3**

---

### ⏱ Time and Space Complexity

| Metric           | Value            |
| ---------------- | ---------------- |
| Time Complexity  | `O(N^2 * log N)` |
| Space Complexity | `O(N^2)`         |

Where `N` is the size of the grid.

---

### 📌 Summary Table

| Feature        | Description                        |
| -------------- | ---------------------------------- |
| Grid Shape     | `n x n`                            |
| Strategy       | Dijkstra with min-heap             |
| Elevation Cost | Maximum elevation on path          |
| Goal           | Reach bottom-right with min effort |

---

# Algorithms

## 🔢 **1. Bridges in a Graph**

🔗 Problem type: **Graph Theory**, **DFS + Low-Link Values**, **Tarjan's Algorithm**

### 📘 Problem Statement

You're given an **undirected graph** with `V` vertices and a list of `edges`.

🎯 A **bridge** (or critical connection) is an edge that, if removed, **increases the number of connected components** in the graph.

Return **all such edges** (bridges) in the graph.

---

### 🧪 Test Case

#### Input:

```txt
V = 5
Edges = [
  [0, 1],
  [1, 2],
  [2, 0],
  [1, 3],
  [3, 4]
]
```

#### Output:

```txt
[[1, 3], [3, 4]]
```

✅ These are bridges: removing them increases the number of disconnected parts.

---

### 💡 Intuition

We perform a **DFS traversal** and compute:

- **Discovery time**: When a node is first visited
- **Lowest reachable time**: The earliest visited node reachable from the current subtree

🔁 If the **lowest reachable time** of a child is **greater** than the discovery time of the current node → the edge is a **bridge**.

> This is the core idea behind **Tarjan’s Algorithm** for bridges.

---

### 🧠 Key Concepts

- **Discovery time (tin\[u])**: Time when DFS visits `u`
- **Low-link value (low\[u])**: Earliest visited vertex reachable from subtree rooted at `u`
- Edge `(u, v)` is a **bridge** if `low[v] > tin[u]`

---

### ✅ JavaScript Code (Tarjan’s Algorithm)

```javascript
function findBridges(V, edges) {
  const adj = Array.from({ length: V }, () => []);
  for (const [u, v] of edges) {
    adj[u].push(v);
    adj[v].push(u);
  }

  const tin = new Array(V).fill(-1);
  const low = new Array(V).fill(-1);
  const visited = new Array(V).fill(false);
  const bridges = [];
  let timer = 0;

  function dfs(u, parent) {
    visited[u] = true;
    tin[u] = low[u] = timer++;

    for (const v of adj[u]) {
      if (v === parent) continue;

      if (!visited[v]) {
        dfs(v, u);
        low[u] = Math.min(low[u], low[v]);

        if (low[v] > tin[u]) {
          bridges.push([u, v]); // bridge found
        }
      } else {
        low[u] = Math.min(low[u], tin[v]);
      }
    }
  }

  for (let i = 0; i < V; i++) {
    if (!visited[i]) {
      dfs(i, -1);
    }
  }

  return bridges;
}
```

---

### 🔍 Dry Run (Step-by-step)

Graph:

```
0---1---3---4
 \  |
   2
```

DFS:

- tin\[0]=0, low\[0]=0
- Visit 1 → tin\[1]=1, low\[1]=1
- Visit 2 → back to 0 → update low\[1]=0
- Visit 3 → no back edge → low\[3]=3
- 3→4 → no back edge → bridge found: (3,4)

Edge (1,3) is a bridge too.

✅ Output: `[[1, 3], [3, 4]]`

---

### ⏱ Time and Space Complexity

| Metric           | Value      |
| ---------------- | ---------- |
| Time Complexity  | `O(V + E)` |
| Space Complexity | `O(V + E)` |

Where `V = vertices`, `E = edges`.

---

### 📌 Summary Table

| Feature        | Description                                |
| -------------- | ------------------------------------------ |
| Graph Type     | Undirected                                 |
| Algorithm Used | Tarjan’s DFS-based Bridge Detection        |
| Output         | List of bridges (critical edges)           |
| Conditions     | `low[v] > tin[u]` → edge (u,v) is a bridge |

---

## 🔢 **2. Articulation Points in a Graph**

🔗 Problem type: **Graph Theory**, **DFS + Low-Link Values**, **Tarjan’s Algorithm**

### 📘 Problem Statement

You are given a **connected undirected graph** with `V` vertices and `E` edges.

🎯 Your task is to find all **articulation points** (also called **cut vertices**) — vertices which, if removed, would **increase the number of connected components** in the graph.

---

### 🧪 Test Case

#### Input:

```txt
V = 5
Edges = [
  [0, 1],
  [1, 2],
  [2, 0],
  [1, 3],
  [3, 4]
]
```

#### Output:

```txt
[1, 3]
```

✅ Removing:

- Node `1` disconnects nodes `3` and `4` from the main cycle.
- Node `3` disconnects node `4`.

---

### 💡 Intuition

We use **Tarjan’s Algorithm** based on:

- **Discovery time** (tin\[u])
- **Lowest reachable time** (low\[u])

> The key idea is:

- A node `u` is an **articulation point** if **any** of its children `v` in DFS satisfies:
  🔹 `low[v] ≥ tin[u]`

🎯 Special Case: If the root of DFS tree has **more than one child**, it’s an articulation point.

---

### 🧠 Core Concepts

- `tin[u]` → when node `u` was first visited
- `low[u]` → earliest discovery time reachable from `u` or its subtree
- If `low[v] >= tin[u]` for a child `v`, then `u` is a **cut vertex**

---

### ✅ JavaScript Code

```javascript
function findArticulationPoints(V, edges) {
  const adj = Array.from({ length: V }, () => []);
  for (const [u, v] of edges) {
    adj[u].push(v);
    adj[v].push(u);
  }

  const visited = new Array(V).fill(false);
  const tin = new Array(V).fill(-1);
  const low = new Array(V).fill(-1);
  const isArticulation = new Array(V).fill(false);
  let timer = 0;

  function dfs(u, parent) {
    visited[u] = true;
    tin[u] = low[u] = timer++;
    let children = 0;

    for (const v of adj[u]) {
      if (v === parent) continue;
      if (!visited[v]) {
        dfs(v, u);
        low[u] = Math.min(low[u], low[v]);
        children++;

        if (parent !== -1 && low[v] >= tin[u]) {
          isArticulation[u] = true;
        }
      } else {
        low[u] = Math.min(low[u], tin[v]);
      }
    }

    // root node case
    if (parent === -1 && children > 1) {
      isArticulation[u] = true;
    }
  }

  for (let i = 0; i < V; i++) {
    if (!visited[i]) {
      dfs(i, -1);
    }
  }

  const result = [];
  for (let i = 0; i < V; i++) {
    if (isArticulation[i]) result.push(i);
  }

  return result;
}
```

---

### 🔍 Dry Run Example

For the graph:

```
0---1---3---4
 \  |
   2
```

#### DFS traversal:

- Node `1` has children: `0, 2, 3`
- `low[3] ≥ tin[1]` → So node `1` is a cut vertex
- Node `3` has child `4` → `low[4] ≥ tin[3]` → So `3` is a cut vertex

✅ Output: `[1, 3]`

---

### ⏱ Time and Space Complexity

| Metric           | Value      |
| ---------------- | ---------- |
| Time Complexity  | `O(V + E)` |
| Space Complexity | `O(V + E)` |

---

### 📌 Summary Table

| Feature           | Description                            |
| ----------------- | -------------------------------------- |
| Graph Type        | Undirected                             |
| Algorithm Used    | DFS + Low-Link (Tarjan’s Algorithm)    |
| Special Condition | Root is AP if it has ≥2 DFS children   |
| Output            | List of articulation points (vertices) |

---

## 🔢 **3. Kosaraju’s Algorithm – Strongly Connected Components (SCCs)**

🔗 Type: Directed Graph, DFS, SCC, Reverse Graph

### 📘 Problem Statement

Given a **directed graph** with `V` vertices and `E` edges, find the number of **Strongly Connected Components (SCCs)**.

🧠 A **Strongly Connected Component (SCC)** is a maximal subset of nodes such that:

- Every node is reachable from every other node in that subset.

---

### 🧪 Test Case

#### Input:

```txt
V = 5
Edges = [
  [0, 2],
  [2, 1],
  [1, 0],
  [0, 3],
  [3, 4]
]
```

#### Output:

```txt
2
```

✅ SCCs: `{0, 1, 2}`, `{3}`, `{4}`
Since `3 -> 4` is one-way, `{3}` and `{4}` are individual SCCs.

---

### 💡 Intuition

Kosaraju’s Algorithm works in **3 steps**:

#### ✅ Step 1: Do a **DFS** and store vertices **by their finishing times** in a stack (topo order).

#### 🔄 Step 2: **Reverse** the graph (transpose).

#### 🔁 Step 3: Pop vertices from the stack, and for each unvisited vertex, do DFS on the **reversed graph**.

Each DFS in this step gives **one SCC**.

---

### 📊 Why This Works

By finishing time:

- The first vertex to finish is **last** in stack.
- Reversing the graph ensures we follow **reverse paths**.

This way, each DFS in Step 3 stays **within a single SCC**.

---

### ✅ JavaScript Code

```javascript
function kosarajuSCC(V, edges) {
  // Step 1: Build original and reversed graph
  const graph = Array.from({ length: V }, () => []);
  const reverseGraph = Array.from({ length: V }, () => []);

  for (const [u, v] of edges) {
    graph[u].push(v);
    reverseGraph[v].push(u); // reversed edge
  }

  const visited = new Array(V).fill(false);
  const stack = [];

  // Step 2: Topological Sort (DFS finishing time)
  function dfs1(u) {
    visited[u] = true;
    for (const v of graph[u]) {
      if (!visited[v]) dfs1(v);
    }
    stack.push(u); // push after all children are done
  }

  for (let i = 0; i < V; i++) {
    if (!visited[i]) dfs1(i);
  }

  // Step 3: DFS on reversed graph
  visited.fill(false);
  let count = 0;

  function dfs2(u) {
    visited[u] = true;
    for (const v of reverseGraph[u]) {
      if (!visited[v]) dfs2(v);
    }
  }

  while (stack.length) {
    const node = stack.pop();
    if (!visited[node]) {
      dfs2(node);
      count++; // one SCC completed
    }
  }

  return count;
}
```

---

### 🔍 Dry Run on Example

Input graph:

```
0 → 2 → 1 → 0 (cycle)
0 → 3 → 4
```

#### Step 1 (DFS order → stack):

- DFS from 0: visit 0 → 2 → 1 → 0 (cycle) → finish: \[1,2,0,3,4]

#### Step 2 (Reversed graph):

- Edges reversed.

#### Step 3 (DFS on reversed):

- DFS from 0 → finds 0,1,2 → SCC1
- DFS from 3 → SCC2
- DFS from 4 → SCC3

✅ Output = `3` SCCs

---

### ⏱ Time and Space Complexity

| Metric           | Value      |
| ---------------- | ---------- |
| Time Complexity  | `O(V + E)` |
| Space Complexity | `O(V + E)` |

Efficient for large graphs.

---

### 📌 Summary Table

| Feature          | Value                         |
| ---------------- | ----------------------------- |
| Graph Type       | Directed                      |
| Result           | Number of SCCs                |
| Strategy         | 2 DFS passes + Reverse graph  |
| Extra Structures | Stack, Reverse Adjacency List |

---
