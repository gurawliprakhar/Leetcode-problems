

---

````markdown
# 📌 Leetcode 2200 - Find All K-Distant Indices in an Array

This repository contains a clean and efficient **Java solution** for **[Leetcode Problem 2200](https://leetcode.com/problems/find-all-k-distant-indices-in-an-array/)**:  
**Find All K-Distant Indices in an Array**

---

## 🧩 Problem Description

Given:
- An integer array `nums`
- An integer `key`
- An integer `k`

Return **all indices `i`** such that there exists at least one index `j` satisfying:
1. `|i - j| <= k`
2. `nums[j] == key`

These indices `i` are called **k-distant indices**.

### ✅ Constraints
- `1 <= nums.length <= 1000`
- `1 <= nums[i] <= 1000`
- `1 <= k <= nums.length`
- The `key` is guaranteed to appear in `nums`

---

## 💡 Intuition

Instead of checking every pair `(i, j)`, we:
1. Identify all positions of `key` in the array
2. For each such position `j`, include all indices from `j - k` to `j + k`
3. Store these indices in a `Set` (to avoid duplicates), then sort and return the result

---

## 🧠 Approach

1. Loop through the array to find all `j` where `nums[j] == key`
2. For each such `j`, add all `i` from `max(0, j - k)` to `min(n - 1, j + k)` into a `Set`
3. Convert the set to a `List` and sort it
4. Return the sorted list

---

## 💻 Java Code

```java
import java.util.*;

public class Solution {
    public List<Integer> findKDistantIndices(int[] nums, int key, int k) {
        Set<Integer> resultSet = new HashSet<>();
        int n = nums.length;

        for (int j = 0; j < n; j++) {
            if (nums[j] == key) {
                int start = Math.max(0, j - k);
                int end = Math.min(n - 1, j + k);
                for (int i = start; i <= end; i++) {
                    resultSet.add(i);
                }
            }
        }

        List<Integer> result = new ArrayList<>(resultSet);
        Collections.sort(result);
        return result;
    }
}
````

---

## 🧪 Dry Run Example

### Input:

```java
nums = [3, 4, 9, 1, 3, 9, 5]
key = 9
k = 1
```

### Step-by-Step Execution:

1. Find all indices `j` where `nums[j] == 9`:

   * `j = 2`
   * `j = 5`

2. For each `j`, compute the range `[j - k, j + k]` and add all valid indices to a set:

   * From `j = 2`: range = \[1, 2, 3] → Add: 1, 2, 3
   * From `j = 5`: range = \[4, 5, 6] → Add: 4, 5, 6

3. Set contents (unordered): `{1, 2, 3, 4, 5, 6}`

4. Sort the set → Final Output:

```java
[1, 2, 3, 4, 5, 6]
```

---

## 📈 Time & Space Complexity

| Metric           | Complexity             |
| ---------------- | ---------------------- |
| Time Complexity  | O(n \* k) (worst-case) |
| Space Complexity | O(n)                   |

> Efficient in practice because `k` is small and only key positions are expanded.

---

## 📦 Tools Used

* Java Collections (`HashSet`, `ArrayList`)
* Java 8+
* Tested on [Leetcode](https://leetcode.com/problems/find-all-k-distant-indices-in-an-array/)

---




---

## ✅ Possible Extensions

* Add support for:

  * Multiple languages (Python, C++)
  * Optimized one-pass variants
* Add unit testing using JUnit

---

## 📜 License

Licensed under the [MIT License](LICENSE).

---

## 🤝 Contributions

Contributions welcome!
Feel free to:

* Fork and submit a pull request
* Suggest alternate solutions or optimizations
* Add more test cases

---

## 🌟 Show Your Support

If this helped you, please **star** the repo to show your support! ⭐

---

## 📬 Contact

Created with ❤️ by [Prakhar Tripathi](https://github.com/gurawliprakhar)

For questions, feel free to open an issue or reach out.

```

---


```
