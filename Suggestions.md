- sum - prefix sum
- always you dooing the array O(n2) can done with hash map by o(n)
- when searching two elements you use one for hashmap and other at that index and iterate find the pair

- sorted - binary Search

- answer in the range `Binary Search on answers`
- min max / max min `binary search on answers`
-

## ✅ When to Use `mod` (Modulo)

You typically apply the **modulo**:

1. **After every multiplication**
2. **After every addition**
3. **After subtraction (with adjustment)**
4. **Never inside exponentiation unless carefully handled (usually at base)**

---

### 🔢 Rules of Modulo Arithmetic

Let `mod = 10⁹ + 7`, a large prime.
Suppose `a` and `b` are integers:

#### Addition

```
(a + b) % mod = ((a % mod) + (b % mod)) % mod
```

#### Subtraction

```
(a - b + mod) % mod = ensures non-negative result
```

#### Multiplication

```
(a * b) % mod = ((a % mod) * (b % mod)) % mod
```

#### Exponentiation

Use **modular exponentiation**: `(a^b) % mod`
This must be done carefully using a loop or recursion:

```js
function modPow(a, b, mod) {
  let result = 1;
  a = a % mod;

  while (b > 0) {
    if (b % 2 === 1) {
      result = (result * a) % mod;
    }
    a = (a * a) % mod;
    b = Math.floor(b / 2);
  }

  return result;
}
```

---

### 🔍 Example

**Avoid doing this:**

```js
let result = (Math.pow(5, 1e15) * Math.pow(4, 1e15)) % MOD; // ❌ Overflow
```

**Do this instead:**

```js
let res = (modPow(5, evenCount, MOD) * modPow(4, oddCount, MOD)) % MOD; // ✅
```

---

### 🧠 Best Practices

- Use `% mod` **after every step of computation** involving big numbers.
- When combining multiple operations, **mod after each multiplication or addition**.
- For large powers, **use modular exponentiation** (not built-in `Math.pow`).
- Use a **prime modulus (like 10⁹+7)** for well-behaved inverse properties if needed.

---

### 💡 In Summary

| Operation | Apply `mod` After                     |
| --------- | ------------------------------------- |
| `a + b`   | `((a % mod) + (b % mod)) % mod`       |
| `a - b`   | `((a % mod) - (b % mod) + mod) % mod` |
| `a * b`   | `((a % mod) * (b % mod)) % mod`       |
| `a^b`     | Use modular exponentiation            |

---
