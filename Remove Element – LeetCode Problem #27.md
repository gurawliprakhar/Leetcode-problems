---

## 🧹 Remove Element – LeetCode Problem #27

### 🔗 [View on LeetCode](https://leetcode.com/problems/remove-element/solutions/6895630/remove-element-by-triprakhar-svot/)

### 🧾 Problem Statement

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in-place. The order of elements may change. Then return the number of elements in `nums` which are not equal to `val`.

You must:
- Modify the array in-place so that the first `k` elements contain the elements not equal to `val`.
- Return `k`, the number of elements not equal to `val`.
- The elements beyond `k` do not matter.

---

### ✅ Example

```text
Input:  nums = [3, 2, 2, 3], val = 3
Output: 2, nums = [2, 2, _, _]

Input:  nums = [0, 1, 2, 2, 3, 0, 4, 2], val = 2
Output: 5, nums = [0, 1, 4, 0, 3, _, _, _]
```

---

### 🧠 Approach

We use the **two-pointer technique** to overwrite elements in-place:

1. Initialize a pointer `temp = 0`.
2. Traverse the array:
   - If `nums[i] != val`, assign `nums[temp] = nums[i]` and increment `temp`.
3. Return `temp` as the new length of the array.

This ensures all non-`val` elements are moved to the front.

---

### 💻 Code (Java)

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int temp = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != val) {
                nums[temp] = nums[i];
                temp++;
            }
        }
        return temp;
    }
}
```

---

### ⏱️ Complexity

| Metric            | Value |
|-------------------|--------|
| Time Complexity   | O(n)   |
| Space Complexity  | O(1)   |

---

### 🧪 Dry Run

**Input**: `nums = [0, 1, 2, 2, 3, 0, 4, 2]`, `val = 2`

| i | nums[i] | Action            | nums (partial)         | temp |
|---|---------|-------------------|--------------------------|------|
| 0 | 0       | keep → nums[0]=0  | [0, _, _, _, _, _, _, _] | 1    |
| 1 | 1       | keep → nums[1]=1  | [0, 1, _, _, _, _, _, _] | 2    |
| 2 | 2       | skip              |                          | 2    |
| 3 | 2       | skip              |                          | 2    |
| 4 | 3       | keep → nums[2]=3  | [0, 1, 3, _, _, _, _, _] | 3    |
| 5 | 0       | keep → nums[3]=0  | [0, 1, 3, 0, _, _, _, _] | 4    |
| 6 | 4       | keep → nums[4]=4  | [0, 1, 3, 0, 4, _, _, _] | 5    |
| 7 | 2       | skip              |                          | 5    |

**Output**: `5`, `nums = [0, 1, 3, 0, 4, _, _, _]`

---

### 🏁 Final Thoughts

This is a classic in-place array manipulation problem that tests your understanding of pointer logic and memory efficiency. Clean, simple, and elegant!

---

