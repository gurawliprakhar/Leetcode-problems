

---

# 🚀 Minimum Window Substring (LeetCode 76)

## 📚 Problem Description:

Given two strings `s` and `t`, find the **smallest substring (window)** in `s` that contains **all the characters from `t` (including duplicates)**.

If there is **no such substring**, return an **empty string**.

---

## ✅ Problem Explanation (In Simple Words):

You are given:

* **s** = A big string (like a paragraph or sentence)
* **t** = A small string (set of characters you must find in s)

Your task:

> Find the **shortest substring** inside `s` that contains **every character from `t` (with correct frequency)**.

---

## ✅ Example Walkthrough:

### Example 1:

**Input:**

```
s = "ADOBECODEBANC"
t = "ABC"
```

**Output:**

```
"BANC"
```

**Why?**

We want the smallest substring in `s` that contains:

* **A**
* **B**
* **C**

✅ Possible windows:

* `"ADOBEC"`
* `"ADOBECODEBA"`
* `"BANC"` ✅ (smallest)

---

### Example 2:

**Input:**

```
s = "a"
t = "a"
```

**Output:**

```
"a"
```

---

### Example 3:

**Input:**

```
s = "a"
t = "aa"
```

**Output:**

```
""
```

Because `s` does not contain enough `'a'`s.

---

## ✅ Algorithm Used:

**Variable Size Sliding Window with Two Pointers (i, j)**

Steps:

1. Use two pointers `i` and `j` to represent the current window in `s`.
2. Expand the window (move `j` right) until it contains all characters from `t`.
3. Shrink the window (move `i` right) to minimize the window while still satisfying the condition.
4. Keep track of the smallest window found.

---

## ✅ Java Code:

```java
import java.util.*;

class Solution {
    public String minWindow(String s, String t) {
        if (s.length() == 0 || t.length() == 0) {
            return "";
        }

        // Count characters in t
        Map<Character, Integer> map = new HashMap<>();
        for (char c : t.toCharArray()) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }

        int i = 0, j = 0;
        int formed = 0;
        int required = map.size();

        Map<Character, Integer> window = new HashMap<>();
        int min = Integer.MAX_VALUE;
        int minL = 0;

        while (j < s.length()) {
            char c = s.charAt(j);
            window.put(c, window.getOrDefault(c, 0) + 1);

            if (map.containsKey(c) && window.get(c).intValue() == map.get(c).intValue()) {
                formed++;
            }

            while (i <= j && formed == required) {
                if (j - i + 1 < min) {
                    min = j - i + 1;
                    minL = i;
                }

                char leftC = s.charAt(i);
                window.put(leftC, window.get(leftC) - 1);

                if (map.containsKey(leftC) && window.get(leftC).intValue() < map.get(leftC).intValue()) {
                    formed--;
                }

                i++;
            }

            j++;
        }

        if (min == Integer.MAX_VALUE) {
            return "";
        } else {
            return s.substring(minL, minL + min);
        }
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        String s = "ADOBECODEBANC";
        String t = "ABC";
        String result = solution.minWindow(s, t);
        System.out.println("Output: " + result);  // Output: BANC
    }
}
```

---

## ✅ Dry Run (Step-by-step for Input `"ADOBECODEBANC", "ABC"`):

| Step      | Window (i to j) | Current Window | Characters Found           | Formed     |
| --------- | --------------- | -------------- | -------------------------- | ---------- |
| Start     | 0-0             | `"A"`          | A                          | 1          |
| Expand    | 0-3             | `"ADOB"`       | A, B                       | 2          |
| Expand    | 0-5             | `"ADOBEC"`     | A, B, C                    | 3 (target) |
| Shrink    | 1-5             | `"DOBEC"`      | ✅                          |            |
| Shrink    | 2-5             | `"OBEC"`       | ✅                          |            |
| Shrink    | 3-5             | `"BEC"`        | ✅ Smallest window till now |            |
| Continue  | ...             | ...            | ...                        | ...        |
| Next Best | 9-11            | `"BANC"`       | ✅ Smaller window           |            |

✅ **Final Answer:** `"BANC"`

---

## ✅ Time and Space Complexity:

| Complexity | Value                                            |
| ---------- | ------------------------------------------------ |
| Time       | O(m + n), where m = length of s, n = length of t |
| Space      | O(n), for storing character frequency maps       |

---

## ✅ Similar Problems:

* Longest Substring Without Repeating Characters
* Minimum Size Subarray Sum
* Longest Substring with At Most K Distinct Characters

---


