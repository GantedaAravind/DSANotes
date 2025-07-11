# **What is An Algorithm**

> An Algorithm is a Step By Step precedure or Formula for solving a problem or accomplishing a task.

> It's a Sequence of Well Defined Instructions or rules that specify how to solve a problem in finite no. of steps

### 📘 What is **Asymptotic Notation**?

**Asymptotic Notation** is a method used in **computer science** mathematical tool to describe the **Time Complexity** of a function or algorithm as its i/o size tends towards infinity(i.e., as $n \to \infty$). It helps as understand how to performance of an algorithm **input size grows very large**

---

### ⚙️ Why do we use it?

We use **asymptotic notation** to:

- Compare the **performance** of algorithms.
- Focus on the **growth rate**, ignoring constant factors and lower-order terms.

---

# 🧠 **Time and Space Complexity**

## 📘 **What is Time and Space Complexity?**

- **Time Complexity** measures how **execution time** grows with **input size**.
- **Space Complexity** measures how much **extra memory** (excluding input) an algorithm needs as input size grows.

---

## 📘 **Big O Notation**

Let $f(n)$ and $g(n)$ be two functions that represent the time (or space) complexity of algorithms.

We say:

$$
f(n) = O(g(n))
$$

**if and only if** there exist constants:

- $c > 0$ (a positive constant multiplier), and
- $n_0 \geq 0$ (a threshold input size)
- O(g(n)) -> {set of Function which statisfy the condition}

such that:

$$
\text{for all } n \geq n_0, \quad f(n) \leq c \cdot g(n)
$$

---

### 🔍 In Plain Words:

- $f(n)$ grows **no faster than** $g(n)$, up to a constant factor, for **large enough** $n$.
- We use it to say that $f(n)$ is **bounded above** by $g(n)$ asymptotically.
- To express the `upper bound` — the maximum amount of time or space an algorithm can use Big O-Notation.

### ✅ **Example:**

Let $f(n) = 3n + 2$

We want to show:

$$
f(n) = O(n)
$$

Proof:

We try to find constants $c$ and $n_0$ such that:

$$
3n + 2 \leq c \cdot n \quad \text{for all } n \geq n_0
$$

Try $c = 4$, then:

$$
3n + 2 \leq 4n \iff 2 \leq n \Rightarrow \text{True when } n \geq 2
$$

So, $f(n) = 3n + 2 = O(n)$ with $c = 4$, $n_0 = 2$

---

## 📘 **Big Omega(Ω) Notation**

**Big Omega notation**, written as $\Omega(g(n))$, gives a **lower bound** on the **growth rate** of a function.

In other words, it tells us the **best-case** or **minimum time/space** an algorithm will take for large input sizes.

---

### 🔢 **Formal Mathematical Definition:**

Let $f(n)$ and $g(n)$ be functions that map natural numbers to non-negative real numbers.
We write:

$$
f(n) = \Omega(g(n))
$$

**if and only if** there exist constants:

- $c > 0$ (a positive constant), and
- $n_0 \geq 0$ (a threshold input size)

such that:

$$
\text{for all } n \geq n_0, \quad f(n) \geq c \cdot g(n)
$$

---

### 💬 **In Plain English:**

- $f(n)$ grows **at least as fast as** $g(n)$ beyond some point.
- It describes the **minimum work** an algorithm will always do.
- Think of it as the **opposite of Big O**, which gives an upper bound.

---

### ✅ **Example:**

Let’s say $f(n) = 3n + 2$.
We want to prove:

$$
f(n) = \Omega(n)
$$

Proof:

We try to find constants $c$ and $n_0$ such that:

$$
3n + 2 \geq c \cdot n
$$

Try $c = 2$:

$$
3n + 2 \geq 2n \quad \Rightarrow \quad n + 2 \geq 0
$$

This is true for **all $n \geq 0$**.
So, we can say:

$$
f(n) = \Omega(n) \quad \text{with } c = 2, \ n_0 = 0
$$

---

## 📘 **Theta (Θ) Notation — Mathematical Definition**

**Theta notation**, written as $\Theta(g(n))$, gives a **tight bound** on the growth of a function.
It means the function grows **at the same rate** as $g(n)$, both **upper** and **lower bounds**.

---

### 🔢 **Formal Definition:**

Let $f(n)$ and $g(n)$ be functions that map natural numbers to positive real numbers.
We say:

$$
f(n) = \Theta(g(n))
$$

**if and only if** there exist constants:

- $c_1 > 0$,
- $c_2 > 0$, and
- $n_0 \geq 0$

such that:

$$
\text{for all } n \geq n_0, \quad c_1 \cdot g(n) \leq f(n) \leq c_2 \cdot g(n)
$$

---

### 💬 **In Plain Words:**

- $f(n)$ grows **at the same rate** as $g(n)$, within constant factors.
- It gives both the **worst-case** and **best-case** growth rate.
- It’s the **most precise** asymptotic notation.

---

### ✅ **Example:**

Let $f(n) = 3n + 2$

We want to prove:

$$
f(n) = \Theta(n)
$$

---

**Step 1: Lower bound (Big Omega):**

We want:

$$
3n + 2 \geq c_1 \cdot n \quad \text{for all } n \geq n_0
$$

Try $c_1 = 2$:

$$
3n + 2 \geq 2n \quad \Rightarrow \quad n + 2 \geq 0 \quad \text{(true when \( n \geq 0 \)) }
$$

---

**Step 2: Upper bound (Big O):**

We want:

$$
3n + 2 \leq c_2 \cdot n
$$

Try $c_2 = 4$:

$$
3n + 2 \leq 4n \quad \Rightarrow \quad 2 \leq n \quad \text{(true when \( n \geq 2 \)) }
$$

---

✅ So:

$$
3n + 2 = \Theta(n) \quad \text{with } c_1 = 2, c_2 = 4, n_0 = 2
$$

---

![](https://www.boardinfinity.com/blog/content/images/2022/10/o--9-.jpg)

## 📘 **Little-o (Small-o) Notation — Mathematical Definition**

**Little-o notation**, written as $o(g(n))$, describes the **strictly lower bound** of a function's growth rate.

It means that $f(n)$ grows **slower** than $g(n)$ — and **never catches up**, even asymptotically.

---

$
o(g(n))$ = $ \{ f(n)$ : for any positive constant
$c$ > 0, there exists a constant
$n_0$ > 0 ${such that}$ 0 $\leq$ $f(n)$ < $c$ $\cdot$ $g(n)$ ${ for all } $ n $\geq$ $n_0$ $\}$

### 🔢 **Formal Definition:**

We say:

$$
f(n) = o(g(n))
$$

**if and only if**:

$$
\lim_{n \to \infty} \frac{f(n)}{g(n)} = 0
$$

---

### 🔍 **Plain English Explanation:**

This means:

- $f(n) \in o(g(n))$ if for **every positive constant** $c$, no matter how small,
- There is some threshold $n_0$ beyond which:

  $$
  f(n) < c \cdot g(n) \quad \text{for all } n \geq n_0
  $$

- In other words, $f(n)$ becomes **insignificantly smaller** than $g(n)$ as $n \to \infty$.

---

### ✅ **Example 1:**

Let $f(n) = n$, $g(n) = n^2$

$$
\frac{f(n)}{g(n)} = \frac{n}{n^2} = \frac{1}{n} \to 0 \text{ as } n \to \infty
$$

✅ So:

$$
n = o(n^2)
$$

---

## 📘 **Little-Omega Notation — $\omega(g(n))$**

### 🧠 **What is Little-Omega Notation?**

- **Little-omega** ($\omega(g(n))$) describes a **strict lower bound** on a function's growth rate.
- It tells us that a function $f(n)$ grows **strictly faster** than $g(n)$ as $n \to \infty$.
- It’s the **opposite of little-o**, just like **Omega (Ω)** is the opposite of **Big-O**.

---

### 🔢 **Mathematical Definition**

$$
f(n) = \omega(g(n))
$$

**if and only if:**

> For **every constant** $c > 0$, there exists a constant $n_0 > 0$ such that:

$$
f(n) > c \cdot g(n) \quad \text{for all } n \geq n_0
$$

---

✅ **Alternative limit-based definition:**

$$
f(n) = \omega(g(n)) \quad \iff \quad \lim_{n \to \infty} \frac{f(n)}{g(n)} = \infty
$$

---

### 💬 **Plain English Explanation**

- $f(n) \in \omega(g(n))$ means:

  - No matter **how large** a constant multiple $c \cdot g(n)$ you choose,
  - Eventually, $f(n)$ will **exceed** it,
  - and keep growing **much faster** than $g(n)$ as $n \to \infty$.

---

### 🟩 **Example 1:**

Let $f(n) = n^2$, $g(n) = n$

$$
\frac{f(n)}{g(n)} = \frac{n^2}{n} = n \to \infty
\Rightarrow n^2 = \omega(n)
$$

---

## 📈 **Time Complexity**

### 📌 **How to Analyze Time Complexity?**

#### 💡 Rule 1: Count Loops

```js
for (let i = 0; i < n; i++) {
  // O(1) operation
}
// ➤ O(n)
```

#### 💡 Rule 2: Nested Loops Multiply

```js
for (let i = 0; i < n; i++) {
  for (let j = 0; j < n; j++) {
    // O(1)
  }
}
// ➤ O(n²)
```

#### 💡 Rule 3: Consecutive loops ADD

```js
for (let i = 0; i < n; i++) {} // O(n)
for (let j = 0; j < m; j++) {} // O(m)
// ➤ O(n + m)
```

#### 💡 Rule 4: Recursive Calls

```js
function fib(n) {
  if (n <= 1) return 1;
  return fib(n - 1) + fib(n - 2);
}
// ➤ O(2^n)
```

Use **recursion trees** or **Master Theorem** for more complex ones.

---

## 🧮 **Space Complexity**

### ✅ What It Measures:

- **Extra memory** used by the algorithm (not counting input).
- Includes **variables, data structures, recursive call stacks**.

---

### 📌 **How to Analyze Space Complexity?**

#### ✅ Variables

```js
let a = 10; // O(1)
let arr = new Array(n); // O(n)
```

#### ✅ Recursive Stack

```js
function binarySearch(start, end) {
  if (start > end) return;
  let mid = Math.floor((start + end) / 2);
  binarySearch(start, mid - 1);
  binarySearch(mid + 1, end);
}
// ➤ O(log n) stack space
```

---

### 👀 Space Complexity in Recursion

If a function calls itself `n` times and each call is independent:

- Stack builds up to depth `n`: O(n)

Example:

```js
function countdown(n) {
  if (n === 0) return;
  countdown(n - 1);
}
// ➤ O(n) space due to call stack
```

---

## 🛠️ Real Example Walkthrough

### 🧮 Example: Two Sum Problem

```js
function twoSum(nums, target) {
  let map = new Map(); // O(n) space

  for (let i = 0; i < nums.length; i++) {
    let complement = target - nums[i];
    if (map.has(complement)) {
      return [map.get(complement), i];
    }
    map.set(nums[i], i);
  }
}
```

- **Time Complexity**: O(n)
- **Space Complexity**: O(n)

Why?

- One pass through `n` elements = O(n)
- Map stores up to `n` elements = O(n)

---
