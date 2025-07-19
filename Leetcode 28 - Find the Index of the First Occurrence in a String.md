
```

```

---

## 🔍 Leetcode 28 — Find the Index of the First Occurrence in a String

### 🧩 Problem Statement

Given two strings, `needle` and `haystack`, return the index of the **first occurrence** of `needle` in `haystack`. If `needle` is not part of `haystack`, return `-1`.

#### ⚠️ Edge Case
- If `needle` is an empty string, return `0`. This follows the convention that an empty string is found at the beginning of any string.

---

### ✏️ Test Cases

#### ✅ Test Case 1
```text
Input:  haystack = "sadbutsad", needle = "sad"
Output: 0
Explanation: "sad" occurs at index 0 and 6. The first match is at index 0.
```

#### ❌ Test Case 2
```text
Input:  haystack = "leetcode", needle = "leeto"
Output: -1
Explanation: "leeto" does not occur in "leetcode".
```

---

## 💻 Java Code – Substring Comparison

```java
public class Solution {
    public int strStr(String haystack, String needle) {
        if (needle.isEmpty()) return 0;

        for (int i = 0; i <= haystack.length() - needle.length(); i++) {
            String window = haystack.substring(i, i + needle.length());
            if (window.equals(needle)) {
                return i;
            }
        }

        return -1;
    }
}
```

---

## 🔁 Dry Run: Detailed Explanation

### Input
```java
haystack = "sadbutsad";
needle   = "sad";
```

### Loop Setup
- `needle.length()` = 3
- Loop from `i = 0` to `i = haystack.length() - needle.length()` → `i = 0 to 6`

### Iterations:

| Step | i | window = haystack.substring(i, i + 3) | Comparison     | Result |
|------|---|----------------------------------------|----------------|--------|
| 1    | 0 | `"sad"`                                | "sad" == "sad" | ✅ Match → return `0` |
| 2    | 1 | `"adb"`                                | != "sad"       | ❌     |
| 3    | 2 | `"dbu"`                                | ❌             |        |
| 4    | 3 | `"but"`                                | ❌             |        |
| 5    | 4 | `"uts"`                                | ❌             |        |
| 6    | 5 | `"tsa"`                                | ❌             |        |
| 7    | 6 | `"sad"`                                | ✅ Match, but first match already returned |

---

## 💬 Explain Like You're Teaching

- Loop through each starting index `i` where `needle` can fit in `haystack`.
- Slice `haystack` using `substring(i, i + needle.length())`.
- Compare that window to `needle` using `.equals()`.
- If a match is found, return the current index `i`.
- If `needle` is empty, return `0` directly.
- If no match is found after the loop finishes, return `-1`.

---

