
---

# Leetcode 80: Remove Duplicates from Sorted Array II

## 🧩 Problem Statement

Given a sorted array `nums`, remove duplicates in-place such that **each unique element appears at most twice**. The relative order of the elements should be preserved.

You must do this using **O(1) extra space**, meaning you cannot use another array.

Return the number `k` such that the first `k` elements of `nums` contain the final result. It does **not matter** what values are left beyond index `k`.

---

## ✅ Constraints

- `1 <= nums.length <= 3 * 10⁴`
- `-10⁴ <= nums[i] <= 10⁴`
- `nums` is sorted in **non-decreasing** order

---

## 💡 Explanation

Since the array is sorted, duplicates are adjacent. You are allowed to keep **at most two** of each number. The idea is to use two pointers:

- `j` to iterate through the array
- `i` to write valid elements

We compare `nums[j]` with `nums[i - 2]`. If they are different, it means the current number hasn't appeared more than twice, so we keep it.

---

## 🧪 Examples

### Example 1
```text
Input:  nums = [1,1,1,2,2,3]
Output: 5
Modified nums = [1,1,2,2,3,_]
```

### Example 2
```text
Input:  nums = [0,0,1,1,1,1,2,3,3]
Output: 7
Modified nums = [0,0,1,1,2,3,3,_,_]
```

---

## 🧠 Java Code

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length <= 2) return nums.length;

        int i = 2;
        for (int j = 2; j < nums.length; j++) {
            if (nums[j] != nums[i - 2]) {
                nums[i] = nums[j];
                i++;
            }
        }
        return i;
    }
}
```

---

## 🔍 Dry Run

### Input: `nums = [1,1,1,2,2,3]`

| Step | j | i | nums[j] | nums[i-2] | Condition | Action              | Array State               |
|------|---|---|---------|-----------|-----------|---------------------|---------------------------|
| Init |   | 2 |         |           |           |                     | [1, 1, 1, 2, 2, 3]        |
| 1    | 2 | 2 | 1       | 1         | false     | Skip                | [1, 1, 1, 2, 2, 3]        |
| 2    | 3 | 2 | 2       | 1         | true      | nums[2] = 2, i++    | [1, 1, 2, 2, 2, 3]        |
| 3    | 4 | 3 | 2       | 1         | true      | nums[3] = 2, i++    | [1, 1, 2, 2, 2, 3]        |
| 4    | 5 | 4 | 3       | 2         | true      | nums[4] = 3, i++    | [1, 1, 2, 2, 3, 3]        |

✅ Final Output: `i = 5`  
Modified array: `[1, 1, 2, 2, 3, _]`

---

## 🧠 Time & Space Complexity

- **Time:** O(n) — Single pass through the array
- **Space:** O(1) — In-place modification

---

## 📎 Related Topics

- Arrays
- Two Pointers
- In-place Algorithms

---

L
