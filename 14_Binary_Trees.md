# 🌳 **Trees in Data Structures**

## 📘 **What is a Tree?**

A **Tree** is a **hierarchical data structure** that simulates a tree structure with a **root** value and subtrees of children, represented as a set of **linked nodes**.

- A Tree is **non-linear** and **acyclic** (no loops).
- It consists of **nodes** connected by **edges**.

---

## 🧩 **Basic Terminology**

| Term               | Definition                                                        |
| ------------------ | ----------------------------------------------------------------- |
| **Node**           | An element of the tree that stores data and links to other nodes. |
| **Root**           | The topmost node in the tree (only one).                          |
| **Edge**           | The connection between one node and another.                      |
| **Child**          | A node directly connected and below another node.                 |
| **Parent**         | A node that has children.                                         |
| **Leaf**           | A node with no children.                                          |
| **Sibling**        | Nodes that share the same parent.                                 |
| **Subtree**        | A tree formed by a node and its descendants.                      |
| **Height of Tree** | The number of edges on the longest path from the root to a leaf.  |
| **Depth**          | Number of edges from the root to the current node.                |
| **Degree**         | The number of children a node has.                                |

---

## 🏷️ **Types of Trees**

### 1. **Binary Tree**

- Each node has **at most two children**: left and right.
- Variants:

  - **Full Binary Tree**: All nodes have 0 or 2 children.
  - **Complete Binary Tree**: All levels are fully filled except the last, which is filled left to right.
  - **Perfect Binary Tree**: All internal nodes have 2 children and all leaves are at the same level.
  - **Skewed Tree**: Nodes have only one child (Left Skewed or Right Skewed).

### 2. **Binary Search Tree (BST)**

- Left subtree has nodes with values **less than** the root.
- Right subtree has nodes with values **greater than** the root.
- Enables efficient **search, insertion, and deletion**.

### 3. **AVL Tree**

- A **self-balancing BST**.
- Balance factor = height(left subtree) - height(right subtree) should be -1, 0, or 1.

### 4. **Heap Tree**

- **Binary Heap** (used in priority queues).

  - **Max-Heap**: Parent node ≥ child nodes.
  - **Min-Heap**: Parent node ≤ child nodes.

### 5. **Trie (Prefix Tree)**

- Used to store **strings** efficiently for **prefix-based searching** (like autocomplete).

### 6. **N-ary Tree**

- A node can have at most **N children**.

---

## 🔁 **Tree Traversals**

### 🔹 **Depth First Search (DFS)**

1. **Inorder Traversal (Left → Root → Right)**

   - Used in BST to get **sorted order**.

2. **Preorder Traversal (Root → Left → Right)**

   - Used to create a **copy** of the tree.

3. **Postorder Traversal (Left → Right → Root)**

   - Used to **delete** a tree or evaluate postfix expressions.

### 🔹 **Breadth First Search (BFS)**

4. **Level Order Traversal**

   - Visit nodes **level by level** from top to bottom.
   - Implemented using a **queue**.

---

## Binary Tree

- Each node has **at most two children**: left and right. ([takeuforward.org][1])
  Variants include:
- **Full Binary Tree**: Each node has either 0 or 2 children.
- **Complete Binary Tree**: All levels filled except maybe the last, which is left-aligned.
- **Perfect Binary Tree**: All internal nodes have 2 children, and all leaves are at the same depth.
- **Skewed Tree**: All nodes have only one child (left or right).

## 🧩 Representation in Memory

- Typically implemented using **nodes with pointers** for left and right (in a binary tree).
- Alternatively, in case of complete trees, can be represented using an **array**.&#x20;

---

## 📏 Height and Depth

- **Depth** of a node = distance from the **root**.
- **Height** of tree = maximum depth among all **leaf** nodes.
  Used to calculate runtime of recursive operations.&#x20;

---

# **Traversals**

## ✅ **1. Preorder Traversal of Binary Tree**

### 🧩 Problem Statement

Given the `root` of a binary tree, return the **preorder traversal** of its node values.

> **Preorder Traversal Order**: `Root → Left → Right`

---

### 🧪 Test Cases

#### Test Case 1:

```
Input:
        1
         \
          2
         /
        3

Output: [1, 2, 3]
```

#### Test Case 2:

```
Input:
        5
       / \
      3   6
     / \
    2   4

Output: [5, 3, 2, 4, 6]
```

#### Test Case 3:

```
Input: null

Output: []
```

#### Test Case 4:

```
Input:
        10
       /
      20
     /
    30

Output: [10, 20, 30]
```

---

### 💡 Intuition

In **preorder traversal**, we always:

1. Visit the **current node**.
2. Recursively traverse the **left subtree**.
3. Recursively traverse the **right subtree**.

This traversal is useful for copying a tree or serializing a binary tree.

---

### 🧪 Dry Run (Recursive)

#### Tree:

```
     1
    / \
   2   3
```

1. Visit 1 → `[1]`
2. Traverse left subtree (node 2): Visit 2 → `[1, 2]`
3. Traverse right subtree (node 3): Visit 3 → `[1, 2, 3]`

---

### ✅ Approach 1: Recursive Preorder Traversal

#### 🔗 Algorithm:

1. Initialize an empty result array.
2. Create a recursive function:

   - If node is null, return.
   - Push node value to result.
   - Call function on left and right child.

3. Return result.

---

#### ✅ JavaScript Code (Recursive)

```javascript
function preorderTraversal(root) {
  let result = [];

  function dfs(node) {
    if (!node) return;
    result.push(node.val); // Visit root
    dfs(node.left); // Traverse left
    dfs(node.right); // Traverse right
  }

  dfs(root);
  return result;
}
```

---

### ✅ Approach 2: Iterative Preorder Using Stack

#### 🔗 Algorithm:

1. Use a stack and push the root.
2. While the stack is not empty:

   - Pop a node and add its value to result.
   - Push **right** child first, then **left** child (so left is processed first).

3. Return result.

---

#### ✅ JavaScript Code (Iterative)

```javascript
function preorderTraversal(root) {
  if (!root) return [];

  let stack = [root];
  let result = [];

  while (stack.length) {
    let node = stack.pop();
    result.push(node.val);

    if (node.right) stack.push(node.right);
    if (node.left) stack.push(node.left);
  }

  return result;
}
```

---

### ⏱️ Time & Space Complexity

| Approach  | Time Complexity | Space Complexity   |
| --------- | --------------- | ------------------ |
| Recursive | O(n)            | O(h) (stack space) |
| Iterative | O(n)            | O(n)               |

> where `n = number of nodes`, and `h = height of the tree`

---

## ✅ **2. Inorder Traversal of Binary Tree**

### 🧩 Problem Statement

Given the `root` of a binary tree, return the **inorder traversal** of its node values.

> **Inorder Traversal Order**: `Left → Root → Right`

---

### 🧪 Test Cases

#### Test Case 1:

```
Input:
    1
     \
      2
     /
    3

Output: [1, 3, 2]
```

#### Test Case 2:

```
Input:
      4
     / \
    2   5
   / \
  1   3

Output: [1, 2, 3, 4, 5]
```

#### Test Case 3:

```
Input: null

Output: []
```

#### Test Case 4:

```
Input:
      10
     /
    5
   /
  2

Output: [2, 5, 10]
```

---

### 💡 Intuition

In **inorder traversal**, we:

1. Recursively visit the **left subtree**.
2. Visit the **current node**.
3. Recursively visit the **right subtree**.

It is especially useful in **Binary Search Trees** (BST), where inorder traversal yields elements in **sorted order**.

---

### 🧪 Dry Run (Recursive)

#### Tree:

```
    2
   / \
  1   3
```

1. Traverse left: 1 → `[1]`
2. Visit 2 → `[1, 2]`
3. Traverse right: 3 → `[1, 2, 3]`

---

### ✅ Approach 1: Recursive Inorder Traversal

#### 🔗 Algorithm:

1. Initialize an empty result array.
2. Define a recursive function:

   - If node is null, return.
   - Call the function on the left child.
   - Add the node’s value to result.
   - Call the function on the right child.

3. Return result.

---

#### ✅ JavaScript Code (Recursive)

```javascript
function inorderTraversal(root) {
  const result = [];

  function dfs(node) {
    if (!node) return;
    dfs(node.left); // Traverse left
    result.push(node.val); // Visit root
    dfs(node.right); // Traverse right
  }

  dfs(root);
  return result;
}
```

---

### ✅ Approach 2: Iterative Inorder Using Stack

#### 🔗 Algorithm:

1. Use a stack to simulate recursion.
2. Traverse to the **leftmost node**, pushing all nodes along the path.
3. Pop from the stack, visit the node, and move to its right child.
4. Repeat until both stack and current node are null.

---

#### ✅ JavaScript Code (Iterative)

```javascript
function inorderTraversal(root) {
  const result = [];
  const stack = [];
  let current = root;

  while (current || stack.length > 0) {
    while (current) {
      stack.push(current);
      current = current.left;
    }
    current = stack.pop();
    result.push(current.val);
    current = current.right;
  }

  return result;
}
```

---

### ⏱️ Time & Space Complexity

| Approach  | Time Complexity | Space Complexity |
| --------- | --------------- | ---------------- |
| Recursive | O(n)            | O(h)             |
| Iterative | O(n)            | O(n)             |

> `n = number of nodes`, `h = height of the tree`

---

### 📌 Summary Table

| Step        | Recursive                  | Iterative                 |
| ----------- | -------------------------- | ------------------------- |
| Visit Order | Left → Root → Right        | Left → Root → Right       |
| Space Usage | Call stack (O(h))          | Explicit stack (O(n))     |
| Use Case    | Simplest for BST traversal | No recursion environments |

---

## ✅ **3. Postorder Traversal of Binary Tree**

### 🧩 Problem Statement

Given the `root` of a binary tree, return the **postorder traversal** of its node values.

> **Postorder Traversal Order**: `Left → Right → Root`

---

### 🧪 Test Cases

#### Test Case 1:

```
Input:
    1
     \
      2
     /
    3

Output: [3, 2, 1]
```

#### Test Case 2:

```
Input:
        4
       / \
      2   6
     / \
    1   3

Output: [1, 3, 2, 6, 4]
```

#### Test Case 3:

```
Input: null

Output: []
```

#### Test Case 4:

```
Input:
      5
     /
    4
   /
  3

Output: [3, 4, 5]
```

---

### 💡 Intuition

In **postorder traversal**, we visit:

1. The **left subtree**,
2. The **right subtree**,
3. And then the **root** node.

It is useful for **deleting trees**, evaluating **postfix expressions**, or when bottom-up processing is required.

---

### 🧪 Dry Run (Recursive)

#### Tree:

```
    1
   / \
  2   3
```

- Traverse left: 2 → `[2]`
- Traverse right: 3 → `[2, 3]`
- Visit root: 1 → `[2, 3, 1]`

---

### ✅ Approach 1: Recursive Postorder Traversal

#### 🔗 Algorithm:

1. Traverse the **left** subtree.
2. Traverse the **right** subtree.
3. Visit the **node** (push its value to result).

---

#### ✅ JavaScript Code (Recursive)

```javascript
function postorderTraversal(root) {
  const result = [];

  function dfs(node) {
    if (!node) return;
    dfs(node.left); // Left
    dfs(node.right); // Right
    result.push(node.val); // Root
  }

  dfs(root);
  return result;
}
```

---

### ✅ Approach 2: Iterative Postorder Using Two Stacks

#### 🔗 Algorithm:

1. Use two stacks `s1` and `s2`.
2. Push root to `s1`. While `s1` is not empty:

   - Pop from `s1`, push it to `s2`.
   - Push **left** and **right** children to `s1`.

3. Pop all items from `s2` to get postorder.

---

#### ✅ JavaScript Code (Two Stacks)

```javascript
function postorderTraversal(root) {
  if (!root) return [];

  const s1 = [root];
  const s2 = [];
  const result = [];

  while (s1.length > 0) {
    const node = s1.pop();
    s2.push(node);
    if (node.left) s1.push(node.left);
    if (node.right) s1.push(node.right);
  }

  while (s2.length > 0) {
    result.push(s2.pop().val);
  }

  return result;
}
```

---

### ✅ Approach 3: Iterative Using One Stack (Modified)

This is trickier and uses a pointer to track the last visited node.

---

### ⏱️ Time & Space Complexity

| Approach             | Time Complexity | Space Complexity |
| -------------------- | --------------- | ---------------- |
| Recursive            | O(n)            | O(h)             |
| Iterative (2 stacks) | O(n)            | O(n)             |

> where `n = number of nodes`, and `h = height of tree`

---

### 📌 Summary Table

| Traversal Type | Visiting Order             | Recursive | Iterative (2 stacks) |
| -------------- | -------------------------- | --------- | -------------------- |
| **Postorder**  | Left → Right → Root        | ✅ Easy   | ✅ Efficient         |
| Use Case       | Delete Tree, Evaluate Expr | ✅        | ✅                   |

---

## ✅ **4. Level Order Traversal of Binary Tree**

### 🧩 Problem Statement

Given the `root` of a binary tree, return the **level order traversal** of its nodes' values.

> Traverse nodes **level by level from left to right**.

---

### 🧪 Test Cases

#### Test Case 1:

```
Input:
    1
   / \
  2   3

Output: [[1], [2, 3]]
```

#### Test Case 2:

```
Input:
      10
     /  \
    20   30
   /      \
  40       50

Output: [[10], [20, 30], [40, 50]]
```

#### Test Case 3:

```
Input: null

Output: []
```

---

### 💡 Intuition

We process nodes **level-by-level**, using a **queue** to:

1. Dequeue the front node
2. Add its children to the queue
3. Repeat until all levels are processed

---

### 🧪 Dry Run

```
Input Tree:
      1
     / \
    2   3
   / \
  4   5

Queue:
[1] -> [2, 3] -> [3, 4, 5] ...

Output:
[[1], [2, 3], [4, 5]]
```

---

### ✅ JavaScript Code (Level Order)

```javascript
function levelOrder(root) {
  if (!root) return [];

  const queue = [root];
  const result = [];

  while (queue.length > 0) {
    let levelSize = queue.length;
    let level = [];

    for (let i = 0; i < levelSize; i++) {
      const node = queue.shift();
      level.push(node.val);
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }

    result.push(level);
  }

  return result;
}
```

---

### ⏱️ Time & Space Complexity

- **Time:** O(n)
- **Space:** O(n) (queue + result)

---

## ✅ **5. Level Order Traversal in Spiral Form (Zigzag)**

### 🧩 Problem Statement

Given the `root` of a binary tree, return the **zigzag level order traversal**:

> Nodes are traversed **left-to-right** on one level and **right-to-left** on the next.

---

### 🧪 Test Cases

#### Test Case 1:

```
Input:
      1
     / \
    2   3

Output: [[1], [3, 2]]
```

#### Test Case 2:

```
Input:
      10
     /  \
    5   15
   / \    \
  2   7    20

Output: [[10], [15, 5], [2, 7, 20]]
```

---

### 💡 Intuition

Use a **queue** to process level by level, and use a **boolean flag** to reverse the order of nodes at every alternate level.

---

### ✅ JavaScript Code (Zigzag Traversal)

```javascript
function zigzagLevelOrder(root) {
  if (!root) return [];

  const result = [];
  const queue = [root];
  let leftToRight = true;

  while (queue.length > 0) {
    let levelSize = queue.length;
    let level = [];

    for (let i = 0; i < levelSize; i++) {
      const node = queue.shift();

      if (leftToRight) {
        level.push(node.val);
      } else {
        level.unshift(node.val);
      }

      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }

    result.push(level);
    leftToRight = !leftToRight;
  }

  return result;
}
```

---

### ⏱️ Time & Space Complexity

- **Time:** O(n)
- **Space:** O(n)

---

### 📌 Summary Table

| Traversal Type     | Pattern               | Use Case                   |
| ------------------ | --------------------- | -------------------------- |
| Level Order        | Left → Right by level | BFS, shortest path in tree |
| Zigzag Level Order | L→R → R→L → L→R → …   | Tree visualizations, games |

---

# ✅ **6. All Tree Traversals in One Traversal (Preorder, Inorder, Postorder)**

## 🧩 Problem Statement

Given the root of a binary tree, return all three traversals — **Preorder**, **Inorder**, and **Postorder** — in a **single traversal** without running three separate functions.

---

## 🧪 Test Cases

### Test Case 1:

```
Input:
      1
     / \
    2   3

Output:
Preorder:  [1, 2, 3]
Inorder:   [2, 1, 3]
Postorder: [2, 3, 1]
```

### Test Case 2:

```
Input:
        10
       /  \
      5    20
     / \     \
    3   8     30

Output:
Preorder:  [10, 5, 3, 8, 20, 30]
Inorder:   [3, 5, 8, 10, 20, 30]
Postorder: [3, 8, 5, 30, 20, 10]
```

---

## 💡 Intuition

We can use a **stack** where each node is pushed along with a `state` (1, 2, 3):

- **State 1**: Process for Preorder, move to left child
- **State 2**: Process for Inorder, move to right child
- **State 3**: Process for Postorder, then pop from stack

This allows us to simulate all three traversals in a single iteration.

---

## 🧪 Dry Run

### Tree:

```
    1
   / \
  2   3
```

Stack progression:

1. Push `(1, 1)` → preorder → push `(1, 2)`, push `(2, 1)`
2. Push `(2, 1)` → preorder → push `(2, 2)`, left null
3. Pop to `(2, 2)` → inorder → push `(2, 3)`, right null
4. Pop to `(2, 3)` → postorder
5. Continue with `(1, 2)` → inorder → push `(1, 3)`, push `(3, 1)`...

---

## ✅ JavaScript Code

```javascript
function allTraversals(root) {
  if (!root) return [[], [], []];

  const preorder = [];
  const inorder = [];
  const postorder = [];

  const stack = [{ node: root, state: 1 }];

  while (stack.length > 0) {
    const top = stack[stack.length - 1];

    if (top.state === 1) {
      preorder.push(top.node.val);
      top.state++;
      if (top.node.left) {
        stack.push({ node: top.node.left, state: 1 });
      }
    } else if (top.state === 2) {
      inorder.push(top.node.val);
      top.state++;
      if (top.node.right) {
        stack.push({ node: top.node.right, state: 1 });
      }
    } else {
      postorder.push(top.node.val);
      stack.pop();
    }
  }

  return [preorder, inorder, postorder];
}
```

---

## ⏱️ Time & Space Complexity

| Metric    | Value                  |
| --------- | ---------------------- |
| **Time**  | O(n)                   |
| **Space** | O(n) (stack + outputs) |

> `n = number of nodes`

---

## 📌 Summary Table

| Traversal Type | Order               | Purpose/Use Case              |
| -------------- | ------------------- | ----------------------------- |
| Preorder       | Root → Left → Right | Copy tree, prefix notation    |
| Inorder        | Left → Root → Right | Sorted order in BST           |
| Postorder      | Left → Right → Root | Delete tree, postfix notation |

---

# **Medium Problems**

## ✅ **1. Height of a Binary Tree**

### 🧩 Problem Statement

Given the `root` of a binary tree, return its **height**.

> The **height** of a binary tree is the **number of edges** in the **longest path** from the root to a leaf node.
> Some definitions count the number of **nodes** instead — in that case, just add `+1`.

---

### 🧪 Test Cases

#### Test Case 1:

```
Input:
    1
   / \
  2   3

Output: 1
```

#### Test Case 2:

```
Input:
      1
     /
    2
   /
  3

Output: 2
```

#### Test Case 3:

```
Input:
      10
     /  \
    20   30
         /
        40

Output: 2
```

#### Test Case 4:

```
Input: null

Output: -1 (or 0 if counting nodes)
```

---

### 💡 Intuition

The height of a binary tree is:

- **0** for a single node tree (1 node, 0 edges)
- **Max height of left/right subtree + 1**

Use **recursion** to get the height of both left and right subtrees, and return the **maximum + 1**.

---

### 🧪 Dry Run

#### Tree:

```
    1
   / \
  2   3
```

- Height(2) = 0, Height(3) = 0 → Height(1) = max(0, 0) + 1 = **1**

---

### ✅ Approach: Recursive DFS

---

#### ✅ JavaScript Code

```javascript
function height(root) {
  if (!root) return -1; // if height is counted in edges
  const leftHeight = height(root.left);
  const rightHeight = height(root.right);
  return Math.max(leftHeight, rightHeight) + 1;
}
```

> 💡 If counting **nodes** in height, use `return 0` for null base case instead of `-1`.

---

### ⏱️ Time & Space Complexity

| Metric | Value        |
| ------ | ------------ |
| Time   | O(n)         |
| Space  | O(h) (stack) |

> `n` is number of nodes, `h` is height of the tree

---

### 📌 Summary

| Term     | Definition                            |     |     |
| -------- | ------------------------------------- | --- | --- |
| Height   | Max number of edges from root to leaf |     |     |
| Depth    | Number of edges from root to a node   |     |     |
| Balanced | If height(left) - height(right)       | ≤ 1 |     |

---

## ✅ **2. Check if the Binary Tree is Height-Balanced**

### 🧩 Problem Statement

Given the `root` of a binary tree, determine whether the tree is **height-balanced**.

> A binary tree is **height-balanced** if for every node, the difference in height between its left and right subtree is at most **1**.

---

### 🧪 Test Cases

#### Test Case 1:

```
Input:
      1
     / \
    2   3

Output: true
```

#### Test Case 2:

```
Input:
        1
       /
      2
     /
    3

Output: false
```

#### Test Case 3:

```
Input: null

Output: true
```

#### Test Case 4:

```
Input:
       1
      / \
     2   2
    /
   3

Output: true
```

---

### 💡 Intuition

We need to check two things:

1. **Height difference** between left and right subtrees of every node is **≤ 1**
2. Both left and right subtrees are themselves balanced

A naive solution calculates the height of subtrees recursively at every node → leads to **O(n²)** time.

To optimize, we can combine **height calculation and balance checking** in a single traversal.

---

### ✅ Approach 1: Optimized Recursive (Bottom-Up)

Return height if subtree is balanced, else return -1 as an **error code**.

---

#### ✅ JavaScript Code

```javascript
function isBalanced(root) {
  function checkHeight(node) {
    if (!node) return 0;

    let left = checkHeight(node.left);
    if (left === -1) return -1;

    let right = checkHeight(node.right);
    if (right === -1) return -1;

    if (Math.abs(left - right) > 1) return -1;

    return Math.max(left, right) + 1;
  }

  return checkHeight(root) !== -1;
}
```

---

### 🧪 Dry Run

#### Tree:

```
    1
   /
  2
 /
3
```

- checkHeight(3) → 0
- checkHeight(2) → left = 1, right = 0 → diff = 1 → OK → return 2
- checkHeight(1) → left = 2, right = 0 → diff = 2 → return **-1** → unbalanced

---

### ⏱️ Time & Space Complexity

| Metric | Value            |
| ------ | ---------------- |
| Time   | O(n)             |
| Space  | O(h) (recursion) |

> `n` = number of nodes, `h` = height of tree

---

### 📌 Summary

| Check                     | Return Value |
| ------------------------- | ------------ |
| Height difference > 1     | Unbalanced   |
| Any subtree is unbalanced | Unbalanced   |
| All nodes balanced        | Balanced     |

---

## ✅ **3. Diameter of a Binary Tree**

### 🧩 Problem Statement

Given the `root` of a binary tree, return the **diameter** of the tree.

> The **diameter** (also known as **width**) of a binary tree is the **length of the longest path** between **any two nodes**, which may or may not pass through the root.

- **Length** = number of **edges** on the path.

---

### 🧪 Test Cases

#### Test Case 1:

```
Input:
    1
   / \
  2   3

Output: 2
Explanation: Path = [2 -> 1 -> 3]
```

#### Test Case 2:

```
Input:
       1
      /
     2
    /
   3
  /
 4

Output: 3
Explanation: Path = [4 -> 3 -> 2 -> 1]
```

#### Test Case 3:

```
Input:
       1
      / \
     2   3
    / \
   4   5

Output: 3
Explanation: Path = [4 -> 2 -> 5] or [4 -> 2 -> 1 -> 3]
```

---

### 💡 Intuition

At every node, the **longest path** (diameter) can be:

```
diameter = height of left subtree + height of right subtree
```

We compute the height of subtrees and update the diameter as we traverse recursively.

---

### 🧪 Dry Run

#### Tree:

```
    1
   / \
  2   3
 / \
4   5
```

- Height(4) = 0, Height(5) = 0 → Node 2 contributes diameter = 1 + 1 = 2
- Height(2) = 2 → Node 1 contributes diameter = 2 (left) + 1 (right) = 3
  → Answer = **3**

---

### ✅ Approach: DFS with Global Variable

---

#### ✅ JavaScript Code

```javascript
function diameterOfBinaryTree(root) {
  let maxDiameter = 0;

  function dfs(node) {
    if (!node) return 0;

    const left = dfs(node.left);
    const right = dfs(node.right);

    // update the diameter at every node
    maxDiameter = Math.max(maxDiameter, left + right);

    return Math.max(left, right) + 1; // return height
  }

  dfs(root);
  return maxDiameter;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(n)  |
| Space  | O(h)  |

> `n` = total nodes, `h` = height of tree (recursion stack)

---

### 📌 Summary Table

| Concept      | Formula / Idea                |
| ------------ | ----------------------------- |
| Diameter     | max(leftHeight + rightHeight) |
| At each node | Compute height and update max |
| Return value | Final value of `maxDiameter`  |

---

## ✅ **4. Maximum Path Sum in a Binary Tree**

### 🧩 Problem Statement

Given the `root` of a binary tree, return the **maximum path sum**.

> A **path** is any sequence of nodes where each pair of adjacent nodes is connected by an edge.
> A path **can start and end at any node** in the tree and **must go downwards** (no cycles or upward movement).

---

### 🧪 Test Cases

#### Test Case 1:

```
Input:
      1
     / \
    2   3

Output: 6
Explanation: Path = 2 → 1 → 3
```

#### Test Case 2:

```
Input:
       -10
       /  \
      9   20
         /  \
        15   7

Output: 42
Explanation: Path = 15 → 20 → 7
```

#### Test Case 3:

```
Input:
      2
     / \
   -1   -2

Output: 2
Explanation: Max path = [2]
```

---

### 💡 Intuition

At each node:

- The path can either:

  - Continue through **one child**, or
  - Split through **both children** (left + node + right) → this could be the answer

We need to:

1. Track the **maximum sum across all such paths** (`globalMax`)
2. Return the **maximum single-side path** to the parent node

---

### 🧪 Dry Run

#### Tree:

```
      -10
      /  \
     9   20
         / \
        15  7
```

- At 15 → return 15
- At 7 → return 7
- At 20 → left=15, right=7 → max path = 15+20+7 = **42**
- At -10 → left=9, right=20 → max path = 9 + (-10) + 42 = 41 (not better than 42)

→ Final answer = **42**

---

### ✅ JavaScript Code

```javascript
function maxPathSum(root) {
  let maxSum = -Infinity;

  function dfs(node) {
    if (!node) return 0;

    // Compute max path sum for left and right subtree
    let left = Math.max(0, dfs(node.left)); // discard negatives
    let right = Math.max(0, dfs(node.right)); // discard negatives

    // Update global max considering this node as root
    maxSum = Math.max(maxSum, left + right + node.val);

    // Return max one-side path to parent
    return node.val + Math.max(left, right);
  }

  dfs(root);
  return maxSum;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(n)  |
| Space  | O(h)  |

> `n` = number of nodes, `h` = height of tree (recursion stack)

---

### 📌 Summary

| Key Logic                        | Details                       |
| -------------------------------- | ----------------------------- |
| Discard negative paths           | `Math.max(0, dfs(...))`       |
| Track best **global split** path | `left + right + node.val`     |
| Return only **one-sided** path   | `node.val + max(left, right)` |

---

## ✅ **5. Check if Two Binary Trees are Identical**

### 🧩 Problem Statement

Given the roots of two binary trees `p` and `q`, write a function to determine whether the two trees are **identical** or not.

> Two trees are **identical** if:
>
> - They have the **same structure**
> - They have **equal node values** at every corresponding position

---

### 🧪 Test Cases

#### Test Case 1:

```
Input:
Tree 1:        1
              / \
             2   3

Tree 2:        1
              / \
             2   3

Output: true
```

#### Test Case 2:

```
Input:
Tree 1:        1
              / \
             2   3

Tree 2:        1
              / \
             2   4

Output: false
```

#### Test Case 3:

```
Input:
Tree 1: null
Tree 2: null

Output: true
```

#### Test Case 4:

```
Input:
Tree 1: null
Tree 2: 1

Output: false
```

---

### 💡 Intuition

Use **DFS (recursion)** to compare nodes one-by-one:

1. If both nodes are `null` → return `true`
2. If one is `null` and the other is not → return `false`
3. If values of both nodes are not equal → return `false`
4. Recursively check **left and right subtrees**

---

### 🧪 Dry Run

#### Tree A:

```
    1
   / \
  2   3
```

#### Tree B:

```
    1
   / \
  2   3
```

- Node(1 vs 1) → equal
- Left(2 vs 2) → equal
- Right(3 vs 3) → equal → ✅ return `true`

---

### ✅ JavaScript Code (Recursive)

```javascript
function isSameTree(p, q) {
  if (!p && !q) return true;
  if (!p || !q) return false;
  if (p.val !== q.val) return false;

  return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
}
```

---

### ✅ JavaScript Code (Iterative - using queue)

```javascript
function isSameTree(p, q) {
  const queue = [[p, q]];

  while (queue.length > 0) {
    const [node1, node2] = queue.shift();

    if (!node1 && !node2) continue;
    if (!node1 || !node2 || node1.val !== node2.val) return false;

    queue.push([node1.left, node2.left]);
    queue.push([node1.right, node2.right]);
  }

  return true;
}
```

---

### ⏱️ Time & Space Complexity

| Metric        | Value |
| ------------- | ----- |
| Time          | O(n)  |
| Space (Rec.)  | O(h)  |
| Space (Iter.) | O(n)  |

> `n` = number of nodes, `h` = height of tree

---

### 📌 Summary

| Condition             | Return   |
| --------------------- | -------- |
| Both nodes are null   | ✅ true  |
| One node is null      | ❌ false |
| Values differ         | ❌ false |
| All match recursively | ✅ true  |

---

## ✅ **6. Zig Zag Traversal of Binary Tree (Spiral Level Order Traversal)**

### 🧩 Problem Statement

Given the `root` of a binary tree, return its **zigzag level order traversal**.

> Traverse nodes level by level, but **alternate the direction** of traversal for each level:

- Level 0: **Left to Right**
- Level 1: **Right to Left**
- Level 2: **Left to Right**
- … and so on

---

### 🧪 Test Cases

#### Test Case 1:

```
Input:
     1
    / \
   2   3

Output: [[1], [3, 2]]
```

#### Test Case 2:

```
Input:
       10
      /  \
     20   30
    / \     \
   40 50     60

Output: [[10], [30, 20], [40, 50, 60]]
```

#### Test Case 3:

```
Input: null

Output: []
```

---

### 💡 Intuition

This is a variation of **level order traversal**:

- Use a **queue** to traverse level by level (BFS)
- Use a **boolean flag** `leftToRight` to reverse the order of each level

---

### 🧪 Dry Run

#### Tree:

```
      1
     / \
    2   3
   / \
  4   5

Traversal steps:
- Level 0 → [1] → left-to-right
- Level 1 → [3, 2] → right-to-left
- Level 2 → [4, 5] → left-to-right
```

---

### ✅ JavaScript Code

```javascript
function zigzagLevelOrder(root) {
  if (!root) return [];

  const result = [];
  const queue = [root];
  let leftToRight = true;

  while (queue.length > 0) {
    let size = queue.length;
    let level = [];

    for (let i = 0; i < size; i++) {
      let node = queue.shift();

      // Insert in order based on direction
      if (leftToRight) {
        level.push(node.val);
      } else {
        level.unshift(node.val); // reverse direction
      }

      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }

    result.push(level);
    leftToRight = !leftToRight; // flip direction
  }

  return result;
}
```

---

### ✅ Approach 2: Two Stacks (Alternative)

- Use two stacks: `currentLevel` and `nextLevel`
- Track direction (`leftToRight`)
- Push children in reverse order based on direction

---

### ⏱️ Time & Space Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(n)  |
| Space  | O(n)  |

> `n` = number of nodes

---

### 📌 Summary Table

| Level | Direction    | Traversal        |
| ----- | ------------ | ---------------- |
| 0     | left → right | push normally    |
| 1     | right → left | unshift at front |
| 2     | left → right | push normally    |

---

## ✅ **7. Boundary Traversal of Binary Tree**

### 🧩 Problem Statement

Given the `root` of a binary tree, return its **boundary traversal** in **anti-clockwise** direction starting from the root.

> Boundary includes:

1. **Left boundary** (excluding leaf nodes)
2. **All leaf nodes** (left to right)
3. **Right boundary** (excluding leaf nodes, in reverse)

---

### 🧪 Test Cases

#### Test Case 1:

```
Input:
       1
      / \
     2   3
    / \   \
   4   5   6

Output: [1, 2, 4, 5, 6, 3]
```

#### Test Case 2:

```
Input:
     1
    /
   2
  /
 3

Output: [1, 2, 3]
```

#### Test Case 3:

```
Input:
    1
     \
      2
       \
        3

Output: [1, 3, 2]
```

#### Test Case 4:

```
Input: null

Output: []
```

---

### 💡 Intuition

We divide the task into 3 parts:

#### 1. **Left Boundary**:

- From root's left child, go down the **left side**
- **Skip** leaf nodes

#### 2. **Leaf Nodes**:

- Perform a **DFS traversal**
- Add node if it has **no children**

#### 3. **Right Boundary**:

- From root's right child, go down the **right side**
- **Skip** leaf nodes
- **Store separately**, then **reverse**

---

### 🧪 Dry Run

For Tree:

```
        1
       / \
      2   3
     / \   \
    4   5   6

- Left Boundary: 2
- Leaves: 4, 5, 6
- Right Boundary (reverse): 3

→ Result: [1, 2, 4, 5, 6, 3]
```

---

### ✅ JavaScript Code

```javascript
function boundaryOfBinaryTree(root) {
  if (!root) return [];

  const result = [];

  function isLeaf(node) {
    return !node.left && !node.right;
  }

  function addLeftBoundary(node) {
    let curr = node.left;
    while (curr) {
      if (!isLeaf(curr)) result.push(curr.val);
      curr = curr.left ? curr.left : curr.right;
    }
  }

  function addLeaves(node) {
    if (!node) return;
    if (isLeaf(node)) {
      result.push(node.val);
      return;
    }
    addLeaves(node.left);
    addLeaves(node.right);
  }

  function addRightBoundary(node) {
    let curr = node.right;
    const stack = [];
    while (curr) {
      if (!isLeaf(curr)) stack.push(curr.val);
      curr = curr.right ? curr.right : curr.left;
    }
    while (stack.length) {
      result.push(stack.pop());
    }
  }

  if (!isLeaf(root)) result.push(root.val);

  addLeftBoundary(root);
  addLeaves(root);
  addRightBoundary(root);

  return result;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Value                                |
| ------ | ------------------------------------ |
| Time   | O(n)                                 |
| Space  | O(h) (recursion stack) or O(n) total |

> `n` = number of nodes, `h` = height of tree

---

### 📌 Summary of Components

| Part           | How It Works                       |
| -------------- | ---------------------------------- |
| Left Boundary  | Traverse down left, skip leaves    |
| Leaf Nodes     | DFS to collect all leaf nodes      |
| Right Boundary | Traverse down right, reverse order |

---

## ✅ **8. Vertical Order Traversal of Binary Tree**

### 🧩 Problem Statement

Given the `root` of a binary tree, return the **vertical order traversal** of its nodes’ values.

> Traverse nodes column-by-column from **left to right**, and **top to bottom** within each column.
> If two nodes share the same position (row and column), **order them by their value**.

---

### 🧪 Test Cases

#### Test Case 1:

```
Input:
      1
     / \
    2   3
   / \ / \
  4  5 6  7

Output: [[4], [2], [1, 5, 6], [3], [7]]
```

#### Test Case 2:

```
Input:
      3
     / \
    9   20
        / \
       15  7

Output: [[9], [3, 15], [20], [7]]
```

#### Test Case 3:

```
Input:
     1
      \
       2
        \
         3

Output: [[1], [2], [3]]
```

---

### 💡 Intuition

Use **BFS traversal** and keep track of:

- `hd` (horizontal distance from root): root = 0, left = -1, right = +1
- `level` (depth)

Store the values in a **map** `Map<hd, [node values]>`, and sort by:

- Horizontal distance (column)
- Then level (row)
- Then value if required

---

### 🧪 Dry Run

```
Tree:
      1
     / \
    2   3
   /     \
  4       5

BFS queue: [ (1, hd=0, level=0) ]
→ Map:
  hd=-2 → [4]
  hd=-1 → [2]
  hd=0  → [1]
  hd=1  → [3]
  hd=2  → [5]
```

---

### ✅ JavaScript Code (BFS)

```javascript
function verticalTraversal(root) {
  if (!root) return [];

  const map = new Map(); // hd => [ [level, value] ]
  const queue = [{ node: root, hd: 0, level: 0 }];
  let minHd = 0,
    maxHd = 0;

  while (queue.length) {
    const { node, hd, level } = queue.shift();

    if (!map.has(hd)) map.set(hd, []);
    map.get(hd).push([level, node.val]);

    minHd = Math.min(minHd, hd);
    maxHd = Math.max(maxHd, hd);

    if (node.left)
      queue.push({ node: node.left, hd: hd - 1, level: level + 1 });
    if (node.right)
      queue.push({ node: node.right, hd: hd + 1, level: level + 1 });
  }

  const result = [];

  for (let hd = minHd; hd <= maxHd; hd++) {
    const values = map.get(hd);
    values.sort((a, b) => {
      if (a[0] !== b[0]) return a[0] - b[0]; // level
      return a[1] - b[1]; // value
    });
    result.push(values.map((x) => x[1]));
  }

  return result;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Value      |
| ------ | ---------- |
| Time   | O(n log n) |
| Space  | O(n)       |

> Because we sort by level and value for each column.

---

### 📌 Summary

| Concept             | Technique Used        |
| ------------------- | --------------------- |
| Horizontal Distance | Left = -1, Right = +1 |
| Level Order         | BFS + coordinates     |
| Column Sort Order   | min → max hd          |
| Row Tie-breaker     | Level, then value     |

---

## ✅ **9. Top View of Binary Tree**

### 🧩 Problem Statement

Given the `root` of a binary tree, return the **top view** of the tree.

> The **top view** includes all nodes that are **visible when the tree is viewed from the top**.
> For each vertical column, only the **first node encountered (from top to bottom)** is included.

---

### 🧪 Test Cases

#### Test Case 1:

```
Input:
        1
       / \
      2   3
       \   \
        4   5

Output: [2, 1, 3, 5]
```

#### Test Case 2:

```
Input:
        10
       /  \
      20   30
     /       \
    40        60

Output: [40, 20, 10, 30, 60]
```

#### Test Case 3:

```
Input:
      1
     /
    2
   /
  3

Output: [3, 2, 1]
```

#### Test Case 4:

```
Input: null

Output: []
```

---

### 💡 Intuition

Use **level order traversal (BFS)** and track the **horizontal distance (`hd`)** of each node:

- Root has `hd = 0`
- Left child has `hd - 1`, right child has `hd + 1`
- For each horizontal distance, **store only the first node** encountered.

---

### 🧪 Dry Run

#### Tree:

```
        1
       / \
      2   3
       \   \
        4   5
```

- hd = -1 → 2
- hd = 0 → 1
- hd = +1 → 3
- hd = +2 → 5

→ Top View: `[2, 1, 3, 5]`

---

### ✅ JavaScript Code

```javascript
function topView(root) {
  if (!root) return [];

  const queue = [{ node: root, hd: 0 }];
  const map = new Map(); // hd => node.val
  let minHd = 0,
    maxHd = 0;

  while (queue.length > 0) {
    const { node, hd } = queue.shift();

    // Add only the first node at each horizontal distance
    if (!map.has(hd)) {
      map.set(hd, node.val);
    }

    minHd = Math.min(minHd, hd);
    maxHd = Math.max(maxHd, hd);

    if (node.left) queue.push({ node: node.left, hd: hd - 1 });
    if (node.right) queue.push({ node: node.right, hd: hd + 1 });
  }

  const result = [];
  for (let hd = minHd; hd <= maxHd; hd++) {
    result.push(map.get(hd));
  }

  return result;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(n)  |
| Space  | O(n)  |

> `n` = number of nodes in the binary tree

---

### 📌 Summary

| Concept             | Explanation                             |
| ------------------- | --------------------------------------- |
| Horizontal Distance | Root = 0, Left = -1, Right = +1         |
| Traverse with BFS   | Level order ensures top-most node first |
| Track with Map      | Store only first node at each `hd`      |
| Result Order        | From min hd to max hd                   |

---

## ✅ **10. Bottom View of Binary Tree**

### 🧩 Problem Statement

Given the `root` of a binary tree, return the **bottom view** of the tree.

> The **bottom view** consists of the nodes that are visible **when the tree is viewed from the bottom**.
> For each vertical column (horizontal distance), return the **last (bottom-most)** node encountered during level-order traversal.

---

### 🧪 Test Cases

#### Test Case 1:

```
Input:
        20
       /  \
      8   22
     / \    \
    5  3     25
      / \
     10 14

Output: [5, 10, 3, 14, 25]
```

#### Test Case 2:

```
Input:
      1
     / \
    2   3
         \
          4
           \
            5

Output: [2, 1, 3, 4, 5]
```

#### Test Case 3:

```
Input:
      1
       \
        2
         \
          3

Output: [1, 2, 3]
```

---

### 💡 Intuition

Like **Top View**, we use:

- **Level-order traversal (BFS)** to guarantee bottom-most node at each horizontal distance.
- A **Map** to store `(hd → node.val)` where we **overwrite** the value for each horizontal distance (hd), ensuring the **last** node encountered is kept.

---

### 🧪 Dry Run

#### Tree:

```
        20
       /  \
      8   22
     / \    \
    5   3    25
       / \
      10 14

Horizontal Distance (hd) mapping:
- hd -2: 5
- hd -1: 10
- hd  0: 3
- hd +1: 14
- hd +2: 25

→ Bottom View: [5, 10, 3, 14, 25]
```

---

### ✅ JavaScript Code

```javascript
function bottomView(root) {
  if (!root) return [];

  const map = new Map(); // hd => node.val
  const queue = [{ node: root, hd: 0 }];
  let minHd = 0,
    maxHd = 0;

  while (queue.length > 0) {
    const { node, hd } = queue.shift();

    // Overwrite value at hd to ensure bottom-most node
    map.set(hd, node.val);

    minHd = Math.min(minHd, hd);
    maxHd = Math.max(maxHd, hd);

    if (node.left) queue.push({ node: node.left, hd: hd - 1 });
    if (node.right) queue.push({ node: node.right, hd: hd + 1 });
  }

  const result = [];
  for (let hd = minHd; hd <= maxHd; hd++) {
    result.push(map.get(hd));
  }

  return result;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(n)  |
| Space  | O(n)  |

> `n` = number of nodes

---

### 📌 Summary Table

| Term                | Meaning                                 |
| ------------------- | --------------------------------------- |
| Horizontal Distance | Left = -1, Right = +1 from parent       |
| Bottom-most node    | Last node seen at each `hd` in BFS      |
| Result Order        | Leftmost to rightmost (`minHd → maxHd`) |

---

## ✅ **11. Left & Right View of Binary Tree**

### 🧩 Problem Statement

Given the `root` of a binary tree, return its:

- **Left View**: Nodes visible when the tree is viewed from the **left side**.
- **Right View**: Nodes visible when the tree is viewed from the **right side**.

> For both views, include **only the first node at each level** when viewed from the left/right direction.

---

### 🧪 Test Cases

#### Test Case 1:

```
Tree:
       1
      / \
     2   3
      \   \
       4   5

Left View:  [1, 2, 4]
Right View: [1, 3, 5]
```

---

#### Test Case 2:

```
Tree:
       10
      /  \
     20  30
    /
   40

Left View:  [10, 20, 40]
Right View: [10, 30, 40]
```

---

#### Test Case 3:

```
Input: null

Output: [] (for both views)
```

---

### 💡 Intuition

Use **Level Order Traversal (BFS)** with a queue:

- **Left View**: take the **first node** at each level
- **Right View**: take the **last node** at each level

---

### 🧪 Dry Run

```
Tree:
      1
     / \
    2   3
         \
          4

Level 0 → [1] → pick 1
Level 1 → [2, 3] → left: 2, right: 3
Level 2 → [4] → both pick 4
```

---

### ✅ JavaScript Code – Left View

```javascript
function leftView(root) {
  if (!root) return [];

  const result = [];
  const queue = [root];

  while (queue.length) {
    const size = queue.length;
    for (let i = 0; i < size; i++) {
      const node = queue.shift();
      if (i === 0) result.push(node.val); // leftmost
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
  }

  return result;
}
```

---

### ✅ JavaScript Code – Right View

```javascript
function rightView(root) {
  if (!root) return [];

  const result = [];
  const queue = [root];

  while (queue.length) {
    const size = queue.length;
    for (let i = 0; i < size; i++) {
      const node = queue.shift();
      if (i === size - 1) result.push(node.val); // rightmost
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
  }

  return result;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(n)  |
| Space  | O(n)  |

> `n` = total number of nodes

---

### 📌 Summary

| View       | Key Logic                   |
| ---------- | --------------------------- |
| Left View  | First node at each level    |
| Right View | Last node at each level     |
| Technique  | Level Order Traversal (BFS) |

---

## ✅ **12. Symmetric Binary Tree**

### 🧩 Problem Statement

Given the `root` of a binary tree, check whether it is **symmetric** around its center.

> A binary tree is **symmetric** if the left subtree is a mirror reflection of the right subtree.

---

### 🧪 Test Cases

#### Test Case 1:

```
Input:
       1
      / \
     2   2
    / \ / \
   3  4 4  3

Output: true
```

#### Test Case 2:

```
Input:
       1
      / \
     2   2
      \   \
      3    3

Output: false
```

#### Test Case 3:

```
Input:
       1
      / \
     2   2
    /     \
   3       3

Output: true
```

#### Test Case 4:

```
Input: null

Output: true
```

---

### 💡 Intuition

To be symmetric, the left and right subtrees must be:

- Structurally **mirror images**
- Contain the **same values** in mirrored positions

We recursively compare:

- Left subtree of the left node ↔ Right subtree of the right node
- Right subtree of the left node ↔ Left subtree of the right node

---

### 🧪 Dry Run

Example:

```
    1
   / \
  2   2
 /     \
3       3

- Compare 2 and 2 → OK
- Compare 3 and 3 → OK
- Compare null and null → OK
→ Tree is symmetric → ✅
```

---

### ✅ JavaScript Code (Recursive)

```javascript
function isSymmetric(root) {
  if (!root) return true;

  function isMirror(t1, t2) {
    if (!t1 && !t2) return true;
    if (!t1 || !t2 || t1.val !== t2.val) return false;

    return isMirror(t1.left, t2.right) && isMirror(t1.right, t2.left);
  }

  return isMirror(root.left, root.right);
}
```

---

### ✅ JavaScript Code (Iterative with Queue)

```javascript
function isSymmetric(root) {
  if (!root) return true;

  const queue = [[root.left, root.right]];

  while (queue.length > 0) {
    const [left, right] = queue.shift();

    if (!left && !right) continue;
    if (!left || !right || left.val !== right.val) return false;

    queue.push([left.left, right.right]);
    queue.push([left.right, right.left]);
  }

  return true;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Value                              |
| ------ | ---------------------------------- |
| Time   | O(n)                               |
| Space  | O(h) → Recursive (or O(n) for BFS) |

> `n` = total nodes, `h` = height of tree

---

### 📌 Summary

| Step              | Description                               |
| ----------------- | ----------------------------------------- |
| Base check        | null vs null → true                       |
| Mirror check      | t1.val === t2.val                         |
| Recursive compare | t1.left ↔ t2.right and t1.right ↔ t2.left |

---

# **Hard Problems**

## ✅ **1. Root to Node Path in Binary Tree**

### 🧩 Problem Statement

Given the `root` of a binary tree and a target `value`, return the path from the **root node to the target node** as a list of values.

> If the target does not exist in the tree, return an empty list.

---

### 🧪 Test Cases

#### Test Case 1:

```
Tree:
        1
       / \
      2   3
     / \
    4   5

Target: 5

Output: [1, 2, 5]
```

#### Test Case 2:

```
Tree:
        7
       / \
      4   9
         /
        8

Target: 8

Output: [7, 9, 8]
```

#### Test Case 3:

```
Tree:
    1
Target: 2

Output: []
```

---

### 💡 Intuition

Perform a **DFS traversal** and build the path as you go:

- If the current node is `null` → return `false`
- If the current node is the **target** → return `true`
- Otherwise, recursively search in the left and right subtrees
- If found in either, return `true`
- Else, backtrack (pop from path)

---

### 🧪 Dry Run

```
Tree:
        1
       / \
      2   3
     / \
    4   5

Target = 5

Path:
- Push 1 → not target
- Push 2 → not target
- Left: 4 → return false → backtrack
- Right: 5 → found → return true

Final path: [1, 2, 5]
```

---

### ✅ JavaScript Code

```javascript
function rootToNodePath(root, target) {
  const path = [];

  function dfs(node) {
    if (!node) return false;

    path.push(node.val); // add to path

    if (node.val === target) return true;

    if (dfs(node.left) || dfs(node.right)) return true;

    path.pop(); // backtrack if not in path
    return false;
  }

  dfs(root);
  return path;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(n)  |
| Space  | O(h)  |

> `n` = number of nodes
> `h` = height of tree (recursion stack + path array)

---

### 📌 Summary

| Step         | Action                       |
| ------------ | ---------------------------- |
| Preorder DFS | Traverse while building path |
| Match target | Return true & retain path    |
| Not found    | Backtrack (pop from path)    |

---

## ✅ **2. Lowest Common Ancestor (LCA) in Binary Tree**

### 🧩 Problem Statement

Given the `root` of a binary tree and two nodes `p` and `q`, return their **Lowest Common Ancestor (LCA)**.

> The **LCA** of two nodes is the **lowest node** in the tree that has both `p` and `q` as **descendants**.

---

### 🧪 Test Cases

#### Test Case 1:

```
Tree:
        3
       / \
      5   1
     / \ / \
    6  2 0  8
      / \
     7   4

Input: p = 5, q = 1
Output: 3
```

#### Test Case 2:

```
Tree:
        3
       / \
      5   1
     / \
    6   2
        / \
       7   4

Input: p = 5, q = 4
Output: 5
```

#### Test Case 3:

```
Tree:
    1
   /
  2

Input: p = 1, q = 2
Output: 1
```

---

### 💡 Intuition

Use **Postorder DFS traversal** to find the node where both `p` and `q` exist in different subtrees.

#### Logic:

- If root is null → return null
- If root is `p` or `q` → return root
- Recursively check left and right subtrees

  - If both return non-null → current root is LCA
  - If one is non-null → propagate upward
  - If both null → return null

---

### 🧪 Dry Run

#### Tree:

```
        3
       / \
      5   1
         / \
        0   8

Input: p = 5, q = 1

- Left returns node 5
- Right returns node 1
- So, root (3) is LCA
```

---

### ✅ JavaScript Code (Recursive)

```javascript
function lowestCommonAncestor(root, p, q) {
  if (!root || root === p || root === q) return root;

  const left = lowestCommonAncestor(root.left, p, q);
  const right = lowestCommonAncestor(root.right, p, q);

  if (left && right) return root; // p and q found in both sides
  return left || right; // propagate non-null result
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Value        |
| ------ | ------------ |
| Time   | O(n)         |
| Space  | O(h) (stack) |

> `n` = number of nodes, `h` = height of tree

---

### 📌 Summary

| Condition             | Action                      |
| --------------------- | --------------------------- |
| root is null          | return null                 |
| root = p or q         | return root                 |
| left & right not null | return root (LCA found)     |
| only one non-null     | return that one (propagate) |

---

## ✅ **3. Maximum Width of a Binary Tree**

### 🧩 Problem Statement

Given the `root` of a binary tree, return the **maximum width** of the tree.

> The **width** of a level is defined as the **number of nodes** between the **leftmost and rightmost non-null nodes**, counting the `nulls` in between as well.

---

### 🧪 Test Cases

#### Test Case 1:

```
Tree:
          1
         / \
        3   2
       /     \
      5       9
     /         \
    6           7

Output: 8
Explanation: Width of last level is from node 6 to node 7 (including nulls) = 8
```

---

#### Test Case 2:

```
Tree:
       1
      / \
     3   2
    /     \
   5       9

Output: 4
```

---

#### Test Case 3:

```
Tree:
    1
   /
  2
 /
4

Output: 1
```

---

### 💡 Intuition

This is a **level-order traversal (BFS)** problem with **indexed positions**:

- Assign **position indices** to nodes like in a complete binary tree:

  - root = 0
  - left = 2 \* index
  - right = 2 \* index + 1

- Track the **first and last indices** at each level
- Width of the level = `last_index - first_index + 1`

---

### 🧪 Dry Run

```
Tree:
        1
       / \
      3   2
     /     \
    5       9
   /         \
  6           7

Indexing:
- Level 0: [1(0)]
- Level 1: [3(0), 2(1)]
- Level 2: [5(0), null, null, 9(3)]
- Level 3: [6(0), null, ..., 7(7)]

Width at level 3: 7 - 0 + 1 = 8 ✅
```

---

### ✅ JavaScript Code

```javascript
function widthOfBinaryTree(root) {
  if (!root) return 0;

  let maxWidth = 0;
  const queue = [{ node: root, index: 0 }];

  while (queue.length > 0) {
    const levelSize = queue.length;
    const firstIndex = queue[0].index;
    let lastIndex = firstIndex;

    for (let i = 0; i < levelSize; i++) {
      const { node, index } = queue.shift();
      const currIndex = index - firstIndex; // normalize to prevent overflow
      lastIndex = currIndex;

      if (node.left) queue.push({ node: node.left, index: 2 * currIndex });
      if (node.right)
        queue.push({ node: node.right, index: 2 * currIndex + 1 });
    }

    maxWidth = Math.max(maxWidth, lastIndex + 1);
  }

  return maxWidth;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(n)  |
| Space  | O(n)  |

> `n` = number of nodes
> Queue stores nodes level by level with index tracking

---

### 📌 Summary

| Step              | Explanation                          |
| ----------------- | ------------------------------------ |
| Index Assignment  | Like complete binary tree (2i, 2i+1) |
| Width Calculation | `last - first + 1` per level         |
| Max Width         | Track max across all levels          |

---

## ✅ **4. Check for Children Sum Property**

### 🧩 Problem Statement

Given the `root` of a binary tree, check whether it satisfies the **Children Sum Property**.

> A Binary Tree satisfies the **Children Sum Property** if, for every node,
> `node.val == (left child's value) + (right child's value)`
> (if children exist; else they are considered as 0).

---

### 🧪 Test Cases

#### Test Case 1:

```
Tree:
      10
     /  \
    8    2
        /
       2

Output: true
```

#### Test Case 2:

```
Tree:
      10
     /  \
    8    2
        /
       1

Output: false
```

#### Test Case 3:

```
Tree:
     5

Output: true
(Leaf node always satisfies the property)
```

#### Test Case 4:

```
Tree: null

Output: true
(Empty tree is considered valid)
```

---

### 💡 Intuition

We perform a **postorder DFS traversal** and verify:

- If current node is `null` → return true
- If it's a **leaf node** → return true
- Else, check:

  - left + right child values == current node’s value
  - recursively ensure left and right subtrees satisfy the property

---

### 🧪 Dry Run

```
Tree:
      10
     /  \
    8    2
        /
       2

- Node 2 has left child 2 → 2 == 2 ✅
- Node 10: 8 (left) + 2 (right) = 10 ✅
→ All nodes satisfy condition ✅
```

---

### ✅ JavaScript Code

```javascript
function isChildrenSum(node) {
  if (!node || (!node.left && !node.right)) return true;

  let leftVal = node.left ? node.left.val : 0;
  let rightVal = node.right ? node.right.val : 0;

  const cond = node.val === leftVal + rightVal;
  return cond && isChildrenSum(node.left) && isChildrenSum(node.right);
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(n)  |
| Space  | O(h)  |

> `n` = number of nodes
> `h` = height of tree (recursion stack)

---

### 📌 Summary

| Condition    | Meaning                                  |
| ------------ | ---------------------------------------- |
| Leaf Node    | Always satisfies property                |
| Null Node    | Considered valid                         |
| General Node | Must satisfy: `node.val == left + right` |

---

## ✅ **5. Print All Nodes at Distance K in a Binary Tree**

### 🧩 Problem Statement

Given the `root` of a binary tree, a `target` node, and an integer `K`, return **all nodes that are K distance away from the target node**.

> Nodes can be **in the subtree** of the target or **upwards toward ancestors**.

---

### 🧪 Test Cases

#### Test Case 1:

```
Tree:
        3
       / \
      5   1
     / \ / \
    6  2 0  8
      / \
     7   4

Target = 5, K = 2
Output: [7, 4, 1]
```

#### Test Case 2:

```
Tree:
      1
     / \
    2   3

Target = 2, K = 1
Output: [1]
```

#### Test Case 3:

```
Tree:
     1
Target = 1, K = 0
Output: [1]
```

---

### 💡 Intuition

#### Step 1: Build a **parent map**

- Since nodes don’t have parent pointers, traverse once to store each node's **parent reference**

#### Step 2: Perform **BFS** starting from the `target` node

- Treat the tree like an **undirected graph** using left, right, and parent connections
- Track visited nodes to avoid cycles
- When distance = `K`, collect nodes in the queue

---

### 🧪 Dry Run

Target = 5, K = 2
From node 5 → distance 1: \[6, 2]
→ distance 2: \[7, 4] (children of 2), \[1] (parent of 5)
✅ Result = \[7, 4, 1]

---

### ✅ JavaScript Code

```javascript
function distanceK(root, target, k) {
  const parentMap = new Map();

  // Step 1: Build parent references
  function buildParent(node, parent = null) {
    if (!node) return;
    if (parent) parentMap.set(node, parent);
    buildParent(node.left, node);
    buildParent(node.right, node);
  }

  buildParent(root);

  // Step 2: BFS from target
  const visited = new Set();
  const queue = [{ node: target, dist: 0 }];
  const result = [];

  while (queue.length) {
    const { node, dist } = queue.shift();
    if (!node || visited.has(node)) continue;
    visited.add(node);

    if (dist === k) {
      result.push(node.val);
      continue;
    }

    queue.push({ node: node.left, dist: dist + 1 });
    queue.push({ node: node.right, dist: dist + 1 });
    if (parentMap.has(node)) {
      queue.push({ node: parentMap.get(node), dist: dist + 1 });
    }
  }

  return result;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(n)  |
| Space  | O(n)  |

> `n` = number of nodes

- Parent map + BFS traversal + visited set

---

### 📌 Summary

| Step            | Explanation                             |
| --------------- | --------------------------------------- |
| Parent Mapping  | Allows moving upward in the tree        |
| BFS from target | Explore all directions from target node |
| Track visited   | Prevent revisiting same nodes           |
| Capture at K    | Collect when distance equals K          |

---

## ✅ **6. Minimum Time to Burn the Binary Tree from a Node**

### 🧩 Problem Statement

You are given the `root` of a binary tree and a `target` node.
A fire starts from the `target` node and spreads to **adjacent nodes** (left, right, and parent) in **1 second**.

Return the **minimum time in seconds** to **burn the entire binary tree**.

---

### 🧪 Test Cases

#### Test Case 1:

```
Tree:
         1
        / \
       2   3
      /
     4
    /
   5

Target = 5
Output: 4
```

#### Test Case 2:

```
Tree:
        1
       / \
      2   3
     / \
    4   5

Target = 2
Output: 2
```

---

### 💡 Intuition

This is an extension of the **“Nodes at Distance K”** problem, but we must calculate how long it takes to **burn all nodes**.

#### Key Steps:

1. **Create a parent map** (to move upward)
2. **BFS from the target node** in all directions (left, right, parent)
3. At each second, fire spreads to adjacent unvisited nodes
4. Count the **time (levels)** required to visit all nodes

---

### 🧪 Dry Run

Target = 2

```
Time 0: [2]
Time 1: [1, 4, 5]
Time 2: [3]
All nodes visited → Output: 2
```

---

### ✅ JavaScript Code

```javascript
function minTimeToBurnTree(root, targetVal) {
  const parentMap = new Map();
  let targetNode = null;

  // Step 1: Build parent references and find target node
  function buildParentMap(node, parent = null) {
    if (!node) return;
    if (node.val === targetVal) targetNode = node;
    if (parent) parentMap.set(node, parent);
    buildParentMap(node.left, node);
    buildParentMap(node.right, node);
  }

  buildParentMap(root);
  if (!targetNode) return 0;

  // Step 2: BFS to simulate fire spreading
  const visited = new Set();
  const queue = [targetNode];
  visited.add(targetNode);
  let time = 0;

  while (queue.length > 0) {
    let size = queue.length;
    let fireSpread = false;

    for (let i = 0; i < size; i++) {
      const curr = queue.shift();

      const neighbors = [curr.left, curr.right, parentMap.get(curr)];

      for (const neighbor of neighbors) {
        if (neighbor && !visited.has(neighbor)) {
          queue.push(neighbor);
          visited.add(neighbor);
          fireSpread = true;
        }
      }
    }

    if (fireSpread) time++;
  }

  return time;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(n)  |
| Space  | O(n)  |

> `n` = number of nodes
> Used for parent map, visited set, and queue

---

### 📌 Summary

| Step           | Description                                 |
| -------------- | ------------------------------------------- |
| Parent Mapping | Enables movement toward the parent node     |
| BFS Simulation | Fire spreads level by level (1 second each) |
| Track Visited  | Prevents infinite loops                     |
| Time Counter   | Increments when fire spreads                |

---

## ✅ **7. Count Total Nodes in a Complete Binary Tree**

### 🧩 Problem Statement

Given the `root` of a **complete binary tree**, return the **total number of nodes** in the tree.

> A **complete binary tree** is a binary tree in which:
>
> - All levels are completely filled **except possibly the last**, and
> - All nodes are as **left as possible** on the last level.

---

### 🧪 Test Cases

#### Test Case 1:

```
Tree:
        1
       / \
      2   3
     / \  /
    4  5 6

Output: 6
```

#### Test Case 2:

```
Tree:
    1
   / \
  2   3

Output: 3
```

#### Test Case 3:

```
Tree:
    null

Output: 0
```

---

### 💡 Intuition

We can count nodes in `O(log² n)` instead of `O(n)` by leveraging the **complete tree property**.

#### Key Observations:

- In a **perfect** binary tree: total nodes = `2^height - 1`
- At each node:

  - If left height == right height → tree is perfect → use formula
  - Else → recurse left and right subtrees

---

### 🧪 Dry Run

```
Tree:
        1
       / \
      2   3
     / \  /
    4  5 6

- At root:
  - Left height = 3 (1 → 2 → 4)
  - Right height = 2 (1 → 3 → 6)
  → not perfect → recurse
```

---

### ✅ JavaScript Code

```javascript
function countNodes(root) {
  if (!root) return 0;

  function getHeight(node, left = true) {
    let height = 0;
    while (node) {
      height++;
      node = left ? node.left : node.right;
    }
    return height;
  }

  const lh = getHeight(root, true);
  const rh = getHeight(root, false);

  if (lh === rh) {
    return (1 << lh) - 1; // 2^h - 1
  }

  return 1 + countNodes(root.left) + countNodes(root.right);
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Value            |
| ------ | ---------------- |
| Time   | O(log² n)        |
| Space  | O(log n) (stack) |

> `n` = number of nodes
> Each level takes O(log n) height calculation

---

### 📌 Summary

| Technique        | Logic                            |
| ---------------- | -------------------------------- |
| Use Tree Height  | For leftmost and rightmost paths |
| Check if Perfect | If left height == right height   |
| Perfect Subtree  | Use formula `2^h - 1`            |
| Else Recurse     | On left and right children       |

---

## ✅ **8. Requirements to Construct a Unique Binary Tree**

### 📘 Problem Context

Given various combinations of tree traversal orders (like Inorder, Preorder, Postorder), can we **uniquely construct** a binary tree?

> Not all traversal pairs can uniquely identify a binary tree. Some combinations **do**, while others **don’t** unless additional information is provided.

---

### 🧠 Core Concept

To **uniquely construct a binary tree**, the combination must allow:

- Identification of the **root**, and
- Accurate **partitioning** of left and right subtrees

---

### ✅ Traversal Combinations That Can Build a Unique Binary Tree

| Traversal Pair           | Uniquely Identifies Tree?  | Explanation                                                 |
| ------------------------ | -------------------------- | ----------------------------------------------------------- |
| **Inorder + Preorder**   | ✅ Yes                     | Preorder gives root, Inorder splits left/right subtrees     |
| **Inorder + Postorder**  | ✅ Yes                     | Postorder gives root, Inorder splits left/right subtrees    |
| **Preorder + Postorder** | ❌ No (except full binary) | Cannot determine tree structure uniquely unless full binary |

---

### ✅ Why "Inorder + Preorder" Works

- **Preorder**: First node = root
- **Inorder**: Root divides tree into left & right subtrees
  → Use this recursively to build the tree

> Example:
> Preorder: `A B D E C F`
> Inorder: `D B E A F C`

Build process:

1. Root = A
2. A splits Inorder into left = `D B E`, right = `F C`
3. Recur on left with Preorder `B D E`, right with `C F`

---

### ❌ Why "Preorder + Postorder" Alone Fails

- **Both** provide root positions but **not enough** to separate left and right subtrees.
- For example, multiple trees can give same Pre and Post traversal.

**Example:**

```
Tree 1:     Tree 2:
   1            1
  /              \
 2                2
```

Both have:

- Preorder: \[1, 2]
- Postorder: \[2, 1]

So, not unique.

---

### ✅ Special Case: Full Binary Tree

If the binary tree is **full** (each node has 0 or 2 children),
then **Preorder + Postorder** can uniquely determine the tree.

---

### 📌 Summary Table

| Traversals           | Unique Tree? | Note                                 |
| -------------------- | ------------ | ------------------------------------ |
| Inorder + Preorder   | ✅ Yes       | Most commonly used                   |
| Inorder + Postorder  | ✅ Yes       | Also works, root from postorder      |
| Preorder + Postorder | ❌ No        | Needs tree to be full for uniqueness |
| Only Inorder         | ❌ No        | Many trees possible                  |
| Only Pre/Postorder   | ❌ No        | Insufficient alone                   |

---

## ✅ **9. Construct Binary Tree from Inorder and Preorder Traversal**

### 🧩 Problem Statement

Given two arrays:

- `preorder[]` → preorder traversal of the tree
- `inorder[]` → inorder traversal of the tree

Return the **root node** of the **binary tree** that they represent.

---

### 🧪 Test Cases

#### Test Case 1:

```
Preorder: [3, 9, 20, 15, 7]
Inorder:  [9, 3, 15, 20, 7]

Output Tree:
      3
     / \
    9  20
       / \
      15  7
```

#### Test Case 2:

```
Preorder: [1, 2, 4, 5, 3]
Inorder:  [4, 2, 5, 1, 3]

Output Tree:
        1
       / \
      2   3
     / \
    4   5
```

---

### 💡 Intuition

- The **first element** of preorder is always the **root**.
- The **position of root** in the inorder array tells us the **left and right subtree ranges**.
- Use **recursive construction** and manage preorder index globally.

---

### 🧪 Dry Run

Given:

```js
preorder = [1, 2, 4, 5, 3];
inorder = [4, 2, 5, 1, 3];
```

- root = 1
- inorder: 1 splits into left = \[4,2,5], right = \[3]
- Recurse on preorder \[2,4,5] and \[3]
- Build left and right recursively

---

### ✅ JavaScript Code

```javascript
function buildTree(preorder, inorder) {
  let preIndex = 0;
  const inorderMap = new Map();
  for (let i = 0; i < inorder.length; i++) {
    inorderMap.set(inorder[i], i);
  }

  function helper(left, right) {
    if (left > right) return null;

    const rootVal = preorder[preIndex++];
    const root = new TreeNode(rootVal);

    const inIndex = inorderMap.get(rootVal);

    root.left = helper(left, inIndex - 1);
    root.right = helper(inIndex + 1, right);

    return root;
  }

  return helper(0, inorder.length - 1);
}
```

> Assumes `TreeNode` is a class with `val`, `left`, and `right` fields.

---

### ⏱️ Time & Space Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(n)  |
| Space  | O(n)  |

> `n` = number of nodes

- Time: Each node visited once
- Space: `O(n)` for map + recursion stack

---

### 📌 Summary

| Step               | Description                    |
| ------------------ | ------------------------------ |
| Preorder Root      | First element is always root   |
| Inorder Split      | Splits left and right subtrees |
| Use Map            | To speed up lookup in inorder  |
| Recur Left → Right | In preorder order              |

---

## ✅ **10. Construct Binary Tree from Inorder and Postorder Traversal**

### 🧩 Problem Statement

Given two arrays:

- `inorder[]` → inorder traversal of a binary tree
- `postorder[]` → postorder traversal of the same binary tree

Construct and return the **root of the binary tree**.

---

### 🧪 Test Cases

#### Test Case 1:

```
Inorder:    [9, 3, 15, 20, 7]
Postorder:  [9, 15, 7, 20, 3]

Output Tree:
        3
       / \
      9  20
         / \
       15   7
```

#### Test Case 2:

```
Inorder:    [4, 2, 5, 1, 3]
Postorder:  [4, 5, 2, 3, 1]

Output Tree:
        1
       / \
      2   3
     / \
    4   5
```

---

### 💡 Intuition

- In **postorder**, the **last element** is always the root.
- Using the **position of root in inorder**, we can divide into left and right subtrees.
- Traverse **postorder in reverse** and build the **tree bottom-up** using recursion.

---

### 🧪 Dry Run

```js
inorder:   [4, 2, 5, 1, 3]
postorder: [4, 5, 2, 3, 1]

- Root = 1 (last of postorder)
- In inorder, 1 splits left: [4, 2, 5], right: [3]
- Recurse on [4, 5, 2] for left, [3] for right
```

---

### ✅ JavaScript Code

```javascript
function buildTree(inorder, postorder) {
  let postIndex = postorder.length - 1;
  const inorderMap = new Map();

  for (let i = 0; i < inorder.length; i++) {
    inorderMap.set(inorder[i], i);
  }

  function helper(left, right) {
    if (left > right) return null;

    const rootVal = postorder[postIndex--];
    const root = new TreeNode(rootVal);

    const inIndex = inorderMap.get(rootVal);

    // Important: Build right first (postorder is L -> R -> Root)
    root.right = helper(inIndex + 1, right);
    root.left = helper(left, inIndex - 1);

    return root;
  }

  return helper(0, inorder.length - 1);
}
```

> `TreeNode` is a class with properties `val`, `left`, and `right`.

---

### ⏱️ Time & Space Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(n)  |
| Space  | O(n)  |

> `n` = number of nodes

- Time: Each node is visited once
- Space: O(n) for map + recursion stack

---

### 📌 Summary

| Step                | Explanation                                 |
| ------------------- | ------------------------------------------- |
| Postorder Root      | Last element is root                        |
| Inorder Split       | Use root index to split left/right subtrees |
| Traverse in Reverse | Right → Left → Root in recursive order      |
| Use Map             | For O(1) lookups of inorder positions       |

---

## ✅ **11. Serialize and Deserialize a Binary Tree**

### 🧩 Problem Statement

You are given the `root` of a binary tree.

- **Serialization** is the process of converting the tree into a string.
- **Deserialization** is the reverse process — converting the string back into the original binary tree.

Return the tree after serializing and deserializing — i.e., `deserialize(serialize(root))` should return the same tree.

---

### 🧪 Test Cases

#### Test Case 1:

```
Input Tree:
       1
      / \
     2   3
        / \
       4   5

Serialized: "1,2,null,null,3,4,null,null,5,null,null"
```

#### Test Case 2:

```
Input Tree:
    null

Serialized: "null"
```

---

### 💡 Intuition

Use **Preorder traversal** (Root → Left → Right) to serialize the tree.

- For serialization:

  - If node is null → record `"null"`
  - Else → record node's value, and recur left and right

- For deserialization:

  - Read values from the serialized string
  - Use recursion to rebuild the tree
  - `"null"` represents a leaf (no child)

---

### 🧪 Dry Run

#### Tree:

```
     1
    / \
   2   3

Preorder: [1, 2, null, null, 3, null, null]

Serialized: "1,2,null,null,3,null,null"
```

During deserialization:

- First value = 1 → root
- Next = 2 → left child
- Next = null → left of 2 is null
- Next = null → right of 2 is null
- Next = 3 → right of 1
- Then nulls for 3’s children

---

### ✅ JavaScript Code

```javascript
class Codec {
  // Serializes a tree to a single string.
  serialize(root) {
    function dfs(node) {
      if (!node) return "null,";
      return `${node.val},` + dfs(node.left) + dfs(node.right);
    }
    return dfs(root);
  }

  // Deserializes your encoded data to tree.
  deserialize(data) {
    const nodes = data.split(",");
    let index = 0;

    function build() {
      if (nodes[index] === "null") {
        index++;
        return null;
      }
      const node = new TreeNode(Number(nodes[index++]));
      node.left = build();
      node.right = build();
      return node;
    }

    return build();
  }
}
```

> Assumes `TreeNode` is a class with properties `val`, `left`, and `right`.

---

### ⏱️ Time & Space Complexity

| Operation   | Time | Space |
| ----------- | ---- | ----- |
| Serialize   | O(n) | O(n)  |
| Deserialize | O(n) | O(n)  |

> `n` = number of nodes
> Traversal and reconstruction each touch every node once.

---

### 📌 Summary

| Step            | Explanation                              |
| --------------- | ---------------------------------------- |
| Preorder        | Used to serialize tree structure         |
| `"null"`        | Marks absent children                    |
| Deserialization | Rebuild tree recursively from string     |
| Output String   | Can be stored, sent, or saved externally |

---

## ✅ **12. Morris Preorder Traversal of a Binary Tree**

### 🧩 Problem Statement

Perform **Preorder Traversal** (Root → Left → Right) of a binary tree using **Morris Traversal**, i.e., without using recursion or a stack and in **O(1)** space.

---

### 🧪 Test Cases

#### Test Case 1:

```
Input Tree:
       1
      / \
     2   3
    / \
   4   5

Preorder Output: [1, 2, 4, 5, 3]
```

#### Test Case 2:

```
Input Tree:
    1
     \
      2
       \
        3

Preorder Output: [1, 2, 3]
```

---

### 💡 Intuition

In Morris Traversal, we avoid recursion/stack by modifying the tree **temporarily**:

- For each node:

  - If `left == null`, visit node and move to `right`
  - Else, find the **inorder predecessor** (rightmost node of left subtree)

    - If its `right == null`, create a **thread** to current node (visit current for preorder), move to `left`
    - If its `right == current`, remove the thread, and move to `right`

> ✅ Morris Preorder: **Visit when thread is created** (before going to left)

---

### 🧪 Dry Run

Tree:

```
       1
      / \
     2   3
    /
   4

1 → 2 (thread created from 4 → 1) → 4 → (thread removed) → 3

Output: [1, 2, 4, 3]
```

---

### ✅ JavaScript Code

```javascript
function morrisPreorderTraversal(root) {
  const result = [];
  let current = root;

  while (current) {
    if (!current.left) {
      result.push(current.val);
      current = current.right;
    } else {
      let predecessor = current.left;
      while (predecessor.right && predecessor.right !== current) {
        predecessor = predecessor.right;
      }

      if (!predecessor.right) {
        result.push(current.val); // visit on first encounter
        predecessor.right = current; // make thread
        current = current.left;
      } else {
        predecessor.right = null; // remove thread
        current = current.right;
      }
    }
  }

  return result;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(n)  |
| Space  | O(1)  |

> `n` = number of nodes

- Threading ensures each edge is visited max twice
- No recursion or stack

---

### 📌 Summary

| Step                 | Explanation                                    |
| -------------------- | ---------------------------------------------- |
| No Stack / Recursion | Uses tree threading instead                    |
| Threading            | Temporarily sets right pointer of predecessor  |
| Preorder Visit       | Occurs **before** going to left                |
| Tree is Restored     | Original structure is restored after traversal |

---

## ✅ **13. Morris Inorder Traversal of a Binary Tree**

### 🧩 Problem Statement

Perform **Inorder Traversal** (Left → Root → Right) of a binary tree using **Morris Traversal**, i.e., in **O(1)** space without recursion or a stack.

---

### 🧪 Test Cases

#### Test Case 1:

```
Input Tree:
       1
      / \
     2   3
    / \
   4   5

Inorder Output: [4, 2, 5, 1, 3]
```

#### Test Case 2:

```
Input Tree:
    1
     \
      2
       \
        3

Inorder Output: [1, 2, 3]
```

---

### 💡 Intuition

Morris traversal avoids recursion/stack by using **temporary threads** to the **inorder predecessor** (rightmost node in left subtree).

#### For Each Node:

1. If `left == null`, **visit** node and move to `right`
2. Else:

   - Find the **inorder predecessor** of the current node
   - If `predecessor.right == null`:
     ➤ Set `predecessor.right = current` (thread)
     ➤ Move to `current.left`
   - Else:
     ➤ Remove the thread (`predecessor.right = null`)
     ➤ **Visit** current node
     ➤ Move to `current.right`

> In **Morris Inorder**, you **visit on returning** from the left subtree (after thread removal).

---

### 🧪 Dry Run

Tree:

```
       1
      / \
     2   3
    / \
   4   5

Steps:
- Start at 1 → go to 2 → go to 4 (no left) → visit 4
- Back to 2 (via thread) → visit 2 → go to 5 → visit 5
- Back to 1 → visit 1 → go to 3 → visit 3

✅ Output: [4, 2, 5, 1, 3]
```

---

### ✅ JavaScript Code

```javascript
function morrisInorderTraversal(root) {
  const result = [];
  let current = root;

  while (current) {
    if (!current.left) {
      result.push(current.val);
      current = current.right;
    } else {
      let predecessor = current.left;
      while (predecessor.right && predecessor.right !== current) {
        predecessor = predecessor.right;
      }

      if (!predecessor.right) {
        // Create thread
        predecessor.right = current;
        current = current.left;
      } else {
        // Thread already exists → visit and remove thread
        predecessor.right = null;
        result.push(current.val);
        current = current.right;
      }
    }
  }

  return result;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(n)  |
| Space  | O(1)  |

> `n` = number of nodes
> Each node is visited at most twice (enter + thread back)

---

### 📌 Summary

| Step                  | Explanation                                       |
| --------------------- | ------------------------------------------------- |
| No recursion or stack | Space optimized using tree threading              |
| Threading             | Point right of predecessor to current temporarily |
| Visit Order           | Visit only after returning from left subtree      |
| Tree Restoration      | Original structure is restored after traversal    |

---

## ✅ **14. Flatten Binary Tree to Linked List**

### 🧩 Problem Statement

Given the `root` of a **binary tree**, flatten the tree in-place into a **linked list**.

- The linked list should use the **right** pointers only.
- The order must follow **preorder traversal**: Root → Left → Right.

🔁 All left pointers must be set to `null`.

---

### 🧪 Test Cases

#### Test Case 1:

```
Input Tree:
        1
       / \
      2   5
     / \   \
    3   4   6

Output Linked List:
1 → 2 → 3 → 4 → 5 → 6
```

#### Test Case 2:

```
Input Tree:
    1
   /
  2

Output: 1 → 2
```

---

### 💡 Intuition

We need to **restructure the tree** so that:

- Every node's `left` is null
- Every node's `right` points to the next node in **preorder traversal**

#### Key Idea (Optimal Approach - O(1) Space, Morris-like):

- For each node:

  - If left subtree exists:

    - Find **rightmost** node in left subtree (predecessor)
    - Point its `right` to the current node’s original `right`
    - Move left subtree to right and nullify left

- Move to `right` (which now includes both subtrees)

---

### 🧪 Dry Run

Tree:

```
      1
     / \
    2   5
   / \
  3   4

Step-by-step restructure:
- Node 1 → move 2 to right, attach 5 to 4 (rightmost of left)
- Node 2 → move 3 to right, attach 4 to 3
- Node 3 → nothing
→ Final: 1→2→3→4→5
```

---

### ✅ JavaScript Code (In-Place, O(1) Space)

```javascript
function flatten(root) {
  let curr = root;

  while (curr) {
    if (curr.left) {
      let predecessor = curr.left;
      while (predecessor.right) {
        predecessor = predecessor.right;
      }

      predecessor.right = curr.right;
      curr.right = curr.left;
      curr.left = null;
    }

    curr = curr.right;
  }
}
```

---

### ✅ Recursive Approach (Elegant, uses O(h) space)

```javascript
function flatten(root) {
  let prev = null;

  function dfs(node) {
    if (!node) return;
    dfs(node.right);
    dfs(node.left);

    node.right = prev;
    node.left = null;
    prev = node;
  }

  dfs(root);
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Morris (In-Place) | Recursive        |
| ------ | ----------------- | ---------------- |
| Time   | O(n)              | O(n)             |
| Space  | O(1)              | O(h) (recursion) |

> `n` = total nodes, `h` = height of tree

---

### 📌 Summary

| Step                      | Description                                  |
| ------------------------- | -------------------------------------------- |
| Preorder Order            | Required flattening order                    |
| Rightmost in Left Subtree | Used to reconnect the original right subtree |
| In-Place                  | No need for extra data structures            |
| Final Tree                | Becomes right-skewed (like linked list)      |

---
