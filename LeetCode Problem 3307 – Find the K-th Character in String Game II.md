

---

# 🚀 LeetCode 3307 - Find the K-th Character in String Game II

> 📌 **Difficulty**: Hard
> 🧠 **Tag**: Reverse Simulation, String, Math

---

## 🧩 Problem Description

You start with a string `s = "a"` and apply a series of operations defined by an array:

Each element of `operations[]` is either:

* `0`: Duplicate the current string and append it to itself → `s = s + s`
* `1`: Shift every character of the current string by one position forward (with `'z'` → `'a'`) and append the result → `s = s + shift(s)`

After all operations, the resulting string becomes very large (up to 10¹⁴ characters).

### 🧠 Task

Given the array `operations[]` and an integer `k`, return the `k-th` character (1-based index) in the final string — **without building the full string**.

---

## 📘 Example

```java
Input:
operations = [0, 1, 0, 1]
k = 10

Output:
'b'
```

### 🧮 Step-by-Step Breakdown

Start with: `"a"`

| Step | Operation | Resulting String                                 |
| ---- | --------- | ------------------------------------------------ |
| 1    | 0         | `"aa"`                                           |
| 2    | 1         | `"aa" + "bb"` → `"aabb"`                         |
| 3    | 0         | `"aabb" + "aabb"` → `"aabbaabb"`                 |
| 4    | 1         | `"aabbaabb" + "bbccbbcc"` → `"aabbaabbbbccbbcc"` |

We want the **10th character**, which is `'b'`.

---

## 🔁 Key Insight

You cannot build the entire string — it's too large.
Instead, **simulate in reverse**:

* Keep track of the current total string length.
* For each operation in reverse:

  * If `k` is in the **second half**, move it to the **first half**.
  * If the operation was a **shift**, increment a shift counter.
* After reversing all operations, apply the final shift to `'a'` to get the result.

---

## 👨‍💻 Java Solution

```java
public class Solution {
    public char findKthCharacter(int[] operations, long k) {
        int shift = 0;
        long len = 1;

        // Compute total length after all operations
        for (int op : operations) {
            len *= 2;
        }

        // Reverse simulate
        for (int i = operations.length - 1; i >= 0; i--) {
            len /= 2;
            if (k > len) {
                k -= len;
                if (operations[i] == 1) {
                    shift++;
                }
            }
        }

        // Apply shift to initial character 'a'
        return (char)((shift % 26) + 'a');
    }
}
```

---

## 🔎 Dry Run

### Input:

```java
operations = [0, 1, 0, 1];
k = 10;
```

### Reverse Simulation Steps:

| Step | op | len    | k > len? | New k | Shift Count |
| ---- | -- | ------ | -------- | ----- | ----------- |
| 3    | 1  | 16 → 8 | ✅        | k = 2 | shift = 1   |
| 2    | 0  | 8 → 4  | ❌        | k = 2 | shift = 1   |
| 1    | 1  | 4 → 2  | ❌        | k = 2 | shift = 1   |
| 0    | 0  | 2 → 1  | ✅        | k = 1 | shift = 1   |

### Final character:

```java
(char)((1 % 26) + 'a') = (char)(1 + 'a') = 'b'
```

✅ Answer: **`'b'`**

---

## ⏱️ Complexity

| Metric   | Value |
| -------- | ----- |
| ⌛ Time   | O(n)  |
| 🧠 Space | O(1)  |

* `n` = number of operations
* Constant space used — no string is built

---

## 🧠 Learnings

* Simulating **in reverse** is often the key to solving problems with exponential growth.
* Tracking indices and transformations backward is more efficient than forward building in such cases.

---

## 🧪 Test Cases

```java
Input: operations = [0, 0, 0, 0], k = 8
Output: 'a'

Input: operations = [1, 1, 1], k = 5
Output: 'd'

Input: operations = [0, 1, 0, 1], k = 10
Output: 'b'
```

---

## 📚 Related Problems

* LeetCode 880 – Decoded String at Index
* LeetCode 394 – Decode String
* LeetCode 2276 – Count Integers in Intervals

---



---
