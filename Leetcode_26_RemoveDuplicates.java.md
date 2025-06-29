
---

# 🧹 Remove Duplicates from Sorted Array

This repository contains a Java solution to the classic LeetCode problem: **Remove Duplicates from Sorted Array**.

## 📘 Problem Statement

Given a sorted integer array `nums`, remove the duplicates **in-place** such that each unique element appears only once. The relative order of the elements should be preserved. Return the number of unique elements, `k`, and ensure the first `k` elements of `nums` contain the unique values.

> You must do this in-place with O(1) extra memory.

### Example 1
```
Input:  nums = [1,1,2]
Output: 2, nums = [1,2,_]
```

### Example 2
```
Input:  nums = [0,0,1,1,1,2,2,3,3,4]
Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
```

---

## 🚀 Approach

Since the array is sorted, duplicates are always adjacent. We use the **two-pointer technique**:

- `unique` points to the position where the next unique element should be placed.
- `i` scans the array from left to right.

If `nums[i] != nums[unique - 1]`, we’ve found a new unique element. We place it at `nums[unique]` and increment `unique`.

---

## 💻 Code

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int unique = 1;
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[unique - 1]) {
                nums[unique] = nums[i];
                unique++;
            }
        }
        return unique;
    }
}
```

---

## 🔍 Dry Run

Input: `nums = [0,0,1,1,1,2,2,3,3,4]`

| i | nums[i] | nums[unique - 1] | Action               | nums (partial)             | unique |
|---|---------|------------------|------------------------|-----------------------------|--------|
| 1 | 0       | 0                | Duplicate, skip        | [0,0,...]                   | 1      |
| 2 | 1       | 0                | Unique → nums[1]=1     | [0,1,...]                   | 2      |
| 3 | 1       | 1                | Duplicate, skip        |                             | 2      |
| 4 | 1       | 1                | Duplicate, skip        |                             | 2      |
| 5 | 2       | 1                | Unique → nums[2]=2     | [0,1,2,...]                 | 3      |
| 6 | 2       | 2                | Duplicate, skip        |                             | 3      |
| 7 | 3       | 2                | Unique → nums[3]=3     | [0,1,2,3,...]               | 4      |
| 8 | 3       | 3                | Duplicate, skip        |                             | 4      |
| 9 | 4       | 3                | Unique → nums[4]=4     | [0,1,2,3,4,...]             | 5      |

**Final Output:**
- `unique = 5`
- Modified array: `[0,1,2,3,4,_,_,_,_,_]`

---

## 🧠 Complexity

- **Time:** O(n)
- **Space:** O(1) — in-place

---

## 📎 Related Topics

- Arrays
- Two Pointers
- In-place Algorithms

---

## 📚 Reference

- [LeetCode Problem #26](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/?envType=study-plan-v2&envId=top-interview-150)  
- [Optimal Solution Walkthrough](https://leetcode.com/problems/remove-duplicates-from-sorted-array/solutions/6880399/optimal-solution/?envType=study-plan-v2&envId=top-interview-150) [¹]

---

