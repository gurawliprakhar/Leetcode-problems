
---

```markdown
# 🚀 LeetCode 2014 – Longest Subsequence Repeated k Times

## 📚 Problem Statement

Given:

- A string `s`
- An integer `k` (`k ≥ 2`)

Your task is to **find the longest string `t`** such that:

- Repeating `t` exactly `k` times (concatenating `t` `k` times) results in a string that is a **subsequence of `s`**.
- Among all possible such strings, return the **lexicographically largest** one.

If no such string exists, return `""` (empty string).

---

## ✅ What Is a Subsequence?

A **subsequence** of a string is formed by deleting zero or more characters **without changing the relative order** of the remaining characters.

For example:

| String | Subsequence | Is Valid? |
|------|-----------|----|
| `a_b_c_d` | `abc` | ✅ |
| `ctaa` | `cat` | ❌ |

---

## 🎯 Example

**Input:**
```

s = "letsleetcode"
k = 2

```

**Output:**
```

"let"

````

### Explanation:

Some possible strings `t` such that `t*k` is a subsequence of `s`:

- `"let"` → `"letlet"` is a subsequence ✅
- `"ete"` → `"eteete"` is also a subsequence ✅

Between `"let"` and `"ete"`, **`"let"` is lexicographically larger**, so it is returned.

---

## 🧠 Approach and Intuition

### Step 1: Frequency Filtering (Pruning the Search Space)
We only need characters that appear at least `k` times in `s`.  
Why?  
Because for `t*k` to exist in `s`, **every character in `t` must appear at least `k` times**.

We:

- Build a **frequency map** of characters in `s`
- Keep only characters with `count ≥ k`
- Sort these characters in **reverse lexicographical order (from `'z'` to `'a'`)**

---

### Step 2: BFS (Breadth-First Search) Traversal using Queue
We perform **level-wise BFS**:

- Start with an empty string.
- At each level:
  - For every string currently in the queue, append each valid character (from our filtered list).
  - Check if this new string, when repeated `k` times, is still a subsequence of `s`.
  - If yes → Add to queue for the next level.

Why BFS?

- It explores **shorter strings first** (satisfying the length constraint).
- It explores **lexicographically larger strings first** at each level (since we iterate characters in reverse lex order).

---

### Step 3: Subsequence Validation (The `isValid()` Function)
For each candidate string `t`:

- Form `t*k`
- Check if this expanded string exists as a subsequence of `s`.

How?

- Use a **two-pointer approach**.
- Loop over `s` and check if characters of `t*k` appear **in order**.

---

## ✅ Full Java Solution

```java
import java.util.*;

public class Solution {
    public String longestSubsequenceRepeatedK(String s, int k) {
        // Step 1: Frequency count
        Map<Character, Integer> freqMap = new HashMap<>();
        for (char ch : s.toCharArray()) {
            freqMap.put(ch, freqMap.getOrDefault(ch, 0) + 1);
        }

        // Step 2: Filter characters with count >= k
        List<Character> validChars = new ArrayList<>();
        for (char ch = 'z'; ch >= 'a'; ch--) {
            if (freqMap.getOrDefault(ch, 0) >= k) {
                validChars.add(ch);
            }
        }

        // Step 3: BFS initialization
        Queue<String> queue = new LinkedList<>();
        queue.offer("");
        String result = "";

        // Step 4: BFS traversal
        while (!queue.isEmpty()) {
            String current = queue.poll();
            for (char ch : validChars) {
                String next = current + ch;
                if (isValid(s, next, k)) {
                    queue.offer(next);
                    if (next.length() > result.length() ||
                       (next.length() == result.length() && next.compareTo(result) > 0)) {
                        result = next;
                    }
                }
            }
        }

        return result;
    }

    // Helper function to check if (sub * k) is a subsequence of s
    private boolean isValid(String s, String sub, int k) {
        int i = 0, count = 0;
        for (char ch : s.toCharArray()) {
            if (ch == sub.charAt(i)) {
                i++;
                if (i == sub.length()) {
                    i = 0;
                    count++;
                    if (count == k) return true;
                }
            }
        }
        return false;
    }
}
````

---

## 🧪 Dry Run Example: `"letsleetcode", k = 2`

### Step 1: Frequency Map:

| Char | Frequency |
| ---- | --------- |
| l    | 2         |
| e    | 4         |
| t    | 2         |
| s    | 1         |
| c    | 1         |
| o    | 1         |
| d    | 1         |

---

### Step 2: Valid Characters (≥ k):

```
['t', 'l', 'e']
```

*(In reverse lex order)*

---

### Step 3: BFS Queue Evolution:

| BFS Level | Queue Contents   | Result                  |
| --------- | ---------------- | ----------------------- |
| Start     | \[""]            | ""                      |
| Level 1   | \["t", "l", "e"] | "t" → "l" → "e"         |
| Level 2   | \["tt", "et"]    | "tt"                    |
| Level 3   | \["ete", "let"]  | Finally becomes "let" ✅ |

---

### Subsequence Checking for "let":

For `k=2`, check if `"letlet"` exists as a subsequence in `"letsleetcode"`.

Step-by-step matching:

| s.charAt(j) | Current Target | Match? | Subsequence progress |
| ----------- | -------------- | ------ | -------------------- |
| l           | l              | ✅      | 1st                  |
| e           | e              | ✅      | 1st                  |
| t           | t              | ✅      | Complete 1st         |
| l           | l              | ✅      | 2nd                  |
| e           | e              | ✅      | 2nd                  |
| t           | t              | ✅      | Complete 2nd ✅       |

Thus, `"letlet"` is a subsequence.

---

## ⏱️ Time Complexity:

| Operation                       | Complexity                                                            |   |   |
| ------------------------------- | --------------------------------------------------------------------- | - | - |
| Frequency count                 | O(n)                                                                  |   |   |
| Subsequence check per candidate | O(n ×                                                                 | t | ) |
| BFS exploration                 | Exponential in worst case (depends on candidate set size & max depth) |   |   |

Where `n = length of s`, and \`|t| = length of candidate string.

---

## 🧮 Space Complexity:

| Structure             | Space                                            |
| --------------------- | ------------------------------------------------ |
| Frequency Map         | O(1) (since max 26 lowercase letters)            |
| Valid Characters List | O(1)                                             |
| BFS Queue             | Depends on candidate string length and branching |
| Overall               | Space scales with BFS levels and candidate pool  |

---

## ✅ Key Takeaways:

* 🔑 **Prune the search space early** by filtering characters with low frequency.
* 🔑 **BFS ensures shortest-length-first & lexicographical order priority**.
* 🔑 Use a **queue** for BFS and a **two-pointer technique** for subsequence checking.
* 🔑 The combination of **character filtering + BFS + lex order** makes the solution both correct and efficient.

---

## ⭐️ If You Found This Helpful:

Please ⭐️ star the repository!
Feel free to fork and use this for your interview prep or coding practice.

Happy coding! 👨‍💻👩‍💻✨

```

---

```
