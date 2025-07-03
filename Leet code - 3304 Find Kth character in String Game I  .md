
# 🔤 Find the K-th Character in String Game I

This repository contains a Java solution to the **"Find the K-th Character in String Game I"** problem.

---

## ✅ Problem Explanation

Alice and Bob are playing a string game. Here's how it works:

- The game **starts with** the string `"a"`.
- In each operation:
  1. For every character `c` in the current string, replace it with its **next character** in the English alphabet.
  2. Append the resulting string to the original.

> ⚠️ Note: If a character is `'z'`, it wraps around to `'a'`.

---

### 🎯 Objective

Given an integer `k`, return the **k-th character** (1-based index) in the final string after enough operations so that the string has at least `k` characters.

---

## 🔁 Example Walkthrough

### Input:
```

k = 10

````

### Step-by-step Simulation:

1. Start with `"a"`
2. Next: `'a' → 'b'` → Append `"b"` → `"ab"`
3. `'a' → 'b'`, `'b' → 'c'` → Append `"bc"` → `"abbc"`
4. `'a' → 'b'`, `'b' → 'c'`, `'b' → 'c'`, `'c' → 'd'` → Append `"bccd"` → `"abbcbccd"`
5. `'a' → 'b'`, `'b' → 'c'`, `'b' → 'c'`, `'c' → 'd'`, `'b' → 'c'`, `'c' → 'd'`, `'c' → 'd'`, `'d' → 'e'` → Append `"bccdccde"`  
   → Final: `"abbcbccdbccdccde"`

✅ The 10th character is **`'c'`**

---

## 💻 Java Code

**File**: `Solution.java`

```java
class Solution {
    public char kthCharacter(int k) {
        String word = "a";

        while (word.length() < k) {
            int n = word.length();
            char[] next = new char[n];

            for (int i = 0; i < n; i++) {
                char c = word.charAt(i);
                next[i] = (char) ((c - 'a' + 1) % 26 + 'a');
            }

            word += new String(next);
        }

        return word.charAt(k - 1);
    }
}
````

---

## 🧪 Dry Run for `k = 10`

### Initial State:

```text
word = "a"
```

### Iteration 1:

* Original: `"a"`
* Next: `"b"`
* Combined: `"ab"`

### Iteration 2:

* Original: `"ab"`
* Next: `"bc"`
* Combined: `"abbc"`

### Iteration 3:

* Original: `"abbc"`
* Next: `"bccd"`
* Combined: `"abbcbccd"`

### Iteration 4:

* Original: `"abbcbccd"`
* Next: `"bccdccde"`
* Combined: `"abbcbccdbccdccde"` → Length = 16 ≥ 10

### Result:

* `k = 10` → character at index `9` (0-based) is `'c'`

✅ Output: `'c'`

---

## 📊 Complexity Analysis

| Metric           | Value              |
| ---------------- | ------------------ |
| Time Complexity  | `O(n)` (up to 500) |
| Space Complexity | `O(n)`             |

Due to the small constraint `k ≤ 500`, this simulation approach is efficient.

---

## 📁 Repository Structure

```
📂 FindKthCharacterGame
├── 📄 README.md
└── 📄 Solution.java
```

---

## 🙌 Author

Crafted with ❤️ by Prakhar Tripathi

---

---

```
```
