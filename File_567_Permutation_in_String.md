



---

## 📁 Leetcode Solutions

| File No. | Problem Name          | Solution File                                                                |
| -------- | --------------------- | ---------------------------------------------------------------------------- |
| 567      | Permutation in String | [File\_567\_Permutation\_in\_String.md](./File_567_Permutation_in_String.md) |

---

## ✅ File\_567\_Permutation\_in\_String.md

````markdown
# 🔢 Leetcode 567: Permutation in String

### ✅ Problem Statement

Given two strings `s1` and `s2`, return `true` if `s2` contains a permutation of `s1`, or `false` otherwise.

A permutation of `s1` is any rearrangement of its characters. You need to check if any substring of `s2` has the same character counts as `s1`.

---

### ✨ Example

**Input:**  
`s1 = "ab"`  
`s2 = "eidbaooo"`

**Output:** `true`  
**Explanation:** `"ba"` is a permutation of `"ab"` and is a substring of `s2`.

---

### 🚀 Approach: Sliding Window + Frequency Map

We use:
- A sliding window of length equal to `s1`
- Frequency arrays of size 26 (for each lowercase letter)
- At each step, we compare the frequency maps

---

### 🧠 Dry Run

**Input:**  
`s1 = "ab"`  
`s2 = "eidbaooo"`

**Step-by-Step:**

1. `s1Map` → counts of `'a'` and `'b'` → `[1, 1, 0, ..., 0]`
2. First window in `s2` → `"ei"` → `[0, 0, 0, ..., 1, 1]`
3. Slide window:
   - `"id"` → still not matching
   - `"db"` → still not matching
   - `"ba"` → ✅ **matches `s1Map`**
4. Return `true`

---

### 🧾 Java Code

```java
public class Solution {
    public boolean checkInclusion(String s1, String s2) {
        if (s1.length() > s2.length()) return false;

        int[] s1Map = new int[26];
        int[] s2Map = new int[26];

        for (int i = 0; i < s1.length(); i++) {
            s1Map[s1.charAt(i) - 'a']++;
            s2Map[s2.charAt(i) - 'a']++;
        }

        for (int i = 0; i < s2.length() - s1.length(); i++) {
            if (matches(s1Map, s2Map)) return true;
            s2Map[s2.charAt(i) - 'a']--;
            s2Map[s2.charAt(i + s1.length()) - 'a']++;
        }

        return matches(s1Map, s2Map);
    }

    private boolean matches(int[] s1Map, int[] s2Map) {
        for (int i = 0; i < 26; i++) {
            if (s1Map[i] != s2Map[i]) return false;
        }
        return true;
    }
}
````

---

### 🧠 Time & Space Complexity

* **Time Complexity:** O(n)
* **Space Complexity:** O(1) (fixed-size arrays)

---

### 🎯 Summary

* This is a classic use case of **Sliding Window + Frequency Count**
* Perfect example to learn window-based comparison
* Works in linear time and constant space

---


```

---

Would you like me to generate a full `README.md` for your GitHub repo that lists all files like this?
```
