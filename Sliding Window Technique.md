

---

# 📚 Sliding Window Technique (Java) - Notes and Examples

---

## ✅ What is Sliding Window?

**Sliding Window** is a powerful algorithmic technique used to solve problems involving:

* Arrays or Strings (linear data structures)
* **Contiguous** subarrays or substrings (continuous elements)
* Optimization problems like finding maximum, minimum, or specific counts in a range

Instead of checking all possible subarrays (brute force, O(n²)),
Sliding Window solves these problems in **O(n)** time.

---

## ✅ Types of Sliding Window Problems

| Type                     | Description                                                                                     |
| ------------------------ | ----------------------------------------------------------------------------------------------- |
| **Fixed Size Window**    | The window size (`k`) is constant throughout                                                    |
| **Variable Size Window** | Window size changes dynamically based on conditions (like unique characters, target sums, etc.) |

---

## ✅ Sliding Window Templates (Java)

### 1️⃣ Fixed Size Window Template:

```java
for (int i = 0; i < k; i++) {
    // Prepare first window
}

for (int i = k; i < arr.length; i++) {
    // Slide the window
    // Add new element, remove outgoing element
}
```

---

### 2️⃣ Variable Size Window Template:

```java
int windowStart = 0;
for (int windowEnd = 0; windowEnd < arr.length; windowEnd++) {
    // Expand the window

    while (/* condition fails */) {
        // Shrink the window from start
        windowStart++;
    }

    // Update result
}
```

---

## ✅ Common Sliding Window Problems with Java

| Problem                                              | Type          | Description                                     |
| ---------------------------------------------------- | ------------- | ----------------------------------------------- |
| Maximum Sum of K Consecutive Elements                | Fixed Size    | Max sum in fixed-length window                  |
| First Negative Integer in Every Window of Size K     | Fixed Size    | Find first negative in every window             |
| Longest Substring Without Repeating Characters       | Variable Size | Max length substring with all unique chars      |
| Smallest Subarray with Sum ≥ Target                  | Variable Size | Min length subarray with sum at least target    |
| Longest Substring with At Most K Distinct Characters | Variable Size | Largest substring with at most K distinct chars |
| Count Occurrences of Anagrams                        | Fixed Size    | Count how many substrings are anagrams          |

---

## ✅ Example Problems with Java Code Links (inside this repo):

| Problem                                        | Java File                      |
| ---------------------------------------------- | ------------------------------ |
| Maximum Sum of K Elements                      | `FixedSizeSlidingWindow.java`  |
| Longest Substring Without Repeating Characters | `LongestUniqueSubstring.java`  |
| Smallest Subarray with Sum ≥ Target            | `SmallestSubarrayWithSum.java` |

(🔗 *Update this table with your actual filenames in the repo*)

---

## ✅ Benefits of Sliding Window:

* Reduces Time Complexity from **O(n²)** → **O(n)**
* Simple to implement with two pointers
* Space efficient (uses constant or minimal extra space)
* Works for both **arrays** and **strings**

---

## ✅ When to Apply Sliding Window:

✔️ When the problem talks about:

* **Subarrays** or **Substrings**
* **Contiguous elements**
* **Max/min/target/count in a window**

✔️ When brute force looks like nested loops with O(n²)

---

## ✅ Final Tip:

🔑 **Mastering Sliding Window** is essential for coding interviews like:
Google, Amazon, Microsoft, etc.

---


