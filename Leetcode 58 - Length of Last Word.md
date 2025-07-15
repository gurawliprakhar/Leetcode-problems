
---

````markdown
# 📘 Leetcode 58 - Length of Last Word

> 🧩 [Problem Link](https://leetcode.com/problems/length-of-last-word/)

---

## 📄 Problem Statement (Simplified)

You are given a string `s` that contains **letters and spaces**.

Your task is to **return the length of the last word** in the string.

### 🧠 What is a "Word"?
A **word** is a **continuous sequence of non-space characters**.

---

## 🎯 Goal:
Write a function that returns how many characters are in the **last word** of the string `s`.

---

## 🧪 Examples

| Input                             | Last Word | Output |
|----------------------------------|-----------|--------|
| `"Hello World"`                  | `"World"` | `5`    |
| `"   fly me   to   the moon  "`  | `"moon"`  | `4`    |
| `"luffy is still joyboy"`        | `"joyboy"`| `6`    |

---

## ✅ Constraints

- `1 <= s.length <= 10⁴`
- `s` contains only **letters and spaces**
- There will always be **at least one word** in `s`

---

## 💻 Java Code

```java
class Solution {
    public int lengthOfLastWord(String s) {
        int n = 0;
        int i = s.length() - 1;

        // Step 1: Skip trailing spaces
        while (i >= 0 && s.charAt(i) == ' ') {
            i--;
        }

        // Step 2: Count characters in the last word
        while (i >= 0 && s.charAt(i) != ' ') {
            n++;
            i--;
        }
        return n;
    }
}
````

---

## 🧪 Dry Run

**Input:**

```java
s = "   fly me   to   the moon  ";
```

### Step-by-step Execution:

```java
int length = 0;
int i = s.length() - 1;  // i = 28 (last index)
```

🔁 **Step 1: Skip trailing spaces**

```java
while (s.charAt(i) == ' ') i--;
```

* i goes from 28 ➝ 27 ➝ 26 ➝ 25 ➝ 24 → now at `'n'` in `"moon"`

🔁 **Step 2: Count the last word**

```java
while (s.charAt(i) != ' ') {
    length++;
    i--;
}
```

| i (index) | s.charAt(i) | length    |
| --------- | ----------- | --------- |
| 24        | `'n'`       | 1         |
| 23        | `'o'`       | 2         |
| 22        | `'o'`       | 3         |
| 21        | `'m'`       | 4         |
| 20        | `' '`       | loop ends |

✔️ Final result:

```java
return length; // ➝ 4
```

---

## ✅ Output

```java
Output: 4
```

---

## 📌 Conclusion

This is a clean and efficient solution to a common string manipulation problem:

* It avoids using `.split()` or regex
* It runs in **O(n)** time with **O(1)** space
* It handles trailing spaces and multiple words gracefully

---

> 🔗 **Leetcode Link**: [Length of Last Word](https://leetcode.com/problems/length-of-last-word/)
>
> ✍️ **Solution by** [@triprakhar](https://leetcode.com/problems/length-of-last-word/solutions/6960086/length-of-last-word-by-triprakhar-bvds/)

```

---

```
