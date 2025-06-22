

---

````markdown
# LeetCode 2138 - Divide a String Into Groups of Size k

> **Difficulty:** Easy  
> **Tags:** String, Simulation

---

## 🧩 Problem Statement

You are given:
- A string `s` consisting of lowercase English letters.
- An integer `k`, the **size of each group**.
- A character `fill`, used to **pad the final group** if it's too short.

---

### 📥 Input:
- `s`: A string of lowercase letters (`1 <= s.length <= 100`)
- `k`: An integer (`1 <= k <= 100`)
- `fill`: A lowercase English letter

---

### 📤 Output:
- An array of strings, where:
  - Each string is of length `k`.
  - All characters from `s` are used exactly once.
  - The final group is padded with `fill` if needed.

---

### 💡 Example:

#### Input:
```java
s = "abcdefghij"
k = 3
fill = 'x'
````

#### Output:

```java
["abc", "def", "ghi", "jxx"]
```

---

## ✅ Approach

We divide the string into consecutive groups of size `k`.
If the final group has fewer than `k` characters, we pad it with the `fill` character.

### 🧠 Key Idea:

To calculate the number of required groups:

```java
int totalGroups = (s.length() + k - 1) / k;
```

This is a **ceiling division** trick to make sure even a partial group is counted.

---

## 🧪 Java Solution

```java
class Solution {
    public String[] divideString(String s, int k, char fill) {
        int n = s.length();
        int totalGroups = (n + k - 1) / k;
        String[] res = new String[totalGroups];
        int index = 0;

        for (int i = 0; i < totalGroups; i++) {
            char[] group = new char[k];
            int j = 0;

            while (j < k && index < n) {
                group[j++] = s.charAt(index++);
            }

            while (j < k) {
                group[j++] = fill;
            }

            res[i] = new String(group);
        }

        return res;
    }
}
```

---

## 🐍 Python Version

```python
def divideString(s: str, k: int, fill: str) -> list[str]:
    res = []
    for i in range(0, len(s), k):
        group = s[i:i+k]
        if len(group) < k:
            group += fill * (k - len(group))
        res.append(group)
    return res
```

---

## 🧵 C++ Version

```cpp
class Solution {
public:
    vector<string> divideString(string s, int k, char fill) {
        vector<string> result;
        int n = s.length();
        int index = 0;
        int totalGroups = (n + k - 1) / k;

        for (int i = 0; i < totalGroups; i++) {
            string group = "";
            int j = 0;

            while (j < k && index < n) {
                group += s[index++];
                j++;
            }

            while (j < k) {
                group += fill;
                j++;
            }

            result.push_back(group);
        }

        return result;
    }
};
```

---

## 🧠 Time and Space Complexity

| Complexity | Value    |
| ---------- | -------- |
| ⏱ Time     | O(n)     |
| 🗂 Space   | O(n / k) |

---

## 🔚 Final Notes

* This is a great practice problem for mastering string manipulation.
* Knowing how to do **ceiling division** using `(n + k - 1) / k` is a key takeaway.

---

### 🔗 Related Problems

* [LeetCode 557 – Reverse Words in a String III](https://leetcode.com/problems/reverse-words-in-a-string-iii/)
* [LeetCode 58 – Length of Last Word](https://leetcode.com/problems/length-of-last-word/)
* [LeetCode 2278 – Percentage of Letter in String](https://leetcode.com/problems/percentage-of-letter-in-string/)

---

**Happy Coding! 🚀**

```


```
