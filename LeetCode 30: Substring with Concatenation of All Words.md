
---

## 🔍 LeetCode 30: Substring with Concatenation of All Words

### 📘 Problem Statement

Given a string `s` and an array of strings `words`, where each word has the same length, return all starting indices of substring(s) in `s` that is a concatenation of each word in `words` exactly once and without any intervening characters.

The order of words in the concatenation can be any permutation.

---

### 🧪 Example

#### Input:
```java
s = "barfoothefoobarman"
words = ["foo", "bar"]
```

#### Output:
```java
[0, 9]
```

#### Explanation:
- Substring `"barfoo"` starting at index 0 is a valid concatenation.
- Substring `"foobar"` starting at index 9 is also valid.

---

### 🧠 Approach

We use a **fixed-size sliding window** combined with **hash maps** to efficiently check each possible substring of length `totalLen = wordLen × number of words`.

#### Steps:
1. Build a frequency map of the `words`.
2. Slide a window of size `totalLen` across `s`, starting from multiple offsets (0 to `wordLen - 1`).
3. At each step, extract words of length `wordLen` and compare their frequency with the original map.
4. If all words match in frequency, record the starting index.

---

### 💻 Java Code

```java
class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> res = new ArrayList<>();
        if (s == null || words == null || words.length == 0) return res;

        int len = words[0].length();
        int count = words.length;
        int totalLen = len * count;

        if (s.length() < totalLen) return res;

        Map<String, Integer> map = new HashMap<>();
        for (String w : words) {
            map.put(w, map.getOrDefault(w, 0) + 1);
        }

        for (int i = 0; i < len; i++) {
            int l = i, r = i, matched = 0;
            Map<String, Integer> window = new HashMap<>();

            while (r + len <= s.length()) {
                String word = s.substring(r, r + len);
                r += len;

                if (map.containsKey(word)) {
                    window.put(word, window.getOrDefault(word, 0) + 1);
                    matched++;

                    while (window.get(word) > map.get(word)) {
                        String leftWord = s.substring(l, l + len);
                        window.put(leftWord, window.get(leftWord) - 1);
                        l += len;
                        matched--;
                    }

                    if (matched == count) {
                        res.add(l);
                    }
                } else {
                    window.clear();
                    matched = 0;
                    l = r;
                }
            }
        }

        return res;
    }
}
```

---

### 🔍 Code Dry Run

#### Input:
```java
s = "barfoothefoobarman"
words = ["foo", "bar"]
```

- `wordLen = 3`, `count = 2`, `totalLen = 6`
- Valid substrings of length 6:
  - `"barfoo"` at index 0 → ✅
  - `"foobar"` at index 9 → ✅

The sliding window checks substrings of length 6 and uses a frequency map to validate them.

---

### 🪟 Why Fixed-Size Sliding Window?

We use a **fixed-size sliding window** because:
- The length of each valid substring is known in advance (`wordLen × count`)
- We can efficiently move the window in steps of `wordLen` and update our frequency map incrementally
- This avoids recomputing everything from scratch and improves performance

---

### ⏱️ Time & Space Complexity

| Type | Complexity |
|------|------------|
| Time | O(N × M × L) where N = length of `s`, M = number of words, L = word length |
| Space | O(M × L) for the frequency maps |

---

