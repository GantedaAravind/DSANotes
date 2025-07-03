# 📚 **Stack**

## 📌 **What is a Stack?**

A **stack** is a **linear data structure** that follows the **LIFO (Last In First Out)** principle. The last element added is the first one to be removed.

> **Real-life Examples**:
>
> - Pile of plates
> - Undo feature in editors

---

## 📊 **Stack Visualization**

![Stack](https://cdn.programiz.com/sites/tutorial2program/files/stack.png)

---

## 🔧 **Basic Stack Operations**

| Operation          | Description                                 |
| ------------------ | ------------------------------------------- |
| `push(x)`          | Add element `x` to the top of the stack     |
| `pop()`            | Remove and return the top element           |
| `peek()` / `top()` | Return the top element without removing it  |
| `isEmpty()`        | Returns `true` if stack is empty            |
| `size()`           | Returns the number of elements in the stack |

---

## 🧠 **Why Use Stack?**

- Reversing a string
- Expression evaluation and conversion
- Backtracking (e.g., maze, recursion, tree traversal)
- Undo/Redo operations

---

## 🏗️ **Implementation of Stack**

### ✅ Using JavaScript Array:

```js
class Stack {
  constructor() {
    this.items = [];
  }

  // Add element to stack
  push(element) {
    this.items.push(element);
  }

  // Remove and return top element
  pop() {
    if (this.isEmpty()) return "Stack Underflow";
    return this.items.pop();
  }

  // Peek top element
  peek() {
    return this.items[this.items.length - 1];
  }

  // Check if stack is empty
  isEmpty() {
    return this.items.length === 0;
  }

  // Return size
  size() {
    return this.items.length;
  }

  // Display stack
  printStack() {
    console.log(this.items.join(" -> "));
  }
}
```

---

## 🧪 **Dry Run: Push and Pop**

```js
const stack = new Stack();
stack.push(10); // [10]
stack.push(20); // [10, 20]
stack.pop(); // [10] → returns 20
```

---

## 🔁 **Stack in Recursion**

Every time a function is called, the **call stack** pushes the function call. When the function returns, it is popped off the stack.

---

## 🔁 **Stack Using Linked List**

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class StackLL {
  constructor() {
    this.top = null;
    this.length = 0;
  }

  push(value) {
    const newNode = new Node(value);
    newNode.next = this.top;
    this.top = newNode;
    this.length++;
  }

  pop() {
    if (!this.top) return "Underflow";
    const popped = this.top;
    this.top = this.top.next;
    this.length--;
    return popped.value;
  }

  peek() {
    return this.top?.value;
  }

  isEmpty() {
    return this.top === null;
  }
}
```

---

## 🧠 **Time and Space Complexity**

| Operation | Time Complexity |
| --------- | --------------- |
| Push      | O(1)            |
| Pop       | O(1)            |
| Peek      | O(1)            |
| isEmpty   | O(1)            |

---

# 📚 **Queue**

## 📌 **What is a Queue?**

A **Queue** is a **linear data structure** that follows the **FIFO (First In First Out)** principle. The first element inserted is the first one to be removed.

> **Real-life Examples**:
>
> - Waiting line at a ticket counter
> - Print queue in printers
> - Task scheduling

---

## 📊 **Queue Visualization**

![Queue](https://miro.medium.com/v2/resize:fit:1001/0*7fDsAPlAoFEca0sW.png)

- **Front**: Element to be removed first
- **Rear**: Element added last

---

## 🔧 **Basic Queue Operations**

| Operation    | Description                         |
| ------------ | ----------------------------------- |
| `enqueue(x)` | Add element `x` to the rear         |
| `dequeue()`  | Remove and return the front element |
| `peek()`     | View the front element              |
| `isEmpty()`  | Check if queue is empty             |
| `size()`     | Number of elements in the queue     |

---

## 🧠 **Why Use Queue?**

- Task scheduling
- Breadth-first search (BFS)
- Buffer handling (keyboard, IO)
- Real-time streaming

---

## 🏗️ **Queue Implementation**

### ✅ Using JavaScript Array

```js
class Queue {
  constructor() {
    this.items = [];
  }

  enqueue(element) {
    this.items.push(element);
  }

  dequeue() {
    if (this.isEmpty()) return "Underflow";
    return this.items.shift();
  }

  peek() {
    return this.items[0];
  }

  isEmpty() {
    return this.items.length === 0;
  }

  size() {
    return this.items.length;
  }

  printQueue() {
    console.log(this.items.join(" <- "));
  }
}
```

---

## 🧪 **Dry Run Example**

```js
const q = new Queue();
q.enqueue(10); // [10]
q.enqueue(20); // [10, 20]
q.dequeue(); // [20] → returns 10
```

---

## 🧵 **Queue Using Linked List**

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedQueue {
  constructor() {
    this.front = null;
    this.rear = null;
  }

  enqueue(value) {
    const newNode = new Node(value);
    if (this.rear) {
      this.rear.next = newNode;
    }
    this.rear = newNode;
    if (!this.front) this.front = newNode;
  }

  dequeue() {
    if (!this.front) return "Underflow";
    const val = this.front.value;
    this.front = this.front.next;
    if (!this.front) this.rear = null;
    return val;
  }

  peek() {
    return this.front?.value;
  }

  isEmpty() {
    return this.front === null;
  }
}
```

---

## 🔁 **Types of Queues**

| Type               | Description                                      |
| ------------------ | ------------------------------------------------ |
| **Simple Queue**   | Basic FIFO queue                                 |
| **Circular Queue** | Connects rear to front to use space efficiently  |
| **Deque**          | Double-ended queue; insert/delete from both ends |
| **Priority Queue** | Elements served based on priority, not arrival   |

---

## 🧠 **Time & Space Complexity**

| Operation | Time Complexity                         |
| --------- | --------------------------------------- |
| Enqueue   | O(1) (amortized for array)              |
| Dequeue   | O(1) (linked list) / O(n) (array shift) |
| Peek      | O(1)                                    |
| isEmpty   | O(1)                                    |

---

# **Learning**

## 1. **Check For Balanced Parentheses**

Check if an expression has balanced parentheses:
Each opening bracket must be closed by the same type of bracket in the correct order.

---

### 🧪 **Test Cases**

#### Test Case 1:

```js
Input: "({[]})";
Output: true;
```

#### Test Case 2:

```js
Input: "([)]";
Output: false;
```

#### Test Case 3:

```js
Input: "{[()()]}";
Output: true;
```

#### Test Case 4:

```js
Input: "(()";
Output: false;
```

---

### 💡 **Intuition**

- Push opening brackets onto the stack.
- For every closing bracket:

  - Check if the stack is empty → unbalanced.
  - Pop the top of the stack and check if it matches the closing bracket.

- At the end, if the stack is empty → balanced.

---

### 🔁 **Dry Run**

Input: `"({[]})"`

- Stack: \[]
- Read `(` → push → `[`
- Read `{` → push → `[(, {]`
- Read `[` → push → `[(, {, []`
- Read `]` → pop `[` ✔
- Read `}` → pop `{` ✔
- Read `)` → pop `(` ✔
- Stack is empty ✅ → Balanced

---

### ✅ **JavaScript Code**

```js
function isBalanced(expression) {
  const stack = [];
  const map = {
    ")": "(",
    "}": "{",
    "]": "[",
  };

  for (let char of expression) {
    if (char === "(" || char === "{" || char === "[") {
      stack.push(char);
    } else if (char === ")" || char === "}" || char === "]") {
      if (stack.pop() !== map[char]) {
        return false;
      }
    }
  }

  return stack.length === 0;
}
```

---

### ⏱️ **Time and Space Complexity**

- **Time Complexity:** O(n)
- **Space Complexity:** O(n) (for the stack)

---

## 🧱 **2. MinStack – Design a Stack Supporting `getMin()` in O(1)**

### 📘 Problem Statement

Design a stack that supports the following operations in **O(1)** time:

- `MinStack()` — Initializes the stack.
- `void push(val)` — Pushes `val` onto the stack.
- `void pop()` — Removes the top element.
- `int top()` — Returns the top element.
- `int getMin()` — Returns the minimum element in the stack.

**Constraints:**

- Only non-empty stack operations will be called for `top()`, `pop()`, and `getMin()`.
- `-2^31 <= val <= 2^31 - 1`
- Up to `3 * 10^4` operations.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: ["MinStack", "push", "push", "push", "getMin", "pop", "top", "getMin"][
  ([], [-2], [0], [-3], [], [], [], [])
];

Output: [null, null, null, null, -3, null, 0, -2];
```

---

### 💡 Intuition

To retrieve the **minimum element in constant time**, we need to store more than just the element values.
Maintain an **auxiliary stack** (`minStack`) that keeps track of the minimum element **up to each level** of the main stack.

- When pushing, compare the new value with the current `min()` and push the new min to `minStack`.
- When popping, also pop from `minStack`.

This ensures `getMin()` always returns the top of `minStack`.

---

### 🔄 Dry Run

Let's walk through:

```js
push(-2)  → stack = [-2], minStack = [-2]
push(0)   → stack = [-2, 0], minStack = [-2, -2]
push(-3)  → stack = [-2, 0, -3], minStack = [-2, -2, -3]
getMin()  → top of minStack = -3
pop()     → stack = [-2, 0], minStack = [-2, -2]
top()     → top of stack = 0
getMin()  → top of minStack = -2
```

---

### 🧑‍💻 JavaScript Code (Optimized Solution)

```js
class MinStack {
  constructor() {
    this.stack = [];
    this.minStack = [];
  }

  push(val) {
    this.stack.push(val);
    const min = this.minStack.length === 0 ? val : Math.min(val, this.getMin());
    this.minStack.push(min);
  }

  pop() {
    this.stack.pop();
    this.minStack.pop();
  }

  top() {
    return this.stack[this.stack.length - 1];
  }

  getMin() {
    return this.minStack[this.minStack.length - 1];
  }
}

// ✅ Test Example
const minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
console.log(minStack.getMin()); // -3
minStack.pop();
console.log(minStack.top()); // 0
console.log(minStack.getMin()); // -2
```

---

### ⏱️ Time & Space Complexity

| Operation | Time Complexity | Space Complexity |
| --------- | --------------- | ---------------- |
| `push`    | O(1)            | O(1) per op      |
| `pop`     | O(1)            | O(1)             |
| `top`     | O(1)            | O(1)             |
| `getMin`  | O(1)            | O(1)             |
| Overall   | ✅ Optimal      | Uses two stacks  |

---

# **Prefix, Infix, PostFix Conversion Problems**

## 📘 ** Introduction to Expressions in Programming**

Expressions are combinations of:

- **Operands** (like numbers or variables)
- **Operators** (like `+`, `-`, `*`, `/`)

There are **three common notations** for writing expressions:

- **Infix**: `A + B`
- **Prefix** (Polish Notation): `+ A B`
- **Postfix** (Reverse Polish Notation): `A B +`

---

### 🔹 ** Infix Notation**

### ✅ **Definition:**

The operator is written **between** the operands.

### 🧾 **Example:**

```
A + B
(3 * 4) + 5
```

### ✅ **Pros:**

- Natural and easy to read (used in most languages).

### ❌ **Cons:**

- Needs **parentheses** to specify the order of evaluation.
- Requires **operator precedence rules** to evaluate correctly.

### 🧠 **Evaluation:**

To evaluate infix:

- Use **precedence** and **associativity**
- Use **stacks** or convert to postfix for easier computation

---

### 🔹 ** Prefix Notation (Polish Notation)**

### ✅ **Definition:**

The operator is written **before** the operands.

### 🧾 **Example:**

```
+ A B
* + A B C
+ * A B - C D
```

### 👇 In Infix:

```
A + B
(A + B) * C
(A * B) + (C - D)
```

### ✅ **Pros:**

- No need for parentheses
- Easy to parse (compilers use this internally)

### ❌ **Cons:**

- Less readable for humans

---

### 🧠 **Evaluation (using stack):**

- Traverse the expression **from right to left**
- If operand → push it on stack
- If operator → pop 2 operands, apply operator, push result

---

### 🔹 ** Postfix Notation (Reverse Polish Notation)**

### ✅ **Definition:**

The operator is written **after** the operands.

### 🧾 **Example:**

```
A B +
A B + C *
A B * C D - +
```

### 👇 In Infix:

```
A + B
(A + B) * C
(A * B) + (C - D)
```

### ✅ **Pros:**

- No parentheses needed
- Efficient for **stack-based evaluation**
- Easy to compute (used in calculators)

---

### 🧠 **Evaluation (using stack):**

- Traverse expression **left to right**
- If operand → push on stack
- If operator → pop 2 operands, apply operator, push result

---

## 🔢 **1. Infix to Postfix Conversion using Stack**

### 📘 Problem Statement

Convert a given **infix expression** (e.g., `a + b * c`) into a **postfix expression** (also known as Reverse Polish Notation, e.g., `a b c * +`) using a stack.

**You must:**

- Handle operator precedence (`*`, `/` > `+`, `-`)
- Handle left-to-right associativity
- Optionally handle parentheses `(` and `)`

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: "a + b * c";
Output: "a b c * +";
```

#### ✅ Test Case 2:

```js
Input: "(a + b) * c";
Output: "a b + c *";
```

#### ✅ Test Case 3:

```js
Input: "a + b + c";
Output: "a b + c +";
```

#### ✅ Test Case 4:

```js
Input: "a * (b + c) / d";
Output: "a b c + * d /";
```

---

### 💡 Intuition

Use a **stack** to keep track of operators. When you encounter:

- **Operand** → directly append to result
- **Operator** → pop from stack to result while stack has operators of higher or equal precedence
- **Left parenthesis `(`** → push to stack
- **Right parenthesis `)`** → pop and append until matching `(` is found

---

### ⚙️ Precedence Rules

| Operator | Precedence | Associativity |
| -------- | ---------- | ------------- |
| `+` `-`  | 1          | Left          |
| `*` `/`  | 2          | Left          |
| `^`      | 3          | **Right**     |

---

### 🔄 Dry Run

For expression: `"a + b * c"`

```text
Tokens: ['a', '+', 'b', '*', 'c']

Result: []
Stack: []

→ 'a' is operand → Result: [a]
→ '+' is operator → Stack: [+]
→ 'b' is operand → Result: [a, b]
→ '*' is operator → precedence of '*' > '+' → push '*' → Stack: [+, *]
→ 'c' is operand → Result: [a, b, c]

Now pop stack: → Result: [a, b, c, *, +]
```

Output: `a b c * +`

---

### 🧑‍💻 JavaScript Code

```js
function infixToPostfix(expression) {
  const precedence = {
    "+": 1,
    "-": 1,
    "*": 2,
    "/": 2,
    "^": 3,
  };

  const isLeftAssociative = (op) => op !== "^";
  const stack = [];
  const output = [];
  const tokens = expression.replace(/\s+/g, "").split("");

  for (let token of tokens) {
    if (/[a-zA-Z0-9]/.test(token)) {
      output.push(token);
    } else if (token === "(") {
      stack.push(token);
    } else if (token === ")") {
      while (stack.length && stack[stack.length - 1] !== "(") {
        output.push(stack.pop());
      }
      stack.pop(); // pop '('
    } else {
      while (
        stack.length &&
        precedence[stack[stack.length - 1]] >= precedence[token] &&
        isLeftAssociative(token)
      ) {
        output.push(stack.pop());
      }
      stack.push(token);
    }
  }

  while (stack.length) {
    output.push(stack.pop());
  }

  return output.join(" ");
}

// ✅ Test
console.log(infixToPostfix("a + b * c")); // a b c * +
console.log(infixToPostfix("(a + b) * c")); // a b + c *
console.log(infixToPostfix("a * (b + c) / d")); // a b c + * d /
```

---

### ⏱️ Time & Space Complexity

- **Time:** O(n), where n is the number of characters
- **Space:** O(n), for the operator stack and output list

---

## 🔢 **2. Prefix to Infix Conversion using Stack**

### 📘 Problem Statement

Given a **prefix expression** (e.g., `+AB`), convert it into an equivalent **infix expression** (e.g., `A + B`).

You must:

- Use a **stack**
- Convert in **O(n)** time
- Ensure proper **bracketed grouping** for multi-operator expressions

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: "+AB";
Output: "(A + B)";
```

#### ✅ Test Case 2:

```js
Input: "*+AB-CD";
Output: "((A + B) * (C - D))";
```

#### ✅ Test Case 3:

```js
Input: "+*AB/CD^EF";
Output: "((A * B) + (C / (E ^ F)))";
```

---

### 💡 Intuition

In a **prefix expression**, the operator comes **before** its operands. To convert to infix:

1. **Traverse the prefix expression from right to left**
2. If the current token is an **operand**, push it onto the stack
3. If the token is an **operator**:

   - Pop two operands from the stack
   - Combine them with the operator and wrap in parentheses: `"(left op right)"`
   - Push the result back on the stack

4. After processing all tokens, the stack will have the final infix expression

---

### 🔄 Dry Run

Let’s take: `*+AB-CD`

Step-by-step (right to left):

```text
Stack: []

→ 'D' → operand → push → ["D"]
→ 'C' → operand → push → ["D", "C"]
→ '-' → operator → pop C, D → "(C - D)" → push → ["(C - D)"]

→ 'B' → operand → push → ["(C - D)", "B"]
→ 'A' → operand → push → ["(C - D)", "B", "A"]
→ '+' → operator → pop A, B → "(A + B)" → push → ["(C - D)", "(A + B)"]

→ '*' → operator → pop (A + B), (C - D) → "((A + B) * (C - D))"
```

✅ Output: `"((A + B) * (C - D))"`

---

### 🧑‍💻 JavaScript Code

```js
function prefixToInfix(prefix) {
  const stack = [];
  const isOperator = (ch) => ["+", "-", "*", "/", "^"].includes(ch);

  for (let i = prefix.length - 1; i >= 0; i--) {
    const ch = prefix[i];

    if (!isOperator(ch)) {
      stack.push(ch);
    } else {
      const op1 = stack.pop();
      const op2 = stack.pop();
      const expr = `(${op1} ${ch} ${op2})`;
      stack.push(expr);
    }
  }

  return stack.pop();
}

// ✅ Test
console.log(prefixToInfix("+AB")); // (A + B)
console.log(prefixToInfix("*+AB-CD")); // ((A + B) * (C - D))
console.log(prefixToInfix("+*AB/CD^EF")); // ((A * B) + (C / (E ^ F)))
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(n)       |

---

## 🔢 **3. Prefix to Postfix Conversion using Stack**

### 📘 Problem Statement

Convert a given **prefix expression** (e.g., `*+AB-CD`) into its equivalent **postfix expression** (e.g., `AB+CD-*`).

You must:

- Use a **stack-based approach**
- Traverse the prefix from **right to left**
- Return the correct postfix expression **without brackets**

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: "+AB";
Output: "AB+";
```

#### ✅ Test Case 2:

```js
Input: "*+AB-CD";
Output: "AB+CD-*";
```

#### ✅ Test Case 3:

```js
Input: "+*AB/CD^EF";
Output: "AB*CEF^/+";
```

---

### 💡 Intuition

In **prefix**, the operator comes **before** operands.
In **postfix**, the operator comes **after** operands.

To convert:

1. **Traverse prefix right to left**
2. If operand → push to stack
3. If operator:

   - Pop two operands
   - Combine in the order: **operand1 + operand2 + operator**
   - Push result back on stack

4. Final result will be the only element left in the stack

---

### 🔄 Dry Run

For `*+AB-CD`

```text
Stack: []

→ 'D' → push → ["D"]
→ 'C' → push → ["D", "C"]
→ '-' → pop(C, D) → "CD-" → push → ["CD-"]

→ 'B' → push → ["CD-", "B"]
→ 'A' → push → ["CD-", "B", "A"]
→ '+' → pop(A, B) → "AB+" → push → ["CD-", "AB+"]

→ '*' → pop(AB+, CD-) → "AB+CD-*" → push → ["AB+CD-*"]
```

✅ Output: `"AB+CD-*"`

---

### 🧑‍💻 JavaScript Code

```js
function prefixToPostfix(prefix) {
  const stack = [];
  const isOperator = (ch) => ["+", "-", "*", "/", "^"].includes(ch);

  for (let i = prefix.length - 1; i >= 0; i--) {
    const ch = prefix[i];

    if (!isOperator(ch)) {
      stack.push(ch);
    } else {
      const op1 = stack.pop();
      const op2 = stack.pop();
      const newExpr = op1 + op2 + ch;
      stack.push(newExpr);
    }
  }

  return stack.pop();
}

// ✅ Test
console.log(prefixToPostfix("+AB")); // AB+
console.log(prefixToPostfix("*+AB-CD")); // AB+CD-*
console.log(prefixToPostfix("+*AB/CD^EF")); // AB*CEF^/+
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(n)       |

---

## 🔢 **4. Postfix to Prefix Conversion using Stack**

### 📘 Problem Statement

Convert a given **postfix expression** (e.g., `AB+CD-*`) into an equivalent **prefix expression** (e.g., `*+AB-CD`).

You must:

- Use a **stack-based approach**
- Traverse the postfix from **left to right**
- Return the final expression in **prefix format** (operator before operands)

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: "AB+";
Output: "+AB";
```

#### ✅ Test Case 2:

```js
Input: "AB+CD-*";
Output: "*+AB-CD";
```

#### ✅ Test Case 3:

```js
Input: "AB*CEF^/+";
Output: "+*AB/C^EF";
```

---

### 💡 Intuition

In **postfix**, the operator comes **after** the operands.
In **prefix**, the operator comes **before** the operands.

To convert:

1. **Traverse postfix from left to right**
2. If the character is an **operand**, push it to the stack
3. If it’s an **operator**:

   - Pop two operands from the stack
   - Combine into: `operator + operand1 + operand2`
   - Push this new expression back to the stack

4. Final stack item is the result

---

### 🔄 Dry Run

Expression: `"AB+CD-*"`

```text
Stack: []

→ 'A' → push → ["A"]
→ 'B' → push → ["A", "B"]
→ '+' → pop A, B → "+AB" → push → ["+AB"]

→ 'C' → push → ["+AB", "C"]
→ 'D' → push → ["+AB", "C", "D"]
→ '-' → pop C, D → "-CD" → push → ["+AB", "-CD"]

→ '*' → pop +AB, -CD → "*+AB-CD" → push → ["*+AB-CD"]
```

✅ Output: `"*+AB-CD"`

---

### 🧑‍💻 JavaScript Code

```js
function postfixToPrefix(postfix) {
  const stack = [];
  const isOperator = (ch) => ["+", "-", "*", "/", "^"].includes(ch);

  for (let ch of postfix) {
    if (!isOperator(ch)) {
      stack.push(ch);
    } else {
      const op2 = stack.pop();
      const op1 = stack.pop();
      const newExpr = ch + op1 + op2;
      stack.push(newExpr);
    }
  }

  return stack.pop();
}

// ✅ Test
console.log(postfixToPrefix("AB+")); // +AB
console.log(postfixToPrefix("AB+CD-*")); // *+AB-CD
console.log(postfixToPrefix("AB*CEF^/+")); // +*AB/C^EF
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(n)       |

---

## 🔢 **5. Postfix to Infix Conversion using Stack**

### 📘 Problem Statement

Given a **postfix expression** (e.g., `AB+`), convert it to its corresponding **infix expression** (e.g., `(A + B)`).

**You must:**

- Use a **stack**
- Maintain **correct grouping** with parentheses
- Handle basic operators: `+`, `-`, `*`, `/`, `^`

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: "AB+";
Output: "(A + B)";
```

#### ✅ Test Case 2:

```js
Input: "AB+CD-*";
Output: "((A + B) * (C - D))";
```

#### ✅ Test Case 3:

```js
Input: "AB*CEF^/+";
Output: "((A * B) + (C / (E ^ F)))";
```

---

### 💡 Intuition

In **postfix**, operators follow their operands.
To convert to **infix**, you reverse this and **wrap each sub-expression in parentheses**.

Use a stack:

1. Traverse the postfix string **left to right**
2. If operand → push to stack
3. If operator:

   - Pop two operands from stack
   - Format: `(operand1 operator operand2)`
   - Push result back on stack

4. Final item in stack is the full infix expression

---

### 🔄 Dry Run

Expression: `"AB+CD-*"`

```text
Stack: []

→ 'A' → push → ["A"]
→ 'B' → push → ["A", "B"]
→ '+' → pop A, B → "(A + B)" → push → ["(A + B)"]

→ 'C' → push → ["(A + B)", "C"]
→ 'D' → push → ["(A + B)", "C", "D"]
→ '-' → pop C, D → "(C - D)" → push → ["(A + B)", "(C - D)"]

→ '*' → pop (A + B), (C - D) → "((A + B) * (C - D))"
```

✅ Output: `"((A + B) * (C - D))"`

---

### 🧑‍💻 JavaScript Code

```js
function postfixToInfix(postfix) {
  const stack = [];
  const isOperator = (ch) => ["+", "-", "*", "/", "^"].includes(ch);

  for (let ch of postfix) {
    if (!isOperator(ch)) {
      stack.push(ch);
    } else {
      const op2 = stack.pop();
      const op1 = stack.pop();
      const expr = `(${op1} ${ch} ${op2})`;
      stack.push(expr);
    }
  }

  return stack.pop();
}

// ✅ Test
console.log(postfixToInfix("AB+")); // (A + B)
console.log(postfixToInfix("AB+CD-*")); // ((A + B) * (C - D))
console.log(postfixToInfix("AB*CEF^/+")); // ((A * B) + (C / (E ^ F)))
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(n)       |

---

## 🔢 **6. Infix to Prefix Conversion using Stack**

### 📘 Problem Statement

Given an **infix expression** (e.g., `(A + B) * (C - D)`), convert it into its corresponding **prefix expression** (e.g., `*+AB-CD`).

You must:

- Use a **stack-based** algorithm
- Maintain **operator precedence** and **associativity**
- Handle **parentheses** and **multi-operator expressions**

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: "A + B";
Output: "+AB";
```

#### ✅ Test Case 2:

```js
Input: "(A + B) * (C - D)";
Output: "*+AB-CD";
```

#### ✅ Test Case 3:

```js
Input: "A * (B + C) / D";
Output: "/*A+BCD";
```

---

### 💡 Intuition

The idea is similar to infix → postfix, but reversed.

**Steps:**

1. **Reverse the infix expression**

   - Swap `(` with `)`

2. **Convert to postfix** using stack logic
3. **Reverse the result** to get prefix

---

### ⚙️ Operator Precedence

| Operator | Precedence | Associativity |
| -------- | ---------- | ------------- |
| `+`, `-` | 1          | Left          |
| `*`, `/` | 2          | Left          |
| `^`      | 3          | **Right**     |

---

### 🔄 Dry Run

For: `"A + B * C"`

1. Reverse → `"C * B + A"`
2. Convert to postfix: → `"CB*A+"`
3. Reverse: → `"+A*BC"`

✅ Output: `"+A*BC"`

---

### 🧑‍💻 JavaScript Code

```js
function infixToPrefix(expression) {
  const precedence = {
    "+": 1,
    "-": 1,
    "*": 2,
    "/": 2,
    "^": 3,
  };

  const isOperator = (ch) => ["+", "-", "*", "/", "^"].includes(ch);
  const isLeftAssociative = (op) => op !== "^";

  function reverseExpression(expr) {
    return expr
      .split("")
      .reverse()
      .map((ch) => {
        if (ch === "(") return ")";
        if (ch === ")") return "(";
        return ch;
      })
      .join("");
  }

  function infixToPostfix(expr) {
    const stack = [];
    const output = [];

    for (let ch of expr) {
      if (/[a-zA-Z0-9]/.test(ch)) {
        output.push(ch);
      } else if (ch === "(") {
        stack.push(ch);
      } else if (ch === ")") {
        while (stack.length && stack[stack.length - 1] !== "(") {
          output.push(stack.pop());
        }
        stack.pop();
      } else {
        while (
          stack.length &&
          ((isLeftAssociative(ch) &&
            precedence[ch] <= precedence[stack[stack.length - 1]]) ||
            (!isLeftAssociative(ch) &&
              precedence[ch] < precedence[stack[stack.length - 1]]))
        ) {
          output.push(stack.pop());
        }
        stack.push(ch);
      }
    }

    while (stack.length) {
      output.push(stack.pop());
    }

    return output.join("");
  }

  const reversed = reverseExpression(expression.replace(/\s+/g, ""));
  const postfix = infixToPostfix(reversed);
  const prefix = postfix.split("").reverse().join("");
  return prefix;
}

// ✅ Test
console.log(infixToPrefix("A + B")); // +AB
console.log(infixToPrefix("(A + B) * (C - D)")); // *+AB-CD
console.log(infixToPrefix("A * (B + C) / D")); // /*A+BCD
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(n)       |

---

# **Monotonic Stack / Queue [ V.V.Imp ]**

## 📚 Monotonic Stack — Full Concept with Examples

A **monotonic stack** is a stack that is maintained in a **monotonically increasing or decreasing order**. It is **not a new data structure**, but a technique commonly used in **array problems**, especially those involving **"next greater/smaller element"**, **ranges**, or **sliding windows**.

---

### 🚀 What Is a Monotonic Stack?

A **monotonic stack** is a stack that keeps its elements in **sorted order**:

- **Monotonic Increasing Stack:** Top of the stack has the **smallest** element.
- **Monotonic Decreasing Stack:** Top of the stack has the **largest** element.

---

### 🔁 How It Works

As you iterate through the array:

- For **increasing stack**, you **pop** elements that are **greater** than or **equal to** the current element.
- For **decreasing stack**, you **pop** elements that are **less** than or **equal to** the current element.

This ensures the stack always maintains its monotonic property.

---

### 🧠 Tips

- Always use **indexes** in the stack if you need to maintain positions.
- You can use Monotonic Stack in **O(n)** time for many tricky problems.
- Ideal for **sliding window**, **stock span**, and **range queries**.

---

## 🔢 **1. Next Greater Element**

### 📘 Problem Statement

Given an array of integers `arr`, for each element, find the **next greater element** (NGE) to its **right**.
If no such element exists, assign `-1`.

Return an array where each index contains the next greater element for the element at that index in the input array.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: [4, 5, 2, 10];
Output: [5, 10, 10, -1];
```

#### ✅ Test Case 2:

```js
Input: [1, 3, 2, 4];
Output: [3, 4, 4, -1];
```

#### ✅ Test Case 3:

```js
Input: [6, 8, 0, 1, 3];
Output: [8, -1, 1, 3, -1];
```

#### ✅ Test Case 4:

```js
Input: [10, 9, 8, 7];
Output: [-1, -1, -1, -1];
```

---

### 💡 Intuition

To solve this in linear time, we use a **stack** to keep track of candidates for the next greater element.

**Key Idea:**

- Traverse the array **right to left**
- Use a **monotonic decreasing stack**
- For each element, pop smaller elements from the stack
- Top of the stack (after popping) is the next greater

---

### 🔄 Dry Run

Input: `[4, 5, 2, 10]`

Right to left:

```text
i = 3: 10 → no elements right → NGE = -1 → stack = [10]
i = 2: 2  → top = 10 → NGE = 10 → stack = [10, 2]
i = 1: 5  → pop 2 → top = 10 → NGE = 10 → stack = [10, 5]
i = 0: 4  → top = 5 → NGE = 5  → stack = [10, 5, 4]
```

✅ Output: `[5, 10, 10, -1]`

---

### 🧑‍💻 JavaScript Code (Optimized using Stack)

```js
function nextGreaterElement(arr) {
  const stack = [];
  const result = new Array(arr.length).fill(-1);

  for (let i = arr.length - 1; i >= 0; i--) {
    while (stack.length && stack[stack.length - 1] <= arr[i]) {
      stack.pop();
    }
    if (stack.length) {
      result[i] = stack[stack.length - 1];
    }
    stack.push(arr[i]);
  }

  return result;
}

// ✅ Test
console.log(nextGreaterElement([4, 5, 2, 10])); // [5, 10, 10, -1]
console.log(nextGreaterElement([1, 3, 2, 4])); // [3, 4, 4, -1]
console.log(nextGreaterElement([10, 9, 8, 7])); // [-1, -1, -1, -1]
console.log(nextGreaterElement([6, 8, 0, 1, 3])); // [8, -1, 1, 3, -1]
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity       |
| ------ | ---------------- |
| Time   | O(n)             |
| Space  | O(n) (for stack) |

---

## 🔢 **2. Next Greater Element II (Circular Array)**

### 📘 Problem Statement

Given a **circular array** of integers `nums`, find the **next greater element** for each element.
If no such element exists, return `-1`.

You must simulate the circular nature of the array — meaning after the last element, it wraps around to the first.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: [1, 2, 1];
Output: [2, -1, 2];
```

#### ✅ Test Case 2:

```js
Input: [5, 4, 3, 2, 1];
Output: [-1, 5, 5, 5, 5];
```

#### ✅ Test Case 3:

```js
Input: [1, 2, 3, 4, 3];
Output: [2, 3, 4, -1, 4];
```

---

### 💡 Intuition

The circular array means we need to **simulate a second pass** through the array.

**Key Idea:**

- Traverse from `2n - 1 → 0` (simulate circular behavior)
- Use a **monotonic decreasing stack**
- When `i >= n`, we don't update the result — just fill the stack
- When `i < n`, update the result

---

### 🔄 Dry Run

Input: `[1, 2, 1]` (n = 3)

Indices we visit: 5 → 4 → 3 → 2 → 1 → 0
(Actual elements: 1 → 2 → 1 → 1 → 2 → 1)

Result initialized as `[-1, -1, -1]`

```text
i = 5 (1): stack empty → push 1
i = 4 (2): 2 > 1 → pop → result[1] = -1 → push 2
i = 3 (1): 1 < 2 → result[0] = 2 → push 1
i = 2 (1): 1 < 2 → result[2] = 2 → push 1
```

✅ Output: `[2, -1, 2]`

---

### 🧑‍💻 JavaScript Code (Optimized Circular Stack Approach)

```js
function nextGreaterElements(nums) {
  const n = nums.length;
  const result = new Array(n).fill(-1);
  const stack = [];

  for (let i = 2 * n - 1; i >= 0; i--) {
    const current = nums[i % n];

    while (stack.length && stack[stack.length - 1] <= current) {
      stack.pop();
    }

    if (i < n) {
      result[i] = stack.length ? stack[stack.length - 1] : -1;
    }

    stack.push(current);
  }

  return result;
}

// ✅ Test
console.log(nextGreaterElements([1, 2, 1])); // [2, -1, 2]
console.log(nextGreaterElements([5, 4, 3, 2, 1])); // [-1, 5, 5, 5, 5]
console.log(nextGreaterElements([1, 2, 3, 4, 3])); // [2, 3, 4, -1, 4]
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity            |
| ------ | --------------------- |
| Time   | O(2n) = O(n)          |
| Space  | O(n) (stack + output) |

---

## 🔢 **3. Next Smaller Element (NSE)**

### 📘 Problem Statement

Given an array of integers `arr`, for each element, find the **next smaller element** to its **right**.
If no such element exists, return `-1` for that position.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: [4, 5, 2, 10, 8];
Output: [2, 2, -1, 8, -1];
```

#### ✅ Test Case 2:

```js
Input: [1, 3, 0, 2, 1];
Output: [0, 0, -1, 1, -1];
```

#### ✅ Test Case 3:

```js
Input: [5, 4, 3, 2, 1];
Output: [4, 3, 2, 1, -1];
```

#### ✅ Test Case 4:

```js
Input: [1, 2, 3, 4];
Output: [-1, -1, -1, -1];
```

---

### 💡 Intuition

This is just like the **Next Greater Element**, but in reverse:

- Use a **monotonic increasing stack**
- Traverse the array **from right to left**
- For each element:

  - Pop from the stack until we find a smaller one
  - If stack is empty → answer is `-1`
  - Else → top of the stack is the next smaller
  - Push current element into the stack

---

### 🔄 Dry Run

Input: `[4, 5, 2, 10, 8]`

Right to left:

```text
i = 4 (8): no right → NSE = -1 → stack = [8]
i = 3 (10): top 8 < 10 → NSE = 8 → stack = [8, 10]
i = 2 (2): pop 10, 8 → NSE = -1 → stack = [2]
i = 1 (5): top 2 < 5 → NSE = 2 → stack = [2, 5]
i = 0 (4): pop 5 → top = 2 → NSE = 2 → stack = [2, 4]
```

✅ Output: `[2, 2, -1, 8, -1]`

---

### 🧑‍💻 JavaScript Code (Using Stack)

```js
function nextSmallerElement(arr) {
  const stack = [];
  const result = new Array(arr.length).fill(-1);

  for (let i = arr.length - 1; i >= 0; i--) {
    while (stack.length && stack[stack.length - 1] >= arr[i]) {
      stack.pop();
    }
    if (stack.length) {
      result[i] = stack[stack.length - 1];
    }
    stack.push(arr[i]);
  }

  return result;
}

// ✅ Test
console.log(nextSmallerElement([4, 5, 2, 10, 8])); // [2, 2, -1, 8, -1]
console.log(nextSmallerElement([1, 3, 0, 2, 1])); // [0, 0, -1, 1, -1]
console.log(nextSmallerElement([5, 4, 3, 2, 1])); // [4, 3, 2, 1, -1]
console.log(nextSmallerElement([1, 2, 3, 4])); // [-1, -1, -1, -1]
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity            |
| ------ | --------------------- |
| Time   | O(n)                  |
| Space  | O(n) (stack + result) |

---

## 🔢 **4. Trapping Rainwater**

### 📘 Problem Statement

Given `n` non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1];
Output: 6;
```

#### ✅ Test Case 2:

```js
Input: [4, 2, 0, 3, 2, 5];
Output: 9;
```

#### ✅ Test Case 3:

```js
Input: [2, 0, 2];
Output: 2;
```

---

### 🧠 Approach 1: Brute Force

---

### 💡 Idea

For each bar, find the **maximum bar on its left** and **right**, then compute how much water it can trap using:

```
water[i] = min(maxLeft, maxRight) - height[i]
```

---

### 🔄 Dry Run (Test Case 3: \[2,0,2])

```
i = 0: maxLeft=2, maxRight=2 → min(2,2)-2 = 0
i = 1: maxLeft=2, maxRight=2 → min(2,2)-0 = 2 ✅
i = 2: maxLeft=2, maxRight=2 → min(2,2)-2 = 0

Total = 2
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n²)      |
| Space  | O(1)       |

---

### ✅ JavaScript Code

```js
function trapBrute(height) {
  let water = 0;
  const n = height.length;

  for (let i = 0; i < n; i++) {
    let leftMax = 0,
      rightMax = 0;

    for (let j = 0; j <= i; j++) leftMax = Math.max(leftMax, height[j]);
    for (let j = i; j < n; j++) rightMax = Math.max(rightMax, height[j]);

    water += Math.min(leftMax, rightMax) - height[i];
  }

  return water;
}
```

---

### ⚡ Approach 2: Prefix and Suffix Arrays

---

### 💡 Idea

Precompute:

- `leftMax[i]` = max height from start to `i`
- `rightMax[i]` = max height from `i` to end

Then:

```
water[i] = min(leftMax[i], rightMax[i]) - height[i]
```

---

### 🔄 Dry Run (Test Case: \[0,1,0,2,1,0,1,3,2,1,2,1])

**leftMax:** \[0,1,1,2,2,2,2,3,3,3,3,3]
**rightMax:** \[3,3,3,3,3,3,3,3,2,2,2,1]

For each index:

```text
i = 1: min(1,3)-1 = 0
i = 2: min(1,3)-0 = 1 ✅
i = 3: min(2,3)-2 = 0
i = 4: min(2,3)-1 = 1 ✅
i = 5: min(2,3)-0 = 2 ✅
i = 6: min(2,3)-1 = 1 ✅
i = 7: min(3,3)-3 = 0
i = 8: min(3,2)-2 = 0
i = 9: min(3,2)-1 = 1 ✅

Total = 6
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(n)       |

---

### ✅ JavaScript Code

```js
function trapPrefixSuffix(height) {
  const n = height.length;
  const leftMax = Array(n),
    rightMax = Array(n);
  let water = 0;

  leftMax[0] = height[0];
  for (let i = 1; i < n; i++) {
    leftMax[i] = Math.max(leftMax[i - 1], height[i]);
  }

  rightMax[n - 1] = height[n - 1];
  for (let i = n - 2; i >= 0; i--) {
    rightMax[i] = Math.max(rightMax[i + 1], height[i]);
  }

  for (let i = 0; i < n; i++) {
    water += Math.min(leftMax[i], rightMax[i]) - height[i];
  }

  return water;
}
```

---

### 💎 Approach 3: Two Pointer Technique (Space Optimized)

---

### 💡 Idea

Use two pointers (`left`, `right`) and variables for `leftMax`, `rightMax`.
Always move the pointer with the **smaller** height.

---

### 🔄 Dry Run (Test Case: \[0,1,0,2,1,0,1,3,2,1,2,1])

```text
left = 0, right = 11
leftMax = 0, rightMax = 1

height[0]=0 ≤ height[11]=1 → left++
left = 1, height=1, leftMax = 1

left = 2, height=0 → min(leftMax, rightMax)=1 → 1-0 = 1 ✅
left = 3, height=2, leftMax = 2

left = 4, height=1 → 2-1 = 1 ✅
left = 5, height=0 → 2-0 = 2 ✅
left = 6, height=1 → 2-1 = 1 ✅

... eventually reach end → Total = 6
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(1)       |

---

### ✅ JavaScript Code

```js
function trapTwoPointers(height) {
  let left = 0,
    right = height.length - 1;
  let leftMax = 0,
    rightMax = 0,
    water = 0;

  while (left < right) {
    if (height[left] <= height[right]) {
      height[left] >= leftMax
        ? (leftMax = height[left])
        : (water += leftMax - height[left]);
      left++;
    } else {
      height[right] >= rightMax
        ? (rightMax = height[right])
        : (water += rightMax - height[right]);
      right--;
    }
  }

  return water;
}
```

---

### 📊 Comparison Summary

| Approach             | Time  | Space | Notes                            |
| -------------------- | ----- | ----- | -------------------------------- |
| Brute Force          | O(n²) | O(1)  | Simple but slow                  |
| Prefix/Suffix Arrays | O(n)  | O(n)  | Efficient and intuitive          |
| Two Pointers         | O(n)  | O(1)  | Most optimal (no extra space) ✅ |

---

## 🔢 **5. Sum of Subarray Minimums**

### 📘 Problem Statement

Given an array of integers `arr`, return the **sum of the minimum value of every possible subarray**.

Return the answer **modulo** `10^9 + 7`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: [3, 1, 2, 4]
Output: 17

Explanation:
All subarrays:
[3]     → min = 3
[3,1]   → min = 1
[3,1,2] → min = 1
[3,1,2,4] → min = 1
[1]     → min = 1
[1,2]   → min = 1
[1,2,4] → min = 1
[2]     → min = 2
[2,4]   → min = 2
[4]     → min = 4

Sum = 3 + 1 + 1 + 1 + 1 + 1 + 1 + 2 + 2 + 4 = **17**
```

#### ✅ Test Case 2:

```js
Input: [11, 81, 94, 43, 3];
Output: 444;
```

---

### 🧠 Approach 1: Brute Force (Nested Loops)

---

### 💡 Idea

Generate all subarrays and calculate their minimum, sum up the results.

---

### 🔄 Dry Run

Input: `[3, 1, 2, 4]`

```text
Subarrays and their minimums:
[3] → 3
[3,1] → 1
[3,1,2] → 1
[3,1,2,4] → 1
[1] → 1
[1,2] → 1
[1,2,4] → 1
[2] → 2
[2,4] → 2
[4] → 4

Sum = 17 ✅
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n²)      |
| Space  | O(1)       |

---

### ✅ JavaScript Code

```js
function sumSubarrayMinsBrute(arr) {
  const MOD = 1e9 + 7;
  let sum = 0;
  const n = arr.length;

  for (let i = 0; i < n; i++) {
    let min = arr[i];
    for (let j = i; j < n; j++) {
      min = Math.min(min, arr[j]);
      sum = (sum + min) % MOD;
    }
  }

  return sum;
}
```

---

### 💎 Approach 2: Monotonic Stack (Optimized Contribution Method)

### 💡 Idea

Each element `arr[i]` is the **minimum** of some subarrays.
We find out how many **subarrays** have `arr[i]` as their minimum and add `arr[i] * count`.

To do this:

- Use **monotonic stacks** to find:

  - **Previous Less Element (PLE)** — how many elements to the left are ≥ `arr[i]`
  - **Next Less Element (NLE)** — how many elements to the right are > `arr[i]`

Then:

```
contribution = arr[i] * (i - PLE) * (NLE - i)
```

---

### 🔄 Dry Run (Input: \[3, 1, 2, 4])

#### Previous Less:

- PLE = \[-1, -1, 1, 2]

#### Next Less:

- NLE = \[1, 5, 4, 4]

Now compute contribution:

```text
i=0: 3 * (0 - (-1)) * (1 - 0) = 3 * 1 * 1 = 3
i=1: 1 * (1 - (-1)) * (5 - 1) = 1 * 2 * 4 = 8
i=2: 2 * (2 - 1) * (4 - 2) = 2 * 1 * 2 = 4
i=3: 4 * (3 - 2) * (4 - 3) = 4 * 1 * 1 = 4
```

Sum = 3 + 8 + 4 + 4 = **19**

🛑 Wait — seems wrong?
Because we used **strictly less than** for PLE/NLE, but for duplicates and correctness, we must use:

- PLE → Previous **less than** (`<`)
- NLE → Next **less than or equal** (`<=`)

That’s the correct variation.

---

### ✅ JavaScript Code (Monotonic Stack)

```js
function sumSubarrayMins(arr) {
  const n = arr.length;
  const MOD = 1e9 + 7;
  const stack = [];

  const prevLess = Array(n).fill(-1);
  const nextLess = Array(n).fill(n);

  // Find Previous Less Element
  for (let i = 0; i < n; i++) {
    while (stack.length && arr[stack[stack.length - 1]] > arr[i]) {
      stack.pop();
    }
    prevLess[i] = stack.length === 0 ? -1 : stack[stack.length - 1];
    stack.push(i);
  }

  stack.length = 0;

  // Find Next Less Element
  for (let i = n - 1; i >= 0; i--) {
    while (stack.length && arr[stack[stack.length - 1]] >= arr[i]) {
      stack.pop();
    }
    nextLess[i] = stack.length === 0 ? n : stack[stack.length - 1];
    stack.push(i);
  }

  // Calculate Contribution
  let sum = 0;
  for (let i = 0; i < n; i++) {
    const left = i - prevLess[i];
    const right = nextLess[i] - i;
    sum = (sum + arr[i] * left * right) % MOD;
  }

  return sum;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(n)       |

---

## 🔢 **6. Sum of Subarray Ranges**

### 📘 Problem Statement

You are given an integer array `nums`.
The **range** of a subarray is defined as the **difference between the maximum and minimum** elements in the subarray.

> Return the **sum of all subarray ranges** in the array.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: [1, 2, 3]
Output: 4

Explanation:
All subarrays and their range:
[1] => 0
[2] => 0
[3] => 0
[1,2] => 2 - 1 = 1
[2,3] => 3 - 2 = 1
[1,2,3] => 3 - 1 = 2

Total = 0 + 0 + 0 + 1 + 1 + 2 = **4**
```

#### ✅ Test Case 2:

```js
Input: [1, 3, 3];
Output: 4;
```

#### ✅ Test Case 3:

```js
Input: [4, -2, -3, 4, 1];
Output: 59;
```

---

### 🧠 Approach 1: Brute Force

---

### 💡 Idea

Generate all subarrays, and for each:

- Compute min and max
- Add `(max - min)` to sum

---

### 🔄 Dry Run (Input: \[1, 2, 3])

```text
[1] → range = 0
[2] → 0
[3] → 0
[1,2] → 2-1 = 1
[2,3] → 3-2 = 1
[1,2,3] → 3-1 = 2

Total = 4 ✅
```

---

### ✅ JavaScript Code (Brute Force)

```js
function subArrayRanges(nums) {
  let total = 0;
  const n = nums.length;

  for (let i = 0; i < n; i++) {
    let min = nums[i],
      max = nums[i];
    for (let j = i + 1; j < n; j++) {
      min = Math.min(min, nums[j]);
      max = Math.max(max, nums[j]);
      total += max - min;
    }
  }

  return total;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n²)      |
| Space  | O(1)       |

---

### ⚡ Approach 2: Monotonic Stack (Efficient)

---

### 💡 Idea

Break the problem into two parts:

```
Sum of all subarray ranges = Sum of subarray maxs - Sum of subarray mins
```

We already know how to compute:

- Sum of subarray minimums → `monotonic increasing stack`
- Sum of subarray maximums → `monotonic decreasing stack`

---

### 🔄 Dry Run (Input: \[1,2,3])

Sum of subarray maximums:

- \[1] → 1
- \[2] → 2
- \[3] → 3
- \[1,2] → 2
- \[2,3] → 3
- \[1,2,3] → 3
  **Sum = 1 + 2 + 3 + 2 + 3 + 3 = 14**

Sum of subarray minimums:

- \[1] → 1
- \[2] → 2
- \[3] → 3
- \[1,2] → 1
- \[2,3] → 2
- \[1,2,3] → 1
  **Sum = 1 + 2 + 3 + 1 + 2 + 1 = 10**

Range Sum = `14 - 10 = 4` ✅

---

### ✅ JavaScript Code (Optimized)

```js
function subArrayRanges(nums) {
  return getSubarraySum(nums, true) - getSubarraySum(nums, false);
}

function getSubarraySum(nums, isMax) {
  const n = nums.length;
  const stack = [];
  const prev = Array(n);
  const next = Array(n);

  // Previous Less or Greater
  for (let i = 0; i < n; i++) {
    while (
      stack.length &&
      (isMax
        ? nums[stack[stack.length - 1]] <= nums[i]
        : nums[stack[stack.length - 1]] >= nums[i])
    ) {
      stack.pop();
    }
    prev[i] = stack.length === 0 ? -1 : stack[stack.length - 1];
    stack.push(i);
  }

  stack.length = 0;

  // Next Less or Greater
  for (let i = n - 1; i >= 0; i--) {
    while (
      stack.length &&
      (isMax
        ? nums[stack[stack.length - 1]] < nums[i]
        : nums[stack[stack.length - 1]] > nums[i])
    ) {
      stack.pop();
    }
    next[i] = stack.length === 0 ? n : stack[stack.length - 1];
    stack.push(i);
  }

  let sum = 0;
  for (let i = 0; i < n; i++) {
    const left = i - prev[i];
    const right = next[i] - i;
    sum += nums[i] * left * right;
  }

  return sum;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(n)       |

---

### 📌 Summary Table

| Approach        | Time    | Space | Notes                                              |
| --------------- | ------- | ----- | -------------------------------------------------- |
| Brute Force     | O(n²)   | O(1)  | Easy but slow                                      |
| Monotonic Stack | ✅ O(n) | O(n)  | Best for large inputs using subarray max-min split |

---

## 🔢 **7. Asteroid Collision**

### 📘 Problem Statement

You are given an array `asteroids` of integers representing moving asteroids in a row.

- Each asteroid moves at the **same speed**.
- **Positive** values → move to the **right**
- **Negative** values → move to the **left**
- When two asteroids **collide**, the smaller one explodes.

  - If both are the same size → both explode.
  - Two asteroids moving in the **same direction** will never meet.

Return the state of the asteroids after **all collisions**.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: [5, 10, -5];
Output: [5, 10];
```

#### ✅ Test Case 2:

```js
Input: [8, -8];
Output: [];
```

#### ✅ Test Case 3:

```js
Input: [10, 2, -5];
Output: [10];
```

#### ✅ Test Case 4:

```js
Input: [-2, -1, 1, 2];
Output: [-2, -1, 1, 2];
```

---

### 💡 Intuition

Use a **stack** to simulate asteroid behavior.

- Traverse the asteroid list:

  - If current is **positive**, push to stack.
  - If current is **negative**:

    - Compare with top of stack (`top`):

      - If `top > 0` (opposite directions), simulate collision:

        - If `|top| < |current|`: top explodes → keep checking
        - If `|top| === |current|`: both explode → pop and skip
        - If `|top| > |current|`: current explodes → stop

      - Else → no collision, push

---

### 🔄 Dry Run (Test Case: \[10, 2, -5])

```text
Stack: []
10 → push → [10]
2 → push → [10, 2]
-5 →
  top = 2 → 2 < 5 → pop 2 → stack = [10]
  top = 10 → 10 > 5 → -5 explodes → stack = [10]

✅ Final = [10]
```

---

### ✅ JavaScript Code (Using Stack)

```js
function asteroidCollision(asteroids) {
  const stack = [];

  for (const a of asteroids) {
    let destroyed = false;

    while (stack.length && a < 0 && stack[stack.length - 1] > 0) {
      const top = stack[stack.length - 1];

      if (top < -a) {
        stack.pop(); // top explodes
        continue;
      } else if (top === -a) {
        stack.pop(); // both explode
        destroyed = true;
        break;
      } else {
        destroyed = true; // current explodes
        break;
      }
    }

    if (!destroyed) {
      stack.push(a);
    }
  }

  return stack;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(n)       |

---

### 📌 Summary

| Rule                          | Action                        |
| ----------------------------- | ----------------------------- |
| Both positive                 | No collision                  |
| Both negative                 | No collision                  |
| Left negative, right positive | No collision                  |
| Right positive, left negative | 🚀 Collision → simulate stack |

---

## 🔢 **8. Remove K Digits**

### 📘 Problem Statement

Given a string `num` representing a **non-negative integer**, and an integer `k`, remove **k digits** from `num` so that the resulting number is the **smallest possible**.

Return the final number as a **string**.
If the result has leading zeros, remove them.
If the result is an empty string, return `'0'`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: (num = "1432219"), (k = 3);
Output: "1219";
```

#### ✅ Test Case 2:

```js
Input: (num = "10200"), (k = 1);
Output: "200";
```

#### ✅ Test Case 3:

```js
Input: (num = "10"), (k = 2);
Output: "0";
```

---

### 🧠 Intuition

To get the **smallest possible number**, remove digits that are:

- **Greater than the digit that follows them**, especially from left to right.

Use a **monotonic increasing stack** to build the answer:

- If the current digit < stack’s top and we still have `k > 0`, **pop the stack**.
- Then push the current digit.

---

### 🔄 Dry Run (Test Case: `"1432219", k = 3`)

```text
Stack: []

1 → push → [1]
4 → 4 > 1 → push → [1, 4]
3 → 3 < 4 → pop(4), k=2 → push(3) → [1, 3]
2 → 2 < 3 → pop(3), k=1 → push(2) → [1, 2]
2 → 2 = 2 → push → [1, 2, 2]
1 → 1 < 2 → pop(2), k=0 → push(1) → [1, 2, 1]
9 → k=0 → push(9) → [1, 2, 1, 9]

Result stack = "1219"
```

---

### ✅ JavaScript Code

```js
function removeKdigits(num, k) {
  const stack = [];

  for (const digit of num) {
    while (k > 0 && stack.length && stack[stack.length - 1] > digit) {
      stack.pop();
      k--;
    }
    stack.push(digit);
  }

  // If still digits to remove, remove from the end
  while (k > 0) {
    stack.pop();
    k--;
  }

  // Remove leading zeros
  let result = stack.join("").replace(/^0+/, "");
  return result === "" ? "0" : result;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(n)       |

---

## 🔢 **9. Largest Rectangle in a Histogram**

### 📘 Problem Statement

You are given an array `heights[]` of `n` non-negative integers representing the height of bars in a histogram where the **width of each bar is 1**.

> Return the **area of the largest rectangle** that can be formed in the histogram.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: [2, 1, 5, 6, 2, 3]
Output: 10

Explanation: The rectangle of height 5 and 6 gives area 5×2 = 10
```

#### ✅ Test Case 2:

```js
Input: [2, 4];
Output: 4;
```

#### ✅ Test Case 3:

```js
Input: [1, 2, 3, 4, 5]
Output: 9

Explanation: Bars 3, 4, 5 → 3×3 = 9
```

---

### 🧠 Approach 1: Brute Force (expand left and right)

---

### 💡 Idea

For every bar, expand left and right until you find a shorter bar.
Calculate area:

```text
area = height[i] * (right - left - 1)
```

---

### 🔄 Dry Run: Input `[2, 1, 5, 6, 2, 3]`

For `i = 2` (height 5):

- Expand left to `i=1` → height=1 < 5 ✅
- Expand right to `i=3` → height=6 >= 5
  Then `i=4` → height=2 < 5 → stop
  → Width = 2 → Area = 5×2 = 10 ✅

Repeat for each bar.

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n²)      |
| Space  | O(1)       |

---

### 💎 Approach 2: Monotonic Stack (Optimal)

---

### 💡 Idea

Use a **monotonic increasing stack** to track **indices**.

- For each bar, if it's **higher than the stack top**, push index.
- Else:

  - Pop the stack
  - Calculate area using:

    ```js
    height = heights[top];
    width = i - stack[stack.length - 1] - 1;
    ```

To make sure we process everything, **append a 0** at the end of `heights`.

---

### 🔄 Dry Run: Input `[2,1,5,6,2,3]`

After appending 0 → `[2,1,5,6,2,3,0]`

```text
i=0: stack=[0]
i=1: 1<2 → pop 0 → height=2, width=1 → area=2 → max=2 → stack=[]
       push 1 → [1]
i=2: 5>1 → push → [1,2]
i=3: 6>5 → push → [1,2,3]
i=4: 2<6 → pop 3 → height=6, width=1 → area=6 → max=6
       pop 2 → height=5, width=2 → area=10 ✅ → max=10
       push 4 → [1,4]
...
Continue → Final max area = 10
```

---

### ✅ JavaScript Code

```js
function largestRectangleArea(heights) {
  const stack = [];
  let maxArea = 0;
  heights.push(0); // Sentinel to flush stack at the end

  for (let i = 0; i < heights.length; i++) {
    while (stack.length && heights[i] < heights[stack[stack.length - 1]]) {
      const height = heights[stack.pop()];
      const width = stack.length === 0 ? i : i - stack[stack.length - 1] - 1;
      maxArea = Math.max(maxArea, height * width);
    }
    stack.push(i);
  }

  return maxArea;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(n)       |

---

### 📌 Summary

| Approach        | Time    | Space | Notes                                |
| --------------- | ------- | ----- | ------------------------------------ |
| Brute Force     | O(n²)   | O(1)  | Easy but slow                        |
| Monotonic Stack | ✅ O(n) | O(n)  | Optimal for histogram rectangle area |

---

# Implementation Problems

## 🔢 **1. Sliding Window Maximum**

### 📘 Problem Statement

You are given an array `nums` and an integer `k`, representing the size of a **sliding window**.

> Return an array of the **maximum** element in every window of size `k`.

---

#### 🧪 Test Cases

##### ✅ Test Case 1:

```js
Input: (nums = [1, 3, -1, -3, 5, 3, 6, 7]), (k = 3);
Output: [3, 3, 5, 5, 6, 7];
```

##### ✅ Test Case 2:

```js
Input: (nums = [9, 11]), (k = 2);
Output: [11];
```

##### ✅ Test Case 3:

```js
Input: (nums = [4, -2]), (k = 2);
Output: [4];
```

---

### 🧠 Intuition

We want to **maintain a list of potential max elements** in the window efficiently.

#### 🔑 Idea: Use a **Monotonic Deque**

- Maintain indices of useful elements in a **decreasing order**
- Front of deque is always the **max of current window**
- Remove:

  - Indices **outside the window**
  - Elements **smaller than current**, as they can't be max anymore

---

### 🔄 Dry Run (Input: `[1,3,-1,-3,5,3,6,7], k=3`)

```text
i=0 → deque=[0]     → window=[1]
i=1 → nums[1]=3 > nums[0]=1 → pop 0 → push 1 → deque=[1]
i=2 → -1 < 3 → push 2 → deque=[1,2] → max=3

i=3 → remove index 1 if out of window → deque=[1,2,3] → max=3
i=4 → nums[4]=5 > all → pop 3,2,1 → push 4 → max=5
...
Result: [3,3,5,5,6,7]
```

---

### ✅ JavaScript Code (Deque - Optimal)

```js
function maxSlidingWindow(nums, k) {
  const deque = [];
  const result = [];

  for (let i = 0; i < nums.length; i++) {
    // Remove elements out of current window
    if (deque.length && deque[0] <= i - k) {
      deque.shift();
    }

    // Remove smaller elements from the back
    while (deque.length && nums[deque[deque.length - 1]] < nums[i]) {
      deque.pop();
    }

    deque.push(i);

    // Record the max
    if (i >= k - 1) {
      result.push(nums[deque[0]]);
    }
  }

  return result;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(k)       |

- Each element is pushed/popped **at most once**

---

### 📌 Summary

| Concept             | Explanation                  |
| ------------------- | ---------------------------- |
| Monotonic deque     | Decreasing → Front = max     |
| Remove old elements | If `index <= i - k`          |
| Remove useless      | Smaller than current element |
| Window starts       | When `i >= k - 1`            |

---

## 🔢 **2. Stock Span Problem**

### 📘 Problem Statement

You're given an array `prices[]` where `prices[i]` is the **price of a stock on the ith day**.

> For each day `i`, return the **stock span**: the number of **consecutive days (including today)** where the price was **less than or equal** to `prices[i]`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input: [100, 80, 60, 70, 60, 75, 85];
Output: [1, 1, 1, 2, 1, 4, 6];
```

#### ✅ Test Case 2:

```js
Input: [10, 4, 5, 90, 120, 80];
Output: [1, 1, 2, 4, 5, 1];
```

---

### 🧠 Intuition

We want to find the **nearest previous greater element** for each day.

- Span = `i - previous_greater_index`
- Use a **monotonic decreasing stack** (stores indices of prices in decreasing order)
- If current price ≥ top of stack → pop (they’re part of the span)
- If stack is empty → span = `i + 1`
  Else → span = `i - stackTop`

---

### 🔄 Dry Run (Input: `[100, 80, 60, 70, 60, 75, 85]`)

```text
i = 0 → price = 100 → stack = [] → span = 1 → push 0
i = 1 → price = 80 < 100 → span = 1 → push 1
i = 2 → price = 60 < 80 → span = 1 → push 2
i = 3 → price = 70 > 60 → pop 2 → span = i - stackTop = 3 - 1 = 2 → push 3
i = 4 → price = 60 < 70 → span = 1 → push 4
i = 5 → price = 75 > 60 → pop 4, pop 3 → span = 5 - 1 = 4 → push 5
i = 6 → price = 85 > 75 → pop 5 → span = 6 - 1 = 6 → push 6

✅ Output: [1, 1, 1, 2, 1, 4, 6]
```

---

### ✅ JavaScript Code

```js
function calculateSpan(prices) {
  const n = prices.length;
  const span = Array(n).fill(1);
  const stack = [];

  for (let i = 0; i < n; i++) {
    while (stack.length && prices[stack[stack.length - 1]] <= prices[i]) {
      stack.pop();
    }

    span[i] = stack.length === 0 ? i + 1 : i - stack[stack.length - 1];
    stack.push(i);
  }

  return span;
}
```

---

#### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(n)       |

Each element is pushed/popped once.

---

### 📌 Summary

| Concept             | Explanation                   |
| ------------------- | ----------------------------- |
| Monotonic Stack     | Decreasing by price           |
| Goal                | Find nearest previous greater |
| Span Formula        | `i - previous_greater_index`  |
| If no greater found | Span = `i + 1`                |

---

## 🔢 **3. The Celebrity Problem**

### 📘 Problem Statement

You are given a `n x n` **matrix `M[][]`**, where:

- `M[i][j] = 1` means person `i` **knows** person `j`
- `M[i][j] = 0` means person `i` **doesn't know** person `j`

> A **celebrity** is someone who:

1. **Is known by everyone**
2. **Knows no one**

Find the **index** of the celebrity if one exists, otherwise return `-1`.

---

### 🧪 Test Cases

#### ✅ Test Case 1:

```js
Input:
M = [
  [0, 1, 0],
  [0, 0, 0],
  [0, 1, 0]
]

Output: 1
Explanation: Everyone knows person 1, and person 1 knows no one.
```

#### ✅ Test Case 2:

```js
Input:
M = [
  [0, 1],
  [1, 0]
]

Output: -1
Explanation: Both know each other → no celebrity
```

---

### 🧠 Intuition

- If person `A` knows `B`, then `A` **cannot** be a celebrity.
- If person `A` doesn't know `B`, then `B` **cannot** be a celebrity.

So we can eliminate one person in each comparison and narrow down to **one candidate**, then **verify** if that person is really a celebrity.

---

### ✅ Approach 1: Stack (Elimination Method)

---

#### 💡 Idea

1. Push all `n` people into a stack
2. While there are at least 2 people:

   - Pop 2 people `A` and `B`
   - If `A` knows `B` → A can’t be celebrity → keep B
   - Else → B can’t be celebrity → keep A

3. One person left → possible celebrity
4. Verify: For all `i ≠ celeb`

   - `M[celeb][i] === 0` (celeb knows no one)
   - `M[i][celeb] === 1` (everyone knows celeb)

---

#### 🔄 Dry Run (Input: `[[0,1,0],[0,0,0],[0,1,0]]`)

```text
Stack: [0,1,2]

Pop 2 & 1 → does 2 know 1? Yes → keep 1
Stack: [0,1]

Pop 0 & 1 → does 0 know 1? Yes → keep 1
Stack: [1]

Check: does everyone know 1 and 1 knows no one?
✅ Yes → return 1
```

---

#### ✅ JavaScript Code

```js
function findCelebrity(M, n) {
  const stack = [];

  for (let i = 0; i < n; i++) {
    stack.push(i);
  }

  while (stack.length > 1) {
    const A = stack.pop();
    const B = stack.pop();

    if (M[A][B] === 1) {
      // A knows B → A is not celebrity
      stack.push(B);
    } else {
      // A doesn't know B → B is not celebrity
      stack.push(A);
    }
  }

  const candidate = stack.pop();

  // Verify candidate
  for (let i = 0; i < n; i++) {
    if (i !== candidate) {
      if (M[candidate][i] === 1 || M[i][candidate] === 0) {
        return -1;
      }
    }
  }

  return candidate;
}
```

---

### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(n)       |

---

### ⚡️ **Approach 2: Two-Pointer Elimination (No Stack)**

#### 💡 Intuition

We can reduce the space complexity by using **two pointers** and eliminate non-celebrity candidates in a single pass.

#### 🔑 Key Insight:

- Initialize `candidate = 0`
- For each person `i = 1 to n-1`:

  - If `candidate` **knows** `i` → candidate can’t be celebrity → update candidate = `i`
  - Else → `i` can’t be celebrity → continue

> After one full pass, you're left with one **potential candidate**.
> Now do a **full verification pass** like in Approach 1.

---

#### 🔄 Dry Run

Input:

```js
M = [
  [0, 1, 0],
  [0, 0, 0],
  [0, 1, 0],
];
```

```text
candidate = 0
i = 1 → M[0][1] = 1 → 0 knows 1 → candidate = 1
i = 2 → M[1][2] = 0 → 1 doesn’t know 2 → keep 1

Verify:
  M[1][0] = 0 ✅
  M[0][1] = 1 ✅
  M[2][1] = 1 ✅
  M[1][2] = 0 ✅

✔️ Return: 1
```

---

#### ✅ JavaScript Code

```js
function findCelebrity(M, n) {
  let candidate = 0;

  // Step 1: Find potential candidate
  for (let i = 1; i < n; i++) {
    if (M[candidate][i] === 1) {
      // candidate knows i → can't be celebrity
      candidate = i;
    }
    // else, i can't be celebrity → skip
  }

  // Step 2: Verify candidate
  for (let i = 0; i < n; i++) {
    if (i !== candidate) {
      if (M[candidate][i] === 1 || M[i][candidate] === 0) {
        return -1;
      }
    }
  }

  return candidate;
}
```

---

#### ⏱️ Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | ✅ O(1)    |

---

### 📌 Summary Comparison

| Approach    | Time    | Space   | Notes                                      |
| ----------- | ------- | ------- | ------------------------------------------ |
| Stack       | O(n)    | O(n)    | Simpler to grasp, uses extra stack         |
| Two-Pointer | ✅ O(n) | ✅ O(1) | Most optimal solution — interview favorite |

---

## 🔢 **4. LRU Cache Implementation**

### 📘 Problem Statement

Design and implement a **data structure** for **Least Recently Used (LRU) Cache** that supports:

- `get(key)` → return the value (if present), else `-1`
- `put(key, value)` → insert/update the value for the key

> Both operations must run in **O(1)** time on average.

---

### 🔒 LRU Behavior

When the cache reaches its capacity:

- Remove the **least recently used** item **before inserting a new one**

---

### 🧪 Test Case Example

```js
Input:
["LRUCache","put","put","get","put","get","put","get","get","get"]
[[2],       [1,1],[2,2],[1], [3,3],[2], [4,4],[1], [3], [4]]

Output:
[null,     null, null, 1,   null, -1,  null, -1,  3,   4]

Explanation:
LRUCache cache = new LRUCache(2);
cache.put(1, 1);
cache.put(2, 2);
cache.get(1);    // returns 1
cache.put(3, 3); // evicts key 2
cache.get(2);    // returns -1 (not found)
cache.put(4, 4); // evicts key 1
cache.get(1);    // returns -1 (not found)
cache.get(3);    // returns 3
cache.get(4);    // returns 4
```

---

### 🧠 Intuition

To achieve **O(1)**:

- Use a **Map** for fast key lookup
- Use a **Doubly Linked List** to track **recency of usage**

### 🧩 Why Doubly Linked List?

- Remove any node in **O(1)** time
- Move accessed node to the **front (most recent)** in **O(1)**

---

### 🔄 Dry Run

Capacity: 2
Insert 1 → list: \[1]
Insert 2 → list: \[2,1]
Get(1) → move 1 to front → \[1,2]
Put 3 → evict LRU (2) → list: \[3,1]
Get(2) → not found
Put 4 → evict LRU (1) → list: \[4,3]
...

---

### ✅ JavaScript Code: Doubly Linked List + HashMap

```js
class Node {
  constructor(key, val) {
    this.key = key;
    this.val = val;
    this.prev = null;
    this.next = null;
  }
}

class LRUCache {
  constructor(capacity) {
    this.capacity = capacity;
    this.map = new Map(); // key -> node
    this.head = new Node(0, 0); // dummy head
    this.tail = new Node(0, 0); // dummy tail
    this.head.next = this.tail;
    this.tail.prev = this.head;
  }

  // Remove node from list
  remove(node) {
    node.prev.next = node.next;
    node.next.prev = node.prev;
  }

  // Insert node right after head
  insert(node) {
    node.next = this.head.next;
    node.prev = this.head;
    this.head.next.prev = node;
    this.head.next = node;
  }

  get(key) {
    if (this.map.has(key)) {
      const node = this.map.get(key);
      this.remove(node);
      this.insert(node); // move to front
      return node.val;
    }
    return -1;
  }

  put(key, value) {
    if (this.map.has(key)) {
      this.remove(this.map.get(key));
    }

    const newNode = new Node(key, value);
    this.insert(newNode);
    this.map.set(key, newNode);

    if (this.map.size > this.capacity) {
      // Remove LRU from tail
      const lru = this.tail.prev;
      this.remove(lru);
      this.map.delete(lru.key);
    }
  }
}
```

---

### ⏱️ Time & Space Complexity

| Operation | Time | Explanation                   |
| --------- | ---- | ----------------------------- |
| `get()`   | O(1) | Map lookup + move to front    |
| `put()`   | O(1) | Insert + remove LRU if needed |
| Space     | O(N) | For map + linked list         |

---

## 🔢 **5. LFU Cache**

### 📘 Problem Statement

Design and implement the **Least Frequently Used (LFU)** cache with the following rules:

- `get(key)` — get the value if the key exists, else return `-1`
- `put(key, value)` — insert/update key
- If the capacity is reached, evict the **least frequently used** key
- If multiple keys have the same frequency, evict the **least recently used**

All operations must run in **O(1)** on average.

---

### 🧪 Test Case

```js
Input:
["LFUCache","put","put","get","put","get","get","put","get","get","get"]
[[2],       [1,1],[2,2],[1], [3,3],[2],  [3],  [4,4],[1], [3],  [4]]

Output:
[null,     null, null, 1,   null, -1,  3,   null, -1,  3,   4]

Explanation:
LFUCache(2)
put(1,1)
put(2,2)
get(1) → returns 1 (freq of 1 becomes 2)
put(3,3) → evicts 2 (freq=1, least recent)
get(2) → -1
get(3) → 3
put(4,4) → evicts 1 (freq=2), 3 remains
get(1) → -1
get(3) → 3
get(4) → 4
```

---

### 🧠 Intuition

To support **frequency + recency**, we need:

- A **map from key → node** with `(key, value, frequency)`
- A **map from frequency → doubly linked list** to keep all keys with the same frequency in order of usage (LRU within frequency group)
- Track `minFreq` to quickly know which frequency to evict

---

### 🔄 Dry Run (put/get operations)

Let’s say:

- `put(1,1)` → freq = 1
- `put(2,2)` → freq = 1
- `get(1)` → freq = 2
- `put(3,3)` → evict least recent with freq=1 → evict 2
- …

We update both maps accordingly and maintain:

- Frequency counts
- LRU order within each frequency group

---

### ✅ JavaScript Code (Optimized O(1) Solution)

```js
class Node {
  constructor(key, val) {
    this.key = key;
    this.val = val;
    this.freq = 1;
    this.prev = null;
    this.next = null;
  }
}

class DoublyLinkedList {
  constructor() {
    this.head = new Node(0, 0);
    this.tail = new Node(0, 0);
    this.head.next = this.tail;
    this.tail.prev = this.head;
    this.size = 0;
  }

  add(node) {
    node.next = this.head.next;
    node.prev = this.head;
    this.head.next.prev = node;
    this.head.next = node;
    this.size++;
  }

  remove(node) {
    node.prev.next = node.next;
    node.next.prev = node.prev;
    this.size--;
  }

  removeLast() {
    if (this.size === 0) return null;
    const node = this.tail.prev;
    this.remove(node);
    return node;
  }
}

class LFUCache {
  constructor(capacity) {
    this.capacity = capacity;
    this.size = 0;
    this.minFreq = 0;
    this.nodeMap = new Map(); // key → node
    this.freqMap = new Map(); // freq → DLL
  }

  get(key) {
    if (!this.nodeMap.has(key)) return -1;
    const node = this.nodeMap.get(key);
    this.updateFreq(node);
    return node.val;
  }

  put(key, value) {
    if (this.capacity === 0) return;

    if (this.nodeMap.has(key)) {
      const node = this.nodeMap.get(key);
      node.val = value;
      this.updateFreq(node);
    } else {
      if (this.size === this.capacity) {
        const minList = this.freqMap.get(this.minFreq);
        const nodeToEvict = minList.removeLast();
        this.nodeMap.delete(nodeToEvict.key);
        this.size--;
      }

      const newNode = new Node(key, value);
      this.nodeMap.set(key, newNode);
      if (!this.freqMap.has(1)) {
        this.freqMap.set(1, new DoublyLinkedList());
      }
      this.freqMap.get(1).add(newNode);
      this.minFreq = 1;
      this.size++;
    }
  }

  updateFreq(node) {
    const oldFreq = node.freq;
    const oldList = this.freqMap.get(oldFreq);
    oldList.remove(node);

    if (oldFreq === this.minFreq && oldList.size === 0) {
      this.minFreq++;
    }

    node.freq++;
    if (!this.freqMap.has(node.freq)) {
      this.freqMap.set(node.freq, new DoublyLinkedList());
    }

    this.freqMap.get(node.freq).add(node);
  }
}
```

---

### ⏱️ Time & Space Complexity

| Operation | Time    | Space |
| --------- | ------- | ----- |
| get/put   | ✅ O(1) | O(n)  |

---

### 📌 Summary

| Component     | Role                                           |
| ------------- | ---------------------------------------------- |
| `nodeMap`     | Key → Node (stores key, val, freq)             |
| `freqMap`     | Freq → DoublyLinkedList of nodes               |
| `minFreq`     | Tracks minimum frequency in cache              |
| Eviction Rule | Evict least recently used from lowest freq DLL |

---
