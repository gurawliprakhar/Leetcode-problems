
---

## 📄 Problem Statement

> Given two strings `s` and `p`, return an array of all the start indices of `p`'s anagrams in `s`. You may return the answer in any order.  
>  
> An anagram is a permutation of letters — the order can differ, but the character counts must match.

---

## 🧪 Examples

### Example 1  
**Input:**  
`s = "cbaebabacd"`  
`p = "abc"`  
**Output:**  
`[0,6]`  
**Explanation:**  
Substrings `"cba"` (index 0) and `"bac"` (index 6) are valid anagrams of `"abc"`.

### Example 2  
**Input:**  
`s = "abab"`  
`p = "ab"`  
**Output:**  
`[0,1,2]`  
**Explanation:**  
Substrings `"ab"`, `"ba"`, and `"ab"` (starting at indices 0, 1, and 2) are all anagrams of `"ab"`.

---

## 🚀 Approach

We use a **fixed-size sliding window** of length `p.length()` and track character frequencies with two **HashMaps**:
- `pFreq`: frequency of characters in the pattern `p`
- `window`: dynamic frequency of characters in the current sliding window of `s`

At each step, we compare the `window` map with `pFreq`. If they match, we record the starting index.

---

## 💻 Code: HashMap + Sliding Window

```java
public List<Integer> findAnagrams(String s, String p) {
    List<Integer> res = new ArrayList<>();
    if (s.length() < p.length()) return res;

    Map<Character, Integer> pFreq = new HashMap<>();
    Map<Character, Integer> window = new HashMap<>();

    for (char c : p.toCharArray()) {
        pFreq.put(c, pFreq.getOrDefault(c, 0) + 1);
    }

    int windowSize = p.length();

    for (int i = 0; i < s.length(); i++) {
        char cur = s.charAt(i);
        window.put(cur, window.getOrDefault(cur, 0) + 1);

        if (i >= windowSize) {
            char toRemove = s.charAt(i - windowSize);
            if (window.get(toRemove) == 1) {
                window.remove(toRemove);
            } else {
                window.put(toRemove, window.get(toRemove) - 1);
            }
        }

        if (window.equals(pFreq)) {
            res.add(i - windowSize + 1);
        }
    }

    return res;
}
```

---

## 🧵 Dry Run: `"cbaebabacd"` with `"abc"`

| Index `i` | Current Char | Window State After Add & Remove | Match with `pFreq`? | `res` |
|-----------|--------------|-------------------------------|----------------------|-------|
| 0         | `'c'`        | `{c=1}`                        | ❌                    | []    |
| 1         | `'b'`        | `{c=1, b=1}`                   | ❌                    | []    |
| 2         | `'a'`        | `{c=1, b=1, a=1}`              | ✅                    | [0]   |
| 3         | `'e'`        | `{b=1, a=1, e=1}`              | ❌                    | [0]   |
| 4–5       | `'b'`, `'a'` | Updates, no match              | ❌                    | [0]   |
| 6         | `'c'`        | `{a=1, b=1, c=1}`              | ✅                    | [0,6] |

✅ Final Output: `[0,6]`

---

