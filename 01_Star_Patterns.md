# 🌟 Star Patterns

## ✅ Fundamental Structure of Star Pattern Code:

### 🔁 Outer `for` loop → **Controls the number of rows**

### 🔁 Inner `for` loop(s) → **Controls what goes inside each row (content)**

## 🧠 Tip:

Think of the inner loops like **painting the row horizontally**, while the outer loop **moves the brush down row by row**.

## 🔹 1. Left-Aligned Triangle

### Pattern:

```
*
* *
* * *
* * * *
* * * * *
```

### 💡 Intuition:

- This pattern **grows row by row**.
- Each row `i` has exactly `i` stars.

### ✅ Code:

```javascript
function leftAlignedTriangle(n) {
  for (let i = 1; i <= n; i++) {
    let row = "";
    for (let j = 1; j <= i; j++) {
      row += "* ";
    }
    console.log(row);
  }
}
leftAlignedTriangle(5);
```

### 📌 Loops:

- Outer loop: rows → `1 to n`
- Inner loop: stars → `1 to i`

---

## 🔹 2. Right-Aligned Triangle

### Pattern:

```
        *
      * *
    * * *
  * * * *
* * * * *
```

### 💡 Intuition:

- Similar to left triangle, but **right-aligned** using **spaces**.
- Each row `i` has `(n - i)` spaces and `i` stars.

### ✅ Code:

```javascript
function rightAlignedTriangle(n) {
  for (let i = 1; i <= n; i++) {
    let spaces = "  ".repeat(n - i); // 2 spaces for better alignment
    let stars = "* ".repeat(i);
    console.log(spaces + stars);
  }
}
rightAlignedTriangle(5);
```

### 📌 Loops:

- Print spaces: `n - i` times
- Print stars: `i` times

---

## 🔹 3. Pyramid Pattern

### Pattern:

```
    *
   * *
  * * *
 * * * *
* * * * *
```

### 💡 Intuition:

- It’s a **centered triangle**.
- For row `i`: we need `n - i` spaces and `i` stars.
- Space is printed before stars to center the pattern.

### ✅ Code:

```javascript
function pyramidPattern(n) {
  for (let i = 1; i <= n; i++) {
    let spaces = " ".repeat(n - i);
    let stars = "* ".repeat(i);
    console.log(spaces + stars);
  }
}
pyramidPattern(5);
```

---

## 🔹 4. Inverted Pyramid

### Pattern:

```
* * * * *
 * * * *
  * * *
   * *
    *
```

### 💡 Intuition:

- It’s the **upside-down version** of a pyramid.
- For row `i`: print `(n - i)` spaces, and `i` stars.

### ✅ Code:

```javascript
function invertedPyramid(n) {
  for (let i = n; i >= 1; i--) {
    let spaces = " ".repeat(n - i);
    let stars = "* ".repeat(i);
    console.log(spaces + stars);
  }
}
invertedPyramid(5);
```

---

## 🔹 5. Diamond Pattern

### Pattern:

```
   *
  * *
 * * *
  * *
   *
```

### 💡 Intuition:

- It’s a **pyramid + inverted pyramid**.
- First half grows, second half shrinks.

### ✅ Code:

```javascript
function diamondPattern(n) {
  for (let i = 1; i <= n; i++) {
    console.log(" ".repeat(n - i) + "* ".repeat(i));
  }
  for (let i = n - 1; i >= 1; i--) {
    console.log(" ".repeat(n - i) + "* ".repeat(i));
  }
}
diamondPattern(3);
```

---

## 🔹 6. Hollow Square Pattern

### Pattern:

```
* * * * *
*       *
*       *
*       *
* * * * *
```

### 💡 Intuition:

- The border is filled with stars, inside is empty.
- Use condition to check: if we're on the border (`i === 1 || i === n || j === 1 || j === n`) then print `*`, else space.

### ✅ Code:

```javascript
function hollowSquare(n) {
  for (let i = 1; i <= n; i++) {
    let row = "";
    for (let j = 1; j <= n; j++) {
      if (i === 1 || i === n || j === 1 || j === n) {
        row += "* ";
      } else {
        row += "  ";
      }
    }
    console.log(row);
  }
}
hollowSquare(5);
```

---

## 🔹 7. Butterfly Pattern

### Pattern:

```
*       *
* *     * *
* * *   * * *
* * * * * * *
```

### 💡 Intuition:

- It has two mirrored triangles with spaces in the middle.
- For each row `i`:

  - Print `i` stars
  - Print `2*(n-i)` spaces
  - Print `i` stars again

### ✅ Code:

```javascript
function butterflyPattern(n) {
  for (let i = 1; i <= n; i++) {
    let stars = "* ".repeat(i);
    let spaces = "  ".repeat(2 * (n - i));
    console.log(stars + spaces + stars);
  }
}
butterflyPattern(4);
```

---

## 🧠 How to Build Intuition

To understand and build your own star patterns:

1. **Draw pattern on paper**.
2. Count:

   - Number of **rows**
   - Number of **spaces** and **stars** in each row.

3. Use **nested loops**:

   - Outer loop → Rows
   - Inner loops → For spaces and stars separately

4. Combine parts as strings, then `console.log`.

---

## 📦 Summary Table

| Pattern Name     | Stars Logic           | Spaces Logic          |
| ---------------- | --------------------- | --------------------- |
| Left Triangle    | `j ≤ i`               | None                  |
| Right Triangle   | `j ≤ i`               | `n - i`               |
| Pyramid          | `j ≤ i`               | `n - i`               |
| Inverted Pyramid | `j ≤ i`               | `n - i`               |
| Diamond          | Growing + Shrinking   | `n - i`               |
| Hollow Square    | Border check          | Inner space condition |
| Butterfly        | `i`, spaces, then `i` | `2*(n - i)`           |

---
