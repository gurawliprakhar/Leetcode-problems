
---

# 📌 LeetCode 1207 - Unique Number of Occurrences (Java Solution)

![LeetCode Badge](https://img.shields.io/badge/LeetCode-Easy-brightgreen.svg)
![Language](https://img.shields.io/badge/Language-Java-blue.svg)

---

## 📖 Problem Statement

Given an integer array `arr`, **return `true` if the number of occurrences of each value is unique**, or `false` otherwise.

---

## 🧠 Approach

This is a **two-step frequency-counting problem**:

1. **Count Frequencies:**
   Use a `HashMap<Integer, Integer>` to count how many times each number appears.

2. **Check Uniqueness of Frequencies:**
   Use a `HashSet<Integer>` to make sure all frequencies are unique.
   If any frequency repeats, return `false`.

---

## ✅ Java Solution

```java
import java.util.*;

public class UniqueOccurrences {
    public boolean uniqueOccurrences(int[] arr) {
        Map<Integer, Integer> freqMap = new HashMap<>();

        // Step 1: Count frequency of each number
        for (int num : arr) {
            freqMap.put(num, freqMap.getOrDefault(num, 0) + 1);
        }

        Set<Integer> freqSet = new HashSet<>();

        // Step 2: Check uniqueness of frequencies
        for (int freq : freqMap.values()) {
            if (!freqSet.add(freq)) {
                return false;  // Duplicate frequency found
            }
        }

        return true;  // All frequencies are unique
    }
}
```

---

## ✅ Example Walkthrough

### Example 1:

```java
Input: arr = [1, 2, 2, 1, 1, 3]
Output: true
Explanation:
Frequencies → [3, 2, 1] → All unique ✅
```

---

### Example 2:

```java
Input: arr = [1, 2]
Output: false
Explanation:
Frequencies → [1, 1] → Duplicate frequencies ❌
```

---

### Example 3 (Detailed):

```java
Input: arr = [-3, 0, 1, -3, 1, 1, 1, -3, 10, 0]
Output: true
Explanation:
Frequencies → [3, 2, 4, 1] → All unique ✅
```

---

## ✅ Complexity Analysis

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(n)       |

Where `n` is the length of the input array.

---

## ✅ Useful Concepts:

* **HashMap** → For frequency counting.
* **HashSet** → For checking uniqueness.

This pattern (`Map → Set`) appears in many LeetCode problems, making it a great learning exercise.

---

## ✅ Related LeetCode Topics:

* Arrays
* HashMap
* HashSet
* Frequency Counter Pattern

---

## ✅ Author

[Prakhar Tripathi](https://github.com/PrakharTripathi-dev) ✨

---


