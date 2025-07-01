
---

# 🧑‍💻 LeetCode 3330: Find the Original Typed String I (Java Solution)

## 🚩 Problem Statement:

Alice was trying to type a specific string on her computer. However, she may have **accidentally held a key for too long**, resulting in one or more extra characters being typed in **at most one group**.

Given the final string `word` displayed on the screen, **return the total number of possible original strings** that Alice might have intended to type.

---

## 🧪 Example Test Cases:

### Example 1:

```
Input: word = "abbcccc"
Output: 5

Explanation: 
Possible original strings:
- "abbcccc" (no mistake)
- "abcccc"
- "abbccc"
- "abbcc"
- "abbc"
```

---

### Example 2:

```
Input: word = "abcd"
Output: 1
```

---

### Example 3:

```
Input: word = "aaaa"
Output: 4

Explanation:
Original could have been:
- "aaaa"
- "aaa"
- "aa"
- "a"
```

---

## ✅ Approach:

This problem focuses on **counting the number of consecutive duplicate characters (groups)**.

For each group with size `n ≥ 2`, Alice could have accidentally over-typed that character.
The total number of possible original strings = **1 (original) + (number of extra characters in each group, summed across all groups).**

---

### 🔑 Key Observations:

* Every group of repeated characters contributes `(n - 1)` possible mistakes.
* Since Alice can only make this mistake in **at most one group**, we sum up these possible reductions from each group.

---

## 💻 Java Solution:

```java
class Solution {
    public int possibleStringCount(String word) {
        int count = 0;
        for (int i = 1; i < word.length(); i++) {
            if (word.charAt(i) == word.charAt(i - 1)) {
                count++;
            }
        }
        return count + 1;
    }
}
```

---

## 🕐 Complexity Analysis:

* **Time Complexity:** O(n), where n is the length of the string.
* **Space Complexity:** O(1), constant space.

---

## ✅ Explanation:

This simple Java code does the following:

* **Iterates once** over the string.
* **Counts each time two consecutive characters are the same**, which represents an extra typed character in that group.
* Finally, **returns `(count + 1)`**, accounting for the original string and each possible typo fix (removing characters from any one group).

---

## ✅ Summary:

This is a great example of how observing patterns in input strings (like **consecutive duplicates**) can help solve seemingly tricky LeetCode problems with **just a few lines of Java code!**

---

## ✨ Related Tags:

`#LeetCode` `#Java` `#StringManipulation` `#Greedy` `#SlidingWindow` `#Counting`

---

If you found this useful, feel free to ⭐️ star this repo and check out my other LeetCode solutions!

---


