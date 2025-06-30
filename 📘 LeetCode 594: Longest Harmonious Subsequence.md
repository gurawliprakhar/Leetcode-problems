

---

# 📘 LeetCode 594: Longest Harmonious Subsequence

## 🚩 Problem Statement

Given an integer array `nums`, find the length of its **Longest Harmonious Subsequence (LHS)**.

---

### ✅ What is a Harmonious Subsequence?

A **harmonious subsequence** is a subsequence where:

* The **difference between its maximum and minimum elements is exactly 1**.
* The elements **do not need to be adjacent**, but **must follow the original order** of the array.

---

## 🧪 Example Walkthroughs

### Example 1:

```text
Input: nums = [1, 3, 2, 2, 5, 2, 3, 7]

Step 1: Build frequency map:
{1=1, 2=3, 3=2, 5=1, 7=1}

Step 2: Check harmonious pairs:
(1,2) → length = 1+3=4
(2,3) → length = 3+2=5 → Max so far
(3,4) → doesn't exist
(5,6) → doesn't exist
(7,8) → doesn't exist

Output: 5
```

The LHS can be `[3, 2, 2, 2, 3]` (length = 5).

---

### Example 2:

```text
Input: nums = [1, 2, 3, 4]

Frequencies: {1=1, 2=1, 3=1, 4=1}

Pairs:
(1,2) → 2
(2,3) → 2
(3,4) → 2

Output: 2
```

---

### Example 3:

```text
Input: nums = [1, 1, 1, 1]

Frequencies: {1=4}

No other number to form a harmonious pair.

Output: 0
```

---

## 🛠️ Dry Run for Input: `[1, 3, 2, 2, 5, 2, 3, 7]`

| Iteration | Current Number | Frequency Map Update      |
| --------- | -------------- | ------------------------- |
| 1         | 1              | {1=1}                     |
| 2         | 3              | {1=1, 3=1}                |
| 3         | 2              | {1=1, 3=1, 2=1}           |
| 4         | 2              | {1=1, 3=1, 2=2}           |
| 5         | 5              | {1=1, 3=1, 2=2, 5=1}      |
| 6         | 2              | {1=1, 3=1, 2=3, 5=1}      |
| 7         | 3              | {1=1, 3=2, 2=3, 5=1}      |
| 8         | 7              | {1=1, 3=2, 2=3, 5=1, 7=1} |

---

## 🧑‍💻 Java Code

```java
import java.util.HashMap;
import java.util.Map;

public class LongestHarmoniousSubsequence {
    public int findLHS(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        
        // Step 1: Build frequency map
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        
        int maxLen = 0;
        
        // Step 2: Check for harmonious pairs (num, num + 1)
        for (int key : map.keySet()) {
            if (map.containsKey(key + 1)) {
                int currentLen = map.get(key) + map.get(key + 1);
                maxLen = Math.max(maxLen, currentLen);
            }
        }
        
        return maxLen;
    }
}
```

---

## ✅ Complexity Analysis

| Complexity | Value |
| ---------- | ----- |
| Time       | O(n)  |
| Space      | O(n)  |

Where `n = nums.length`.

---

## ✅ Summary

This problem tests your skills in:

* **HashMap frequency counting**
* **Neighbor value checking**
* **Optimized O(n) time solutions**

Great problem for interview prep! ✅

---

Feel free to ⭐ star this repo and fork for your Java LeetCode practice! 🚀

---
