E
---

# 🚀 Longest Substring Without Repeating Characters (Java - Sliding Window Approach)

## ✅ Problem Statement:

Given a string `s`, find the **length of the longest substring without repeating characters**.

### 📋 Example:

For input:

```
s = "abcabcbb"
```

Expected output:

```
3
```

**Explanation:**
The longest substring without repeating characters is `"abc"`, which has length `3`.

---

## ✅ Why Use Sliding Window?

This problem requires checking **all possible substrings** while ensuring **no repeating characters**.
Using brute force with nested loops would take **O(n²)** time.

✅ **Sliding Window** helps by:

* Keeping track of a **dynamic window (substring)** that satisfies the condition (all unique characters).
* Moving the window **forward efficiently** whenever a duplicate character is found.
* Solving the problem in **O(n) time complexity**, which is much faster.

---

## ✅ Which Sliding Window Type?

| Property    | Type                                                                                        |
| ----------- | ------------------------------------------------------------------------------------------- |
| Window Size | ✅ **Variable Size Window**                                                                  |
| Why?        | The size of the substring **grows and shrinks dynamically** based on character repetitions. |

---

## ✅ Java Code (Your Code)

```java
import java.util.HashSet;
import java.util.Set;

class Solution {
    public int lengthOfLongestSubstring(String s) {
        int i = 0;
        int longSub = 0;

        Set<Character> set = new HashSet<>();

        for (int j = 0; j < s.length(); j++) {
            char cur = s.charAt(j);

            // If duplicate found, shrink the window from the start
            while (set.contains(cur)) {
                set.remove(s.charAt(i));
                i++;
            }

            // Add current character to the set
            set.add(cur);

            // Update the maximum length found so far
            longSub = Math.max(longSub, j - i + 1);
        }

        return longSub;
    }
}
```

---

## ✅ Dry Run (For Input `"abcabcbb"`):

| Step | `i` | `j` | Current Char | Set Contents                  | Action                 | longSub |
| ---- | --- | --- | ------------ | ----------------------------- | ---------------------- | ------- |
| 1    | 0   | 0   | a            | {a}                           | Add 'a'                | 1       |
| 2    | 0   | 1   | b            | {a, b}                        | Add 'b'                | 2       |
| 3    | 0   | 2   | c            | {a, b, c}                     | Add 'c'                | 3 ✅     |
| 4    | 0→1 | 3   | a            | {b, c, a} → remove 'a' at i=0 | Shrink window          | 3       |
| 5    | 1→2 | 4   | b            | {c, a, b} → remove 'b' at i=1 | Shrink window          | 3       |
| 6    | 2→3 | 5   | c            | {a, b, c} → remove 'c' at i=2 | Shrink window          | 3       |
| 7    | 3→5 | 6   | b            | {b}                           | Shrink to remove old b | 3       |
| 8    | 5→7 | 7   | b            | {b}                           | Shrink to remove old b | 3       |

---

✅ **Final Answer:**

```
3
```

---

## ✅ Algorithm Explanation:

* **Two pointers:**

  * `i` → Start of the window
  * `j` → End of the window (looping through string)

* **HashSet:**
  Tracks unique characters in the current window.

* **If duplicate found:**
  Shrink the window from the start until the duplicate is removed.

* **Window Size:**
  `(j - i + 1)` → Length of the current unique substring.

* **Update `longSub`:**
  Keeps track of the **maximum length** found.

---

## ✅ Time and Space Complexity:

| Complexity | Value |
| ---------- | ----- |
| Time       | O(n)  |
| Space      | O(n)  |

Where `n = length of the string`.

---

## ✅ When to Use This Sliding Window Approach:

✔️ When the problem involves **contiguous substrings**
✔️ When you need to **track unique elements within a range**
✔️ When input size is large and you need **O(n)** performance

---


