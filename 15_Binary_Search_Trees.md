# 🌳 Binary Search Tree (BST) - Beginner to Advanced

## **What is a Binary Search Tree?**

A **Binary Search Tree (BST)** is a special type of binary tree where:

- The **left subtree** of a node contains **only nodes with keys less than the node’s key**.
- The **right subtree** of a node contains **only nodes with keys greater than the node’s key**.
- Both the left and right subtrees must also be **binary search trees**.

### 🔷 Properties:

- Binary tree structure.
- Unique keys (no duplicates, usually).
- Average time complexity for search, insert, delete: **O(log n)** (for balanced BSTs).

---

## 🔧 **Basic Operations in BST**

### ➕ Insert

- Recursively go left or right based on value.

```javascript
class Node {
  constructor(val) {
    this.val = val;
    this.left = null;
    this.right = null;
  }
}

function insert(root, key) {
  if (root == null) return new Node(key);
  if (key < root.val) root.left = insert(root.left, key);
  else if (key > root.val) root.right = insert(root.right, key);
  return root;
}
```

---

### 🔍 Search

- Works like binary search.

```javascript
function search(root, key) {
  if (!root || root.val === key) return root;
  if (key < root.val) return search(root.left, key);
  return search(root.right, key);
}
```

---

### ❌ Delete

3 cases:

1. Node has no child → just remove.
2. Node has one child → replace with child.
3. Node has two children → replace with inorder successor or predecessor.

```javascript
function minValue(node) {
  let current = node;
  while (current.left != null) current = current.left;
  return current;
}

function deleteNode(root, key) {
  if (!root) return null;
  if (key < root.val) root.left = deleteNode(root.left, key);
  else if (key > root.val) root.right = deleteNode(root.right, key);
  else {
    if (!root.left) return root.right;
    if (!root.right) return root.left;

    let temp = minValue(root.right);
    root.val = temp.val;
    root.right = deleteNode(root.right, temp.val);
  }
  return root;
}
```

---

## 📈 **Time Complexity**

| Operation | Average Case | Worst Case (Skewed Tree) |
| --------- | ------------ | ------------------------ |
| Search    | O(log n)     | O(n)                     |
| Insert    | O(log n)     | O(n)                     |
| Delete    | O(log n)     | O(n)                     |

> For **balanced BSTs (like AVL or Red-Black Trees)**, the worst case is also O(log n).

---

## ⚠️ BST vs Balanced BST (AVL/Red-Black Tree)

| Feature        | BST           | AVL Tree / Red-Black Tree         |
| -------------- | ------------- | --------------------------------- |
| Balanced       | No            | Yes                               |
| Search (Worst) | O(n)          | O(log n)                          |
| Insert/Delete  | Faster        | Slightly Slower (due to rotation) |
| Use case       | Simple, quick | Large datasets, DB engines        |

---

# **Practice Problems**

## 🔢 **1. Ceil in a Binary Search Tree**

### 📘 Problem Statement

Given a **Binary Search Tree (BST)** and a target value `x`, find the **ceil of x** in the BST.

The **ceil of x** in BST is the **smallest node value in BST that is greater than or equal to x**.
If no such node exists, return `-1`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

Input:

```
       8
      / \
     4   12
    / \   / \
   2   6 10 14
x = 5
```

Output: `6`

#### ✅ Test Case 2:

Input:

```
       8
      / \
     4   12
    / \   / \
   2   6 10 14
x = 1
```

Output: `2`

#### ✅ Test Case 3:

Input:

```
       8
      / \
     4   12
    / \   / \
   2   6 10 14
x = 15
```

Output: `-1`

#### ✅ Test Case 4:

Input:

```
       8
      / \
     4   12
    / \   / \
   2   6 10 14
x = 8
```

Output: `8`

---

### 💡 Intuition

In a BST:

- Left subtree contains smaller values,
- Right subtree contains larger values.

To find the **ceil of `x`**, we move through the tree:

- If current node value is **equal to `x`**, it’s the ceil.
- If current node value is **less than `x`**, ceil must be on the **right**.
- If current node value is **greater than `x`**, it **may be the ceil**, but we continue to look in the **left** subtree to find a smaller ceil.

---

### 🔍 Dry Run

BST:

```
       8
      / \
     4   12
    / \   / \
   2   6 10 14
```

x = 5
Start at root = 8
→ 8 > 5 ⇒ possible ceil = 8, move left
→ 4 < 5 ⇒ move right
→ 6 > 5 ⇒ possible ceil = 6
No more children → return **6**

---

### ✅ Optimized Solution (BST Property Based)

```javascript
class Node {
  constructor(val) {
    this.val = val;
    this.left = null;
    this.right = null;
  }
}

function findCeil(root, x) {
  let ceil = -1;
  while (root !== null) {
    if (root.val === x) return root.val;
    if (root.val < x) {
      root = root.right;
    } else {
      ceil = root.val;
      root = root.left;
    }
  }
  return ceil;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity:** `O(H)` where `H` is the height of the tree (O(log N) for balanced BST, O(N) for skewed)
- **Space Complexity:** `O(1)` (Iterative), `O(H)` if using recursion

---

## 🔢 **2. Floor in a Binary Search Tree**

### 📘 Problem Statement

Given a **Binary Search Tree (BST)** and an integer `x`, find the **floor of x** in the BST.

The **floor of x** in BST is the **greatest value in BST that is less than or equal to x**.
If no such value exists, return `-1`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

Input:

```
       8
      / \
     4   12
    / \   / \
   2   6 10 14
x = 5
```

Output: `4`

#### ✅ Test Case 2:

Input:

```
       8
      / \
     4   12
    / \   / \
   2   6 10 14
x = 13
```

Output: `12`

#### ✅ Test Case 3:

Input:

```
       8
      / \
     4   12
    / \   / \
   2   6 10 14
x = 1
```

Output: `-1`

#### ✅ Test Case 4:

Input:

```
       8
      / \
     4   12
    / \   / \
   2   6 10 14
x = 10
```

Output: `10`

---

### 💡 Intuition

In a BST:

- Values in the left subtree are smaller,
- Values in the right subtree are larger.

To find the **floor of `x`**:

- If current node value is **equal to `x`**, that’s the floor.
- If current node value is **greater than `x`**, go **left** to find smaller candidates.
- If current node value is **less than `x`**, it's a **candidate for floor**, but check **right** subtree for closer/larger value still ≤ `x`.

---

### 🔍 Dry Run

BST:

```
       8
      / \
     4   12
    / \   / \
   2   6 10 14
```

x = 5
Start at root = 8
→ 8 > 5 ⇒ move left
→ 4 < 5 ⇒ possible floor = 4, move right
→ 6 > 5 ⇒ move left (no left child)
Return **4**

---

### ✅ Optimized Solution (BST Property Based)

```javascript
class Node {
  constructor(val) {
    this.val = val;
    this.left = null;
    this.right = null;
  }
}

function findFloor(root, x) {
  let floor = -1;
  while (root !== null) {
    if (root.val === x) return root.val;
    if (root.val > x) {
      root = root.left;
    } else {
      floor = root.val;
      root = root.right;
    }
  }
  return floor;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity:** `O(H)` where `H` is height of the tree
- **Space Complexity:** `O(1)` if iterative, `O(H)` if recursive

---

## 🔢 **3. Insert a Given Node in a Binary Search Tree**

### 📘 Problem Statement

You are given the **root** of a Binary Search Tree (BST) and an integer `key`.
Insert the `key` into the BST and return the root of the updated tree.
You must maintain the **BST properties**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

Input:

```
       8
      / \
     4   12
    / \   / \
   2   6 10 14
key = 5
```

Output: Node `5` is inserted as the right child of node `4`

#### ✅ Test Case 2:

Input:

```
       5
      /
     3
key = 4
```

Output: Node `4` is inserted as the right child of node `3`

#### ✅ Test Case 3:

Input:

```
  null
key = 7
```

Output: New node with value `7` becomes the root

#### ✅ Test Case 4:

Input:

```
       10
         \
         20
key = 25
```

Output: Node `25` is inserted as the right child of node `20`

---

### 💡 Intuition

The insertion operation in a BST leverages the property:

- If `key < root.val`, go to **left**
- If `key > root.val`, go to **right**

We keep moving until we find a `null` spot where the new node can be placed.

---

### 🔍 Dry Run

Example BST:

```
       8
      / \
     4   12
    / \   / \
   2   6 10 14
```

Insert: `5`
→ Start at 8 → 5 < 8 → move left to 4
→ 5 > 4 → move right to 6
→ 5 < 6 → move left, which is `null` → insert node here

---

### ✅ Iterative Solution

```javascript
class Node {
  constructor(val) {
    this.val = val;
    this.left = null;
    this.right = null;
  }
}

function insertIntoBST(root, key) {
  const newNode = new Node(key);
  if (root === null) return newNode;

  let curr = root;
  while (true) {
    if (key < curr.val) {
      if (curr.left === null) {
        curr.left = newNode;
        break;
      }
      curr = curr.left;
    } else {
      if (curr.right === null) {
        curr.right = newNode;
        break;
      }
      curr = curr.right;
    }
  }
  return root;
}
```

---

### ✅ Recursive Solution

```javascript
function insertIntoBST(root, key) {
  if (root === null) return new Node(key);

  if (key < root.val) {
    root.left = insertIntoBST(root.left, key);
  } else {
    root.right = insertIntoBST(root.right, key);
  }

  return root;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity:** `O(H)` where `H` is the height of the tree

  - Balanced BST: `O(log N)`
  - Skewed BST: `O(N)`

- **Space Complexity:**

  - Recursive: `O(H)` (due to recursion stack)
  - Iterative: `O(1)`

---

## 🔢 **4. Delete a Node in a Binary Search Tree**

### 📘 Problem Statement

You are given the **root** of a Binary Search Tree (BST) and an integer `key`.
Your task is to **delete** the node with value `key` and return the new root.

The resulting tree must remain a valid **BST**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

Input:

```
       8
      / \
     4   12
    / \   / \
   2   6 10 14
key = 4
```

Output:
Node `4` is deleted. Node `6` (inorder successor) replaces it.

#### ✅ Test Case 2:

Input:

```
    5
   /
  3
key = 3
```

Output:
Node `3` is deleted → it's a leaf node, just removed.

#### ✅ Test Case 3:

Input:

```
    10
      \
      20
key = 10
```

Output:
Node `10` is deleted → replaced by `20`

#### ✅ Test Case 4:

Input:

```
    null
key = 5
```

Output:
Tree remains `null` → node not found.

---

### 💡 Intuition

In BST deletion, we have **3 scenarios** to handle:

1. **Node to delete has no children** (leaf): Simply remove it.
2. **Node has one child**: Replace the node with its child.
3. **Node has two children**:

   - Replace the node’s value with its **inorder successor** (minimum value in the right subtree).
   - Then, delete the inorder successor recursively.

---

### 🔍 Dry Run

Tree:

```
       8
      / \
     4   12
    / \   / \
   2   6 10 14
```

Delete `4`

- `4` has two children → find inorder successor = `6`
- Replace `4` with `6`
- Delete `6` (which is a leaf)

Result:

```
       8
      / \
     6   12
    /    / \
   2    10 14
```

---

### ✅ Optimized Recursive Solution (JavaScript)

```javascript
class Node {
  constructor(val) {
    this.val = val;
    this.left = null;
    this.right = null;
  }
}

function deleteNode(root, key) {
  if (!root) return null;

  if (key < root.val) {
    root.left = deleteNode(root.left, key);
  } else if (key > root.val) {
    root.right = deleteNode(root.right, key);
  } else {
    // Node found
    if (!root.left) return root.right;
    if (!root.right) return root.left;

    // Node with two children: get inorder successor
    let successor = getMin(root.right);
    root.val = successor.val;
    root.right = deleteNode(root.right, successor.val);
  }
  return root;
}

function getMin(node) {
  while (node.left) {
    node = node.left;
  }
  return node;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity:** `O(H)` where `H` is the height of the tree

  - Balanced BST: `O(log N)`
  - Skewed BST: `O(N)`

- **Space Complexity:**

  - Recursive: `O(H)` (stack space)

---

## 🔢 **5. K-th Smallest / Largest Element in a Binary Search Tree**

### 📘 Problem Statement

You are given the **root** of a Binary Search Tree (BST) and an integer `k`.

- Find the **k-th smallest** element in the BST.
- Similarly, find the **k-th largest** element in the BST.

✅ BST Property:

- Inorder traversal → sorted in **ascending** order
- Reverse Inorder → sorted in **descending** order

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```
       8
      / \
     4   12
    / \   / \
   2   6 10 14
```

- k = 3

  - K-th **Smallest** = `6`
  - K-th **Largest** = `10`

#### ✅ Test Case 2:

```
     5
    / \
   3   7
  /
 2
```

- k = 1

  - K-th **Smallest** = `2`
  - K-th **Largest** = `7`

#### ✅ Test Case 3:

```
     10
       \
        20
```

- k = 2

  - K-th **Smallest** = `20`
  - K-th **Largest** = `10`

---

### 💡 Intuition

#### For K-th Smallest:

- Perform **inorder traversal** (Left → Root → Right)
- Keep a counter, when it reaches `k`, return the node value

#### For K-th Largest:

- Perform **reverse inorder traversal** (Right → Root → Left)
- Keep a counter, when it reaches `k`, return the node value

---

### 🔍 Dry Run: K-th Smallest

Tree:

```
       8
      / \
     4   12
    / \   / \
   2   6 10 14
```

Inorder: \[2, 4, 6, 8, 10, 12, 14]
k = 3 → Output = `6`

---

### ✅ Code – JavaScript

#### 🔹 K-th Smallest Element

```javascript
function kthSmallest(root, k) {
  let count = 0;
  let result = -1;

  function inorder(node) {
    if (!node || count >= k) return;
    inorder(node.left);
    count++;
    if (count === k) {
      result = node.val;
      return;
    }
    inorder(node.right);
  }

  inorder(root);
  return result;
}
```

---

#### 🔹 K-th Largest Element

```javascript
function kthLargest(root, k) {
  let count = 0;
  let result = -1;

  function reverseInorder(node) {
    if (!node || count >= k) return;
    reverseInorder(node.right);
    count++;
    if (count === k) {
      result = node.val;
      return;
    }
    reverseInorder(node.left);
  }

  reverseInorder(root);
  return result;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity:** `O(H + k)`

  - Where H is height of tree (log N for balanced BST, N for skewed)

- **Space Complexity:** `O(H)` (recursion stack)

---

### 📊 Summary Table

| BST Traversal Type | Problem       | Order      | Strategy            |
| ------------------ | ------------- | ---------- | ------------------- |
| Inorder            | K-th Smallest | Ascending  | Left → Root → Right |
| Reverse Inorder    | K-th Largest  | Descending | Right → Root → Left |

---

## 🔢 **6. Check if a Tree is a Binary Search Tree (BST)**

### 📘 Problem Statement

Given the root of a binary tree, check whether it is a **Binary Search Tree (BST)**.

**A tree is a BST if for every node**:

- All values in the **left subtree** are **less** than the node’s value.
- All values in the **right subtree** are **greater** than the node’s value.
- And **both left and right subtrees** are also BSTs.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```
       8
      / \
     4   12
    / \   / \
   2   6 10 14
```

Output: ✅ BST

#### ✅ Test Case 2:

```
       10
      /  \
     5   20
        /
       9
```

Output: ❌ Not a BST (9 is in the right subtree of 10 but less than 10)

#### ✅ Test Case 3:

```
    1
     \
      2
       \
        3
```

Output: ✅ BST

#### ✅ Test Case 4:

```
    3
   / \
  2   5
     /
    1
```

Output: ❌ Not a BST (1 is on the right of 3 but less than 3)

---

### 💡 Intuition

We need to ensure that:

- Each node respects the **range constraint**:

  - Node value must lie in the range: `min < node.val < max`

### ✅ Key Insight:

- Start with full range: `(-∞, ∞)`
- For left child: new max = parent.val
- For right child: new min = parent.val

---

### 🔍 Dry Run

Example:

```
       10
      /  \
     5   15
        /
       6
```

- `10` is valid
- `5` is valid
- `15` is valid (should be > 10)
- `6` is invalid (it's in the right subtree of 10, but less than 10)

Result → ❌ Not a BST

---

### ✅ Optimized Recursive Solution (with min-max range)

```javascript
function isBST(root) {
  return validate(root, -Infinity, Infinity);
}

function validate(node, min, max) {
  if (!node) return true;
  if (node.val <= min || node.val >= max) return false;

  return (
    validate(node.left, min, node.val) && validate(node.right, node.val, max)
  );
}
```

---

##$ ✅ Inorder Traversal (Alternative Approach)

A BST’s **inorder traversal** yields a **strictly increasing** sequence.

```javascript
function isBSTInorder(root) {
  let prev = null;
  let isValid = true;

  function inorder(node) {
    if (!node || !isValid) return;
    inorder(node.left);
    if (prev !== null && node.val <= prev) {
      isValid = false;
      return;
    }
    prev = node.val;
    inorder(node.right);
  }

  inorder(root);
  return isValid;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity:** `O(N)` (visit each node once)
- **Space Complexity:**

  - Recursive: `O(H)` (call stack)
  - Iterative (with stack): `O(H)`
  - Morris Traversal (if used): `O(1)`

---

### 📊 Summary Table

| Approach           | Description                         | Valid BST |
| ------------------ | ----------------------------------- | --------- |
| Min-Max Recursion  | Use range constraints per node      | ✅        |
| Inorder Traversal  | Check for strictly increasing order | ✅        |
| Preorder/Postorder | ❌ Not reliable for checking BST    | ❌        |

---

## 🔢 **7. Lowest Common Ancestor (LCA) in a Binary Search Tree**

### 📘 Problem Statement

Given a **Binary Search Tree (BST)** and two nodes `p` and `q`, find their **Lowest Common Ancestor (LCA)**.

🔹 The **LCA of two nodes** is the **lowest node** in the BST that has both `p` and `q` as **descendants** (where we allow a node to be a descendant of itself).

✅ In BST, LCA is the **first node** where the two nodes split into **left and right**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```
       6
      / \
     2   8
    / \ / \
   0  4 7  9
     / \
    3   5
p = 2, q = 8
```

Output: `6`

#### ✅ Test Case 2:

Same tree
p = 2, q = 4
Output: `2` (node is ancestor of itself)

#### ✅ Test Case 3:

```
     5
    /
   3
p = 3, q = 5
```

Output: `5`

---

### 💡 Intuition

Leverage BST properties:

- If `p` and `q` are both **smaller** than current node → go **left**
- If `p` and `q` are both **greater** than current node → go **right**
- If one is on the **left** and one is on the **right**, or current node is `p` or `q` → current node is the **LCA**

---

### 🔍 Dry Run

Tree:

```
       6
      / \
     2   8
    / \ / \
   0  4 7  9
```

p = 2, q = 8
→ Start at 6
→ 2 < 6 and 8 > 6 ⇒ **split** happens here ⇒ LCA = `6`

---

### ✅ Optimized BST-Based Solution (Iterative)

```javascript
function lowestCommonAncestor(root, p, q) {
  let curr = root;

  while (curr) {
    if (p.val < curr.val && q.val < curr.val) {
      curr = curr.left;
    } else if (p.val > curr.val && q.val > curr.val) {
      curr = curr.right;
    } else {
      return curr;
    }
  }

  return null;
}
```

---

### ✅ Recursive Version

```javascript
function lowestCommonAncestor(root, p, q) {
  if (!root) return null;

  if (p.val < root.val && q.val < root.val)
    return lowestCommonAncestor(root.left, p, q);

  if (p.val > root.val && q.val > root.val)
    return lowestCommonAncestor(root.right, p, q);

  return root;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity:** `O(H)`

  - Where H = height of the BST
  - Balanced: `O(log N)`
  - Skewed: `O(N)`

- **Space Complexity:**

  - Iterative: `O(1)`
  - Recursive: `O(H)` (recursion stack)

---

## 🔢 **8. Minimum Increments to Equalize Leaf Paths**

### 📘 Problem Statement

You are given a **binary tree**, where each **node has a value** (non-negative integers).
Your task is to **increment** the values of nodes in such a way that **all root-to-leaf path sums become equal**.

At each step, you can **increment any node’s value by 1**.
Return the **minimum number of total increments** required to achieve this.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```
      1
     / \
    2   3
```

- Path sums:

  - 1 → 2 = 3
  - 1 → 3 = 4

- To make both equal, increase `2` to `3`
- 🔁 Total increments = 1

#### ✅ Test Case 2:

```
        1
       / \
      2   3
     /   / \
    4   5   6
```

- Path sums:

  - 1 → 2 → 4 = 7
  - 1 → 3 → 5 = 9
  - 1 → 3 → 6 = 10

- Max path sum = 10
- Increments needed:

  - (1 → 2 → 4): needs 3
  - (1 → 3 → 5): needs 1
  - (1 → 3 → 6): needs 0

- 🔁 Total = 4

---

### 💡 Intuition

- Find the **maximum path sum** among all root-to-leaf paths.
- Then, for each root-to-leaf path, compute how much **less** it is from the max.
- Add that **difference** to total increments.

We can use **postorder DFS traversal** to:

1. Calculate the sum of each path.
2. Accumulate the **difference** needed at each subtree.

---

### ✅ Recursive DFS Solution (JavaScript)

```javascript
function minIncrements(root) {
  let totalIncrements = 0;

  function dfs(node) {
    if (!node) return 0;

    const leftSum = dfs(node.left);
    const rightSum = dfs(node.right);

    // Increment the smaller side to match the bigger
    totalIncrements += Math.abs(leftSum - rightSum);

    // Return max path sum through this node
    return node.val + Math.max(leftSum, rightSum);
  }

  dfs(root);
  return totalIncrements;
}
```

🧠 **Key Idea:**
We recursively find left and right subtree sums, and **equalize them** by adding the absolute difference to total operations.

---

### ⏱ Time and Space Complexity

- **Time Complexity:** `O(N)` — each node is visited once
- **Space Complexity:** `O(H)` — recursion stack (H = height)

---

## 🔢 **9. Construct a Binary Search Tree from Preorder Traversal**

### 📘 Problem Statement

You are given an array `preorder[]` representing the **preorder traversal** of a **Binary Search Tree (BST)**.
Your task is to construct the **original BST** from this preorder traversal and return its root.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

Input: `preorder = [8, 5, 1, 7, 10, 12]`
Output:

```
        8
       / \
      5   10
     / \    \
    1   7    12
```

#### ✅ Test Case 2:

Input: `preorder = [10, 5, 1, 7, 40, 50]`
Output:

```
        10
       /  \
      5    40
     / \     \
    1   7     50
```

#### ✅ Test Case 3:

Input: `preorder = [1]`
Output: Single node tree with value 1

---

### 💡 Intuition

In **preorder traversal**, the first element is always the **root**.

In a BST:

- All nodes in the **left subtree** are **less than root**
- All nodes in the **right subtree** are **greater than root**

We maintain a **range** for valid values using `min` and `max`.
We recursively construct left and right subtrees based on this range.

---

### 🔍 Dry Run

Input: `[8, 5, 1, 7, 10, 12]`

- Root = 8
- 5 < 8 → go left
- 1 < 5 → left
- 7 > 5 but < 8 → right of 5
- 10 > 8 → right
- 12 > 10 → right of 10

---

### ✅ Optimized Recursive Solution (O(N) with Index Tracking)

```javascript
class Node {
  constructor(val) {
    this.val = val;
    this.left = null;
    this.right = null;
  }
}

function bstFromPreorder(preorder) {
  let index = 0;

  function buildBST(min, max) {
    if (index === preorder.length) return null;

    let val = preorder[index];
    if (val < min || val > max) return null;

    let root = new Node(val);
    index++;

    root.left = buildBST(min, val);
    root.right = buildBST(val, max);

    return root;
  }

  return buildBST(-Infinity, Infinity);
}
```

---

### ✅ Iterative Stack-Based Version

```javascript
function bstFromPreorder(preorder) {
  if (!preorder.length) return null;

  const root = new Node(preorder[0]);
  const stack = [root];

  for (let i = 1; i < preorder.length; i++) {
    let node = new Node(preorder[i]);
    let parent = null;

    while (stack.length && stack[stack.length - 1].val < node.val) {
      parent = stack.pop();
    }

    if (parent) {
      parent.right = node;
    } else {
      stack[stack.length - 1].left = node;
    }

    stack.push(node);
  }

  return root;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(H)` = recursion stack or stack size (H = height)

---

## 🔢 **10. Inorder Successor / Predecessor in a BST**

### 📘 Problem Statement

You are given a **Binary Search Tree (BST)** and a target node `x`.

- Find its **Inorder Successor** (the node with the **next higher** value than `x`)
- Find its **Inorder Predecessor** (the node with the **next smaller** value than `x`)

> If such a node doesn’t exist, return `null`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```
        8
       / \
      4   12
     / \   / \
    2   6 10 14
```

- `x = 6`

  - Inorder Successor: `8`
  - Inorder Predecessor: `4`

#### ✅ Test Case 2:

```
        5
         \
          6
           \
            7
```

- `x = 6`

  - Inorder Successor: `7`
  - Inorder Predecessor: `5`

#### ✅ Test Case 3:

```
       10
      /
     5
x = 5
```

- Inorder Successor: `10`
- Inorder Predecessor: `null`

---

### 💡 Intuition

### ✅ Inorder Successor:

- If `x.right` exists → successor is **leftmost node in x’s right subtree**
- Else → move up the tree; the **deepest ancestor** for which `x` lies in its **left subtree**

### ✅ Inorder Predecessor:

- If `x.left` exists → predecessor is **rightmost node in x’s left subtree**
- Else → move up; the **deepest ancestor** where `x` lies in the **right subtree**

---

### 🔍 Dry Run

Tree:

```
        8
       / \
      4   12
     / \   / \
    2   6 10 14
```

Target = 6

- Right subtree doesn’t exist
- So move up: 6 → 4 → 8
- 6 is in **left** of 8 → 8 is the **successor**
- 6 is in **right** of 4 → 4 is the **predecessor**

---

### ✅ JavaScript Code (Iterative BST-Based)

### 🔹 Inorder Successor

```javascript
function inorderSuccessor(root, x) {
  let successor = null;

  while (root) {
    if (x.val < root.val) {
      successor = root;
      root = root.left;
    } else {
      root = root.right;
    }
  }

  return successor;
}
```

### 🔹 Inorder Predecessor

```javascript
function inorderPredecessor(root, x) {
  let predecessor = null;

  while (root) {
    if (x.val > root.val) {
      predecessor = root;
      root = root.right;
    } else {
      root = root.left;
    }
  }

  return predecessor;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity:** `O(H)` where H = height of the tree
- **Space Complexity:** `O(1)` (iterative)

---

## 🔢 **11. Merge Two Binary Search Trees**

### 📘 Problem Statement

You are given the **roots of two BSTs**: `root1` and `root2`.
Your task is to **merge** these BSTs into a **single BST** that contains all elements from both trees, and return the root of the **new balanced BST**.

✅ The final tree should follow **BST rules**, and ideally be **balanced** for optimal operations.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```
BST 1:       3            BST 2:       8
            / \                       / \
           1   4                     6   10
```

Merged Output BST:

```
         6
       /   \
      3     8
     / \   / \
    1   4 7   10
```

#### ✅ Test Case 2:

```
root1 = null, root2 = valid BST
⇒ Output: root2

root1 = valid BST, root2 = null
⇒ Output: root1
```

---

### 💡 Intuition

To merge two BSTs efficiently:

#### ✅ Step-by-step approach:

1. Perform **inorder traversal** of both BSTs to get two **sorted arrays**.
2. Merge the two sorted arrays into **one sorted array**.
3. Construct a **balanced BST** from the merged array.

This ensures `O(N)` time and **balanced structure**.

---

### 🔍 Dry Run

Input BSTs:

- BST1 inorder: \[1, 3, 4]
- BST2 inorder: \[6, 8, 10]

Merged array: \[1, 3, 4, 6, 8, 10]
Construct Balanced BST from merged array → done!

---

### ✅ JavaScript Implementation

### 🔹 Step 1: Inorder Traversal

```javascript
function inorderTraversal(root, result) {
  if (!root) return;
  inorderTraversal(root.left, result);
  result.push(root.val);
  inorderTraversal(root.right, result);
}
```

### 🔹 Step 2: Merge Two Sorted Arrays

```javascript
function mergeSortedArrays(arr1, arr2) {
  let merged = [],
    i = 0,
    j = 0;

  while (i < arr1.length && j < arr2.length) {
    if (arr1[i] < arr2[j]) merged.push(arr1[i++]);
    else merged.push(arr2[j++]);
  }

  while (i < arr1.length) merged.push(arr1[i++]);
  while (j < arr2.length) merged.push(arr2[j++]);

  return merged;
}
```

### 🔹 Step 3: Build BST from Sorted Array

```javascript
class Node {
  constructor(val) {
    this.val = val;
    this.left = null;
    this.right = null;
  }
}

function buildBSTFromSortedArray(arr, start, end) {
  if (start > end) return null;

  const mid = Math.floor((start + end) / 2);
  const root = new Node(arr[mid]);

  root.left = buildBSTFromSortedArray(arr, start, mid - 1);
  root.right = buildBSTFromSortedArray(arr, mid + 1, end);

  return root;
}
```

### 🔹 Final Merge Function

```javascript
function mergeTwoBSTs(root1, root2) {
  let list1 = [],
    list2 = [];

  inorderTraversal(root1, list1);
  inorderTraversal(root2, list2);

  const mergedList = mergeSortedArrays(list1, list2);
  return buildBSTFromSortedArray(mergedList, 0, mergedList.length - 1);
}
```

---

### ⏱ Time and Space Complexity

| Step                       | Time     | Space    |
| -------------------------- | -------- | -------- |
| Inorder traversal (2 BSTs) | O(N + M) | O(N + M) |
| Merging sorted arrays      | O(N + M) | O(N + M) |
| Building balanced BST      | O(N + M) | O(H)     |

✅ **Overall Time Complexity:** `O(N + M)`
✅ **Space Complexity:** `O(N + M)`

---

## 🔢 **12. Two Sum in BST — Check if a Pair with Sum K Exists**

### 📘 Problem Statement

Given the **root of a Binary Search Tree** (BST) and a **target integer K**,
determine if there exist **two elements** in the BST such that their sum is **equal to K**.

> Return `true` if such a pair exists, otherwise `false`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```
       5
      / \
     3   6
    / \    \
   2   4    7
K = 9
```

Output: ✅ `true` (2 + 7 = 9)

#### ✅ Test Case 2:

Same tree
K = 28
Output: ❌ `false`

#### ✅ Test Case 3:

```
     1
      \
       2
        \
         3
K = 4
```

Output: ✅ `true` (1 + 3)

---

### 💡 Intuition

There are **3 approaches** to solve this:

---

### ✅ **Approach 1: Inorder Traversal + Two Pointers**

- Perform **inorder traversal** → gives a **sorted array**
- Use **two pointer technique** on the array to find if any pair sums to `K`

---

### 🔍 Dry Run

Tree:

```
       5
      / \
     3   6
    / \    \
   2   4    7
```

Inorder: \[2, 3, 4, 5, 6, 7]
K = 9
2 + 7 = ✅

---

### ✅ JavaScript Code: Inorder + Two Pointers

```javascript
function findTarget(root, k) {
  let inorder = [];

  function dfs(node) {
    if (!node) return;
    dfs(node.left);
    inorder.push(node.val);
    dfs(node.right);
  }

  dfs(root);

  let left = 0,
    right = inorder.length - 1;

  while (left < right) {
    const sum = inorder[left] + inorder[right];
    if (sum === k) return true;
    else if (sum < k) left++;
    else right--;
  }

  return false;
}
```

---

### ✅ Approach 2: DFS + HashSet (Like "Two Sum" in array)

- Traverse the tree using DFS.
- For each node, check if `k - node.val` is in a **HashSet**.
- If yes, return true.
- Else, add node value to the set.

---

### 🔹 JavaScript Code: DFS + Set

```javascript
function findTarget(root, k) {
  const set = new Set();

  function dfs(node) {
    if (!node) return false;
    if (set.has(k - node.val)) return true;
    set.add(node.val);
    return dfs(node.left) || dfs(node.right);
  }

  return dfs(root);
}
```

---

### ⏱ Time and Space Complexity

| Approach     | Time | Space |
| ------------ | ---- | ----- |
| Inorder + 2P | O(N) | O(N)  |
| DFS + Set    | O(N) | O(N)  |
| BST Iterator | O(N) | O(H)  |

> Where N = number of nodes, H = height of BST

---

## 🔢 **13. Recover BST | Correct BST with Two Nodes Swapped**

### 📘 Problem Statement

Two nodes of a **Binary Search Tree (BST)** are **swapped by mistake**, violating the BST property.
You need to **recover the BST** by fixing these two nodes **without changing the tree’s structure**.

> Return the root of the corrected BST.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

**Input BST (Incorrect):**

```
      3
     / \
    1   4
       /
      2
```

Here, nodes `2` and `3` are swapped.
**Correct BST:**

```
      2
     / \
    1   4
       /
      3
```

#### ✅ Test Case 2:

```
      10
     /  \
    5    15
   / \   /
  2  20 12
```

Swapped nodes: 20 and 12
Correct BST:

```
      10
     /  \
    5    15
   / \   /
  2  12 20
```

---

### 💡 Intuition

In a BST, the **inorder traversal** gives **sorted values**.

If two nodes are swapped:

- One violation (non-adjacent nodes): we’ll see **two drops** in order
- One violation (adjacent nodes): we’ll see **one drop**

> Identify the two nodes that break the order and **swap them back**.

---

### 🔍 Dry Run

Inorder of valid BST: `[1, 2, 3, 4]`
Inorder of broken BST: `[1, 3, 2, 4]`

We see a **drop from 3 to 2** ⇒ Swap 3 and 2

---

### ✅ JavaScript Code (Recursive Inorder Traversal)

```javascript
function recoverTree(root) {
  let first = null,
    second = null,
    prev = null;

  function inorder(node) {
    if (!node) return;

    inorder(node.left);

    if (prev && node.val < prev.val) {
      if (!first) first = prev;
      second = node;
    }
    prev = node;

    inorder(node.right);
  }

  inorder(root);

  // Swap the values of the two nodes
  [first.val, second.val] = [second.val, first.val];

  return root;
}
```

---

### ⏱ Time and Space Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:**

  - Recursive stack: `O(H)`
  - Can be optimized to `O(1)` using **Morris Inorder Traversal**

---

## 🔢 **14. Largest BST in a Binary Tree**

### 📘 Problem Statement

You are given a **Binary Tree** (not necessarily a BST).
Find the **size (number of nodes)** of the **largest subtree** that is a **Binary Search Tree (BST)**.

> A subtree is a tree that consists of a node and all its descendants.
> You must identify the **largest such subtree** that follows BST properties.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```
       10
      /  \
     5   15
    / \    \
   1   8    7
```

Output: `3`
Explanation: The subtree rooted at node `5` is a valid BST with size 3.

---

#### ✅ Test Case 2:

```
     5
    / \
   2   4
```

Output: `2`
Explanation: Subtree rooted at `2` is a valid BST

---

#### ✅ Test Case 3:

```
     2
    / \
   1   3
```

Output: `3`
Explanation: The whole tree is a valid BST

---

### 💡 Intuition

Use **post-order traversal** (left → right → root)
At each node, determine:

- Whether the **left and right subtrees** are BSTs
- The **minimum and maximum** values in the subtree
- The **size** of the largest BST subtree rooted at that node

If current node satisfies BST property:

- Combine left + right + root and return updated size and boundaries

---

### ✅ What We Track for Each Node:

```text
- isBST (true/false)
- size (size of BST subtree)
- minVal (min value in subtree)
- maxVal (max value in subtree)
```

---

### ✅ JavaScript Code

```javascript
function largestBSTSubtree(root) {
  let maxSize = 0;

  function postOrder(node) {
    if (!node) {
      return { isBST: true, size: 0, min: Infinity, max: -Infinity };
    }

    const left = postOrder(node.left);
    const right = postOrder(node.right);

    // Check if current subtree is a BST
    if (
      left.isBST &&
      right.isBST &&
      node.val > left.max &&
      node.val < right.min
    ) {
      const currSize = left.size + right.size + 1;
      maxSize = Math.max(maxSize, currSize);
      return {
        isBST: true,
        size: currSize,
        min: Math.min(node.val, left.min),
        max: Math.max(node.val, right.max),
      };
    }

    return { isBST: false, size: 0, min: 0, max: 0 };
  }

  postOrder(root);
  return maxSize;
}
```

---

### 🔍 Dry Run

Tree:

```
       10
      /  \
     5   15
    / \    \
   1   8    7
```

- Left subtree of `10`: BST of size 3 (1,5,8) ✅
- Right subtree of `10`: not a BST because 7 < 15 ❌
  → Max BST size = 3

---

### ⏱ Time and Space Complexity

- **Time Complexity:** `O(N)` (visit every node once)
- **Space Complexity:** `O(H)` (recursion stack)

---
