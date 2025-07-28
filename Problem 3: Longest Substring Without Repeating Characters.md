
---

# 🧮 Problem 3 - Longest Substring Without Repeating Characters

## 📘 Problem Statement  
Ek string `s` di gayi hai. Aapko **longest substring without repeating characters** ka length find karna hai.

---

## 🧠 Approach — Sliding Window + HashSet  

Window expand karte raho jab tak characters unique ho.  
Duplicate milte hi left pointer ko aage badhao aur set se remove karte jao, taaki window fir se unique ho jaaye.

---

## 🔍 Dry Run – `"pwwkew"`

| Right | Char | Kya Hua?                                                             | Left | Window         | maxLen |
|-------|------|---------------------------------------------------------------------|------|----------------|--------|
| 0     | 'p'  | Unique, add kiya → `{p}`                                            | 0    | {p}            | 1      |
| 1     | 'w'  | Unique, add kiya → `{p, w}`                                         | 0    | {p, w}         | 2      |
| 2     | 'w'  | Duplicate! Remove 'p' aur 'w' → left = 2                            | 2    | { }            | 2      |
|       |      | 'w' add back → `{w}`                                                | 2    | {w}            | 2      |
| 3     | 'k'  | Add kiya → `{w, k}`                                                 | 2    | {w, k}         | 2      |
| 4     | 'e'  | Add kiya → `{w, k, e}` → `maxLen = 3`                               | 2    | {w, k, e}      | 3      |
| 5     | 'w'  | Duplicate! Remove 'w' → left = 3 → Add 'w' again → `{k, e, w}`      | 3    | {k, e, w}      | 3      |

🔚 Final Output: **3**

---

## 💻 Java Code

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Set<Character> wdw = new HashSet<>();
        int i = 0, maxLen = 0;

        for (int j = 0; j < s.length(); j++) {
            char cur = s.charAt(j);
            while (wdw.contains(cur)) {
                wdw.remove(s.charAt(i));
                i++;
            }
            wdw.add(cur);
            maxLen = Math.max(maxLen, j - i + 1);
        }
        return maxLen;
    }
}
```

---

## 📊 Complexity

- ⏱ **Time:** O(n) – Har character ek baar window mein aata hai aur ek baar remove hota hai  
- 🧠 **Space:** O(m) – jahan `m` charset size hai (a-z, A-Z, etc.)

---

