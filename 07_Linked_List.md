# 📘 Linked List

## 🔹 What is a Linked List?

A **Linked List** is a linear data structure where each element (called a **node**) is stored at a random memory location and contains:

- **Data**
- **Pointer (next)** to the next node in the sequence.

Unlike arrays, it doesn’t need contiguous memory and grows dynamically.

![Linked List](https://upload.wikimedia.org/wikipedia/commons/6/6d/Singly-linked-list.svg)

---

## 🔹 Node Structure

Each node has:

- Data field
- Pointer to next node

### C-style representation:

```c
struct Node {
   int data;
   struct Node* next;
};
```

---

## 🔹 Types of Linked Lists

### 🔸 1. Singly Linked List

Each node points to the next node.

![Singly Linked List](https://upload.wikimedia.org/wikipedia/commons/6/6d/Singly-linked-list.svg)

---

### 🔸 2. Doubly Linked List

Each node points to both the **previous** and **next** node.

![Doubly Linked List](https://upload.wikimedia.org/wikipedia/commons/5/5e/Doubly-linked-list.svg)

---

### 🔸 3. Circular Linked List

The last node points back to the first node.

#### 🔹 Singly Circular:

![Circular Singly Linked List](https://upload.wikimedia.org/wikipedia/commons/thumb/d/df/Circularly-linked-list.svg/350px-Circularly-linked-list.svg.png)

#### 🔹 Doubly Circular:

![Circular Doubly Linked List](https://examradar.com/wp-content/uploads/2016/10/Figure-3.8.1.-Circular-Double-Linked-List.png)

---

## 🔹 Operations on Linked Lists

### 🔸 Traversal

Move through each node until the end.

### 🔸 Insertion

- At beginning
- At end
- At a specific position

### 🔸 Deletion

- From beginning
- From end
- From a specific position

### 🔸 Search

Look for a specific value in the list.

### 🔸 Reversal

Reverse the direction of all pointers.

---

## 🔹 Time and Space Complexities

| Operation   | Singly LL | Doubly LL |
| ----------- | --------- | --------- |
| Insert Head | O(1)      | O(1)      |
| Insert Tail | O(n)\*    | O(n)\*    |
| Delete Head | O(1)      | O(1)      |
| Delete Tail | O(n)      | O(1)\*\*  |
| Search      | O(n)      | O(n)      |

> \* Can be O(1) if you maintain a tail pointer.
> \*\* For Doubly LL with tail pointer.

---

## 🔹 Advantages

- Dynamic size (no pre-allocation)
- Efficient insertions/deletions at head
- Great for implementing stacks, queues

---

## 🔹 Disadvantages

- Extra memory (pointer per node)
- Sequential access only (no indexing)
- More complex implementation/debugging

---

## 🔹 Applications

- Stack and Queue implementation
- Undo operations (text editors)
- Graph representations (Adjacency List)
- Dynamic memory allocation
- Music/playlist navigation

---

## 🔹 Linked List vs Array

| Feature            | Array    | Linked List  |
| ------------------ | -------- | ------------ |
| Memory Allocation  | Static   | Dynamic      |
| Access             | O(1)     | O(n)         |
| Insertion/Deletion | O(n)     | O(1) at head |
| Memory Waste       | Possible | Efficient    |

---

Here’s a complete and **fully featured Linked List class in JavaScript**, covering **all commonly used methods** for singly linked lists. Each method includes:

✅ Clean implementation
✅ Handles edge cases
✅ Suitable for DSA practice and interviews

---

## 📦 **Single LinkedList** Class

```javascript
// Node class
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

// LinkedList class
class LinkedList {
  constructor() {
    this.head = null;
  }

  // ✅ Insert at the beginning
  insertAtBeginning(data) {
    const newNode = new Node(data);
    newNode.next = this.head;
    this.head = newNode;
  }

  // ✅ Insert at the end
  insertAtEnd(data) {
    const newNode = new Node(data);
    if (!this.head) {
      this.head = newNode;
      return;
    }

    let temp = this.head;
    while (temp.next) {
      temp = temp.next;
    }
    temp.next = newNode;
  }

  // ✅ Insert at a given position (0-based)
  insertAtPosition(data, index) {
    if (index < 0) return;

    const newNode = new Node(data);
    if (index === 0) {
      newNode.next = this.head;
      this.head = newNode;
      return;
    }

    let prev = null;
    let curr = this.head;
    let count = 0;

    while (curr !== null && count < index) {
      prev = curr;
      curr = curr.next;
      count++;
    }

    if (count !== index) {
      console.log("Index out of bounds");
      return;
    }

    newNode.next = curr;
    prev.next = newNode;
  }

  // ✅ Delete at beginning
  deleteAtBeginning() {
    if (!this.head) return;
    this.head = this.head.next;
  }

  // ✅ Delete at end
  deleteAtEnd() {
    if (!this.head) return;

    if (!this.head.next) {
      this.head = null;
      return;
    }

    let temp = this.head;
    while (temp.next && temp.next.next) {
      temp = temp.next;
    }

    temp.next = null;
  }

  // ✅ Delete at a given index
  deleteAtPosition(index) {
    if (index < 0 || !this.head) return;

    if (index === 0) {
      this.head = this.head.next;
      return;
    }

    let curr = this.head;
    let prev = null;
    let count = 0;

    while (curr && count < index) {
      prev = curr;
      curr = curr.next;
      count++;
    }

    if (!curr) {
      console.log("Index out of bounds");
      return;
    }

    prev.next = curr.next;
  }

  // ✅ Search for a value
  search(value) {
    let temp = this.head;
    let index = 0;

    while (temp) {
      if (temp.data === value) return index;
      temp = temp.next;
      index++;
    }

    return -1; // not found
  }

  // ✅ Reverse the linked list
  reverse() {
    let prev = null;
    let curr = this.head;
    let next = null;

    while (curr) {
      next = curr.next;
      curr.next = prev;
      prev = curr;
      curr = next;
    }

    this.head = prev;
  }

  // ✅ Get length of the list
  getLength() {
    let count = 0;
    let temp = this.head;

    while (temp) {
      count++;
      temp = temp.next;
    }

    return count;
  }

  // ✅ Get middle element (slow-fast pointer)
  getMiddle() {
    let slow = this.head;
    let fast = this.head;

    while (fast && fast.next) {
      slow = slow.next;
      fast = fast.next.next;
    }

    return slow ? slow.data : null;
  }

  // ✅ Check if the list has a cycle (Floyd's Algorithm)
  hasCycle() {
    let slow = this.head;
    let fast = this.head;

    while (fast && fast.next) {
      slow = slow.next;
      fast = fast.next.next;

      if (slow === fast) return true;
    }

    return false;
  }

  // ✅ Print the entire list
  display() {
    let temp = this.head;
    let result = "";

    while (temp) {
      result += temp.data + " -> ";
      temp = temp.next;
    }

    console.log(result + "NULL");
  }
}
```

---

## 🧪 Example Usage

```javascript
const ll = new LinkedList();
ll.insertAtEnd(10);
ll.insertAtEnd(20);
ll.insertAtEnd(40);
ll.insertAtPosition(30, 2);
ll.insertAtBeginning(5);
ll.display(); // 5 -> 10 -> 20 -> 30 -> 40 -> NULL

ll.deleteAtBeginning();
ll.deleteAtEnd();
ll.deleteAtPosition(1);
ll.display(); // 10 -> 30 -> NULL

console.log("Found at:", ll.search(30)); // Index: 1
console.log("Length:", ll.getLength()); // Length: 2
console.log("Middle:", ll.getMiddle()); // Middle: 30

ll.reverse();
ll.display(); // 30 -> 10 -> NULL
```

---

## 🔚 Summary

- Types: **Singly**, **Doubly**, **Circular**.
- Used for dynamic memory use cases.

---

# Single Linked List

## 1. **Length of the Linked List**

Given the **head of a singly linked list**, determine the **number of nodes** (i.e., the length) in the list.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: 1 → 2 → 3 → 4 → 5 → null
Output: 5
```

#### Test Case 2:

```js
Input: 10 → 20 → 30 → null
Output: 3
```

#### Test Case 3:

```js
Input: 5 → null
Output: 1
```

#### Test Case 4:

```js
Input: null;
Output: 0;
```

---

### 💡 Intuition

To find the length of a singly linked list:

- Start from the `head` node.
- Traverse each node one by one.
- Keep a **counter** and increment it at each node.
- Stop when you reach `null`.

This is a basic linear traversal — we just count nodes.

---

### 🔄 Dry Run

Input:

```js
head = 1 → 2 → 3 → null
```

1. `count = 0`, current = 1
2. Visit 1 → `count = 1`
3. Visit 2 → `count = 2`
4. Visit 3 → `count = 3`
5. Reached `null` → stop

✅ Final answer: `3`

---

### 🧑‍💻 JavaScript Code

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

function getLength(head) {
  let count = 0;
  let current = head;

  while (current !== null) {
    count++;
    current = current.next;
  }

  return count;
}

// Test Cases
console.log(getLength(buildLinkedList([1, 2, 3, 4, 5]))); // 5
console.log(getLength(buildLinkedList([10, 20, 30]))); // 3
console.log(getLength(buildLinkedList([5]))); // 1
console.log(getLength(buildLinkedList([]))); // 0
```

---

### ⏱️ Time & Space Complexity

#### ⏳ Time Complexity: `O(n)`

- `n` is the number of nodes in the linked list.
- We visit each node once.

#### 🗂️ Space Complexity: `O(1)`

- No extra space is used (only a few variables).

---

- Always handle the **edge case of an empty list** (`head === null`).

---

## 2. **Search Element in a Linked List**

Given the **head** of a singly linked list and a **key**, determine whether the **key exists** in the list or not.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: head = 1 → 2 → 3 → 4 → 5, key = 3
Output: true
```

#### Test Case 2:

```js
Input: head = 10 → 20 → 30 → null, key = 40
Output: false
```

#### Test Case 3:

```js
Input: head = 5 → null, key = 5
Output: true
```

#### Test Case 4:

```js
Input: (head = null), (key = 1);
Output: false;
```

---

### 💡 Intuition

To check if a value exists in the linked list:

- Start from the head node.
- Traverse each node and compare the current node's value to the target key.
- If found, return `true`.
- If the traversal ends without a match, return `false`.

Simple **linear search** logic is applied here.

---

### 🔄 Dry Run

Input:

```js
head = 1 → 2 → 3 → null, key = 2
```

1. Current = 1 → `1 !== 2`
2. Move to 2 → `2 === 2` ✅
   Return `true`

---

### 🧑‍💻 JavaScript Code

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

function searchInLinkedList(head, key) {
  let current = head;

  while (current !== null) {
    if (current.value === key) {
      return true; // Key found
    }
    current = current.next;
  }

  return false; // Key not found
}

// Test Cases
console.log(searchInLinkedList(buildLinkedList([1, 2, 3, 4, 5]), 3)); // true
console.log(searchInLinkedList(buildLinkedList([10, 20, 30]), 40)); // false
console.log(searchInLinkedList(buildLinkedList([5]), 5)); // true
console.log(searchInLinkedList(buildLinkedList([]), 1)); // false
```

---

### ⏱️ Time & Space Complexity

#### ⏳ Time Complexity: `O(n)`

- We may traverse all nodes in the worst case.

#### 🗂️ Space Complexity: `O(1)`

- No extra space, just pointer and condition check.

---

- Make sure to handle edge cases like **empty lists**.

---

# Medium Problems : Single Linked List

## 1. **Reverse a Singly Linked List**

Given the `head` of a singly linked list, **reverse the linked list** and return the new head.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: 1 → 2 → 3 → 4 → 5 → null
Output: 5 → 4 → 3 → 2 → 1 → null
```

#### Test Case 2:

```js
Input: 10 → 20 → 30 → null
Output: 30 → 20 → 10 → null
```

#### Test Case 3:

```js
Input: 5 → null
Output: 5 → null
```

#### Test Case 4:

```js
Input: null;
Output: null;
```

---

### 💡 Approch 1 :

To reverse a singly linked list, we need to change the direction of the `next` pointers of the nodes.

We maintain three pointers:

- `prev`: starts as `null`
- `curr`: starts at `head`
- `next`: temporarily stores `curr.next` so we don’t lose the rest of the list during reversal

In each iteration:

1. Save `next = curr.next`
2. Reverse: `curr.next = prev`
3. Move `prev = curr` and `curr = next`

At the end, `prev` will be the **new head** of the reversed list.

---

#### 🔄 Dry Run

Input:

```js
head = 1 → 2 → 3 → null
```

| Step | curr | next | prev | Linked List  |
| ---- | ---- | ---- | ---- | ------------ |
| Init | 1    | -    | null | 1 → 2 → 3    |
| 1    | 1    | 2    | null | 1 → null     |
| 2    | 2    | 3    | 1    | 2 → 1 → null |
| 3    | 3    | null | 2    | 3 → 2 → 1    |

✅ Final reversed list: `3 → 2 → 1 → null`

---

#### 🧑‍💻 JavaScript Code

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

function reverseLinkedList(head) {
  let prev = null;
  let curr = head;

  while (curr !== null) {
    const next = curr.next; // Save next
    curr.next = prev; // Reverse current
    prev = curr; // Move prev
    curr = next; // Move curr
  }

  return prev; // New head of reversed list
}

// Test Cases
let list1 = buildLinkedList([1, 2, 3, 4, 5]);
printLinkedList(reverseLinkedList(list1)); // 5 → 4 → 3 → 2 → 1 → null

let list2 = buildLinkedList([10, 20, 30]);
printLinkedList(reverseLinkedList(list2)); // 30 → 20 → 10 → null

let list3 = buildLinkedList([5]);
printLinkedList(reverseLinkedList(list3)); // 5 → null

let list4 = buildLinkedList([]);
printLinkedList(reverseLinkedList(list4)); // null
```

---

#### ⏱️ Time & Space Complexity

#### ⏳ Time Complexity: `O(n)`

- Each node is visited once.

#### 🗂️ Space Complexity: `O(1)`

- No extra data structures; only three pointers.

---

---

### Approch 2 : Recursive

In recursion, we handle the **reversal** as follows:

1. **Base case**: If head is `null` or `head.next` is `null`, return `head`.
2. Recursively call the function on `head.next`.
3. Reverse the link by doing:

   ```js
   head.next.next = head;
   head.next = null;
   ```

4. Return the new head from recursive calls.

---

#### 🔄 Dry Run

Input:

```js
head = 1 → 2 → 3 → null
```

- Call stack:

  - reverse(1)

    - reverse(2)

      - reverse(3)

        - base case: return 3

Now unwind:

- 2.next.next = 2 → 3.next = 2 → 3 → 2
- 2.next = null → 3 → 2 → null
- Similarly, 1 → 2 → 3 becomes 3 → 2 → 1 → null

✅ Final: `3 → 2 → 1 → null`

---

#### 🧑‍💻 JavaScript Code (Recursive)

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

// Recursive reversal
function reverseLinkedListRecursive(head) {
  if (head === null || head.next === null) {
    return head; // Base case
  }

  const newHead = reverseLinkedListRecursive(head.next); // Recurse

  head.next.next = head; // Reverse link
  head.next = null; // Break original link

  return newHead;
}

// Test Cases
let list1 = buildLinkedList([1, 2, 3, 4, 5]);
printLinkedList(reverseLinkedListRecursive(list1)); // 5 → 4 → 3 → 2 → 1 → null

let list2 = buildLinkedList([10, 20, 30]);
printLinkedList(reverseLinkedListRecursive(list2)); // 30 → 20 → 10 → null

let list3 = buildLinkedList([5]);
printLinkedList(reverseLinkedListRecursive(list3)); // 5 → null

let list4 = buildLinkedList([]);
printLinkedList(reverseLinkedListRecursive(list4)); // null
```

---

#### ⏱️ Time & Space Complexity

#### ⏳ Time Complexity: `O(n)`

- Each node is visited once via recursion.

#### 🗂️ Space Complexity: `O(n)`

- Due to recursive call stack (n recursive calls).

---

## 2. **Middle of the Linked List**

Given the head of a singly linked list, return the **middle node**.

- If there are **two middle nodes**, return the **second** one.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: 1 → 2 → 3 → 4 → 5 → null
Output: 3
```

#### Test Case 2:

```js
Input: 1 → 2 → 3 → 4 → 5 → 6 → null
Output: 4
```

#### Test Case 3:

```js
Input: 10 → 20 → null
Output: 20
```

#### Test Case 4:

```js
Input: 42 → null
Output: 42
```

---

### 💡 Approach 1: Using Length Count

#### 🔎 Intuition

1. Traverse the list once to count the number of nodes.
2. Calculate `mid = Math.floor(length / 2)`
3. Traverse again up to `mid` index and return the node.

---

#### 🔄 Dry Run (Test Case 1)

Input:

```js
1 → 2 → 3 → 4 → 5
```

**First Pass (counting):**

- Count = 5
- Mid = `Math.floor(5 / 2)` = 2

**Second Pass (reach index 2):**

- Node at index 2 = 3 → ✅

---

#### 🧑‍💻 JavaScript Code (Length Count)

```javascript
function findMiddleByCounting(head) {
  let count = 0;
  let current = head;

  // 1st pass: Count length
  while (current) {
    count++;
    current = current.next;
  }

  const mid = Math.floor(count / 2);

  // 2nd pass: Reach middle
  current = head;
  for (let i = 0; i < mid; i++) {
    current = current.next;
  }

  return current;
}
```

---

### 💡 Approach 2: Slow and Fast Pointer (Optimal) (TortoiseHare Method)

#### 🔎 Intuition

Use two pointers:

- `slow` moves one step at a time.
- `fast` moves two steps at a time.

When `fast` reaches the end, `slow` will be at the **middle**.

✅ Only one pass needed — more efficient.

---

#### 🔄 Dry Run (Test Case 2)

Input:

```js
1 → 2 → 3 → 4 → 5 → 6 → null
```

| Iteration | slow | fast |
| --------- | ---- | ---- |
| 1         | 2    | 3    |
| 2         | 3    | 5    |
| 3         | 4    | null |

✅ Middle: `4`

---

#### 🧑‍💻 JavaScript Code (Slow & Fast Pointer)

```javascript
function findMiddleByPointers(head) {
  let slow = head;
  let fast = head;

  while (fast !== null && fast.next !== null) {
    slow = slow.next;
    fast = fast.next.next;
  }

  return slow;
}
```

---

### ⏱️ Time & Space Complexity

#### ✅ Approach 1: Length Count

- **Time:** `O(n + n/2)` → `O(n)`
- **Space:** `O(1)`

#### ✅ Approach 2: Slow & Fast Pointer (Optimal)

- **Time:** `O(n)`
- **Space:** `O(1)`

---

## 3. **Detect Loop in a Singly Linked List**

Given the head of a singly linked list, **determine if there is a cycle (loop)** in the list.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: 1 → 2 → 3 → 4 → 2 (cycle)
Output: true
```

#### Test Case 2:

```js
Input: 1 → 2 → 3 → 4 → null
Output: false
```

#### Test Case 3:

```js
Input: 10 → 20 → 30 → 10 (cycle)
Output: true
```

#### Test Case 4:

```js
Input: 99 → null
Output: false
```

---

### 💡 Approach 1: Hashing (Visited Set)

#### 🔎 Intuition

- Use a `Set` to store visited nodes.
- While traversing the list, check if the current node is already in the set.

  - If yes → loop exists
  - If no → continue traversal

---

#### 🔄 Dry Run (Test Case 1)

```js
1 → 2 → 3 → 4
       ↑    ↓
       ← ← ←
```

Visited Set:

- Add 1
- Add 2
- Add 3
- Add 4
- Next is 2 → already visited → ✅ Loop detected

---

#### 🧑‍💻 JavaScript Code (Hashing)

```javascript
function detectLoopWithSet(head) {
  const visited = new Set();

  let current = head;
  while (current) {
    if (visited.has(current)) {
      return true; // Loop detected
    }
    visited.add(current);
    current = current.next;
  }

  return false; // No loop
}
```

---

### 💡 Approach 2: Floyd’s Cycle Detection (Tortoise and Hare)

#### 🔎 Intuition

- Use two pointers:

  - `slow` moves 1 step
  - `fast` moves 2 steps

- If there's a loop, `slow` and `fast` will eventually meet.
- If there's no loop, `fast` will reach `null`.

✅ More space-efficient than hashing.

---

#### 🔄 Dry Run (Test Case 1)

```js
1 → 2 → 3 → 4
       ↑    ↓
       ← ← ←
```

- slow = 1, fast = 1
- slow = 2, fast = 3
- slow = 3, fast = 2
- slow = 4, fast = 4 ✅ Met → Loop detected

---

#### 🧑‍💻 JavaScript Code (Floyd’s Algorithm)

```javascript
function detectLoopFloyd(head) {
  let slow = head;
  let fast = head;

  while (fast !== null && fast.next !== null) {
    slow = slow.next;
    fast = fast.next.next;

    if (slow === fast) {
      return true; // Loop detected
    }
  }

  return false; // No loop
}
```

---

### 👨‍🔧 Helper Functions (Including Loop Builder)

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

function buildLinkedListWithLoop(values, loopIndex = -1) {
  if (values.length === 0) return null;

  const nodes = values.map((val) => new Node(val));
  for (let i = 0; i < nodes.length - 1; i++) {
    nodes[i].next = nodes[i + 1];
  }

  if (loopIndex !== -1) {
    nodes[nodes.length - 1].next = nodes[loopIndex]; // create loop
  }

  return nodes[0]; // head
}

// Testing
let list1 = buildLinkedListWithLoop([1, 2, 3, 4], 1); // loop at node 2
let list2 = buildLinkedListWithLoop([1, 2, 3, 4]); // no loop
let list3 = buildLinkedListWithLoop([10, 20, 30], 0); // loop at node 10
let list4 = buildLinkedListWithLoop([99]); // single node no loop

console.log(detectLoopWithSet(list1)); // true
console.log(detectLoopWithSet(list2)); // false
console.log(detectLoopFloyd(list3)); // true
console.log(detectLoopFloyd(list4)); // false
```

---

### ⏱️ Time & Space Complexity

#### ✅ Approach 1: Hashing

- **Time:** `O(n)`
- **Space:** `O(n)` for the visited set

#### ✅ Approach 2: Floyd's Tortoise & Hare

- **Time:** `O(n)`
- **Space:** `O(1)` ✅ optimal

---

## 4. **Find the Starting Point of Loop in a Linked List**

Given the head of a singly linked list, **if there’s a loop**, return the **node where the loop begins**.

- If no loop exists, return `null`.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: 1 → 2 → 3 → 4 → 5 → 3 (loop to node with value 3)
Output: Node with value 3
```

#### Test Case 2:

```js
Input: 10 → 20 → 30 → 40 → 50 → 20 (loop to node with value 20)
Output: Node with value 20
```

#### Test Case 3:

```js
Input: 1 → 2 → 3 → 4 → null
Output: null
```

#### Test Case 4:

```js
Input: 1 → null
Output: null
```

---

### 💡 Intuition (Floyd’s Cycle + Reset to Head)

Once a **cycle is detected** using Floyd's algorithm (slow and fast meet), we do the following:

1. Move one pointer (`slow`) back to the **head**.
2. Keep the other pointer (`fast`) at the **meeting point**.
3. Move both pointers **one step at a time**.
4. The node where they meet again is the **start of the loop**.

#### Why It Works?

Let:

- `L` = distance from head to start of loop
- `C` = length of loop
- `X` = distance from start of loop to meeting point inside loop

After `fast` and `slow` meet:

- Distance moved by slow = `L + X`
- Distance moved by fast = `2(L + X)`

\=> Fast has done 1 extra loop:
`2(L + X) - (L + X) = C * k` → So, `L = C - X`, and moving both from `head` and `meeting point` will meet at loop start.

---

#### 🔄 Dry Run (Test Case 1)

```text
1 → 2 → 3 → 4 → 5
          ↑     ↓
          ← ← ←
```

- Slow = 3, Fast = 3 (meeting point inside loop)
- Reset slow to head:

  - Move slow and fast one step at a time
  - They meet again at node `3` → ✅ loop start

---

![](https://static.takeuforward.org/content/starting-of-loop-image6-HTpYvsVD)
![](https://static.takeuforward.org/content/starting-of-loop-image7-Iqeb2eA8)
![](https://static.takeuforward.org/content/starting-of-loop-image7-Iqeb2eA8)
![](https://static.takeuforward.org/content/starting-of-loop-image9-4izAdHOp)

#### 🧑‍💻 JavaScript Code

```javascript
function findLoopStart(head) {
  let slow = head;
  let fast = head;

  // Step 1: Detect loop
  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;

    if (slow === fast) {
      break; // meeting point found
    }
  }

  // No loop
  if (!fast || !fast.next) return null;

  // Step 2: Find loop start
  slow = head;
  while (slow !== fast) {
    slow = slow.next;
    fast = fast.next;
  }

  return slow; // loop start node
}
```

---

### 📌 Final Notes

- This is a **must-know** for interviews.
- It's often asked after loop detection to see if you understand **Floyd’s full power**.
- Follow-ups include:

  - **Remove the loop**
  - **Length of the loop**
  - **Detect intersection with loops**

---

## 5. **Length of Loop in a Linked List**

Given the `head` of a linked list, determine the **length of the loop** (if present).
Return `0` if no loop exists.

---

### 🧪 Test Cases

#### Test Case 1:

![](https://static.takeuforward.org/wp/uploads/2023/12/tuxpi.com_.1698730326-1024x537.jpg)

```js
Input: 1 → 2 → 3 → 4 → 5 → back to 3
Output: 3
```

#### Test Case 2:

![](https://static.takeuforward.org/wp/uploads/2023/12/tuxpi.com_.1698730362-1024x268.jpg)

```js
Input: 1 → 2 → 3 → 4 → 9 → 9 → null
Output: 0
```

#### Test Case 3:

```js
Input: 10 → 20 → 30 → 40 → 50 → 30 (loop)
Output: 3
```

#### Test Case 4:

```js
Input: 42 → null
Output: 0
```

---

### 💡 Intuition

1. First, detect if there is a **cycle** using **Floyd’s Cycle Detection** (`slow` and `fast` pointers).
2. Once they meet, a cycle is confirmed.
3. To find the **length**, keep one pointer at the meeting point and move it until it comes back to the same point, counting steps.

---

### 🔄 Dry Run (Test Case 1)

```text
1 → 2 → 3 → 4 → 5
          ↑     ↓
          ← ← ←
```

- slow and fast meet at node 4 → ✅ Loop detected
- Now fix pointer at 4 and count until we come back to 4:

  - 4 → 5 → 3 → 4 → count = 3
    ✅ Length of loop = 3

---

![](https://static.takeuforward.org/wp/uploads/2023/12/WhatsApp-Image-2023-12-17-at-18.20.52-922x1024.jpeg)
![](https://static.takeuforward.org/wp/uploads/2023/12/WhatsApp-Image-2023-12-17-at-18.20.52-922x1024.jpeg)

### 🧑‍💻 JavaScript Code

```javascript
function lengthOfLoop(head) {
  let slow = head;
  let fast = head;

  // Step 1: Detect loop
  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;

    if (slow === fast) {
      // Step 2: Count loop length
      return countLoopLength(slow);
    }
  }

  return 0; // No loop
}

function countLoopLength(meetingPoint) {
  let count = 1;
  let current = meetingPoint.next;

  while (current !== meetingPoint) {
    count++;
    current = current.next;
  }

  return count;
}
```

---

### ⏱️ Time & Space Complexity

#### ✅ Time Complexity: `O(n)`

- Linear time for loop detection and loop length counting.

#### ✅ Space Complexity: `O(1)`

- No extra space used (Floyd's algorithm is in-place).

---

## 6. **Check if a Linked List is Palindrome**

Given the head of a singly linked list, check whether the linked list is a **palindrome**.

A palindrome list reads the same **forwards** and **backwards**.

---

### 🧪 Test Cases

#### Test Case 1:

![](https://static.takeuforward.org/wp/uploads/2023/12/Screenshot-2023-11-12-at-2.19.16-PM-1024x184.png)

```js
Input: 1 → 2 → 3 → 2 → 1
Output: true
```

#### Test Case 2:

![](https://static.takeuforward.org/wp/uploads/2023/12/Screenshot-2023-11-12-at-2.19.16-PM-1024x184.png)

```js
Input: 1 → 2 → 3 → 3 → 2 → 1
Output: true
```

#### Test Case 3:

![](https://static.takeuforward.org/wp/uploads/2023/12/Screenshot-2023-11-12-at-2.26.29-PM-1024x194.png)

```js
Input: 1 → 2 → 3 → 2 → 3
Output: false
```

#### Test Case 4:

```js
Input: 42;
Output: true;
```

#### Test Case 5:

```js
Input: null;
Output: true;
```

---

### 💡 Approach 1: Copy to Array

#### 🔎 Intuition

- Traverse the list and copy values into an array.
- Check if the array is equal to its reverse.

✅ Simple, but uses `O(n)` space.

---

#### 🔄 Dry Run (Test Case 1)

```js
arr = [1, 2, 3, 2, 1]
reverse(arr) = [1, 2, 3, 2, 1] → ✅ Palindrome
```

---

#### 🧑‍💻 Code (Copy to Array)

```javascript
function isPalindromeArray(head) {
  const values = [];

  let current = head;
  while (current) {
    values.push(current.value);
    current = current.next;
  }

  for (let i = 0; i < values.length / 2; i++) {
    if (values[i] !== values[values.length - 1 - i]) {
      return false;
    }
  }

  return true;
}
```

---

### 💡 Approach 2: Reverse Second Half (Optimal)

#### 🔎 Intuition

1. Find middle using slow and fast pointers.
2. Reverse the second half.
3. Compare first half with reversed second half.
4. (Optional) Restore list by reversing second half again.

✅ In-place, `O(1)` space and `O(n)` time.

---

![](https://static.takeuforward.org/wp/uploads/2023/12/Screenshot-2023-11-12-at-6.03.39-PM-1024x908.png)

#### 🔄 Dry Run (Test Case 2)

```js
List: 1 → 2 → 3 → 3 → 2 → 1

Middle = 3
Second half after reverse: 1 → 2 → 3
Compare: 1 = 1, 2 = 2, 3 = 3 → ✅
```

---

#### 🧑‍💻 Code (Optimal Approach)

```javascript
function isPalindromeLinkedList(head) {
  if (!head || !head.next) return true;

  // Step 1: Find middle
  let slow = head,
    fast = head;
  while (fast.next && fast.next.next) {
    slow = slow.next;
    fast = fast.next.next;
  }

  // Step 2: Reverse second half
  let secondHalfStart = reverseList(slow.next);

  // Step 3: Compare both halves
  let first = head;
  let second = secondHalfStart;
  let isPalin = true;

  while (second) {
    if (first.value !== second.value) {
      isPalin = false;
      break;
    }
    first = first.next;
    second = second.next;
  }

  // Step 4: Optional - restore list
  slow.next = reverseList(secondHalfStart);

  return isPalin;
}

function reverseList(head) {
  let prev = null;
  let curr = head;

  while (curr) {
    let next = curr.next;
    curr.next = prev;
    prev = curr;
    curr = next;
  }

  return prev;
}
```

---

### ⏱️ Time & Space Complexity

#### ✅ Approach 1: Using Array

- **Time:** `O(n)`
- **Space:** `O(n)`

#### ✅ Approach 2: Reverse Half (Optimal)

- **Time:** `O(n)`
- **Space:** `O(1)` ✅ Best for interviews

---

## 7. **Segregate Even and Odd Nodes in Linked List**

Given a singly linked list of integers, **rearrange it so that all even nodes come before all odd nodes**, **preserving their relative order**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: 1 → 2 → 3 → 4 → 5 → 6 → null
Output: 2 → 4 → 6 → 1 → 3 → 5 → null
```

#### Test Case 2:

```js
Input: 1 → 3 → 5 → null
Output: 1 → 3 → 5 → null
```

#### Test Case 3:

```js
Input: 2 → 4 → 6 → 8 → null
Output: 2 → 4 → 6 → 8 → null
```

#### Test Case 4:

```js
Input: null;
Output: null;
```

---

### 💡 Intuition

1. Create **two separate lists**:

   - One for even nodes
   - One for odd nodes

2. Traverse the original list and distribute nodes to the corresponding lists.
3. Link the end of even list to the start of odd list.
4. Return the head of the even list.

✅ This approach preserves relative order.

---

#### 🔄 Dry Run (Test Case 1)

Input:

```js
1 → 2 → 3 → 4 → 5 → 6
```

Processing:

- Even: 2 → 4 → 6
- Odd: 1 → 3 → 5

Final Output:

```js
Even Head → 2 → 4 → 6 → 1 → 3 → 5 → null
```

![](https://lh4.googleusercontent.com/Dq42kif-qjpL8wOotdlNYh8PBa1rh5abZae19pQ8buylkh93evnLmCD-I7Wqwh0cMC3VemvJ2sGTJncenff1uGRg8VGK5AKRp--wuAYqR3VlvYY1uasO4RNgDBDZJeVDenH0uSY6)
![](https://lh3.googleusercontent.com/Uo7NXkqehsNDRsti1dfOG0YkYDwReSrSEgmUn49DQ7DuKjdZGWGKFrogE6eX47mOeaNcoEp_W1CgzBSiDVaCkracpNEagTxxrwIxP4bFs21TSNf1vas4U0g47ctDWJSpC963UCBJ)
![](https://lh6.googleusercontent.com/-iwAMihb-awsopN6uhs-fV1aXsZZ5Il0H56sC7GQd35GZjUjan-7Dtn9Mn1VdYuGTED7cbdZfx1VHdO3GSBG9m5wnzWfjTqYseOzxgiGIloheNnZV4qSJf8s2Y15DPdhZTCUklnO)
![](https://lh3.googleusercontent.com/yUk62TBUiKBQYbBegyX7uU-XvMYUjLWF4EKaStb_63zegetABNVKodzFFTGoDpvvXSimOqps9RP8mzPo0zmEGGpdSYrP3lWmNMTHjZcsDYaeO4GB-nj3IJtMUtjvtI5K7xReJVgh)
![](https://lh3.googleusercontent.com/x_nbnSbv_X5jij8S4vSSKNhraLb8w76eF-Vmysbto1z9NePe9iX0maVmS-a5kKG9y48WKvUyxz8AKKmTmDvuLMsXVgxxVOtOjvO-k6zRzSlEBZZs1eXEVFxmg1Ns7FZLRnLzVDta)
![](https://lh3.googleusercontent.com/_v-3mL0-BMY6l0tM2UAVeNWUIm160L69zF7WvtEd_bvg7BfslOjtLsUkkKGhY_nN7w4NRnO5Qg-KkDbn8dR0fEUy8CbHHVLxvcq-A-pjwHmEvOU9uV0x9jsqF6t-fIbVYPjFDKjP)

---

#### 🧑‍💻 JavaScript Code

```javascript
function segregateEvenOdd(head) {
  if (!head || !head.next) return head;

  let evenStart = null,
    evenEnd = null;
  let oddStart = null,
    oddEnd = null;

  let current = head;

  while (current) {
    const nextNode = current.next;
    current.next = null;

    if (current.value % 2 === 0) {
      // Even node
      if (!evenStart) {
        evenStart = evenEnd = current;
      } else {
        evenEnd.next = current;
        evenEnd = evenEnd.next;
      }
    } else {
      // Odd node
      if (!oddStart) {
        oddStart = oddEnd = current;
      } else {
        oddEnd.next = current;
        oddEnd = oddEnd.next;
      }
    }

    current = nextNode;
  }

  // No even nodes
  if (!evenStart) return oddStart;

  // Attach even to odd
  evenEnd.next = oddStart;

  return evenStart;
}
```

---

### ⏱️ Time & Space Complexity

#### ✅ Time Complexity: `O(n)`

- Single pass to distribute nodes.

#### ✅ Space Complexity: `O(1)`

- No extra data structures used; just rearranging pointers.

---

## 8. **Delete N-th Node from the End of Linked List**

Given a singly linked list and an integer `N`, delete the **N-th node from the end** of the list and print the updated list.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: 5 → 1 → 2, N = 2
Output: 5 → 2
```

#### Test Case 2:

```js
Input: 1 → 2 → 3 → 4 → 5, N = 3
Output: 1 → 2 → 4 → 5
```

#### Test Case 3:

```js
Input: 10 → 20 → 30 → 40 → 50, N = 5
Output: 20 → 30 → 40 → 50
```

#### Test Case 4:

```js
Input: 42, (N = 1);
Output: null;
```

---

### 💡 Intuition (Two-Pointer Technique)

1. Use two pointers: `first` and `second`
2. Move `first` N steps ahead.
3. Now move both `first` and `second` until `first` reaches the end.
4. `second` will be just before the node to delete.
5. Modify `second.next` to skip the node.

✅ One pass solution using two pointers!

---

#### 🔄 Dry Run (Test Case 2)

```js
Input: 1 → 2 → 3 → 4 → 5, N = 3

Step 1: Move first pointer 3 steps → at node 4
Step 2: Move both until first reaches null
   second ends at node 2
Step 3: Delete 3 → second.next = second.next.next

Output: 1 → 2 → 4 → 5 ✅
```

![](https://static.takeuforward.org/wp/uploads/2023/12/tuxpi.com_.1702844019.jpg)
![](https://static.takeuforward.org/wp/uploads/2023/12/tuxpi.com_.1702844072.jpg)
![](https://static.takeuforward.org/wp/uploads/2023/12/tuxpi.com_.1702844098.jpg)

---

### 🧑‍💻 JavaScript Code (Optimal)

```javascript
function deleteNthFromEnd(head, n) {
  const dummy = new Node(0);
  dummy.next = head;

  let first = dummy;
  let second = dummy;

  // Move first N+1 steps to reach right position
  for (let i = 0; i <= n; i++) {
    if (first === null) return head; // N > length
    first = first.next;
  }

  // Move both until first reaches end
  while (first !== null) {
    first = first.next;
    second = second.next;
  }

  // Delete node
  second.next = second.next.next;

  return dummy.next;
}
```

---

### ⏱️ Time & Space Complexity

#### ✅ Time Complexity: `O(n)`

- Single pass through the list using two pointers.

#### ✅ Space Complexity: `O(1)`

- No extra memory used besides pointers.

---

## 9. **Delete the Middle Node from a Linked List**

Given the head of a linked list, **delete the middle node** and return the modified head.

- If the number of nodes is **odd**, delete the **middle**.
- If even, delete the **second middle** node (as per the question).

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: 1 → 2 → 3 → 4 → 5
Output: 1 → 2 → 4 → 5
```

#### Test Case 2:

```js
Input: 1 → 2 → 3 → 4
Output: 1 → 2 → 4
```

#### Test Case 3:

```js
Input: 42;
Output: null;
```

#### Test Case 4:

```js
Input: 1 → 2
Output: 1
```

---

### 💡 Intuition (Slow & Fast Pointer)

1. Use `slow` and `fast` pointer approach to find the **middle node**.
2. Use an additional `prev` pointer to keep track of node before `slow`.
3. Once the middle is found, delete it using:
   `prev.next = slow.next`
4. Return the modified head.

📌 Note: In **even length**, `slow` will point to the **second middle**, which matches the problem requirement.

---

#### 🔄 Dry Run (Test Case 2)

```js
List: 1 → 2 → 3 → 4

- slow = 1, fast = 1
- slow = 2, fast = 3
- slow = 3, fast = null → stop

prev = 2
slow = 3 → delete node 3

Result: 1 → 2 → 4 ✅
```

![](https://static.takeuforward.org/wp/uploads/2023/12/Screenshot-2023-12-02-at-9.50.35-PM-1024x373.png)
![](https://static.takeuforward.org/wp/uploads/2023/12/Screenshot-2023-12-02-at-10.00.37-PM-1024x468.png)

---

### 🧑‍💻 JavaScript Code (Optimal)

```javascript
function deleteMiddle(head) {
  if (!head || !head.next) return null;

  let slow = head;
  let fast = head;
  let prev = null;

  while (fast && fast.next) {
    prev = slow;
    slow = slow.next;
    fast = fast.next.next;
  }

  // Delete the middle node
  prev.next = slow.next;

  return head;
}
```

---

### ⏱️ Time & Space Complexity

#### ✅ Time Complexity: `O(n)`

- One pass to find middle and update links.

#### ✅ Space Complexity: `O(1)`

- In-place operations with pointers.

---

## 10. **Sort a Linked List by Node Values**

Given the head of a **singly linked list**, sort its nodes in **ascending order** based on the **data value** in each node.

Return the new head of the sorted linked list.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: 4 → 2 → 1 → 3
Output: 1 → 2 → 3 → 4
```

#### Test Case 2:

```js
Input: 5 → 3 → 8 → 2 → 6
Output: 2 → 3 → 5 → 6 → 8
```

#### Test Case 3:

```js
Input: 10;
Output: 10;
```

#### Test Case 4:

```js
Input: null;
Output: null;
```

---

### 💡 Approach 1: Merge Sort (Optimal for Linked List)

#### 🔎 Why Merge Sort?

- Linked lists are **ideal for merge sort** because:

  - Finding the middle is easy using slow/fast pointers.
  - Merging two lists can be done in-place.

- Unlike arrays, quicksort isn't optimal for linked lists.

---

#### 🔄 Dry Run

Input:

```text
List: 4 → 2 → 1 → 3

1. Split into: 4→2 and 1→3
2. Split further: 4, 2, 1, 3
3. Merge sorted: (4, 2) → 2→4; (1, 3) → 1→3
4. Merge final: 1 → 2 → 3 → 4 ✅
```

---

### 🧑‍💻 JavaScript Code (Merge Sort)

```javascript
function sortLinkedList(head) {
  if (!head || !head.next) return head;

  // Step 1: Find middle
  let mid = getMiddle(head);
  let rightHead = mid.next;
  mid.next = null;

  // Step 2: Recursively sort halves
  let left = sortLinkedList(head);
  let right = sortLinkedList(rightHead);

  // Step 3: Merge sorted lists
  return mergeSortedLists(left, right);
}

function getMiddle(head) {
  let slow = head;
  let fast = head;

  while (fast.next && fast.next.next) {
    slow = slow.next;
    fast = fast.next.next;
  }

  return slow;
}

function mergeSortedLists(l1, l2) {
  let dummy = new Node(-1);
  let current = dummy;

  while (l1 && l2) {
    if (l1.value < l2.value) {
      current.next = l1;
      l1 = l1.next;
    } else {
      current.next = l2;
      l2 = l2.next;
    }
    current = current.next;
  }

  current.next = l1 || l2;
  return dummy.next;
}
```

---

### ⏱️ Time & Space Complexity

#### ✅ Time Complexity: `O(n log n)`

- Each split takes `O(log n)` steps.
- Each merge takes `O(n)`.

#### ✅ Space Complexity: `O(log n)` (recursive stack)

- No array used, merge is in-place using pointers.

---

## 11. **Sort a Linked List of 0s, 1s, and 2s (Change Links Only)**

You are given a singly linked list where each node contains data `0`, `1`, or `2`.
**Sort the list in ascending order by rearranging the nodes' links only**, **not the data**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: 1 → 2 → 0 → 1 → 2 → 0
Output: 0 → 0 → 1 → 1 → 2 → 2
```

#### Test Case 2:

```js
Input: 2 → 1 → 2
Output: 1 → 2 → 2
```

#### Test Case 3:

```js
Input: 0 → 0 → 0
Output: 0 → 0 → 0
```

#### Test Case 4:

```js
Input: 1 → 1 → 1
Output: 1 → 1 → 1
```

#### Test Case 5:

```js
Input: 2 → 2 → 1 → 0
Output: 0 → 1 → 2 → 2
```

---

### 💡 Intuition

We’ll use **three dummy head pointers** to create **three separate lists**:

- One for `0s`
- One for `1s`
- One for `2s`

#### Steps:

1. Traverse the original list.
2. Append each node to the appropriate sub-list (`0s`, `1s`, or `2s`).
3. Merge the three sub-lists: `0s → 1s → 2s`.
4. Return the new head of the merged list.

✅ **No data swapping. Only links are changed.**

---

#### 🔄 Dry Run (Test Case 1)

```js
Input: 1 → 2 → 0 → 1 → 2 → 0

0s List: 0 → 0
1s List: 1 → 1
2s List: 2 → 2

Merged: 0 → 0 → 1 → 1 → 2 → 2 ✅
```

---

### 🧑‍💻 JavaScript Code

```javascript
function sortZeroOneTwoList(head) {
  if (!head || !head.next) return head;

  // Dummy heads and tails for 0s, 1s, and 2s
  let zeroD = new Node(0),
    oneD = new Node(0),
    twoD = new Node(0);
  let zero = zeroD,
    one = oneD,
    two = twoD;

  let current = head;

  // Distribute nodes into 0s, 1s, and 2s
  while (current) {
    if (current.value === 0) {
      zero.next = current;
      zero = zero.next;
    } else if (current.value === 1) {
      one.next = current;
      one = one.next;
    } else {
      two.next = current;
      two = two.next;
    }
    current = current.next;
  }

  // Combine lists: 0s → 1s → 2s
  zero.next = oneD.next ? oneD.next : twoD.next;
  one.next = twoD.next;
  two.next = null;

  return zeroD.next;
}
```

---

### 👨‍🔧 Helper Code and Test Cases

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

function buildLinkedList(values) {
  if (!values.length) return null;
  const head = new Node(values[0]);
  let current = head;
  for (let i = 1; i < values.length; i++) {
    current.next = new Node(values[i]);
    current = current.next;
  }
  return head;
}

function printLinkedList(head) {
  const result = [];
  while (head) {
    result.push(head.value);
    head = head.next;
  }
  console.log(result.join(" → ") + " → null");
}

// Tests
printLinkedList(sortZeroOneTwoList(buildLinkedList([1, 2, 0, 1, 2, 0]))); // 0 → 0 → 1 → 1 → 2 → 2 → null
printLinkedList(sortZeroOneTwoList(buildLinkedList([2, 1, 2]))); // 1 → 2 → 2 → null
printLinkedList(sortZeroOneTwoList(buildLinkedList([0, 0, 0]))); // 0 → 0 → 0 → null
printLinkedList(sortZeroOneTwoList(buildLinkedList([1, 1, 1]))); // 1 → 1 → 1 → null
printLinkedList(sortZeroOneTwoList(buildLinkedList([2, 2, 1, 0]))); // 0 → 1 → 2 → 2 → null
```

---

### ⏱️ Time & Space Complexity

#### ✅ Time Complexity: `O(n)`

- One pass to split, another to join.

#### ✅ Space Complexity: `O(1)`

- Rearranging existing nodes; no extra data structures.

---

## 12. **Intersection of Two Singly Linked Lists**

Given the heads of two singly linked lists, return the **node** at which the two lists intersect. If they do not intersect, return `null`.

### 🧪 Test Cases

#### Test Case 1:

```js
List A: 4 → 1 → 8 → 4 → 5
List B: 5 → 6 → 1 → 8 → 4 → 5
Output: Node with value 8
```

#### Test Case 2:

```js
List A: 1 → 9 → 1 → 2 → 4
List B: 3 → 2 → 4
Output: Node with value 2
```

#### Test Case 3:

```js
List A: 2 → 6 → 4
List B: 1 → 5
Output: null
```

---

### 💡 Intuition

The trick is: **if two linked lists intersect, they will have a common tail.**
You need to return the **reference** (not value) of the first common node.

We’ll use a **two-pointer technique** to get this in **O(m + n) time and O(1) space**.

---

### ✅ Optimal Approach (O(m + n) Time, O(1) Space)

#### 📌 Idea:

- Initialize two pointers: `a` at `headA` and `b` at `headB`
- Traverse both lists. When `a` reaches end, redirect it to `headB`. When `b` reaches end, redirect it to `headA`.
- If they intersect, they’ll meet at the intersection point after at most `m + n` steps.
- If not, both will reach `null`.

---

#### 🔄 Dry Run (Example 1)

```
A: 4 → 1 → 8 → 4 → 5
B: 5 → 6 → 1 → 8 → 4 → 5

Pointer A: 4 → 1 → 8 → 4 → 5 → 5 → 6 → 1 → 8
Pointer B: 5 → 6 → 1 → 8 → 4 → 5 → 4 → 1 → 8

They both meet at node with value 8 ✅
```

![](https://lh3.googleusercontent.com/lQGGtwWBXL3Kvl15qC71jpZwvbokF4h963ahFBTd1fAathQjnPSbpxWbCaXv8c3OjJSaWJRot_Ug9WL85_SEPy9ShJxNNCLUFHTWsjS6pQKWGbGoK4Jhpe4Ebgr4VfbCWfOQ0uHC)

### 🧑‍💻 JavaScript Code

```javascript
function getIntersectionNode(headA, headB) {
  if (!headA || !headB) return null;

  let a = headA;
  let b = headB;

  while (a !== b) {
    a = a ? a.next : headB;
    b = b ? b.next : headA;
  }

  return a; // Could be null or intersection node
}
```

---

### 👨‍🔧 Helper Explanation

This works because:

- After the first pass, both pointers traverse equal distances:

  - `a` traverses: lengthA + lengthB
  - `b` traverses: lengthB + lengthA

If an intersection exists, they **sync at the intersection node**.
If not, both reach `null` and return `null`.

---

### ⏱️ Time & Space Complexity

#### ✅ Time: `O(m + n)`

- One pass through both lists

#### ✅ Space: `O(1)`

- No extra space used

---

## 13. **Add 1 to a Number Represented by a Linked List**

You are given the head of a **singly linked list** where each node represents a **digit** of a number. The most significant digit comes first.
**Add 1** to the number and return the **head of the updated linked list**.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: 1 → 2 → 3
Output: 1 → 2 → 4
Explanation: 123 + 1 = 124
```

#### Test Case 2:

```js
Input: 9 → 9 → 9
Output: 1 → 0 → 0 → 0
Explanation: 999 + 1 = 1000
```

#### Test Case 3:

```js
Input: 0;
Output: 1;
```

#### Test Case 4:

```js
Input: 1 → 9 → 9
Output: 2 → 0 → 0
Explanation: 199 + 1 = 200
```

---

### 💡 Intuition

We can **reverse** the linked list, **add 1** starting from the least significant digit (the new head), and then **reverse it back**.

This way, we simulate regular addition with carry like we do with an array.

---

#### 🔄 Dry Run (Test Case 2)

```
Original: 9 → 9 → 9
Reverse: 9 → 9 → 9
Add 1: (carry=1) → 0 → 0 → 0 → carry remains 1 → add node with 1
Reverse back: 1 → 0 → 0 → 0 ✅
```

---

### 🧑‍💻 JavaScript Code

```javascript
function addOne(head) {
  head = reverseList(head); // Step 1: Reverse the list

  let current = head;
  let carry = 1;
  let prev = null;

  while (current) {
    let sum = current.value + carry;
    current.value = sum % 10;
    carry = Math.floor(sum / 10);
    prev = current;
    current = current.next;
  }

  // If carry is left after all nodes
  if (carry > 0) {
    prev.next = new Node(carry);
  }

  return reverseList(head); // Step 2: Reverse back
}

function reverseList(head) {
  let prev = null;
  let current = head;

  while (current) {
    let next = current.next;
    current.next = prev;
    prev = current;
    current = next;
  }

  return prev;
}
```

---

### ⏱️ Time & Space Complexity

#### ✅ Time Complexity: `O(n)`

- One pass to reverse
- One pass to add
- One pass to reverse again

#### ✅ Space Complexity: `O(1)`

- In-place reversal and addition

---

## 14. **Add Two Numbers Represented by Linked Lists**

Given two non-empty linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each node contains a **single digit**.

Add the two numbers and return the **sum as a linked list**, also in reverse order.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input:
l1 = [2, 4, 3]
l2 = [5, 6, 4]

Output: [7, 0, 8]
Explanation: 342 + 465 = 807
```

#### Test Case 2:

```js
Input:
l1 = [9, 9, 9, 9]
l2 = [1]

Output: [0, 0, 0, 0, 1]
Explanation: 9999 + 1 = 10000
```

#### Test Case 3:

```js
Input: l1 = [0];
l2 = [0];

Output: [0];
```

---

### 💡 Intuition

Since the digits are stored in **reverse order**, we can:

1. Traverse both lists simultaneously.
2. Add the corresponding digits, keeping track of the **carry**.
3. If carry remains after traversal, add it as a new node.

---

#### 🔄 Dry Run (Example)

```js
Input: [2, 4, 3], [5, 6, 4]
Add:    2+5 = 7
        4+6 = 10 → put 0, carry 1
        3+4+1 = 8

Output: 7 → 0 → 8 ✅
```

---

### 🧑‍💻 JavaScript Code

```javascript
function addTwoNumbers(l1, l2) {
  let dummy = new Node(0);
  let current = dummy;
  let carry = 0;

  while (l1 || l2 || carry) {
    const val1 = l1 ? l1.value : 0;
    const val2 = l2 ? l2.value : 0;

    let sum = val1 + val2 + carry;
    carry = Math.floor(sum / 10);

    current.next = new Node(sum % 10);
    current = current.next;

    if (l1) l1 = l1.next;
    if (l2) l2 = l2.next;
  }

  return dummy.next;
}
```

---

### ⏱️ Time & Space Complexity

#### ✅ Time Complexity: `O(max(m, n))`

- Traverse each list once

#### ✅ Space Complexity: `O(max(m, n))`

- New list to store result

---

# Medium Problems : Double Linked List

## 1. **Delete All Occurrences of a Key in a Doubly Linked List**

Given the `head` of a **Doubly Linked List (DLL)** and a **key**, delete **all occurrences** of that key in the list.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: 1 ⇄ 2 ⇄ 3 ⇄ 2 ⇄ 4, key = 2
Output: 1 ⇄ 3 ⇄ 4
```

#### Test Case 2:

```js
Input: 2 ⇄ 2 ⇄ 2 ⇄ 2, key = 2
Output: null
```

#### Test Case 3:

```js
Input: 1 ⇄ 2 ⇄ 3 ⇄ 4, key = 5
Output: 1 ⇄ 2 ⇄ 3 ⇄ 4
```

#### Test Case 4:

```js
Input: 5 ⇄ 2 ⇄ 2 ⇄ 6, key = 2
Output: 5 ⇄ 6
```

---

### 💡 Intuition

Doubly linked lists have both `next` and `prev` pointers, so **removal is easier** compared to singly linked lists.

We’ll traverse the list and for every node:

- If `node.data === key`, we remove the node:

  - Adjust `prev.next` and `next.prev` accordingly.
  - If it’s the **head**, move the `head` pointer.

---

#### 🔄 Dry Run

```text
DLL: 1 ⇄ 2 ⇄ 3 ⇄ 2 ⇄ 4
Key: 2

Delete 1st 2: 1 ⇄ 3 ⇄ 2 ⇄ 4
Delete 2nd 2: 1 ⇄ 3 ⇄ 4 ✅
```

---

### 🧑‍💻 JavaScript Code

```javascript
function deleteOccurrences(head, key) {
  let current = head;

  while (current) {
    let nextNode = current.next;

    if (current.value === key) {
      // If node is head
      if (current === head) {
        head = current.next;
        if (head) head.prev = null;
      } else {
        if (current.prev) current.prev.next = current.next;
        if (current.next) current.next.prev = current.prev;
      }
    }

    current = nextNode;
  }

  return head;
}
```

---

### ⏱️ Time & Space Complexity

#### ✅ Time Complexity: `O(n)`

- One full traversal of the list.

#### ✅ Space Complexity: `O(1)`

- In-place deletion; no extra space used.

---

### 📌 Final Notes

- Always check for **head deletions** separately.
- Ensure `prev` and `next` pointers are properly handled — a common interview bug.
- Very useful when working with **LRU Cache**, **edit history**, or **playlist navigation**.

---

Would you like to move on to:

- **Reverse a DLL**
- **Insert at Kth position in DLL**
- Or another linked list problem from your DSA sheet?

## 2. **Find Pairs with Given Sum in Doubly Linked List (DLL)**

You are given the **head of a sorted doubly linked list** and an integer `target`.
Return all **unique pairs of nodes** whose values sum up to the `target`.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: DLL = 1 ⇄ 2 ⇄ 4 ⇄ 5 ⇄ 6 ⇄ 8 ⇄ 9, target = 7
Output: [ [1,6], [2,5] ]
```

#### Test Case 2:

```js
Input: DLL = 1 ⇄ 3 ⇄ 5 ⇄ 7, target = 8
Output: [ [1,7], [3,5] ]
```

#### Test Case 3:

```js
Input: DLL = 1 ⇄ 2 ⇄ 3, target = 6
Output: []
```

---

### 💡 Intuition

We use the **two-pointer technique** — a common strategy for **sorted arrays** — and apply it to the doubly linked list:

1. Start one pointer at the head (`start`), another at the tail (`end`).
2. Check if `start.value + end.value == target`.
3. If sum < target, move `start` forward.
4. If sum > target, move `end` backward.
5. Stop when `start === end` or they cross.

This works efficiently because DLLs allow **both forward and backward** traversal.

---

#### 🔄 Dry Run (Example 1)

```
DLL: 1 ⇄ 2 ⇄ 4 ⇄ 5 ⇄ 6 ⇄ 8 ⇄ 9
Target = 7

start = 1, end = 9 → sum = 10 > 7 → move end ←
start = 1, end = 8 → sum = 9 > 7 → move end ←
start = 1, end = 6 → sum = 7 ✅ [1,6]
start = 2, end = 5 → sum = 7 ✅ [2,5]
start = 4, end = 4 → break ✅
```

---

### 🧑‍💻 JavaScript Code

```javascript
function findPairsWithSumDLL(head, target) {
  if (!head) return [];

  // Step 1: Find tail
  let tail = head;
  while (tail.next) tail = tail.next;

  let start = head;
  let end = tail;
  const result = [];

  // Step 2: Two pointer technique
  while (start !== end && start.prev !== end) {
    const sum = start.value + end.value;

    if (sum === target) {
      result.push([start.value, end.value]);
      start = start.next;
      end = end.prev;
    } else if (sum < target) {
      start = start.next;
    } else {
      end = end.prev;
    }
  }

  return result;
}
```

---

### ⏱️ Time & Space Complexity

#### ✅ Time Complexity: `O(n)`

- One pass using two pointers

#### ✅ Space Complexity: `O(1)`

- No extra memory used except result array

---

## 3. **Remove Duplicates from a Sorted Doubly Linked List**

You are given the **head of a sorted doubly linked list (DLL)**. Your task is to **remove all duplicate nodes**, so that only distinct elements remain.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: 1 ⇄ 2 ⇄ 2 ⇄ 3 ⇄ 4 ⇄ 4 ⇄ 5
Output: 1 ⇄ 2 ⇄ 3 ⇄ 4 ⇄ 5
```

#### Test Case 2:

```js
Input: 1 ⇄ 1 ⇄ 1 ⇄ 1
Output: 1
```

#### Test Case 3:

```js
Input: 1 ⇄ 2 ⇄ 3 ⇄ 4
Output: 1 ⇄ 2 ⇄ 3 ⇄ 4
```

#### Test Case 4:

```js
Input: null;
Output: null;
```

---

### 💡 Intuition

Since the list is **sorted**, all duplicates will be **adjacent**. So, we just need to:

- Traverse the list
- Compare each node with its next
- If both have the same value, remove the `next` node by adjusting pointers

---

#### 🔄 Dry Run

```text
DLL: 1 ⇄ 2 ⇄ 2 ⇄ 3 ⇄ 4 ⇄ 4 ⇄ 5

Step 1: 2 == 2 → remove 2
Step 2: 4 == 4 → remove 4

Result: 1 ⇄ 2 ⇄ 3 ⇄ 4 ⇄ 5 ✅
```

---

### 🧑‍💻 JavaScript Code

```javascript
function removeDuplicatesFromSortedDLL(head) {
  if (!head) return null;

  let current = head;

  while (current && current.next) {
    if (current.value === current.next.value) {
      // Remove duplicate node
      let duplicate = current.next;
      current.next = duplicate.next;
      if (duplicate.next) {
        duplicate.next.prev = current;
      }
    } else {
      current = current.next;
    }
  }

  return head;
}
```

---

### 👨‍🔧 Helper Code and Test Cases

```javascript
class DLLNode {
  constructor(value) {
    this.value = value;
    this.next = null;
    this.prev = null;
  }
}

function buildDLL(values) {
  if (!values.length) return null;
  let head = new DLLNode(values[0]);
  let current = head;
  for (let i = 1; i < values.length; i++) {
    const newNode = new DLLNode(values[i]);
    current.next = newNode;
    newNode.prev = current;
    current = newNode;
  }
  return head;
}

function printDLL(head) {
  const result = [];
  let tail = null;
  while (head) {
    result.push(head.value);
    if (head.next === null) tail = head;
    head = head.next;
  }
  console.log("Forward: " + result.join(" ⇄ "));
}
```

#### ✅ Run Test Cases

```javascript
let head = buildDLL([1, 2, 2, 3, 4, 4, 5]);
head = removeDuplicatesFromSortedDLL(head);
printDLL(head); // Forward: 1 ⇄ 2 ⇄ 3 ⇄ 4 ⇄ 5

head = buildDLL([1, 1, 1, 1]);
head = removeDuplicatesFromSortedDLL(head);
printDLL(head); // Forward: 1

head = buildDLL([1, 2, 3, 4]);
head = removeDuplicatesFromSortedDLL(head);
printDLL(head); // Forward: 1 ⇄ 2 ⇄ 3 ⇄ 4
```

---

### ⏱️ Time & Space Complexity

#### ✅ Time Complexity: `O(n)`

- One traversal through the list

#### ✅ Space Complexity: `O(1)`

- In-place operations

---

# Hard Problems

## 1. **Reverse a Linked List in Groups of Size K**

Given a singly linked list, reverse the nodes of the list **k at a time** and return the modified list.

If the number of nodes is **not a multiple of k**, then leave the remaining nodes as-is.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8, k = 3
Output: 3 → 2 → 1 → 6 → 5 → 4 → 7 → 8
```

#### Test Case 2:

```js
Input: 1 → 2 → 3 → 4 → 5, k = 2
Output: 2 → 1 → 4 → 3 → 5
```

#### Test Case 3:

```js
Input: 1 → 2 → 3, k = 1
Output: 1 → 2 → 3
```

#### Test Case 4:

```js
Input: 1 → 2 → 3 → 4 → 5, k = 5
Output: 5 → 4 → 3 → 2 → 1
```

---

### 💡 Intuition

To reverse the list in groups of `k`:

1. Reverse the **first k nodes**.
2. Recursively call the function for the **next group**.
3. Connect the reversed group with the result of the recursive call.

**Base Condition**: If less than `k` nodes are left, return the head as-is.

---

#### 🔄 Dry Run (Example 1)

```text
Original: 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8, k = 3
Group 1: 3 → 2 → 1
Group 2: 6 → 5 → 4
Remaining: 7 → 8 (less than k) → leave as-is
Final: 3 → 2 → 1 → 6 → 5 → 4 → 7 → 8 ✅
```

---

### 🧑‍💻 JavaScript Code

```javascript
function reverseInGroups(head, k) {
  if (!head || k === 1) return head;

  let current = head;
  let prev = null;
  let next = null;

  // Step 1: Check if we have at least k nodes
  let count = 0;
  let temp = head;
  while (count < k && temp) {
    temp = temp.next;
    count++;
  }

  if (count < k) return head; // Not enough nodes to reverse

  // Step 2: Reverse k nodes
  count = 0;
  while (count < k && current) {
    next = current.next;
    current.next = prev;
    prev = current;
    current = next;
    count++;
  }

  // Step 3: Recursively call for the remaining list
  if (next) {
    head.next = reverseInGroups(next, k);
  }

  return prev;
}
```

---

### ⏱️ Time & Space Complexity

#### ✅ Time Complexity: `O(n)`

- Each node is visited once.

#### ✅ Space Complexity:

- **Recursive stack**: `O(n/k)` due to recursion
- **Iterative version** possible with `O(1)` space.

---

## 2. **Rotate a Linked List to the Right by K Places**

Given the head of a singly linked list, rotate the list to the right by `k` places.

---

### 🧪 Test Cases

#### Test Case 1:

```js
Input: (head = [1, 2, 3, 4, 5]), (k = 2);
Output: [4, 5, 1, 2, 3];
```

#### Test Case 2:

```js
Input: (head = [0, 1, 2]), (k = 4);
Output: [2, 0, 1];
```

#### Test Case 3:

```js
Input: (head = []), (k = 5);
Output: [];
```

#### Test Case 4:

```js
Input: (head = [1, 2]), (k = 0);
Output: [1, 2];
```

---

### 💡 Intuition

To rotate right by `k` places:

1. **Convert the list into a circular linked list**.
2. **Find the new head** after `length - (k % length)` steps.
3. **Break the circle** to make it a proper list again.

---

#### 🔄 Dry Run

```text
Input: 1 → 2 → 3 → 4 → 5, k = 2

Step 1: Make it circular: 1 → 2 → 3 → 4 → 5 → (points back to 1)

List length = 5
New head = (5 - (2 % 5)) = 3 steps ahead → Node 4 becomes new head
Break the circle after node 3

Result: 4 → 5 → 1 → 2 → 3 ✅
```

---

### 🧑‍💻 JavaScript Code

```javascript
function rotateRight(head, k) {
  if (!head || !head.next || k === 0) return head;

  // Step 1: Get the length and last node
  let length = 1;
  let tail = head;
  while (tail.next) {
    tail = tail.next;
    length++;
  }

  // Step 2: Make it a circular linked list
  tail.next = head;

  // Step 3: Find new tail (length - k % length - 1) and new head
  k = k % length;
  let stepsToNewTail = length - k;
  let newTail = head;
  for (let i = 1; i < stepsToNewTail; i++) {
    newTail = newTail.next;
  }

  const newHead = newTail.next;
  newTail.next = null; // Break the cycle

  return newHead;
}
```

---

### ⏱️ Time & Space Complexity

#### ✅ Time Complexity: `O(n)`

- One pass to calculate length, one pass to move to new tail

#### ✅ Space Complexity: `O(1)`

- Only pointers used; no extra storage

---

## 3. **Flatten a Multilevel Linked List into a Single Sorted Linked List**

---

### 📘 Problem Statement

Given a **linked list** where each node contains:

- `next` pointer (to the next node in the top-level list)
- `child` pointer (to the head of a sorted linked list)

Flatten this multilevel structure into a **single-level sorted linked list**, using only the `child` pointer to represent the final list.

---

### 🧪 Test Cases

#### Test Case 1:

```
Top-level list:       5 → 10 → 19 → 28
                       ↓   ↓    ↓    ↓
                       7   20   22   35
                       ↓        ↓    ↓
                       8        50   40
                       ↓             ↓
                       30            45

Output:
5 → 7 → 8 → 10 → 19 → 20 → 22 → 28 → 30 → 35 → 40 → 45 → 50
```

---

### 💡 Intuition

This is essentially a **merge k sorted lists** problem.

Each `node`'s `child` list is sorted. So, we:

- Flatten the list **recursively**
- Use a helper function to **merge two sorted lists** (like in Merge Sort)

---

### 🔄 Approach

1. If head is `null` or there is no `next`, return head.
2. Recursively flatten the `next` list.
3. Merge the current node’s `child` list with the flattened `next` list.
4. Return the merged list.

> The final list will use only the `child` pointer.

---

### 🧑‍💻 JavaScript Code

```javascript
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
    this.child = null;
  }
}

// Merge two sorted lists using child pointers
function merge(a, b) {
  if (!a) return b;
  if (!b) return a;

  let result;
  if (a.val < b.val) {
    result = a;
    result.child = merge(a.child, b);
  } else {
    result = b;
    result.child = merge(a, b.child);
  }

  result.next = null; // Flattening to one level
  return result;
}

// Main function to flatten list
function flatten(head) {
  if (!head || !head.next) return head;

  // Recursively flatten the next list
  head.next = flatten(head.next);

  // Merge current list with flattened next list
  head = merge(head, head.next);

  return head;
}
```

---

### 🖼️ Visualization

#### Input:

```
Head: 5 → 10 → 19
        ↓     ↓
        7     22
        ↓
        8
```

#### After Flattening:

```
5 → 7 → 8 → 10 → 19 → 22 → null
```

---

### ⏱️ Time & Space Complexity

#### ✅ Time Complexity: `O(N log K)`

- N = total number of nodes
- K = number of top-level `next` nodes
- Every merge is `O(n)`, and we do `log K` merges recursively

#### ✅ Space Complexity: `O(log K)`

- Recursion depth

---

## 4. **Clone a Linked List with `next` and `random` Pointers**

### 📘 Problem Statement

You're given a linked list where each node has two pointers:

- `next` — points to the next node
- `random` — points to any node in the list (or `null`)

Your task is to **create a deep copy** of this linked list — cloning **both** the `next` and `random` pointers correctly.

---

### 🧪 Test Cases

#### Test Case 1:

```
Original:
Node: 1 → 2 → 3
Random: 1 → 3, 2 → 1, 3 → 2

Output (clone):
1' → 2' → 3'
Random: 1' → 3', 2' → 1', 3' → 2'
```

#### Test Case 2:

```
Input: head = null
Output: null
```

---

### 💡 Intuition

To **clone** such a structure, we need to:

1. Clone each node and insert it just after the original.
2. Set the cloned node’s `random` using original's `random`.
3. Detach the cloned list from the original.

This **interleaving approach** avoids using extra memory for mapping.

---

#### 🔄 Dry Run

```
Original:
1 → 2 → 3
Random:
1 → 3
2 → 1
3 → 2

Step 1: Interleave clones:
1 → 1' → 2 → 2' → 3 → 3'

Step 2: Set random pointers:
1'.random = 1.random.next = 3'
2'.random = 2.random.next = 1'
3'.random = 3.random.next = 2'

Step 3: Separate cloned list:
Cloned: 1' → 2' → 3'
```

---

### 🧑‍💻 JavaScript Code

```javascript
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
    this.random = null;
  }
}

function cloneLinkedList(head) {
  if (!head) return null;

  // Step 1: Clone nodes and insert them next to original nodes
  let current = head;
  while (current) {
    const newNode = new Node(current.val);
    newNode.next = current.next;
    current.next = newNode;
    current = newNode.next;
  }

  // Step 2: Assign random pointers to clone nodes
  current = head;
  while (current) {
    if (current.random) {
      current.next.random = current.random.next;
    }
    current = current.next.next;
  }

  // Step 3: Separate the original and clone lists
  current = head;
  const cloneHead = head.next;
  while (current) {
    const clone = current.next;
    current.next = clone.next;
    if (clone.next) {
      clone.next = clone.next.next;
    }
    current = current.next;
  }

  return cloneHead;
}
```

---

### ⏱️ Time & Space Complexity

#### ✅ Time Complexity: `O(n)`

- We visit each node 3 times.

#### ✅ Space Complexity: `O(1)`

- No extra data structure used (no hashmap).

---
