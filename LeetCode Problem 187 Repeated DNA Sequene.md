
---

## 🧬 Problem: Repeated DNA Sequences

### 🔹 What's the real-world scenario?

In genetics, a **DNA sequence** is a string made up of four characters: `'A'`, `'C'`, `'G'`, and `'T'`, which represent nucleotides.

Scientists may need to **identify repeated patterns** in a long DNA strand to find potential mutations or important biological markers.

---

### 🔹 What are we asked to do?

You're given a **long DNA string `s`**, and you need to **find all 10-letter-long substrings that appear more than once** in that string.

You should return a **list of these repeated sequences**.

---

### 🧪 Example

#### Input:

```text
s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"
```

#### Output:

```text
["AAAAACCCCC", "CCCCCAAAAA"]
```

These 10-letter sequences appear **more than once** in the DNA string.

---

### 🎯 Goal

Efficiently find **which substrings of length 10** repeat **at least twice** in the string.

---

### 🚦Constraints

* Length of `s` is up to **100,000** characters.
* Only contains `'A'`, `'C'`, `'G'`, `'T'`.

---

### 🧠 Common Techniques to Solve:

* **Sliding Window**: Check every substring of length 10.
* **HashSet**: Keep track of which sequences you've seen once, and which you've seen more than once.
* **Optional**: Use **bit manipulation** for optimized memory (since only 4 characters → 2 bits each).

---

### 💬 How to explain simply:

> "Given a long string of DNA, we’re just scanning through it and collecting all the 10-letter pieces that show up more than once."

---


For the **"Repeated DNA Sequences"** problem, WE are going to use the **Fixed-Size Sliding Window** technique.

---

## ✅ Type of Sliding Window: **Fixed-Size Window**

### Why?

* You are only interested in **substrings of exactly 10 characters**.
* So your window size is always fixed at **10**.
* You move the window **one character at a time** (i.e., slide it forward by 1) and check each 10-character-long substring.

---

## 🧱 Window Structure

* Start from `i = 0` to `i = s.length() - 10`.
* At each position, extract the substring `s.substring(i, i + 10)`.

### Pseudocode:

```java
for (int i = 0; i <= s.length() - 10; i++) {
    String window = s.substring(i, i + 10);
    // check and store if already seen
}
```

---

## 🔁 Summary

| Feature         | Value                                           |
| --------------- | ----------------------------------------------- |
| **Type**        | Fixed-size sliding window                       |
| **Window size** | 10 characters                                   |
| **Move by**     | 1 character per step                            |
| **Use**         | To extract all 10-letter substrings efficiently |

---

Let's walk through a **detailed step-by-step example** of how the **sliding window** works in the **“Repeated DNA Sequences”** problem using the input:

---

## 🧪 Example Input:

```text
s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"
```

We need to find **all 10-letter substrings** that appear **more than once**.

---

## ⚙️ Step-by-Step Using Fixed Sliding Window (Size = 10)

We'll slide a window of **10 characters**, one step at a time:

We’ll use two sets:

* `seen`: to store all substrings we’ve seen once.
* `repeated`: to store substrings we’ve seen **more than once**.

---

### 🔁 Iteration-by-Iteration:

| i  | `s.substring(i, i+10)` | Seen Before? | Action Taken      |
| -- | ---------------------- | ------------ | ----------------- |
| 0  | AAAAACCCCC             | ❌ No         | Add to `seen`     |
| 1  | AAAACCCCCA             | ❌ No         | Add to `seen`     |
| 2  | AAACCCCCAA             | ❌ No         | Add to `seen`     |
| 3  | AACCCCCAAA             | ❌ No         | Add to `seen`     |
| 4  | ACCCCCAAAA             | ❌ No         | Add to `seen`     |
| 5  | CCCCCAAAAA             | ❌ No         | Add to `seen`     |
| 6  | CCCCAAAAAC             | ❌ No         | Add to `seen`     |
| 7  | CCCAAAAACC             | ❌ No         | Add to `seen`     |
| 8  | CCAAAAACCC             | ❌ No         | Add to `seen`     |
| 9  | CAAAAACCCC             | ❌ No         | Add to `seen`     |
| 10 | AAAAACCCCC             | ✅ Yes        | Add to `repeated` |
| 11 | AAAACCCCCA             | ✅ Yes        | Add to `repeated` |
| 12 | AAACCCCCAA             | ✅ Yes        | Add to `repeated` |
| 13 | AACCCCCAAA             | ✅ Yes        | Add to `repeated` |
| 14 | ACCCCCAAAA             | ✅ Yes        | Add to `repeated` |
| 15 | CCCCAAAAAG             | ❌ No         | Add to `seen`     |
| 16 | CCCAAAAAGG             | ❌ No         | Add to `seen`     |
| 17 | CCAAAAAGGG             | ❌ No         | Add to `seen`     |
| 18 | CAAAAAGGGT             | ❌ No         | Add to `seen`     |
| 19 | AAAAAGGGTT             | ❌ No         | Add to `seen`     |
| 20 | AAAAGGGTTT             | ❌ No         | Add to `seen`     |

---

### 📦 Final Sets:

* `repeated = { "AAAAACCCCC", "CCCCCAAAAA" }`
* These were the two 10-letter sequences that occurred **more than once**.

---

## ✅ Final Output:

```java
["AAAAACCCCC", "CCCCCAAAAA"]
```

> Order doesn't matter, so your output may list them in any sequence.

---

## 🔄 Visualizing the First Few Windows:

```
Index:     0123456789
Window 1:  [AAAAACCCCC]
Window 2:   [AAAACCCCCA]
Window 3:    [AAACCCCCAA]
...
```

Each time we move the window **one character to the right**, extract the 10-character substring, and check if we’ve seen it before.

---




# Code
```java []
class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        Set<String> seen = new HashSet<>();
        Set<String> repeated = new HashSet<>();

        //if string is sort
        ///then no sequence possible
        if (s.length() < 10) {
            return new ArrayList<>();
        }

        for (int i = 0; i <= s.length() - 10; i++) {
            //String window = s.substring(i, i + 10);
            String window = findSubstring(s, i, i + 10);
            if (!seen.add(window)) {
                repeated.add(window);
            }
        }

        return new ArrayList<>(repeated);
    }

    public String findSubstring(String s, int i, int j) {
        char[] temp = new char[j - i];
        
        for (int k = i; k < j; k++) {
            temp[k - i] = s.charAt(k);
        }

        String res  = "";
        for (int k = 0; k < temp.length; k++) {
            res += temp[k];
        }
        return res;
    }
}
```
