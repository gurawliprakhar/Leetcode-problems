# 🧹 Move Zeroes

**LeetCode Problem 283**  
**Difficulty**: Easy  
**Link**: [Move Zeroes – LeetCode](https://leetcode.com/problems/move-zeroes/)

---

## 📝 Problem Statement

Given an integer array `nums`, move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

You must do this **in-place** without making a copy of the array.

---

## 📌 Constraints

- `1 <= nums.length <= 10⁴`
- `-2³¹ <= nums[i] <= 2³¹ - 1`

---

## 🔄 Example

### Example 1:
```
Input:  nums = [0,1,0,3,12]
Output: [1,3,12,0,0]
```

### Example 2:
```
Input:  nums = [0]
Output: [0]
```

---

## 💡 Approach: Two Pointers

We use two pointers:
- `i`: to iterate through the array.
- `j`: to track the position to place the next non-zero element.

### Steps:
1. Traverse the array with `i`.
2. If `nums[i]` is non-zero, assign it to `nums[j]` and increment `j`.
3. After the loop, fill the rest of the array from `j` to the end with `0`s.

This ensures all non-zero elements are moved to the front in order, and all zeros are pushed to the end.

---

## ✅ Java Code

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int i = 0, j = 0;
        while (i < nums.length) {
            if (nums[i] == 0) {
                i++;
            } else {
                nums[j] = nums[i];
                i++;
                j++;
            }
        }
        while (j < nums.length) {
            nums[j] = 0;
            j++;
        }
    }
}
```

---

## 🔍 Dry Run

### Input:
```
nums = [0, 1, 0, 3, 12]
```

### Execution:

| Step | i | j | nums                  | Action                     |
|------|---|---|------------------------|----------------------------|
| 1    | 0 | 0 | [0, 1, 0, 3, 12]       | nums[0] == 0 → skip        |
| 2    | 1 | 0 | [1, 1, 0, 3, 12]       | nums[1] != 0 → nums[0]=1   |
| 3    | 2 | 1 | [1, 1, 0, 3, 12]       | nums[2] == 0 → skip        |
| 4    | 3 | 1 | [1, 3, 0, 3, 12]       | nums[3] != 0 → nums[1]=3   |
| 5    | 4 | 2 | [1, 3, 12, 3, 12]      | nums[4] != 0 → nums[2]=12  |
| 6    | - | 3 | [1, 3, 12, 0, 0]       | Fill remaining with 0s     |

### Output:
```
[1, 3, 12, 0, 0]
```

---

## ⏱️ Time & Space Complexity

| Metric         | Value        |
|----------------|--------------|
| Time           | O(n)         |
| Space          | O(1)         |
| In-place       | ✅ Yes       |
| Stable Order   | ✅ Maintained |

---

## 🧠 Follow-Up

Can you minimize the total number of **writes** to the array?  
Yes — by only writing when `i != j`, we can reduce unnecessary assignments.
