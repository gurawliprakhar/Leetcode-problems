--

# 🚀 Leetcode 424 - Longest Repeating Character Replacement

## 🧩 Problem Statement

You are given a string `s` consisting of only **uppercase English letters**. You are also given an integer `k`.

🔁 You can replace **at most `k` characters** in the string with **any uppercase letter** (A-Z).

🎯 Your task is to find the **length of the longest substring** containing the same letter after performing at most `k` replacements.

---

## 📌 Constraints

* `1 <= s.length <= 10⁵`
* `s` consists only of uppercase English letters
* `0 <= k <= s.length`

---

## 🧪 Examples

### Example 1:

```
Input: s = "ABAB", k = 2  
Output: 4  
Explanation: Replace two 'A's with 'B', resulting in "BBBB".
```

### Example 2:

```
Input: s = "AABABBA", k = 1  
Output: 4  
Explanation: Replace one 'A' with 'B' to get "AABBBBA" → longest substring = "BBBB"
```

---

## ✅ Approach: Sliding Window + Frequency Map

We use a sliding window approach:

* Track the frequency of characters in the current window.
* Maintain `maxFreq`, the count of the most frequent character.
* If characters to change (`window size - maxFreq`) exceed `k`, shrink the window from the left.
* Keep updating the maximum window size (`maxLen`).

---

## 📦 Java Code

```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int characterReplacement(String s, int k) {
        Map<Character, Integer> map = new HashMap<>();
        int i = 0, maxFreq = 0, maxLen = 0;

        for (int j = 0; j < s.length(); j++) {
            char cur = s.charAt(j);
            map.put(cur, map.getOrDefault(cur, 0) + 1);
            maxFreq = Math.max(maxFreq, map.get(cur));

            while ((j - i + 1) - maxFreq > k) {
                char lchar = s.charAt(i);
                map.put(lchar, map.get(lchar) - 1);
                i++;
            } 
            maxLen = Math.max(maxLen, j - i + 1);
        } 
        return maxLen;
    }
}
```

---

## 🧠 Dry Run

Let’s dry-run for:
`s = "AABABBA"`, `k = 1`

| `j` | `s[j]` | `map`      | `maxFreq` | `Window` | `Changes Needed` | Action                  | `maxLen` |
| --- | ------ | ---------- | --------- | -------- | ---------------- | ----------------------- | -------- |
| 0   | A      | {A:1}      | 1         | \[0]     | 0                | Valid, expand           | 1        |
| 1   | A      | {A:2}      | 2         | \[0,1]   | 0                | Valid, expand           | 2        |
| 2   | B      | {A:2, B:1} | 2         | \[0,2]   | 1                | Valid, expand           | 3        |
| 3   | A      | {A:3, B:1} | 3         | \[0,3]   | 1                | Valid, expand           | 4        |
| 4   | B      | {A:3, B:2} | 3         | \[0,4]   | 2                | Too many → shrink `i++` | 4        |
|     |        | {A:2, B:2} | 3         | \[1,4]   |                  |                         |          |
| 5   | B      | {A:2, B:3} | 3         | \[1,5]   | 1                | Valid, expand           | 4        |
| 6   | A      | {A:3, B:3} | 3         | \[1,6]   | 2                | Too many → shrink `i++` | 4        |
|     |        | {A:2, B:3} |           |          |                  |                         |          |

**🔚 Final Answer**: `4`
Example valid substrings: `"AABA"`, `"ABAB"`, `"BABB"`

---

## 🧾 Summary

* ✅ Efficient sliding window approach
* ✅ Time Complexity: `O(n)`
* ✅ Space Complexity: `O(1)` (since only 26 uppercase letters)

---


