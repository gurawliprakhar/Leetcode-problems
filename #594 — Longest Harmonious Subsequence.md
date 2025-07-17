
---

# 🧩 Longest Harmonious Subsequence

## 🚀 Problem Statement

You are given an array of integers. A **harmonious subsequence** is a group of elements where the **difference between the maximum and minimum value is exactly 1**. Your task is to find the **length of the longest harmonious subsequence**.

📌 A **subsequence** can skip elements but must maintain original order.

---

## ✨ Example

### ✅ Example 1
```text
Input:  [1, 3, 2, 2, 5, 2, 3, 7]
Output: 5
Explanation: Longest harmonious subsequence is [3, 2, 2, 2, 3]
```

### ✅ Example 2
```text
Input:  [1, 2, 3, 4]
Output: 2
Explanation: Valid subsequences: [1, 2], [2, 3], [3, 4]
```

### ✅ Example 3
```text
Input:  [1, 1, 1, 1]
Output: 0
Explanation: All values are same → max - min = 0 → Not harmonious
```

---

## 📘 Constraints

- `1 <= nums.length <= 20,000`
- `-10^9 <= nums[i] <= 10^9`

---

## 🧠 Approach

1. **Sort the array** to group similar values.
2. Use **two pointers** (`i`, `j`) to slide through the array.
3. If `nums[j] - nums[i] > 1`, move `i` forward.
4. If `nums[i] == nums[j] - 1`, update the max length.
5. Return the longest harmonious window size.

---

## 💻 Java Code

```java
public int findLHS(int[] nums) {
    int n = nums.length;

    Arrays.sort(nums); // Sort to group similar numbers

    int maxLen = 0;

    for (int i = 0, j = 0; j < n; j++) {
        int k = nums[j];

        while (i < j && nums[i] < k - 1) {
            i++; // Shrink window from left
        }

        if (nums[i] == k - 1) {
            maxLen = Math.max(maxLen, j - i + 1);
        }

        /*
        🧪 Sample Dry Run — Input: [1, 3, 2, 2, 5, 2, 3, 7]
        Sorted: [1, 2, 2, 2, 3, 3, 5, 7]

        j | nums[j] | i shifts to | nums[i] | Condition (nums[i] == k - 1) | Length (j - i + 1) | maxLen
        1 |    2    |     0       |    1    |            ✅                |         2          |   2
        2 |    2    |     0       |    1    |            ✅                |         3          |   3
        3 |    2    |     0       |    1    |            ✅                |         4          |   4
        4 |    3    |     1       |    2    |            ✅                |         4          |   4
        5 |    3    |     1       |    2    |            ✅                |         5          |   5
        6 |    5    |     5       |    3    |            ❌                |         -          |   5
        7 |    7    |     6       |    5    |            ❌                |         -          |   5
        */
    }

    return maxLen;
}
```

---

## 🧪 Test Case Summary

| Input                   | Output | Explanation                                           |
|------------------------|--------|-------------------------------------------------------|
| `[1, 3, 2, 2, 5, 2, 3, 7]` | `5`    | `[3, 2, 2, 2, 3]` is the longest harmonious subsequence |
| `[1, 2, 3, 4]`          | `2`    | Valid subsequences: `[1,2]`, `[2,3]`, `[3,4]`         |
| `[1, 1, 1, 1]`          | `0`    | No valid harmonious group                            |

---

