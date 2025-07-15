

---

````markdown
# 🧠 Leetcode 3136 - Valid Word

## 📄 Problem Statement (Simplified)

You are given a string called `word`. You need to decide whether this string is **valid** based on the following rules:

### ✅ A word is valid if:
1. It has **at least 3 characters**.
2. It contains **only letters or digits** (no special symbols like `$`, `#`, etc.).
3. It has **at least one vowel**: `a, e, i, o, u` (case-insensitive).
4. It has **at least one consonant** (any letter that is not a vowel).

---

## 🧪 Example

| Input       | Valid? | Reason                                                              |
|-------------|--------|---------------------------------------------------------------------|
| `"234Adas"` | ✅     | Length ≥ 3, no special characters, has vowels (`a`), consonants (`d`) |
| `"b3"`      | ❌     | Too short and no vowel                                              |
| `"a3$e"`    | ❌     | Contains special character `$`                                      |

---

## 💻 Java Code

```java
class Solution {
    public boolean isValid(String word) {
        // Rule 1: Check minimum length
        if (word.length() < 3) {
            return false;
        }

        boolean hasVowel = false;
        boolean hasConsonant = false;

        for (int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);

            // Rule 2: Must be letter or digit only
            if (!Character.isLetterOrDigit(ch)) {
                return false;
            }

            // Convert to lowercase for uniformity
            char lower = Character.toLowerCase(ch);

            // Rule 3: Check for vowels
            if (lower == 'a' || lower == 'e' || lower == 'i' || lower == 'o' || lower == 'u') {
                hasVowel = true;
            } 
            // Rule 4: Check for consonants
            else if (Character.isLetter(lower)) {
                hasConsonant = true;
            }
        }

        // Must contain both a vowel and a consonant
        return hasVowel && hasConsonant;
    }
}
````

---

## 🔍 Dry Run (Example: `"234Adas"`)

### Initial State:

```java
hasVowel = false;
hasConsonant = false;
```

| Index | Char | Lowercase | Letter/Digit? | Vowel? | Consonant? | State                 |
| ----- | ---- | --------- | ------------- | ------ | ---------- | --------------------- |
| 0     | '2'  | '2'       | ✅ Yes         | ❌      | ❌          | -                     |
| 1     | '3'  | '3'       | ✅ Yes         | ❌      | ❌          | -                     |
| 2     | '4'  | '4'       | ✅ Yes         | ❌      | ❌          | -                     |
| 3     | 'A'  | 'a'       | ✅ Yes         | ✅      | ❌          | `hasVowel = true`     |
| 4     | 'd'  | 'd'       | ✅ Yes         | ❌      | ✅          | `hasConsonant = true` |
| 5     | 'a'  | 'a'       | ✅ Yes         | ✅      | ❌          | -                     |
| 6     | 's'  | 's'       | ✅ Yes         | ❌      | ✅          | -                     |

### Final Check:

* ✅ Length ≥ 3
* ✅ All characters are valid
* ✅ `hasVowel = true`
* ✅ `hasConsonant = true`

✔️ **Result: `true` (Valid Word)**

---

## 📌 Conclusion

This problem is a good test of:

* String manipulation
* Character type checking
* Basic validation rules

It’s great for beginners practicing input filtering and string logic.

---

> 🔗 Leetcode Link: [Valid Word - 3136](https://leetcode.com/problems/valid-word/)
>
> ✍️ Solution by [@triprakhar](https://leetcode.com/problems/valid-word/solutions/6960011/valid-word-leetcode-3136-by-triprakhar-hz2u/)

```

---

