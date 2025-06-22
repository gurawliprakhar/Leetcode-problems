

---

# 🔢 LeetCode 3085 — Minimum Deletions to Make String K-Special

> **Tag**: Greedy, HashMap, String
> **Difficulty**: Medium
> **Language**: Java

---

## 🧩 Problem Summary

You are given a string `word` and an integer `k`. Your goal is to delete characters from `word` to make it **k-special**.

### A string is k-special if:

> For **every pair of characters** in the string,
> `|frequency(char1) - frequency(char2)| ≤ k`

Your task is to return the **minimum number of deletions** required to make the string k-special.

📘 **LeetCode Link:** [Problem 3085 - Minimum Deletions to Make String K-Special](https://leetcode.com/problems/minimum-deletions-to-make-string-k-special/)

---

## 🧠 Example

### Input:

```java
word = "dabdcbdcdcd"
k = 2
```

### Character Frequencies:

```
'd' → 5  
'a' → 1  
'b' → 2  
'c' → 3
```

### Output:

```java
2
```

### Explanation:

* Delete `'a'` (1) and 1 `'d'` → frequencies become `{b=2, c=3, d=4}`.
* All frequency differences are within `k = 2`.

✅ Total deletions = **2**

---

## 💡 Approach

We use a **greedy** strategy combined with **frequency bucketing**.

### Steps:

1. Count frequencies of each character using a `HashMap`.
2. Try every frequency `x` as the **minimum target**.
3. For each frequency `f` in the list:

   * If `f < x`: delete all occurrences (too small).
   * If `f > x + k`: delete `f - (x + k)` characters (too large).
4. Track the **minimum deletions** needed across all `x`.

---

## 🚀 Java Solution

```java
class Solution {
    public int minimumDeletions(String word, int k) {
        HashMap<Character, Integer> map = new HashMap<>();

        // Step 1: Frequency count
        for (char c : word.toCharArray()) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }

        // Step 2: Store non-zero frequencies
        List<Integer> list = new ArrayList<>();
        for (int freq : map.values()) {
            list.add(freq);
        }

        // Step 3: Try every frequency as base frequency
        int res = Integer.MAX_VALUE;
        for (int x : list) {
            int cur = 0;
            for (int f : list) {
                if (f < x) {
                    cur += f; // delete all
                } else if (f > x + k) {
                    cur += f - (x + k); // delete excess
                }
            }
            res = Math.min(res, cur);
        }

        return res;
    }
}
```

---

## 🔍 Dry Run Example

With `list = [1, 2, 3, 5]` and `k = 2`:

| Base `x` | Range `[x, x+k]` | Deletions |
| -------- | ---------------- | --------- |
| 1        | \[1, 3]          | 2         |
| 2        | \[2, 4]          | 2         |
| 3        | \[3, 5]          | 3         |
| 5        | \[5, 7]          | 6         |

✅ **Minimum deletions = 2**

---

## 📊 Complexity

| Type       | Value     |
| ---------- | --------- |
| Time       | O(26²)    |
| Space      | O(26)     |
| Input size | Up to 10⁵ |

---

## 🧪 Test Cases

```java
Input: word = "aabbcc", k = 0  
Output: 4  
// Only one character type can remain if all frequencies must be equal.

Input: word = "abcabc", k = 1  
Output: 0  
// All characters occur 2 times → already k-special.

Input: word = "a", k = 0  
Output: 0  
```

---

## 🧾 Requirements

* Java 8+
* No external libraries required

---

## 🙌 Let's Connect

* 💼 [LinkedIn](https://www.linkedin.com/)
* 🧠 [Medium](https://medium.com/)
* ☕ Follow for more solutions like this one!

---

If you found this helpful, feel free to ⭐ star the repository, fork it, and submit PRs for improvements!

---


