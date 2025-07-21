

---

````markdown
# 🧩 Leetcode 1957: Delete Characters to Make Fancy String

> 🚀 A Java greedy solution to the Leetcode problem [Delete Characters to Make Fancy String](https://leetcode.com/problems/delete-characters-to-make-fancy-string/).

---

## 📜 Problem Statement

You're given a string `s` consisting of lowercase English letters. Modify the string such that **no three consecutive characters are the same**.

- You can **delete** characters, but you should **delete as few as possible**.
- Return the final version of the string.
- The result is **guaranteed to be unique**.

---

## 🧠 Approach

We use a **greedy strategy**:
- Traverse each character in the input string.
- If appending the current character would result in **three same characters in a row**, **skip it**.
- Otherwise, add it to the result.

---

## 💻 Java Solution

```java
class Solution {
    public String makeFancyString(String s) {
        StringBuilder res = new StringBuilder();

        for (char c : s.toCharArray()) {
            int n = res.length();
            if (n >= 2 && c == res.charAt(n - 1) && c == res.charAt(n - 2)) {
                continue;
            } else {
                res.append(c);
            }
        }
        return res.toString();
    }
}
````

---

## 🔍 Example Dry Run

### Input: `"aaabaaaa"`

### Output: `"aabaa"`

Step-by-step:

```
Input:   a a a b a a a a
Result:  a a   b a a
```

---

## ⏱️ Complexity

| Type  | Value |
| ----- | ----- |
| Time  | O(n)  |
| Space | O(n)  |

---

## 📎 Related Links

* 🔗 [Problem on Leetcode](https://leetcode.com/problems/delete-characters-to-make-fancy-string/)

---


---

## 🙌 Support

If you found this helpful, feel free to ⭐ the repo or follow me for more coding solutions!

```

---


```
