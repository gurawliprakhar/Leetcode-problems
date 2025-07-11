
```markdown
# LeetCode 413: Arithmetic Slices

## 📍 Problem Description

You’re given an array of integers — say `[1, 3, 5, 7]` — and your job is to count how many **arithmetic subarrays** there are.

> 🟢 **What's an Arithmetic Subarray?**  
An arithmetic subarray is a sequence of **three or more consecutive numbers** in the array where the **difference between each pair of elements is the same**.  
For example, `[1, 3, 5, 7]` has a common difference of `+2`, so it's arithmetic.

---

## 🎯 Objective

Your task is to:
- Traverse the array.
- Identify all **contiguous** subarrays of length **≥ 3** that satisfy the arithmetic condition.
- Count and return the total number of valid arithmetic slices.

---

## 🧪 Example

**Input:**  
```java
nums = [1, 2, 3, 4]
```

**Output:**  
```
3
```

**Explanation:**
- `[1, 2, 3]` → arithmetic ✅  
- `[2, 3, 4]` → arithmetic ✅  
- `[1, 2, 3, 4]` → arithmetic ✅  
Total = **3** slices 🔥

---

## 🧠 Solution Overview

We use a **sliding window** approach with nested loops:
- Outer loop starts at index `i` and calculates `diff = nums[i+1] - nums[i]`.
- Inner loop from `j = i+2` checks whether `nums[j] - nums[j-1] == diff`.
  - If yes: increment count.
  - If no: break the inner loop and move to the next base.

---

## 💻 Code

```java
class Solution {
    public int numberOfArithmeticSlices(int[] nums) {
        int n = nums.length;
        int count = 0;

        for (int i = 0; i <= n - 3; i++) {
            int diff = nums[i + 1] - nums[i];

            for (int j = i + 2; j < n; j++) {
                if (nums[j] - nums[j - 1] == diff) {
                    count++;
                } else {
                    break;
                }
            }
        }

        return count;
    } 
}
```

---

## 🔬 Dry Run Example

**Input:**
```java
nums = [1, 3, 5, 7, 8]
```

### Execution Steps:
| i | j | nums[j-1] → nums[j] | Difference | Matches diff? | Count |
|--|--|-----------------------|------------|----------------|--------|
| 0 | 2 | 3 → 5               | 2          | ✅              | 1      |
| 0 | 3 | 5 → 7               | 2          | ✅              | 2      |
| 0 | 4 | 7 → 8               | 1          | ❌              |        |
| 1 | 3 | 5 → 7               | 2          | ✅              | 3      |

**Final Output:** `count = 3`

---

## 🧵 Visual Tip for YouTube

Use the above table format or trace animations to clearly highlight how the count evolves and when the differences break — especially helpful for engaging explanations.

---

```
